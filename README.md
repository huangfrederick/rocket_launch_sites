# SpaceX Falcon 9 First Stage Landing Prediction

Binary classification project predicting whether a Falcon 9 first stage booster will successfully land and be recovered for reuse. Booster recovery status directly determines launch cost — a recovered booster significantly reduces the cost of a subsequent launch, making this a meaningful prediction target beyond a classification exercise.

---

## Project Overview

SpaceX lists Falcon 9 launches at approximately $74M, compared to competitors charging upward of $90M for comparable payloads. A primary cost driver is first stage reusability. This project uses publicly available launch data to predict recovery success and explore which mission parameters are most predictive of that outcome.

**Data sources:**
- SpaceX REST API — launch records, booster data, payload information
- Wikipedia — supplementary launch outcome and manifest data

**Data pipeline:** Raw API responses and scraped Wikipedia tables → pandas cleaning and labeling → structured CSV files (included in `/data`)

---

## Getting Started

### Clone the Repository

```bash
git clone https://github.com/huangfrederick/rocket_launch_sites.git
cd your-repo-name
```

### Install Dependencies

This project uses standard Python data science libraries. Install them via pip:

```bash
pip install -r requirements.txt
```

Or install individually:

```bash
pip install pandas numpy scikit-learn matplotlib seaborn folium requests beautifulsoup4 jupyter
```

A `requirements.txt` is included in the root of the repository.

### Run the Notebooks

Launch Jupyter and open the notebooks in order:

```bash
jupyter notebook
```

Navigate to the `notebooks/` directory and run them sequentially (01 → 04).

---

## Requirements

| Package | Purpose |
|---|---|
| `pandas` | Data manipulation and cleaning |
| `numpy` | Numerical operations |
| `scikit-learn` | Model training, GridSearchCV, evaluation |
| `matplotlib` | Plotting and confusion matrices |
| `seaborn` | Statistical visualizations |
| `folium` | Interactive geospatial maps |
| `requests` | SpaceX API calls |
| `beautifulsoup4` | Wikipedia scraping |
| `jupyter` | Notebook environment |

Python 3.8+ recommended.

---

## Methods

### Exploratory Data Analysis
- Payload mass, orbit type, launch site, booster version, and flight number analyzed for relationship to landing outcome
- Launch site geolocation visualized using Folium — interactive map with markers for each active launch site
- Feature distributions and class balance examined with Matplotlib and Seaborn

### Modeling
Four classifiers (logistic regression, SVMs, KNN, and Decision Tree) were trained, tuned with GridSearchCV, and evaluated.

**Evaluation:** `.score()` accuracy on held-out test set; confusion matrices plotted for each model to visualize false positive/negative tradeoffs.

---

## Repository Structure

```
├── data/
│   ├── Falcon9_api_data.csv        # Cleaned and labeled launch records
│   └── ...                           # Additional datasets
├── notebook pdfs/
│   ├── Launch Data Collection.pdf    # API calls and Wikipedia scraping
│   ├── Launch Data Wrangling.pdf     # Cleaning, labeling, feature engineering
│   ├── Launch Site Locations.pdf     # Exploratory analysis and Folium visualization
│   └── Falcon 9 Classifications.pdf  # Model training, GridSearchCV, evaluation
├── requirements.txt
└── README.md
```

---
