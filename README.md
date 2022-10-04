# Capstone-project-1--Hotel-booking-analysis
This is the first capstone project about the Hotel booking analysis.

# Capstone project Hotel booking analysis

Hotel industry is crucial part of the service industry as well as tourism industry. Managing the available resources would be challenge for them .So we want insure that they could use their resources in better way as well as avoid the waste of resources .This dataset could help them to understand the bookings and their different aspects of it as well as choices of customers.

Our experiment with this data is to analyze the data and give valuable insights for the hotels industry. We have organized the data in best possible way to get helpful insights from it. 



## Data set information 


•	hotel: Name of hotel ( City or Resort)

•	is_canceled: Whether the booking is canceled or not (0 for no canceled and 1 for canceled)

•	lead_time: time (in days) between booking transaction and actual arrival.

•	arrival_date_year: Year of arrival

•	arrival_date_month: month of arrival

•	arrival_date_week_number: week number of arrival date.

•	arrival_date_day_of_month: Day of month of arrival date

•	stays_in_weekend_nights: No. of weekend nights spent in a hotel

•	stays_in_week_nights: No. of weeknights spent in a hotel

•	adults: No. of adults in single booking record.

•	children: No. of children in single booking record.

•	babies: No. of babies in single booking record. 

•	meal: Type of meal chosen 

•	country: Country of origin of customers (as mentioned by them)

•	market_segment: What segment via booking was made and for what purpose.

•	distribution_channel: Via which medium booking was made.

•	is_repeated_guest: Whether the customer has made any booking before(0 for No and 1 for 

	Yes)
•	previous_cancellations: No. of previous canceled bookings.

•	previous_bookings_not_canceled: No. of previous non-canceled bookings.

•	reserved_room_type: Room type reserved by a customer.

•	assigned_room_type: Room type assigned to the customer.

•	booking_changes: No. of booking changes done by customers

•	deposit_type: Type of deposit at the time of making a booking (No deposit/ Refundable/ No refund)

•	agent: Id of agent for booking

•	company: Id of the company making a booking

•	days_in_waiting_list: No. of days on waiting list.

•	customer_type: Type of customer(Transient, Group, etc.)
•	adr: Average Daily rate.

•	required_car_parking_spaces: No. of car parking asked in booking

•	total_of_special_requests: total no. of special request.

•	reservation_status: Whether a customer has checked out or canceled,or not showed 

•	reservation_status_date: Date of making reservation status.

## Deployment

To deploy this project run

```bash
  ## <b> Have you ever wondered when the best time of year to book a hotel room is? Or the optimal length of stay in order to get the best daily rate? What if you wanted to predict whether or not a hotel was likely to receive a disproportionately high number of special requests? This hotel booking dataset can help you explore those questions!

## <b>This data set contains booking information for a city hotel and a resort hotel, and includes information such as when the booking was made, length of stay, the number of adults, children, and/or babies, and the number of available parking spaces, among other things. All personally identifying information has been removed from the data. </b>

## <b> Explore and analyze the data to discover important factors that govern the bookings. </b>
# ***Capstone project: Hotel Booking Analysis***
#Importing library for Data Analysis
import pandas as pd
import numpy as np
import seaborn as sns
import matplotlib.pyplot as plt
%matplotlib inline

# Mounting drive to colab notebook
from google.colab import drive
drive.mount('/content/drive')

# Reading the file in pandas 
data=("/content/drive/MyDrive/Copy of Hotel Bookings (1).csv")

data=pd.read_csv(data)

#checking the data and columns and information store in columns  
data.head(5)

# We have check rows and columns in data
data.shape

# We have to check if there are any NaN values present and how to we can replace that.
data.isnull().sum()

# we can see that there is lot of NaN values in company column  so we can drop that
data=data.drop(['company'], axis=1) 
We can see that NaN values can cause damage to analysis ,we have to replace them best possible way.
data.shape
data.children.describe()

# we have seen that the children column has min value equal to 0(zero) so it is assumed to be good choice we can replace it with zero
data["children"]=data['children'].fillna(0)
data.isnull().sum()

#As there many places where country is not specified so we can replace that with anonymous
data['country']=data[["country"]].fillna("Anonymous")
data.isnull().sum()
data["agent"].describe()

# Here we can see that values of agent , as we dont know the agents related to hotels we can replace it with zero
data['agent']=data['agent'].fillna(0)
We can see that Agents and their data minumum number of agents is and maximum no of agents are 535 and as well the average number of agents are 86 to this hotels.

#Check whether there any NaN values in data
data.isnull().sum()

# let's see first what type hotel are there in data?
# How much the percentage of hotel in data?
data.hotel.unique()
We found that there are two types hotels and their data is given in file 
data.hotel.value_counts()
labels=data['hotel'].value_counts().index.tolist()
labels
value_data=data['hotel'].value_counts().tolist()
value_data

**Observation:1**
Here we are trying to show the % of bookings happend related to hotels and we found that there are there 66.6 % hotels are city hotels and 33.4 % hotels are Resort hotels.

plt.figure(figsize=(10,7))
plt.pie(value_data,labels=labels,autopct='%1.1f%%')
plt.show
plt.title('City hotel and Resort hotel  bookings data')
data.lead_time.describe()

**Observation:2**
 Lead time is duration between the time of booking and actual check in hotel.

so found that the 'mean' lead time' of hotel is 104 days and the 'min' lead time is 0 days and as well as 'maximum' lead time is 737 days 

# lead time = time between reservation and actual check in
booking=data.is_canceled.value_counts()
booking
data['is_canceled']=data.is_canceled.replace([0,1],['booked','canceled'])
booking_info=data.is_canceled.value_counts().index.tolist()
booking_info_nums=data.is_canceled.value_counts().tolist()
booking_data={'booking_info':booking_info,"booking_info_nums":booking_info_nums}
data.is_canceled.value_counts(normalize=True)

**Observation:3**
62% people booked and checked in hotel 
38% people booked and didn't checked in hotel

pd.DataFrame(booking_data)
plt.figure(figsize=(10,7))
plt.bar(booking_info, booking_info_nums, color ='maroon',
        width = 0.4)
 
plt.xlabel("booking_info")
plt.ylabel("No of bookings")
plt.title(" Information about booking and cancellation")
plt.show()

data_year=data.arrival_date_year.unique()
data_year
data.arrival_date_year.value_counts()

year_list=data.arrival_date_year.value_counts().index.tolist()
print(year_list)

year_bookings=data.arrival_date_year.value_counts().tolist()
print(year_bookings)

plt.figure(figsize = (10, 5))
plt.bar(year_list,year_bookings)
plt.xlabel("year")
plt.ylabel("No. of bookings")
plt.title("Year vs No. of bookings")
plt.show()

**Observation:4**
In above plot we can see that year and their corresponding bookings .
*  most bookings happend during the year 2016
* Then after that 2017 and followed by 2015

plt.subplots(figsize=(7,5))
sns.countplot(x='arrival_date_year', hue='hotel',  data=data);
plt.title('Hotels bookings comparison with year')
plt.ylabel('No of bookings')
plt.xlabel(' Year of bookings')

**Observation:5**
We can see from above graph that the performace of hotel respective to their year and bookings
*   By looking at graphs we can conclude that bookings were more happened in city hotels than resort hotels .


plt.subplots(figsize=(7,5))
sns.countplot(x='lead_time', hue='hotel',  data=data);
plt.title(' lead time comparison with hotels ')
plt.xlabel ('lead time of hotels')
plt.ylabel(' lead time occurance') 

**Observation:6**
we have compare the lead time data with the hotels and we found that the lead time is more in city hotel and less in resort hotels .
data.lead_time.describe()

plt.subplots(figsize=(15,5))
sns.countplot(x='arrival_date_month', hue='hotel',  data=data);
plt.title('comparing hotel bookings with months in Year')
plt.xlabel(' months of Year')
plt.ylabel('No of bookings')

**Observation:7**
In above graph we can take few things that are ;
*   August month is amongs busiest amongs rest of the month both in city and resort hotels.
*   while january months is lowest visted by travles to city and Resort hotel.

*   We can see that certain pattern of bookings happens increasing towards from the january to august 
*   and after august months it start to fall again in booking to january




plt.subplots(figsize=(15,5))
sns.countplot(x='arrival_date_day_of_month', hue='hotel',  data=data);
plt.title ('comparison with arrival date against bookings')
plt.ylabel('No of bookings')
plt.xlabel('date of months')

**Observation:8**
* From above graph we can noticed the pattern of bookings
related month date we found that hotel booking rise certainly after 3-4 days between and we can say that mostly at weekends .

plt.subplots(figsize=(10,5))
sns.countplot(x='stays_in_weekend_nights', hue='hotel',  data=data);
plt.title(' weekend night stays in hotels')
plt.xlabel('weekends  nights stays')
plt.ylabel('No of bookings')

**Observation:9**
*  People who booked hotels for less than 2 at weekends they mostly stays in city hotel 
* people with more than 2 days mostly choose to stay at resort  hotel for weekends . 



plt.subplots(figsize=(10,5))
sns.countplot(x='is_canceled', hue='hotel',  data=data);

**Observation:10**
*   In terms of booking % people choose city hotel so booking rate are  more in city hotel 
*  And cancelation rate is also more in city hotels


plt.subplots(figsize=(10,5))
sns.countplot(x='meal', hue='hotel',  data=data);
plt.title('Meal comparison with hotels')

**Observation:11**
*   BB (bed n breakfast) meal type prefered mostly in city hotel than Resort hotel in rest of all meal type 
* Next meal mostly prefered is **HB** (half board = breakfast+ dinner normally) and followed by **SC**( self catering) 

data.arrival_date_month.value_counts(normalize=True).plot(kind='line')

**Observation:12**
* Simple observation from above graph that booking trends related to hotel, in August it reaches to its peak and and december it is lowest. 
months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']

months_data=data.arrival_date_month.value_counts().reindex(months)
months_data
month_list=months_data.index
month_list
month_percentage=months_data/months_data.sum()*100
month_percentage.values

plt.figure(figsize=(15,5))
sns.lineplot(month_percentage.index,month_percentage.values, data=months_data)
plt.show()

**Observation:13**
* This graph is better showing the bookig trends

city_hotel_data=data.loc[data.hotel=='City Hotel' ]
city_hotel_data
sorted_months =data.loc[data.hotel=='City Hotel' ,'arrival_date_month'].value_counts().reindex(months)

x1 = sorted_months.index
y1 = sorted_months/sorted_months.sum()*100



## Select only Resort Hotel
sorted_months =data.loc[data.hotel=='Resort Hotel' ,'arrival_date_month'].value_counts().reindex(months)

x2 = sorted_months.index
y2 = sorted_months/sorted_months.sum()*100
plt.figure(figsize=(15,5))
ax = plt.subplots(figsize=(15,6))
sns.lineplot(x1, y1.values, label='City Hotel')
sns.lineplot(x1, y2.values, label='Resort Hotel')

plt.show()
plt.title('comparison of months with No of bookings')
plt.xlabel('months of year')
plt.ylabel('percentage of bookings')

Observation:14
* Its seen that booking of the both hotel rise in august 
* its also seen that the people more likely choosen Resort hotels than city hotel in August.

travel_data=data.loc[data.is_canceled=='booked','country'].value_counts()
travel_data_top=travel_data.head(10)
travel_data_top
travel_data
plt.bar(travel_data_top.index,travel_data_top.values,)
plt.ylabel("travelers country booking")
plt.xlabel("Top countries")
plt.title("Top traveling countries")

**Observation:15**
* Here we can see that the country have more booking is **Portugal**,followed by **Great britain** , **France** and so on spain,Germany,Ireland,Italy,belgium,Netherland,USA.
travel_data_top_frame=pd.DataFrame(travel_data_top)
travel_data_top_frame

plt.subplots(figsize=(10,5))
sns.countplot(x='country', hue='hotel',  data=data,order=data.country.value_counts().iloc[:10].index);
plt.title(' country and their booking choices')
plt.xlabel('countries')
plt.ylabel(' no of bookings')

Observation:16
* Its shown from above bars that the people from Portugal likely to stay more in *City hotel* and opposite to that people of **great britain** is more likely to stay in *Resort hotel*

plt.subplots(figsize=(10,5))
sns.countplot(x='reserved_room_type', hue='hotel',  data=data);
plt.title(' Rooms choices and hotels')
plt.xlabel(" Room types")
plt.ylabel(' No of bookings')

**Observation:17**
* We can see that most of the customers choose the room type of A and and more likely in city hotels 
* Followed by the D,E F type of rooms

plt.subplots(figsize=(10,5))
sns.countplot(x='reserved_room_type', hue='hotel',  data=data,order=data.reserved_room_type.value_counts().iloc[:10].index);

plt.subplots(figsize=(10,5))
sns.countplot(x='distribution_channel', hue='hotel',  data=data);
plt.title (' Distribution channel comparison')
plt.ylabel('No of bookings')
plt.xlabel('Distribution channels')

**Observation:18**
* Here , We can see that the TA/TO (travel agents/ tour operators) is TOP distribution channel amongs all and followed by the direct bookig and corporate bookings.

plt.subplots(figsize=(10,5))
sns.countplot(x='stays_in_week_nights', hue='hotel',  data=data,order=data.stays_in_week_nights.value_counts().iloc[:10].index);

**Observation:19**
* we can see that people with less than 3 nights are more likely stay in city hotels .
* we also see that people with more than 3 night stays are more like stay at Resort hotels

plt.subplots(figsize=(10,5))
sns.countplot(x='customer_type', hue='hotel',  data=data);
plt.title('type of customers vs hotels')
plt.xlabel('customer type')
plt.ylabel('No of bookings')

**Observation:20**
* we can see that the most of the customers in city and Resort hotel are from transient type and then followed by the transient party and contract type of customer.

plt.subplots(figsize=(10,5))
sns.countplot(x='days_in_waiting_list', hue='arrival_date_month',  data=data,order=data.days_in_waiting_list.value_counts().iloc[:10].index);
plt.title(' waiting days comparison with the months ')
plt.xlabel('waitings days')
plt.ylabel ('no of occurance of waiting days')

**Observation:21**
* we can see that the waiting days in list is more in *August  and July* and less in *December* and *january*

plt.subplots(figsize=(10,5))
sns.countplot(x='days_in_waiting_list', hue='hotel',  data=data,order=data.days_in_waiting_list.value_counts().iloc[:10].index);

Observation:22
* Waiting days are more in city hotels than Resort hotels.
booking_data=data.loc[data.is_canceled=='booked']
booking_data['assigned_same_rooms']=booking_data.loc[ booking_data['reserved_room_type'] == booking_data['assigned_room_type'] ] = 'assigned_same'
plt.subplots(figsize=(10,5))
sns.countplot(x='assigned_same_rooms', hue='hotel',  data=booking_data);

Observation:23
* We can see that chances of getting assigned same room is more in Resort hotel than city hotels.
data.adults.describe()
plt.subplots(figsize=(10,5))
sns.countplot(x='adults', hue='hotel',  data=data);
plt.xlabel('No of adults')
plt.ylabel(' No of bookings')
plt.title('comparison with the number of adults')

**Observation:24**
* Adults are more likely to stay in city hotels than the Resort hotels.
single  = booking_data[(booking_data.adults==1) & (booking_data.children==0) & (booking_data.babies==0)]
plt.subplots(figsize=(10,5))
sns.countplot(x='adults', hue='hotel',  data=single);
plt.xlabel('single consumer')
Observation:25

* single customer bookings are more in Resort hotel than city hotels.
couple  = booking_data[(booking_data.adults==2) & (booking_data.children==0) & (booking_data.babies==0)]
plt.subplots(figsize=(10,5))
sns.countplot(x='adults', hue='hotel',  data=couple,);
plt.xlabel('couple data')
plt.ylabel('couple bookings')
plt.title("couples and their hotel choices")
Observation:26

* couples are more likely to stay in Resort hotel than the city hotels.
Family_or_friends  = booking_data[(booking_data.adults==2) + (booking_data.children==1) & (booking_data.babies==2)]
plt.subplots(figsize=(10,5))
sns.countplot(x='adults', hue='hotel',  data=Family_or_friends);
plt.xlabel('family and friends data')
plt.ylabel('family and friends bookings')
plt.title("family and friends and their hotel choices")

Observation:27
*  Family and Friends type of customer choosen to Resort hotels than the city hotels.

**Conclusion:**

*  66.4 % hotels are City hotels and 33.6 % are Resort Hotels.
*  62% is booking rate and 38% are cancelation rate
* city hotels have more cancelation rate and vice versa.
* Lead time is more in city hotels than the Resort hotels.
* August is busiest month and December is least busiest months.
* BB ( bed and breakfast) mostly prefered meal type in city and Resort hotels.
*Portugal, Great britain ,france are top three countries with most number of bookings.
*TA/TO is top performing distribution channel amongs rest of all.
*Both hotels have mostly transient type of customers.
* Chances of getting same assigned room is more in Resort hotel than city hotel.
*Bookings are mostly done by couples followed by family and friends and thereafter sigles.




```


## Acknowledgements

 - Hands on practise on large dataset
 - Explored differnt python library 
 - Dealing with the handling of null values
 - Data visualization
 - plotting of graphs
 - Data cleaning



## Challenges

- Handling of data
- cleaning of null values
- feature making
- writing data summery

## Reference
- www.geeksforgeeks.com
- www.medium.com
- www.web3school.com
