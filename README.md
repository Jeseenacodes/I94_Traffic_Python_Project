# Interstate 94 Traffic Volume Analysis 🚗

An exploratory data analysis (EDA) investigating key indicators that predict heavy traffic on Interstate 94, including temporal patterns, seasonal trends, and weather conditions.

**Dataset:** Metro Interstate Traffic Volume  
**Period:** October 2, 2012 – September 30, 2018 (6+ years)  
**Records:** 48,204 hourly observations  
**Location:** Minneapolis-St. Paul, Minnesota

---

## 📊 Project Overview

This project analyzes over six years of hourly traffic and weather data to identify what actually drives traffic congestion on I-94. Through exploratory data analysis, the project challenges common assumptions and reveals surprising patterns in traffic behavior.

### Key Question
**What predicts heavy traffic on I-94?** Time of day? Weather? Season? Or something else?

### Main Finding
**Time of day and day of week are the strongest predictors.** Weather, surprisingly, is weak—with surprising nuance in how specific weather combinations drive traffic behavior.

---

## 🔍 Key Findings

### 1. **Time of Day: The Strongest Indicator** ⏰
- **Weekday rush hours** (7 AM & 4 PM): **6,000+ cars/hour**
- **Off-peak hours**: 4,200-5,000 cars/hour
- **Pattern**: Sharp spikes during commute times, gradual decline through evening

### 2. **Day of Week: A Clear Binary Split** 📅
- **Weekdays (Mon–Fri)**: 5,000–5,300 cars/hour average
- **Weekends (Sat–Sun)**: 3,400–3,900 cars/hour average
- **Gap**: ~30% lower traffic on weekends; no rush-hour spikes

### 3. **Seasonality: Behavior, Not Temperature** 🌡️
- **Warm months** (Mar–Oct): 4,900–4,930 cars/hour
- **Cold months** (Nov–Feb): 4,380–4,720 cars/hour
- **Temperature correlation**: +0.128 (weakest predictor)
- **Why**: Reflects behavior (remote work, activity levels) not thermometers

### 4. **Weather: Combination Effects Matter** 🌧️
| Weather Event | Avg Traffic | Correlation |
|---|---|---|
| Rain + Snow | **5,167 cars/hour** | N/A |
| Snow Only | 2,788 cars/hour | +0.001 |
| Rain Only | 3,290 cars/hour | +0.004 |
| Temperature | — | +0.128 |
| Cloud Cover | — | −0.033 |

**Key Insight**: Rain + snow together produce 85% more traffic than snow alone, suggesting people drive when conditions feel manageable (even if ambiguous) but stay home when conditions feel dangerous.

### 5. **Holiday Effect** 🎄
- Limited holiday records in the dataset (only 61 non-null entries at midnight)
- Non-holiday daytime traffic: median ~4,800 cars/hour, IQR 4,200–5,500

---

## 📈 Data Overview

### Dataset Structure
```
Total Records:     48,204
Columns:           9
Date Range:        2012-10-02 to 2018-09-30
Traffic Volume:    0 – 7,280 cars/hour
Mean Traffic:      3,260 cars/hour
```

### Features
| Feature | Type | Description | Completeness |
|---|---|---|---|
| `date_time` | DateTime | Hour of observation | 100% |
| `traffic_volume` | Integer | Cars/hour | 100% |
| `holiday` | String | Holiday name (if applicable) | 0.1% |
| `temp` | Float | Temperature (K) | 100% |
| `rain_1h` | Float | Rainfall in 1h (mm) | 100% |
| `snow_1h` | Float | Snowfall in 1h (mm) | 100% |
| `clouds_all` | Integer | Cloud cover (%) | 100% |
| `weather_main` | String | Primary weather type | 100% |
| `weather_description` | String | Detailed weather description | 100% |

### Data Quality Notes
- ✅ All columns fully populated except `holiday` (61/48,204 non-null = expected)
- ✅ No missing traffic volume data
- ✅ Consistent hourly intervals across 6+ years
- ⚠️ July 2016 anomaly: Sharp drop to ~3,950 cars/hour (attributed to Westbound I-94 construction)

---

## 🎯 Analysis Highlights

### Traffic Distribution
- **Bimodal distribution**: 
  - Peak 1: 0–500 cars/hour (~8,100 occurrences) — nighttime
  - Peak 2: 4,500–5,000 cars/hour (~7,900 occurrences) — daytime
  
### Day vs. Night Split
| Metric | Daytime (7 AM–7 PM) | Nighttime (7 PM–7 AM) |
|---|---|---|
| Mean Traffic | 4,762 cars/hour | 1,785 cars/hour |
| 75th Percentile | 4,252 cars/hour | 2,819 cars/hour |
| Distribution | Left-skewed (consistently high) | Right-skewed (mostly low) |

### Hourly Patterns (Daytime)
```
Hour    Weekday Traffic    Weekend Traffic
07:00   ~6,000 (peak)      ~3,200
10:00   ~5,200             ~3,800
13:00   ~5,100             ~4,200
16:00   ~6,200 (peak)      ~4,100
19:00   ~5,800             ~3,900
```

### Monthly Seasonality
```
Month      Avg Traffic
January    4,450
March      4,900
July       4,900 (3,950 in 2016 due to construction)
October    4,930
November   4,380
```

---

## 💡 Key Insights & Implications

### For Commuters
- ✅ **Predictability is your best friend**: Rush hours (7–9 AM, 3–5 PM weekdays) are reliably heavy
- ✅ **Flexibility wins**: Commute outside peak hours or use weekends for errands
- ✅ **Weather shouldn't scare you**: Rain or light snow has minimal impact on traffic
- ✅ **Remote work options**: Cold months naturally have 12% lower traffic

### For Urban Planners & Infrastructure Managers
- 📍 **Rush hour optimization has high ROI**: Even small shifts in peak traffic timing could materially reduce congestion
- 📍 **Weekday/weekend capacity should differ**: 30% gap justifies flexible capacity management
- 📍 **Weather prediction ≠ Traffic prediction**: Near-zero correlations suggest weather-based models may overfit
- 📍 **Seasonality is behavioral**: Remove barriers to winter commuting (maintenance, transit reliability) to smooth traffic

### For Data Scientists & Analysts
- 🔬 **Bimodal distributions justify stratified analysis**: Day/night split revealed cleaner patterns
- 🔬 **Interaction effects matter**: Rain + snow combinations are more predictive than individual metrics
- 🔬 **Detailed categories > broad categories**: Specific weather descriptions outperformed weather types
- 🔬 **Weak correlations ≠ no pattern**: Temporal and categorical patterns complement correlational analysis

---

## 📁 Project Structure

```
I-94-Traffic-Analysis/
├── README.md                    # This file
├── data/
│   └── metro_traffic_volume.csv # Raw dataset (48,204 rows × 9 columns)
├── analysis/
│   ├── eda.ipynb               # Exploratory Data Analysis
│   ├── traffic_by_time.py      # Hourly & daily patterns
│   ├── seasonality.py          # Monthly & seasonal analysis
│   └── weather_analysis.py     # Weather impact analysis
├── visualizations/
│   ├── traffic_distribution.png
│   ├── day_vs_night.png
│   ├── hourly_patterns.png
│   ├── monthly_trends.png
│   └── weather_comparison.png
├── reports/
│   ├── findings_summary.md     # Key findings document
│   ├── medium_blog.md          # Full Medium article
│   └── linkedin_posts.md       # Social media posts
└── requirements.txt            # Python dependencies
```

---

## 🛠️ Getting Started

### Prerequisites
- Python 3.7+
- Pandas, NumPy, Matplotlib, Seaborn
- Jupyter Notebook (for EDA)

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/I-94-Traffic-Analysis.git
   cd I-94-Traffic-Analysis
   ```

2. **Create a virtual environment**
   ```bash
   python -m venv venv
   source venv/bin/activate  # On Windows: venv\Scripts\activate
   ```

3. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

4. **Run the analysis**
   ```bash
   jupyter notebook analysis/eda.ipynb
   ```

### Quick Analysis

```python
import pandas as pd
import matplotlib.pyplot as plt

# Load data
df = pd.read_csv('data/metro_traffic_volume.csv')

# Split day/night
daytime = df[(df['hour'] >= 7) & (df['hour'] < 19)]
nighttime = df[(df['hour'] < 7) | (df['hour'] >= 19)]

# Compare patterns
print(f"Daytime mean: {daytime['traffic_volume'].mean():.0f} cars/hour")
print(f"Nighttime mean: {nighttime['traffic_volume'].mean():.0f} cars/hour")

# Visualize
daytime.groupby('hour')['traffic_volume'].mean().plot()
plt.xlabel('Hour of Day')
plt.ylabel('Traffic Volume')
plt.title('Daytime Traffic Pattern')
plt.show()
```

---

## 📊 Visualizations

### Traffic Distribution
<img width="819" height="639" alt="image" src="https://github.com/user-attachments/assets/5694d379-a1dc-4338-8a31-fa865b1d20aa" />

### Day vs. Night
<img width="1300" height="429" alt="image" src="https://github.com/user-attachments/assets/979b5108-1703-4016-afb1-833920755bf7" />

### Hourly Patterns
<img width="830" height="1105" alt="image" src="https://github.com/user-attachments/assets/b931f15d-ff59-4922-91ca-5a55c8b585f6" />

### Monthly Trends
<img width="2004" height="563" alt="image" src="https://github.com/user-attachments/assets/ea14fb22-79a1-425a-b7fd-ec6020000565" />

### Weather Impact
<img width="1844" height="897" alt="image" src="https://github.com/user-attachments/assets/cdbfa916-c523-41b0-a05a-4c7a55617ed2" />

<img width="645" height="436" alt="image" src="https://github.com/user-attachments/assets/18b944b8-991a-4c96-b264-82818be6911d" />


---

## 📚 Key Statistics

### Correlation Analysis
| Variable | Correlation with Traffic | Strength |
|---|---|---|
| Hour of Day | N/A | ✅ Very Strong (patterns) |
| Day of Week | N/A | ✅ Strong (30% variation) |
| Month | N/A | ✅ Moderate (11% variation) |
| Temperature | +0.128 | ❌ Weak |
| Rain (1h) | +0.004 | ❌ Negligible |
| Snow (1h) | +0.001 | ❌ Negligible |
| Cloud Cover | −0.033 | ❌ Negligible |

### Traffic Volume by Category
| Category | Mean | Median | Std Dev | Min | Max |
|---|---|---|---|---|---|
| All Data | 3,260 | 3,260 | 1,986 | 0 | 7,280 |
| Daytime | 4,762 | 4,827 | 1,074 | 1,120 | 7,280 |
| Nighttime | 1,785 | 1,675 | 1,239 | 0 | 6,823 |
| Weekday | 4,910 | 5,074 | 1,037 | 1,154 | 7,280 |
| Weekend | 3,662 | 3,622 | 1,388 | 0 | 6,949 |

---

## 🔬 Methodology

### Analysis Approach
1. **Data Cleaning**: Validation, handling missing values, outlier identification
2. **Exploratory Analysis**: Distribution analysis, temporal patterns, categorical breakdown
3. **Stratification**: Separated day/night, weekday/weekend for cleaner patterns
4. **Correlation Analysis**: Computed Pearson correlations for numeric variables
5. **Pattern Recognition**: Identified trends in hourly, daily, monthly, and seasonal dimensions
6. **Behavioral Insights**: Interpreted statistical findings through a behavioral lens

### Tools Used
- **Pandas**: Data manipulation and aggregation
- **NumPy**: Numerical computations
- **Matplotlib & Seaborn**: Visualization
- **Jupyter**: Interactive analysis and documentation
- **Python**: Analysis scripting

---

## 📖 Read More

### Full Reports
- 📄 **Medium Article**: 


### Key Takeaway
**Time and behavior drive traffic. Weather plays a supporting role.** Understanding when and why people commute is more valuable than predicting weather.

---

## 🎓 Limitations & Future Work

### Current Limitations
- ⚠️ **Aggregate data**: Cannot distinguish eastbound vs. westbound traffic
- ⚠️ **No external factors**: Missing special events, incidents, transit strikes, economic data
- ⚠️ **Limited holiday data**: Only 61 holiday records at midnight
- ⚠️ **Pre-COVID**: Data ends Sept 2018; remote work trends post-2020 not captured

### Future Directions
1. **Predictive Modeling**: Train ML models (Random Forest, LSTM) to forecast traffic
2. **Causal Analysis**: Investigate causation vs. correlation for weather effects
3. **Geospatial Analysis**: Compare patterns across different locations on I-94
4. **Real-time Apps**: Develop traffic prediction tools for commuter decision-making
5. **Behavioral Studies**: Integrate with survey data on commute choices
6. **Scenario Testing**: Model impact of flexible work hours, toll pricing, transit investments

---

## 📄 Data Source

**Metro Interstate Traffic Volume Dataset**  
Source: UCI Machine Learning Repository  
License: CC0 Public Domain  

Data collected from ASOS (Automated Surface Observing System) stations and traffic sensors on I-94 near Minneapolis-St. Paul.

**Original Dataset**: [UCI ML Repository - Metro Interstate Traffic Volume](https://archive.ics.uci.edu/dataset/492/metro+interstate+traffic+volume)

---

## 👤 Author

**Jeseena Parveen K.**  
Data Analyst  
LinkedIn: [@jeseena-parveen-k](https://www.linkedin.com/in/jeseena-parveen-k/)

---

## 📜 License

This project is released under the MIT License. See LICENSE file for details.

---

## 🤝 Contributing

Contributions are welcome! Please feel free to:
- Report bugs or issues
- Suggest improvements
- Submit pull requests with enhancements
- Share new analyses or visualizations

To contribute:
1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## ❓ FAQ

**Q: Why is weather such a weak predictor?**  
A: Weather metrics (temperature, rain, snow) show weak linear correlations, but combinations and specific descriptions matter. More importantly, traffic is primarily driven by when people work (commute times) rather than weather conditions.

**Q: Can I use this to predict traffic?**  
A: This EDA identifies patterns; a predictive model would require ML methods (time series, LSTM, Random Forest). The strong time-based patterns suggest any model should heavily weight hour and day of week.

**Q: Is this data still relevant?**  
A: The dataset ends in Sept 2018 (pre-COVID). Post-pandemic, remote work may reduce rush-hour peaks. However, the temporal and behavioral patterns are likely still dominant predictors.

**Q: Can I apply this to other highways?**  
A: Possibly! The methodology is generalizable, but specific patterns (when people commute, seasonal behavior) will vary by location. I-94 serves Minneapolis-St. Paul; your highway may have different patterns.

**Q: Why focus on daytime traffic?**  
A: Nighttime traffic is mostly low and less relevant to "heavy traffic" questions. The bimodal distribution justified splitting the analysis for cleaner daytime patterns.

---

## 📧 Contact

Questions or feedback? Reach out via:
- **LinkedIn**: [@jeseena-parveen-k](https://www.linkedin.com/in/jeseena-parveen-k/)

---

**Last Updated**: March 2024  
**Data Period**: October 2012 – September 2018  
**Analysis Type**: Exploratory Data Analysis (EDA)
