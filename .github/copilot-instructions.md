# Copilot Instructions for AI Coding Agents

## Project Overview
This workspace is focused on data analysis and visualization using Python and Jupyter Notebooks. The main data sources are Excel and CSV files, with analysis scripts and notebooks organized by topic and complexity. The project leverages pandas, matplotlib, and external datasets (e.g., HuggingFace datasets).

## Directory Structure
- `File excel/`: Contains raw data files (Excel, CSV) for analysis.
- `File Python/`: Contains Python scripts and Jupyter notebooks. Notebooks are organized into subfolders by topic and difficulty (e.g., `1_basics/`, `2_advanced/`).

## Key Patterns & Conventions
- **Data Loading**: Use pandas for reading local files and HuggingFace `datasets` for remote datasets. Example:
  ```python
  import pandas as pd
  from datasets import load_dataset
  df = pd.read_csv('path/to/file.csv')
  dataset = load_dataset('lukebarousse/data_jobs')
  df = dataset['train'].to_pandas()
  ```
- **Data Cleaning**: Common patterns include converting date columns, exploding lists, and pivoting tables. Example:
  ```python
  df['job_posted_date'] = pd.to_datetime(df['job_posted_date'])
  df['job_skills'] = df['job_skills'].apply(lambda x: ast.literal_eval(x) if pd.notna(x) else x)
  df_exploded = df.explode('job_skills')
  df_pivot = df_exploded.pivot_table(index='month', columns='job_skills', aggfunc='size', fill_value=0)
  ```
- **Visualization**: Use matplotlib for plotting. Always set titles, labels, legends, and grids for clarity. Example:
  ```python
  df_pivot.iloc[:, :5].plot(kind='line', linewidth=4)
  plt.title('Top 5 Skills Over Months')
  plt.xlabel('Month')
  plt.ylabel('Count')
  plt.legend(title='Skills')
  plt.grid()
  plt.show()
  ```
- **Notebook Organization**: Each notebook should be self-contained, with clear markdown explanations and code cells grouped logically (data loading, cleaning, analysis, visualization).

## Developer Workflows
- **No build/test automation detected**: Work is interactive via Jupyter Notebooks and Python scripts. Focus on reproducible analysis and clear cell outputs.
- **Debugging**: Use notebook cell outputs and pandas/matplotlib inspection. No custom debugging tools or scripts found.

## Integration Points
- **External Data**: HuggingFace datasets, local Excel/CSV files.
- **Libraries**: pandas, matplotlib, ast, datasets (HuggingFace).

## Project-Specific Advice
- When adding new analysis, follow the existing notebook structure: start with markdown context, then code for data loading, cleaning, and visualization.
- For new data sources, place files in `File excel/` and document their use in markdown cells.
- For advanced visualizations, use the patterns in `2_advanced/` notebooks as reference.

## Example Files
- `File Python/py_with_lukebarousse/project_course/2_advanced/16_matplotlib_advanced_customization.ipynb`: Advanced matplotlib usage and data pivoting.
- `File Python/py_with_lukebarousse/project_course/1_basics/Learn_Pandas.ipynb`: Introductory pandas patterns.

---

If any section is unclear or missing important details, please provide feedback or specify which workflows or conventions need further documentation.
