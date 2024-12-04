# Analyzing High-Growth Industries: Insights from Unicorn Companies
![Hand with calculator](calculator.jpg)

Welcome to my project on analyzing high-growth industries through the lens of unicorn companies! Unicorns—privately held startup companies valued at over $1 billion—are reshaping the investment landscape. In this analysis, I used SQL to identify the best-performing industries based on the number of new unicorns created between 2019 and 2021. By leveraging SQL queries, I explored their average valuations, growth trends, and emergence timelines to uncover actionable insights for portfolio strategies.

## View the Notebook
You can check out the full analysis here: [View Notebook](https://github.com/caryhtan/Analyzing-Unicorn-Companies/blob/main/notebook.ipynb)

## What I Did
I focused on answering the following key questions:
- Which three industries produced the highest number of new unicorns from 2019 to 2021?
- How many unicorns emerged within these industries?
- What year did these companies achieve unicorn status?
- What is the average valuation (in billions) of these unicorns?

### Data Sources
I worked with the following database tables:

1. **dates**
   - **`company_id`**: A unique ID for each company.
   - **`date_joined`**: The date the company became a unicorn.
   - **`year_founded`**: The year the company was founded.

2. **funding**
   - **`company_id`**: A unique ID for each company.
   - **`valuation`**: The company’s value in US dollars.
   - **`funding`**: The amount of funding raised in US dollars.

3. **industries**
   - **`company_id`**: A unique ID for each company.
   - **`industry`**: The industry the company operates in.

### What I Found
Here are some key insights I discovered:
- **Top Industries**: The three best-performing industries between 2019 and 2021 were technology, healthcare, and finance.
- **Unicorn Growth**: These industries accounted for a significant number of unicorns, reflecting their dominance in driving innovation.
- **Valuation Trends**: On average, unicorns in these industries had valuations of over $2 billion, showcasing their immense market potential.

## How I Did It
To answer these questions, I:
1. Used SQL queries to analyze the database tables and extract relevant metrics.
2. Filtered data to focus on unicorns created between 2019 and 2021.
3. Aggregated results to calculate the number of unicorns and their average valuations for each industry.
4. Sorted the final table by year and number of unicorns in descending order for clarity.

### Example Query
Here’s an example of the SQL query I used:
```sql
WITH unicorns_recent AS (
    SELECT 
        i.industry,
        EXTRACT(YEAR FROM d.date_joined) AS year,
        COUNT(d.company_id) AS num_unicorns,
        ROUND(AVG(f.valuation) / 1e9, 2) AS average_valuation_billions
    FROM industries i
    JOIN dates d ON i.company_id = d.company_id
    JOIN funding f ON i.company_id = f.company_id
    WHERE EXTRACT(YEAR FROM d.date_joined) BETWEEN 2019 AND 2021
    GROUP BY i.industry, year
)
SELECT *
FROM unicorns_recent
ORDER BY year DESC, num_unicorns DESC;
