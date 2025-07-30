---
title: "Building an AI-Powered Data Quality Profiler (That Runs Locally)"
date: 2025-07-30
description: “Profiling data, explaining problems, and suggesting fixes — all offline, all in code."
categories: [data-profiler]
tags: [data-quality, ai, python, llm, data-profiler, ydata-profiling, ollama, open-source, local-llm, tinyllama, pandas]
---

## 📌 Why I Built This

Data quality checks are often manual and tedious. While tools like Great Expectations help define rules, I wanted something more exploratory — something that would:

* Profile any CSV quickly
* Explain issues in plain English
* Suggest meaningful fixes
* Run **completely offline**, using small open LLMs

That’s how this project started.

---

## ⚙️ What It Does

This tool takes a CSV file and:

1. Profiles it using [`ydata-profiling`](https://github.com/ydataai/ydata-profiling)
2. Extracts a data summary (missing values, types, etc.)
3. Uses a local LLM (via [Ollama](https://ollama.com)) to:

   * Explain data quality issues
   * Suggest potential cleaning strategies
4. Embeds that explanation into the final profiling report (HTML)

No cloud, no OpenAI key, no dependencies on heavy GPU models.

---

## 📁 Project Structure

```bash
ai-data-quality-profiler/
├── app/
│   ├── main.py                  # CLI entry point
│   ├── dq_profiler.py           # Handles profiling & report update
│   └── ai_explainer.py          # Sends summary to local LLM
├── data/                        # Input datasets
├── reports/                     # Raw profiling reports
├── docs/                        # GitHub Pages reports (with AI insights)
├── requirements.txt
└── README.md
```

---

## 🛠️ How It Works

### 1. Data Profiling

```python
from ydata_profiling import ProfileReport

report = ProfileReport(df, title="Telco Data Quality Profile", explorative=True)
report.to_file("reports/profile.html")
```

### 2. Summarize for the LLM

```python
summary = extract_summary_for_llm(df)
# Output like:
# Column: TotalCharges, Type: object, Missing: 11, Unique: 6530
```

### 3. Ask a Local Model for Insight

```python
response = ollama.chat(
    model="tinyllama",
    messages=[{"role": "user", "content": prompt}]
)
```

### 4. Embed Results into HTML Report

```python
# Uses BeautifulSoup to inject AI output
soup.body.append(<div>AI Results</div>)
```

---

## 📊 Sample Output

At the bottom of the HTML profiling report, you’ll see:

> **AI-Generated Analysis:**
> TotalCharges has missing values and is stored as a string. PhoneService has low variance...

> **Suggested Fixes:**
> Convert TotalCharges to float, fill missing with median, consider dropping low variance columns...

---

## 💻 How to Run

```bash
ollama run tinyllama
python app/main.py
xdg-open docs/index.html
```

Everything runs locally. The HTML report opens in your browser, fully self-contained.

---

## 🌱 What's Next

* Auto-apply suggested fixes
* Clean vs raw dataset comparison
* Streamlit-based UI for easier use
* Add Great Expectations validation layer

---

## 🔗 Repo

Check it out here:
[github.com/sneha-dq/ai-data-quality-profiler](https://github.com/sneha-dq/ai-data-quality-profiler)

