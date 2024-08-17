# Starbucks Nutrition Data Analysis

### Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Steps](#steps)
- [Key Takeaways](#key-takeaways)  
&ensp;


### Project Overview

Have you ever wondered how your favorite Starbucks drinks affect your health? Or do you just go for what your heart wants without a second thought?<br/>
This Starbucks Nutrition Data Analysis project aims to provide clear information about the nutritional content of Starbucks beverages, 
helping you identify what to avoid and what the healthier drink choices are.
&ensp;


### Data Sources

- starbucks.csv  (https://www.kaggle.com/datasets/henryshan/starbucks) :<br/>
  Contains detailed information about each beverage, including category and nutritional content such as calories, sugar, protein, and caffeine.
&ensp;


### Tools

- Python
&ensp;


### Steps

The following steps were taken to complete the analysis. :  
&ensp;

1. Established specific questions such as:

    - Which drinks should be avoided due to high calorie or sugar content?
    - Which category has the highest and lowest calorie content?
    - Which are the most sugary drinks?
    - How much caffeine does each beverage contain?
    - What are the healthiest drinks among all the Starbucks beverages?  
&ensp;
2. Imported Python libraries (Pandas, NumPy, and Matplotlib) into Jupyter Notebook. 

3. Imported starbucks csv file and inspected the data.
    - Checked column names and their data types.
    - Fill the null values with 0.  
&ensp;

4. Data Analysis  
I created bar charts to compare the nutritional content for each category and beverage.  

     **1. The average calorie content for each beverage category**<br/>
   
       ```
       df.groupby(['Beverage_category'])['Calories'].mean().plot(kind='barh', color='Orange', edgecolor='Black')
       plt.xlabel("Calories (average)")
       plt.ylabel('Beverage_category')
       plt.title("Avg Calories per Beverage Category")

       plt.show()
       ```
      ![PP7 Python Visu 1](https://github.com/user-attachments/assets/e7a54e4a-35dd-40c4-9221-d0583bd560fc)

     **Findings**: Surprisingly, smoothies are the most calorie-rich category of all.
   &ensp;

---

   
     **2. Top 5 Highest-Calorie Beverages**
   
       ```
       # Calculate the average calories per beverage
       avg_calories = df.groupby(['Beverage'])['Calories'].mean()

       # Get the top 5 highest average calorie values
       top5_high_cal_drinks = avg_calories.nlargest(5).sort_values(ascending=True)

       # Plot the top 5 highest calorie beverages
       top5_high_cal_drinks.plot(kind='barh',color='Red',edgecolor='Black')
       plt.ylabel('Beverage')
       plt.xlabel("Calories (avg)")
       plt.title("Top 5 Highest Calorie Beverages")

       plt.show()
       ```
       
       ![PP7 Python Visu 2](https://github.com/user-attachments/assets/25f20b96-0f6a-4fa3-8f82-11fb6a2ac4a5)
       
      **Findings**: 2 out of the top 5 most calorie-dense beverages are smoothies. The top 2 are Frappucchinos.  
   &ensp;

---

       **Top 5 Most Sugary Drinks**




   

### Key Takeaways

- I found that most fraudulent transactions occurred between 10 p.m. and 3 a.m., which is bedtime for most people.
- I initially assumed that older individuals would have more fraudulent transactions because they are more likely to be targeted.<br/>
  However, I was wrong. I created a visualization to explore this in more detail for the next project.
- The other factors did not provide key insights regarding a correlation with the occurrence of fraudulent transactions.
- The total number of fraudulent transactions in 2020 decreased by only 1% compared to 2019.  
&ensp;

**Thank you for reading**!😄


