# Coupons Dataset

## Introduction
**Will a customer accept the coupon?**
In this excercise we analysed data from the UCI Machine Learning Repository to determine the circumstances that increase the probability a customer will accept a coupon.
In the first section,  Questions data cleaning required removing nan Values, then considering empty values and duplicate rows. Then in Directed Analysis, the required set of grouping and filering questions were completed. The second section, Independent Investigations began with filtering on the restaurants20to50 and different groups where the intuition was developed that youger people, 31 or younger with friends seemed more inclined to accept couponts.  Then huntch was then verified emperically by looking at all five coupon categories and doing the same filtering. In all venues, younger people with friends had a higher percentage of acceptance. Then in the last two sections weather and temperature were explored  using first crosstab with seaborn heatmaps, then groupby-mean valuecounts to generate a comtination table.  In both excercises it was clear that warm sunny days have much higher acceptance rates. In a surprise, snowy days were a strong third place.  The conclusion, which should come as no surprise, coupons are accepted more readily on warm sunny days by younger people with friends.  

This is the summary of data exploration contained on the Jupyter Notebook. 
1. Guided quesions [5.1 Questions](./notebooks/prompt-work.ipynb)
1. Independent investigation [Independent](./notebooks/prompt-work-independent.ipynb)

## Guided Questions
### Data Cleaning
#### 1. Nan Values

 A subset of the 26 columns had Nan values.
  These were cleaned up with  

```data['car'] = data['car'].fillna('')``` 


| Column  | Nan Count | 
| --- | --- | 
| car| 12576 | 
| Bar| 107| 
|CoffeeHouse|217
|CarryAway|151|
|RestaurantLessThan20 | 130 |
|Restaurant20To50|189|

#### 2. Empty Values

The **car** column only had 108 filled values 
* Scooter and motorcycle,
* crossover,
* Mazda5,
* do not drive,
* Car that is too old to install Onstar :D

The Car column is less than 1 percent of the data, but it is interesting. Perhaps is we isolate the labeled cars we might see that folks that 'do not drive' or use 'Scooter and motercle' may be more amenable to using a coupon.

The decision was made to keep these values

#### 3. Duplicate Rows

```len(data[data.duplicated() == True])``` revealed 74 duplicate rows.

74 of the 12684 rows are duplicates. Its unclear if these are problems with the data or if the two individual of the same profile were surveyed at the same time. Given the time is a rough measure of time - no minutes or seconds - is it possible that more than one person who met the same profile were surveyed. Perhaps they were together? Even if they are duplicates they represent 0.6 percent of the data, so we will keep them in.

## Directed Analysis

### Bar Customers

#### 1. What proportion of the total observations chose to accept the coupon?

7210 of 12684 or 57 percent of the observations accepted the coupon

#### 2.  Use a bar plot to visualize the coupon column.
 
<img src="./notebooks/images/all_yes.png" width="300" height="300" alt="Alt text description" />

#### 3. Use a histogram to visualize the temperature column.

<img src="./notebooks/images/temperature.png" width="300" height="300" alt="Alt text description" />


#### 4.  What proportion of bar coupons were accepted?
827 of 2017 or 41 percent of individuals in the Bar used the coupon

#### 5. Compare the acceptance rate between those who went to a bar 3 or fewer times a month to those who went more.

* Those who went to a bar 3 or fewer times a month

<img src="./notebooks/images/bar_less_three.png" width="300" height="300" alt="Alt text description" />


* Those who went more

<img src="./notebooks/images/bar_greater_than_three.png" width="300" height="300" alt="Alt text description" />

#### 6. Compare the acceptance rate between drivers who go to a bar more than once a month and are over the age of 25 to the all others. Is there a difference?

* Drivers who go to a bar more than once a month and are over the age of 25

For this analysis ```data[data['car'] != 'do not drive'] # remove 'do not drive']```  removed the non-drivers.

<img src="./notebooks/images/drivers_more_than_once_over25.png" width="300" height="300" alt="Alt text description" />

* All the others

<img src="./notebooks/images/all_less_than_once_less25.png" width="300" height="300" alt="Alt text description" />

#### 7. Use the same process to compare the acceptance rate between drivers who go to bars more than once a month and had passengers that were not a kid and had occupations other than farming, fishing, or forestry.¶

<img src="./notebooks/images/drivers_more_than_once_no_kids.png" width="300" height="300" alt="Alt text description" />

#### 8. Ccompare the acceptance rates between those drivers who:

*  Go to bars more than once a month, had passengers that were not a kid, and were not widowed 

<img src="./notebooks/images/drivers_more_than_once_no_kids_not_widowed.png" width="300" height="300" alt="Alt text description" />

*  Go to bars more than once a month and are under the age of 30 OR

<img src="./notebooks/images/drivers_more_than_once_under_30.png" width="300" height="300" alt="Alt text description" />

*  Go to cheap restaurants more than 4 times a month and income is less than 50K.

<img src="./notebooks/images/drivers_cheap_more_than_four_income_less_50.png" width="300" height="300" alt="Alt text description" />

Sixty-one percent of drivers who do to less than 20 dollar restaurants, more than 4 times a month, and make less than 50K use coupons.


---

## Independent Investigations
  Thie part is at the Independent Investigations part of
  [5.1 Questions](./notebooks/prompt-work.ipynb)


### Expensive Restaurants

Looking at the set of individuals at Restaurant20To50, some exploratory experimentation yielded interesting results.

* 264 individuals went to expensive restaurants, and 175 or sixty-six percent accepted coupons
* If these individual had kids the positive rate was 55 percent
* With friends the yes ratio is 69%

| Restaurant20To50  | Count  | Yes | Coupon Acceptance Rate| 
| --- | --- | --| --|
| | 264 | 175 | 66% | 
| With Kids| 11| 6 | 54%|
| With Friends| 91 |63| 69%|
|With Pargner|5|5|65%|

### Above 50 years old
| 50plus  | Count  | Yes | Coupon Acceptance Rate| 
| --- | --- | --| --|
| | 473 | 280 | 59% | 
| With Friends| 91 |63| 69%|
|Alone|1595|875|55%|

### Young - 21, 26 or 31
| Young  | Count  | Yes | Coupon Acceptance Rate| 
| --- | --- | --| --|
| | 7251 | 4226 | 58% | 
| With Friends| 1906 |1332| 70%|
|Alone|4240|2266|54%|

### Coffee House - Greater than 8 times a month
| Coffee House gt8  | Count  | Yes | Coupon Acceptance Rate| 
| --- | --- | --| --|
| | 1111 | 648 | 58% | 
| With Friends| 1906 |1332| 70%|
| With Kids| 516 |284| 55%|
| With Friends| 286 |191| 67%|
|Alone|666|366|55%|

### Young - (21, 26 or 31), Coffee House, With Friends, Greater than 8 times a month

|   | Count  | Yes | Coupon Acceptance Rate| 
| --- | --- | --| --|
| | 173 | 117 | 68% | 
| 7AM| 0 || |
| 2PM| 66 |51| 77%|
| 10PM| 33 |20| 60%|

## It looks like younger people with friends accept more coupons, and the time of day matters

## More Independent work [Independent](./notebooks/prompt-work-independent.ipynb)

Having established the intuition that younger people with friends are more ammenable to acceptinng coupons, I decided to do systematic study of the five different coupon types.
For each group I selected moderate traffic ['4~8', '1~3', 'gt8'], then compared with friends to alone.  Then I filtered then to younger population ["21", "26", "31"] then compared Young, Young Alone, Young with Frieds, then Young with Friends at 2 PM, 6 PM, and 10 PM.  The results revealed that in all categories Moderate customers who were young with friends were more accepting of coupons, and the time is a factor.  

### CoffeeHouse

|  CoffeeHouse | Ratio  | Acceptance Rate| 
| --- | --- | --|
|Moderate | 1269/1922 | 66.02497398543184|
|Friends  |461/604  |76.32450331125827|
|Alone  |643/1089  |59.04499540863177|
|Young  |760/1139 | 66.72519754170325|
|Young  and Alone  |378/640 |59.06249999999999|
|Young with Friends  |284/370 | 76.75675675675676|
|Two PM  |153/199 | 76.88442211055276|
|Six PM  |32/50  |64.0|
|Ten PM  |21/32  |65.625|

### RestaurantLessThan20 

|  RestaurantLessThan20 | Ratio  | Acceptance Rate| 
| --- | --- | --|
|Moderate | 1649/3245 | 50.81664098613251|
|Friends  |604/989 | 61.071789686552066|
|Alone  |810/1825  |44.38356164383562|
|Young  |985/1886  |52.226935312831394|
|Young  and Alone | 473/1068  |44.28838951310862|
|Young with Friends | 373/581 | **64.19965576592082**|
|Two PM  |194/304 | 63.81578947368421|
|Six PM  |46/79  |58.22784810126582|
|Ten PM  |35/51 | **68.62745098039215**|

### RestaurantRestaurant20To50LessThan20 

|  RestauranRestaurant20To50tLessThan20 | Ratio  | Acceptance Rate| 
| --- | --- | --|
|Moderate | 719/1350 | 53.25925925925926|
|Friends | 263/406  |64.77832512315271|
|Alone  |339/751  |45.13981358189081|
|Young  |434/819  |52.991452991452995|
|Young  and Alone  |210/453  |46.35761589403973|
|Young with Friends|  161/253 | **63.63636363636363**|
|Two PM  |82/131  |62.59541984732825|
|Six PM  |19/34  |55.88235294117647|
|Ten PM  |19/25  |**76.0**|

### Bar 

|  Bar | Ratio  | Acceptance Rate| 
| --- | --- | --|
|Moderate | 625/1245 | 50.20080321285141|
|Friends | 244/406 | 60.09852216748769|
|Alone  |313/708  |44.2090395480226|
|Young  |461/925  |49.83783783783784|
|Young  and Alone | 232/533  |43.52720450281426|
|Young with Friends|  186/308  |**60.3896103896104**|
|Two PM|  101/165 | **61.212121212121204**|
|Six PM|  25/49  |51.02040816326531|
|Ten PM|  12/20  |60.0|

### CarryAway

|  CarryAway | Ratio  | Acceptance Rate| 
| --- | --- | --|
|Moderate | 1698/3322|  51.11378687537628|
|Friends | 633/1037 | 61.041465766634516|
|Alone  |848/1869  |45.37185660781166|
|Young  |1051/2029 | 51.79891572203056|
|Young  and Alone|  511/1139  |44.863915715539946|
|Young with Friends|  403/644  |**62.577639751552795**|
|Two PM | 206/340  | 60.588235294117645 |
|Six PM | 48/86  |55.81395348837209|
|Ten PM | 38/55 | **69.0909090909091**|


### Category Work
For this analysis I learned how to use the astype('category') command to turn categorical values into something plottable by seaborn. 
```
for col in df.columns:
    df[col] = df[col].astype('category')
```
Then by using the pandas crosstab command I was able to render seaborn heatmaps with a category compared to 'Y'. The following are seaborn heat maps for a collection of categories.

<img src="./notebooks/images/weather.png" width="300" height="300" alt="Alt text description" />


<img src="./notebooks/images/temperature.png" swidth="300" height="300" alt="Alt text description" />


<img src="./notebooks/images/female_coffee_friends.png" width="300" height="300" alt="Alt text description" />


## Combinations
I also learned how to use the groupby + mean feature. Here I looked at 
weather and temperature and all its combinations, using the value_counts was able to capture all combinations and the number of 1's.

**This shows that Warm Sunny days are best for coupon acceptance.
It is interesting that Snowy day showed a strong third place**

|  weather | temperature  | Y | 
| --- | --- | --|
|Sunny |	80| 	3919|
|Sunny |	55| 	1501|
|Snowy |	30| 	661|
|Sunny |	30| 	569|
|Rainy |	55| 	560|
|Rainy |	80| 	0|
|Rainy |	30| 	0|
|Snowy |	55| 	0|
|Snowy 	|80 |	0|


## Conclusion


In this study I tried several methods of analysis.  At first, I just explored the data with different filters and came upon the intuition that younger customsers with friends seemed more responsive to accepting coupons.  This was confirmed by the systematic comparison of the five different coupon types where in every category younger customers with friends were more accepting of coupons.  This was further qualified by the time of day showing some times were bette for different places. 

Finally I looked at temperature and weather using pandas cross tab graphs and combinations using groupby, mean with value counts. In both experiments coupons were more accepted in warm sunny days.

## Further work
This excercise was interesting give  the variety of categories.  To make this empirical, it would be a good excercise to quantify the categories and their correlation to 1 and 0 using a regression model. I don't know what the algorithms is. This has been difficult using lables rather than numerical data, but there should be some way to test all the combinations and find which one's result in the greatest number of coupon acceptance. 
