# 911-Calls-Data-Analysis-Capstone-Project

## 📌 Introduction
This project explores and analyzes a dataset of **911 emergency calls** from Montgomery County, Pennsylvania, USA. The goal is to uncover patterns and trends in emergency incidents using Python data analysis techniques and data visualization.  
The analysis also demonstrates practical skills in **data wrangling**, **exploratory data analysis (EDA)**, **time series analysis**, and **visual storytelling**.

---

## 🚨 Problem Statement
Emergency call centers handle thousands of calls daily, but without proper analysis, decision-makers may struggle to:
- Understand the most common emergencies.
- Allocate resources effectively.
- Identify seasonal or time-based patterns in emergency incidents.

This project analyzes over **600,000 records** of 911 calls to answer key questions such as:
- Which zip codes and townships have the highest number of calls?
- What are the most common reasons for calling 911?
- How do emergencies vary by time of day, day of week, and month?
- Are there visible trends or seasonal variations in emergencies?

---

## 🛠 Skills Demonstrated
- **Data Cleaning & Preprocessing** (handling missing values, feature extraction)
- **Exploratory Data Analysis (EDA)** using `pandas`, `numpy`
- **Data Visualization** with `matplotlib` and `seaborn`
- **Time Series Analysis** (trend detection, aggregation)
- **Feature Engineering** from datetime data
- **Grouping & Aggregation** in pandas
- **Visual Pattern Recognition** (heatmaps, clustermaps)

---

## 📂 Data Sourcing
The dataset was obtained from [Kaggle – Montco 911 Calls](https://www.kaggle.com/mchirico/montcoalert).  
It contains real emergency call data from Montgomery County, Pennsylvania.

---

## 📊 Data Description
The dataset includes the following columns:

| Column     | Description |
|------------|-------------|
| `lat`      | Latitude of the incident |
| `lng`      | Longitude of the incident |
| `desc`     | Description of the emergency call |
| `zip`      | Zip code of the incident |
| `title`    | Emergency title, including the reason and type |
| `timeStamp`| Date and time of the call |
| `twp`      | Township where the incident occurred |
| `addr`     | Address of the incident |
| `e`        | Dummy variable (always 1) |

---

## 🧹 Data Preparation
The following steps were performed during data preparation:
1. **Loaded the dataset** into pandas DataFrame.
2. **Checked data types** and converted `timeStamp` to datetime objects.
3. **Extracted new features**: `Hour`, `Month`, `DayOfWeek`.
4. **Mapped** `DayOfWeek` numeric values to weekday names.
5. **Created a new column `Reason`** by extracting the category from the `title` column (EMS, Fire, or Traffic).
6. **Handled missing values** in the `zip` column.

---

## ❓ Questions & Answers

### 1️⃣ What are the top 5 zip codes for 911 calls?

- 19401.0 45606
- 19464.0 43910
- 19403.0 34888
- 19446.0 32270
- 19406.0 22464

**Interpretation:** Zip code **19401** (Norristown area) had the highest number of emergency calls.

---

### 2️⃣ What are the top 5 townships for 911 calls?
- LOWER MERION 55490
- ABINGTON 39947
- NORRISTOWN 37633
- UPPER MERION 36010
- CHELTENHAM 30574

**Interpretation:** **Lower Merion Township** recorded the highest number of emergency calls.

---

### 3️⃣ What are the most common reasons for a 911 call?

```python

# Create new column 'Reason' by splitting the title column
df['Reason'] = df['title'].apply(lambda x: x.split(':')[0])
# Most common Reason for a 911 call
most_common_reason = df['Reason'].value_counts()
#print("Most Common Reasons:\n", most_common_reason)
# Plotting count of 911 calls by Reason with percentage labels
plt.figure(figsize=(12, 6))
ax = sns.countplot(data=df, x='Reason', palette='viridis')

# Calculate total for percentage computation
total = len(df)

# Annotate each bar with percentage
for p in ax.patches:
    count = p.get_height()
    percentage = f'{100 * count / total:.1f}%'
    ax.annotate(
        percentage, 
        (p.get_x() + p.get_width() / 2., count),  # position at the center top of the bar
        ha='center', 
        va='bottom', 
        fontsize=11, 
        color='black', 
        xytext=(0, 5),  # offset slightly above the bar
        textcoords='offset points'
    )

plt.title("Count of 911 Calls by Reason")
plt.tight_layout()
plt.show()

```

📷 ![](Count_of_911_Calls_by_Reason.png)
- EMS 332692
- Traffic 230208
- Fire 100622

**Note:**  
- **EMS** stands for *Emergency Medical Services*, which includes incidents like cardiac arrests, injuries, and other medical emergencies.
- Traffic calls include road accidents, hazards, and congestion issues.
- Fire calls include building fires, gas leaks, and hazardous material incidents.

**Interpretation:** The majority of calls were for **medical emergencies (EMS)**, followed by traffic-related incidents.

---

### 4️⃣ How do emergency calls vary by day of week?
📷 ![](911_Calls_by_Day_of_Week.png)

---

### 5️⃣ How do emergency calls vary by month?
📷 ![](911_Calls_by_Month.png)

---

### 6️⃣ What trends exist in 911 calls per month?
📷 ![](911_Calls_per_Month.png)

---

### 7️⃣ What does the daily trend of calls look like by reason?
📷 ![](911_Calls_Per_Day_by_Reason.png)

---

### 8️⃣ What patterns exist in 911 calls by hour and day of week? (Heatmap)
📷 ![](Heatmap_of_911_Calls_by_Hour_and_Day_of_Week)

---

### 9️⃣ What patterns exist in 911 calls by month and day of week? (Clustermap)
📷 ![](Clustermap_of_911_Calls_by_Month_and_Day_of_Week)

---

## 📈 Interpretation of Results
- Medical emergencies (EMS) dominate 911 calls, indicating the need for strong health response units.
- Certain zip codes and townships have significantly higher call volumes, suggesting the need for resource prioritization.
- Time-based trends show peak call hours during daytime and weekdays.
- Seasonal patterns suggest possible correlations between certain emergencies and specific months.

---

## 💡 Recommendations
1. **Allocate more EMS resources** to high-volume zip codes and townships.
2. **Deploy targeted traffic safety measures** in regions with high traffic-related call volumes.
3. **Prepare for seasonal spikes** in certain emergencies by analyzing month-specific patterns.
4. **Improve public awareness programs** to reduce non-critical calls.

---

## 🏁 Conclusion
This analysis provides valuable insights into the patterns and trends in 911 emergency calls for Montgomery County, PA.  
By understanding when, where, and why emergencies occur most frequently, emergency response teams can improve **resource allocation**, **response time**, and **public safety strategies**.

---

