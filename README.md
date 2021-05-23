# Self-Assessment
Over the past twenty-four weeks studying online part time and being able to learn a variety of different programs. As the weeks progressed the assignments did get harder. I was able to learn excel,python,javascript,SQl,tableau,R,Git Hub and machine learning. I would say I enjoyed Tableau and pandas the most and will probably be the most used in my field. I would say Java script was the hardest for me but then got hang of it.
# Team Assessment
Our team was about of five people and we were able to all come together and we did a great job at presenting our project. Our project was based on how covid affected the stock market. There was certain tech stock that flourished in the stock market. While their where other sectors that did not and really struggled to get by like the airline industry. We were all able to meet each week and practice even with everyone’s busy schedule. I really enjoyed working on a team.
Project
# Final_Project_Group5: An Analysis into the Tech Sector before and after Covid:
The uncertainty that COVID has brought to various industries around the world has seemingly overlooked or enriched certain sectors. Tech in particular has been able to flourish during pandemic,in part due to many business moving from office workplace to employees working from home; schools moving to remote learning and public transportation shifting to private rides and other forms of transportation. Our goal in our final project is to take a look at the impact covid has had on the Tech industry, and where we expect it to go moving forward.
Communication Protocals
Roles
Github: Collaborative
MI : Dan Marks
Dashboard : Perry Abdulkadir
Database : Wengi
Protocals
•	Colaboration through Slack group
•	Lay out 5 questions we will be answering, distributed questions
•	Meetings throughout the week outside of class
•	Shared Google doc: https://docs.google.com/document/d/1SY56LAwAWJcryRgtg58EKAuqdpSpt0IqHUjSmKUIQa4/edit
•	Zoom meetings
Questions:
Big Picture Question: How have American tech stocks performed during the Covid-19 pandemic?
ML Question: Do bluechip stocks have any advantage in forecasting stock prices compared to newer companies? (IPO after 2018)
Hypothesis: Blue chip companies will have safer more controlled growth whereas startups with have more volitality, higher risk but also higher gains in positive cases and losses in negative cases
The Rise of SPACs: During Covid, SPACs have become more popular. Since the vaccine released, which have been proven to be more successful (performing better in the market) -- IPOs or SPACs?
Hypothesis: SPACs (Special Purpose Acquisition Corporations) are essentially shell corporations that form with the intention of purchasing a private corporation. It is an alternate method of taking a corporation public with less red tape than an IPO. The SPAC has existed for several decades, but has gained a great deal of attention lately. Despite the buzz around SPACs, they have generated less return for investors than IPOs because this alternate method of going public signals to markets some underlying issue in the company’s fiscal health.
How did tech compnies manage during covid, some flourished, while others fell. Were different subsectors of tech hit differently?
Hypothesis: Tech stocks have surged during covid and helped the stock market rise. The pandemic has fueled the tech stocks while hurting other industries like the airline industry. With more people working from home and the need for cloud software helped the tech stock rise. While the airline industry was hurt because people were not traveling like they used to. The below charts show the upward trend of tech and downward of airline.
Is there a positive correlation between a companys ethical practices and profitability?
Hypothesis:
Source Data:
We will be pulling data from finance.yahoo.com, finance.google.com, Bloomberg and FactSet data sets
Companys we are looking into:
Our top 5 bluechip/recent ipo/SPAC companies were chosen because of two metrics: Tech sector and highest market cap as of 5/1/2021
 
Database Design
 
Analysis
Machine Learning:
The question we sought to answer with machine learning was comparing Bluechip stock to newly IPO'd stocks. I started experimenting with various ML methods but found most were not applicable to time series modeling. I ended up with ARIMA and ARMA as they are perfect at predicting future values in a given time series.
What is ARIMA?
'Auto Regressive Integrated Moving Average' or ARIMA for short can be used in analysis of time series models to better understand the data or predict future points based on its own past values. They are categorized with 3 terms: pdq An ARMA model (Autoregressive Moving Average) is very similar to an ARIMA model, but it without differencing your model.
p value:
p value is the order of the Auto Regressive (AR) term. This refers to the number of lags needed in the model to be used as predictors. We can find different p values to test by creating a partial autocorrelation plot (PACF)
 
By default 1 should be tested in your model, but we can also see 3 and 14 are above the standard deviation and should be considered as a p value.
d value:
d value is the number of differencing required to make the time series stationary we first perform an ADF test. If the p-value is >.05 we cannot reject the null hypothesis and will need to find the order of the differencing.
 
After we conclude the model is not stationary there are 2 methods in finding the number of differencin required:
 
First we can plot the auto correlation with different differencing number and see if the auto correlation drastically changes. Above, I tested with differencing of 1, 2 and 3 and concluded that differencing the model 1 time was enough. To double check my results I imported ndiffs module from pdarima.arima-utils package and concluded 1 difference was adequate for the model.
q value:
q value is the order of the Moving Average (MA) term. This explains the number of lagged forecast errors in our ARIMA model. We can chose our q values by creating an ACF plot:
 
From here we can see 1 and 3 should be tested as our q terms.
Moving on to modeling
Now that we have decided on our p d and q terms we must split our data into training and testing data.  
By splitting with this method we do not need to manually calulate 80% and 20% of our data and the code is more fluid for shorter or longer time series. Below we can see the data we are working on and visualize our train vs test data:
![](https://github.com/DanMarks12/Final_Project_Group5/blob/main/ML_tests/Github_JPGs/trainvstest.JPG}
The ARMA and ARIMA models I built came up with varying results. The majority of the time ARIMA seemed to better forecast stock prices where ARMA did have an advantage across a few stocks. Below are 2 example models:
   
After running the ARIMA and ARMA models I noticed an issue in comparing the results of the tests. Initially I believed mean squared average (MSE) score would be the best indication if the model was succesful or not, but since we are looking at 10 different stocks an MSE score would be more applicable to each individual stocks price (be it open, close, high, low). Because of this I decided to compare the stocks by their Mean Percent Error (MPE) scores. The MPE is the computed average by which forecasts of a model differ from actual values of the forecast. Below is the code run after each model illustrating the calculation used to find MPE scores
 
Exploring the results
 
As we can see here a distribution of the MPE scores for all stocks. We see blue chip stocks trend towards 0 (which indicates a more accurate forecast) across both ARIMA and ARMA models. If we look at the results plotted against the market cap we see similar results:
 
Here we can see market cap vs our MPE scores. We can also see for the most part the ARIMA model provided more accurate predictions than ARMA.
IPO vs SPACs
There are plenty of reasons why a company would want to go public, a couple being: liquidity and raise funds and open channels for higher revenues in the future. An IPO stands for “Initial Public Offering” and it involves a journey of working with investors, risk assessors, underwriters, etc. to invest money into the company so it can be taken public. A SPAC stands for “Special Purpose Acquisition Company” which is a shell company that saves its money until it figures out what it wants to spend its money on. SPACs have becoming popular in more recent times as it costs less time and money for companies to go public. However, a SPAC has a time limit of one to two years to acquire a target company before it delists off the market and is forced to give back all the investor money.
During Covid, SPACs have gained a lot of traction in terms of popularity. To best address my hypothesis that states IPOs are more profitable compared to SPACs, I have chosen five companies that have IPO’ed and five SPACs, specifically in the Technology sector. The IPO companies I have chosen are Zoom, Moderna, CrowdStrike, DocuSign and Peloton. The SPACs I have chosen are Reinvent Technology Partners, Mason Industrial Technology, E.Merge Technology Acquisition Corp, ScION Tech Growth, and TPG Pace Tech Opportunities Corp. Below, you will find the their growth since over time since the vaccine got released to the general public in early 2021.
 
IPOs
 
SPACs
In these graphs, we are comparing the Market Capitalization of these companies. Market Capitalization is the market value of a publicly traded company’s outstanding shares. Market cap is calculated by the share price multiplied by the number of shares outstanding. As you can see from both graphs, all ten companies have not had much growth in these past four months. However, the companies that IPO’ed have a higher Market Capitalization to begin with and have been quite steady throughout these months since the vaccine got released. SPACs have started with a lower Market Cap and have continued to stay in that low range. One of the SPACs even had a large fall in Market Cap in March. Although SPACs look to be profitable, IPOs have proven to be the safer and more profitable option in the long run.
How have different sub-sectors of the tech industry performed during the Covid-19 pandemic?
Hypothesis: certain sub-sectors of the tech industry have generated smaller returns to shareholders because of greater exposure to the economic risks associated with Covid-19. Semiconductor manufacturers suffered lower returns because of greater supply chain disruption. Meanwhile, social media companies have reaped the rewards of a world that is now fully reliant on the Internet for social interaction.
Have tech stocks with higher ESG scores generated higher returns during the Covid-19 pandemic?
Hypothesis: companies with better ESG scores (environmental, social, governance) have performed better during the Covid-19 pandemic. In a chaotic world, consumers are more likely to support charitable corporations. Furthermore, companies that have better accommodated employees during the pandemic by providing more sick leave, greater remote work opportunities, and bonuses have reaped the rewards of greater employee morale and productivity.
Data: The data for this analysis came from three sources. I used Pandas Data Reader to pull basic stock info (open, close, high, low, volume, adjusted close) from Yahoo Finance’s API. I used data from two of the main ESG rating agencies, MSCI and Morningstar’s Sustainalytics to get data on ESG scores. They are the only two major rating agencies that have their ESG rankings available for free. I decided to use both because they offer different advantages. The benefit of Sustainalytics is that it offers a simple number from 0 to 100 as its ESG rating, with 0 being the best and 100 being the worst. The benefit of Sustainalytics comes from the continuous nature of its rankings. However, MSCI’s ESG ratings offered advantages too. While its ratings are categorical, it provides historical ratings going back to 2017. This chronological information allowed me to see if, for example, an increase in ESG score corresponded with an uptick in stock price in a given year.
Scope of the analysis: Initially, I began my data exploration using just the five largest tech companies by market cap. However, it became apparent that I would need more data points to make stronger conclusions. So, I pulled stock data for all companies in the S&P500 that are either classified as “technology” or “communications services” by the index. It is important to note that in 2018, the S&P500 made an effort to “de-FAANG” its tech sector; because of the massive market caps of Facebook, Amazon, Apple, Netflix, Microsoft, and Alphabet, the tech sector of the index was massively overweight compared to other sectors. Those companies that focused more on social media, streaming, or digital content creation were spun off into “communication services,” while “technology” became the domain of companies specializing in hardware production. I included both sectors in my analysis of the tech sector, because in colloquial speech “tech” is synonymous with Facebook, Microsoft, Google, and Netflix, but all are considered “communication services” under the new classification. So, I pulled stock and ESG data for the 98 companies that met one of these criteria.
Data collection, cleaning, and preparation: Please note that for the sake of brevity I have omitted some of the more basic and mundane steps of data cleaning, such as renaming columns. Those intermediary steps can all be viewed in the accompanying notebook.
First, I created a .csv file (Tech and Comms Sustainability Scores 2.csv) with the ticker, Sustainalytics score, sector (tech or communication services), MSCI 2017 ESG rating, MSCI 2018 ESG rating, MSCI 2019 ESG rating, MSCI 2020 ESG rating, and MSCI 2021 ESG rating. I collected this data manually; there were few enough stocks and the websites were navigable enough that it would have taken more time to build a scraper.
Then, I built a for loop to collect the stock data for all tickers in my list using Yahoo Finance’s API for our period of analysis, 2019 to now:
tickers_list = tickers_df['Ticker'].tolist()
full_df = pd.DataFrame()
for item in tqdm(tickers_list):
    try:
        temp_df = web.DataReader(item, data_source='yahoo', start='2019-01-01', end='2021-04-28')
        temp_df.columns = [item + '_' + e for e in temp_df.columns.tolist()]
        full_df = pd.concat([full_df, temp_df], axis=1)
    except:
        continue
I then calculated the percentage returns for that time period using the for loop below and appended them as a new column to the data frame. Essentially, it loops through all the tickers and divides the closing price on April 28, 2021 by the closing price on January 1, 2019:
cols_to_keep = [e for e in full_df.columns.tolist() if 'Close' in e]
first = full_df[cols_to_keep].iloc[0,:]
last = full_df[cols_to_keep].iloc[584,:]
return_19_21_df = pd.DataFrame(last/first, columns = ['return']) 
return_19_21_df.index = [e.replace('_Close', '') for e in return_19_21_df.index.tolist()]
return_19_21_df.reset_index(inplace=True)
return_19_21_df
Next, I coded the MSCI ESG ratings to be integers rather than categorical variables. In my initial data exploration, I had dummified the ratings, that proved to be too cumbersome. Instead, I assigned numerical values to the classifications, with the worst (CCC) becoming 0 and the best (AAA) becoming 6. The code below converted the MSCI ratings to numbers:
dict  = {'CCC':0, 'B':1, 'BB':2, 'BBB':3, 'A':4, 'AA':5, 'AAA':6}
years = ['MSCI ESG 2017', 'MSCI ESG 2018', 'MSCI ESG 2019', 'MSCI ESG 2020', 'MSCI ESG 2021']
for y in years:
    tech_comms_df_final[y] = tech_comms_df_final[y].map(dict)
tech_comms_df_final
At this point, I had collected to core data I needed for my analysis. However, I wanted to further expand my analysis by calculating the returns of stocks for each year individually in 2017, 2018, 2019, 2020, and 2021. Because I had historical MSCI ESG ratings going back to 2017, I wanted to see if there was relationship between ESG scores and prices in a given year, i.e., would a drop in ESG score in 2019 correspond with a drop in stock price?
I will show my code for collecting the 2017 data as an example; I used the same method for all the other years, too.
First, I used a for loop and a similar method my method for collecting 2019-2021 data. It calculates return over the period by dividing the last day’s closing price by the first day’s closing price. It then puts the tickers and calculated returns in a new, temporary data frame:
#create for loop to pull stock data for 2017 and add as column
from tqdm import tqdm_notebook as tqdm
full_2017_df = pd.DataFrame()
for item in tqdm(tickers_list):
    try:
        temp_df = web.DataReader(item, data_source='yahoo', start='2017-01-01', end='2017-12-31')
        temp_df.columns = [item + '_' + e for e in temp_df.columns.tolist()]
        full_2017_df = pd.concat([full_2017_df, temp_df], axis=1)
    except:
        continue
Finally, this new data frame is merged with the master data frame.
returns_2017_final_df = tech_comms_df_final.merge(return_2017_df, left_on='Ticker', right_on='index')
Analysis
Using Matplotlib, I plotted the Sustainalytics ESG score on the X-axis of a scatter plot and returns on the Y.
tech_comms_df_final.plot.scatter(x = 'Sustainalytics Score', y = 'return')
 
Visually, there does not appear to be a relationship between Sustainalytics ESG score and returns.
I then made the same plot using the most recent ESG scores from MSCI in place of the Sustainalytics scores.
tech_comms_df_final.plot.scatter(x = 'MSCI ESG 2021', y = 'return')
 
Again, there appears to be no relationship. I confirmed this lack of relationship by calculating the correlation between returns over the time period studied and Sustainalytics score:
tech_comms_df_final['Sustainalytics Score'].corr(tech_comms_df_final['return'])
The R of 0.252 did not indicate a significant relationship.
There was also no relationship between returns and the latest MSCI scores:
tech_comms_df_final['MSCI ESG 2021'].corr(tech_comms_df_final['return'])

The R of -0.078 again indicated no relationship between the variables.
I then ran correlations for the MSCI ESG scores of each year against returns for that year. For example, I obtained the R for the relationship between MSCI scores in 2017 and the stock returns over the course of 2017. Here too, there was no significant relationship for any year.
corr_cols = [['MSCI ESG 2017', 'MSCI ESG 2018', 'MSCI ESG 2019', 'MSCI ESG 2020', 'MSCI ESG 2021'],
             ['2017 standard deviation', '2018 standard deviation', '2019 standard deviation', '2020 standard deviation', '2021 standard deviation']]
corr_cols = list(zip(*corr_cols))
for item in corr_cols:
print(item[0][-4:], 'correlation :', returns_2021_final_df[item[0]].corr(returns_2021_final_df[item[1]]))
Year	Correlation
2017	0.132
2018	0.040
2019	0.056
2020	0.234
2021	-0.004
None of these results indicate a meaningful relationship.
There are two primary factors to consider when investing: returns and risk (which is related, but not identical to volatility). They typically have an inverse relationship. Perhaps higher ESG scores do not drive higher returns but instead inspire confidence in company ownership and therefore result in lower volatility. Standard deviation is the most common proxy for volatility in the investing world. So, I calculated the standard deviation of each stock’s price over 2019-2021 using the code below:
cols_to_keep = [e for e in full_df.columns.tolist() if 'Close' in e]
std_2019_2021 = full_df[cols_to_keep].std()
std_2019_2021.index = [e.replace('_Close', '') for e in std_2019_2021.index.tolist()]
std_2019_2021
Creating a scatter plot using this data reveals that there is no relationship between standard deviation of Sustainalytics ESG scores and standard deviation of stock returns.
returns_2021_final_df.plot.scatter(x = 'Sustainalytics Score', y = '2019-2021 standard deviation')
 
There is also no relationship between MSCI score in 2021 and standard deviation of 2019-2021 returns.
 
Finally, there is no correlation between annual standard deviation and annual MSCI scores.
corr_cols = [['MSCI ESG 2017', 'MSCI ESG 2018', 'MSCI ESG 2019', 'MSCI ESG 2020', 'MSCI ESG 2021'],
             ['2017 standard deviation', '2018 standard deviation', '2019 standard deviation', '2020 standard deviation', '2021 standard deviation']]
corr_cols = list(zip(*corr_cols))
for item in corr_cols:
    print(item[0][-4:], 'correlation :', returns_2021_final_df[item[0]].corr(returns_2021_final_df[item[1]]))
Conclusion
There is yet to be an academic consensus on how ESG factors into a stock’s pricing. Over the past few years, the conventional thinking was high ESG scores at the very least led to lower risk (volatility), if not higher returns. (See, for example, Umeå School of Business, Economics, and Statistics, Jakobsson, R., & Lundberg, L. (2018). The Effect of ESG Performance on Share Price Volatility.))
However, more recent analysis has challenged this notion that ESG positively impacts investment performance. Writing in the journal Sustainability in 2020, authors from the University of Rome found no relationship between volatility or returns and ESG (La Torre M, Mango F, Cafaro A, Leo S. Does the ESG Index Affect Stock Return? Evidence from the Eurostoxx50. Sustainability. 2020; 12(16):6387.).
This analysis fits in with more recent analysis showing that ESG does not significantly impact investment performance. Of course, this analysis was limited to US tech stocks in the past few years. Further analysis needs to be done to see if this pattern holds in other contexts. The upshot for investors is this: if you are looking for reduced volatility or greater returns after the market jitters caused by Covid, don’t necessarily look to tech stocks with high ESG. High ESG tech stocks are just as likely as low ESG tech stocks to have low volatility and high returns. That being said, there is still of course moral value in ESG investing, even if that does not allow you to have your cake and eat it too.
Presentation
https://docs.google.com/presentation/d/1lW8-Si68omeYsMeeIKVGWdINQx402azv0Sgm5ooQO6I/edit?usp=sharing
   



