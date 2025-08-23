# Project: Using time series analysis for sales and demand forecasting


## **Business context**

The Nielsen BookScan service is the world’s largest continuous book sales tracking service in the world, operating in the UK, Ireland, Australia, New Zealand, India, South Africa, Italy, Spain, Mexico, Brazil, Poland, and Colombia. Nielsen BookScan collects transactional data at the point of sale, directly from tills and dispatch systems of all major book retailers. This ensures detailed and highly accurate sales information on which books are selling and at what price, giving clients the most up-to-date and relevant data. The Nielsen BookScan Total Consumer Market (TCM) data covers approximately 90% of all retail print book purchases in the UK. The remaining sites are specialised, such as gift shops, specialist booksellers, and tourist information centres.


Nielsen BookScan can be used to:
- Monitor titles and authors against the competition and overall market.
- Analyse pricing and discounting by format or category.
- Gauge the success of marketing campaigns and promotions.
- See which categories are growing and declining.
- Learn what works in your market and how that might differ from other countries.

Nielsen BookScan sales data can be analysed by various criteria, including category, publisher, and format, allowing users to see which genres are selling in which format. Users can track market trends to see which titles are driving the results, and patterns can easily be interpreted. In addition, the actual selling price is included. This inclusion makes it easier to identify trends for the level of discounting (e.g. by title, author, genre, format, region, and publisher) when analysing book sales.

**Project context**

Nielsen is seeking to invest in developing a new service aimed at small to medium-sized independent publishers. This service is aimed at supporting publishers in using historical sales data to make data-driven decisions about their future investment in new publications. Their publisher customers are interested in being able to make more accurate predictions of the overall sales profile post-publication for better stock control and initial investment, but they are also interested in understanding the useful economic life span that a title may have.

Nielsen is targeting small to medium-sized independent publishers as their research has shown that there is a strong demand for this insight, but businesses cannot invest in this infrastructure and would pay a premium to have access to quality-assured data and analysis in this area. Producing a new publication requires a significant upfront investment, and they would like to be able to more accurately identify books with strong long-term potential. More specifically, they are looking for titles with sales patterns that exhibit well-established seasonal patterns and positive trends that show potential great returns and to learn more about these types of publications. Nielsen will then apply this understanding to their commission and print volume strategy to be more successful in acquiring titles that have longevity. Additionally, this will enable them to deliver better returns by ensuring the correct stock levels in relation to demand and avoiding over- or understocking, which can be costly.

You will notice that some titles experience fluctuations in sales due to various factors, such as increased media attention or cultural relevance (e.g. the recent resurgence of interest in George Orwell’s 1984). However, certain books endure over time and are often studied in academic settings for their deeper significance.

For this project, Nielsen has provided you with two data sets. The objective is to identify sales patterns that demonstrate seasonal trends or any other traits, providing insights to inform reordering, restocking, and reprinting decisions for various books (by their International Standard Book Number, or ISBN).

## **Problem Statement**

Neilson BookScan is a leading book sales tracking service that collects highly accurate point-of sale data from major UK book retailers, covering nearly 90% of the market. To support small to  medium sized publishers, Nielsen aims to develop a forecasting tool that predicts a book’s sales  profile after publication. This would enable publishers manage upfront investment risks by identifying titles with strong long-term and seasonal demand.

## **Data Set Cleaning**

Nielson provided us with two .xlsx files of real-world data from Nielsen. The first file is an ISBN list that contains industry-standard metadata about each book, and the other is a UK weekly trended timeline that contains weekly sales data.  
1. ISBN List File: 
2. UK weekly trended timeline Dataset:

The main dataset used was the UK weekly trended timeline, which provided book sales volume 
data by ISBN across four product categories. These were combined into a single Data Frame and 
resampled the data to weekly frequency using the end date of each reporting period for 
consistency. Missing weekly data was filled using linear imputation. Negative sales volumes, which are considered invalid, were replaced with NaN values and imputing them using the same 
approach. After investigating all the ISBN’s timeseries plots, it was decided to conduct further analysis on the Volume of Sales of two books, ‘The Alchemist and ‘The Very Hungry Caterpillar’. The dataset for both books were filtered to only contain data from 01-01-2012 up to the latest week sales were made

## **Results & Conclusion**

**Decomposition:**  
STL was selected as the ideal model to utilise to understand the structure of the time series as it is robust against outliers and can help identify sales spikes. We utilised period of 52 weeks to decompose our data as our timeseries plots for the two books showed seasonality. Reviewing the time series plots for the volume of sales of the two books, it can be assumed that both are multiplicative, showing the amplitude of the peaks increasing or decreasing in the dataset at times. However, when transformation was performed. The transformation flattened the trend, dampened the seasonal variation to near zero and so it was assumed to be additive. The Alchemists Volume of sales data showed a strong seasonality strength of 0.79, and a has a trend of 0.51. The Hungry Caterpillars Volume of sales data similarly showed moderately high seasonality of 0.67 and a strong trend strength of 0.78.

**Auto-Correlation (ACF) of the Datasets:**
The Alchemist’s Volume of Sales, shows positive autocorrelation with a sharp decay in 
autocorrelation after the first lag. Only the first lag is significant and influences the current volume of sales. The Very Hungry Caterpillar volume sales show’s decay after the first lag although decays slower than The Alchemist. Only the first lag is statistically significant to the current revenue. Both books show a high spike at week 52 indicating an annual seasonality for both books. Only the week before volume of sales influences current volume of sales. Please see the notebook.

**Partial-Autocorrelation (PACF) of the Datasets:**
The PACF Plots for both books are similar, they show a strong positive correlation for the first two lags, however after that the PACF shows no Correlation. There is a spike after week 52 which indicates annual seasonality. Please see the notebook

** Stationarity ADF test for the Two Book Datasets: **
The Alchemist shows a p value (1.36x10-17) which is less than 0.05. As a result, we reject the null hypothesis and assume the volume of sales feature is stationary. However, the p value (0.18) for The Very Hungry Caterpillar is greater than 0.05 thus, we fail to reject the null hypothesis and assume the volume sales feature is non-stationary based on the ad fuller stationarity test. 

##
