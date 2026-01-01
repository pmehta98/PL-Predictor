# Premier League Match Predictor

A machine learning project that predicts Premier League match outcomes using historical data and advanced feature engineering. The model uses an ensemble of XGBoost, Random Forest, and Logistic Regression classifiers to predict home wins, draws, and away wins.

## Features

- Fetches live Premier League data from Football-Data.org API
- Historical data analysis (2020-2026 seasons)
- Advanced feature engineering:
  - Overall team form (last 5 matches)
  - Venue-specific scoring patterns (home/away performance)
  - Head-to-head statistics (last 4 meetings)
  - Goal differentials and rolling averages
- Weighted ensemble model combining three classifiers
- Interactive prediction interface with team selection
- Feature importance analysis and visualization

## Model Performance

- Test Accuracy: ~48.2% (weighted ensemble)
- Training data: 830 matches across 3 seasons
- Features: 11 engineered features including form, scoring patterns, and H2H stats

## Prerequisites

- Python 3.8+
- Free API key from [Football-Data.org](https://www.football-data.org/)

## Installation

1. Clone this repository:
```bash
git clone https://github.com/yourusername/PL-predictor.git
cd PL-predictor
```

2. Install required packages:
```bash
pip install -r requirements.txt
```

3. Get your free API key:
   - Sign up at [Football-Data.org](https://www.football-data.org/client/register)
   - Copy your API key from the dashboard

## Usage

1. Open the Jupyter notebook:
```bash
jupyter notebook PL_predictor_model.ipynb
```

2. Run the cells in order:
   - **Step 1**: Enter your API key when prompted
   - **Step 2**: Fetch current 2025-26 season data
   - **Step 3**: Fetch and merge historical data (2020-2024)
   - **Step 4**: Engineer features (form, scoring, H2H)
   - **Step 5**: Train ensemble model (XGBoost, Random Forest, Logistic Regression)
   - **Step 6**: View team ID mapping and select teams to predict
   - **Step 7**: Get prediction probabilities for your selected match

3. The notebook will generate CSV files automatically (these are not included in the repo):
   - `pl_2025_current.csv` - Current season finished matches
   - `pl_2025_full.csv` - All current season matches
   - `pl_master_data.csv` - Combined historical and current data
   - `pl_master_features.csv` - Engineered features dataset

## Example Prediction Output

```
Prediction for Manchester City FC vs Crystal Palace FC:
Manchester City FC Form (last 5 overall): 2.00 pts
Crystal Palace FC Form (last 5 overall): 2.00 pts
Manchester City FC Scoring (last 5 home): 2.4 avg goals scored, 0.8 conceded
Crystal Palace FC Scoring (last 5 away): 1.4 avg goals scored, 0.8 conceded
H2H Manchester City FC Win Rate: 50.0%

Predicted: Manchester City FC Win
Probabilities:
  Manchester City FC Win: 41.5%
  Draw: 37.6%
  Crystal Palace FC Win: 20.9%
```

## Feature Engineering Details

The model uses 11 key features:

1. **Home_Form** - Home team's average points from last 5 matches (all venues)
2. **Away_Form** - Away team's average points from last 5 matches (all venues)
3. **Form_Diff** - Difference between home and away form
4. **Home_Goals_Scored_Rolling** - Home team's average goals scored in last 5 home games
5. **Home_Goals_Conceded_Rolling** - Home team's average goals conceded in last 5 home games
6. **Away_Goals_Scored_Rolling** - Away team's average goals scored in last 5 away games
7. **Away_Goals_Conceded_Rolling** - Away team's average goals conceded in last 5 away games
8. **H2H_Home_Win_Rate** - Home team's win rate in last 4 head-to-head meetings
9. **H2H_Goal_Diff_Avg** - Average goal difference in last 4 head-to-head meetings
10. **Home_Encoded** - Encoded home team ID
11. **Away_Encoded** - Encoded away team ID

## Model Architecture

The prediction system uses a weighted ensemble approach:
- **XGBoost Classifier** (300 estimators, max_depth=6)
- **Random Forest Classifier** (300 estimators)
- **Logistic Regression**

Each model's predictions are weighted based on their test accuracy, providing more robust predictions than any single model.

## Limitations

- Free API tier has rate limits (10 calls/minute)
- Model accuracy is inherently limited by the unpredictable nature of football
- Historical data before 2023 may be unavailable depending on API access
- Predictions are probabilistic and should not be used for gambling

## Contributing

Feel free to fork this repository and submit pull requests. Some ideas for improvement:
- Add more features (injuries, weather, referee stats)
- Implement neural network models
- Add live match tracking
- Improve visualization of predictions

## License

This project is open source and available under the MIT License.

## Acknowledgments

- Data provided by [Football-Data.org](https://www.football-data.org/)
- Built with scikit-learn, XGBoost, and pandas

## Contact

For questions or suggestions, please open an issue on GitHub.
