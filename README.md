# SmartProp Rwanda: House Price Prediction Model

A machine learning model that estimates the sale price of a house from its land, building and location data. It returns an estimated price, a price range, and the main reasons behind the estimate.

This repository is part of the **SmartProp Rwanda** project, an AI-assisted property valuation and monitoring platform for property owners in Rwanda.

> **Status:** practice phase. The model is trained on a public dataset from the USA to learn and test the full pipeline. It will be retrained on Rwandan data when that data is available. Results here do **not** describe Rwandan property prices.

## What the notebook does

| Step | Description |
| --- | --- |
| 1 | Setup and settings |
| 2 | Load the data |
| 3 | Check data quality |
| 4 | Clean the data |
| 5 | Explore the data (EDA) |
| 6 | Create features |
| 7 | Split into train and test by area (the test set contains areas the model has never seen) |
| 8 | Compare models with cross-validation (baseline, Ridge, Random Forest, XGBoost) |
| 9 | Tune the best model |
| 10 | Build an 80% price range from past errors |
| 11 | Final test on unseen areas |
| 12 | Explain the model with SHAP |
| 13 | Save the model and its settings |
| 14 | Prediction function (the basis of the future API) |

## Data

- **Dataset:** [kc_house_data](https://www.kaggle.com/datasets/yeonseokcho/kc-house-data), about 21,600 house sales in King County, USA (2014-2015).
- **Target:** `price` (the sale price). The model is trained on the logarithm of the price.
- The data file is **not** included in this repository. Download it from Kaggle and place `kc_house_data.csv` in the `data/` folder. Check the dataset's licence on its Kaggle page.

## Project structure

```
smartmodal/
├── house_price.ipynb     # the full notebook
├── data/                 # dataset (not tracked by Git)
├── models/               # saved models (not tracked by Git)
├── requirements.txt
└── README.md
```

## Setup

```bash
# 1. Clone the repository
git clone https://github.com/<your-username>/<repository-name>.git
cd <repository-name>

# 2. Create and activate a virtual environment
python3 -m venv .venv
source .venv/bin/activate          # on Windows: .venv\Scripts\activate

# 3. Install the libraries
pip install -r requirements.txt

# 4. Download kc_house_data.csv from Kaggle into data/

# 5. Start JupyterLab and open the notebook
jupyter lab
```

## How to run

Open `house_price.ipynb` and run the cells from top to bottom, one at a time. Read the output of each step before moving to the next one. The tuning step (Step 9) takes a few minutes.

## Results

Results on `kc_house_data` (unseen test areas):

| Metric | Value |
| --- | --- |
| Average error (MAE) | [fill in] |
| Average error in % (MAPE) | [fill in] |
| Houses within 20% of the real price | [fill in] |
| 80% range contains the real price | [fill in] |

## Example prediction

```python
predict_price({
    "sqft_living": 1800, "sqft_lot": 6000, "bedrooms": 3, "bathrooms": 2,
    "lat": 47.55, "long": -122.25, "yr_built": 1985, "grade": 7, "condition": 3
})
```

The function returns the estimated price, a low and high price (80% range), the top five reasons for the estimate, the model version, and a disclaimer.

## Limitations

- The model learned one county in one year. It says nothing about prices in Kigali or in other places.
- Prices change over time, so the model needs to be retrained regularly.
- The estimate is for guidance only. It is **not** a certified valuation. Mortgage, tax and compensation valuations in Rwanda must be prepared by a certified valuer.

## Roadmap

- [x] Price model pipeline on practice data
- [ ] Retrain on Rwandan sales data (land area in m², village or sector, price in RWF)
- [ ] Add the inputs from the proposal: land right, Master Plan zone, services, road access
- [ ] Add photo features (condition score and defect count from an image model)
- [ ] Wrap `predict_price` in an API
- [ ] Connect the API to the dashboard

## Privacy

Never commit real owner data, UPIs, photos, tokens or passwords to this repository. Keep the repository private while it handles any real data.

## Author

Patrick Nambajimana
