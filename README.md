# Buenos Aires Apartment Price Predictor
A machine learning project that predicts apartment prices in Buenos Aires based on size, location, and neighborhood. Built using Python and scikit-learn, this model helps users estimate real estate values through an interactive dashboard.

##  Project Overview

This project builds a predictive model for apartment prices in Buenos Aires using features like covered surface area, geographic coordinates (latitude/longitude), and neighborhood. The model is trained on real estate data and deployed via an interactive dashboard where users can input property details to get instant price predictions.

##  Features

- **Data Preprocessing**: Cleans and prepares real estate data for modeling
- **Feature Engineering**: Encodes categorical variables and handles missing values
- **Machine Learning Pipeline**: Uses Ridge regression for price prediction
- **Interactive Dashboard**: Allows users to input property details and view predicted prices
- **Model Evaluation**: Compares baseline and trained model performance using MAE

##  Dataset

The dataset includes apartment listings from Buenos Aires with the following features:
- `price_aprox_usd`: Target variable (apartment price in USD)
- `surface_covered_in_m2`: Covered area in square meters
- `lat` / `lon`: Geographic coordinates
- `neighborhood`: Buenos Aires neighborhood

## Tools & Technologies Used

### Programming & Data Science
- **Python 3** - Primary programming language
- **Jupyter Notebook** - Interactive development environment
- **pandas** - Data manipulation and analysis
- **scikit-learn** - Machine learning library
- **seaborn** - Statistical data visualization
- **category-encoders** - Categorical variable encoding

### Machine Learning
- **Ridge Regression** - Regularized linear model
- **Pipeline** - Streamlined ML workflow
- **OneHotEncoder** - Categorical feature encoding
- **SimpleImputer** - Missing value handling
- **mean_absolute_error** - Model evaluation metric

### Interactive Features
- **ipywidgets** - Interactive dashboard components
- **Dropdown, Sliders** - User input controls

## Data Preprocessing

### Data Cleaning Steps:
1. **Data Import & Combination**
   - Combined 5 separate CSV files into single DataFrame
   - 6,582 total apartment listings after filtering

2. **Data Filtering**
   - Only apartments in "Capital Federal"
   - Property type: "apartment" only
   - Price limit: < $400,000 USD
   - Removed outliers in `surface_covered_in_m2` (10th-90th percentile)

3. **Feature Engineering**
   - Split `lat-lon` column into separate `lat` and `lon` features
   - Extracted neighborhood from `place_with_parent_names` column

4. **Column Removal Strategy**
   - **High Null Columns**: Removed `floor`, `expenses` (>50% missing)
   - **Low Cardinality**: Removed `operation`, `property_type`, `currency`, `properati_url`
   - **Leaky Features**: Removed `price`, `price_aprox_local_currency`, `price_per_m2`, `price_usd_per_m2`
   - **Multicollinearity**: Removed `surface_total_in_m2`, `rooms` (high correlation with covered surface)

### Final Feature Set:
- `surface_covered_in_m2` - Covered area in square meters
- `lat` - Latitude coordinates
- `lon` - Longitude coordinates  
- `neighborhood` - Buenos Aires neighborhood (categorical)

## Results & Insights

### Model Performance
| Metric | Baseline | Trained Model | Improvement |
|--------|----------|---------------|-------------|
| **MAE** | $44,860 | $24,207 | **46% reduction** |
| **Mean Price** | $132,384 | - | - |

### Key Insights
1. **Feature Importance**: Location (coordinates + neighborhood) and size are strongest price predictors
2. **Model Effectiveness**: Ridge regression effectively handles the feature space with regularization
3. **Business Impact**: Model provides reasonable price estimates within ~$24K of actual values

### Interactive Dashboard Capabilities
- Users can input specific property characteristics
- Real-time price predictions for any Buenos Aires neighborhood
- Adjustable parameters: area (30-101 m²), coordinates, neighborhood selection
