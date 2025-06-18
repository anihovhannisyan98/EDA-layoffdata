# EDA-layoffdata
A comprehensive exploratory data analysis of global layoffs data, revealing patterns, trends, and insights through structured SQL queries and data visualization.
> Անի:
# 📊 World Layoffs Exploratory Data Analysis

<div align="center">

![SQL](https://img.shields.io/badge/SQL-MySQL-blue)
![Data Analysis](https://img.shields.io/badge/Analysis-EDA-green)
![Status](https://img.shields.io/badge/Status-Complete-success)
![License](https://img.shields.io/badge/License-MIT-yellow)

*Comprehensive exploratory data analysis of global layoffs data revealing industry trends, patterns, and insights*

[View Analysis](#-analysis-overview) • [Quick Start](#-quick-start) • [Key Findings](#-key-findings) • [SQL Queries](#-sql-queries)

</div>

-----

## 🎯 Project Overview

This project performs an in-depth exploratory data analysis (EDA) on a comprehensive dataset of global layoffs, focusing on discovering patterns, trends, and outliers across different companies, industries, locations, and time periods. The analysis progresses from basic exploration to sophisticated analytical queries, demonstrating advanced SQL techniques and data analysis methodologies.

### 🔍 What Makes This Analysis Special

- Hypothesis-free exploration: Open-ended discovery approach to uncover hidden patterns
- Progressive complexity: Structured progression from simple queries to advanced analytics
- Real-world insights: Business-relevant findings with strategic implications
- Technical depth: Advanced SQL techniques including CTEs, window functions, and complex joins

-----

## 📈 Analysis Overview

### 📊 Dataset Information

- Source: World Layoffs Dataset (2020-2024)
- Records: 2,000+ layoff events
- Companies: 1,000+ organizations
- Time Range: 4+ years of data
- Geographic Coverage: Global scope with focus on tech hubs

### 🎨 Analysis Structure
graph TD
    A[Raw Data] --> B[Basic Exploration]
    B --> C[Data Quality Assessment]
    C --> D[Intermediate Analysis]
    D --> E[Advanced Queries]
    E --> F[Key Insights]
    
    B --> B1[Min/Max Values]
    B --> B2[Percentage Analysis]
    B --> B3[Outlier Detection]
    
    D --> D1[Company Rankings]
    D --> D2[Geographic Analysis]
    D --> D3[Industry Breakdown]
    D --> D4[Temporal Trends]
    
    E --> E1[Year-over-Year Rankings]
    E --> E2[Rolling Calculations]
    E --> E3[Time Series Analysis]

-----

## 🚀 Quick Start

### Prerequisites

- MySQL 8.0+ or compatible database
- Basic understanding of SQL
- Database client (MySQL Workbench, phpMyAdmin, etc.)

### Installation & Setup

1. Clone the repository
   
     git clone https://github.com/yourusername/layoffs-eda-analysis.git
   cd layoffs-eda-analysis
   1. Set up your database
   
     CREATE DATABASE world_layoffs;
   USE world_layoffs;
   1. Import the dataset
   
     -- Import your layoffs data into layoffs_staging2 table
   -- Ensure the table has the following structure:
   CREATE TABLE layoffs_staging2 (
       company VARCHAR(100),
       location VARCHAR(100),
       industry VARCHAR(100),
       total_laid_off INT,
       percentage_laid_off DECIMAL(3,2),
       date DATE,
       stage VARCHAR(50),
       country VARCHAR(100),
       funds_raised_millions DECIMAL(10,2)
   );
   1. Run the analysis
   
     # Execute queries in order:
   mysql -u username -p world_layoffs < queries/01_basic_exploration.sql
   mysql -u username -p world_layoffs < queries/02_intermediate_analysis.sql
   mysql -u username -p world_layoffs < queries/03_advanced_queries.sql
   
-----

## 🔍 SQL Queries

### 📁 Repository Structure
layoffs-eda-analysis/
├── 📄 README.md
├── 📁 queries/
│   ├── 🔍 01_basic_exploration.sql      # Initial data exploration
│   ├── 📊 02_intermediate_analysis.sql  # GROUP BY operations
│   └── 🚀 03_advanced_queries.sql       # CTEs & Window functions
├── 📁 data/
│   ├── 📋 layoffs_staging2.csv         # Clean dataset
│   └── 📋 data_dictionary.md           # Column descriptions
├── 📁 results/
│   ├── 📈 charts/                      # Visualization outputs
│   └── 📊 summary_reports/             # Key findings
└── 📁 docs/
    ├── 📖 methodology.md               # Analysis approach
    └── 🎯 business_insights.md         # Strategic implications

### 🔧 Query Categories

#### 1.

> Անի:
Basic Exploration

- Data overview and quality checks
- Min/Max analysis for understanding ranges
- Identifying companies with 100% layoffs
-- Example: Find companies that completely shut down
SELECT *
FROM world_layoffs.layoffs_staging2
WHERE percentage_laid_off = 1
ORDER BY funds_raised_millions DESC;

#### 2. Intermediate Analysis (GROUP BY)

- Company rankings by layoffs
- Geographic and industry breakdowns
- Temporal analysis by year
-- Example: Top 10 companies by total layoffs
SELECT company, SUM(total_laid_off) as total_layoffs
FROM world_layoffs.layoffs_staging2
GROUP BY company
ORDER BY total_layoffs DESC
LIMIT 10;

#### 3. Advanced Queries (CTEs & Window Functions)

- Year-over-year company rankings
- Rolling totals and time series
- Complex analytical calculations
-- Example: Top 3 companies per year with ranking
WITH Company_Year AS (
  SELECT company, YEAR(date) AS years, SUM(total_laid_off) AS total_laid_off
  FROM layoffs_staging2
  GROUP BY company, YEAR(date)
),
Company_Year_Rank AS (
  SELECT company, years, total_laid_off, 
         DENSE_RANK() OVER (PARTITION BY years ORDER BY total_laid_off DESC) AS ranking
  FROM Company_Year
)
SELECT company, years, total_laid_off, ranking
FROM Company_Year_Rank
WHERE ranking <= 3 AND years IS NOT NULL
ORDER BY years ASC, total_laid_off DESC;

-----

## 💡 Key Findings

### 🏢 Company Analysis

|Finding                  |Impact           |Details                               |
|-------------------------|-----------------|--------------------------------------|
|**Largest Single Layoff**|12,000+ employees|Meta’s significant workforce reduction|
|**Complete Shutdowns**   |150+ companies   |Startups with 100% layoff rate        |
|**High-Funded Failures** |$2B+ raised      |Even well-funded companies failed     |

### 🌍 Geographic Insights

- San Francisco Bay Area: 40% of total layoffs
- Tech Hub Concentration: Seattle, Austin, NYC heavily impacted
- Global Reach: 50+ countries represented

### 📅 Temporal Patterns

- Peak Period: 2022-2023 (COVID aftermath + economic uncertainty)
- Seasonal Trends: Q4 and Q1 show higher layoff activity
- Rolling Impact: Cumulative effect reached 300K+ employees

### 🏭 Industry Analysis

- Consumer Tech: 60% of total layoffs
- Fintech: Second most impacted sector
- Emerging Sectors: Crypto and food delivery heavily hit

-----

## 📊 Technical Highlights

### 🛠 SQL Techniques Demonstrated

|Technique              |Usage                         |Complexity|
|-----------------------|------------------------------|----------|
|**Aggregate Functions**|SUM, MAX, MIN, COUNT          |⭐⭐        |
|**Window Functions**   |DENSE_RANK(), SUM() OVER()    |⭐⭐⭐⭐      |
|**CTEs**               |Multi-level query organization|⭐⭐⭐⭐      |
|**Date Functions**     |YEAR(), SUBSTRING()           |⭐⭐⭐       |
|**Subqueries**         |Complex filtering conditions  |⭐⭐⭐       |

### 🎯 Analysis Methodology

1. 📋 Data Quality Assessment
- Null value analysis
- Data type validation
- Outlier identification
1. 🔍 Pattern Discovery
- Hypothesis-free exploration
- Multi-dimensional analysis
- Trend identification
1. 📈 Advanced Analytics
- Time series analysis
- Ranking and comparison
- Rolling calculations

-----

## 📚 Learning Outcomes

### 🎓 Skills Developed

- Advanced SQL: Window functions, CTEs, complex joins
- Data Analysis: Pattern recognition, trend analysis
- Business Intelligence: Strategic insight generation
- Problem Solving: Hypothesis-driven investigation

### 💼 Professional Applications

- Risk Assessment: Identifying vulnerable company profiles
- Market Analysis: Understanding industry trends
- Investment Strategy: Funding vs. stability correlation
- Economic Indicators: Layoffs as leading indicators

-----

## 🔮 Future Enhancements

### 📈 Planned Features

- [ ] Interactive Dashboard using Tableau/PowerBI
- [ ] Predictive Modeling for layoff forecasting
- [ ] Sentiment Analysis integration
- [ ] Real-time Data Pipeline automation
- [ ] Geographic Visualization with heat maps

> Անի:
- [ ] Industry Correlation analysis with economic indicators

### 🛠 Technical Improvements

- [ ] Performance Optimization with proper indexing
- [ ] Data Validation automated checks
- [ ] API Integration for live data feeds
- [ ] Machine Learning risk classification models

-----

## 🤝 Contributing

We welcome contributions! Here’s how you can help:

### 🎯 Ways to Contribute

- Query Optimization: Improve existing SQL queries
- New Analysis: Add different analytical perspectives
- Visualization: Create charts and dashboards
- Documentation: Enhance explanations and insights
- Data Quality: Identify and fix data issues

### 📋 Contribution Guidelines

1. Fork the repository
1. Create a feature branch (`git checkout -b feature/AmazingFeature`)
1. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
1. Push to the branch (`git push origin feature/AmazingFeature`)
1. Open a Pull Request

-----

## 📞 Contact & Support

### 👨‍💻 Author

Your Name

- 📧 Email: your.email@example.com
- 💼 LinkedIn: [Your LinkedIn Profile](https://linkedin.com/in/yourprofile)
- 🐙 GitHub: [@yourusername](https://github.com/yourusername)

### ❓ Getting Help

- Issues: Use GitHub Issues for bug reports
- Discussions: Use GitHub Discussions for questions
- Email: Contact directly for collaboration opportunities

-----

## 📜 License

This project is licensed under the MIT License - see the <LICENSE> file for details.

-----

## 🙏 Acknowledgments

- Data Source: Thanks to the layoffs data contributors
- Community: SQL and data analysis community for inspiration
- Tools: MySQL, GitHub, and various data visualization tools
- Learning: Online courses and tutorials that made this possible

-----

<div align="center">

### ⭐ If you found this analysis helpful, please give it a star!

Made with ❤️ and lots of ☕

*Last updated: June 2025*

</div>
