# Influencer Analysis Report
Analysis of American Influencer based on their Instagram datasets (Marketing Analytics Kompas Gramedia Recruitment Test)

### Background
Influencer now is the essential parts for promoting business product. Besides emerging Interesting Job in Digital Era

With the Big numbers of World Wide Internet Users are reach **4,66 Billions**, Besides Instagram is the one of Social Media with the most users from whole internet users that Approximately 1 Billions Monthly Users

## Data Collections
There is a .xls file containing these data 
- Influencer Data: contains a list of influencers and their statistics including followers, likes, posts, prices, gender, account created, category ID.
  - which have 220 rows and 13 columns
  - and this data is clean because has no duplicates and missing value   
- Influencer Category: contains category group, category ID, and category name.
  - which have 21 rows and 3 columns
  - and this data is clean because has no duplicates and missing value
- Influencer Agency: contains agency location, agency location ID, and agency fee.
  - which have 45 rows and 3 columns
  - and this data is clean because has no duplicates and missing value

Then those datasets combined one by one with merge functions from pandas library which is Influencer Data and Influencer Category combined using id column `Category ID` as key to be the first temp data, and then first temp data combined with Influencer Agency using id column `Agency Location ID` as key as final temp. Then it exported to new `.csv` that called `influencer_dataset.csv` with `Index=False` as parameter to avoid `unnamed: 0` column.

```
# first temp dataset 
influencer_temp = pd.merge(left=influencer_data, right=influencer_categ, left_on='Category ID', right_on='Category ID')

# final temp dataset
influencer_final = pd.merge(left=influencer_temp, right=influencer_agen, left_on='Agency Location ID', right_on='Agency Location ID')
```

## Data Inspection
then `influencer_dataset.csv` loaded that have 220 rows and 17 columns contained, and the data still clean and no duplicates.

But the Data Cleaning is done by Data Transformation about date column `Account Created` with `object` datatype to be `datetime`. And then for `Follower` which is should be integer, but actually in this case the data type is `object`. So the transformation of this column involving for loop iteration to iterate each rows and define the empty list to store the iterated rows, with using condition if string contains million convert to be millions, else string contains thousand convert to be thousand that involving changing data type from float until int.
```
foll_temp = []
# iterate df column
for colname, colval in influencer_df.iterrows():
    # if df follower == str thousands
    if 'thousand' in colval['Followers']:
        # remove "thousands" menggunakan replace 
        num1 = colval['Followers'].replace('thousand','')
        # convert into numeric and multiple by 1000
        num1 = int(float(num1)*1000)
        foll_temp.append(num1)
    # elif df follower == str million
    else:
        # remove "million" menggunakan replace 
        num2 = colval['Followers'].replace('million','')
        # convert into numeric and multiple by 1000000
        num2 = int(float(num2) * 1000000)
        foll_temp.append(num2)
 
foll_temp = pd.Series(foll_temp)
influencer_df['Followers'] = foll_temp
```

## Exploratory Data Analysis
Exploratory Data Analysis with Pandas, Matplotlib and Seaborn library.

### INFLUENCER CATEGORY
![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/category_group1.png)

From This Type, **most influencer** comes from **Auto & Vehicles** followed by **Art & Design**


![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/category_group2.png)

From This Type, most **influencer** are come from **business category**, followed by **Finance and Games**


![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/category_group3.png)

From This Type, Looks like the **top 3 category** with most influencers are **Shopping**, **Music & Audio** and **News & Magazine**


![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/category_group4.png)

Looks like this type of category has **smallest number** of influencers, that mostly from **Socials**


### INFLUENCER CATEGORY WITH MOST FOLLOWERS
![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/follower_category_group1.png)

Even the **most influencer** comes from **Auto & Vehicles** and **Art & Design**, But **Beauty** is the category which **interest most followers**


![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/follower_category_group2.png)

**Business** has **most influencer**, also **has most followers at runner up**. Because **Comics** has **bigger followers** than **Business** Even **has the smallest influencers**


![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/follower_category_group3.png)

**Music & Audio** has **most influencer**, also **has most followers at runner up**. But **House & Home** has **the most followers**.


![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/follower_category_group4.png)

Even **Travel & Local** has the **smaller influencers** than **Social**, But the it Has the **bigger Followers** more than **Social**


### INFLUENCER AGENCY LOCATIONS
![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/most_agency_loc.png)

**South Carolina** is the Agency Location with Most Influencers, Followed by **Illinois**, **New Mexico**, **Maryland**, **Florida**, **Massachusetts** and **Mississippi**.


![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/agency_with_most_fees.png)

And the Agency Location with Most Influencer are High Paying Fees, Start From **South Carolina**, **Illinois**, **Maryland** and **Massachusetts**. But it’s Look Like **New Mexico**, **Mississippi** and **Florida** are cheaper


### INFLUENCER ENGANGEMENT 
#### MOST ACTIVE INFLUENCERS

![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/most_foll_influen.png)

**@tawnyprevost**, **@joaneewan**, **@venniestamp**, **@gingerwimbush** and **@sharricroslin** have **the biggest followers**


![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/most_post_influen.png)

But those influencers have the most followers didn’t make some post. Because **@praek**, **@robbidennie** and **@tarrapetri** are have **4.5 million followers** even though they have reach **4210 posts**


![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/most_postlikes_influen.png)

But made some posts are doesn’t affect user’s willingness to do many likes, in case **@charlesettatatem**  which have **842892 likes** but only have **422 Posts**, and then here are **@praek**, **@robbidennie** and **@tarrapetri** that only have **450227 Likes**



![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/most_postcom_influen.png)

**@armandcote** have active followers that has been made for **11563 average of comments** that has huge follower **even under 7.9 Millions followers**


#### INFLUENCER COST

![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/most_postprice_influen.png)

**@gerdanegri**, **@vannaemigh** and **@lilianleggett** are the top paid influencer for each **feed post**, those have **made their post** that reach **111**


![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/most_videoprice_influen.png)

**@robbiedennie**, **@tarrapetri** and **@oraek** are the top paid influencer for **each video post** that the **highest type of post**, who is also the influencer with the **biggest number of posts**


![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/most_storyprice_influen.png)

**@lilianleggett**, **@gerdanegri** and **@vannaemigh** are the top paid influencer for each instastory, which also are top paid influencer for each **feed post**. 


### Correlation analysis

![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/multivar_corr.png)

Find out the correlation from each features, which the biggest number of positive correlation is fell on price per video post that around category of post price 


![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/price_post_corr.png)

Then check the correlation between post with each price category, that **video post have the most positive correlation** with **Price of Each Video Post**. That can be conclude that **instagram video post can motivate influencer** to post **more video** than other category.


![](https://github.com/hendrywijaya98/American-Influencer-Analysis-Project/blob/main/images/enggange_corr.png)

Checking about correlation between Followers, Post, with Average Likes and Comment. **Average Likes have positive correlation with Average Comment** which looks like that **follower’s like can trigger follower’s comments**. For the followers doesn’t have interesting correlation because the positive correlation of post and average post are not too big.

## CONCLUSIONS
Closing Statement with the most interesting Fact

**Influencer** are **like to Post Video** rather that other category because the **high paid**, and the rest about Category, Agency Location doesn’t have Significant Effect
