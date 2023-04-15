# Data Wrangling - E-commerce Olist
Project for Pacmann School of Data 
The dataset has information of 100k orders from 2016 to 2018 made at multiple marketplaces Olist e-commerce platform. 
It has information about: order status, price, payment and freight performance to customer location, product attributes and finally reviews written by customers.

The public dataset is published on Kaggle by Olist Store and the data has been anonymized. 
For this project this data has been merged into a database file by the Pacmann Team, where I study data science.

For this project, I will focus on order transaction on origin & destination city and delivery time. 
This project will mostly consist of data wrangling (data cleaning and preparation), the later part will be visualization using python (matplotlib)

In this project my objectives are :
1. How is the overall order transaction over 2016 to 2018 ?
2. How is the distribution orders based on route type on origin & destination city?
4. How is the delivery time performance from the logistic partner?

Here's the overview of table connection inside database :
![image](https://user-images.githubusercontent.com/125140421/232181863-29eafaed-0394-4bcd-aa9e-ca086d9b1650.png)

You can check out my code on my repositories or read my medium article here :
https://medium.com/@dsyafz/data-wrangling-e-commerce-olist-91f3e2782c71

My summarize steps 

Data wrangling :
1. Import module
    I use pandas, numpy, sqlite3, and matplotlib. I also use tabulate to create table
2. Connect to database
    I use sqlite3 to fetch all tables from database file
3. Create data frame
4. Merging data
5. Data casting
    Changing a couple of object type into datetime64[ns]
6. Create checking table
    To check values on used columns like : how many non-null values, how many null values, % of null values, how many duplicate rows
7. Filtering data
    I only use delivered status data
8. Handling missing values in date columns
    Drop columns that has missing value (there's only few of them, like 0.01%) 
9. Create new columns
    time_diff_prep => how many days does it takes for seller to prepare the ordered product until handing it over to 3PL (third party logistic)
    
    time_diff => how many days does it takes for 3PL to sent the ordered product to customer (actual)
    
    time_diff_sla => how many days does it takes for 3PL to sent the ordered product to customer (expected estimation)
    
    SLA_diff_days => how many difference days between actual and expected delivery
    
    over_SLA => check if actual delivery time is longer than expected delivery time
    
    route => define whether delivery route is intercity (different city) or intracity (same city) 
    
10. Handling missing values & inconsistent value in product name columns
    There's three inconsistent product name that need to be replaced.
    There's 1559 values (around 1.4%) with nan value that need to be filled as "unknown"
11. Recheck table checking
    There's no missing value anymore

Visualizations :
1. How is the overall order transaction over 2016 to 2018 ?
I create line chart to show overall transaction orders on the dataset

![image](https://user-images.githubusercontent.com/125140421/232182975-749ecb65-ca61-4271-87d3-e9c739be047e.png)

It looks there’s a decline number of orders on December 2017 but it’s quicklt bounced back. Overall Olist is showing a consistent growth.

2. How is the distribution orders based on route type on origin & destination city?
I create pie chart to show route type distribution

![image](https://user-images.githubusercontent.com/125140421/232183027-8d0bd096-b155-47a9-a344-674d92084393.png)

It turns out most of Olist orders comes from intercity route.

Breakdown to see top origin city 

![image](https://user-images.githubusercontent.com/125140421/232183071-9ef06407-1382-4913-81e1-3bde8347925f.png)

There’s huge gap between Sao Paulo and Ibitinga. Other than Sao Paulo, intracity orders on other city is quite small.

Breakdown to see top destination city 

![image](https://user-images.githubusercontent.com/125140421/232183085-efc29737-5f7b-4052-be28-69e2ad96c183.png)

We can see that the top destination city is still Sao Paulo. This means the most active customers and sellers is in Sao Paulo.

3. How is the delivery time performance from the logistic partner?

When e-commerce companies collaborate with another logistics company, they usually make a Service Level Agreement (SLA). 
It’s like a contract that sets the rules for shipping goods to the customer, 
like how long does it takes to get your goods and what kind of condition they should be in when they arrive.

I create pie chart to show over SLA distribution

![image](https://user-images.githubusercontent.com/125140421/232183127-e519f288-30bf-4c1c-9404-b1fe51def921.png)

Olist’s logistic partner performance delivery time is really good! There’s only 7.4 % from overall orders that’s over SLA.

We’ll focus on orders that are over SLA. Let’s see how many days it takes for most of these deliveries to be completed.

![image](https://user-images.githubusercontent.com/125140421/232183138-df67b43f-9106-4b93-aa9f-224ba39389d9.png)

Here’s SLA difference days that contributes 70% of over SLA orders.

![image](https://user-images.githubusercontent.com/125140421/232183154-c24752d9-1c56-4107-8a76-04adb693ba98.png)

Let’s see which route that has the most over SLA orders on overall dataset

![image](https://user-images.githubusercontent.com/125140421/232183159-a085c012-ef34-407f-9b12-e3390ce90e62.png)

Surprisingly, the most over SLA orders comes from route Sao Paulo to Sao Paulo. 
Even if the over SLA orders on that route only contributes 6 %, it is still a little weird because it’s an intracity route.

Let’s take a closer look at intracity route: Sao Paulo

![image](https://user-images.githubusercontent.com/125140421/232183171-c87a34fb-80ce-4b9a-9842-8a440845f930.png)

It looks like only around 3% of deliveries on this route are running behind schedule (aka over SLA), which isn’t too bad.

However, the number late of days can vary quite a bit, so it’s hard to pinpoint the exact cause of the delays. 
It’s possible that there are some issues on the logistic partner’s side of things. 
Olist need to look into it further to figure out what’s going on.


Conclusion & Insight :
1. Overall order transactions on Olist’s ecommerce platform have been growing steadily.
2. The distribution of route types on Olist’s platform is imbalanced, with intracity routes is only 5% of total orders. 
    This suggests that seller locations are not evenly spread throughout Brazil.
3. Olist’s logistic partner has a strong delivery time performance, with only 7% of orders failing to meet the shipping time SLA.
    Olist can take advantage of this opportunity by creating a penalty agreement with their logistic partner if one is not already in place
    
Thank you!
