# Photonic Chip Performance Benchmarking

**Ein Data-Science-Projekt zur Analyse synthetischer und experimenteller Daten von photonischen Rechenchips**

## Zielsetzung

- Die **demütigen Suche** nach veröffentlichten Messdaten aus Papers
Dieses Projekt entstand aus der **frustrierten Suche** nach öffentlich verfügbaren, nutzbaren Datensätzen zu photonischen integrierten Schaltkreisen (PICs).  
Während die Forschung zu photonic Matrix-Multiplikation, AI-Acceleratoren und Hybrid-Systemen boomt, sind **echte experimentelle Rohdaten eher rar**. 

Deshalb kombinieren wir:
- Die **demütigen Suche** nach veröffentlichten Messdaten aus Papers
- Die **Generierung realistischer synthetischer Daten** unter Berücksichtigung typischer photonic-Effekte (Noise, Drift, Crosstalk)
- Systematische **Analyse und Benchmarking** gegenüber elektronischen Systemen

**Ziel**: Ein reproduzierbares Framework schaffen, mit dem Data Analysts, QA-Ingenieure und Forscher photonic Hardware besser verstehen und bewerten können – auch ohne Zugang zu teurer Lab-Hardware.

## Research Questions

1. Wie stark beeinflussen typische photonic Noise-Quellen (Phase Drift, Crosstalk, Laser Intensity Noise) die **Precision** von Matrix-Multiplikationen im Vergleich zu idealen elektronischen Systemen?

2. Ab welcher Matrix-Größe / Bit-Precision wird der Vorteil photonischer Acceleratoren (Geschwindigkeit, Parallelität) durch Noise/Drift zunichte gemacht?

3. Wie gut lassen sich reale experimentelle Daten (z. B. aus Papers) mit synthetischen Modellen reproduzieren?

4. Welche Metriken (Energy-Accuracy-Tradeoff, Drift over Time, Effective Bit Precision) sind für **Hybrid photonic-electronic Systeme** am kritischsten?

## Relevante Variablen (Sketch)

- **Eingabeparameter**: Matrix-Größe, Noise Level, Drift Factor, Crosstalk Factor, Bit Precision
- **Ausgabemetriken**: MAE, RMSE, SNR (dB), Effective Bits, Energy Efficiency (simuliert)
- **Kontext-Variablen**: Matrix-Typ (random, sparse, aus realen AI-Layern), Temperatur-Einfluss (modelliert), Wellenlängen-Kanäle
- **Vergleichsgrößen**: Photonic vs. Electronic (GPU/TPU Baseline)

## Projektstruktur

- `notebooks/` → 01_Data_Collection, 02_Synthetic_Data_Generation, 03_Analysis, 04_Research_Questions
- `data/raw/` → Heruntergeladene Supplementary Materialien
- `photonic_benchmark.db` → DuckDB-Datenbank
- `src/` → wiederverwendbare Funktionen

## Amateurhafter Ansatz

Ja, das Projekt ist bewusst **amateurhaft** gestartet:  
Wir haben Papers, arXiv, GitHub und Repositorys durchsucht, nur um festzustellen, dass die meisten Autoren keine großen Rohdatensätze veröffentlichen.  
Daher ein hybrider Ansatz: So viel echte Daten wie möglich sammeln + hochwertige synthetische Daten erzeugen.

Der Datensatz bleibt bewusst **einfach und flach**.  
Alle Experimente können komfortabel in **einer einzigen CSV-Datei** oder einer einzelnen DuckDB-Tabelle gespeichert werden.

**(vorl.) Struktur der Haupttabelle** (`experiments`):

- `sample_id`
- `matrix_size`
- `noise_level`, `drift_factor`, `crosstalk_factor`
- `mae`, `rmse`, `snr_db`, `effective_bits`
- `matrix_type`, `bit_precision`
- `timestamp`, `comments`, `paper_reference`

Das reicht für die meisten Analysen vollkommen aus. Komplexere Modelle (z. B. vollständige Matrizen pro Zeile) werden nur bei Bedarf als separate Dateien gespeichert.

## Getting Started

```bash
pip install -r requirements.txt
jupyter lab# photonic-benchmark-project
