# Grocery Shopping Optimization 
## About the Project
This project was created by two classmates and myself for our Decision Analytics cours within the MMA program at McGill. 

We were tasked to come up with a problem that we would like to optimize using Gurobi Opimization in Python. 

We decided to optimize a grocery shopping trip to help deal with food insecurity within Toronto. The goal of this project is to deliver a model that provides the lowest-cost grocery list per user by considering lifestyle factors such as desired nutritional intake and travel time to help tackle food insecurity.

The basic model was built by minimizing the cost of purchasing grocery items and the cost of traveling to the grocery store, subject to transportation, nutrients, diversity, and allergy constraints. The objective of the model was that it would automatically determine one store the user should visit for groceries, as well as one recommended traveling mode to achieve the lowest cost. The later part, however, can also be pre-selected by the user. For our model, the user was assumed to reside on the campus of the University of Toronto, and thus, the origin of travel. The stores to be chosen are two Loblaws branches, two No Frills branches, one Metro branch, one Walmart branch, and one Grocery Gateway branch. The modes of transportation include driving, walking, biking, and public transport (Toronto subway). The user is assumed to have an allergy to peanuts to demonstrate the model’s capability of excluding a particular type of ingredient.



# Data Inputs

The data on which the optimization model was built was obtained from the University of Toronto’s (UofT) Food Labelling Information Program (FLIP) curated by the L’Abbe Lab. Data in the FLIP database contains information about packaged food items across different stores in Toronto that is updated every 3-4 years. The application of our model was restricted to the data in the 2020 dataset, as it was the first dataset to map items to the retail stores and include item prices. The data also includes information about item characteristics, such as their food category, container weight, serving size, and nutritional value per serving.  

Here is a sample of what the data looks like: 

# Grocery Shopping Optimization 
## About the Project
This project was created by two classmates and myself for our Decision Analytics cours within the MMA program at McGill. 

We were tasked to come up with a problem that we would like to optimize using Gurobi Opimization in Python. 

We decided to optimize a grocery shopping trip to help deal with food insecurity within Toronto. The goal of this project is to deliver a model that provides the lowest-cost grocery list per user by considering lifestyle factors such as desired nutritional intake and travel time to help tackle food insecurity.

The basic model was built by minimizing the cost of purchasing grocery items and the cost of traveling to the grocery store, subject to transportation, nutrients, diversity, and allergy constraints. The objective of the model was that it would automatically determine one store the user should visit for groceries, as well as one recommended traveling mode to achieve the lowest cost. The later part, however, can also be pre-selected by the user. For our model, the user was assumed to reside on the campus of the University of Toronto, and thus, the origin of travel. The stores to be chosen are two Loblaws branches, two No Frills branches, one Metro branch, one Walmart branch, and one Grocery Gateway branch. The modes of transportation include driving, walking, biking, and public transport (Toronto subway). The user is assumed to have an allergy to peanuts to demonstrate the model’s capability of excluding a particular type of ingredient.



# Data Inputs
## Grocery Data

The data on which the optimization model was built was obtained from the University of Toronto’s (UofT) Food Labelling Information Program (FLIP) curated by the L’Abbe Lab. Data in the FLIP database contains information about packaged food items across different stores in Toronto that is updated every 3-4 years. The application of our model was restricted to the data in the 2020 dataset, as it was the first dataset to map items to the retail stores and include item prices. The data also includes information about item characteristics, such as their food category, container weight, serving size, and nutritional value per serving.  

Here is a sample of what the data looks like: 

| Product ID | Product Name | TRA Category | Ingredients | Store Code | Container Size (mL) | Container Size (g) |
|------------|--------------|--------------|-------------|------------|---------------------|--------------------|
|    NA         | NA              |   NA            |   NA           |       NA      |       NA               |        NA             |


| Regular   Price | Price per 100 g | Serving Size on NFT (other than   grams) | Container   Size (as indicated on package) | KCAL | FAT | SATFAT |
|-----------------|-----------------|------------------------------------------|--------------------------------------------|------|-----|--------|
|            NA     |      NA         NA    |  NA                                       |                                           NA |     NA  | NA     |      NA   |

| TRANS | CHOL | NA | CHO | FIBRE | SUGAR | FREESUG | PRO |
|-------|------|----|-----|-------|-------|---------|-----|
|     NA   | NA      |  NA   | NA     |   NA     | NA       |     NA     |   NA   |

| K | VITA | VITC | CALCIUM | IRON |
|---|------|------|---------|------|
| NA   |  NA     |   NA    |   NA       |  NA     |


## Google Maps Data

The distance and time information were obtained by retrieving a distance matrix from the Google Maps API. Since our model assumes that the user will want to visit only one store when grocery shopping, only the distances of the shortest paths between the origin and all the seven stores and their corresponding travel times were kept. To facilitate the development of the model, the distance and travel time of the round trip between each store and the origin were calculated by adding the metrics of the trips in both ways. This process was repeated for four different modes of travel, namely driving, walking, biking, and public transport (Toronto subway) to make the model more inclusive and to reflect the reality of the different travel options available to different groups of society more closely. 


Total distance and travel time between the origin and each store for driving:

 
 |     Store              |     Travel Distance (m)    |     Travel Duration (s)    |
|------------------------|----------------------------|----------------------------|
|     Loblaws MLG        |     4356                   |     1012                   |
|     No Frills          |     7482                   |     1705                   |
|     No Frills Joe's    |     5520                   |     1483                   |
|     Walmart            |     51655                  |     3777                   |
|     Grocery Gateway    |     8676                   |     1754                   |
|     Loblaws            |     2155                   |     2669                   |
|     Metro              |     3836                   |     911                    |


Total distance and travel time between the origin and each store for walking:

|     Store              |     Travel Distance (m)    |     Travel Duration (s)    |
|------------------------|----------------------------|----------------------------|
|     Store              |     Travel Distance (m)    |     Travel Duration (s)    |
|     Loblaws MLG        |     2826                   |     2199                   |
|     No Frills          |     7112                   |     5516                   |
|     No Frills Joe's    |     4613                   |     3483                   |
|     Walmart            |     38150                  |     28753                  |
|     Grocery Gateway    |     7520                   |     5730                   |
|     Loblaws            |     4628                   |     3517                   |
|     Metro              |     2472                   |     1913                   |


Total distance and travel time between the origin and each store for the subway:

|     Store              |     Travel Distance (m)    |     Travel Duration (s)    |
|------------------------|----------------------------|----------------------------|
|     Store              |     Travel Distance (m)    |     Travel Duration (s)    |
|     Loblaws MLG        |     2826                   |     2199                   |
|     No Frills          |     7112                   |     5516                   |
|     No Frills Joe's    |     4613                   |     3483                   |
|     Walmart            |     38150                  |     28753                  |
|     Grocery Gateway    |     7520                   |     5730                   |
|     Loblaws            |     4628                   |     3517                   |
|     Metro              |     2472                   |     1913                   |


Total distance and travel time between the origin and each store for biking:


|     Store              |     Travel Distance (m)    |     Travel Duration (s)    |
|------------------------|----------------------------|----------------------------|
|     Loblaws MLG        |     3191                   |     816                    |
|     No Frills          |     7579                   |     2073                   |
|     No Frills Joe's    |     5395                   |     1373                   |
|     Walmart            |     40373                  |     8685                   |
|     Grocery Gateway    |     8776                   |     1935                   |
|     Loblaws            |     4668                   |     1023                   |
|     Metro              |     2837                   |     707                    |


# Model Output
The output of the linear optimization model determined Joe’s No Frills as the optimal grocery to shop at along with biking as the optimal mode of transportation. These results satisfy the travelling time constraint as well as minimize the travelling cost.The total cost of all the items at Joe’s No Frills is $28.36. 

Grocery list from the model output: 
|     Food Product                        |     Quantity    |
|-----------------------------------------|-----------------|
|     Sparkling Passion Fruit Beverage    |     1           |
|     Parle Krackjack Cookies             |     1           |
|     Pear J Sparkling Pear Drink         |     1           |
|     Grade A White Eggs, Large           |     1           |
|     Hazelnut Wafers                     |     1           |
|     Whole Leaf Spinach                  |     1           |
|     Chicken Hot Dogs                    |     2           |
|     Luncheon Meat                       |     1           |
|     Whole Flaxseed                      |     1           |
|     Sliced Mushrooms                    |     1           |
|     Yellow Split Peas                   |     2           |
|     Lupini Beans                        |     2           |

Total nutritional information from the model output: 

|     Nutrient             |     Value    |
|--------------------------|--------------|
|     Calories (kcal)      |     20991    |
|     Protein (g)          |     1401     |
|     Fat (g)              |     841      |
|     Trans Fat (g)        |     2        |
|     Saturated Fat (g)    |     143      |
|     Carbohydrates (g)    |     2175     |
|     Fibre                |     1049     |
|     Sugar (g)            |     240      |
|     Sodium (mg)          |     12985    |
|     Cholesterol (mg)     |     2196     |
|     Vitamin A (mg)       |     593      |
|     Vitamin C (mg        |     169      |
|     Calcium (mg)         |     8838     |
|     Iron (mg)            |     224      |
|     Potassium (mg)       |     41795    |



