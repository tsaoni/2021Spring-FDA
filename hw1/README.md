# 資料分析與學習基石 作業一

###### F74072277 許郁翎

## Dataset Description

### 使用的資料集

Telecom users dataset
link: https://www.kaggle.com/radmirzosimov/telecom-users-dataset

#### 資料集提供的特徵(features):

##### Numerical Features

* tenure - how many months a person has been a client of the company
* MonthlyCharges - current monthly payment
* TotalCharges - the total amount that the client has paid for the services for the entire time


##### Categorical Features

* customerID - customer id
* gender - client gender (male / female)
* SeniorCitizen - whether the client is a pensioner (1, 0)
* Partner - whether the client is married (Yes, No)
* Dependents - does the client have dependents (Yes, No)
* PhoneService - is the telephone service activated (Yes, No)
* MultipleLines - whether multiple telephone lines are connected (Yes, No, No phone service)
* InternetService - client's Internet provider (DSL, Fiber optic, No)
* OnlineSecurity - is the online security service enabled (Yes, No, No internet service)
* OnlineBackup - is the online backup service activated (Yes, No, No internet service)
* DeviceProtection - does the client have equipment insurance (Yes, No, No internet service)
* TechSupport - is the technical support service activated (Yes, No, No internet service)
* StreamingTV - is the streaming TV service activated (Yes, No, No internet service)
* StreamingMovies - is the streaming cinema service activated (Yes, No, No internet service)
* Contract - type of customer contract (Month-to-month, One year, Two year)
* PaperlessBilling - whether the client uses paperless billing (Yes, No)
* PaymentMethod - payment method (Electronic check, Mailed check, Bank transfer (automatic), Credit card (automatic))

#### 要預測的目標(target):

* Churn - whether there was a churn (Yes or No)

#### 數值資料分析

![](https://i.imgur.com/9viQBHh.png)

##### 資料分布長條圖

![](https://i.imgur.com/AXqrWAy.png)
![](https://i.imgur.com/6OrwozK.png)
![](https://i.imgur.com/YAhwbyV.png)

##### 資料之間的相關係數分布圖

![](https://i.imgur.com/FXj9R43.png)


#### 分類資料分析

![](https://i.imgur.com/ZDGkSh9.png)
![](https://i.imgur.com/YsOwT22.png)
![](https://i.imgur.com/KCOez63.png)

由上面資料，我們可以得出初步觀察:

* 客戶的性別比沒有太大差距(男性約略高出女性50人)，且大多客戶並無待扶養親屬。
* 約90%的客戶皆有使用電話服務(telephone service)，大約一半的客戶沒有使用額外服務(additional services)。
* 大約一半的客戶的合約都是按月份(From month to month)來簽。
* 超過一半的客戶是用無紙付費(paperless billing)。
* 大約1/3的客戶使用電子支付(Electronic check)。




## Code Analysis

以下的程式都是用ensemble的方法，集合一群model去預測target。

### 分析程式1

EDA and Building models for predicting outflow
link: https://www.kaggle.com/radmirzosimov/eda-and-building-models-for-predicting-outflow

#### 使用XGBClassifier分類器


初使化XGBClassifier並且把training data丟進去訓練
![](https://i.imgur.com/eOU1Ydp.png)

訓練結果在testing set上的準確率
![](https://i.imgur.com/zb4Fze4.png)

classification report
![](https://i.imgur.com/knkFCUP.png)

#### 使用stacking的技術，結合多個分類器預測

![](https://i.imgur.com/PZxk4tS.png)


分別初使化GradientBoostingClassifier，RandomForestClassifier，AdaBoostClassifier跟SVC
以及切割訓練跟測試資料
![](https://i.imgur.com/giganQP.png)

把最佳參數分別丟入model個別訓練
![](https://i.imgur.com/G15tn0E.png)

把XGBClassifier當作final classifier
![](https://i.imgur.com/wcyboON.png)

訓練結果在testing set上的準確率
![](https://i.imgur.com/w2jdcYW.png)

~~不知道為什麼準確率從0.7938230383973289掉到0.7796327212020033

classification report
![Uploading file..._tox5hcwfe]()
![Uploading file..._tox5hcwfe]()



### 分析程式2

Telecom Customer Churn
link: https://www.kaggle.com/docxian/telecom-customer-churn

#### 用random forest集合多個decision tree當classifier

把所有的features集合起來
![](https://i.imgur.com/Bfl8GFA.png)

初使化RandomForestEstimator，把用來做cross validation的訓練資料切割成n_CV等份
![](https://i.imgur.com/KavTkWD.png)

RandomForestEstimator在training data上的performance
![](https://i.imgur.com/2t5sH74.png)

把estimator預測的顧客流失數量跟實際顧客流失數做比較
![](https://i.imgur.com/hiYBhIN.png)

estimator預測出每個feature影響力大小
![](https://i.imgur.com/wiDJhAS.png)

estimator在testing set的performance
![](https://i.imgur.com/WGGXtE2.png)

#### Gradient Boosting

初始化Gradient Boosting Estimator
![](https://i.imgur.com/9WfqA13.png)

把estimator預測的顧客流失數量跟實際顧客流失數做比較
![](https://i.imgur.com/HPsAa64.png)

estimator在training data上的performance
![](https://i.imgur.com/yBBqRzs.png)

estimator預測出每個feature影響力大小
![](https://i.imgur.com/fy2Wdvo.png)

estimator在testing set的performance
![](https://i.imgur.com/boxLV5p.png)

在testing set上預測單一顧客流失的機率的程式碼
![](https://i.imgur.com/oMv4gkN.png)


