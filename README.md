# 🍛 Zomato EDA: Decoding India's Restaurant Scene

Welcome to my Zomato Exploratory Data Analysis (EDA) project! 

This repository is more than just a standard data analysis project—it's a hands-on reproduction and expansion of a real, published research paper: *Machine Learning-Driven Statistical Analysis of Indian Restaurants: Insights from the Zomato Dataset* (Vaidhy et al., 2025).

## 📄 The Research Paper Connection

This project is heavily inspired by and directly reproduces methodologies from:
> **Machine Learning-Driven Statistical Analysis of Indian Restaurants: Insights from the Zomato Dataset**  
> *By Ayushi Vaidhy, Deepak Batham, Rachit Jain, Amit Kumar Manjhwar (2025)*  
> [DOI: 10.2298/FUEE2502355V](https://doi.org/10.2298/FUEE2502355V)

**What I used from the paper:**
- **The Core Dataset Idea**: Using the 2 Lakh+ Zomato India dataset to find real market patterns.
- **The Data Cleaning Pipeline**: Mirroring their approach to dropping duplicates, dealing with missing text fields, and standardizing costs.
- **The EDA Roadmap**: Looking at the exact metrics they did—top chains, city-wise averages, and price vs. rating correlations.
- **The Machine Learning Benchmarks (Upcoming)**: Using their published accuracy and error metrics (R², MAE) for Linear Regression, Random Forest, XGBoost, etc., as hard targets to hit or beat.

**What I added myself:**
- **Rigorous Statistical Validation**: The paper points out visual patterns (e.g., "higher cost restaurants get better ratings"), but I introduced actual hypothesis testing (Pearson correlations, T-Tests, ANOVAs) to prove if these claims are statistically significant or just noise.
- **Missing Data Strategy**: I explicitly categorized missing data mechanisms (MCAR, MAR, MNAR) to justify my imputation strategies.

## 🎯 The Motive Behind the Project

I built this project to answer a fundamental question: **What really drives a restaurant's success (and its rating) on Zomato?** 

While it's easy to build basic charts, I wanted to hold my analysis to the standard of published research. The paper provided a great benchmark because it reported *hard numbers* for their models rather than just eyeballing trends. 

However, I also wanted to go a step further. The original paper noted patterns—like higher cost correlating with better ratings—but never actually tested them for statistical significance. So, in this project, I'm not only reproducing their data cleaning and EDA pipelines, but I'm also injecting rigorous statistical validation (p-values, T-tests, ANOVAs) to prove whether these patterns are real or just noise.

## 🗂️ What's Inside?

We are working with a massive dataset of over **2 Lakh (200,000+) restaurants** across India. The analysis is broken down into structured phases:

1. **Phase 1: Setup & Data Loading**
   Setting up the environment and loading in the raw Zomato data to understand the baseline we are working with.
   
2. **Phase 2: Deep Cleaning**
   Real-world data is messy. Here, we handle duplicates, impute missing values (classifying them as MCAR, MAR, or MNAR), clean up data types, and categorize price ranges.
   
3. **Phase 3: Exploratory Data Analysis (EDA)**
   The fun part! We dive into:
   - Identifying the biggest chains and the highest-rated ones.
   - Analyzing city-by-city foodie trends (Gurgaon vs. Bangalore vs. Hyderabad).
   - Visualizing how cost, online delivery, and table booking impact overall ratings using distributions, violin plots, and scatter plots.

4. **Phase 4: Statistical Validation**
   *This is my personal addition to the paper's methodology.*
   We run Pearson correlations and mean comparisons to statistically validate claims like "more expensive restaurants get better ratings" and "online delivery boosts ratings."

5. **Phase 5 & 6: Predictive Modeling (Coming Soon)**
   Bridging the gap between correlation and prediction. We will benchmark Linear Regression against powerful tree-based models (Decision Trees, Random Forests, XGBoost) to predict a restaurant's aggregate rating based on its features.

## 🛠️ Tech Stack
- **Python** 
- **Pandas & NumPy** for heavy data lifting
- **Matplotlib & Seaborn** for beautiful, insightful visualizations


## 💡 Key Takeaway
At its core, this project is about bridging the gap between raw data and actionable business intelligence in the food-tech space. Feel free to explore the notebook, tweak the code, and discover your own insights!

## ⚖️ Disclaimer & Legal
- **Data Ownership**: The dataset used in this project is sourced from Kaggle. All restaurant data, names, and metrics are the intellectual property of [Zomato](https://www.zomato.com/). 
- **Educational Purpose**: This project is strictly for non-commercial, educational, and academic research purposes. It is not affiliated with, endorsed by, or sponsored by Zomato or the authors of the referenced research paper.
