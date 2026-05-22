---
name: logolotse-agent-optimizer
description: Prüft und optimiert das LogoLotse-Agenten-Team, indem aktuelle KI-Modelle aller Anbieter (Anthropic, OpenAI, Google, Mistral, xAI, Open-Weights) per Internetrecherche analysiert und gegen die Aufgaben jedes Agenten bewertet werden. Resultat sind konkrete Änderungsvorschläge zu Modellwahl, Aufgabenbeschreibung (capabilities), Heartbeat-Intervall, Skills und Budget – eingereicht über den Paperclip-Approval-Workflow. Quartalsweise zusätzlich Analyse der Organisations-Struktur (Agenten zusammenlegen, aufteilen in einfache/komplexe Anteile, neue Rollen, Terminate) als Empfehlung an den Board. Diesen Skill zwingend nutzen, wenn der monatliche oder vierteljährliche Team-Review ansteht, wenn ein grösseres neues Modell veröffentlicht wurde (z.B. neues Claude/GPT/Gemini/Mistral), wenn ein Agent sein Budget wiederholt überschreitet oder unterschreitet, wenn Aufgaben hängen bleiben, oder wenn jemand sagt "schau die Agenten-Aufstellung an", "sind wir noch auf den richtigen Modellen", "optimiere das Team", "check den Stack" oder ähnliches. Auch dann nutzen, wenn das genaue Wort "Optimierung" nicht fällt – der Skill soll lieber einmal zu oft als einmal zu wenig triggern.
---

# LogoLotse Agent Optimizer

Ein Skill für den CEO-Agenten (Lead-Architekt) zur periodischen Überprüfung und Optimierung des LogoLotse-Agenten-Teams in Paperclip.

## Zweck

Das KI-Modell-Ökosystem bewegt sich schnell. Was vor drei Monaten die beste Wahl war, ist heute vielleicht teuer und überholt. Gleichzeitig ändert sich der LogoLotse-Code: Agenten, die am Anfang sinnvoll waren, sind später unter- oder überfordert. Dieser Skill stellt sicher, dass das Team regelmässig und strukturiert auf den aktuellen Stand gebracht wird, statt dass Modellwahl und Konfiguration einfrieren.

## Wann diesen Skill ausführen

**Geplant:**

- Einmal pro Monat als Team-Review (erster Heartbeat nach Monatsbeginn): Modell, Capabilities, Heartbeat, Skills, Budget.
- Einmal pro Quartal ein erweiterter Review mit zusätzlicher **Organisations-Struktur-Analyse** (Zusammenlegen, Aufteilen, neue Rollen, Terminate).

**Ereignisgetrieben:**

- Grösseres Modell-Release bei einem der führenden Anbieter (neues Flaggschiff-Modell, keine Minor-Updates).
- Agent überschreitet Budget zwei Monate in Folge.
- Agent liegt drei Monate unter 30% Budgetverbrauch.
- Häufige Re-Reviews oder Korrekturen bei den Outputs eines Agenten.
- Neue kantonale Anforderung erfordert neue Fähigkeiten im Team.

## Workflow

### Schritt 1 - Ist-Zustand erfassen

Paperclip-API abfragen und für jeden Agenten festhalten:

```bash
curl -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  http://localhost:3100/api/companies/$COMPANY_ID/agents
```

Pro Agent dokumentieren:

- Rolle, Capabilities-Text, Skills, aktuelles Modell.
- Heartbeat-Intervall und Anzahl Runs letzter 30 Tage.
- Budgetverbrauch absolut und in % des Monatsbudgets.
- Anzahl abgeschlossener Tasks, Reopen-Quote, durchschnittliche Task-Dauer.
- Letzte 5 Tasks: Was war die Aufgabe, wurde sie gut gelöst?

Zusätzlich Kontext-Snapshot: `GET /api/companies/$COMPANY_ID/goals` und die aktuellen Roadmap-Ziele einsehen.

### Schritt 2 - Modell-Landschaft recherchieren

Siehe `references/model-landscape.md` für die zu prüfenden Anbieter und Benchmark-Quellen.

Grundregel: Für jede Kategorie (Frontier, Mid-Tier, Lightweight, Code-Spezialist) die aktuell beste Option pro Anbieter identifizieren und Preis/Leistung gegeneinander stellen. Recherche immer mit aktuellem Datum durchführen.

Web-Suche verwenden, nicht nur interne Annahmen. Die Trainings-Cutoffs der Agenten machen eigene Einschätzungen zur aktuellen Modell-Landschaft unzuverlässig.

**Wichtig:** Nicht nur Claude-Modelle prüfen, nur weil der CEO-Agent selbst ein Claude ist. Jeder Wechsel zu einem anderen Anbieter ist legitim, wenn er die Kriterien erfüllt.

### Schritt 3 - Jeden Agenten bewerten

Siehe `references/evaluation-matrix.md` für die Scoring-Methode.

Pro Agent vier Dimensionen prüfen:

- **Modell-Fit**: Passt das aktuelle Modell noch zur Aufgabe? Gibt es eine Option, die mindestens 15% besser auf relevantem Benchmark abschneidet oder bei gleicher Qualität mindestens 30% günstiger ist?
- **Capabilities**: Beschreibt der Text noch die tatsächliche Aufgabe? Fehlen neue Fähigkeiten? Gibt es veraltete Anforderungen?
- **Heartbeat-Intervall**:
  - Zu häufig: >30% Runs sind No-Ops (`keine neue Arbeit`) -> Intervall verlängern.
  - Zu selten: Tasks liegen >1 Heartbeat-Zyklus in `Ready` ohne Aufnahme -> Intervall verkürzen.
  - Passend: 40-70% der Runs produzieren Arbeit.
- **Skills-Array**: Sind deklarierte Skills noch aktuell? Fehlt etwas, das regelmässig gebraucht wird? Gibt es seit 60 Tagen ungenutzte Skills?

### Schritt 3.5 - Organisations-Struktur-Analyse (nur Quartals-Review)

Nur ausführen, wenn:

- Es ein Quartals-Review ist (erster Monat eines Quartals), oder
- Der Board explizit eine Strukturanalyse angefordert hat.

Siehe `references/org-structure-review.md` für die Regeln und Signal-Definitionen.

Kurzablauf:

1. Vier Signal-Typen messen: **Split**, **Merge**, **Hire**, **Terminate**.
2. Maximal **eine** Struktur-Empfehlung pro Quartal ausgeben.
3. Ergebnis ist **keine Approval-Request**, sondern eine Empfehlung im Abschnitt `Organisations-Analyse` des Vorschlagsdokuments.
4. `Keine Änderung empfohlen` ist ein valides Ergebnis.

### Schritt 4 - Anti-Churn-Regeln anwenden

1. Maximal zwei Agenten pro Review-Zyklus ändern.
2. DSG/Security-Reviewer-Rolle nie downgraden.
3. Capabilities nur ändern, wenn faktisch falsch oder unvollständig.
4. Heartbeat-Änderungen nur in 50%-Schritten.
5. Modellwechsel braucht mindestens eine aktuelle Benchmark- oder Pricing-Quelle (URL + Datum).

### Schritt 5 - Vorschlagsdokument erstellen

Format siehe `templates/proposal-template.md`.

Das Dokument enthält:

- Management-Summary (was ändert sich, was nicht, warum).
- Landschafts-Befund (was sich seit letztem Review verändert hat).
- Pro Agent: aktueller Zustand -> Vorschlag -> Begründung + Quelle.
- Geschätzter Kosteneffekt (monatlich, in USD).
- Nicht-geänderte Agenten mit Kurzbegründung.

### Schritt 6 - Governance-konformer Submit

**Der CEO-Agent ändert keine Agenten direkt.** Jede Änderung geht als Approval-Request an den Board:

```bash
curl -X POST \
  -H "Authorization: Bearer $PAPERCLIP_API_KEY" \
  -H "Content-Type: application/json" \
  http://localhost:3100/api/companies/$COMPANY_ID/approvals \
  -d '{
    "type": "update_agent",
    "requestedByAgentId": "<ceo-agent-id>",
    "payload": {
      "agentId": "<target-agent-id>",
      "changes": { ... },
      "rationale": "... mit Quellen-URL"
    }
  }'
```

Pro Änderung ein separater Approval-Request, damit der Mensch einzeln entscheiden kann.

Zusätzlich das gesamte Vorschlagsdokument als Issue/Task im CEO-Backlog ablegen, damit es im Audit-Trail erhalten bleibt.

## Was der Skill nicht macht

- Keine Agenten eigenmächtig feuern oder einstellen.
- Keine Modell-Experimente ohne Begründung.
- Keine Budget-Erhöhungen ohne Nachweis.
- Keine Inhalts-Fachentscheidungen zur Schullogopädie.

## Abschluss

Am Ende des Skill-Laufs folgende Information an den Board melden:

- Anzahl erstellter Approval-Requests.
- Erwarteter Netto-Kosteneffekt (+/- USD/Monat).
- Datum des nächsten geplanten Reviews.
- Offene Fragen, bei denen eine Entscheidung des Menschen benötigt wird.
