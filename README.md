<p align="center">
  <img src="figures/sentiment/Fig_DualLevel_ConceptualFramework.png" width="85%" alt="Dual-Level Sentiment Model"/>
</p>

<h1 align="center">When the Floor Speaks, Does the Market Listen?</h1>
<h3 align="center">Employee Sentiment, Stock Performance, and the Dual-Level Quality Signal</h3>

<p align="center">
  <strong>Yulin Tian &nbsp;&bull;&nbsp; Ilia Kornietskii</strong><br/>
  Master of Science in Data Science for Business &nbsp;|&nbsp; Master of Science in Strategic Marketing Management<br/>
  BI Norwegian Business School &nbsp;|&nbsp; Supervisor: Auke Hunneman<br/>
  <em>GRA 19701 Master Thesis &nbsp;|&nbsp; June 2025</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Reviews-1.9M-blue" alt="Reviews"/>
  <img src="https://img.shields.io/badge/Firms-86-green" alt="Firms"/>
  <img src="https://img.shields.io/badge/Industries-12-orange" alt="Industries"/>
  <img src="https://img.shields.io/badge/Period-2016--2023-red" alt="Period"/>
  <img src="https://img.shields.io/badge/Words-18%2C900+-purple" alt="Words"/>
  <img src="https://img.shields.io/badge/References-49-yellow" alt="References"/>
  <img src="https://img.shields.io/badge/Python-3.12-blue" alt="Python"/>
  <img src="https://img.shields.io/badge/License-MIT-brightgreen" alt="License"/>
</p>

---

## The Story in 30 Seconds

> **Does employee voice carry information that stock markets care about?**

We analysed **1,898,445 Glassdoor employee reviews** across **86 large publicly listed firms** spanning **12 industries** over **7 years** (January 2016 to March 2023). We built a novel **Composite Sentiment Index**, ran panel regressions, portfolio sorts, a COVID-19 natural experiment, and LDA topic modelling.

**The surprise:** Employee sentiment *does* matter — but not how you would expect. Within firms, **sentiment peaks precede stock return declines** (β = −0.061, p = 0.001), because the market has already priced in employee quality before the Glassdoor score peaks. Across firms, high-sentiment companies consistently outperform — but the premium is already reflected in stock prices.

**Our contribution:** The **Dual-Level Sentiment Model** — employee voice is a structural quality marker, not a trading signal. The market is listening faster than Glassdoor can report.

---

## Key Results at a Glance

<table>
  <tr>
    <th>Hypothesis</th>
    <th>Test</th>
    <th>Key Result</th>
    <th>Verdict</th>
  </tr>
  <tr>
    <td><strong>H1:</strong> Cross-sectional quality premium</td>
    <td>Between estimator; Portfolio sort</td>
    <td>β = +0.018 (p = 0.068); Q5−Q1 = +1.1% p.a.</td>
    <td>🟡 Positive direction, not significant</td>
  </tr>
  <tr>
    <td><strong>H2:</strong> Within-firm information pricing</td>
    <td>Two-Way FE (M3); Horizon analysis</td>
    <td>β = −0.061*** (p = 0.001); −0.153* at 6m</td>
    <td>🟢 <strong>Supported (primary finding)</strong></td>
  </tr>
  <tr>
    <td><strong>H3:</strong> COVID organisational resilience</td>
    <td>Median split; Cumulative returns</td>
    <td>High ≈ +69% cum. log-return vs Low group</td>
    <td>🟡 Suggestive, economically meaningful</td>
  </tr>
  <tr>
    <td><strong>H4:</strong> Topical content across industries</td>
    <td>LDA (K=11); Industry Barometer</td>
    <td>11 interpretable topics; strong variation</td>
    <td>🟢 <strong>Supported</strong></td>
  </tr>
</table>

---

## Selected Figures

<p align="center">
  <img src="figures/sentiment/Fig4.10_PanelRegression_CoeffPlot.png" width="48%" alt="Panel Regression"/>
  &nbsp;&nbsp;
  <img src="figures/sentiment/Fig4.14_HorizonAnalysis.png" width="48%" alt="Horizon Analysis"/>
</p>
<p align="center"><em>Left: Panel regression coefficient across four model specifications. Right: The negative effect strengthens at longer horizons (1m → 3m → 6m).</em></p>

<p align="center">
  <img src="figures/sentiment/Fig4.17_COVIDResilience_HighLowSentiment.png" width="48%" alt="COVID Resilience"/>
  &nbsp;&nbsp;
  <img src="figures/topic_modelling/Fig5.13_IndustryBarometer_Heatmap.png" width="48%" alt="Industry Barometer"/>
</p>
<p align="center"><em>Left: COVID-19 resilience — high-sentiment firms recovered faster. Right: Industry Barometer heatmap across 12 industries.</em></p>

---

## Repository Structure

```
📦 thesis-employee-sentiment-stock-performance/
│
├── 📄 README.md                      ← You are here
├── 📄 LICENSE                        ← MIT License
├── 📄 .gitignore
│
├── 📁 data/
│   ├── 📁 0_original/                ← Raw Glassdoor data (large files excluded)
│   ├── 📁 1_preparation/             ← Intermediate processing files
│   └── 📁 2_analysis/                ← Final datasets for analysis
│       ├── monthly_panel.csv         ← 7,482 firm-month panel (main regression data)
│       ├── vader_scores_cache.csv.zip← VADER sentiment scores (1.9M reviews)
│       └── lda_coherence_scores.csv  ← LDA topic coherence results
│
├── 📁 notebooks/                     ← 5 Jupyter notebooks (full pipeline)
│   ├── 1_Data_Availability_Detection.ipynb
│   ├── 2_Dataset_Finalisation.ipynb
│   ├── 3_EDA_Overview.ipynb
│   ├── 4_Sentiment_StockPrice.ipynb  ← Primary analysis (Part I: "Feel")
│   └── 5_TopicModelling_Barometer.ipynb  ← Topic analysis (Part II: "Say")
│
├── 📁 figures/
│   ├── 📁 eda/                       ← 18 exploratory data analysis figures
│   ├── 📁 sentiment/                 ← 31 sentiment & stock price figures
│   └── 📁 topic_modelling/           ← 21 topic modelling figures
│
└── 📁 docs/
    └── Thesis_Presentation.pptx      ← Summary presentation slides
```

---

## Analytical Pipeline

The thesis follows a two-strand design — **"What Employees Feel"** and **"What Employees Say"**:

```
┌─────────────────────────────────────────────────────────────────────┐
│                        DATA PIPELINE                                │
│                                                                     │
│  Glassdoor Reviews ──→ NB1: Detection ──→ NB2: Finalisation        │
│  (raw HTML/CSV)        (87 firms)          (86 firms, 1.9M rows)   │
│                                                                     │
│  Stock Prices ─────────────────────────────→ Monthly log-returns    │
└─────────────────┬───────────────────────────────────┬───────────────┘
                  │                                   │
    ┌─────────────▼──────────────┐     ┌──────────────▼──────────────┐
    │  PART I: "FEEL"            │     │  PART II: "SAY"             │
    │  NB3: EDA Overview         │     │  NB5: Topic Modelling       │
    │  NB4: Sentiment & Stock    │     │       LDA (K=11)            │
    │       Composite Index      │     │       Industry Barometer    │
    │       Panel Regression     │     │       Firm Competitor Map   │
    │       M1→M4 (Pooled→FE)   │     │       Sentiment-Topic       │
    │       Granger Causality    │     │       Bridge                │
    │       Portfolio Sort       │     │                             │
    │       COVID Resilience     │     │                             │
    └─────────────┬──────────────┘     └──────────────┬──────────────┘
                  │                                   │
                  └──────────┬────────────────────────┘
                             │
              ┌──────────────▼──────────────────┐
              │  DUAL-LEVEL SENTIMENT MODEL     │
              │                                 │
              │  Cross-sectional: quality marker │
              │  Within-firm: mean reversion     │
              │  Crisis: resilience proxy        │
              │  Topics: strategic intelligence  │
              └─────────────────────────────────┘
```

---

## Methodology Highlights

| Component | Approach | Key Detail |
|-----------|----------|------------|
| **Composite Index** | Two-tier weighted score | Tier 1 (60%): rating, recommend, CEO, outlook. Tier 2 (40%): 5 sub-ratings |
| **NLP Sentiment** | VADER (Hutto & Gilbert, 2014) | Applied separately to pros and cons text (1.9M reviews) |
| **Panel Regression** | Four specifications | M1: Pooled OLS → M2: Firm FE → M3: Two-Way FE → M4: +Text control |
| **Robustness** | 8 supplementary tests | Granger, reverse causality, portfolio sort, horizon, COVID, Δsentiment |
| **Topic Modelling** | LDA (Blei et al., 2003) | K=11 for both pros and cons; coherence-optimised |
| **Visualisation** | 70 publication-quality figures | Consistent style (DejaVu Serif, 300 DPI, industry colour palette) |

---

## Dataset Overview

| Dimension | Value |
|-----------|-------|
| Total employee reviews | **1,898,445** |
| Firms | **86** (large, publicly listed, US) |
| Industries | **12** |
| Study period | **January 2016 – March 2023** (87 months) |
| Panel observations | **7,482** firm-month (≥5 reviews threshold) |
| Review fields | Rating, 5 sub-ratings, Recommend, CEO Approval, Outlook, Pros text, Cons text |
| Stock data | Monthly closing prices → log-returns |

> **Note:** The full dataset (`Thesis_Dataset_Final.csv`, ~400MB) exceeds GitHub's file size limit and is not included. The `monthly_panel.csv` used for all regressions is included. See `data/` folder READMEs for reproduction instructions.

---

## How to Reproduce

### Requirements

```bash
Python 3.12
pip install pandas numpy matplotlib seaborn scipy statsmodels linearmodels
pip install nltk gensim wordcloud pyLDAvis tqdm
pip install jupyter
```

### Running the Notebooks

```bash
# Clone the repository
git clone https://github.com/YOUR_USERNAME/thesis-employee-sentiment-stock-performance.git
cd thesis-employee-sentiment-stock-performance

# Run notebooks in order
jupyter notebook notebooks/
```

1. **Notebook 1** — Data availability detection (requires original dataset)
2. **Notebook 2** — Dataset finalisation (requires original dataset)
3. **Notebook 3** — EDA overview (requires `Thesis_Dataset_Final.csv`)
4. **Notebook 4** — Sentiment & stock price analysis (requires final dataset + stock prices)
5. **Notebook 5** — Topic modelling & barometer (requires final dataset + VADER cache)

> Notebooks 3–5 can run independently if you have the final dataset. Notebooks 4–5 cache intermediate results (VADER scores, coherence scores) for efficiency.

---

## Citation

If you use this work, please cite:

```
Tian, Y., & Kornietskii, I. (2025). When the floor speaks, does the market listen?
Employee sentiment, stock performance, and the dual-level quality signal
[Master's thesis, BI Norwegian Business School].
```

---

## Authors

| | Name | Programme | Contact |
|--|------|-----------|---------|
| 🎓 | **Yulin Tian** | MSc Data Science for Business | BI Norwegian Business School |
| 🎓 | **Ilia Kornietskii** | MSc Strategic Marketing Management | BI Norwegian Business School |
| 👨‍🏫 | **Auke Hunneman** | Supervisor | Associate Professor, BI |

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

<p align="center">
  <em>"What employees feel and say matters — not because it predicts next month's stock return, but because it reveals the quality of the organisation beneath the financial statements."</em>
</p>
