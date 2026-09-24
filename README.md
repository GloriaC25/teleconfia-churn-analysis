# teleconfia-churn-analysis

Churn-Analyse für einen Telekommunikationsanbieter in Florida — Python, SQL & logistische Regression

## Kontext

Teleconfia, ein Telekommunikationsanbieter, testet den Markteintritt in Florida. Neue Kundinnen und Kunden erhielten ein Jahr lang vergünstigte Konditionen — nach Ablauf dieser Frist wanderten viele von ihnen ab (Churn). Ziel dieser Analyse ist es, die Stadtgebiete und individuellen Kunden zu identifizieren, die am stärksten gefährdet sind, um zwei gezielte Marketingkampagnen zu ermöglichen: eine Plakatkampagne für besonders betroffene Stadtgebiete und eine individuelle Kontaktaufnahme mit abwanderungsgefährdeten Kundinnen und Kunden.

## Fragestellung

- Welche vier Stadtgebiete weisen die höchste Kundenabwanderung auf?
- Welche kategorische Datenreihe eignet sich, um individuell gefährdete Kunden zu identifizieren?
- Welche ganzzahlige Datenreihe eignet sich dafür, und wo liegt ein sinnvoller Grenzwert?
- Welche Fließkomma-Datenreihe ergänzt diese Auswahl — bestimmt über eine logistische Regression?
- Wie lassen sich die Ergebnisse visualisieren und in konkrete Empfehlungen übersetzen?

## Vorgehen

1. **Einlesen der Daten**: Verbindung zur SQLite-Datenbank über SQLAlchemy, SQL-Abfragen zur Kombination der Tabellen `churn_data` und `cities`
2. **Überprüfung & Reinigung**: Umgang mit fehlenden Werten, Entfernen redundanter Spalten, Korrektur unplausibler Werte, Typkonvertierung
3. **Explorative Analyse**: Berechnung der Abwanderungsrate je Stadtgebiet
4. **Segmentierung**: Untersuchung dreier möglicher Risikosignale — eine kategorische Variable, eine ganzzahlige Variable mit naheliegendem Grenzwert, und eine Fließkomma-Variable
5. **Logistische Regression**: Bestimmung eines datenbasierten Grenzwerts für die Fließkomma-Variable
6. **Visualisierung & Empfehlungen**: Aufbereitung der Ergebnisse für zwei konkrete Marketingkampagnen

## Wichtigste Erkenntnisse

**Stadtgebiete mit höchster Abwanderung** (Gesamtdurchschnitt: 14,5 %):
Jacksonville (29,8 %), Orlando1 (23,7 %), Cape Coral (21,8 %), Orlando2 (19,1 %)

**Drei Risikosignale für individuelle Kunden:**

| Signal | Kategorie | Ergebnis | Gefährdete aktive Kunden |
|---|---|---|---|
| International Plan | kategorisch | 42,4 % Churn (vs. 11,5 % ohne Plan) | 186 |
| Kundenservice-Anrufe | ganzzahlig | Sprunghafter Anstieg ab 4 Anrufen | 129 |
| Tagesminuten | Fließkomma (log. Regression) | Grenzwert bei 350,74 Minuten | 1 |

## Empfehlungen

1. **Kampagne 1 (Plakate)**: Fokus auf die vier identifizierten Stadtgebiete, ergänzt um eine Prüfung möglicher Ursachen (Netzqualität, Wettbewerb, Service vor Ort)
2. **Kampagne 2 (individuelle Ansprache)**: Priorisierte Kontaktliste basierend auf den drei Risikosignalen, mit Fokus auf Kunden mit mehreren gleichzeitigen Risikofaktoren
3. **Maßnahmen**: Tarifoptimierung und bessere Kommunikation beim International Plan, Beschwerdemanagement bei häufigen Service-Anrufen, proaktive Ansprache von Heavy-Usern

## Limitationen

- Die Daten decken nur ein Jahr und ausschließlich das Pilotgebiet Florida ab
- Preis-, Wettbewerbs- und Netzqualitätsdaten lagen nicht vor
- Die logistische Regression basiert auf einem einzelnen Prädiktor; ein Modell mit mehreren Variablen könnte zusätzliche Einsichten liefern
- Korrelation bedeutet keine Kausalität — die identifizierten Signale sind starke Indikatoren, nicht zwingend Ursachen der Abwanderung

## Tech Stack

Python (pandas, matplotlib, statsmodels) · SQL · SQLAlchemy · SQLite · Jupyter Notebook

## Struktur

```
teleconfia-churn-analysis/
├── data/
│   └── telco_churn.db
├── telco_churn_analysis.ipynb
└── README.md
```
