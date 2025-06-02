# Greening Moonshot

<table data-header-hidden><thead><tr><th width="289"></th><th></th></tr></thead><tbody><tr><td>Data Owner</td><td>Anne Fernqvist (<a href="mailto:anne.fernqvist@undp.org">anne.fernqvist@undp.org</a>)</td></tr><tr><td>Availability in Data Warehouse</td><td>Available</td></tr><tr><td>Data Refresh Rate</td><td>Daily</td></tr><tr><td>Accountability Weighted Scoring</td><td>30%</td></tr></tbody></table>

## Introduction

[The UNDP Environmental Management Tool (EMT)](https://undpspowa03.azurewebsites.net/EMT/Pages/welcome?SPHostUrl=https%3a%2f%2fundp.sharepoint.com%2fteams%2fEMT&code=1.AQwAXtvls0QpN0iZ9XSIrOVDGZ4L1m_NfkFHs38MqnsFLB0MAM8MAA.AgABBAIAAABVrSpeuWamRam2jAF1XRQEAwDs_wUA9P9-N5xzDWXUEDkmSu_LDveIUPZkTqCUOn8JRlVmsr7HEnYCmcJIFcY-l7JjFfQA0i57P26qpCIjunz7Gj4K-SnaqpvDsYJVXcTwuh3gpRPOnkA33ygyPbZwGk64PGTp11P3MDtnJtZM1TLxTSvIoiMnAPMko_5oIBeUEFQr6TTIpiMA-QD2hM9Ao5LjOHKIWdvJXMVnZ3OTJcuuYmJ4NH9ZALza6ixPaXWn7h-36xmePHp7riiXTK0h5VSfAf-dzQEH7fGmyxI7miyAFbrJT19zP7rWIOR6Z2rtoVJaH5B5K51NX8FLCrch739dkp-_N81VOGMayrLq3CJ--HCsRQSqv18VJRnr5uwmx2o_WgS31iKp_O8lhMqk2_NakZhbZXpy2pStcF-0lEmDW-PkTTCo6ef6Io1ZA7sQR8yYivtEREcJRyJf1aBOmxuRS2jlPuxkhaUDk2yzem81b3F-e8pt8R1-yRcS2MSybOI1BGW13wp0woLLsw-mB82z6Dz94Gt1Ftp1PyN9TrdB4HQ7-buHn0sh0zdri1IKWCFfmBZYwtleAc8Rbh-I7CjdTWjiJDzIOH8vmPMw7tby6OiIAc2k-D9aVzWPsoJE_ywKRuQRsnOl4H82M1CMZrThr6CI1NtZOD7Y-viVGkdp_jDdeDtR96Ya7STSlpiTHiFM7iPKcTMWKj6gPYr9lRgzIAN5cHx-1a00rvNeTMojlNXL-odI9SuI369hW1lBr6ZXh7fK4q7LjfvS9JW0iiTSGB0DdvhOQNceLqPYqyk2_XiRtYTDgg&session_state=003f5ad9-a463-fd2a-9022-05785f3f80ed) methodology follows international standards like the GHG (Greenhouse Gas) Protocol to measure UNDP's carbon footprint across facilities, vehicles, and travel. The assessment scope includes emissions from activities paid for and controlled by UNDP like office utilities, vehicle fuels, staff travel, etc. It excludes project activities by external entities.UNDP facilities data covers main offices, and other offices are extrapolated based on the number of personnel. Shared offices are prorated based on UNDP's share.

The main categories of emissions are:

* Air travel
* Electricity
* Vehicle fuel use
* Refrigerants
* Heating
* Public transport

[You can read the full methodology for EMT here.](https://undp.sharepoint.com/sites/sustainable-undp/greening-operations/Shared%20Documents/Forms/AllItems.aspx?id=%2Fsites%2Fsustainable-undp%2Fgreening-operations%2FShared%20Documents%2FEMT%2FEMT%20methodology%2Epdf&parent=%2Fsites%2Fsustainable-undp%2Fgreening-operations%2FShared%20Documents%2FEMT)

While the data is available in the UNDP Data Warehouse, the data is taken from the EMT Dashboard (i.e. PowerBI) because there are custom business rules applied on top of the raw data, and we do not want to have to update the Performance App each time the business rules change. Therefore, the EMT Dashboard hold the master business rules for the Greening Moonshot reporting.


## Organisational Objective

The Greening Moonshot aims to reduce UNDP’s total carbon emissions by 50% by 2030 compared to 2018. This requires reducing the three main categories of Facility Electricity, Vehicle Fuels, and Air Travel by 55%.

## Data

The data for the current year is a mix of actuals and projected:

* **Actuals:** This is the travel emissions data (year-to-date)
* **Projected:** Everything else, including the remainder of the travel emissions data.&#x20;

{% hint style="info" %}
The projections are based on the last reporting year.&#x20;
{% endhint %}

The data export contains the following columns:

1. **Report\_Title\_Office**: This column contains the title of the report and the name of the office for which the data is being reported.
2. **year**: This column indicates the year in which the data was reported.
3. **bureau**: This column specifies the bureau within UNDP that the office belongs to.&#x20;
4. **category**: This column denotes the category of emissions or activity being reported such as air travel, electricity, heating, public transport, refrigerants, and vehicle fuel use.
5. **amt**: This column represents the amount of emissions or activity measured in terms of CO2 equivalent (tCO2e) for emissions.
6. **office\_facility\_id**: This column provides a unique identifier for the office facility.
7. **office\_name**: This column contains the name of the office.
8. **office\_unit**: This column lists the unit or division within the office.
9. **property\_address**: This column provides the address of the office facility.


## Data Export

{% hint style="danger" %}
This has not yet been defined.
{% endhint %}

## Calculation of Scoring

To track annual progress towards the 2030 target, a linear reduction trendline is plotted from the 2018 baseline to the 2030 goal of 50% reduction:

<figure><img src="../../.gitbook/assets/UNDP Greening Moonshot Trendline.png" alt=""><figcaption><p>50% linear reduction trendline from 2018 baseline to 2030.</p></figcaption></figure>

Each year, the maximum allowed carbon footprint level will be identified based on this linear reduction trendline. If the total carbon footprint is below this trendline-based maximum level in any given year, then the full score of 100 points will be awarded.

However, for every 1% that the actual annual total carbon emissions exceeds the maximum level allotted for that year as per the linear reduction trendline, 2 points will be deducted from the total possible score of 100.

We can provide an example for 2022:

* To stay within the trendline for the 2030 target, the 2022 target was a maximum of 52,184 tCO2e.
* The actual 2022 carbon footprint was 52,535 tCO2e
* So the actual emissions were 52,535 - 52,184 = 351 tCO2e higher than the trendline maximum
* 351 tCO2e is 0.67% higher than the trendline maximum (351/52,184 = 0.0067 i.e. 0.67%)
* As per the methodology, for every 1% above the maximum, 2 points are deducted
* Therefore, the score would be:
  * 100 points (max)
  * 0.67% above the maximum
  * 0.67 rounded up is 1%
  * 2 points deducted for being 1% above the maximum
  * So the total score is 100 - 2 = 98 points

## Traffic Light System

| Traffic Light | Score |
| ------------- | ----- |
| Green         | 100+  |
| Yellow        | 90+   |
| Red           | <90   |
