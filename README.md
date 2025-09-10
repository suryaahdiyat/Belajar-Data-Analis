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
fig.suptitle('Likelihood of Skills Requested in US Job Postings', fontsize=14)
fig.tight_layout(h_pad=1)
```

### Result

![Visualization of top skills for data roles](./File%20Python\py_with_lukebarousse\project_course\3_project\images\skill_demand_all_data_roles.png)
