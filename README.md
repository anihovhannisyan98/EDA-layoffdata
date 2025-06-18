# World Layoffs EDA Project

Welcome to the World Layoffs EDA project! This repository contains SQL queries, analysis, and insights from exploratory data analysis (EDA) performed on a global layoffs dataset. The goal is to uncover trends, patterns, and outliers in recent layoff events across companies, industries, and countries.

---

## 📊 Project Overview

This project explores a dataset of company layoffs, including details such as:

- Company name
- Location and country
- Industry
- Number and percentage of employees laid off
- Date of layoff
- Company stage (e.g., Post-IPO, Series B)
- Funds raised

The EDA process is designed to answer key questions, spot trends, and highlight notable events, such as companies that laid off their entire workforce, the largest single-day layoffs, and industry or country-level impacts.

---

## 🗂️ Dataset

- Source: layoffs.csv
- Columns: company, location, industry, total_laid_off, percentage_laid_off, date, stage, country, funds_raised_millions
- Sample Data:

| company    | location        | industry     | total_laid_off | percentage_laid_off | date      | stage     | country      | funds_raised_millions |
|------------|----------------|--------------|----------------|---------------------|-----------|-----------|--------------|-----------------------|
| Atlassian  | Sydney         | Other        | 500            | 0.05                | 3/6/2023  | Post-IPO  | Australia    | 210                   |
| SiriusXM   | New York City  | Media        | 475            | 0.08                | 3/6/2023  | Post-IPO  | United States| 525                   |

---

## 🔍 EDA Highlights

### Simple Exploration

- Max Layoffs: Find the largest single layoff event.
- Layoff Percentage: Identify companies that laid off 100% of their staff (often startups that shut down).
- Funds Raised: See which failed companies had raised the most capital.

### Aggregate Analysis

- Top Companies: Companies with the most total layoffs (single event and cumulative).
- By Location/Country: Cities and countries with the highest layoffs.
- By Year: Layoff trends over time.
- By Industry/Stage: Which sectors and company stages were most affected.

### Advanced Analysis

- Top Companies per Year: Using window functions to rank companies by layoffs each year.
- Rolling Layoffs: Calculate rolling monthly totals to visualize layoff waves.

---

## 🧑‍💻 Example SQL Queries
SQL

-- Largest single layoff event
SELECT MAX(total_laid_off)
FROM world_layoffs.layoffs_staging2;

-- Companies that laid off 100% of their staff
SELECT *
FROM world_layoffs.layoffs_staging2
WHERE percentage_laid_off = 1
ORDER BY funds_raised_millions DESC;

-- Total layoffs by industry
SELECT industry, SUM(total_laid_off)
FROM world_layoffs.layoffs_staging2
GROUP BY industry
ORDER BY 2 DESC;
---

## 📈 Insights & Observations

- Several startups laid off their entire workforce, often after raising significant venture capital.
- The largest layoffs were concentrated in tech, finance, and media sectors.
- Layoff waves often corresponded with global economic events and funding slowdowns.
- Some well-funded companies (e.g., Quibi) still failed, illustrating that high capital does not guarantee survival.

---

## 🚀 Getting Started

1. Clone this repo.
2. Load the layoffs.csv dataset into your SQL environment.
3. Run the provided SQL queries to reproduce the analysis or adapt them for deeper exploration.

---

## 🤝 Contributions

Feel free to fork, open issues, or submit pull requests with new queries, visualizations, or insights!

---

## 📄 License

This project is open-source and free to use under the MIT License.

---

## 📬 Contact

For questions or collaboration, please open an issue or reach out via GitHub.

---

Happy exploring!
