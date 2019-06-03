# Financial-Machine-Learning: Predicting stock market returns

In this section,I  investigate the possibility of predicting future price movements (next two days: t + 2) relative to an individual company belonging to the SPY500 index. The prediction will be attempted based on past price and volume dynamics that you will try to summarize using four families of technical analytics.

## 3.1 Data Preparation

### 3.1.1 Data sourcing

Download the following time series of economic macro indicators:
1. US Market volatility (VIX) • https://fred.stlouisfed.org/series/VIXCLS 
2. US Inﬂation (CPI) • https://fred.stlouisfed.org/series/CPIAUCSL
3. US Investment grade corporate bonds spread (IGS) • https://fred.stlouisfed.org/series/BAMLC0A0CM 
4. US high yield corporate bonds spread (HYS) • https://fred.stlouisfed.org/series/BAMLH0A0HYM2 
5. US 3-months treasury bill rate (UST3)• https://fred.stlouisfed.org/series/TB3MS 
6. Crude oil price (O) • https://fred.stlouisfed.org/series/DCOILWTICO 
7. US M1 money (M1) • https://fred.stlouisfed.org/series/M1 
8. Term spread (TS) https://fred.stlouisfed.org/series/T10Y2Y

Use Yahoo ﬁnance to download the time series of prices and volume of the following sector exchange trade funds (ETFs):
1. Technology (XLK)
2. Financials (XLF)
3. Healthcare (XLV)
4. Consumer Cyclicals (XLY)
5. Industrials (XLI)
6. Consumer Non-Cyclicals (XLP)
7. Energy (XLE)
8. Utilities(XLU)
9. Telecommunications Services (XTL)
10. Basic Materials (XLB)
Download SPY from the same source.

### 3.1.2 Feature extraction

1. Compute the one month changes of M1 and CPI
2. Compute the 90 days realized volatility of SPY
3. For each sector ETF, compute the daily returns
Rn = 10000×log
Pt Pt−n 4. Construct a panel data set for each sector D = {Xi,Yi}i=N i=1 where Yi is the next day ETF return, and Xi is the feature vector of : • VIX• IGS • HYS • TS • CPI one month change • O • UST3 • M1 one month change • SPY realized volatility minus VIX 
5. In all datasets, include data from January 2000 forward.
6. The aim is to attempt predicting the next day return of each sector ETF for the economic factor indicators. I have to ﬁt 10 separate models.

## 3.2 Data Analysis 

• For each ETF sector and its corresponding panel data set: 
1. Find the descriptive statistics of the dependent and independent variables. 2. Plot their histogram. 3. Plot the log-scale histogram 4. Show the scatter-plot between the the independent variables and the dependent variable Y (Y in the y-axis). 5. Does the previous scatter plots exhibit any visual patterns ? 6. The k-Binned scatter plot between two paired variables X and Y consists of sorting X and discretizing (binning) it into k equal frequency bins, then computing the averages of X and Y in each bin and plotting the k Y averages as a function of the k X averages. Plot the 10-binned scatter plot between each independent variable and the target variable (Y in the y-axis). Do you see any patterns ? . 7. Compute the linear correlation between each independent variable and the target variable. Check the statistical signiﬁcance of the computed correlations ? 8. The mutual information between two discrete random variables X and Y (for simplicity we assume that they have the same number of values N ) is deﬁned as: I(X,Y ) =X i,j p(X = i,Y = j)log P(X = i,Y = j) P(X = i)P(Y = j) . To compute the mutual information between two continuous variables you need to discretize both variables (equal frequency discretization). Use equal frequency into 20 bins and compute the mutual information between each independent variable and the target variable. Consider using qcut and crosstab from pandas. 9. Plot the mutual information against the linear correlation (one point for each variable). Does the mutual information agree with the linear correlation ?

## 3.3 A linear model 

• For each ETF sector and its corresponding panel data set: 
1. Fit a linear model to the data to predict Y . Use statsmodels 2. What are the assumptions of the linear model? 3. Check if they are violated by the model you have just learned. 4. Split the data into training data and testing data. Build a linear model using the training data and test it on the testing data. 5. Compute the 20-Binned scatter plot between Y and ˆ Y for both training and testing (ˆ Y on the x-axis). 6. How does the R-squared compare between the training and testing subsets? 

## 3.4 Long/short strategy 

• Train the 10 models over the period 2000-2009 • Starting from January 2010, and every day, use each model to predict the next day return of the corresponding ETF. • After obtaining prediction returns for US sectors, rank the sectors by expected return , and go long (buy ) top 3 and short (sell) bottom 3 sectors. • Compute the daily returns of your invested portfolio of ETFs/sectors. Your portfolio is being rebalanced (new sectors are selected based on the prediction ) every day. • Compute the cumulative return of your portfolio at the end of your testing/investment window.

• Compute the Sharpe ratio of your strategy: rp −rf σp

where
– rp: the mean of your portfolio daily returns – σp : the standard deviation your portfolio daily returns – rf: the risk-free return. You can use the annualized one month US T-bill rate (divide by 250) ∗ https://fred.stlouisfed.org/series/DGS1MO 
• What is the CAPM alpha and beta of your portfolio ? CAPM alpha and beta can be found by ﬁtting the following regression rp −rf = α + β(rm −rf)  where rm is the market return (you can use SPY returns that you have already downloaded and used for the realized volatility).
