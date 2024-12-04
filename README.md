# Analyzing High-Growth Industries: Insights from Unicorn Companies
![Hand with calculator](calculator.jpg)

Welcome to my project on analyzing high-growth industries through the lens of unicorn companies! Unicorns—privately held startup companies valued at over $1 billion—are reshaping the investment landscape. In this analysis, I explored trends in valuations, funding, and industry growth rates using data from a comprehensive unicorn database. I combined multiple database tables to uncover insights and performed this analysis using Python and Jupyter Notebook.

## View the Notebook
You can check out the full analysis here: [View Notebook](https://github.com/caryhtan/Analyzing-Unicorn-Companies/blob/main/notebook.ipynb)

## What I Did
I focused on answering the following key questions:
- Which industries produce the highest company valuations?
- What is the rate at which unicorns are emerging?
- How does funding relate to valuation across industries?

### Data Sources
I used the following database tables for this project:

1. **dates**
   - **`company_id`**: A unique ID for each company.
   - **`date_joined`**: The date the company became a unicorn.
   - **`year_founded`**: The year the company was founded.

2. **funding**
   - **`company_id`**: A unique ID for each company.
   - **`valuation`**: The company’s value in US dollars.
   - **`funding`**: The amount of funding raised in US dollars.
   - **`select_investors`**: A list of key investors in the company.

3. **industries**
   - **`company_id`**: A unique ID for each company.
   - **`industry`**: The industry the company operates in.

4. **companies**
   - **`company_id`**: A unique ID for each company.
   - **`name`**: The company name.

## What I Found
Here are some key insights I discovered:
- **Top Industries**: Industries like technology and healthcare are leading in producing the highest valuations.
- **Unicorn Growth**: The rate of unicorn emergence has significantly increased over the past decade.
- **Funding to Valuation Relationship**: Higher funding rounds are generally correlated with higher valuations, but certain industries outperform this trend.

## How I Did It
To answer these questions, I:
1. Loaded and merged the database tables into a single comprehensive dataset.
2. Calculated metrics such as average valuation and funding by industry.
3. Visualized trends in unicorn emergence over time.
4. Explored relationships between funding and valuation across industries.

### Example Code
Here’s an example of the code I used:
```python
# Merge tables for analysis
merged_data = pd.merge(dates, funding, on='company_id')
merged_data = pd.merge(merged_data, industries, on='company_id')

# Calculate average valuation by industry
average_valuation = merged_data.groupby('industry')['valuation'].mean()

# Visualize unicorn emergence over time
unicorn_growth = merged_data['date_joined'].dt.year.value_counts().sort_index()
plt.plot(unicorn_growth.index, unicorn_growth.values)
plt.title('Number of Unicorns by Year')
plt.xlabel('Year')
plt.ylabel('Number of Unicorns')
plt.show()
