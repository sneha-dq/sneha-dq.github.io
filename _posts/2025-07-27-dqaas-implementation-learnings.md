---
title: "Building DQaaS: Data Quality as a Service using Great Expectations + Flask"
date: 2025-07-27
author: Sneha Shrivastav
description: Learn how to turn Great Expectations into a Python-based DQaaS with Flask, enabling reusable, automated data quality validation.
categories: [data quality]
tags: [data quality, great expectations, flask, dqaas, python, dataops]
---


I've recently been working on building a **data quality validation framework** that’s flexible, callable, and lightweight — something that doesn’t rely too heavily on manual CLI commands or notebooks.

The goal was simple: **DQaaS** (Data Quality as a Service) using **Great Expectations** and **Flask**, coded from scratch.

And let me be honest — while GE is powerful, it wasn’t always straightforward.

---

## 💭 Why I Started This

Data quality isn’t a one-time validation anymore. I needed something that:

- Could validate **any CSV** dynamically
- Didn’t require me to reconfigure GE through CLI every time
- Worked like a **service** — callable with parameters
- Could scale later to cron jobs, Airflow, or even trigger via other apps

---

## ⚙️ The Stack I Used

- Python 3.12
- Great Expectations (GE) 1.5.6
- Flask
- VS Code + GitHub

---

## 📁 Project Structure

```
dqaas-project/
├── app.py                    # Flask API for validation
├── run_validation.py         # Core logic with GE
├── data/
│   └── employees.csv         # Sample file
├── gx/                       # Great Expectations context dir
├── requirements.txt
└── README.md
```

---

## 🛠️ Challenges I Faced

I faced quite a few bumps while setting this up:

- **GE CLI didn’t install correctly** at first. I had to manually downgrade and reinstall to get `great_expectations` CLI to work inside venv.
- The **default `great_expectations` folder** was sometimes missing — GE started using `gx/` in newer versions.
- Running validations via code required some digging — the docs focused more on CLI or notebooks.
- At one point, my **suite files just vanished**. I had to recreate them using `suite.new()` and manage everything in code to avoid such surprises.
- The **`RuntimeBatchRequest` vs `BatchRequest`** confusion was real. I learned to wrap my runtime CSV inputs into the right batch structure.
- Untracked folders like `gx/uncommitted` didn’t show up in Git — turns out `.gitignore` hides them by default (makes sense).

Each hurdle made the final version much more solid.

---

## ✅ What It Does Now

- Accepts a CSV path via an API call
- Loads the data dynamically using a GE runtime batch
- Applies expectation suite (in code)
- Saves it and runs a checkpoint
- Returns success/failure in API response
- Lets you open the Data Docs HTML in browser

---

## 🧠 Example Expectations

```python
validator.expect_column_to_exist("employee_id")
validator.expect_column_values_to_not_be_null("employee_id")
validator.expect_column_values_to_be_unique("employee_id")
validator.expect_column_values_to_be_between("age", min_value=20, max_value=60)
```

---

## 🔁 Running the API

Start the Flask app:

```bash
python app.py
```

Call the validation service:

```bash
curl -X POST http://127.0.0.1:5000/validate      -H "Content-Type: application/json"      -d '{"file_path": "data/employees.csv", "suite_name": "employees_suite"}'
```

Output:

```json
{
  "success": true,
  "message": "Validation completed",
  "data_docs_url": "gx/uncommitted/data_docs/local_site/index.html"
}
```

Then just open the link and view the interactive validation report.

---

## 🔭 What’s Next

- [x] DQaC with GE — done!
- [x] Flask API to wrap it — done!
- [ ] Auto-generate expectations from profiling
- [ ] Cron job or Airflow DAG to schedule it
- [ ] Unit tests for core validation logic
- [ ] Publish Data Docs to GitHub Pages

---

## 🙋‍♀️ About Me

I'm **Sneha Shrivastav**, a data quality architect focused on clean, reusable, automatable solutions in modern data platforms.

📌 [GitHub](https://github.com/sneha-dq)  
📘 [Blog](https://sneha-dq.github.io)

---

## ✨ Final Thoughts

If you've been running your DQ checks manually or tied to notebooks/CLI, this kind of service unlocks flexibility. It’s easy to plug into pipelines, CI jobs, or just call when needed.

**This is how DQaC becomes DQaaS** — by wrapping it smartly.

Stay tuned for the next post where I auto-create expectations and build a complete pipeline! 💡
