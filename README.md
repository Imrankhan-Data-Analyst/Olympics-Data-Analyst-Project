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

## plt.figure(figsize=(12,6))
## plt.xticks(rotation=20)
## plt.title('Overall Participation by Country')
## sns.barplot(x=top_10_countries.index, y=top_10_countries, palette = 'pastel')

## <Axes: title={'center': 'Overall Participation by Country'}, xlabel='Team', ylabel='count'>

### 📊 Visualization:
![image](https://github.com/user-attachments/assets/ddb96763-9aec-4a2b-80b9-ef1c4a31cd5a)

## Key Issues Resolved:

### 85% medals missing (non-winners) → filtered

### 23% weight data missing → used sport averages

### Fixed 12 mismatched NOC codes (e.g., "SGP" vs "SIN" for Singapore)

# 3. 📊 Key Insights with Interactive Visuals
## A. 🏟️ Participation Trends
### 1. Top 10 Competing Nations

# Age Distribution of the participants

## plt.figure(figsize=(12, 6))
## plt.title("Age distribution of the athletes")
## plt.xlabel('Age')
## plt.ylabel('Number of participants')
## plt.hist(athletes_df['Age'], bins=np.arange(10, 80, 2), color='orange', edgecolor='white');

### 📊 Visualization:
![image](https://github.com/user-attachments/assets/a99b00f6-d93e-4aca-b9f6-6b6f097cea2c)

## Rank	Country	Athletes
### 1	USA	18,548
### 2	France	12,109
### 3	UK	11,482

# 2. ♀️ Gender Equality Journey
## Timeline of Female Participation:

## Pie plot for male and female athletes

## plt.figure(figsize=(12,6))
## plt.title('Gender Distribution')
## plt.pie(gender_counts, labels=gender_counts.index, autopct='%1.1f%%', startangle=150, shadow=True);

### 📊 Visualization:
![image](https://github.com/user-attachments/assets/2f1b89f8-2da6-4aed-b251-84d7a9c963ce)

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
## Sunburst Chart by Country & Sport:

## sns.set(style="darkgrid")
## plt.figure(figsize=(20, 10))
## sns.countplot(x='Year', data=womenOlympics, palette="Spectral")
## plt.title('Women participation')









## Text(0.5, 1.0, 'Women participation')

### 📊 Visualization:
![image](https://github.com/user-attachments/assets/1fc39552-0344-4e1d-af21-fbb871ec7609)

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

## part = womenOlympics.groupby('Year')['Sex'].value_counts()
## plt.figure(figsize=(20, 10))
## part.loc[:,'F'].plot()
## plt.title('plot of Female Athletes over time')

## Text(0.5, 1.0, 'plot of Female Athletes over time')

### 📊 Visualization:
![image](https://github.com/user-attachments/assets/e399a9d7-4890-473b-bd9c-514b3b31896b)

# C. 💪 Athlete Physique
## Height vs Weight by Sport
## Interactive 3D Plot:

### python
### import plotly.express as px
### px.scatter_3d(olympics.dropna(), x='Height', y='Weight', z='Age', 
### color='Sport', symbol='Sex')

# Plot for sporting_event


## plt.figure(figsize=(10,5))
## plt.tight_layout()
## sns.countplot(sporting_event)
## plt.title('Gold Medals for Athletes over 60 years')

## Text(0.5, 1.0, 'Gold Medals for Athletes over 60 years')

## 📊 Visualization:
![image](https://github.com/user-attachments/assets/094826f1-c62b-4a66-8eb7-e81f3d51b5c1)

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

## sns.barplot(x=team_names.value_counts().head(20), y=team_names.value_counts().head(20).index)

## plt.ylabel(None);
## plt.xlabel('Countrywise Medals for the year 2016');

## 📊 Visualization:
![image](https://github.com/user-attachments/assets/b79089ec-215d-420b-9ee4-0fbb8d14c456)

## Seaborn	Statistical plots	sns.violinplot(x='Sport', y='Age', data=olympics)

## plt.figure(figsize =(12, 10))
## axis = sns.scatterplot(x="Height", y="Weight", data=not_null_medals, hue="Sex")
## plt.title('Height vs Weight of Olympic Medalists')

## Text(0.5, 1.0, 'Height vs Weight of Olympic Medalists')

## 📊 Visualization:
![image](https://github.com/user-attachments/assets/732bd39d-aee1-4aae-a431-e7c2f87fae3a)

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
### git clone https://github.com/Imrankhan-Data-Analyst/olympics-analysis
### pip install -r requirements.txt
### jupyter notebook

# 🎯 Final Takeaways
## Key Findings:
## Gender Progress

### Female athlete participation has increased 20-fold since 1900.

## USA Dominance

### Leads historically in total athletes (18,000+) and gold medals (2,600+).

## Sport Specialization

### Physical/age demands vary significantly (e.g., gymnasts vs. marathon runners).

# Design Specifications:
## Color Palette:

### Primary: #1F77B4 (blue), #FF7F0E (orange), #2CA02C (green)

### Accents: #D62728 (red), #9467BD (purple)

# Typography:

## Headers: Bebas Neue

## Body: Open Sans

