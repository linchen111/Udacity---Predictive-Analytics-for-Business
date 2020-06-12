## Business and Data Understanding

##### What decisions need to be made?

 Perform an analysis to recommend the city for Pawdacity’s newest store

##### What data is needed to inform those decisions?

We need to predict the yearly sales for each city, and it can be calculated from Past Sales Data, Demographic Data of the cities, Population data, and the sales of competitor stores.

## Analysis, Modeling, and Validation

##### Building the Training Set

###### Data cleaning

![image-20200611224514899](/Users/linchen/Desktop/Project/project_2_petstore/clean_workflow.png)

For Pawdacity sales, transpose tool is used to get *month* and *amount* field, then summarize by *city*.

For demographic data, select tool is used to pick fields we need.

For population data, *text_to_column*, *left* , *replace* and *replacechar*  function are used for data cleaning.

Then I use *joint_multiple* to join above three files, then save the data as *clean_ data.csv*.

For work check:

|          Column          |   Sum   |
| :----------------------: | :-----: |
|    Census Population     | 213862  |
|  Total Pawdacity Sales   | 3773304 |
| Households with Under 18 |  34064  |
|        Land Area         |  33071  |
|    Population Density    |  62.8   |
|      Total Families      |  62653  |

###### Dealing with outliers

![deal_with_outliers](/Users/linchen/Desktop/Project/project_2_petstore/deal_with_outliers.png)

*QUARTILE* in Excel is used to identify outliers with IQR, numbers higher than the upper limit are highlighted in the table.

```python
## We can also do it in python
# calculate quartile
first_quartile = data['field'].describe()['25%']
third_quartile = data['field'].describe()['75%']

# calculate IQR
iqr = third_quartile -first_quartile

# remove ouliters(if you are certain)
data = data [(data['field']>(first_quartile - 3*iqr)) & (data['field']<(third_quartile + 3*iqr))]
```

City Cheyenne has 4 outliers in families, population and sale amounts, but I choose to keep it considering Cheyenne is center city with lots of people, high sales makes sense. 

<div align="center" >
<img src="/Users/linchen/Desktop/Project/project_2_petstore/Cheyenne_1.png" style="width: 30%;display: inline;"/>
<img src="/Users/linchen/Desktop/Project/project_2_petstore/Cheyenne_2.png" style="width: 30%;display: inline;" />
<img src="/Users/linchen/Desktop/Project/project_2_petstore/Cheyenne_3.png" style="width: 30%;display: inline;" />
</div>

The above three figures show that the points of city Cheyenne are in line with the overall linear relationship.

<img src="/Users/linchen/Desktop/Project/project_2_petstore/RockSprings.png" alt="RockSprings" style="zoom:25%;" />

Similarly, land area of Rock Springs also makes sense in *land_area-sales* relationship(shown in above figure).

Finally, Gillete's data is deleted considering its other fields are at their average while sales is abnormally high.

##### How and why did you select the predictor variables in your model?

![image-20200612104329258](/Users/linchen/Desktop/Project/project_2_petstore/image-20200612104329258.png)

Correlation is used to see if there is any possibility ofmulticollinearity in dataset.

![Correlation_matrix](/Users/linchen/Desktop/Project/project_2_petstore/Correlation_matrix.png)

So *Census*, *Families*,*Households with under 18* and *Population density* have strongcorrelations which each other, while *Land area* is not. 

*Land area* and *Total families* are selected to bulid the final model.

`Sales=197330.41-48.42*land.area+49.14*total.families`

##### Explain why you believe your linear model is a good model.

![image-20200612105823320](/Users/linchen/Desktop/Project/project_2_petstore/image-20200612105823320.png)

The p-values for *land area* and *total families* are both below 0.05 and the  R-squared value is close to 1.

## Conclusion

##### What is your recommendation? 

When it comes to choose new city to open a store.

1. The new store should be located in a new city. That means there should be no existing stores in the new city.
2. The total sales for the entire competition in the new city should be less than $500,000
3. The new city where you want to build your new store must have a  population over 4,000 people (based upon the 2014 US Census estimate).
4. The predicted yearly sales must be over $200,000.
5. The city chosen has the highest predicted sales from the predicted set.

So four cities is selected:

| City    | 2014 Estimate | Population VOLUME  SALES | Land Area |
| ------- | ------------- | ------------------------ | --------- |
| Jackson | 10,449        | 110000                   | 1757      |
| Lander  | 7,642         | 108197                   | 3346      |
| Laramie | 32,081        | 76000                    | 2513      |
| Worland | 5,366         | 100000                   | 1294      |

Then linear model is used to to predict total sales.

| City        | 2014 Estimate | Population VOLUME  SALES | Land Area | Total Family | Predict Sales |
| ----------- | ------------- | ------------------------ | --------- | ------------ | ------------- |
| Jackson     | 10,449        | 110000                   | 1757      | 2313         | 225917.29     |
| Lander      | 7,642         | 108197                   | 3346      | 3876         | 225783.73     |
| ==Laramie== | 32,081        | 76000                    | 2513      | 4668         | 301036.47     |
| Worland     | 5,366         | 100000                   | 1294      | 1364         | 197701.89     |

So I would recommend the city of Laramie 

## Appendix 

Difference between QUARTILE.EXC and QUARTILE.INC in Excel.

https://zhuanlan.zhihu.com/p/79461597

By 知乎专栏：小数据

