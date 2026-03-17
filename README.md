# Coupons Dataset


## Introduction

## Data Cleaning
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
## Exploratory Analysis

#### 4.  What proportion of bar coupons were accepted?
827 of 2017 or 41 percent of individuals in the Bar used the coupon

#### 5. Compare the acceptance rate between those who went to a bar 3 or fewer times a month to those who went more.

* those who went to a bar 3 or fewer times a month

<img src="./notebooks/images/bar_less_three.png" width="300" height="300" alt="Alt text description" />

## Exploratory Analysis

* those who went more

<img src="./notebooks/images/bar_greater_than_three.png" width="300" height="300" alt="Alt text description" />

#### 6. Compare the acceptance rate between drivers who go to a bar more than once a month and are over the age of 25 to the all others. Is there a difference?

* drivers who go to a bar more than once a month and are over the age of 25

For this analysis ```data[data['car'] != 'do not drive'] # remove 'do not drive']```  removed the non-drivers.

<img src="./notebooks/images/drivers_more_than_once_over25.png" width="300" height="300" alt="Alt text description" />

* all the others

<img src="./notebooks/images/all_less_than_once_less25.png" width="300" height="300" alt="Alt text description" />

#### 7. Use the same process to compare the acceptance rate between drivers who go to bars more than once a month and had passengers that were not a kid and had occupations other than farming, fishing, or forestry.¶

<img src="./notebooks/images/drivers_more_than_once_no_kids.png" width="300" height="300" alt="Alt text description" />

#### 8. ompare the acceptance rates between those drivers who:

*  go to bars more than once a month, had passengers that were not a kid, and were not widowed 

<img src="./notebooks/images/drivers_more_tdrivers_more_than_once_no_kids_not_widowedhan_once_no_kids.png" width="300" height="300" alt="Alt text description" />

*  go to bars more than once a month and are under the age of 30 OR

<img src="./notebooks/images/drivers_more_than_once_under_30.png" width="300" height="300" alt="Alt text description" />

*  go to cheap restaurants more than 4 times a month and income is less than 50K.

<img src="./notebooks/images/drivers_cheap_more_than_four_income_less_50.png" width="300" height="300" alt="Alt text description" />


## Conclusion



