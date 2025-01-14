# 🚢 Spaceship Titanic - Kaggle Competition Solution

Welcome to my repository for the Spaceship Titanic Kaggle competition!
This project provides a solution to the binary classification problem: predicting whether a passenger aboard the Spaceship Titanic was transported to another dimension (Transported = 1) or not (Transported = 0).

## 📋 Project Description

### The goal is to build an accurate machine learning model to predict passenger transportation outcomes.
### The model processes the provided data, handles missing values, encodes categorical features, and scales numerical features to achieve high performance metrics.

## 🛠️ Methodology

### The preprocessing is handled by the preprocess_data():

1. Handling Missing Values:
    For numerical features, missing values are filled with the median.
    For categorical features, missing values are filled with the most frequent value.
2. Splitting the "Cabin" Feature:
    The Cabin feature is split into three new features: Deck, Cabin_num, and Side using .str.split().
3. Dropping Unnecessary Features:
    Features such as Name and Cabin are dropped.
4. Converting Data Types:
    The Age feature is converted to an integer type.
    The Cabin_num feature is also converted to an integer type.


## 🔋 Encoding and Scaling Features

### The function order_and_scale_features() is used to process categorical and numerical features:

1. Numerical Features: Scaled using RobustScaler to reduce the effect of outliers.
2. Categorical Features: Encoded using OrdinalEncoder.

The function supports both training mode (is_train=True) and testing mode:

1. In training mode, the function encodes and scales the features while saving the fitted parameters.
2. In testing mode, it only transforms the data using the saved encoder and scaler.

## 🚴🏻‍♂️ Model Training

### The project uses two main machine learning models:

RandomForestClassifier: A straightforward and interpretable ensemble method.
    
    random_forest = RandomForestClassifier(
        n_estimators=200,
        max_features='sqrt',
        min_samples_split=4,
        min_samples_leaf=2,
        random_state=42)
    random_forest.fit(X_train_final, y_train)

CatBoostClassifier: A gradient boosting algorithm that is particularly effective for categorical data.

    cgbdt = CatBoostClassifier(
        iterations=200,
        learning_rate=0.2,
        random_seed=42,
        verbose=200,
        l2_leaf_reg=7
    )
    cgbdt.fit(X_train_final, y_train)

## 📈 Results

### The best results were achieved using the CatBoostClassifier, with:

    Local validation accuracy: ~82%
    Kaggle public leaderboard score: ~0.79
