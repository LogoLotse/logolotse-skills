---
name: Logopädie-Skills
description: "DLV-Research und Produktableitung für LogoLotse und Schullogopädie. Nutze diesen Skill bei Produktfragen, PRDs, User Stories, Feature-Spezifikationen, Therapie-Workflows, Berichtswesen, Datenschutz, Backlog-Priorisierung und Strategie-Fragen rund um LogoLotse und Schullogopädie Deutschschweiz. Auch anwenden bei Fragen zu DLVaktuell-Publikationen, DLV-Positionspapieren, interdisziplinärer Zusammenarbeit, Wartelisten, Ressourcenplanung und kantonaler Konfigurierbarkeit. Lieber einmal zu viel als zu wenig triggern."
---

# Logopädie-Skills

Dieser Skill hilft dabei:

- bei Produktfragen gezielt DLV-Wissen abzurufen,
- bei PRDs automatisch passende Fachquellen einzubeziehen,
- regelmässig neue DLV-Ausgaben zu prüfen,
- Backlog-Ideen aus Fachartikeln abzuleiten,
- LogoLotse stärker an der echten Zielgruppenrealität auszurichten.

# Skill: DLV-Research und Produktableitung für Schullogopädie

## Zweck

Dieser Skill befähigt die Logopädie-Spezialistin, DLVaktuell-Publikationen und DLV-Positionspapiere als fachliche Inspirations-, Validierungs- und Kritikquelle für LogoLotse zu nutzen.

DLVaktuell ist die Publikation des Deutschschweizer Logopädinnen- und Logopädenverbandes und damit eine wichtige Stimme der Zielgruppe.

## Primäre Quellen

* DLVaktuell-Ausgaben
* DLV-Positionspapiere
* DLV-Fachartikel mit Bezug zu:
  * Schullogopädie
  * Kindergarten
  * Schule
  * LRS / Dyslexie
  * SES / Sprachentwicklungsstörung
  * Sprachverständnis
  * Mehrsprachigkeit / DaZ
  * Unterstützte Kommunikation
  * Stottern / Redefluss
  * Aussprachestörungen
  * Berichtswesen
  * ICF
  * Datenschutz
  * Nachteilsausgleich
  * Wartelisten
  * Fachkräftemangel
  * interdisziplinäre Zusammenarbeit
  * Lehrpersonen, SHP, Eltern, Schulpsychologie

## Wann anwenden

Wende diesen Skill an bei:

* neuen Produktideen für LogoLotse
* PRDs und MVP-Konzepten
* User Stories
* Feature-Spezifikationen
* fachlichen Plausibilitätschecks
* Therapie- und Abklärungsworkflows
* Berichtswesen
* Datenschutz- und Rollenmodellen
* Eltern- und Lehrpersonenkommunikation
* schulischer Zusammenarbeit
* kantonaler Konfigurierbarkeit
* Wartelisten- und Ressourcenplanung
* Backlog-Priorisierung
* Strategie- und Positionierungsfragen

## Vorgehen

### 1. Thema einordnen

Bestimme zuerst, welches fachliche oder schulische Thema betroffen ist:

* Abklärung / Diagnostik
* Therapieplanung
* Therapiedokumentation
* Berichtswesen
* Förderplanung
* interdisziplinäre Zusammenarbeit
* Elternarbeit
* Schuladministration
* Datenschutz
* LRS
* SES
* Sprachverständnis
* Mehrsprachigkeit
* UK
* Stottern
* Aussprachestörungen
* Nachteilsausgleich
* Kindergarten
* Ressourcen / Wartelisten
* Fachkräftemangel
* KI in der Logopädie

### 2. Relevante DLV-Quellen suchen

Nutze den DLV-Relevanzkatalog in `references/dlv-catalog.yaml` (Quellen, Key-Topics, Produktimplikationen, Tags) und die extrahierten DLV-Texte.

Priorisiere Quellen mit direktem Bezug zur Schullogopädie in der Deutschschweiz.

### 3. Quelle auswerten

Extrahiere nicht nur Inhalte, sondern übersetze sie in LogoLotse-relevante Erkenntnisse:

* fachlicher Bedarf
* Pain Point im Alltag
* betroffene Rolle
* Prozessschritt
* möglicher LogoLotse-Workflow
* Datenmodell-Auswirkung
* UI-/UX-Auswirkung
* Datenschutz-/Berechtigungsimplikation
* kantonale Konfigurierbarkeit
* mögliche User Story
* MVP-Relevanz

### 4. Quellenstatus kennzeichnen

Unterscheide klar:

* „Quelle sagt“
* „Fachliche Interpretation“
* „Produktableitung“
* „Offene Frage / Annahme“

### 5. Ergebnis produktfähig machen

Leite aus der Quelle konkrete Anforderungen ab:

* funktionale Anforderungen
* nicht-funktionale Anforderungen
* User Stories
* Akzeptanzkriterien
* Risiken
* MVP-Empfehlung
* spätere Ausbaustufen

## Standard-Output

Wenn dieser Skill angewendet wird, verwende nach Möglichkeit folgende Struktur:

```markdown
## Relevante DLV-Quellen

| Quelle | Artikel / Thema | Relevanz |
|---|---|---|

## Fachlicher Kern

...

## Pain Points aus Sicht Schullogopädie

...

## Produktimplikationen für LogoLotse

...

## Mögliche User Stories

- Als Schullogopädin möchte ich ...
- Als Lehrperson möchte ich ...
- Als SHP möchte ich ...
- Als Schulleitung möchte ich ...
- Als Elternteil möchte ich ...

## Datenmodell-Auswirkungen

...

## Datenschutz / Rollenmodell

...

## MVP-Einschätzung

- Muss ins MVP:
- Später:
- Nicht sinnvoll / zu riskant:

## Offene Fragen

...
```

## Gewichtung wichtiger DLV-Quellen

Sehr hoch gewichten:

1. DLVaktuell 2/2019 – Dokumentation / Berichte
2. DLVaktuell 1/2020 – Schnittstellen
3. DLVaktuell 2/2023 – Logopädie und Psychologie (enthält: Versorgungslage im Schulbereich)
4. DLVaktuell 3/2022 – Sprachverständnis bei Schüler:innen
5. DLVaktuell 3/2024 – Selbstfürsorge im Beruf
6. DLV-Positionspapiere zu Nachteilsausgleich, LRS, Mehrsprachigkeit, Lehrplan 21, Fachkräftemangel und Kindergarten-Erfassung

## Qualitätsregeln

* Keine DLV-Quelle überinterpretieren.
* Keine einzelne Quelle als allgemeingültige Wahrheit darstellen.
* Immer prüfen, ob es kantonale Unterschiede geben kann.
* Immer prüfen, ob Datenschutz oder Rollenrechte betroffen sind.
* Immer aus Sicht der praktizierenden Schullogopädin argumentieren.
* Immer produktbezogen übersetzen: Was bedeutet das für LogoLotse?

# Modus: DLV-Inspiration für LogoLotse

## Zweck

Dieser Modus dient nicht der reinen Zusammenfassung, sondern der kreativen, aber fachlich geerdeten Produktinspiration aus DLV-Quellen.

## Auslöser

Verwende diesen Modus, wenn der Nutzer nach neuen Ideen, Backlog-Impulsen, Produktchancen oder fachlichen Trends fragt.

## Vorgehen

Wähle eine relevante DLV-Quelle oder ein DLV-Positionspapier und erzeuge daraus konkrete LogoLotse-Impulse.

## Output pro Quelle

```markdown
## Quelle

- Ausgabe / Dokument:
- Artikel / Thema:
- Relevanz für LogoLotse:

## Fachliches Signal

Was zeigt diese Quelle über den Alltag oder Bedarf der Schullogopädie?

## Drei Pain Points

1. ...
2. ...
3. ...

## Drei Produktideen

### Produktidee 1
- Kurzbeschreibung:
- Zielgruppe:
- Nutzen:
- MVP-tauglich: ja/nein
- Risiken:

### Produktidee 2
...

### Produktidee 3
...

## Zwei User Stories

- Als Schullogopädin möchte ich ..., damit ...
- Als Lehrperson / SHP / Elternteil / Schulleitung möchte ich ..., damit ...

## Eine Hypothese für Nutzerinterviews

„Wir glauben, dass ...“

## Eine MVP-Entscheidung

- Muss ins MVP:
- Später:
- Nicht verfolgen:
```

## Qualitätsanspruch

Produktideen müssen:

* im Schulalltag plausibel sein
* Zeit sparen oder Koordination verbessern
* fachlich korrekt sein
* Datenschutz und Rollen berücksichtigen
* kantonale Unterschiede nicht ignorieren

## DLV-Quellenkatalog

Der vollständige kuratierte Quellenkatalog (DLVaktuell-Ausgaben, Positionspapiere, Key-Topics, Produktimplikationen, Tags) ist in `references/dlv-catalog.yaml` abgelegt.

Lese diese Datei, wenn du gezielt nach DLV-Quellen zu einem bestimmten Thema suchst oder die Produktimplikationen einer Ausgabe abrufen möchtest.
