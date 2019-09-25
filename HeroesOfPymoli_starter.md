
### Note
* Instructions have been included for each segment. You do not have to follow them exactly, but they are included to help you think through the steps.


```python
# Dependencies and Setup

import pandas as pd
import numpy as np

# File to Load (Load file as per path)
file_to_load = "Resources/purchase_data.csv"

# Read Purchasing File and store into Pandas data frame
purchase_data = pd.read_csv(file_to_load)
purchase_data.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
    </tr>
    <tr>
      <td>1</td>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
    </tr>
    <tr>
      <td>2</td>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
    </tr>
    <tr>
      <td>3</td>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
    </tr>
    <tr>
      <td>4</td>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
    </tr>
  </tbody>
</table>
</div>



## Player Count

* Display the total number of players



```python
numberofplayers=purchase_data['SN'].value_counts()

players_df = pd.DataFrame({
    "Total Players": [len(numberofplayers)]
})
players_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Players</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>576</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Total)

* Run basic calculations to obtain number of unique items, average price, etc.


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame



```python
#Take Price Column and Sum
Total_Revenue=purchase_data["Price"].sum()
#print(f"Total Revenue :",Total_Revenue)

#Take Price Column and find Mean
Avg_Purchase_Price=purchase_data["Price"].mean()
#print(f"Average Purchase Price :",round(Avg_Purchase_Price,2))

#Take Price Column and find total count
Total_Number_Purchase=purchase_data["Price"].count()
#print(f"Total Number of Purchase :", Total_Number_Purchase)

# FInd number of Unique Value
Number_Unique_Item=purchase_data["Item Name"].nunique()
#print(f"Number of Unique Item :", Number_Unique_Item)

# Create DataFrame Using above varibales

purchasing_df = pd.DataFrame({
    "Number of Unique Items": [Number_Unique_Item],
    "Average Price $"       : [round(Avg_Purchase_Price,2)],
    "Number of Purchases"   : [Total_Number_Purchase],
    "Total Revenue $"       : [Total_Revenue]
})
purchasing_df

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Number of Unique Items</th>
      <th>Average Price $</th>
      <th>Number of Purchases</th>
      <th>Total Revenue $</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>179</td>
      <td>3.05</td>
      <td>780</td>
      <td>2379.77</td>
    </tr>
  </tbody>
</table>
</div>



* Percentage and Count of Male Players


* Percentage and Count of Female Players


* Percentage and Count of Other / Non-Disclosed





```python
# #Group by Gender & SN, find unique values

gender_count = purchase_data.groupby('Gender')['SN'].nunique()
Total_Gender_Count = purchase_data.groupby('Gender')['SN'].nunique().sum()


percentage_gender = (gender_count/Total_Gender_Count)*100

#print(percentage_gender)

gender_demo = pd.DataFrame({
                        "Total Counts": gender_count,
                        "Percentage of Players": round(percentage_gender,2),
                       })
# Index Added
# gender_demo.index = (["Female", "Male", "Other / Non-Disclosed"])
gender_demo.sort_values('Total Counts',ascending = False)


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Counts</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Male</td>
      <td>484</td>
      <td>84.03</td>
    </tr>
    <tr>
      <td>Female</td>
      <td>81</td>
      <td>14.06</td>
    </tr>
    <tr>
      <td>Other / Non-Disclosed</td>
      <td>11</td>
      <td>1.91</td>
    </tr>
  </tbody>
</table>
</div>




## Purchasing Analysis (Gender)

* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. by gender




* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
# Group by Gender
gender_group_purchase_data = purchase_data.groupby(["Gender"])
gender_group_purchase_data.count()

purchase_count=gender_group_purchase_data["SN"].count()
#print(purchase_count)

avg_purchase_price=gender_group_purchase_data["Price"].mean()
#print(avg_purchase_price)

total_purchase_value=gender_group_purchase_data["Price"].sum()
#print(total_purchase_value)


avg_purchase_price_perperson = round((gender_group_purchase_data["Price"].sum() / gender_count),2)
#print(avg_purchase_price_perperson)


# Create new DataFrame
purchase_analysis_gender = pd.DataFrame({ "Purchase Count"               : purchase_count,
                                          "Average Purchase Price"       : round(avg_purchase_price,2),
                                          "Total Purchase Value"         : total_purchase_value,
                                          "Avg Total Purchase per Person": avg_purchase_price_perperson})

purchase_analysis_gender
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Avg Total Purchase per Person</th>
    </tr>
    <tr>
      <th>Gender</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Female</td>
      <td>113</td>
      <td>3.20</td>
      <td>361.94</td>
      <td>4.47</td>
    </tr>
    <tr>
      <td>Male</td>
      <td>652</td>
      <td>3.02</td>
      <td>1967.64</td>
      <td>4.07</td>
    </tr>
    <tr>
      <td>Other / Non-Disclosed</td>
      <td>15</td>
      <td>3.35</td>
      <td>50.19</td>
      <td>4.56</td>
    </tr>
  </tbody>
</table>
</div>



## Age Demographics

* Establish bins for ages


* Categorize the existing players using the age bins. Hint: use pd.cut()


* Calculate the numbers and percentages by age group


* Create a summary data frame to hold the results


* Optional: round the percentage column to two decimal points


* Display Age Demographics Table



```python
age_bins = [0, 9.99, 14.99, 19.99, 24.99, 29.99, 34.99, 39.99, 100]
group_names = ["<10", "10-14", "15-19", "20-24", "25-29", "30-34", "35-39", "40+"]

purchase_data["Age_Summary"]= pd.cut(purchase_data["Age"], age_bins, labels=group_names)
purchase_data

purchase_data.head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase ID</th>
      <th>SN</th>
      <th>Age</th>
      <th>Gender</th>
      <th>Item ID</th>
      <th>Item Name</th>
      <th>Price</th>
      <th>Age_Summary</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>0</td>
      <td>0</td>
      <td>Lisim78</td>
      <td>20</td>
      <td>Male</td>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>3.53</td>
      <td>20-24</td>
    </tr>
    <tr>
      <td>1</td>
      <td>1</td>
      <td>Lisovynya38</td>
      <td>40</td>
      <td>Male</td>
      <td>143</td>
      <td>Frenzied Scimitar</td>
      <td>1.56</td>
      <td>40+</td>
    </tr>
    <tr>
      <td>2</td>
      <td>2</td>
      <td>Ithergue48</td>
      <td>24</td>
      <td>Male</td>
      <td>92</td>
      <td>Final Critic</td>
      <td>4.88</td>
      <td>20-24</td>
    </tr>
    <tr>
      <td>3</td>
      <td>3</td>
      <td>Chamassasya86</td>
      <td>24</td>
      <td>Male</td>
      <td>100</td>
      <td>Blindscythe</td>
      <td>3.27</td>
      <td>20-24</td>
    </tr>
    <tr>
      <td>4</td>
      <td>4</td>
      <td>Iskosia90</td>
      <td>23</td>
      <td>Male</td>
      <td>131</td>
      <td>Fury</td>
      <td>1.44</td>
      <td>20-24</td>
    </tr>
  </tbody>
</table>
</div>




```python
group_data = purchase_data.groupby(['SN', 'Age_Summary'])['Age'].count()
#print(group_data)

total_counts = group_data.groupby('Age_Summary').count()
total_counts

# %Calcualtions
percentage =round((total_counts/len(group_data))*100,2)
percentage
age_demographics = pd.DataFrame ({
                                      "Total Counts"          : total_counts,
                                      "Percentage of Players" : percentage,
                                  })
age_demographics

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Total Counts</th>
      <th>Percentage of Players</th>
    </tr>
    <tr>
      <th>Age_Summary</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>&lt;10</td>
      <td>17</td>
      <td>2.95</td>
    </tr>
    <tr>
      <td>10-14</td>
      <td>22</td>
      <td>3.82</td>
    </tr>
    <tr>
      <td>15-19</td>
      <td>107</td>
      <td>18.58</td>
    </tr>
    <tr>
      <td>20-24</td>
      <td>258</td>
      <td>44.79</td>
    </tr>
    <tr>
      <td>25-29</td>
      <td>77</td>
      <td>13.37</td>
    </tr>
    <tr>
      <td>30-34</td>
      <td>52</td>
      <td>9.03</td>
    </tr>
    <tr>
      <td>35-39</td>
      <td>31</td>
      <td>5.38</td>
    </tr>
    <tr>
      <td>40+</td>
      <td>12</td>
      <td>2.08</td>
    </tr>
  </tbody>
</table>
</div>



## Purchasing Analysis (Age)

* Bin the purchase_data data frame by age


* Run basic calculations to obtain purchase count, avg. purchase price, avg. purchase total per person etc. in the table below


* Create a summary data frame to hold the results


* Optional: give the displayed data cleaner formatting


* Display the summary data frame


```python
# Count purchase data using SN by age bin
purchase_data_item = purchase_data.groupby('Age_Summary')['SN'].count()
#print(purchase_data_item)
average_purchase_price = purchase_data.groupby('Age_Summary')['Price'].mean()
#print(round(average_purchase_price,2))
total_purchase_value = purchase_data.groupby('Age_Summary')['Price'].sum()
#print(total_purchase_value)
avg_total_purchase_per_person = total_purchase_value/total_counts
#print(round(avg_total_purchase_per_person,2))

purchase_analysis_df = pd.DataFrame ({"Purchase Count": purchase_data_item,
                                  "Average Purchase Price ": round(average_purchase_price,2),
                                  "Total Purchase Value": total_purchase_value,
                                  "Avg Total Purchase per Person": round(avg_total_purchase_per_person,2),
                                  })
purchase_analysis_df
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
      <th>Avg Total Purchase per Person</th>
    </tr>
    <tr>
      <th>Age_Summary</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>&lt;10</td>
      <td>23</td>
      <td>3.35</td>
      <td>77.13</td>
      <td>4.54</td>
    </tr>
    <tr>
      <td>10-14</td>
      <td>28</td>
      <td>2.96</td>
      <td>82.78</td>
      <td>3.76</td>
    </tr>
    <tr>
      <td>15-19</td>
      <td>136</td>
      <td>3.04</td>
      <td>412.89</td>
      <td>3.86</td>
    </tr>
    <tr>
      <td>20-24</td>
      <td>365</td>
      <td>3.05</td>
      <td>1114.06</td>
      <td>4.32</td>
    </tr>
    <tr>
      <td>25-29</td>
      <td>101</td>
      <td>2.90</td>
      <td>293.00</td>
      <td>3.81</td>
    </tr>
    <tr>
      <td>30-34</td>
      <td>73</td>
      <td>2.93</td>
      <td>214.00</td>
      <td>4.12</td>
    </tr>
    <tr>
      <td>35-39</td>
      <td>41</td>
      <td>3.60</td>
      <td>147.67</td>
      <td>4.76</td>
    </tr>
    <tr>
      <td>40+</td>
      <td>13</td>
      <td>2.94</td>
      <td>38.24</td>
      <td>3.19</td>
    </tr>
  </tbody>
</table>
</div>



## Top Spenders

* Run basic calculations to obtain the results in the table below


* Create a summary data frame to hold the results


* Sort the total purchase value column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
top_spenders= purchase_data['SN'].value_counts()
#print(top_spenders)

average_purchase_price_spenders = purchase_data.groupby('SN')['Price'].mean()
#print(round(average_purchase_price_spenders,2))

total_purchase_value_spenders = purchase_data.groupby('SN')['Price'].sum()
#print(round(total_purchase_value_spenders,2))

# Cretaing DataFrame
spender_analysis_df = pd.DataFrame ({ "Purchase Count"         : top_spenders,
                                      "Average Purchase Price" : round(average_purchase_price_spenders,2),
                                      "Total Purchase Value"   : total_purchase_value_spenders,
                                  })
spender_analysis_df.sort_values('Purchase Count', ascending = False).head()

```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Purchase Count</th>
      <th>Average Purchase Price</th>
      <th>Total Purchase Value</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>Lisosia93</td>
      <td>5</td>
      <td>3.79</td>
      <td>18.96</td>
    </tr>
    <tr>
      <td>Iral74</td>
      <td>4</td>
      <td>3.40</td>
      <td>13.62</td>
    </tr>
    <tr>
      <td>Idastidru52</td>
      <td>4</td>
      <td>3.86</td>
      <td>15.45</td>
    </tr>
    <tr>
      <td>Asur53</td>
      <td>3</td>
      <td>2.48</td>
      <td>7.44</td>
    </tr>
    <tr>
      <td>Inguron55</td>
      <td>3</td>
      <td>3.70</td>
      <td>11.11</td>
    </tr>
  </tbody>
</table>
</div>



## Most Popular Items

* Retrieve the Item ID, Item Name, and Item Price columns


* Group by Item ID and Item Name. Perform calculations to obtain purchase count, item price, and total purchase value


* Create a summary data frame to hold the results


* Sort the purchase count column in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the summary data frame




```python
#Group by Item ID & Item Name than perform calculations

most_popular_items= purchase_data.groupby('Item ID')['Item Name'].value_counts()
#print(most_popular_items)

most_popular_items_price= purchase_data.groupby(['Item ID','Item Name'])['Price'].mean()
#print(most_popular_items_price)

most_popular_items_price_total= purchase_data.groupby(['Item ID','Item Name'])['Price'].sum()
#print(most_popular_items_price_total)

# Cretaing DataFrame

most_popular_items_df = pd.DataFrame ({ "Purchase Count"        : most_popular_items,
                                        "Item Price"            : most_popular_items_price,
                                        "Total Purchase Value"  : most_popular_items_price_total,
                                  })
most_popular_items_df.sort_values('Purchase Count', ascending = False).head()


```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>178</td>
      <td>Oathbreaker, Last Hope of the Breaking Storm</td>
      <td>12</td>
      <td>4.23</td>
      <td>50.76</td>
    </tr>
    <tr>
      <td>145</td>
      <td>Fiery Glass Crusader</td>
      <td>9</td>
      <td>4.58</td>
      <td>41.22</td>
    </tr>
    <tr>
      <td>108</td>
      <td>Extraction, Quickblade Of Trembling Hands</td>
      <td>9</td>
      <td>3.53</td>
      <td>31.77</td>
    </tr>
    <tr>
      <td>82</td>
      <td>Nirvana</td>
      <td>9</td>
      <td>4.90</td>
      <td>44.10</td>
    </tr>
    <tr>
      <td>19</td>
      <td>Pursuit, Cudgel of Necromancy</td>
      <td>8</td>
      <td>1.02</td>
      <td>8.16</td>
    </tr>
  </tbody>
</table>
</div>



## Most Profitable Items

* Sort the above table by total purchase value in descending order


* Optional: give the displayed data cleaner formatting


* Display a preview of the data frame




```python
# Above DataFrame in Ascending Order
most_popular_items_df.sort_values('Purchase Count', ascending = True).head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th></th>
      <th>Purchase Count</th>
      <th>Item Price</th>
      <th>Total Purchase Value</th>
    </tr>
    <tr>
      <th>Item ID</th>
      <th>Item Name</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>51</td>
      <td>Endbringer</td>
      <td>1</td>
      <td>4.66</td>
      <td>4.66</td>
    </tr>
    <tr>
      <td>27</td>
      <td>Riddle, Tribute of Ended Dreams</td>
      <td>1</td>
      <td>3.30</td>
      <td>3.30</td>
    </tr>
    <tr>
      <td>104</td>
      <td>Gladiator's Glaive</td>
      <td>1</td>
      <td>1.93</td>
      <td>1.93</td>
    </tr>
    <tr>
      <td>118</td>
      <td>Ghost Reaver, Longsword of Magic</td>
      <td>1</td>
      <td>2.17</td>
      <td>2.17</td>
    </tr>
    <tr>
      <td>42</td>
      <td>The Decapitator</td>
      <td>1</td>
      <td>1.75</td>
      <td>1.75</td>
    </tr>
  </tbody>
</table>
</div>


