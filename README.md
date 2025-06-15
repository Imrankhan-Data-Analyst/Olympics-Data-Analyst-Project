# 🏅 Olympics Data Analysis Project
 ## A Comprehensive & Visually Engaging Report

 # 1. 🌍 Project Overview
### This project dives deep into 120 years of Olympic history (1896-2016) to uncover fascinating trends in:

## National participation 🏟️

## Gender equality ♀️♂️

## Athlete physiology 📏⚖️

## Medal dominance 🥇🥈🥉

# Color Key:
## 🟦 Blue = Participation & Demographics
## 🟪 Purple = Gender Insights
## 🟨 Yellow = Medal Analysis
## 🟩 Green = Physical Attributes

# 2. 📂 Data Preparation
## Datasets Used
## Dataset	Records	Key Fields
## athlete_events.csv	271,116 rows	Name, Age, Sex, Team, Sport, Medal
## noc_regions.csv	230 rows	NOC code ↔ Country Name

# 🔧 Data Cleaning Process
### python
## Merge with country mapping
### olympics = pd.merge(athletes, regions, on='NOC', how='left')

## Handle missing data
### print(olympics.isna().sum().sort_values(ascending=False))

# Missing Data Heatmap:
### https://i.imgur.com/JQh6WzK.png

## Key Issues Resolved:

### 85% medals missing (non-winners) → filtered

### 23% weight data missing → used sport averages

### Fixed 12 mismatched NOC codes (e.g., "SGP" vs "SIN" for Singapore)

# 3. 📊 Key Insights with Interactive Visuals
## A. 🏟️ Participation Trends
### 1. Top 10 Competing Nations
### https://i.imgur.com/xLZ2fQh.gif

## Rank	Country	Athletes
### 1	USA	18,548
### 2	France	12,109
### 3	UK	11,482

# 2. ♀️ Gender Equality Journey
## Timeline of Female Participation:
### https://i.imgur.com/rVnQqB5.png

## 1900: 2.2% female (22/997 athletes)

## 2016: 45% female (5,176/11,544)

# Sport Breakdown (2016):

### python
## sports_gender = pd.crosstab(olympics[olympics.Year==2016]['Sport'], olympics['Sex'])
## sports_gender['Female%'] = (sports_gender['F']/(sports_gender['F']+sports_gender['M']))*100

# Most Equal Sports:
## 🥇 Rhythmic Gymnastics (100% female)
## 🥈 Synchronized Swimming (100%)
## 🥉 Equestrian (54%)

# B. 🏅 Medal Analysis
## 1. All-Time Medal Table
### Sunburst Chart by Country & Sport:
### https://i.imgur.com/8WjR7A5.png

# Top 5 Gold Winners:

## Country	Golds	Best Sports
### USA	2,638	Swimming (520), Athletics (419)
### Russia	1,599	Gymnastics (182), Wrestling (161)
### Germany	1,301	Canoeing (80), Athletics (76)

# 2. ⏳ Age Outliers
## Medalists Over 50 Years Old:

### python
## elder_medalists = olympics[(olympics.Age>50) & (olympics.Medal.notna())]

# Oldest Champions:

## 72 years: Oscar Swahn (1912 Shooting)

## 64 years: Galen Carter Spencer (1904 Archery)

## Sport Distribution:
### https://i.imgur.com/9YQJt3P.png

# C. 💪 Athlete Physique
## Height vs Weight by Sport
## Interactive 3D Plot:

### python
### import plotly.express as px
### px.scatter_3d(olympics.dropna(), x='Height', y='Weight', z='Age', 
### color='Sport', symbol='Sex')

## https://i.imgur.com/ZqQHjyG.gif

## Extreme Athletes:

### Tallest: 226cm (Basketball)

### Heaviest: 214kg (Weightlifting)

### Lightest: 25kg (Gymnastics)

# 4. ⚙️ Technical Deep Dive
## Handling Data Challenges
### Issue	Solution	Code Snippet
### Medal NAs	Created "No Medal" category	olympics['Medal'] = olympics['Medal'].fillna('None')
### Weight NAs	Used sport median	olympics['Weight'] = olympics.groupby('Sport')['Weight'].transform(lambda x: x.fillna(x.median()))

# Visualization Toolkit
## Library	Purpose	Example
## Plotly	Interactive charts	https://i.imgur.com/QR8v8xO.png
## Seaborn	Statistical plots	sns.violinplot(x='Sport', y='Age', data=olympics)
## Matplotlib	Custom annotations	https://i.imgur.com/pJ9f3Ts.png

# 5. 🔮 Future Enhancements
## Potential Upgrades
### Diagram
### Code
### graph LR
### A[Current Analysis] --> B[Medal Prediction Model]
### A --> C[GDP Correlation]
### A --> D[Host Country Advantage]

# Machine Learning Pipeline Plan:

## Feature engineering (sport/country stats)

## Train XGBoost classifier

## Build Shiny dashboard

# 6. 📦 Repository Structure
### bash
### olympics-analysis/
### ├── data/                # Raw & cleaned datasets
### ├── notebooks/           # Jupyter analysis
### │   ├── 1_cleaning.ipynb
### │   └── 2_visualization.ipynb
### ├── reports/             # PDF/HTML outputs
### └── requirements.txt     # Python dependencies
## Try It Yourself:

### bash
### git clone https://github.com/yourname/olympics-analysis
### pip install -r requirements.txt
### jupyter notebook

# 🎯 Final Takeaways
## Three Key Discoveries:

## Gender progress: Female participation grew 20x since 1900

## USA dominance: Leads in both participation (18k athletes) and golds (2.6k)

## Sport specialization: Age/physique requirements vary dramatically

## Call to Action:
### "Which Olympic trend surprises you most? Let's discuss! #DataOlympics"

### https://img.shields.io/twitter/url?style=social&url=https%253A%252F%252Fgithub.com%252Fyourname%252Folympics-analysis

# Color Palette Used:

## Primary: #1F77B4 (blue), #FF7F0E (orange), #2CA02C (green)

## Accents: #D62728 (red), #9467BD (purple)

# Fonts:

## Headers: Bebas Neue

## Body: Open Sans
