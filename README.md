# 🏅 Tokyo Olympics 2021 — SQL Analytics Project

### 📊 SQLite-Mediated Data Analysis using Python | SQL | Pandas | Seaborn

This project explores the **Tokyo 2021 Olympics** dataset using **SQLite3** and **Python** for end-to-end data analysis.  
It demonstrates **database design, ERD modeling, complex SQL queries, and data visualization** — showcasing both **analytical** and **engineering** skills.

---

## 🎯 **Project Objective**

To perform comprehensive **SQL-based data analysis** of the 2021 Tokyo Olympics using **SQLite as the analytical engine** integrated with **Python (pandas)** — covering:
- Country-wise medal distribution and efficiency  
- Athlete-to-coach ratios and discipline participation  
- Gender-based participation and event insights  
- Data modeling through ERD and relational schema design  

---

## 🧱 **Database Design**

The project uses a **relational schema** built around a **Fact–Dimension model**:

- **Fact Table** → `Medals`  
- **Dimension Tables** → `Athletes`, `Coaches`, `Teams`, `EntriesGender`

### 🔗 Schema Relationships:
- `Athletes.NOC`, `Coaches.NOC`, `Teams.NOC` → **Foreign Keys →** `Medals("Team/NOC")`  
- `Athletes.Discipline`, `Coaches.Discipline`, `Teams.Discipline` → **Foreign Keys →** `EntriesGender(Discipline)`

---

## 🧩 **Entity Relationship Diagram (ERD)**

ERD created using **eralchemy2** and  **Graphviz**.

 

🟨 **Fact Table:** Medals  
🟦 **Dimension Tables:** Athletes, Coaches, Teams, EntriesGender  


---

## ⚙️ **Tech Stack**

| Tool | Purpose |
|------|----------|
| 🐍 **Python 3.12+** | Main programming language |
| 🗄️ **SQLite3** | Lightweight relational database engine |
| 🧠 **Pandas** | SQL mediation + data manipulation |
| 📈 **Matplotlib / Seaborn** | Data visualization |
| 🧩 **eralchemy2 / Graphviz** | ERD generation and schema visualization |

---

## 🧮 **Analytical Focus Areas**

### 1️⃣ Medal Analytics
- Country-wise gold, silver, bronze, and total medals  
- Medal efficiency (Medals per Athlete)  
- Medal distribution by discipline and gender

### 2️⃣ Participation Insights
- Gender distribution (Male vs Female)  
- Most popular sports by participation  
- Discipline-wise representation by country  

### 3️⃣ Performance Metrics
- Coach-to-Athlete ratio per country and discipline  
- Countries with most diverse disciplines  
- Medal share % by region and team size  

---

## 🧠 **Key SQL Highlights**

- **Aggregations & Joins**
  ```sql
  SELECT a.NOC AS Country, COUNT(a.Name) AS Total_Athletes, 
         COUNT(DISTINCT c.Name) AS Total_Coaches,
         ROUND(100.0 * COUNT(DISTINCT c.Name)/COUNT(DISTINCT a.Name), 2) AS Coach_Athlete_Percentage
  FROM Athletes a
  JOIN Coaches c ON a.NOC = c.NOC AND a.Discipline = c.Discipline
  GROUP BY a.NOC
  ORDER BY Coach_Athlete_Percentage DESC;

- ### Gender Participation
 SELECT e.Discipline, e.Female, e.Male, 
       ROUND(100.0 * e.Female / e.Total, 2) AS Female_Percentage
FROM EntriesGender e
ORDER BY Female_Percentage DESC;

- ### Medal Efficiency
  SELECT m."Team/NOC" AS Country, m.Total AS Total_Medals,
       COUNT(DISTINCT a.Name) AS Total_Athletes,
       ROUND(1.0 * m.Total / COUNT(DISTINCT a.Name), 3) AS Medal_Efficiency
FROM Medals m
JOIN Athletes a ON a.NOC = m."Team/NOC"
GROUP BY m."Team/NOC"
ORDER BY Medal_Efficiency DESC;

### 🗃️ Dataset Description

All datasets were sourced from Kaggle’s Tokyo 2021 Olympics Dataset and include:

### Table	Description
Athletes	Names, NOC, and Discipline of competitors
Coaches	Coaching staff details by NOC and sport
EntriesGender	Gender-based participation by discipline
Medals	Country-wise medal counts (Gold, Silver, Bronze, Total)
Teams	Team-level participation and events


### 🧩 Schema Creation Code Snippet
CREATE TABLE Athletes (
  Name TEXT,
  NOC TEXT,
  Discipline TEXT,
  FOREIGN KEY (NOC) REFERENCES Medals("Team/NOC"),
  FOREIGN KEY (Discipline) REFERENCES EntriesGender(Discipline)
);

### 🚀 Project Workflow

1️⃣ Load data from Kaggle CSVs into pandas
2️⃣ Store each dataset as a SQLite table
3️⃣ Define relationships & generate ERD
4️⃣ Perform SQL-based analysis with pandas
5️⃣ Visualize key findings using seaborn/matplotlib
6️⃣ Document insights and results


### 🧾 Key Insights

--USA led in total medals and had one of the best medal efficiencies.
-- Athletics and Swimming were the top disciplines by athlete count.
-- Spain had the highest number of coaches per discipline.
-- Gender participation was nearly balanced in most team sports.
-- Small countries like San Marino had high medal efficiency despite few athletes.




### 🏁 Conclusion

This project demonstrates complete end-to-end SQL analytics using SQLite3 as the database engine and Python as the execution and visualization layer, showcasing the full workflow expected in modern data analytics. By integrating multiple Olympic datasets—Athletes, Coaches, Teams, Medals, and Gender Entries—I designed a relational database with proper foreign-key relationships and produced a clean, analysis-ready data model.

Through advanced SQL queries and exploratory analysis, several clear insights emerged:

The United States, China, and Japan dominated in medal performance, with the USA leading both total medals and overall athletic representation.

Team sports like Basketball, Football, and Hockey showed high coach-to-athlete ratios, highlighting greater support requirements.

Medal efficiency analysis revealed that smaller nations such as San Marino and Bermuda had exceptional performance relative to their athlete counts.

Gender distribution showed strong participation in Athletics and Swimming, with discipline-level comparisons uncovering variations in male vs. female representation.

Country-wise discipline participation highlighted how different nations focus on distinct sporting strengths.

Overall, the project effectively bridges data engineering (schema design, ERD creation, database modeling), data analytics (complex joins, aggregations, ratios, performance metrics), and visualization (Python, Seaborn, Graphviz). It showcases my ability to manage structured datasets end-to-end, derive meaningful insights, and present them clearly—making it a strong portfolio piece for data analyst and business intelligence roles.
