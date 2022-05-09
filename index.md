# Welcome to Cast - Away - Ballot!
##  <font color='lightseagreen'>Introduction and Motivation</font>
![Cast Away Ballot Logo](/docs/assets/images/cast-away-ballot-logo.png)
Casting a ballot in an election should be as effortless as possible. Cast-away-ballots are ballots that are stranded due to access times and/or wait times at the nearest polling station. 

In March 25th, 2021, The State of Georgia passed the Election Integrity Act. As a part of this law, previously used mobile voting buses are restricted and absentee ballot request and delivery periods are shortened. These changes may induce more demand for in-person voting on election day.

The objective of this project is to look at Georgia Census block groups find:

1. Which population groups in Georgia have more **in-person voting time burden** than others?
2. Where can mobile bus voting sites or new polling stations be used to alleviate travel and waiting times?

Voting Time Burden is defined as:

Voting Time Burden = Travel Time to Polling Station (Round trip) + Time Voting at Polling Station

*Based on a similar study conducted by UC Berkeley Professor Daniel Chatman for Travis County, TX.*

##  <font color='lightseagreen'>Summary of Findings</font>
1. In a K-means clustering analysis, High income block group clusters having a voting burden of nearly 10 minutes less than other block groups. Total voting time burden does not vary drastically from 43 minutes for low to middle income block group clusters.

2. Voting time burden can be plotted to identify areas with potential voter equity issues. After an investigation into real-life geospatial conditions of "high time burden" areas, mobile voting or additional polling locations should be considered

##  <font color='lightseagreen'>Aknowledgements</font>
Thank you to Elly Wanyonyi, Cade Luongo, Mihir Thakar for laying the foundations of this project. This project is an extension of work done with Elly, Cade, Mihir in the class CE263N at UC Berkeley advised by Professor Marta Gonzalez.

Thank you to Professor Daniel Chatman for discussing his work in Travis County, TX and providing guidance on the methodology of this project.

Thank you to Stephen Fowler of Georgia Public Broadcasting for generously providing Georgia polling station location information and observed voters/hr.

Thank you to Steven Davenport, PhD and the Center for New Data for generously providing de-identified device data for estimated wait times for polling stations in Georgia.

##  <font color='lightseagreen'>Data and Methodology</font>
### Data
There are three primary datasets used in this analysis.

#### **2010 GA Census Block Group**

![Census Logo](/docs/assets/images/Census Data Image.png)

Population centroids, race, ethnicity, income, car ownership of block groups was analyzed in this project. Data that is only avaliable on a tract-level was projected onto the block group level.

#### **2020 GA Polling Locations**

![Polling Locations](/docs/assets/images/Polling Locations Image.png)

Courtesy of Stephen Fowler from GPB. Includes addresses, precinct id's, and contacts for polling locations in the state of Georgia for voting in 2020.

#### **2020 Nov Election Poll Smartphone Wait Times**

![Smartphone Locations](/docs/assets/images/Smartphone Location Image.png)

Courtesy of Steven Davenport, PhD and Center for New Data. Deidentified device wait times at polling addresses on November 3rd, 2020 in Georgia. Estimated times are calculated using methods in Chen. et. al. 

### Methodology
#### Polling Station Wait Times
First the wait time at each polling station is determined. Using the deidentified device id dataset, a 90th percentile is determined for each polling station in which data is avaliable. 

There are about 2300 polling stations in Georgia, but smartphone wait times exists for 1201 polling stations. To address this limitation, we assume that nearby polling stations share similar wait time. That is, we spatially assign 90th percentile wait times of polling stations without smartphone data by pulling from the nearest polling station with smartphone wait data. 

![Polling Station Data Map](/docs/assets/images/Polling wait time figure.png)

#### Travel Times
Travel times are determined by plotting the population centroid of GA census block groups and polling stations. Each block group is assigned to their nearest polling station and a Google Maps API is used to generate travel times during the morning rush hour. Travel time is weighted by census car ownership. That is, block groups with higher rates of car ownership will have travel times weighted more towards car.

![BlockGroup to Poll Assignment](/docs/assets/images/blockgroup to poll.png)

#### Combining Travel Time and Wait times

Travel times and wait times are combined for a rich dataset of block groups with demographic data and voting times!

![Combining Travel Time and Wait Times](/docs/assets/images/combiningTTandWait.png)


##  <font color='lightseagreen'>Results</font>
First a k-means clustering analysis was completed to view block groups with similar demographic and voting time burden characteristics. Five clusters was used in this analysis and ordered by voting time burden. Median statistics are shown below.

![Kmeans Results](/docs/assets/images/Kmeans results.png)
It is seen in the clustering analysis that the two lowest burden clusters generally have the highest median income. Interestingly, the middle, high, and highest burden clusters have similar voting time burdens. This indicates that most block groups exhibit similar voting times of around 43 minutes, but higher income groups have notably less voting time burden.

Although it is interesting to plot block group clusters, it is more useful and informative to look at a choropleth of voting time burden:

![Results](/docs/assets/images/Results 1.png)

With this plot, it is easy to identify areas with potential voter equity issues. To effectively and strategically use mobile voting buses or new polling sites, red and orange locations should be considered first. For example:

![Proposing Polling Locations](/docs/assets/images/propose poll.png)
##  <font color='lightseagreen'>Conclusions</font>
Quantifying voting time burden is useful to effectively address voter equity issues. When certain population groups have a higher voting time burden than others, this can disproportionately cause some groups to have lower turnout than others.

High income block group clusters having a voting burden of nearly 10 minutes less than other block groups. Total voting time burden does not vary drastically from 43 minutes for low to middle income block group clusters.

##  <font color='lightseagreen'>References</font>

**Travel Burdens for Voters to Access a Ballot Drop Box** (Travis County Motion for Relief)
Dr. Daniel Chatman
https://www.brennancenter.org/sites/default/files/2020-10/Appellees%27%20Emergency%20Motion%20for%20Relief%20%26%20Exhibits.pdf

**Racial Disparities in Voting Wait Times: Evidence from Smartphone Data**
Chen, et al.
https://www.nber.org/system/files/working_papers/w26487/w26487.pdf


**Access to Polls: Assessment of Early Vote Wait Times in Georgia’s General Election and Potential Effects of Voting Restrictions in Runoff**
Center for New Data
https://www.newdata.org/ga-analysis

**Here’s What The Data Shows About Polling Places, Lines In Georgia's Primary**
Stephen Fowler
https://www.gpb.org/news/2020/07/17/heres-what-the-data-shows-about-polling-places-lines-in-georgias-primary

##  <font color='lightseagreen'>Contact</font>
Questions? Contact: wangjason98@gmail.com





