# SpaceX Falcon 9 First Stage Landing Prediction

Binary classification project predicting whether a Falcon 9 first stage booster will successfully land and be recovered for reuse. Booster recovery status directly determines launch cost, as a recovered booster significantly reduces the cost of a subsequent launch, making this a meaningful prediction target beyond a classification exercise.

---

## Project Overview

Building a Falcon 9 booster costs roughly $30M; the expendable second stage adds another $10M, putting the cost of a single fully-expendable launch at around $45M. SpaceX lists Falcon 9 launches at approximately $74-77M, compared to competitors charging upward of $90M for comparable payloads. Historically, rocket launches for the Saturn V rockets used for NASA's Apollo missions averaged around $12K/kg sent to space, with later costs notably reaching ~$80K/kg for the space shuttle used during the deployment of the Hubble Space Telescope and supply deliveries to the International Space Station, despite being "reusable". A primary cost driver is first stage reusability. If the booster is recovered and reflown, refurbishing it for another launch costs about $1M, turning a ~$45M expense into a ~$1M one on every subsequent flight.

The idea this project is built around is that landing success isn't a footnote to these missions but the difference between a $45M booster and a $1M one.

This project uses publicly available launch data to predict recovery success and explore which mission parameters are most predictive of that outcome.

## Background and Motivation

For most of spaceflight history, cost per kilogram to orbit went up, not down. The Saturn V put a kilogram in orbit for about $12,000 in today's dollars; the Space Shuttle, despite being designed for reuse, cost roughly $80,000/kg, making it the most expensive way humans have ever reached orbit. Fuel is not the entire problem, as propellant (e.g., liquid methane and kerosene) is only about 0.3% of a rocket's total cost. The machine itself was the expense, and for 60 years the space exploriation just threw rockets in the ocean after one flight.

That changed in 2016, when SpaceX landed a Falcon 9 booster on a drone ship and flew it again. Cost per kilogram to orbit fell more than 20x. Reuse is no longer theoretical at this point either. This is because individual boosters have now flown as many as 34 times, and SpaceX flew 165 Falcon 9 launches last year alone, only possible because landing succeeds reliably enough to fly the same hardware over and over.

In other words, the entire economic case for Falcon 9 (and later on Starship), the reason SpaceX can out-price competitors and stay profitable, rests on if the booster can land. This directly affects the number of flights you can put out, as the majority of Falcon 9 flights carry SpaceX's Starlink satellites which make up its most consistent source of profit. When SpaceX went public on Nasdaq in June 2026 as the largest IPO in history, Starlink was the company's only profitable segment.

The economic case for SpaceX and the first stage of its Falcon 9 boosters rests on their landing outcome, forming the question/target variable that this introductory machine learning project wanted to answer and model.

**Data sources:**
- SpaceX REST API — launch records, booster data, payload information
- Wikipedia — supplementary launch outcome and manifest data

**Data pipeline:** Raw API responses and scraped Wikipedia tables → pandas cleaning and labeling → structured CSV files (included in `/data`)

---

## Getting Started

### Clone the Repository

```bash
git clone https://github.com/huangfrederick/rocket_launch_sites.git
cd rocket_launch_sites
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

Navigate to the `notebooks/` directory and run them sequentially (collection, wrangling, visualization, classfication).

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
