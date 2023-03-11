# Association-Rules
I will use the Apriori algorithm to combine items in a supermarket and determine which products have the most influence on each other.

# Data cleaning
Data has missing data and I will drop it.

![image](https://user-images.githubusercontent.com/110837675/224461250-261adeaa-60cd-4579-944f-11bb58a75689.png)

I will use the 'dropna' function to delete missing data. Since there are too many missing data, I am unable to determine which data is missing in which products. In fact, if such a situation arises, I will investigate further to determine it more clearly. Delete data won't ensure data integrity.

```php
data= data.dropna()
```
I will create product list.
```php
records =[]
for i in range (0, len(data)):
    row=[]
    for j in range (0, data.shape[1]):
        if data.values[i,j] != 0:
            row.append(str(data.values[i,j]))
    records.append(row)
```
Explain this code :
1.records =[] initializes an empty list called records.

2.for i in range(0, len(data)): loops through each row in data.

3.row=[] initializes an empty list called row for each row in data.

4.for j in range(0, data.shape[1]): loops through each column in the current row of data.

5.if data.values[i,j] != 0: checks if the value in the current cell of data is not equal to 0.

6.row.append(str(data.values[i,j])) if the value is not 0, it converts the value to a string and appends it to the row list.

7.records.append(row) appends the row list to the records list after all columns in the current row have been processed.

```php
te = TransactionEncoder()
te_ary = te.fit(records).transform(records)
df = pd.DataFrame(te_ary,columns=te.columns_)
```
This code snippet uses the TransactionEncoder object from the mlxtend library to transform a list of lists of data into a binary matrix. The matrix is then converted into a pandas DataFrame object for easy data processing and analysis.

# Build Model.
```
frequent_itemsets = apriori(df, min_support=0.001,use_colnames=True)
print(frequent_itemsets)
from mlxtend.frequent_patterns import association_rules
association_rules(frequent_itemsets,metric='confidence',min_threshold=0.001)
```
![image](https://user-images.githubusercontent.com/110837675/224461898-18caf51d-54f5-4566-bc2f-c41810dd2575.png)

- antecedents	: The product bought previously

- consequents : The product bought after.

- antecedent support : Antecedent support is the probability (or frequency) of occurrence of the previous item set (antecedent) in transactions containing this element set. It is calculated as the number of transactions that contain the previous element set divided by the total number of transactions. Antecedent support is used to measure the frequency of occurrence of the previous set of elements in the data set.

- consequent support : Consequent support is the probability (or frequency) of occurrence of the following itemsets (consequent) in transactions containing this element set. It is calculated as the number of transactions that contain the following set of elements divided by the total number of transactions. Consequent support is used to measure the frequency of occurrence of the following set of elements in the data set.

- support : The percentage of occurrences of a set of supports in the total number of transactions. (example : there are 2 itemsets A and B, support A,B= Total number of transactions contained and B/ Total number of transactions)

- confidence : measure the effect of action A on action B.

- lift : Lift is used to measure dependencies between support sets. High Lift indicates a strong relationship between the support sets. A lift of 1 indicates that the support sets are independent of each other, while a lift greater than 1 indicates a positive dependency between the support sets, and a lift less than 1 indicates a negative dependency between the support sets.

- conviction : emphasize dependon A in B (The higher, the greater the dependence)

- leverage : Leverage calculates the distance between the observed frequencies of itemsets and their expected frequencies if they are independent. A leverage of 0 indicates that the itemsets are independent, a leverage greater than 0 indicates that itemsets tend to occur together (positive correlation), and leverage less than 0 indicates that itemsets tend to appear opposite. each other (negative correlation).





















