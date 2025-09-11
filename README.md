# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To identify the most in-demand skills for the top three data roles, I filtered the positions based on their popularity and then extracted the five key skills for each role. This query highlights the most common job titles along with their top skills, making it clear which skills I should prioritize depending on the role I aim for.

You can view my notebook with the detailed steps here:
[2_skill_demand.ipynb](./File%20Python/py_with_lukebarousse/project_course/3_project/2_skill_demand.ipynb)

### Visualize Data

```python
fig, ax = plt.subplots(len(job_title), 1)

sns.set_theme(style='ticks')
for i, title in enumerate(job_title): #enumerate to get index
  df_plot = df_skills_perc[df_skills_perc['job_title_short'] == title].head(5)
  sns.barplot(data=df_plot, x='skill_perc', y='job_skills', ax=ax[i], hue='skills_count', legend=False, palette='dark:b_r')
  ax[i].set_title(job_title[i])
  ax[i].set_ylabel('')
  ax[i].set_xlabel('')
  ax[i].set_xlim(0, 78)

  for n, v in enumerate(df_plot['skill_perc']):
    ax[i].text(v +1, n, f'{v:.0f}%', va='center')

  if i != len(job_title) -1:
    ax[i].set_xticks([])


sns.despine()
fig.suptitle('Likelihood of Skills Requested in Indonesia Job Postings', fontsize=14)
fig.tight_layout(h_pad=1)
```

### Result

![Visualization of top skills for data roles](./File%20Python/py_with_lukebarousse/project_course/3_project/images/2/skill_demand_ID.png)

### Insight

Data Analyst

- SQL (49%) is the most demanded, reflecting the need for strong querying and data wrangling skills.
- Python (32%) is becoming important, showing a shift toward automation and advanced analysis.
- Excel (31%) remains highly relevant for day-to-day business reporting.
- Tableau (25%) and R (17%) are valued for visualization and statistical tasks but less central.

Data Engineer

- SQL (57%) and Python (44%) are core, showing the foundation in databases and programming.
- Big data & cloud tools: Spark (23%), AWS (22%), and Hadoop (20%) highlight the demand for distributed processing and cloud-based data management.
- This role emphasizes infrastructure, scalability, and data pipelines.

Data Scientist

- Python (53%) is the top skill, reinforcing its role in modeling, ML, and data analysis.
- SQL (49%) shows that database querying is still essential.
- R (35%) supports statistical analysis and research-oriented work.
- Visualization tools: Tableau (17%) is relevant but less dominant than in Analyst roles.
- Spark (14%) indicates some overlap with engineering for handling large datasets.

#### Key Takeaways

- SQL and Python are universal skills across all three roles, forming the core foundation for anyone pursuing a data career in Indonesia.
- Analysts still rely heavily on Excel and Tableau, but Python is increasingly important.
- Engineers are expected to master big data and cloud ecosystems (Spark, AWS, Hadoop), in addition to SQL/Python.
- Scientists need strong programming and statistical skills (Python, R), with some demand for big data tools like Spark.
- Compared to US job postings, Indonesia shows a stronger reliance on Excel for Analysts and Hadoop for Engineers, reflecting slightly different market maturity and tool adoption.

## 2. How are in-demand skills trending for Data Analysts?

### Visualize Data

```python
sns.lineplot(data=df_plot, dashes=False, palette='tab10')

plt.title('Trending Top Skills for Data Analysts in Indonesia')
plt.ylabel('Likelihood in Job Posting')
plt.xlabel('2023')
plt.legend().remove()

for i in range(5):
  plt.text(11.2, df_plot.iloc[-1, i], df_plot.columns[i])

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))


```

### Result

![Trending Top Skills for Data Analysts in Indonesia](./File%20Python/py_with_lukebarousse/project_course/3_project/images/3/skill_trend_DA_ID.png)

### Insight

Skill Trends

SQL

- Consistently the top skill throughout the year, peaking above 65% in Feb–Mar.
- Dips mid-year but recovers toward the end (~50% in Dec).
- Reinforces SQL as the core competency for Data Analysts.

Excel

- Shows relatively stable demand (25–40%).
- Peaked around Aug–Sep (~43%), reflecting its importance for reporting and business tasks.
- Remains a strong baseline tool for analysts.

Python

- Gradual rise across the year, fluctuating between 25–40%.
- Gained more traction in the second half of 2023, showing a shift toward automation and advanced analytics.

Tableau

- Fluctuates heavily (15–30%).
- Saw a mid-year dip but recovered slightly toward the end.
- Suggests visualization skills are valued but less consistently required.

R

- Lowest demand, generally below 20%.
- Early-year spike (~35% in Feb) but dropped sharply afterward.
- Indicates that R is niche, mostly for specialized statistical roles rather than mainstream analyst positions.

#### Key Takeaways

For Data Analysts in Indonesia:

- SQL remains king — must-have skill across all months.
- Excel is stable and reliable, reflecting its ongoing relevance in business environments.
- Python is trending upward, signaling a move toward modern analytics and automation.
- Tableau adds value but demand is less consistent.
- R is declining in relevance for analysts, being overshadowed by Python.

### Additional chart for Data Engineer and Data Scientist

![Trending Top Skills for Data Engineer in Indonesia](./File%20Python/py_with_lukebarousse/project_course/3_project/images/3/skill_trend_DE_ID.png)

![Trending Top Skills for Data Scientist in Indonesia](./File%20Python/py_with_lukebarousse/project_course/3_project/images/3/skill_trend_DS_ID.png)

## 3. What The Top 6 Highest Pay Job in Indonesia?

### Visualize Data

```python
sns.boxplot(data=df_top6, x='salary_year_avg', y='job_title_short', order=job_order)
plt.title(f'Salary Distribution in The {job_country}')
plt.xlabel('Yealy Salary ($USD)')
plt.ylabel('')
ax = plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))
plt.xlim(0, 600000)
plt.show()

```

### Result

![Top 6 Highest Roles Pay Indonesia](./File%20Python/py_with_lukebarousse/project_course/3_project/images/4/salary_analysis_ID.png)

### Insight

Role-Based Salary Insights
Data Scientist

- Median salary around $120K–$150K/year.
- Wide range, with some salaries exceeding $500K (likely senior/global positions).
- Shows high earning potential and strong demand.

Data Engineer

- Median around $110K–$140K/year.
- Distribution similar to Data Scientist, but slightly lower ceiling.
- Consistently lucrative due to demand for infrastructure and cloud expertise.

Machine Learning Engineer

- Median roughly $130K/year with a wider spread.
- Some of the highest outliers (~$400K+), reflecting the premium for ML/AI expertise.
- Role has high variability depending on specialization and company size.

Senior Data Analyst

- Median near $100K–$120K/year.
- Narrower distribution compared to scientists/engineers.
- Outliers still reach $300K+, but less frequent.

Data Analyst

- Median around $80K–$100K/year.
- Lower ceiling than Senior Analysts, but still strong for entry/mid-level roles.
- Wide spread indicates varying expectations across companies.

Business Analyst

- Median around $70K–$90K/year, lowest among the roles shown.
- Narrow distribution, with fewer extreme outliers.
- Reflects its closer alignment with business operations rather than technical/engineering focus.

### Additional chart for The Most Jobs Count in Country

![Top Highest Roles Pay Unites States](./File%20Python/py_with_lukebarousse/project_course/3_project/images/4/salary_analysis_US.png)

![Top Highest Roles Pay India](./File%20Python/py_with_lukebarousse/project_course/3_project/images/4/salary_analysis_IND.png)

![Top Highest Roles Pay United Kingdom](./File%20Python/py_with_lukebarousse/project_course/3_project/images/4/salary_analysis_UK.png)

## 4. What Are the Most In-Demand and Highest Paying Skills for Data Analysts?

### Visualize Data

```python
job_country = "Indonesia"
job_title_short = "Data Analyst"

df_first = df[(df['job_title_short'] == job_title_short) & (df['job_country'] == job_country)].copy()

df_first = df_first.dropna(subset=['salary_year_avg'])

df_exploded = df_first.explode('job_skills')

df_exploded = df_exploded.groupby('job_skills')['salary_year_avg'].agg(['count', 'median'])

top_10_pay = df_exploded.sort_values(by='median', ascending=False).head(10)

top_10_demand = df_exploded.sort_values(by='count', ascending=False).head(10).sort_values(by='median', ascending=False)\

fig, ax = plt.subplots(2, 1)

dict_to_view = {
  f'Top 10 Highest Paid Skills for {job_title_short}' : top_10_pay,
  f'Top 10 Most In-Demand Skills for {job_title_short}' : top_10_demand
  }
for i, (title, col) in enumerate(dict_to_view.items()):
  sns.barplot(data=col, x='median', y=col.index, ax=ax[i], hue='median', legend='', palette='light:b')
  ax[i].set_title(title)
  ax[i].set_ylabel('')
  ax[i].set_xlim(0, 140_000)
  ax[i].xaxis.set_major_formatter(plt.FuncFormatter(lambda x, _: f'${int(x/1000)}K'))

plt.suptitle(f'Highest Pay vs Demand Skills in The {job_country}', fontsize=14)
fig.tight_layout()

```

### Result

![Most In-Demand and Highest Paying Skills for Data Analysts in Indonesia](./File%20Python/py_with_lukebarousse/project_course/3_project/images/5/most_demanded_vs_highest_pay_skills_ID.png)

### Insight

The comparison shows a clear distinction between what companies ask for most and what skills are rewarded with higher salaries.

- Highest Paying Skills: Tools like Power BI, JavaScript, Looker, and Tableau lead the list, with median salaries often above $100K/year. These specialized BI and visualization platforms offer a strong salary premium, reflecting their value in turning raw data into actionable insights.
- Most In-Demand Skills: Employers, however, most frequently request Power BI, Tableau, SQL, and Excel. These are the everyday essentials for reporting and analysis, forming the baseline toolkit for most Data Analyst roles.
- Overlap: Power BI and Tableau stand out because they are both highly demanded and highly paid, making them strategic skills to invest in.
- Gap: Programming languages like Python and R appear on both lists but rank lower in terms of salary compared to BI tools, showing they are important but not the top drivers of pay. Meanwhile, skills like GitLab or Asana show up in demand but don’t translate to higher compensation.

### Additional chart for The Most Jobs Count in Country

![Most In-Demand and Highest Paying Skills for Data Analysts in United States](./File%20Python/py_with_lukebarousse/project_course/3_project/images/5/most_demanded_vs_highest_pay_skills_US.png)

## 5. What is the Most Optimal Skill to learn for Data Analyst?

### Visualize Data

```python
job_country = "Indonesia"
job_title_short = "Data Analyst"

df_first = df[(df['job_title_short'] == job_title_short) & (df['job_country'] == job_country)].copy()
df_first = df_first.dropna(subset=['salary_year_avg'])

df_exploded = df_first.explode('job_skills')

# df_exploded[['salary_year_avg', 'job_skills']]
df_grouped = df_exploded.groupby('job_skills')['salary_year_avg'].agg(['count', 'median']).sort_values(by='count', ascending=False)
df_grouped = df_grouped.rename(columns={'count':'skill_count', 'median': 'median_salary'})

df_job_count = len(df_first)

df_grouped['skill_percent'] = df_grouped['skill_count'] / df_job_count * 100

# filtering more than 5%
# skill_min_percent = 5
# df_high_demand = df_grouped[df_grouped['skill_percent'] > skill_min_percent]

# filtering top 10
df_high_demand = df_grouped.head(10)

df_technology = df['job_type_skills'].copy()

df_technology = df_technology.drop_duplicates()
df_technology = df_technology.dropna()

technology_dict = {}
for row in df_technology:
  row_dict = ast.literal_eval(row) # convert string to dictionary
  for key, value in row_dict.items():
    if key in technology_dict: # if key does exist in technology_dict, add value to existing key
      technology_dict[key] += value
    else : # if key does not exist in technology_dict, add key and value
      technology_dict[key] = value

# most value is duplicated
# removing duplicates value by converting to set and back to list (the value, not the whole technology_dict)
for key, value in technology_dict.items():
  technology_dict[key] = list(set(value))

df_technology = pd.DataFrame(list(technology_dict.items()), columns=['technology', 'skills'])

df_technology = df_technology.explode('skills')
df_plot = df_high_demand.merge(df_technology, left_on='job_skills', right_on='skills')

from adjustText import adjust_text
from matplotlib.ticker import PercentFormatter

sns.scatterplot(
  data=df_plot,
  x='skill_percent',
  y='median_salary',
  hue='technology'
)

plt.xlabel(f"Percent of {job_title_short} Jobs")
plt.ylabel('Median Yearly Salary')
plt.title(f'Most Optimal Skills for {job_title_short} in {job_country}')

sns.despine()
sns.set_theme(style='ticks')

texts = []

for i, txt in enumerate(df_high_demand.index):
  texts.append(plt.text(df_high_demand['skill_percent'].iloc[i], df_high_demand['median_salary'].iloc[i], txt))

ax = plt.gca()

ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K'))

ax.xaxis.set_major_formatter(PercentFormatter(decimals=0))

adjust_text(texts, arrowprops=dict(arrowstyle='->', color='gray', lw=1))
plt.tight_layout()
plt.show()
```

### Result

![Most Optimal Skill to learn for Data Analyst in Indonesia](./File%20Python/py_with_lukebarousse/project_course/3_project/images/6/optimal_skill_DA_ID.png)

### Insight

- SQL

  - Highest demand (70% of jobs) and solid median salary ($100K).
  - Absolute must-have core skill for Data Analysts, even if not the top-paying.

- Python

  - Very high demand (60%) but lower salary ($75K).
  - Widely required, but oversupply may keep pay more modest compared to BI tools.

- Excel

  - High demand (50%) and decent salary ($90K).
  - Still critical for everyday analysis and reporting.

- Power BI & Tableau

  - Power BI: Moderate demand (~15%) but the highest pay (~$130K).
  - Tableau: Demand (25%) with strong salary ($105K).
  - These are the sweet spot skills that bring both relevance and high earning potential.

- Cloud Tools (AWS, BigQuery)

  - Lower demand (10–25%) and relatively lower salaries ($60–80K).
  - Good to know, but not priority skills for analysts compared to BI/SQL.

- Other tools (GitLab, Asana, R)
  - Low demand and modest salaries (<$75K).
  - Useful in niche contexts but not career-defining for Data Analysts.

### Additional chart for The Most Optimal Skill to learn for Data Analyst

![Most Optimal Skill to learn for Data Analyst in United States](./File%20Python/py_with_lukebarousse/project_course/3_project/images/6/optimal_skill_DA_US.png)
