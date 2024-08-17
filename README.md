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


4. Data Analysis<br/>
I created bar charts to compare the nutritional content for each category and beverage.  

     **1. Average Calorie Content for Each Beverage Category**<br/>
   
       ```
       df.groupby(['Beverage_category'])['Calories'].mean().plot(kind='barh', color='Orange', edgecolor='Black')
       plt.xlabel("Calories (average)")
       plt.ylabel('Beverage_category')
       plt.title("Avg Calories per Beverage Category")

       plt.show()
       ```
      ![PP7 Python Visu 1](https://github.com/user-attachments/assets/e7a54e4a-35dd-40c4-9221-d0583bd560fc)

     **Results**: Surprisingly, smoothies are the most calorie-rich category of all.  
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
       
      **Results**: Two out of the top five most calorie-dense beverages are smoothies. The top 2 are Frappucchinos.  
    &ensp;
   

   ---
   
     **3. Top 5 Most Sugary Drinks**

       ```
       # Rename a column
         df.iloc[:,11]
         df.rename(columns={df.columns[11]: 'Sugars'},inplace = True)

       # Calculate the average calories per beverage
         avg_sugar = df.groupby(['Beverage'])['Sugars'].mean()

       # Get the top 5 most sugary drinks
         top5_sugary_drinks = avg_sugar.nlargest(5).sort_values(ascending=True)

       # Plot the top 5 most sugary drinks
         top5_sugary_drinks.plot(kind='barh',color='Pink',edgecolor='Black')
         plt.ylabel('Beverage')
         plt.xlabel('Sugars (avg g)')
         plt.title("Top 5 Most Sugary Drinks")

         plt.show()
       ```
      ![PP7 Python Visu 3](https://github.com/user-attachments/assets/ea7cfa7b-5fe3-4d78-a20d-52e894f5488f)
   
    **Results**: Four of the top 5 most sugary drinks are Frappucchinos. Sweet!<br/>
                  Caramel Apple Spice (Without Wipped Cream) is one of the signature espresso drinks.  
   &ensp;

 
 ---

  **4. Average Caffeine Content in Each Beverage Category** 
  
       ```
         # Look at the column and preprocess it for analysis first

         # Rename the column
           df.rename(columns = {'Caffeine (mg)':'Caffeine'}, inplace=True)

         # See the values
           df['Caffeine'].values

         # Get rid of object values to convert datatype into integer
           values_to_drop = ['Varies','varies']
           df2 = df[df['Caffeine'].isin(values_to_drop) == False]
           df2['Caffeine'].values

         # Change the data type from object to integer
           df2['Caffeine'] = df2['Caffeine'].astype(int)
           df2['Caffeine'].dtypes

         # Plot the avg caffeine content in each category
           df2.groupby('Beverage_category')['Caffeine'].mean().plot(kind='barh',color='Sienna',edgecolor='Black')
           plt.ylabel('Beverage Category')
           plt.xlabel("Caffeine (avg)")
           plt.title("Average Caffeine Content in Each Category")
      ```

  ![PP7 Python Visu 4](https://github.com/user-attachments/assets/e51a1d64-99ca-4308-a4e2-c3e79078a03c)

  **Results**: Coffee has the highest caffeine content of all categories. Not surprising at all.  
   &ensp;


   ---


   **5. Top 10 Healthiest Drinks**
   
   Let’s determine the healthier drink choices. It is generally considered safe for most healthy adults to consume up to 400 mg of caffeine per day.<br/>
   The recommended daily intake of added sugar is no more than 36 grams for men and 25 grams for women. I used the average of these sugar recommendations and the healthy caffeine limit for calculations.
   
     ```
     healthy_drinks = df2[(df2['Caffeine'] < 400) & (df2['Sugars'] < 30.5)]
     healthy_drinks.head()

     avg_healthy_drinks = healthy_drinks.groupby(['Beverage'])[["Caffeine","Sugars"]].mean()

     top10_healthy_drinks = avg_healthy_drinks.nsmallest(10, columns=['Caffeine','Sugars']).sort_values(by=['Caffeine', 'Sugars'],ascending=False)

     top10_healthy_drinks.plot(kind='barh',stacked=True,edgecolor='Black')
     plt.ylabel('Beverages')
     plt.xlabel("Caffeine and Sugar (avg)")
     plt.title("Top 10 Healthiest Drinks")

     plt.show()
     ```

  ![PP7 Python Visu 5](https://github.com/user-attachments/assets/9d0ffaaa-8e41-4d6a-8567-992166fc6eb7)

  **Results**: Tea is generally considered a healthier drink. Surprisingly, hot chocolate and the chocolate banana smoothie contain less sugar than most other beverages.  
   &ensp;


---

### Key Takeaways

- Frappuccinos are very high in calories and sugar content. It’s best to avoid them or reserve them for cheat days.
- According to the analysis, smoothies are considered healthy due to their low caffeine and sugar content, though they are high in calories.<br/>
  They can be a good meal replacement when solid food isn't an option.
- Coffee contains a significant amount of caffeine, but it’s safe to consume if limited to 400 milligrams per day.
- The healthiest choices are teas. If you drink coffee daily, switching to tea could make you even healthier.



&ensp;

**Thank you for reading**! I hope this analysis encourages you to think about how you can improve your health and diet😄


