# AI &amp; ML Project 2023
### Dataset : ShopEasy

## [Section 1] Introduction
In this project we are assigned to discover and analyze buying habits and behaviors of customers in a leading e-commerse site called ShopEasy. The dataset contains a wide variety of features that can be analyzed and compared with eachother. Through this analysis we are able to distinguish differences between redundant and essential features to then aid us in the categorization of the customer base. We aim to elevate the shopping experience for every customer, creating a more personal enviorment customized to their unique preferences and needs. This is done by understanding the different clusters that we achieve, observing prominent features in them and creating a targetted experience for each cluster.

## [Section 2] Method
In our project we firstly wanted to visualize the data and each of its features. We started with an EDA(exploratory data analysis) and used various techniques to observe each features and their relationship between eachother. From the description of the dataframe we can already notice some data that doesn't match. The most obvious example is in how the max value of leastAmountPaid is higher than the max value of account total. This could be due to a recording error, or something similar which will further be analyzed later on. We checked for data integrity by observing whether there were duplicates or missing values. There were no duplicates but a small percentage of missing values(around 3.5%) in the columns 'leastAmountPaid' and 'maxSpendLimit' where we chose to drop the rows containing the missing values as the percentage was so small. 
 
 Next we performed univariate and bivariate analysis on the data. Firstly we did an univariate analysis, which provides insight on how a single variable is distributed across the dataframe. The analysis is conducted using boxplot and histogram to visualize the data as most of the data are numerical features. From this data we noticed a lot of the features have right skewed distributions such as accountTotal, itemCosts, maxSpendLimit ect. A few have left skewed distributions such as frequencyIndex and accountLifespan. itemBuyFrequency instead has a bimodal distribution and webusage has a uniform distirbution. Skewed distribution can suggest a high concentration of values on the higher or lower end of the scale, depending on left or right skewed distribution respectively and can suggest that outliers are present. Therefore we created boxplots to visualize the outliers. In numerous of the box plots we observe a large number of outliers that suggest there is high variations in some of these features. However, before further analyzing the outliers we will want to do that after choosing the features that fit best for the purpose of clustering. 
 Below is an image of the first nine histograms and boxplots:
 
<img width="1181" alt="Screenshot 2024-01-02 at 01 07 15" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/86d77641-c6bc-481d-a41d-7db7c3b3b0ce">
<img width="1181" alt="Screenshot 2024-01-02 at 01 07 32" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/2f0a0c78-aa08-413e-a19a-34b07a749f8d">
 
 We proceeded with bivariate analysis to examine the relationships between pairs of variables. Here we choosed to examine pairs of variables that showed similar values to eachother from the boxplots. We noticed similar values between itemCosts and singleItemCosts as well as itemBuyFrequency and multipleItemBuyFrequency. Anything that is missed will be further analyzed in the multivariate analysis. Another interesting observation that could be analyzed is how leastAmountPaid has outliers that reach around 80000 in value, which is much higher than the highest value in monthlyPaid or worst accountTotal. This also raises some question on the integrity of the attribute monthlyPaid as the description of the feature is very vague only describing "Total amount paid by the user every month" which is assuming an user pays the same total amount every month or it might be an average. Instead for accountTotal, not only does leastAmountPaid have higher values than it, which would already be an anomaly as in no case would "The least amount paid by the user in a single transaction" be higher than the "Total amount spent by the user on ShopEasy since their registration". This is because leastAmountPaid should be included in the total amount spent by user on ShopEasy, so under normal circumstances accountTotal should always be higher than leastAmountPaid. 
 
 We then further observed the distribution of categorical features accountType and location and discovered that both categorical features have equal distribution across all users. We also used KDE plots to understand whether there is a difference in distribution between the categorical feature distributions to another feature such as itemBuyFrequency and discovered that location feature might not be relevant to understanding buying habits and behaviour of customers, as they have no effect on the distribution of other features and in a e-commerce context where almost everything is done online, on a website, location does not really matter. Although accountType did not have an affect on feature distribution as well, we wanted to keep accountType as it is a feature that would provide more future insight on the user base of each cluster.
 Below are the KDE plots for accountType/ location with itemBuyFrequency:
 
<img width="453" alt="Screenshot 2024-01-02 at 01 23 54" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/ffc734d7-deed-43f8-9dde-a5780ff5242f">
<img width="447" alt="Screenshot 2024-01-02 at 01 24 09" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/2a0d0b41-9807-40a2-bd27-50b36dbc1da6">
 
 Before we used a heatmap to visualize all the correlations we label encoded from sklearn to encode accountType categorical values. We use label encoding for accountType as they can be considered ordinal(where the order of categories is meaningful'premium' being first and 'student' being last). The reasoning as premium account type pay the most, while student account type get discounts so they pay the least. And regular account types pay a normal amount. For location categorical values, since it is a nominal data, we chose not to use label encoding as it might assume a natural order in the location, instead using dummy variables would be more appropriate in this case where each category is represented by a binary vector. We then observed the correlation heatmap to observe the features in a more holistic way. Below are the notes we took observing the heatmap:
  
  Firstly, we can confirm that there is no correlation between the locations and other attributes. As mentioned before since we are analyzing customers on an e-commerce website, the location often does not matter unless it in a whole different country, which in this case it is not. Therefore we decided not to select this feature as it is not relevant to our analysis. It is different for account type as this categorical feature is actually relevant to our analysis even though it has no coorrelation seen in the heatmap with any other feature. From the heatmap one can also observe a few features that can be considered irrelevant for the analysis or redundant. We choose to drop accountTotal as although it can be an essential feature to evaluate a user's engagement with the e-commerce website, the values it portrayed were inconsistent compared to other attributes such as itemCosts, and monthlypaid meaning either the total amount does not depict a value in money or uses a different currency or in general is inaccurate. Using this logic we also choose to drop leastAmountPaid, having little to no correlation with the other features, as mentioned before, the values portrayed are inconsistent compared to other attributes such as monthlyPaid. After further observation we notice that the attribute ,monthlyPaid also has inconsistencies with attributes such as itemCosts and also add no additional insight that itemCosts wouldn't add therefore we choose to drop monthlyPaid. This also leads to dropping features such as webUsage and frequencyIndex, not only having little to no correlation with the rest of the features but both also have a very similar definition to itemBuyFrequency which actually does have correlation to other features that are relevant to our analysis. We also drop the feature paymentCompletionRate for the lack of correlation with other features as well as the lack of insight it can provide. We also consider dropping maxSpendLimit for the same reason as accountTotal and leastAmountPaid, which is for the reason that it proves to have inconsistencies between other features such as monthly paid, where although the limit is set to a certain value for a user, that same user would have higher singleItemCosts value than the maxSpendLimit value. "The maximum amount the user can spend in a single purchase, set by ShopEasy based on user's buying behavior and loyalty" is the definition of maxSpendLimit and the definition for singleItemCosts is "Costs of items that the user bought in a single purchase without opting for installments" so therefore it is again an inconsistent value and we decide to drop maxSpendLimit. Additonally features such as singleItemBuyFrequency and multipleItemBuyFrequency or singleItemCosts and multipleItemCosts are a more specific version of itemBuyFrequency and itemCosts respectively. These two pair of features can be generalized by itemBuyFrequency and itemCosts and would provide a more significant insight to our analysis compared to the general insigh provided by itemBuyFrequency and itemCosts. Therefore itemBuyFrequency and itemCosts are dropped. We also drop emergencyUseFrequency due to its high correlation and similar definition to emergencyCount, meaning it could be considered redundant to have it.
Below is an image of the heat map: 
<img width="1029" alt="Screenshot 2024-01-02 at 01 08 20" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/e4e2ac54-dd63-4a6d-bab7-ea48470615b3">

 
  Now that we have observed and analyzed the data we moved on to preprocessing our data. Since we dropped the columns leastAmountPaid and maxSpendLimit which were the columns who originally had the missing data we added the missing values back as they wouldn't be missing for the new columns that are present in the dataframe. We dropped the features we deemed redudant or not insightful and removed outliers that were 4 standard deviations away from the mean of the remaining features. Since the range of the feature values differs from feature to feature we also scaled the data.
 
  Moving on we chose what type of problem this is and we understood it was a clustering problem. This is because the dataset provides a mix of numerical and categorical data, ideal for segmentation and clustering analysis. From this we could already rule out regression as it is used to predict a continuous outcome. Instead this question focuses on predicted clusters of customers for a more personal user experience. Classification is not chosen as well because it is used in supervised learning meaning, is used when there is already a predefined categorical outcome such as whether the clothes will be on sale or not. In this case, although we will be dividing the customers/users into clusters(categories) it is not the same as in the sense that the clusters are not predefined but rather require to be uncovered through analysis of the different clusters that are formed when applying different clustering algorithms. In fact clustering problem is used in unsupervised learning where there is no predefined outcome.
  
  We chose to test 3 models of clustering, K-means++, hierchical clustering and DBSCAN. There are different reason for which we chose each one. We chose to do all 3 for a more comparative analysis where each method could provide insight on clustering the same data, it can reveal more aspects of the clusters. Firstly, K-means which is used to deal with larger datasets generally works better than hierchical clustering. It is also very versatile for a wide range of applications. Hierchical clustering instead uses a dendrogram that makes the clustering process more interpretable through a visual aspect. DBSCAN is the only model out of the 3 that does not need a predefined cluster number, instead it needs an eps value and min_samples values( will be explained in the next section) and is especially good at handling noise as it removes outliers completely from the clustering process and considers them a seperate clusters. Both hierchical clustering and K-means clustering are defined as linear clustering models as they are able to effectively handle linearly separable data. On the other hand, we have DBSCAN which is reffered to as a non linear clustering algorithm as it identifies clusters with more complex shapes that are not linearly separable. By linearly seperable I mean that clusters can be divided by a straight line on a hyper plane. We decided that for our analysis of the clusters we would only use hierchical clustering and K-means clustering as later on we discover that some outliers are needed to create meaningful and insightful clusters that we can analyze which DBSCAN does not allow us to do. Below a flowchart illustrating the steps of the project is depicted:

<img width="1049" alt="Screenshot 2024-01-01 at 03 15 39" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/4deaad80-e7be-4536-b319-12852e3fb3c6">

We also made a conda environment called shopEasy_environment.yml to ensure accsibility and functionality of the jupyter notebook with all the needed imports.

To make the environment work just download the shopEasy_environment.yml in the repository, open a terminal and run "conda env create -f aimlenvironment.yml" and then "conda activate shopeasy_env". Then run "python -m ipykernel install --user --name=shopeasy_env --display-name "Python (shopeasy_env)"". Finally run "jupyter notebook".(don't include the quotation marks in your code)

## [Section 3] Experimental Design
We conducted multiple experimente in order to validate our target contributions in this project(to find number of clusters, eps, Minpts) we will list them below:
First, we started with the elbow method. This is used to determine the most fitting number of clusters that should be used in the K-means clustering algorithm. The inertia, "also known as the within-cluster sum of squares", is measure of how close values in a cluster are to their centroid. The elbow method consist of running the k-means algorithm multiple times with different number of k clusters and plotting down the inertia they get for each k. The inertia decreases as the number of clusters increase. On the elbow plot, the inertia is the y value and k number of clusters is the x value. The optimum number of clusters is where the point of inertia starts decreasing at a slower rate and is called the "elbow". Past this point there will be diminishing returns. Additionaly, we did not use silhuoette score range to find the most appropriate number of clusters as overlapping is bound to happen in databases such as these where there is no absolute distinction between each customers. It is important to find the general type of customers and it is enough to use the elbow method for that. Such as in cases where the silhuoette score range will display two clusters as the option with the least overlapping but it would not be insightful from an analysis point of view trying to discover the different types of users in shopeasy. Furthermore, basing our cluster number on silhuoette score can also lead to overfitting as it may suggest a higher number of clusters which will not be insightful or interpretable as subtle differences are not of essential concern, especially in complex and high-dimensional data. Below is an image of the elbow plot:

<img width="692" alt="Screenshot 2024-01-02 at 02 29 05" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/9e24b06b-46d0-404f-b464-297c9ac6cd0e">

In hierchical clustering we used dendrograms to find the optimum number of clusters. Dendograms depict the similarity and order in which clusters were formed. The first cluster that is formed has the shortest branch. Before creating the dendrogram, we considered which linkage function to use and after careful consideration we decided that Ward's method is an appropriate function to use as it minimizes within cluster variance providing effective analysis against high variance dataset. To determine the number of clusters we used the cut method to cut across the dendrogram without going through any horizontal lines and see how many branches we cut. This is usually up to the user for where to cut. Below is an image of the dendrogram: 

<img width="457" alt="Screenshot 2024-01-02 at 03 16 13" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/ce0b1ec4-760f-43d5-83cd-bd6758328046">

Here we used Scipy's hierarchical clustering functions to compute and plot a dendrogram. The color produced is part of what the function does which is to represent different clusters using color thresholding based on distance between each cluster. Although the dendrogram already shows an optimum number of cluster, the context of the database also has to be considered into the final decision of what number of clusters is best for this dataset. Therefore although the dendrogram depicts 3 ideal clusters, 5 clusters could provide more insight on the types of user base on the platform ShopEasy. 

Moving foward, in DBSCAN two primary parameters are defined by the user:

'eps' (epsilon) :This parameter defines the max distance allowed between two values for them to be considered in the same neighborhood.
Minimum samples (“MinPts”): This parameter determines the fewest/ minimum number of points required in a neighborhood for the point to be a core point. This number includes itself therefore if the parameter is 4, a point needs 3 points in its neighborhood to be conisdered a core point.
For MinPts value there is no automatic method to determine an optimum value. Essentially, it should be set using knowledge of the data set. Some rules that are followed are: larger datasets require larger value of minpts, noisier datase require larger minpts value, and generally should be of greater size or equal to the number of attributes in the data or dimensionality of the data. In this case we'll just follow the rule of MinPts= 2*dim. In this case we have 9 dimensions therefore MinPts = 18.

For 'eps' value, one technique allows us to automatically identify the optimum 'eps' value where it calculates the average distance between each point and its k nearest neighbors. In this case 'k' will be equal to the MinPts we selected above. Then after the average k-distances are calculated, they are plotted in ascending order on a graph where the optimum 'eps' can be found at the maximum curvature for 'eps'. Below is an image of optimum 'eps' plot:

<img width="449" alt="Screenshot 2024-01-02 at 03 19 35" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/8a08f42f-17f6-4b2f-aa2b-90a2c1b2266d">

For evaluation metrics we used the silhuoette score. The silhuoette score measures how similar a value is to its own cluster compared to other clusters and we used it because we wanted to confirm that clusters were actually being formed. Ranging from -1 for incorrect clustering, 0 fo overlapping clusters and 1 for highly dense clusters. The silhuoette scores we got for the K-means, hierchical clustering, and DBSCAN are 0.2608019426418297, 0.19473892330055398, and 0.11019299423577715 respectively. The silhuoette score are quite low as mentioned above, and suggests clusters are not highly distinct. Several similarities could be shared between customers of each cluster, but this does not mean that there are no patterns. Data that is broad-ranging such as this dataset on users on an e-commerce platform can often contain variability and therefore the score can be acceptable to indentify customer clusters for a more personalized user experience. The DBSCAN score is especially low which we will get into in the next section. 

## [Section 4] Results
To visualize the results of the clusters in a clear and analytical way, we plotted a particular type of graph that helped us visualize the clusters in a more coherent manner as we have nine features to analyze, the high dimensionality of the graph does not allow us to use normal plotting graph instead we created a graph inspired by https://towardsdatascience.com/clustering-with-more-than-two-features-try-this-to-explain-your-findings-b053007d680a this artical that would display clusters in a circle plot helping me visualize the mean attributes of each cluster. We used plotly.express to plot these graphs, below is the graph we got for K-means as an example: 

<img width="1098" alt="Screenshot 2024-01-02 at 03 44 42" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/7f24195f-f012-4ee1-b67f-2ea5025cf4f2">

We also printed out all the feature means for each cluster, in each clustering model, below is an image showing the result we got for K-means: 

<img width="554" alt="Screenshot 2024-01-02 at 03 53 44" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/a0abe62e-8b21-4587-8ae2-f87979786c93">

Futhermore we plotted out a pie chart to visualize the percentage of user in each cluster as seen below: 

<img width="1060" alt="Screenshot 2024-01-02 at 03 55 16" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/a9ec0b90-f696-42aa-9731-594448675d82">

These all resulted in a more complete understanding of the clusters and here is what we found: 

For the analysis of customer segment we’ll mainly use the results found in K-Means ++ clustering and Hierarchical clustering as we achieved the same number of segments and similar results to each other. In DBSCAN, a large percentage of data is considered as noise (more than 14%, 1211 users), which leads to an inaccurate insight when observing the clusters as it might exclude particular shopping habit of users who vary from clusters. This can be considered a very huge difference compared to the other two clustering methods, and therefore we will not be considered in the analysis. 

Firstly we identify 5 number of segments. We could’ve chosen 3 for a better silhouette score in hierarchical clustering, but we believe that 5 will give us the most insight in analysing and providing a more personal user shopping experience. In K- means ++ the first cluster we can observe that stands out to us is labeled as cluster number 2. It has the highest mean singleItemCosts, multipleItemCosts, singleItemBuyFrequency, itemCount, and accountLifespan. It also has the lowest mean accountType and second highest mean multipleBuyFrequency. From these features we can already have a general understanding of what this cluster represents. This cluster can be defined as a high spending long term user base with a focus in single instalment purchases. This cluster makes up 12 percent of the total dataset with 1013 users. The low account type mean of -0.046186 can also suggest that they are composed largely of premium and regular account type user base(premium account type are defined as -1.218483, regular account type as 0.008311, and student account type as 1.235104). A similar cluster is made using the hierarchical clustering method, which is cluster number 0, it has the highest mean singleItemCosts, multipleItemCosts, singleItemBuyFrequency, and ItemCount as well as second highest mean multipleItemBuyFrequency and accountLifespan and second to lowest mean accountType of -0.010072. Similar to K-means++, here this cluster takes up 15.1% of the whole user database. Therefore we can identify our first cluster as High spending long term premium/regular users with a focus in single instalment purchases.

Our second cluster can be said to be quite similar to our first cluster but also very different. This user base can be identified in the K-means++ as cluster 4, with the highest mean multipleItemBuyFrequency, and second highest mean multipleItemCosts, ItemCount, and accountLifeSpan. This indicate the cluster has a high spending long term user that is more oriented in buying items through multiple instalments. They also have the second to lowest value in accountType of -0.005989 indicating they are composed mostly of regular and premium users. This cluster makes up for 24.5% of the user base. This is also the case in hierarchical clustering where cluster 3 has the highest mean multipleItemBuyFrequency and accountLifeSpan, second highest mean multipleItemCosts, and ItemCount. They also have an accountType of -0.00421 which is the third to lowest but still indicate in general a vast number of users in between regular and premium. The percentage of users in this cluster is 26.7% very similar to the results we have in K-means++ and so we have identified our second cluster as High spending long term premium/regular users with a focus in multiple instalment purchases.

Next we can see in both models that there is cluster that has the highest emergencyCount and emergencyFunds. First in the K-means++ model we observe that cluster 3 has the highest emergencyCount and emergencyFunds by a lot almost 2 in value compared to the rest of the clusters. They also have the second to lowest accountLifespan and second to highest accountType of 0.002396. They have the second to lowest singleItemCosts, and multipleItemCosts, as well as multipleItemBuyFrequency and third to lowest singleItemBuyFrequency. In general this cluster has multiple below average features with emergencyCount and emergencyFunds standing out. emergencyFunds is defined as "Amount that the user decided to keep as a backup in their ShopEasy wallet “ therefore this user base could be users that rely solely on their ShopEasy wallet. An interesting observation is that their account type is the second highest indicating some number of student users as well, although still below 0.008311 which is what regular users are classified as. Therefore we can define this cluster a mix of all users. There is also another aspect to note which is accountLifeSpan, but user with lower accountLifespan tend to have higher emergencyCount and emergencyFunds meaning this may be a more newer feature in shopEasy that user are taking advantage of. Let’s observe hierarchical clustering to check whether the same is true for its clusters. We can notice immediately two spikes in emergencyFunds and emergencyCount with cluster two. It also has the second highest accountType and the second lowest accountLifespan. All similar to k-means++. Due to the efficiency and convenience of using an online wallet, but also having a lower value in other features such as ItemCount users might be using the wallet as budgeting tool using only a certain amount allocated by the user but as well as saving the money for limited time offers without needed to do large bank transfers and so we call our user base Efficient wallet reserver users. These users are 12.3 percent of users in K-means++ and 9.26 percent of users in hierarchical clustering. Still quite similar.

Our fourth cluster also has a very defining feature in both models which is a very low accountLifespan and the highest accountType. In K-means++ they have an accountType value of 0.165837 indicating a number of users in this cluster are between student and regular. It also has below the mean features such as singleItemCosts multipleItemCosts, singleItemBuyFrequency, multipleItemBuyFrequency, and itemCount. This can be explained by the fact that they are all new accounts and have not spent much money on the website. This is also the case for hierarchical clustering where all features mentioned above are below average and also emergencyCount is below average. This can be a defining feature for the fourth cluster which as that their simply New Users, this is mostly because their accountLifespan is very very low compared to the rest of the users. These users make up 6.11 % of users in kmeans++ and 9.39% of users in Hierarchical clustering.

The fifth and final cluster doesn’t really have any defining features. In Kmeans++ it has below average means in all the features except for accountLifeSpan with and accountType of -0.007546. This can indicate that the account has been inactive as although the accountLifespan is quite high or at least above average, its other features are all mediocre in comparison or below average. The account type reveals that its mostly users between premium and regular. The same is said for the cluster in hierarchical clustering model where all features are below average except for accountLifespan and accountType value of -0.017117. This indicates that this cluster is mostly user base of inactive premium/regular users. This user base makes up a large number of the whole dataset of 45.1% in kmeans++ and 39.6% in hierarchical clustering.

To summarize the five clusters are:

1. High spending long term premium/regular users with a focus in single instalment purchases

2. High spending long term premium/regular users with a focus in multiple instalment purchases

3. Efficient wallet reservers

4. New Users who have minimal purchases

5. Inactive premium/regular users

## [Section 5] Conclusions
In conclusion, we have found five customer segments in this shopEasy dataset. Through the multiple analysis we did during our EDA we gained a deeper understanding of the data, following with our preprocessing to clean up the data we further had a clearer vision of where the data was heading. Last but not least, through the clustering algorithms we were able to differ between different types of customers and have a more meaningful insight on the data itself. Through this project we also gained a more profound understanding on clustering models and how unpredictable human behavior can be as we are able to observe the variety in data(although this could be a result of randomly man made data)

In this case we were met with challenges such as choosing the right features for the clustering models. Of course we don't fully know if we are correct or not, but we believe that our reasoning is correct and in a context such as unsupervised reasoning that is what matters the most. Of course we also tried to include other features and test them out but as we mentioned, the evaluation metric, which in this case is the silhuoette score, was not as important as understanding the features and gaining insights from them. Moving on if we were continue from this point, we would try to create a more personalize experience for these cluster of users, creating targetted promotions, special events and increasing over all engagement as we noticed a large number of inactive users. In conclusion, although we did not recieve the best silhuoette scores, we gained a much more significant amount of insight from the clusters we created, and properly segmented the customer base accordingly. 

## Additional:
Since GitHub's rendering of Jupyter notebook does not support the JavaScript-based interactive feature that Plotly graph uses I have uploaded the codes below with their respective graph output.
For K-means++:  

kmeansmodel = KMeans(n_clusters = 5, init = 'k-means++', n_init = 10, random_state = 42)  
labels=kmeansmodel.fit_predict(scaled_df)  
clusters = scaled_df.copy()  
clusters['label'] = labels  
cluster_means = clusters.groupby("label").mean()  
polar = cluster_means.reset_index()  
polar = pd.melt(polar, id_vars=["label"])  
fig = px.line_polar(polar, r="value", theta="variable", color="label", line_close=True, height=800, width=1400)  
fig.show()  

#plot code inspired by https://towardsdatascience.com/clustering-with-more-than-two-features-try-this-to-explain-your-findings-b053007d680a  
This is the output:
<img width="1098" alt="Screenshot 2024-01-02 at 03 44 42" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/7f24195f-f012-4ee1-b67f-2ea5025cf4f2">

pie=clusters.groupby('label').size().reset_index()  
pie.columns=['label','value']  
px.pie(pie,values='value',names='label',color=['red','blue','green','purple','orange'])  
#plot code inspired by https://towardsdatascience.com/clustering-with-more-than-two-features-try-this-to-explain-your-findings-b053007d680a  
This is the output:

<img width="1060" alt="Screenshot 2024-01-02 at 03 55 16" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/a9ec0b90-f696-42aa-9731-594448675d82">

For Hierchical clustering:  
agglomerative_clustering = AgglomerativeClustering(n_clusters=5, metric='euclidean', linkage='ward')  
label_1 = agglomerative_clustering.fit_predict(scaled_df)  
clusters_1 = scaled_df.copy()  
clusters_1['label'] = label_1  
cluster_means1 = clusters_1.groupby('label').mean()  
polar = cluster_means1.reset_index()  
polar = pd.melt(polar, id_vars=["label"])  
fig = px.line_polar(polar, r="value", theta="variable", color="label", line_close=True, height=800, width=1400)  
fig.show()  
#plot code inspired by https://towardsdatascience.com/clustering-with-more-than-two-features-try-this-to-explain-your-findings-b053007d680a  
This is the output:  

<img width="944" alt="Screenshot 2024-01-02 at 04 46 09" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/39d3a055-2653-42ae-8c09-0ffb3c3a7215">

pie=clusters_1.groupby('label').size().reset_index()  
pie.columns=['label','value']  
px.pie(pie,values='value',names='label',color=['red','blue','green','purple', 'orange'])  
#plot code inspired by https://towardsdatascience.com/clustering-with-more-than-two-features-try-this-to-explain-your-findings-b053007d680a  
This is the output:

<img width="954" alt="Screenshot 2024-01-02 at 06 14 25" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/6d488482-be4f-418a-be00-d019dbaccdc0">

and for DBSCAN: 

dbscan_clustering = DBSCAN(eps = 1.2, min_samples =18)  
label_2 = dbscan_clustering.fit_predict(scaled_df)  
clusters_2 = scaled_df.copy()  
clusters_2['label'] = label_2  
cluster_means2 = clusters_2.groupby('label').mean()  
polar = cluster_means2.reset_index()  
polar = pd.melt(polar, id_vars=["label"])  
fig = px.line_polar(polar, r="value", theta="variable", color="label", line_close=True, height=800, width=1400)  
fig.show()  
This is the output:  

<img width="956" alt="Screenshot 2024-01-02 at 04 47 48" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/c5abf456-39ed-4cfe-ade7-9501daa3264b">

pie=clusters_2.groupby('label').size().reset_index()  
pie.columns=['label','value']  
px.pie(pie,values='value',names='label',color=['red','blue','green','purple'])  
#plot code inspired by https://towardsdatascience.com/clustering-with-more-than-two-features-try-this-to-explain-your-findings-b053007d680a  
This is the output:

<img width="979" alt="Screenshot 2024-01-02 at 06 16 17" src="https://github.com/kevinwang2307/ShopEasy-289121/assets/145768116/8d18e103-9563-4367-84f1-5d564f679c1a">

## Bibliography:
“2.3. Clustering.” n.d. Scikit-Learn. https://scikit-learn.org/stable/modules/clustering.html.   
Kiptoon, Diborah. 2023. “Feature Selection in Machine Learning - Diborah Kiptoon - Medium.” Medium, August 18, 2023. https://medium.com/@jdkiptoon/feature-selection-in-machine-learning-20417d052b80.  
Letelier, Mauricio. 2021. “Clustering With More Than Two Features? Try This To Explain Your Findings.” Medium, December 15, 2021. https://towardsdatascience.com/clustering-with-more-than-two-features-try-this-to-explain-your-findings-b053007d680a.   
Mullin, Tara. 2021. “DBSCAN Parameter Estimation Using Python - Tara Mullin - Medium.” Medium, December 15, 2021. https://medium.com/@tarammullin/dbscan-parameter-estimation-ff8330e3a3bd.  
S, Calvin Aziszam. 2022. “Python for Data Science: Implementing Exploratory Data Analysis (EDA) and K-Means Clustering.” Medium, July 17, 2022. https://medium.com/@aziszamcalvin/python-for-data-science-implementing-exploratory-data-analysis-eda-and-k-means-clustering-bcf1d24adc12.




