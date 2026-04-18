# Google-Colab-Projects
# 📊 Personal Habits & Mood Analysis

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2.0%2B-150458?logo=pandas&logoColor=white)
![Matplotlib](https://img.shields.io/badge/Matplotlib-3.7%2B-orange)
![Seaborn](https://img.shields.io/badge/Seaborn-0.12%2B-4c72b0)
![Google Colab](https://img.shields.io/badge/Google%20Colab-ready-F9AB00?logo=googlecolab&logoColor=white)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)
![License](https://img.shields.io/badge/License-MIT-green)

> An end-to-end **Exploratory Data Analysis (EDA)** project built in Google Colab that tracks daily personal habits — sleep, exercise, journaling, reading, screen time and spending — and identifies which ones have the strongest statistical relationship with daily mood.

---

## 📌 Table of Contents

- [Project Overview](#-project-overview)
- [Dataset](#-dataset)
- [Project Structure](#-project-structure)
- [Notebook Walkthrough](#-notebook-walkthrough)
- [Key Visualizations](#-key-visualizations)
- [Key Findings](#-key-findings)
- [How to Run](#-how-to-run)
- [Tech Stack](#-tech-stack)
- [FAQ](#-faq)
- [Author](#-author)

---

## 🔍 Project Overview

This project answers a simple but meaningful question:

> **Which daily habits are most associated with feeling good?**

Using 90 days of personal habit data sourced from Kaggle, this notebook walks through the full data analytics pipeline:

```
Raw CSV  →  Data Loading  →  EDA  →  Cleaning  →  Analysis  →  Visualizations  →  Insights
```

It is written to be fully understandable by someone with no prior programming or data science experience — every code block is commented in plain language — while also being technically rigorous enough for a professional technical interview.

---

## 📂 Dataset

| Field | Description |
|---|---|
| **Source** | [Kaggle — Daily Habits & Mood Dataset](https://www.kaggle.com/) |
| **Format** | CSV |
| **Rows** | 90 (one per day) |
| **Columns** | 8 |
| **Time range** | ~3 months of daily observations |

### Columns

| Original column name | Renamed to | Type | Description |
|---|---|---|---|
| `Date` | index | datetime | Date of observation |
| `Sleep_Hours` | `sleep_h` | float | Hours of sleep |
| `Workout_Duration_Min` | `workout_min` | float | Minutes of exercise (0 if none) |
| `Journaling (Y/N)` | `journaling` | int (0/1) | Whether journaling was done |
| `Reading_Min` | `reading_min` | float | Minutes spent reading |
| `Screen_Time_Hours` | `screen_h` | float | Hours of screen time |
| `Daily_Expense (RM)` | `expense_rm` | float | Daily spending in Malaysian Ringgit |
| `Mood_Score (1-10)` | `mood` | float | Self-reported mood score |

> **Note:** If the CSV file is unavailable, the notebook includes a synthetic data generator using `numpy` that replicates the same schema and statistical properties.

---

## 📁 Project Structure

```
personal-habits-analysis/
│
├── analisis_habitos_personales.py   # Main analysis script (all 9 cells)
├── README.md                        # This file
│
├── outputs/                         # Auto-generated when notebook runs
│   ├── grafico_evolucion_temporal.png
│   ├── grafico_distribuciones.png
│   ├── grafico_humor_semana.png
│   ├── grafico_correlaciones_heatmap.png
│   ├── grafico_scatter_habitos_humor.png
│   └── grafico_tendencia_humor.png
│
└── data/
    └── habits.csv                   # Source dataset (from Kaggle)
```

---

## 🗂 Notebook Walkthrough

The notebook is divided into **10 clearly separated cells**, each with a specific role:

### 1. Library imports
Imports `pandas`, `numpy`, `matplotlib`, and `seaborn`. Configures global plot styling via `rcParams` so all charts share a consistent look without repeating setup code.

### 2. Graphic setting
Using plt.rcParams and sns.set_palette, so all graphics would not have and edge but an specifit size.

### 3. Data loading
Offers **4 loading options** depending on the environment:
- **Option A** — Manual upload via Google Colab file picker
- **Option B** — Mount and read from Google Drive
- **Option C** — Local path (for VS Code users)
- **Option D** — Synthetic data generator (no file needed, uses `numpy.random`)

### 4. Exploratory Data Analysis (EDA)
First contact with the data. Uses:
- `df.head()` — inspect first 5 rows
- `df.info()` — column types and non-null counts
- `df.describe()` — descriptive statistics (mean, std, min, max, quartiles)
- `df.isnull().sum()` — null value audit per column

### 5. Data cleaning & preparation
Transforms raw data into analysis-ready format:
- Converts `Date` column from `object` to `datetime64`
- Sets `Date` as the DataFrame index (enables time-series operations)
- Renames columns to short, clean, lowercase names (avoids errors with spaces and special characters)
- Encodes `Journaling (Y/N)` → `0/1` (binary encoding for numeric analysis)
- Engineers a new feature: `weekday` (0=Monday, 6=Sunday)
- Fills missing values with column means (`fillna(df.mean())`)

### 6. Statistical analysis
Computes and prints per-variable summaries (mean, median, min, max, std). Also calculates:
- Percentage of days with journaling
- Percentage of days with exercise
- Average mood broken down by day of the week (with ASCII bar chart)

### 7. Visualizations
Produces three charts saved as `.png`:
1. **Multi-panel time series** — all 6 habit variables plotted over time with a 7-day rolling mean overlay
2. **Distribution histograms** — `sns.histplot` with KDE curve and mean line per variable
3. **Bar chart** — average mood by day of the week (weekdays in blue, weekends in red)

### 8. Correlation analysis
Computes the Pearson correlation matrix and produces two charts:
1. **Heatmap** — lower triangle only (upper is redundant by symmetry), `RdYlBu` palette, values annotated
2. **Scatter plots with regression lines** — each habit vs mood, with `r` coefficient in the title

### 9. Rolling averages & trend analysis
Overlays three layers on a single mood chart:
- Raw daily values (low opacity)
- 7-day rolling mean (short-term trend)
- 30-day rolling mean (long-term trend)
- ±1 standard deviation band (shows volatility)

### 10. Conclusions & insights
Programmatically extracts and prints:
- All correlations with mood sorted descending
- Best and worst day of the week for mood
- Mood difference on exercise vs non-exercise days
- Mood difference on journaling vs non-journaling days
- Plain-language recommendations with a caution about correlation ≠ causation

---

## 📈 Key Visualizations

| Chart | What it shows |
|---|---|
| Time series + rolling mean | How habits evolve over 90 days |
| Histograms + KDE | Distribution shape of each variable |
| Bar chart by weekday | Which days of the week have better mood |
| Correlation heatmap | All pairwise relationships at a glance |
| Scatter + regression | Direction and strength of each habit-mood link |
| Trend bands | Short vs long-term mood trajectory |

---

## 🔑 Key Findings

> Results will vary depending on the actual dataset used. The following are typical patterns observed with the synthetic data generator.

- **Sleep** shows a moderate positive correlation with mood — more sleep tends to associate with higher scores.
- **Exercise** days show measurably higher average mood than rest days.
- **Screen time** shows a negative correlation — higher screen time associates with lower mood scores.
- **Journaling** days average slightly higher mood than non-journaling days.
- **Day of the week** patterns exist — mood tends to dip mid-week and recover toward the weekend.

> ⚠️ **Important:** All findings are correlational, not causal. Establishing causation requires controlled experiments. Correlation only tells us that two variables move together — not that one causes the other.

---

## ▶️ How to Run

### Option 1 — Google Colab (recommended)

1. Open [Google Colab](https://colab.research.google.com/)
2. Go to `File → Upload notebook` and upload `analisis_habitos_personales.py`
   - Or paste each cell manually into a new notebook
3. Upload your `habits.csv` file when prompted (Cell 2, Option A)
   - Or skip this and use the built-in synthetic data generator (Option D)
4. Go to `Runtime → Run all` to execute all cells in order

> ✅ **Best practice:** Always use `Runtime → Restart session and run all` before presenting or submitting. This ensures the notebook is fully reproducible from top to bottom.

### Option 2 — VS Code / local environment

```bash
# 1. Clone or download the repository
git clone https://github.com/your-username/personal-habits-analysis.git
cd personal-habits-analysis

# 2. Create and activate a virtual environment
python -m venv venv
source venv/bin/activate        # macOS/Linux
venv\Scripts\activate           # Windows

# 3. Install dependencies
pip install pandas numpy matplotlib seaborn

# 4. Run the script
python analisis_habitos_personales.py
```

---

## 🛠 Tech Stack

| Library | Version | Purpose |
|---|---|---|
| `pandas` | 2.0+ | Data loading, cleaning, transformation, grouping |
| `numpy` | 1.24+ | Numerical operations, synthetic data generation |
| `matplotlib` | 3.7+ | Base plotting engine, figure layout, date formatting |
| `seaborn` | 0.12+ | Statistical visualizations (heatmap, histplot, regplot) |
| Python | 3.10+ | Core language |
| Google Colab | — | Cloud notebook environment |

---

## ❓ FAQ

**Q: Can I use this with my own data instead of the Kaggle dataset?**
> Yes. As long as your CSV has the same column names, it will work without modification. If your columns are named differently, update the `rename()` dictionary in Cell 4.

**Q: What does the synthetic data generator do exactly?**
> It uses `numpy.random` with a fixed seed (`seed=42`) to generate 90 days of realistic-looking habit data. Sleep follows a normal distribution centered at 7 hours. Mood is constructed as a weighted combination of sleep and exercise values plus noise, which is why correlations appear in the output.

**Q: Why is `seed=42` used?**
> Setting a random seed makes results reproducible every time the code runs, it generates the exact same "random" numbers. This is standard practice in data science and machine learning to ensure experiments can be replicated.

**Q: Does correlation mean causation here?**
> No. A correlation of r=0.4 between sleep and mood means they tend to move together, but does not prove that sleeping more *causes* better mood. There could be a third variable (e.g. stress level) affecting both. Establishing causation requires a randomised controlled experiment.

**Q: Why use a rolling mean instead of plotting raw values?**
> Raw daily values are noisy a single bad day creates a spike that obscures the overall trend. A 7-day rolling mean smooths out that noise and reveals the underlying direction, the same technique used in financial charts for stock prices.

**Q: Why is the upper triangle of the heatmap hidden?**
> A correlation matrix is symmetric: the correlation between A and B is identical to the correlation between B and A. Showing both halves doubles the visual information without adding new content. Masking the upper triangle (`np.triu`) keeps the chart clean and easier to read.

---

## 👤 Author

**EstebanUMBJ**
- GitHub: https://github.com/EstebanUMBJ

---

## 📄 License

This project is licensed under the MIT License — feel free to use, modify and distribute it with attribution.

---

*Built as part of a Data Analytics learning portfolio. Dataset sourced from Kaggle.*
