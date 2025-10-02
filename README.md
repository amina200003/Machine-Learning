# Student Stress Level Classification

## Context
This project aims to classify **student stress levels** using biometric data, with a focus on the target variable **`Stress_Level_Biosensor`**.  
Several classifiers were tested to determine which one performs best.

##  Data Preparation
Before training the models, data preprocessing was necessary:  

- The target variable `Stress_Level_Biosensor` contains **continuous quantitative values**.  
- For classification tasks, values must be **discrete**.  
- The **`pandas.cut`** function was used to split the values into intervals and assign category labels corresponding to stress levels.  

### Initial Segmentation
- `[0 - 4.5[` → **low**  
- `[4.5 - 8.5[` → **medium**  
- `[8.5 - 10]` → **high**  

> ⚠️ This segmentation caused a **class imbalance issue**, especially for the **high stress** category, which was non-existent in the dataset.

 ### Optimized Segmentation
- `[0 - 4.5[` → **low**  
- `[4.5 - 10[` → **high**  
- `[10 - ∞[` → **unknown** (no student in the dataset reached this stress level)  

✅ This new segmentation resulted in more balanced classes and more reliable outcomes.   

## Methodology
- The dataset was split into:  
  - **70%** for training  
  - **30%** for testing  

- The following classifiers were applied:  
  - 🌲 RandomForest Classifier  
  - ⚡ Perceptron  
  - 📈 Logistic Regression  
  - 🔲 Support Vector Machine (SVM)  

Although performance results were similar across models, each algorithm **assigned different weights to features**, showing distinct classification strategies.  

## 📊 Results
Using the optimized segmentation:  
- **Overall accuracy**: **75%** **with SVM**  
- **Total errors**: **74 out of 300 samples** **with SVM**  

These results show an improvement compared to the first segmentation. However, performance may still be limited due to the arbitrary interval choice and class imbalance.  
