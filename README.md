# AI &amp; ML Project 2023
### Dataset : ShopEasy

### Members: Kevin Wang (289121), Ahmet Akgun(287241), Kaixin Lai(289991)

## [Section 1] Introduction
In this project we are assigned to discover and analyze buying habits and behaviors of customers in a leading e-commerse site called ShopEasy. The dataset contains a wide variety of features that can be analyzed and compared with eachother. Through this analysis we are able to distinguish differences between redundant and essential features to then aid us in the categorization of the customer base. We aim to elevate the shopping experience for every customer, creating a more personal enviorment customized to their unique preferences and needs. This is done by understanding the different clusters that we achieve, observing prominent features in them and creating a targetted experience for each cluster.

## [Section 2] Method
[Section 2] Methods – Describe your proposed ideas (e.g., features, algorithm(s),
training overview, design choices, etc.) and your environment so that:
    
• A reader can understand why you made your design decisions and the reasons behind any other choice related to the project
• A reader should be able to recreate your environment (e.g., conda list, conda envexport, etc.)
• It may help to include a figure illustrating your ideas, e.g., a flowchart illustrating the steps in your machine learning system(s)

In our project we firstly wanted to visualize the data and each feature in it. We started with an EDA(exploratory data analysis) and used various techniques to observe the each features and their relationship between eachother. We checked for data integrity by observing whether there were duplicates or missing values. There were no duplicates but a small percentage of missing values(around 3.5%) in the columns 'leastAmountPaid' and 'maxSpendLimit' where we chose to drop the rows containing the missing values as the percentage was so small.
<img width="1049" alt="Screenshot 2024-01-01 at 03 15 39" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/4deaad80-e7be-4536-b319-12852e3fb3c6">



Imagine a platform named ShopEasy, a leading e-commerce site that sells a variety of products, from books and gadgets to furniture and fashion. Over the years, they have amassed a vast amount of user data. This data is a gold mine of insights waiting to be discovered. ShopEasy aims to provide personalized user experiences, special promotions, and improved services. But to do this effectively, they first need to understand the buying habits and behaviors of their customers. By applying segmentation to this dataset, ShopEasy aims to uncover these hidden patterns and provide an enhanced, personalized shopping experience for its users.

