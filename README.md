# finalassignmnet1
1st final assignment of Python project for data science
{
 "cells": [
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<center>\n",
    "    <img src=\"https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/labs/project/Images/SN_logo.png\" width=\"300\" alt=\"cognitiveclass.ai logo\">\n",
    "</center>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h1>Extracting Stock Data Using a Python Library</h1>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "A company's stock share is a piece of the company more precisely:\n",
    "<p><b>A stock (also known as equity) is a security that represents the ownership of a fraction of a corporation. This\n",
    "entitles the owner of the stock to a proportion of the corporation's assets and profits equal to how much stock they own. Units of stock are called \"shares.\" [1]</p></b>\n",
    "\n",
    "An investor can buy a stock and sell it later. If the stock price increases, the investor profits, If it decreases,the investor with incur a loss.  Determining the stock price is complex; it depends on the number of outstanding shares, the size of the company's future profits, and much more. People trade stocks throughout the day the stock ticker is a report of the price of a certain stock, updated continuously throughout the trading session by the various stock market exchanges. \n",
    "<p>You are a data scientist working for a hedge fund; it's your job to determine any suspicious stock activity. In this lab you will extract stock data using a Python library. We will use the <coode>yfinance</code> library, it allows us to extract data for stocks returning data in a pandas dataframe. You will use the lab to extract.</p>\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<h2>Table of Contents</h2>\n",
    "<div class=\"alert alert-block alert-info\" style=\"margin-top: 20px\">\n",
    "    <ul>\n",
    "        <li>Using yfinance to Extract Stock Info</li>\n",
    "        <li>Using yfinance to Extract Historical Share Price Data</li>\n",
    "        <li>Using yfinance to Extract Historical Dividends Data</li>\n",
    "        <li>Exercise</li>\n",
    "    </ul>\n",
    "<p>\n",
    "    Estimated Time Needed: <strong>30 min</strong></p>\n",
    "</div>\n",
    "\n",
    "<hr>\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 1,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "Collecting yfinance==0.2.4\n",
      "  Downloading yfinance-0.2.4-py2.py3-none-any.whl (51 kB)\n",
      "\u001b[2K     \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m51.4/51.4 kB\u001b[0m \u001b[31m6.0 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
      "\u001b[?25hRequirement already satisfied: cryptography>=3.3.2 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from yfinance==0.2.4) (38.0.2)\n",
      "Requirement already satisfied: pytz>=2022.5 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from yfinance==0.2.4) (2022.6)\n",
      "Collecting appdirs>=1.4.4\n",
      "  Downloading appdirs-1.4.4-py2.py3-none-any.whl (9.6 kB)\n",
      "Requirement already satisfied: html5lib>=1.1 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from yfinance==0.2.4) (1.1)\n",
      "Collecting frozendict>=2.3.4\n",
      "  Downloading frozendict-2.3.5-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (99 kB)\n",
      "\u001b[2K     \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m99.8/99.8 kB\u001b[0m \u001b[31m7.9 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
      "\u001b[?25hCollecting multitasking>=0.0.7\n",
      "  Downloading multitasking-0.0.11-py3-none-any.whl (8.5 kB)\n",
      "Collecting lxml>=4.9.1\n",
      "  Downloading lxml-4.9.2-cp37-cp37m-manylinux_2_17_x86_64.manylinux2014_x86_64.manylinux_2_24_x86_64.whl (6.6 MB)\n",
      "\u001b[2K     \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m6.6/6.6 MB\u001b[0m \u001b[31m53.1 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m:00:01\u001b[0m0:01\u001b[0m\n",
      "\u001b[?25hRequirement already satisfied: numpy>=1.16.5 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from yfinance==0.2.4) (1.21.6)\n",
      "Requirement already satisfied: pandas>=1.3.0 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from yfinance==0.2.4) (1.3.5)\n",
      "Requirement already satisfied: requests>=2.26 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from yfinance==0.2.4) (2.28.1)\n",
      "Collecting beautifulsoup4>=4.11.1\n",
      "  Downloading beautifulsoup4-4.11.2-py3-none-any.whl (129 kB)\n",
      "\u001b[2K     \u001b[90m━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━\u001b[0m \u001b[32m129.4/129.4 kB\u001b[0m \u001b[31m14.8 MB/s\u001b[0m eta \u001b[36m0:00:00\u001b[0m\n",
      "\u001b[?25hRequirement already satisfied: soupsieve>1.2 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from beautifulsoup4>=4.11.1->yfinance==0.2.4) (2.3.2.post1)\n",
      "Requirement already satisfied: cffi>=1.12 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from cryptography>=3.3.2->yfinance==0.2.4) (1.15.1)\n",
      "Requirement already satisfied: webencodings in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from html5lib>=1.1->yfinance==0.2.4) (0.5.1)\n",
      "Requirement already satisfied: six>=1.9 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from html5lib>=1.1->yfinance==0.2.4) (1.16.0)\n",
      "Requirement already satisfied: python-dateutil>=2.7.3 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from pandas>=1.3.0->yfinance==0.2.4) (2.8.2)\n",
      "Requirement already satisfied: charset-normalizer<3,>=2 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from requests>=2.26->yfinance==0.2.4) (2.1.1)\n",
      "Requirement already satisfied: certifi>=2017.4.17 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from requests>=2.26->yfinance==0.2.4) (2022.12.7)\n",
      "Requirement already satisfied: urllib3<1.27,>=1.21.1 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from requests>=2.26->yfinance==0.2.4) (1.26.13)\n",
      "Requirement already satisfied: idna<4,>=2.5 in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from requests>=2.26->yfinance==0.2.4) (3.4)\n",
      "Requirement already satisfied: pycparser in /home/jupyterlab/conda/envs/python/lib/python3.7/site-packages (from cffi>=1.12->cryptography>=3.3.2->yfinance==0.2.4) (2.21)\n",
      "Installing collected packages: multitasking, appdirs, lxml, frozendict, beautifulsoup4, yfinance\n",
      "  Attempting uninstall: lxml\n",
      "    Found existing installation: lxml 4.6.4\n",
      "    Uninstalling lxml-4.6.4:\n",
      "      Successfully uninstalled lxml-4.6.4\n",
      "  Attempting uninstall: beautifulsoup4\n",
      "    Found existing installation: beautifulsoup4 4.10.0\n",
      "    Uninstalling beautifulsoup4-4.10.0:\n",
      "      Successfully uninstalled beautifulsoup4-4.10.0\n",
      "Successfully installed appdirs-1.4.4 beautifulsoup4-4.11.2 frozendict-2.3.5 lxml-4.9.2 multitasking-0.0.11 yfinance-0.2.4\n"
     ]
    }
   ],
   "source": [
    "!pip install yfinance==0.2.4\n",
    "#!pip install pandas==1.3.3"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 2,
   "metadata": {},
   "outputs": [],
   "source": [
    "import yfinance as yf\n",
    "import pandas as pd"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "tags": []
   },
   "source": [
    "## Using the yfinance Library to Extract Stock Data\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Using the `Ticker` module we can create an object that will allow us to access functions to extract data. To do this we need to provide the ticker symbol for the stock, here the company is Apple and the ticker symbol is `AAPL`.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 3,
   "metadata": {},
   "outputs": [],
   "source": [
    "apple = yf.Ticker(\"AAPL\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Now we can access functions and variables to extract the type of data we need. You can view them and what they represent here https://aroussi.com/post/python-yahoo-finance.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 4,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "--2023-02-21 06:11:22--  https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/data/apple.json\n",
      "Resolving cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud (cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud)... 169.63.118.104\n",
      "Connecting to cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud (cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud)|169.63.118.104|:443... connected.\n",
      "HTTP request sent, awaiting response... 200 OK\n",
      "Length: 5699 (5.6K) [application/json]\n",
      "Saving to: ‘apple.json’\n",
      "\n",
      "apple.json          100%[===================>]   5.57K  --.-KB/s    in 0s      \n",
      "\n",
      "2023-02-21 06:11:23 (46.4 MB/s) - ‘apple.json’ saved [5699/5699]\n",
      "\n"
     ]
    }
   ],
   "source": [
    "!wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/data/apple.json"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "### Stock Info\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Using the attribute  <code>info</code> we can extract information about the stock as a Python dictionary.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 5,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "{'zip': '95014',\n",
       " 'sector': 'Technology',\n",
       " 'fullTimeEmployees': 100000,\n",
       " 'longBusinessSummary': 'Apple Inc. designs, manufactures, and markets smartphones, personal computers, tablets, wearables, and accessories worldwide. It also sells various related services. In addition, the company offers iPhone, a line of smartphones; Mac, a line of personal computers; iPad, a line of multi-purpose tablets; AirPods Max, an over-ear wireless headphone; and wearables, home, and accessories comprising AirPods, Apple TV, Apple Watch, Beats products, HomePod, and iPod touch. Further, it provides AppleCare support services; cloud services store services; and operates various platforms, including the App Store that allow customers to discover and download applications and digital content, such as books, music, video, games, and podcasts. Additionally, the company offers various services, such as Apple Arcade, a game subscription service; Apple Music, which offers users a curated listening experience with on-demand radio stations; Apple News+, a subscription news and magazine service; Apple TV+, which offers exclusive original content; Apple Card, a co-branded credit card; and Apple Pay, a cashless payment service, as well as licenses its intellectual property. The company serves consumers, and small and mid-sized businesses; and the education, enterprise, and government markets. It distributes third-party applications for its products through the App Store. The company also sells its products through its retail and online stores, and direct sales force; and third-party cellular network carriers, wholesalers, retailers, and resellers. Apple Inc. was incorporated in 1977 and is headquartered in Cupertino, California.',\n",
       " 'city': 'Cupertino',\n",
       " 'phone': '408 996 1010',\n",
       " 'state': 'CA',\n",
       " 'country': 'United States',\n",
       " 'companyOfficers': [],\n",
       " 'website': 'https://www.apple.com',\n",
       " 'maxAge': 1,\n",
       " 'address1': 'One Apple Park Way',\n",
       " 'industry': 'Consumer Electronics',\n",
       " 'ebitdaMargins': 0.33890998,\n",
       " 'profitMargins': 0.26579002,\n",
       " 'grossMargins': 0.43019,\n",
       " 'operatingCashflow': 112241000448,\n",
       " 'revenueGrowth': 0.112,\n",
       " 'operatingMargins': 0.309,\n",
       " 'ebitda': 128217997312,\n",
       " 'targetLowPrice': 160,\n",
       " 'recommendationKey': 'buy',\n",
       " 'grossProfits': 152836000000,\n",
       " 'freeCashflow': 80153247744,\n",
       " 'targetMedianPrice': 199.5,\n",
       " 'currentPrice': 177.77,\n",
       " 'earningsGrowth': 0.25,\n",
       " 'currentRatio': 1.038,\n",
       " 'returnOnAssets': 0.19875,\n",
       " 'numberOfAnalystOpinions': 44,\n",
       " 'targetMeanPrice': 193.53,\n",
       " 'debtToEquity': 170.714,\n",
       " 'returnOnEquity': 1.45567,\n",
       " 'targetHighPrice': 215,\n",
       " 'totalCash': 63913000960,\n",
       " 'totalDebt': 122797998080,\n",
       " 'totalRevenue': 378323009536,\n",
       " 'totalCashPerShare': 3.916,\n",
       " 'financialCurrency': 'USD',\n",
       " 'revenuePerShare': 22.838,\n",
       " 'quickRatio': 0.875,\n",
       " 'recommendationMean': 1.8,\n",
       " 'exchange': 'NMS',\n",
       " 'shortName': 'Apple Inc.',\n",
       " 'longName': 'Apple Inc.',\n",
       " 'exchangeTimezoneName': 'America/New_York',\n",
       " 'exchangeTimezoneShortName': 'EDT',\n",
       " 'isEsgPopulated': False,\n",
       " 'gmtOffSetMilliseconds': '-14400000',\n",
       " 'quoteType': 'EQUITY',\n",
       " 'symbol': 'AAPL',\n",
       " 'messageBoardId': 'finmb_24937',\n",
       " 'market': 'us_market',\n",
       " 'annualHoldingsTurnover': None,\n",
       " 'enterpriseToRevenue': 7.824,\n",
       " 'beta3Year': None,\n",
       " 'enterpriseToEbitda': 23.086,\n",
       " '52WeekChange': 0.4549594,\n",
       " 'morningStarRiskRating': None,\n",
       " 'forwardEps': 6.56,\n",
       " 'revenueQuarterlyGrowth': None,\n",
       " 'sharesOutstanding': 16319399936,\n",
       " 'fundInceptionDate': None,\n",
       " 'annualReportExpenseRatio': None,\n",
       " 'totalAssets': None,\n",
       " 'bookValue': 4.402,\n",
       " 'sharesShort': 111286790,\n",
       " 'sharesPercentSharesOut': 0.0068,\n",
       " 'fundFamily': None,\n",
       " 'lastFiscalYearEnd': 1632528000,\n",
       " 'heldPercentInstitutions': 0.59397,\n",
       " 'netIncomeToCommon': 100554997760,\n",
       " 'trailingEps': 6.015,\n",
       " 'lastDividendValue': 0.22,\n",
       " 'SandP52WeekChange': 0.15217662,\n",
       " 'priceToBook': 40.38392,\n",
       " 'heldPercentInsiders': 0.0007,\n",
       " 'nextFiscalYearEnd': 1695600000,\n",
       " 'yield': None,\n",
       " 'mostRecentQuarter': 1640390400,\n",
       " 'shortRatio': 1.21,\n",
       " 'sharesShortPreviousMonthDate': 1644883200,\n",
       " 'floatShares': 16302795170,\n",
       " 'beta': 1.185531,\n",
       " 'enterpriseValue': 2959991898112,\n",
       " 'priceHint': 2,\n",
       " 'threeYearAverageReturn': None,\n",
       " 'lastSplitDate': 1598832000,\n",
       " 'lastSplitFactor': '4:1',\n",
       " 'legalType': None,\n",
       " 'lastDividendDate': 1643932800,\n",
       " 'morningStarOverallRating': None,\n",
       " 'earningsQuarterlyGrowth': 0.204,\n",
       " 'priceToSalesTrailing12Months': 7.668314,\n",
       " 'dateShortInterest': 1647302400,\n",
       " 'pegRatio': 1.94,\n",
       " 'ytdReturn': None,\n",
       " 'forwardPE': 27.099087,\n",
       " 'lastCapGain': None,\n",
       " 'shortPercentOfFloat': 0.0068,\n",
       " 'sharesShortPriorMonth': 108944701,\n",
       " 'impliedSharesOutstanding': 0,\n",
       " 'category': None,\n",
       " 'fiveYearAverageReturn': None,\n",
       " 'previousClose': 178.96,\n",
       " 'regularMarketOpen': 178.55,\n",
       " 'twoHundredDayAverage': 156.03505,\n",
       " 'trailingAnnualDividendYield': 0.004833482,\n",
       " 'payoutRatio': 0.1434,\n",
       " 'volume24Hr': None,\n",
       " 'regularMarketDayHigh': 179.61,\n",
       " 'navPrice': None,\n",
       " 'averageDailyVolume10Day': 93823630,\n",
       " 'regularMarketPreviousClose': 178.96,\n",
       " 'fiftyDayAverage': 166.498,\n",
       " 'trailingAnnualDividendRate': 0.865,\n",
       " 'open': 178.55,\n",
       " 'toCurrency': None,\n",
       " 'averageVolume10days': 93823630,\n",
       " 'expireDate': None,\n",
       " 'algorithm': None,\n",
       " 'dividendRate': 0.88,\n",
       " 'exDividendDate': 1643932800,\n",
       " 'circulatingSupply': None,\n",
       " 'startDate': None,\n",
       " 'regularMarketDayLow': 176.7,\n",
       " 'currency': 'USD',\n",
       " 'trailingPE': 29.55445,\n",
       " 'regularMarketVolume': 92633154,\n",
       " 'lastMarket': None,\n",
       " 'maxSupply': None,\n",
       " 'openInterest': None,\n",
       " 'marketCap': 2901099675648,\n",
       " 'volumeAllCurrencies': None,\n",
       " 'strikePrice': None,\n",
       " 'averageVolume': 95342043,\n",
       " 'dayLow': 176.7,\n",
       " 'ask': 178.53,\n",
       " 'askSize': 800,\n",
       " 'volume': 92633154,\n",
       " 'fiftyTwoWeekHigh': 182.94,\n",
       " 'fromCurrency': None,\n",
       " 'fiveYearAvgDividendYield': 1.13,\n",
       " 'fiftyTwoWeekLow': 122.25,\n",
       " 'bid': 178.4,\n",
       " 'tradeable': False,\n",
       " 'dividendYield': 0.005,\n",
       " 'bidSize': 3200,\n",
       " 'dayHigh': 179.61,\n",
       " 'regularMarketPrice': 177.77,\n",
       " 'preMarketPrice': 178.38,\n",
       " 'logo_url': 'https://logo.clearbit.com/apple.com'}"
      ]
     },
     "execution_count": 5,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "import json\n",
    "with open('apple.json') as json_file:\n",
    "    apple_info = json.load(json_file)\n",
    "    # Print the type of data variable    \n",
    "    #print(\"Type:\", type(apple_info))\n",
    "apple_info"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "We can get the <code>'country'</code> using the key country\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 6,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'United States'"
      ]
     },
     "execution_count": 6,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "apple_info['country']"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "tags": []
   },
   "source": [
    "### Extracting Share Price\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "A share is the single smallest part of a company's stock  that you can buy, the prices of these shares fluctuate over time. Using the <code>history()</code> method we can get the share price of the stock over a certain period of time. Using the `period` parameter we can set how far back from the present to get data. The options for `period` are 1 day (1d), 5d, 1 month (1mo) , 3mo, 6mo, 1 year (1y), 2y, 5y, 10y, ytd, and max.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 7,
   "metadata": {},
   "outputs": [],
   "source": [
    "apple_share_price_data = apple.history(period=\"max\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "The format that the data is returned in is a Pandas DataFrame. With the `Date` as the index the share `Open`, `High`, `Low`, `Close`, `Volume`, and `Stock Splits` are given for each day.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 8,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Open</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Close</th>\n",
       "      <th>Volume</th>\n",
       "      <th>Dividends</th>\n",
       "      <th>Stock Splits</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>1980-12-12 00:00:00-05:00</th>\n",
       "      <td>0.099722</td>\n",
       "      <td>0.100155</td>\n",
       "      <td>0.099722</td>\n",
       "      <td>0.099722</td>\n",
       "      <td>469033600</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1980-12-15 00:00:00-05:00</th>\n",
       "      <td>0.094953</td>\n",
       "      <td>0.094953</td>\n",
       "      <td>0.094519</td>\n",
       "      <td>0.094519</td>\n",
       "      <td>175884800</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1980-12-16 00:00:00-05:00</th>\n",
       "      <td>0.088015</td>\n",
       "      <td>0.088015</td>\n",
       "      <td>0.087582</td>\n",
       "      <td>0.087582</td>\n",
       "      <td>105728000</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1980-12-17 00:00:00-05:00</th>\n",
       "      <td>0.089749</td>\n",
       "      <td>0.090183</td>\n",
       "      <td>0.089749</td>\n",
       "      <td>0.089749</td>\n",
       "      <td>86441600</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1980-12-18 00:00:00-05:00</th>\n",
       "      <td>0.092351</td>\n",
       "      <td>0.092785</td>\n",
       "      <td>0.092351</td>\n",
       "      <td>0.092351</td>\n",
       "      <td>73449600</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                               Open      High       Low     Close     Volume  \\\n",
       "Date                                                                           \n",
       "1980-12-12 00:00:00-05:00  0.099722  0.100155  0.099722  0.099722  469033600   \n",
       "1980-12-15 00:00:00-05:00  0.094953  0.094953  0.094519  0.094519  175884800   \n",
       "1980-12-16 00:00:00-05:00  0.088015  0.088015  0.087582  0.087582  105728000   \n",
       "1980-12-17 00:00:00-05:00  0.089749  0.090183  0.089749  0.089749   86441600   \n",
       "1980-12-18 00:00:00-05:00  0.092351  0.092785  0.092351  0.092351   73449600   \n",
       "\n",
       "                           Dividends  Stock Splits  \n",
       "Date                                                \n",
       "1980-12-12 00:00:00-05:00        0.0           0.0  \n",
       "1980-12-15 00:00:00-05:00        0.0           0.0  \n",
       "1980-12-16 00:00:00-05:00        0.0           0.0  \n",
       "1980-12-17 00:00:00-05:00        0.0           0.0  \n",
       "1980-12-18 00:00:00-05:00        0.0           0.0  "
      ]
     },
     "execution_count": 8,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "apple_share_price_data.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "We can reset the index of the DataFrame with the `reset_index` function. We also set the `inplace` paramter to `True` so the change takes place to the DataFrame itself.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 9,
   "metadata": {},
   "outputs": [],
   "source": [
    "apple_share_price_data.reset_index(inplace=True)"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "We can plot the `Open` price against the `Date`:\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 10,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:xlabel='Date'>"
      ]
     },
     "execution_count": 10,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "iVBORw0KGgoAAAANSUhEUgAAAigAAAGVCAYAAADUsQqzAAAAOXRFWHRTb2Z0d2FyZQBNYXRwbG90bGliIHZlcnNpb24zLjUuMywgaHR0cHM6Ly9tYXRwbG90bGliLm9yZy/NK7nSAAAACXBIWXMAAA9hAAAPYQGoP6dpAABOT0lEQVR4nO3deXgT5doG8HuSNOlCW6ClG5QWkQoKsu8ioGwVUQE5IHwKLiCiKAIfytGjuOKKqIh6vqOAgqKo4AIKCAIiqCyHTWQve0vZutKmWZ7vj9KhadMNks4kvX/XlauZdybT5+m0zZN33nlHEREBERERkY4YtA6AiIiIqCQWKERERKQ7LFCIiIhId1igEBERke6wQCEiIiLdYYFCREREusMChYiIiHTHpHUAl8PpdOLkyZMIDQ2Foihah0NERESVICLIzs5GXFwcDIby+0h8skA5efIk4uPjtQ6DiIiILsOxY8fQoEGDcrfxyQIlNDQUQGGCYWFhGkdDRERElZGVlYX4+Hj1fbw8PlmgFJ3WCQsLY4FCRETkYyozPIODZImIiEh3WKAQERGR7rBAISIiIt3xyTEoleVwOGCz2bQOw2+YzeYKLwsjIiLyBL8sUEQEaWlpyMjI0DoUv2IwGNCoUSOYzWatQyEiIj/nlwVKUXESFRWF4OBgTubmAUWT46WmpqJhw4b8mRIRkVf5XYHicDjU4iQiIkLrcPxKvXr1cPLkSdjtdgQEBGgdDhER+TG/G1BQNOYkODhY40j8T9GpHYfDoXEkRETk7/yuQCnCUxCex58pERFVF78tUIiIiMh3sUAhIiIi3WGBojPHjh3D/fffj7i4OJjNZiQkJOCxxx7D2bNntQ6NiIh8kMMpmPrNDny15bjWoVQJCxQdOXToENq1a4d9+/bh888/x4EDB/DBBx9g1apV6Ny5M86dO6d1iERE5GN+2HESn/95DJMXbdc6lCphgaIjDz/8MMxmM1asWIHu3bujYcOGSE5Oxs8//4wTJ07gqaeeAgAkJibihRdewPDhw1GrVi3ExcXh3XffddlXZmYmxowZg6ioKISFheGmm27C9u2XfjmnTZuGVq1a4dNPP0ViYiLCw8MxbNgwZGdnV2vORETkXUfOXtA6hMtSIwoUEcGFArsmDxGpVIznzp3D8uXLMW7cOAQFBbmsi4mJwYgRI/DFF1+o+3v99ddx/fXXY+vWrZg6dSoef/xxrFy5Us23f//+SEtLw7Jly7Blyxa0adMGN998s0svzMGDB7FkyRL88MMP+OGHH7B27Vq88sorHvqpExGRHsxYuU/rEC6L303U5k6ezYFrn1muyffe/XxfBJsr/jHv378fIoJmzZq5Xd+sWTOcP38ep0+fBgB07doVTz75JAAgKSkJv/32G9566y307t0bv/zyC3bu3In09HRYLBYAwBtvvIElS5bgq6++wpgxYwAUzg47d+5chIaGAgDuvvturFq1Ci+99NIV501ERHQlakQPij8o6jkpmoukc+fOLus7d+6Mv//+GwCwZcsW5OTkICIiArVq1VIfKSkpOHjwoPqaxMREtTgBgNjYWKSnp3s7FSIiogrViB6UoAAjdj/fV7PvXRlXX301FEXB7t27cccdd5Rav2fPHtSpUweRkZFl7qOoeHE6nYiNjcWaNWtKbVO7dm31ecnp6hVFgdPprFS8RETke46du4CNB89iYJv6CDDqu4+iRhQoiqJU6jSLliIiItC7d2/Mnj0bjz/+uMs4lLS0NCxYsAD33HOPWoT8/vvvLq///fff0bRpUwBAmzZtkJaWBpPJhMTExGrLgYiI9K3nG2tgdwrOXSjA2O6NtQ6nXFUun9atW4cBAwYgLi4OiqJgyZIlLusVRXH7eP3119VtevToUWr9sGHDrjgZXzdr1ixYrVb07dsX69atw7Fjx/DTTz+hd+/eqF+/vsvYkN9++w2vvfYa9u3bh/feew+LFi3CY489BgDo1asXOnfujDvuuAPLly/H4cOHsWHDBjz99NPYvHmzVukREZHG7M7C4QIfrU/ROJKKVblAyc3NRcuWLTFr1iy361NTU10eH3/8MRRFweDBg122Gz16tMt2H3744eVl4EeaNGmCzZs3o3Hjxhg6dCgaN26MMWPGoGfPnti4cSPq1q2rbjtp0iRs2bIFrVu3xgsvvIA333wTffsWnsZSFAXLli3DjTfeiPvuuw9JSUkYNmwYDh8+jOjoaK3SIyIinTidbdU6hAopUtnrYN29WFGwePFit2Mmitxxxx3Izs7GqlWr1LYePXqgVatWmDlz5mV936ysLISHhyMzMxNhYWEu6/Lz85GSkoJGjRohMDDwsvavd4mJiZgwYQImTJhQrd+3JvxsiYj8TeKTS922H36lfzVHUv77d0leHSFz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FihERETkYWv3ni53fUWXGTv1cJlOBVigEBER+ZjNR86Vu77kDQF9EQsUIiIiH1PRGJOKTgE9kdwUADCqS6KnQvI43x/mS0REVMOEVHCVTmJESLnre14The3P9kFYoH7LAP1GRkRERG6VN4QkLNBU4UyyABAeFODBiDyvyqd41q1bhwEDBiAuLg6KomDJkiXqOpvNhieeeAItWrRASEgI4uLicM899+DkSdeZ6Xr06AFFUVwew4YNu+JkiIiIaoLvtp8oc11ggLEaI/GeKhcoubm5aNmyJWbNmlVq3YULF7B161b861//wtatW/HNN99g3759uO2220ptO3r0aKSmpqqPDz/88PIyICIiqmG+3Hy8zHXp2dbL3m+ojiZ4q3IkycnJSE5OdrsuPDwcK1eudGl799130aFDBxw9ehQNGzZU24ODgxETE1PVb09EREQ1gNev4snMzISiKKhdu7ZL+4IFCxAZGYnrrrsOkydPRnZ2dpn7sFqtyMrKcnkQERGRZ00f3AIAMLF3ksaReHmQbH5+Pp588kkMHz4cYWFhavuIESPQqFEjxMTEYNeuXZg6dSq2b99eqvelyPTp0/Hcc895M1QiIqIa79br49A9qR5CA7UfQOu1AsVms2HYsGFwOp2YPXu2y7rRo0erz5s3b44mTZqgXbt22Lp1K9q0aVNqX1OnTsXEiRPV5aysLMTHx3srdCIiohpLD8UJ4KUCxWaz4R//+AdSUlKwevVql94Td9q0aYOAgADs37/fbYFisVhgsej/vgFERETkGR4vUIqKk/379+OXX35BREREha/566+/YLPZEBsb6+lwiIiIyAdVuUDJycnBgQMH1OWUlBRs27YNdevWRVxcHO68805s3boVP/zwAxwOB9LS0gAAdevWhdlsxsGDB7FgwQLccsstiIyMxO7duzFp0iS0bt0aXbt29VxmRERENVC/6/zjCtkqFyibN29Gz5491eWisSEjR47EtGnT8N133wEAWrVq5fK6X375BT169IDZbMaqVavw9ttvIycnB/Hx8ejfvz+effZZGI3+MbkMERGRVh7XwRU4nlDlAqVHjx6QcubYLW8dAMTHx2Pt2rVV/bZERERUgVcGtcA1MaFah+ERvJsxERGRnxjWoWHFG/kIFihERESkOyxQiIiISHdYoBAREfmoyFr+O0cYCxQiIiIf9dLA5lqH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sbFy5513ytSpU+Xmm28WRVHku+++0zDayjlw4IBL1exwOHz+WJXMScT3j9NLL70kzzzzjHz++edqW35+viQkJMizzz4rIiIFBQXqunbt2sm9996r/nPVK3d5iYiMGjVKAgMDZdSoUbJt2zbZsWOHfP/99xIYGCjPP/+8RtFWztKlS0XE9dPohQsXpFGjRj59rErmVfT13nvv9dlj9eGHH8q///1vWbt2rdqWk5Pj88eqKK81a9a4tHv7WOm6QJkzZ47ExMRIixYtJDQ0VMaNGycnTpwQEZEHH3xQrr/+enXbooP+yiuvSHx8vNrtpEfu8jpy5IiIiGzcuFFat24tX375pUvhMnr0aGnSpInLL7eefPTRR9KwYUNp27atdOzYUT799FM1/jFjxvjksSqZ0/z588VqtYpI4acHXzxOf/zxhzRs2FDatGkjycnJEhoaKoMHD5aDBw+KiMjkyZMlKSlJTp06JSKidtXOmzdPateurdtxQ+7yuvPOO+Xvv/8WEZG0tDR5+umn1f8fRd544w2JjIzU5fH64YcfpH79+qIoivz2228iUljwixQWKFOmTPHJY+UuL6fTqf4dpaen+9yx+uyzzyQqKko6d+4srVq1knr16slLL70kIiKZmZk+e6zc5fXyyy+r6719rHRboPznP/+Rq6++Wj7//HM5ffq0LFiwQEJCQmTbtm0iIvL1119L06ZNZebMmSJyqdvs9OnTEhQUJL/++qtmsZfHXV61atVyGWi5YcOGUmMa/v77bzGbzbJhw4ZqjrhiM2fOVHNav369PPPMM6IoisyePVucTqd8//33kpSU5FPHyl1OBoNB3nvvPTX+9evX+9RxEhGZOHGi9O/fX0QK3+x27twpCQkJMnbsWMnIyJDff/9d2rRpI+PGjRORS59qf/nlF4mKipLt27drFnt5ysrroYceUv95uhsn9Pnnn0udOnVk586d1RpvRX799Vfp16+fPPLII5KcnCzt2rUrtc3PP/8s7du396ljVVFeRTnk5uaWeq1ej9WCBQukZcuW8sEHH4iIyIkTJ2TWrFkSEhIimZmZIiKycuVKnztW5eVV/G/Jm8dKdwVKUSU9fPhwufvuu13WJSUlydatW0Wk8BPRo48+KvHx8S7V24oVK6Rhw4ZqIaMXFeVVVrxFn5j+85//SHR0tO7+OHNzc6V3795q92XRH163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\n",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "apple_share_price_data.plot(x=\"Date\", y=\"Open\")"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "tags": []
   },
   "source": [
    "### Extracting Dividends\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Dividends are the distribution of a companys profits to shareholders. In this case they are defined as an amount of money returned per share an investor owns. Using the variable `dividends` we can get a dataframe of the data. The period of the data is given by the period defined in the 'history` function.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 11,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Date\n",
       "1987-05-11 00:00:00-04:00    0.000536\n",
       "1987-08-10 00:00:00-04:00    0.000536\n",
       "1987-11-17 00:00:00-05:00    0.000714\n",
       "1988-02-12 00:00:00-05:00    0.000714\n",
       "1988-05-16 00:00:00-04:00    0.000714\n",
       "                               ...   \n",
       "2022-02-04 00:00:00-05:00    0.220000\n",
       "2022-05-06 00:00:00-04:00    0.230000\n",
       "2022-08-05 00:00:00-04:00    0.230000\n",
       "2022-11-04 00:00:00-04:00    0.230000\n",
       "2023-02-10 00:00:00-05:00    0.230000\n",
       "Name: Dividends, Length: 78, dtype: float64"
      ]
     },
     "execution_count": 11,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "apple.dividends"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "We can plot the dividends overtime:\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 12,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "<AxesSubplot:xlabel='Date'>"
      ]
     },
     "execution_count": 12,
     "metadata": {},
     "output_type": "execute_result"
    },
    {
     "data": {
      "image/png": "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oHHjxjVePxHVPAYWIlJcYmIiAgICcP78eQwePBjR0dGYP38+GjVqhF27dmHcuHEoKiq66eNNJhN0Oh3i4+Oh0+lKfa1+/fo1XT4R1QIGFiJS1M8//4wjR45g6tSp2L9/PwwGA95++21otcVL7NavX19qvIODA4xGY6ljHTt2hNFoRHp6Onr27FlrtRNR7WFgIaJaU1BQgLS0NBiNRly+fBk//vgjFi5ciCFDhmDs2LE4cuQIDAYD3n//fQwdOhS7d+/GBx98UOo5WrRogZycHPz0009o3749nJ2dERwcjEceeQRjx47F22+/jY4dOyIjIwM///wz2rVrh8GDByvUMRFVF14lRES15scff0TTpk3RokULDBw4EL/88gsWL16M7777DjqdDh06dMA777yDN954A23btsXq1auxcOHCUs/RvXt3REdHY9SoUfDw8MCbb74JAFi+fDnGjh2LZ599FiEhIbj33nuxd+9e+Pn5KdEqEVUzXiVEREREVo8zLERERGT1GFiIiIjI6jGwEBERkdVjYCEiIiKrx8BCREREVo+BhYiIiKweAwsRERFZPQYWIiIisnoMLERERGT1GFiIiIjI6jGwEBERkdX7f1NHf7Jb1oiKAAAAAElFTkSuQmCC\n",
      "text/plain": [
       "<Figure size 640x480 with 1 Axes>"
      ]
     },
     "metadata": {},
     "output_type": "display_data"
    }
   ],
   "source": [
    "apple.dividends.plot()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Exercise \n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "Now using the `Ticker` module create an object for AMD (Advanced Micro Devices) with the ticker symbol is `AMD` called; name the object <code>amd</code>.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 13,
   "metadata": {},
   "outputs": [],
   "source": [
    "amd = yf.Ticker(\"AMD\")"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 14,
   "metadata": {},
   "outputs": [
    {
     "name": "stdout",
     "output_type": "stream",
     "text": [
      "--2023-02-21 06:22:36--  https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/data/amd.json\n",
      "Resolving cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud (cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud)... 169.63.118.104\n",
      "Connecting to cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud (cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud)|169.63.118.104|:443... connected.\n",
      "HTTP request sent, awaiting response... 200 OK\n",
      "Length: 5838 (5.7K) [application/json]\n",
      "Saving to: ‘amd.json’\n",
      "\n",
      "amd.json            100%[===================>]   5.70K  --.-KB/s    in 0s      \n",
      "\n",
      "2023-02-21 06:22:36 (33.4 MB/s) - ‘amd.json’ saved [5838/5838]\n",
      "\n"
     ]
    }
   ],
   "source": [
    "!wget https://cf-courses-data.s3.us.cloud-object-storage.appdomain.cloud/IBMDeveloperSkillsNetwork-PY0220EN-SkillsNetwork/data/amd.json"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 15,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "{'zip': '95054',\n",
       " 'sector': 'Technology',\n",
       " 'fullTimeEmployees': 15500,\n",
       " 'longBusinessSummary': 'Advanced Micro Devices, Inc. operates as a semiconductor company worldwide. The company operates in two segments, Computing and Graphics; and Enterprise, Embedded and Semi-Custom. Its products include x86 microprocessors as an accelerated processing unit, chipsets, discrete and integrated graphics processing units (GPUs), data center and professional GPUs, and development services; and server and embedded processors, and semi-custom System-on-Chip (SoC) products, development services, and technology for game consoles. The company provides processors for desktop and notebook personal computers under the AMD Ryzen, AMD Ryzen PRO, Ryzen Threadripper, Ryzen Threadripper PRO, AMD Athlon, AMD Athlon PRO, AMD FX, AMD A-Series, and AMD PRO A-Series processors brands; discrete GPUs for desktop and notebook PCs under the AMD Radeon graphics, AMD Embedded Radeon graphics brands; and professional graphics products under the AMD Radeon Pro and AMD FirePro graphics brands. It also offers Radeon Instinct, Radeon PRO V-series, and AMD Instinct accelerators for servers; chipsets under the AMD trademark; microprocessors for servers under the AMD EPYC; embedded processor solutions under the AMD Athlon, AMD Geode, AMD Ryzen, AMD EPYC, AMD R-Series, and G-Series processors brands; and customer-specific solutions based on AMD CPU, GPU, and multi-media technologies, as well as semi-custom SoC products. It serves original equipment manufacturers, public cloud service providers, original design manufacturers, system integrators, independent distributors, online retailers, and add-in-board manufacturers through its direct sales force, independent distributors, and sales representatives. The company was incorporated in 1969 and is headquartered in Santa Clara, California.',\n",
       " 'city': 'Santa Clara',\n",
       " 'phone': '408 749 4000',\n",
       " 'state': 'CA',\n",
       " 'country': 'United States',\n",
       " 'companyOfficers': [],\n",
       " 'website': 'https://www.amd.com',\n",
       " 'maxAge': 1,\n",
       " 'address1': '2485 Augustine Drive',\n",
       " 'industry': 'Semiconductors',\n",
       " 'ebitdaMargins': 0.24674,\n",
       " 'profitMargins': 0.19240999,\n",
       " 'grossMargins': 0.48248002,\n",
       " 'operatingCashflow': 3520999936,\n",
       " 'revenueGrowth': 0.488,\n",
       " 'operatingMargins': 0.22198,\n",
       " 'ebitda': 4055000064,\n",
       " 'targetLowPrice': 107,\n",
       " 'recommendationKey': 'buy',\n",
       " 'grossProfits': 7929000000,\n",
       " 'freeCashflow': 3122749952,\n",
       " 'targetMedianPrice': 150,\n",
       " 'currentPrice': 119.22,\n",
       " 'earningsGrowth': -0.454,\n",
       " 'currentRatio': 2.024,\n",
       " 'returnOnAssets': 0.21327,\n",
       " 'numberOfAnalystOpinions': 38,\n",
       " 'targetMeanPrice': 152.02,\n",
       " 'debtToEquity': 9.764,\n",
       " 'returnOnEquity': 0.47428,\n",
       " 'targetHighPrice': 200,\n",
       " 'totalCash': 3608000000,\n",
       " 'totalDebt': 732000000,\n",
       " 'totalRevenue': 16433999872,\n",
       " 'totalCashPerShare': 3.008,\n",
       " 'financialCurrency': 'USD',\n",
       " 'revenuePerShare': 13.548,\n",
       " 'quickRatio': 1.49,\n",
       " 'recommendationMean': 2.2,\n",
       " 'exchange': 'NMS',\n",
       " 'shortName': 'Advanced Micro Devices, Inc.',\n",
       " 'longName': 'Advanced Micro Devices, Inc.',\n",
       " 'exchangeTimezoneName': 'America/New_York',\n",
       " 'exchangeTimezoneShortName': 'EDT',\n",
       " 'isEsgPopulated': False,\n",
       " 'gmtOffSetMilliseconds': '-14400000',\n",
       " 'quoteType': 'EQUITY',\n",
       " 'symbol': 'AMD',\n",
       " 'messageBoardId': 'finmb_168864',\n",
       " 'market': 'us_market',\n",
       " 'annualHoldingsTurnover': None,\n",
       " 'enterpriseToRevenue': 8.525,\n",
       " 'beta3Year': None,\n",
       " 'enterpriseToEbitda': 34.551,\n",
       " '52WeekChange': 0.51966953,\n",
       " 'morningStarRiskRating': None,\n",
       " 'forwardEps': 4.72,\n",
       " 'revenueQuarterlyGrowth': None,\n",
       " 'sharesOutstanding': 1627360000,\n",
       " 'fundInceptionDate': None,\n",
       " 'annualReportExpenseRatio': None,\n",
       " 'totalAssets': None,\n",
       " 'bookValue': 6.211,\n",
       " 'sharesShort': 27776129,\n",
       " 'sharesPercentSharesOut': 0.0171,\n",
       " 'fundFamily': None,\n",
       " 'lastFiscalYearEnd': 1640390400,\n",
       " 'heldPercentInstitutions': 0.52896,\n",
       " 'netIncomeToCommon': 3161999872,\n",
       " 'trailingEps': 2.57,\n",
       " 'lastDividendValue': 0.005,\n",
       " 'SandP52WeekChange': 0.15217662,\n",
       " 'priceToBook': 19.194977,\n",
       " 'heldPercentInsiders': 0.00328,\n",
       " 'nextFiscalYearEnd': 1703462400,\n",
       " 'yield': None,\n",
       " 'mostRecentQuarter': 1640390400,\n",
       " 'shortRatio': 0.24,\n",
       " 'sharesShortPreviousMonthDate': 1644883200,\n",
       " 'floatShares': 1193798619,\n",
       " 'beta': 1.848425,\n",
       " 'enterpriseValue': 140104957952,\n",
       " 'priceHint': 2,\n",
       " 'threeYearAverageReturn': None,\n",
       " 'lastSplitDate': 966902400,\n",
       " 'lastSplitFactor': '2:1',\n",
       " 'legalType': None,\n",
       " 'lastDividendDate': 798940800,\n",
       " 'morningStarOverallRating': None,\n",
       " 'earningsQuarterlyGrowth': -0.453,\n",
       " 'priceToSalesTrailing12Months': 11.805638,\n",
       " 'dateShortInterest': 1647302400,\n",
       " 'pegRatio': 0.99,\n",
       " 'ytdReturn': None,\n",
       " 'forwardPE': 25.258476,\n",
       " 'lastCapGain': None,\n",
       " 'shortPercentOfFloat': 0.0171,\n",
       " 'sharesShortPriorMonth': 88709340,\n",
       " 'impliedSharesOutstanding': 0,\n",
       " 'category': None,\n",
       " 'fiveYearAverageReturn': None,\n",
       " 'previousClose': 123.23,\n",
       " 'regularMarketOpen': 123.04,\n",
       " 'twoHundredDayAverage': 116.6998,\n",
       " 'trailingAnnualDividendYield': 0,\n",
       " 'payoutRatio': 0,\n",
       " 'volume24Hr': None,\n",
       " 'regularMarketDayHigh': 125.66,\n",
       " 'navPrice': None,\n",
       " 'averageDailyVolume10Day': 102167370,\n",
       " 'regularMarketPreviousClose': 123.23,\n",
       " 'fiftyDayAverage': 115.95,\n",
       " 'trailingAnnualDividendRate': 0,\n",
       " 'open': 123.04,\n",
       " 'toCurrency': None,\n",
       " 'averageVolume10days': 102167370,\n",
       " 'expireDate': None,\n",
       " 'algorithm': None,\n",
       " 'dividendRate': None,\n",
       " 'exDividendDate': 798940800,\n",
       " 'circulatingSupply': None,\n",
       " 'startDate': None,\n",
       " 'regularMarketDayLow': 118.59,\n",
       " 'currency': 'USD',\n",
       " 'trailingPE': 46.389107,\n",
       " 'regularMarketVolume': 99476946,\n",
       " 'lastMarket': None,\n",
       " 'maxSupply': None,\n",
       " 'openInterest': None,\n",
       " 'marketCap': 194013855744,\n",
       " 'volumeAllCurrencies': None,\n",
       " 'strikePrice': None,\n",
       " 'averageVolume': 102428813,\n",
       " 'dayLow': 118.59,\n",
       " 'ask': 117.24,\n",
       " 'askSize': 1100,\n",
       " 'volume': 99476946,\n",
       " 'fiftyTwoWeekHigh': 164.46,\n",
       " 'fromCurrency': None,\n",
       " 'fiveYearAvgDividendYield': None,\n",
       " 'fiftyTwoWeekLow': 72.5,\n",
       " 'bid': 117.24,\n",
       " 'tradeable': False,\n",
       " 'dividendYield': None,\n",
       " 'bidSize': 900,\n",
       " 'dayHigh': 125.66,\n",
       " 'regularMarketPrice': 119.22,\n",
       " 'preMarketPrice': 116.98,\n",
       " 'logo_url': 'https://logo.clearbit.com/amd.com'}"
      ]
     },
     "execution_count": 15,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "import json\n",
    "with open('amd.json') as json_file:\n",
    "    amd_info = json.load(json_file)\n",
    "    # Print the type of data variable    \n",
    "    #print(\"Type:\", type(apple_info))\n",
    "amd_info"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<b>Question 1</b> Use the key  <code>'country'</code> to find the country the stock belongs to, remember it as it will be a quiz question.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 16,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'United States'"
      ]
     },
     "execution_count": 16,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "amd_info['country']"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<b>Question 2</b> Use the key  <code>'sector'</code> to find the sector the stock belongs to, remember it as it will be a quiz question.\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 17,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "'Technology'"
      ]
     },
     "execution_count": 17,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "amd_info[\"sector\"]"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "<b>Question 3</b> Obtain stock data for AMD using the `history` function, set the `period` to max. Find the `Volume` traded on the first day (first row).\n"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 20,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/plain": [
       "Open            1.632800e+02\n",
       "High            1.644600e+02\n",
       "Low             1.561000e+02\n",
       "Close           1.619100e+02\n",
       "Volume          3.250584e+08\n",
       "Dividends       0.000000e+00\n",
       "Stock Splits    2.000000e+00\n",
       "dtype: float64"
      ]
     },
     "execution_count": 20,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "amd_share_price_data = amd.history(period=\"max\")\n",
    "amd_share_price_data.max()"
   ]
  },
  {
   "cell_type": "code",
   "execution_count": 21,
   "metadata": {},
   "outputs": [
    {
     "data": {
      "text/html": [
       "<div>\n",
       "<style scoped>\n",
       "    .dataframe tbody tr th:only-of-type {\n",
       "        vertical-align: middle;\n",
       "    }\n",
       "\n",
       "    .dataframe tbody tr th {\n",
       "        vertical-align: top;\n",
       "    }\n",
       "\n",
       "    .dataframe thead th {\n",
       "        text-align: right;\n",
       "    }\n",
       "</style>\n",
       "<table border=\"1\" class=\"dataframe\">\n",
       "  <thead>\n",
       "    <tr style=\"text-align: right;\">\n",
       "      <th></th>\n",
       "      <th>Open</th>\n",
       "      <th>High</th>\n",
       "      <th>Low</th>\n",
       "      <th>Close</th>\n",
       "      <th>Volume</th>\n",
       "      <th>Dividends</th>\n",
       "      <th>Stock Splits</th>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>Date</th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "      <th></th>\n",
       "    </tr>\n",
       "  </thead>\n",
       "  <tbody>\n",
       "    <tr>\n",
       "      <th>1980-03-17 00:00:00-05:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>3.302083</td>\n",
       "      <td>3.125000</td>\n",
       "      <td>3.145833</td>\n",
       "      <td>219600</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1980-03-18 00:00:00-05:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>3.125000</td>\n",
       "      <td>2.937500</td>\n",
       "      <td>3.031250</td>\n",
       "      <td>727200</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1980-03-19 00:00:00-05:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>3.083333</td>\n",
       "      <td>3.020833</td>\n",
       "      <td>3.041667</td>\n",
       "      <td>295200</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1980-03-20 00:00:00-05:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>3.062500</td>\n",
       "      <td>3.010417</td>\n",
       "      <td>3.010417</td>\n",
       "      <td>159600</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "    <tr>\n",
       "      <th>1980-03-21 00:00:00-05:00</th>\n",
       "      <td>0.0</td>\n",
       "      <td>3.020833</td>\n",
       "      <td>2.906250</td>\n",
       "      <td>2.916667</td>\n",
       "      <td>130800</td>\n",
       "      <td>0.0</td>\n",
       "      <td>0.0</td>\n",
       "    </tr>\n",
       "  </tbody>\n",
       "</table>\n",
       "</div>"
      ],
      "text/plain": [
       "                           Open      High       Low     Close  Volume  \\\n",
       "Date                                                                    \n",
       "1980-03-17 00:00:00-05:00   0.0  3.302083  3.125000  3.145833  219600   \n",
       "1980-03-18 00:00:00-05:00   0.0  3.125000  2.937500  3.031250  727200   \n",
       "1980-03-19 00:00:00-05:00   0.0  3.083333  3.020833  3.041667  295200   \n",
       "1980-03-20 00:00:00-05:00   0.0  3.062500  3.010417  3.010417  159600   \n",
       "1980-03-21 00:00:00-05:00   0.0  3.020833  2.906250  2.916667  130800   \n",
       "\n",
       "                           Dividends  Stock Splits  \n",
       "Date                                                \n",
       "1980-03-17 00:00:00-05:00        0.0           0.0  \n",
       "1980-03-18 00:00:00-05:00        0.0           0.0  \n",
       "1980-03-19 00:00:00-05:00        0.0           0.0  \n",
       "1980-03-20 00:00:00-05:00        0.0           0.0  \n",
       "1980-03-21 00:00:00-05:00        0.0           0.0  "
      ]
     },
     "execution_count": 21,
     "metadata": {},
     "output_type": "execute_result"
    }
   ],
   "source": [
    "amd_share_price_data.head()"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {
    "jp-MarkdownHeadingCollapsed": true,
    "tags": []
   },
   "source": [
    "<h2>About the Authors:</h2> \n",
    "\n",
    "<a href=\"https://www.linkedin.com/in/joseph-s-50398b136/?utm_medium=Exinfluencer&utm_source=Exinfluencer&utm_content=000026UJ&utm_term=10006555&utm_id=NA-SkillsNetwork-Channel-SkillsNetworkCoursesIBMDeveloperSkillsNetworkPY0220ENSkillsNetwork900-2022-01-01\">Joseph Santarcangelo</a> has a PhD in Electrical Engineering, his research focused on using machine learning, signal processing, and computer vision to determine how videos impact human cognition. Joseph has been working for IBM since he completed his PhD.\n",
    "\n",
    "Azim Hirjani\n"
   ]
  },
  {
   "cell_type": "markdown",
   "metadata": {},
   "source": [
    "## Change Log\n",
    "\n",
    "| Date (YYYY-MM-DD) | Version | Changed By    | Change Description        |\n",
    "| ----------------- | ------- | ------------- | ------------------------- |\n",
    "| 2020-11-10        | 1.1     | Malika Singla | Deleted the Optional part |\n",
    "| 2020-08-27        | 1.0     | Malika Singla | Added lab to GitLab       |\n",
    "\n",
    "<hr>\n",
    "\n",
    "## <h3 align=\"center\"> © IBM Corporation 2020. All rights reserved. <h3/>\n",
    "\n",
    "<p>\n"
   ]
  }
 ],
 "metadata": {
  "kernelspec": {
   "display_name": "Python",
   "language": "python",
   "name": "conda-env-python-py"
  },
  "language_info": {
   "codemirror_mode": {
    "name": "ipython",
    "version": 3
   },
   "file_extension": ".py",
   "mimetype": "text/x-python",
   "name": "python",
   "nbconvert_exporter": "python",
   "pygments_lexer": "ipython3",
   "version": "3.7.12"
  }
 },
 "nbformat": 4,
 "nbformat_minor": 4
}
