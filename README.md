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

![Visualization of top skills for data roles](./File%20Python/py_with_lukebarousse/project_course/3_project/images/skill_demand_ID.png)

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

![Trending Top Skills for Data Analysts in Indonesia](./File%20Python/py_with_lukebarousse/project_course/3_project/images/skill_trend_DA_ID.png)

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

Data Engineer
![Trending Top Skills for Data Engineer in Indonesia](./File%20Python/py_with_lukebarousse/project_course/3_project/images/skill_trend_DE_ID.png)

Data Scientist
![Trending Top Skills for Data Scientist in Indonesia](./File%20Python/py_with_lukebarousse/project_course/3_project/images/skill_trend_DS_ID.png)
