# Grocery Shopping Optimization 
## About the Project
This project was created by two classmates and myself for our Decision Analytics cours within the MMA program at McGill. 

We were tasked to come up with a problem that we would like to optimize using Gurobi Opimization in Python. 

We decided to optimize a grocery shopping trip to help deal with food insecurity within Toronto. The goal of this project is to deliver a model that provides the lowest-cost grocery list per user by considering lifestyle factors such as desired nutritional intake and travel time to help tackle food insecurity.

The basic model was built by minimizing the cost of purchasing grocery items and the cost of traveling to the grocery store, subject to transportation, nutrients, diversity, and allergy constraints. The objective of the model was that it would automatically determine one store the user should visit for groceries, as well as one recommended traveling mode to achieve the lowest cost. The later part, however, can also be pre-selected by the user. For our model, the user was assumed to reside on the campus of the University of Toronto, and thus, the origin of travel. The stores to be chosen are two Loblaws branches, two No Frills branches, one Metro branch, one Walmart branch, and one Grocery Gateway branch. The modes of transportation include driving, walking, biking, and public transport (Toronto subway). The user is assumed to have an allergy to peanuts to demonstrate the model’s capability of excluding a particular type of ingredient.



# Data Inputs

The data on which the optimization model was built was obtained from the University of Toronto’s (UofT) Food Labelling Information Program (FLIP) curated by the L’Abbe Lab. Data in the FLIP database contains information about packaged food items across different stores in Toronto that is updated every 3-4 years. The application of our model was restricted to the data in the 2020 dataset, as it was the first dataset to map items to the retail stores and include item prices. The data also includes information about item characteristics, such as their food category, container weight, serving size, and nutritional value per serving.  

Here is a sample of what the data looks like: 

| Product ID | Product Name | TRA Category | Ingredients | Store Code | Container Size (mL) | Container Size (g) |
|------------|--------------|--------------|-------------|------------|---------------------|--------------------|
|            |              |              |             |            |                     |                    |


| Regular   Price | Price per 100 g | Serving Size on NFT (other than   grams) | Container   Size (as indicated on package) | KCAL | FAT | SATFAT |
|-----------------|-----------------|------------------------------------------|--------------------------------------------|------|-----|--------|
|                 |                 |                                          |                                            |      |     |        |

| TRANS | CHOL | NA | CHO | FIBRE | SUGAR | FREESUG | PRO |
|-------|------|----|-----|-------|-------|---------|-----|
|       |      |    |     |       |       |         |     |

| K | VITA | VITC | CALCIUM | IRON |
|---|------|------|---------|------|
|   |      |      |         |      |
