-----------
QUICK NOTE:
----------

I did have a tutoring session on 7/7/23 with David Pecot and we did several changes to my code but I did not write down since we were plodding along together. 

I do have some general snippets of what we did:
1. I had an issue on the last two sets(Scores by School Size, Scores by School Type) where they just WOULD NOT change. Some coding we kept but I'll post what I can remembe what we did edits to together. I apologize if it is not everything but I will list out all I recall.

-------
CODE:
-------

# Calculate the total school budget and per capita spending per school
per_school_budget = school_data.groupby('school_name')['budget'].sum()
per_school_capita = per_school_budget / per_school_counts
per_school_budget
per_school_capita
------------------------------

# Calculate the average test scores per school
per_school_math = school_data_complete.groupby('school_name')['math_score'].mean()
per_school_reading = school_data_complete.groupby('school_name')['reading_score'].mean()
per_school_math
per_school_reading
------------------------------

per_school_summary = pd.concat([school_types, school_budgets,school_counts, student_budgets,average_math, average_reading, per_school_passing_math, per_school_passing_reading, overall_passing_rate], axis=1)
per_school_summary.columns = ["School Type","Total School Budget","Total Student Count","Per Student Budget", "Average Math Score", "Average Reading Score","Percent Passing Math", "Percent Passing Reading", "Percent Overall Passing"]
per_school_summary
-----------------------------

# Use `pd.cut` to categorize spending based on the bins.
school_spending_df["Per Student Budget"] = pd.to_numeric(school_spending_df["Per Student Budget"].replace('[/$]', '', regex=True))

spending_bins = [1, 585, 630, 645, 680]
labels = ["<$585", "$585-630", "$630-645", "$645-680"]

school_spending_df["Spending Ranges (Per Student)"] = pd.cut(school_spending_df["Per Student Budget"], bins=spending_bins,labels=labels)
school_spending_df

----------------------------