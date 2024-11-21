
# Diabetes Prediction Project

## Project Overview  
This project leverages machine learning techniques to predict the likelihood of an individual having diabetes based on health-related attributes. The primary goal is to build a deployable model that can process new input data and return predictions on diabetes likelihood.  

---

## Dataset  
The dataset, **`diabetes_prediction_dataset.csv`**, contains health metrics for various individuals, with each row representing a distinct individual. Key attributes include:  

- **Gender**: The biological sex of the individual. This attribute may influence susceptibility to diabetes. Categories include:
  - `Male`
  - `Female`
  - `Other`
  
- **Age**: The age of the individual, ranging from 0 to 80 years. Age is an important factor in determining diabetes risk, as it is more commonly diagnosed in older adults.

- **BMI (Body Mass Index)**: A measure of body fat based on height and weight. Higher BMI values are associated with a greater risk of developing diabetes. 
  - *Categories*: Underweight, Normal, Overweight, Obese

- **Hypertension**: A binary variable (0 or 1) indicating whether the individual has hypertension. 
  - `0` = No hypertension
  - `1` = Has hypertension

- **Heart Disease**: A binary variable (0 or 1) indicating whether the individual has heart disease.
  - `0` = No heart disease
  - `1` = Has heart disease

- **Smoking History**: Smoking is considered a risk factor for diabetes and can exacerbate diabetes complications. This attribute has 5 categories:
  - `Not Current`: Individual does not currently smoke but has a history of smoking.
  - `Former`: Individual used to smoke but has quit.
  - `No Info`: No information available on smoking status.
  - `Current`: Individual currently smokes.
  - `Never`: Individual has never smoked.
  - `Ever`: Individual has smoked at some point in their life.

- **Blood Glucose Level**: Refers to the amount of glucose in the bloodstream at a given time. High blood glucose levels are a key indicator of diabetes. Elevated blood glucose is associated with an increased risk of developing diabetes.

- **HbA1c Level**: Hemoglobin A1c (HbA1c) level is a measure of a person's average blood sugar level over the past 2-3 months. Higher levels indicate a greater risk of developing diabetes. Typically, an HbA1c level greater than 6.5% suggests the presence of diabetes.

### Target Variable:
- **Diabetes**: A binary variable indicating whether the individual has diabetes.
  - `0` = No diabetes
  - `1` = Has diabetes


---

## Project Structure  
The repository includes the following:  

- **`README.md`**: Overview of the project and setup instructions  
- **`data/`**: Contains the dataset file  
- **`notebook.ipynb`**: Jupyter Notebook for data exploration, cleaning, feature engineering, model selection, and tuning  
- **`train.py`**: Script to train the final model and save it for deployment  
- **`predict.py`**: Script to load the saved model and host it as a web service  
- **`requirements.txt`**: List of required Python packages  
- **`Dockerfile`**: Setup for deploying the model using Docker
- **`models/`**: Directory containing the saved model and preprocessing pipeline files:
  - `dv.pkl`: The trained data preprocessing model
  - `xgb_model.pkl`: The trained XGBoost model  

---

## Installation and Usage  

### Step 1: Clone the Repository  
```bash
git clone <repository-url>
cd Diabetes-Prediction
```  

### Step 2: Install Dependencies  
Install required packages:  
```bash
pip install -r requirements.txt
```  

Alternatively, use **conda** or **Pipenv** if preferred.  

### Step 3: Run Data Preparation and Model Training  
- Open **`notebook.ipynb`** for exploratory data analysis (EDA), feature engineering, and model training.  
- Or train the model directly using:  
  ```bash
  python train.py
  ```  

### Step 4: Start the Prediction Service  
To start a Flask or BentoML prediction service:  
```bash
python predict.py
```  

This will launch a web server to accept prediction requests.  

---

## Usage Example  

Send a POST request with relevant health data in JSON format, such as:  
```json
{
 "gender": "female",
 "age": 30.0,
 "hypertension": "no_hypertension",
 "heart_disease": "has_heart_disease",
 "smoking_history": "current",
 "bmi": 30.73,
 "HbA1c_level": 6.6,
 "blood_glucose_level": 150
}
```  
The service will respond with a diabetes prediction.  

---

## Deployment  
The project includes a **Dockerfile** for containerization. To deploy:  
1. Build the Docker container:  
   ```bash
   docker build -t diabetes-prediction .
   ```  
2. Run the container:  
   ```bash
   docker run -p 9696:9696 diabetes-prediction
   ```  

This will start the service on `http://localhost:9696`.  
