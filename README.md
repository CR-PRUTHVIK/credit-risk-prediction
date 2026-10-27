# Credit Risk Prediction

A machine-learning web application that estimates loan/credit risk from
applicant and loan information. The project uses a trained **XGBoost**
model served through **FastAPI**, with a web interface built using HTML,
CSS, and JavaScript.

> **Important:** This is an educational project, not a financial-advice
> tool or a substitute for a lender's formal credit assessment.
> Predictions can be wrong and should not be used as the sole basis for
> real lending decisions.

## Features

-   Predicts credit/loan risk using a saved machine-learning model.
-   Serves predictions through a FastAPI backend.
-   Includes a browser-based interface in the `static/` directory.
-   Uses a separately saved decision threshold (`best_threshold.pkl`) to
    convert a predicted probability into a risk classification.
-   Includes a notebook and dataset used during model development.

## Tech stack

-   Python
-   FastAPI
-   XGBoost
-   scikit-learn
-   pandas
-   Joblib
-   HTML, CSS, JavaScript

The exact package versions are listed in
[`requirements.txt`](requirements.txt).

## Project structure

``` text
credit.risk/
├── main.py                    # FastAPI application and prediction endpoint
├── credit_risk_model.pkl      # Trained model artifact
├── best_threshold.pkl         # Saved classification threshold
├── credit_risk_dataset.csv    # Dataset used for model development
├── Credit_risk.ipynb          # Model development/training notebook
├── requirements.txt           # Python dependencies
├── runtime.txt                # Runtime version/configuration, if used by deployment
├── render.yaml                # Render deployment configuration
└── static/
    ├── index.html             # Web page
    ├── styles.css             # Styling
    └── script.js              # Frontend behavior
```

Some generated or supporting files may be present locally but are not
required for every deployment.

## How the application works

1.  A user enters loan/applicant information in the web interface.
2.  The frontend sends the information to the FastAPI backend.
3.  The backend loads the saved model and obtains a risk probability.
4.  The saved threshold is used to convert the probability into a
    predicted class.
5.  The API returns the prediction details for the interface to display.

The model and threshold files must correspond to the same
trained/calibrated model version. If either artifact is replaced, test
the complete prediction flow again.

## Run locally on Windows

### 1. Open the project folder

``` powershell
cd D:\credit.risk
```

### 2. Create and activate a virtual environment

``` powershell
py -3.11 -m venv venv
.\venv\Scripts\Activate.ps1
```

If PowerShell blocks activation, you can use Command Prompt instead, or
follow your machine's Python execution-policy guidance.

### 3. Install dependencies

``` powershell
python -m pip install --upgrade pip
pip install -r requirements.txt
```

### 4. Start the FastAPI server

``` powershell
uvicorn main:app --reload
```

If `uvicorn` is not found, verify that the virtual environment is
activated and that the required server package is present in
`requirements.txt`.

### 5. Open the application

-   Web application: http://127.0.0.1:8000/
-   Interactive API documentation: http://127.0.0.1:8000/docs

Keep the terminal running while using the app. Press `Ctrl+C` in the
terminal to stop the server.

## API

The prediction endpoint is:

``` text
POST /predict
```

It accepts the loan-related input fields defined by the request model in
`main.py`. Check that file for the exact field names, data types, and
required fields.

Example request shape (replace the placeholder keys and values with the
exact schema in `main.py`):

``` json
{
  "feature_1": 0,
  "feature_2": 0
}
```

The endpoint returns the model's prediction information, including a
probability, predicted class, threshold, and risk label, as implemented
by the API.

## Model and threshold

The project stores the trained estimator in `credit_risk_model.pkl` and
the selected classification threshold in `best_threshold.pkl`. The
threshold affects the trade-off between precision and recall, so it
should be selected and evaluated on appropriate validation data rather
than chosen arbitrarily.

Do not report model accuracy, precision, recall, F1-score, ROC-AUC, or
other performance values unless they have been measured and documented
for the current saved model.

## Deployment

The repository includes `render.yaml`, which may be used for Render
deployment configuration. Review its build and start commands and ensure
the required model files and dependencies are available in the deployed
environment before deploying.

## Git workflow

After making and testing code changes:

``` powershell
git add .
git commit -m "Describe your changes"
git push
```

Make sure `.gitignore` excludes local environments, Python cache files,
and secrets.

## Responsible use and data privacy

-   Do not commit API keys, passwords, personal applicant records, or
    other confidential data.
-   Confirm that you have permission to publish the dataset and any
    trained artifacts before making the repository public.
-   Treat predictions as estimates, not guarantees.
-   Check for bias, data leakage, and performance differences across
    relevant groups before any real-world use.

## Author

Created as a machine-learning project for learning and demonstration.
