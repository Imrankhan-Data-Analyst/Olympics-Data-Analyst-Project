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

