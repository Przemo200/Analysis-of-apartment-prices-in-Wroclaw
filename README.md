# Apartments price analysis & prediction in Wroclaw

## Project overview
This project aims to analyze apartment prices in Wroclaw, Poland using a real-world dataset. The analysis includes extensive data cleaning, exploratory data analysis (EDA) and the construction of machine learning models to predict property prices. The goal is to offer insights into key price drivers and build tools to help buyers, sellers, investors and real estate agents make better data-driven decisions.

---

## Why Wroclaw?
Wroclaw is a rapidly growing city in southwestern Poland, known for its dynamic economy, rich academic environment and increasing population. As a student currently living and renting in Wroclaw, the local housing market is both relevant and insightful to explore. The city's real estate market reflects trends found in many urban centers in Central Europe, making it a valuable case study.

---

## Dataset
- **Source**: [Kaggle - Apartment Prices in Poland](https://www.kaggle.com/datasets/krzysztofjamroz/apartment-prices-in-poland)
- **File used**: `apartments_pl_2024_06.csv`
- **Focus**: this project filters and analyzes only listings located in **Wroclaw**.

### Key features:
- `squareMeters`: total area of the apartment
- `rooms`: number of rooms
- `floor`, `floorCount`: apartment floor and building height
- `buildYear`: construction year
- `centreDistance`: distance to city centre (in km)
- `price`: total price in PLN

---

## Exploratory Data Analysis (EDA)

### Cleaning and preprocessing:
- Removed listings with unrealistic values (e.g., size < 10 m², price/m² > 30,000 PLN)
- Handled missing values in floor and apartment type columns
- Created a new column `price_per_m2` (price divided by square meters)

### Visual analysis:
- **Histograms** for price and price per m² distribution
- **Boxplots** to examine how price per m² varies with number of rooms
- **Line plots** to explore price trends by construction year
- **Correlation heatmap** to show relationships between numeric variables
- **Bar charts** showing average price and price per m² grouped by room count
- **Heatmap** showing average price per m² based on floor and room count
- **Scatter plot** of apartment size vs price colored by number of rooms

These visualizations helped reveal important patterns and dependencies in the Wroclaw real estate market.

---

## Predictive modeling

### 1. **Linear regression**
- Simple model using numerical predictors: size, rooms, floor, floor count, year built and distance to center
- Performance:
  - **R²**: ~0.69
  - **MAE**: ~92,000 PLN
  - **RMSE**: ~126,000 PLN
- Strengths: interpretable, fast to train
- Weaknesses: assumes linearity, less effective with complex relationships

### 2. **XGBoost regressor**
- Gradient boosting decision tree model
- Handles non-linear relationships and interactions between features well
- Performance:
  - **higher R²** than linear model: ~0.79
  - **lower MAE and RMSE**
- Feature importance reveals that **apartment size**, **build year** and **centre distance** are the top predictors

---

## Sample price prediction
A sample prediction was performed using both models for an apartment with the following attributes:
- 60 m²
- 3 rooms
- 5th floor in a 6-floor building
- Built in 2021
- 8 km from the city center

| Model              | Predicted Price | MAE (± Error Range) |
|-------------------|----------------:|---------------------:|
| Linear Regression | ~750,000 PLN    | ± 92,000 PLN        |
| XGBoost           | ~809,000 PLN    | ± 70,000 PLN        |

---
## **Models summary**

This project uses two regression models to predict apartment prices

###**Linear Regression**
- **How it works**  
  Linear regression assumes a **linear relationship** between the target variable (price) and the input features (size, rooms, floor, etc.). It fits a straight line that minimizes the squared error between predicted and actual values.

- **Why it was chosen**  
  It's a simple and interpretable baseline model that shows the **direct influence of each variable**. It's fast to train and provides useful insights into linear relationships.

- **Limitations**  
  Real estate prices often follow **non-linear patterns**. Linear models can be misled by **correlated variables** (multicollinearity). In this case, it incorrectly identified distance to city center as the most important feature, likely due to its correlation with other factors.

---

###**XGBoost Regressor**
- **How it works**  
  XGBoost is an **ensemble method** that builds multiple decision trees in sequence. Each tree learns to correct the errors of the previous ones. It can model **complex and non-linear interactions** between features.

- **Why it was chosen**  
  XGBoost is widely used for **structured data** and consistently delivers top results in regression and classification tasks. It handles **missing values**, **non-linearity** and **feature interactions** effectively.

- **Strengths**  
  - Models complex patterns  
  - More robust to outliers  
  - Provides feature importance metrics  
  - **Higher accuracy** than linear models

---

###**Conclusion**
- **XGBoost outperforms linear regression** on this dataset 
- While linear regression is useful for quick insights and interpretability, XGBoost is **better suited for production-level predictions** due to its flexibility and accuracy

---

## Key business insights

1. **Apartment size is the most influential pricing factor**  
   Larger apartments consistently command higher total prices, making apartment size the strongest predictor of value.

2. **Newer apartments yield higher values**  
   Properties built in the last decade are significantly more expensive per meter squared, reflecting buyer preference for modern construction, better amenities, and energy efficiency.

3. **Proximity to city center shows misleading importance in linear regression**  
   In linear regression distance to the city center appeared as the most influential feature. However, this result is likely distorted by correlations with other factors (e.g., apartment size, age of buildings).  
   The XGBoost model, which captures non-linear relationships, correctly highlights that **square meters** are the true dominant driver of apartment price.

4. **Advanced models improve price prediction**  
   XGBoost significantly outperforms linear regression by capturing complex patterns in the data leading to more accurate and reliable predictions.

5. **Insight-driven strategy benefits all stakeholders**  
   Buyers can better spot valuable opportunities, sellers can set fair prices and real estate agents can offer more accurate market evaluations, improving decision-making for everyone involved.


---

## Tools & technologies used
- **Python 3**
- **Pandas**, **NumPy** for data manipulation
- **Matplotlib**, **Seaborn** for visualization
- **Scikit-learn** for linear regression and evaluation
- **XGBoost** for advanced regression modeling
- **Google Colab** for development environment

---

## Future work
- Include categorical features such as apartment type and neighborhood (one-hot encoding)
- Incorporate geospatial analysis (e.g. coordinates, district boundaries)
- Expand model with more data sources (e.g. building materials, amenities)
- Deploy as a web application for public or business use (e.g. Streamlit or Flask)

---

## Author
- **Name**: Przemysław Dyjak
- **Location**: Wroclaw, Poland
- **Contact**: [LinkedIn](https://www.linkedin.com/in/przemys%C5%82aw-dyjak-666a11356/)

---

## License
This project is licensed under the **GNU General Public License v3.0 (GPL-3.0)**.
