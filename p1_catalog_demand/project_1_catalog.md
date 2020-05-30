## Business and Data Understanding

##### What decisions need to be made?

公司想依据现有的数据，预测一下如果给250位顾客派发新的产品册能否带来一定收入，从而决定是否进行派发。

Based on the existing data, the company would like to predict whether the distribution of new product catalog to 250 customers will bring certain profits, so as to decide whether to distribute them.

##### What data is needed to inform those decisions?

* 已有的顾客数据，来建立预测模型
* 通过线性回归模型，预测这250个顾客的可能花费，求出总和即可
* Existing customer data, to establish a prediction model
* Through the linear regression model, we can predict the possible costs of these 250 customers and calculate the sum

## Analysis, Modeling, and Validation

![image-20200530110716916](/Users/linchen/Desktop/读书笔记/image-20200530110716916.png)

##### How and why did you select the predictor variables in your model?

![image-20200530110853951](/Users/linchen/Desktop/读书笔记/image-20200530110853951.png)

The general content of the dataset used for training is shown in the figure above. Useless information can be ignored first, like *Name*,*ID*,*ZIP*,etc.

Because *Avg_sale_amount* is our forecast variable, we can explore the relationship between characteristic parameters that may be relevant.

<img src="/Users/linchen/Desktop/读书笔记/image-20200530112738374.png" alt="image-20200530112738374" style="zoom:33%;" />

<img src="/Users/linchen/Desktop/读书笔记/image-20200530112821576.png" alt="image-20200530112821576" style="zoom:33%;" />

<img src="/Users/linchen/Desktop/读书笔记/image-20200530112842900.png" alt="image-20200530112842900" style="zoom:33%;" />

From the scatter diagram of the above three possible variables and *Avg_sales_amount*, it's obvious that *Avg_num_products_purchased* has strong linear relationship with *Avg_sales_amount*,and different *Customer_segment* have different *Avg_sales_amount*. While *Years_as_customer*‘s influence on *Avg_sales_amount* is not clear.(In fact, when using it as a parameter of linear regression, the corresponding p-value is relatively large)

##### Explain why you believe your linear model is a good model.

 ![image-20200530115505223](/Users/linchen/Desktop/读书笔记/image-20200530115505223.png)

Report for this linear model is shown in figure above. For two variables we select, their p-value is far less than 0.05 which means their relationship with *Avg_sales_amount* is strong. R-squared and adjusted R-squared are also good enough which indicating the linear model we bulit is reliable.

**Linear equation:**

*Avg_sales_amount=303.46-149.36(Customer_SegmentLoyalty Club Only)+281.34(Customer_SegmentLoyalty Club and Credit Card)-245.42(Customer_SegmentStore Mailing List)+66.98·Avg_Num_Products_Purchased*

#### Conclusion

##### What is your recommendation? Should the company send the catalog to these 250 customers?

affirmative. The final calculated profit is **$22050**. The company is interested in it when  projected profits is above $20000.

