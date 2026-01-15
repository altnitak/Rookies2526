# 🏀 Three-Point Inflation in the NBA  
## Where is the limit?

## 1. Projektbeschreibung
In den letzten Jahrzehnten hat sich Basketball und der gesamte Spielstil in der NBA stark verändert.  
Insbesondere der Drei-Punkte-Wurf hat seit Mitte der 2010er-Jahre massiv an Bedeutung gewonnen.  
Während Teams kontinuierlich mehr Dreier pro Spiel nehmen, stellt sich die Frage, ob dieses steigende Wurfvolumen langfristig effizient bleibt oder ob ein Sättigungspunkt erreicht wird.

Unser Projekt analysiert die Entwicklung des Drei-Punkte-Wurfs mit offiziellen Daten aller NBA-Teams seit 1996/97 bis heute. Von Datenaufbereitung über statistische Tests bis hin zu einer Machine-Learning Analyse.

---

## 2. Ziel & Forschungsfrage

**Zentrale Forschungsfrage:**  
> *Wo liegt das Limit der Drei-Punkte-Inflation in der NBA und wie hat sich das Spiel geändert?*

Wir teilen hierfür unser Projekt in folgende Teilfragen:
- Wie hat sich die Anzahl der Drei-Punkte-Versuche (3PA) seit 1996 entwickelt?
- Gibt es Hinweise auf einen Effizienzverlust bei steigendem Wurfvolumen?
- Lässt sich ein struktureller Wendepunkt um 2014/15–2015/16 identifizieren?
- Ist der Drei-Punkte-Wurf im Jahr 2025/26 weiterhin ein zentraler Erfolgsfaktor für Teams?

---

## 3. Datengrundlage

- **Analyseebene:** Team × Saison  
- **Zeitraum:** 1996–2026  
- **Quellen:**
  - Historische NBA-Team-Saisondaten (1996–2024) aus einem offenen Datensatz von *OpenDataBay*  
    (Datensatz zum Analysezeitpunkt öffentlich verfügbar, inzwischen entfernt)
  - Aktuelle Saisondaten (2024/25-2025/26) per Web Scraping von öffentlich zugänglichen NBA-Teamstatistiken
- Der historische Datensatz liegt lokal vor und wurde unverändert als Ausgangspunkt der Analyse verwendet.
- **Zentrale Variablen:**
  - Drei-Punkte-Würfe: 3PA, 3PM, 3P%
  - Weitere Effizienzmaße: FG%, FT%
  - Team-Erfolg: Wins, Winning Percentage

Alle Kennzahlen werden auf **Per-Game-Basis** berechnet, um Vergleichbarkeit zwischen vollständigen und verkürzten Saisons sicherzustellen.

---

## 4. Datenaufbereitung

Die Daten wurden umfassend bereinigt und vereinheitlicht:
- Standardisierung der Saisonformate (z. B. 2015/16)
- Umgang mit fehlenden Werten in laufenden Saisons
- Berechnung statistischer Kennzahlen auf Basis der Rohdaten
  

Die ursprünglich per Web Scraping erhobenen Rohdaten wurden unmittelbar nach der Erhebung zusammengeführt und bereinigt.  
Daher liegen im Repository ausschließlich die bereinigten und gesäuberten Datensätze vor. Der ursprüngliche OpenDataBay-Datensatz liegt unverändert im Ordner `data/raw/`.

Das Ergebnis, womit schließlich auch gearbeitet wurde ist eine konsistente, lückenfreie Master-Tabelle.

---

## 5. Feature Engineering: True 3PT%

Neben der klassischen Drei-Punkte-Quote (3P%) wird eine zusätzliche Effizienzkennzahl verwendet:

**True 3PT% (Bayes-adjustiert)**  
- reduziert Verzerrungen durch kleine Stichproben
- zieht extreme Quoten kontrolliert in Richtung Ligadurchschnitt
- erlaubt robustere Vergleiche zwischen Teams und Saisons

Diese Kennzahl stellt einen methodischen Mehrwert gegenüber reinen Rohquoten dar.

---

## 6. Methodik

### 6.1 Deskriptive Analyse
- Zeitreihenanalyse von 1996 bis 2026
- Untersuchung der Entwicklung von:
  - 3PA pro Spiel
  - 3P%
  - True 3PT%
- Visuelle und statistische Identifikation eines strukturellen Wendepunkts um 2015/16

---

### 6.2 Statistische Hypothesentests

**Vergleichszeiträume:**
- Saison **2015/16** (Beginn der modernen Drei-Punkte-Ära)
- Saison **2025/26** (aktuelle NBA)

**Hypothesen (gerichtet):**
- **H₀:** Die durchschnittliche Drei-Punkte-Quote (3P%) in 2025/26 ist gleich oder höher als in 2015/16.
- **H₁:** Die durchschnittliche Drei-Punkte-Quote (3P%) in 2025/26 ist niedriger als in 2015/16.

**Testverfahren:**
- Zwei-Stichproben-t-Test nach Welch (robust gegenüber ungleichen Varianzen)
- Signifikanzniveau: α = 0,05
- Tests sowohl für klassische 3P% als auch für True 3PT%

Zur Ergänzung der Signifikanztests wird die Effektgröße (Cohen’s d) berechnet.

---

### 6.3 Machine Learning (ergänzende Analyse)

Zur Bewertung der praktischen Relevanz des Drei-Punkte-Wurfs für den Teamerfolg werden Regressions- und ML-Modelle eingesetzt.

- **Zielvariable:** Wins / Winning Percentage  
- **Features:**
  - 3PA pro Spiel
  - 3P%
  - True 3PT%
  - FG%
  - FT%

**Modelle:**
- Lineare Regression (Baseline)
- Nichtlineares Modell (z. B. Random Forest)

Ziel ist nicht Vorhersageoptimierung, sondern die Analyse relativer Feature-Bedeutungen.

---

## 7. Limitationen

- Die Saison 2025/26 ist zum Analysezeitpunkt noch nicht vollständig abgeschlossen.
- Die Analyse erfolgt auf Team-Ebene und berücksichtigt keine spielerspezifischen Effekte.
- Kontextfaktoren wie Shot Difficulty oder defensive Adjustments können nur indirekt abgebildet werden.

---

## 8. Projektstruktur

```text
Rookies2526/
├── data/
│   ├── raw/
│   └── processed/
├── notebooks/
│   ├── 01_data_audit.ipynb
│   ├── 02_trend_analysis.ipynb
│   ├── 03_true_3pt.ipynb
│   ├── 04_hypothesis_tests.ipynb
│   └── 05_modeling.ipynb
├── reports/
│   └── figures/
├── slides/
├── requirements.txt
├── .gitignore
└── README.md


