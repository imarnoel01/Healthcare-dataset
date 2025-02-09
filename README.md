# Healthcare-dataset
 Highlights  the health care sector for overloaded doctors, allocation of more revenue to high performing department and implore better marketing for under performing departments, peak visit day, age distribution. Of patient How doctors experiences affect patients visits, which experience level is the most popular..
Data set gotten from Kaggle.com 
healthcare 

Cleaned this data form SQL
Rearranging the phone column and removing extra characters to give accurate phone numbers  using the replace function and then using concat to join the cleaned up numbers together
Further checked for duplicate and found 6 duplicated columns, I used the windows function to get the columns and then deleted it form the table 
Checked for missing values and null but all seems to be intact..
Then I prepared the data for future exploratory analysis 


Insights / problems and solutions 
1.## most frequently visited doctor
## identifies which doctor handles the most patients

2.## determine peak visit day
 ## determine the busiest day of visits
 ## so we can optimise scheduling and improve  efficiency
 ## doctors should be available on Sundays and and Saturdays
 ## where visits drops on Thursdays, visits can be re-scheldued 

3##find the revenue by departments
 ##problem- which department generate the most revenue
 ##solutions_highlights the department with the most revenue and allocate more budget to these  departments
 ##as they can generate more profit to the company
 ##improve more marketing for under performing departments.

4## whats the age distribution of patients
  ## what age groups visits the hospitals more
 ##adults care  service is high in demand  and wellness program should be promoted to help the young adults

5##find which department serve different age groups

6 ## identify which doctors has the most and least patients visit
  ## Problem if one doctor has significantly more visit than others , patient distribution is uneven
  ## which can lead to long wait time
   ##solution adjust visit scheduling so that high workload doctors can  get support
   ##introduce patients reassignment strategies for better balance

7 ## find patients who have not visited the doctor in over a year
  ##solutions set up  a reminder sms or email to inactive patients

8.   ## does doctors experience affect patients visits
   
   ## more experience doctors may attracts patients due to reputations
   ## and less experience doctors may have fewer patients  leading to under-utilizations
   
##?? does more experience lead to more patients

9## visits are evenly distributed ,the hospitals is managing the  patients well

10## which experience level is the most popular
 ## the seniors happens to be the most trusted ,the mid doctors made the most revenue showing the price is not equal to the work load
 ##hospital need to consider reducing the price in which the mids charge, new doctors needs more mentorships in order to gain more patients trust
 ## the seniors attracts the most patients judging by the total visit.

 Updated my sql queeries to Tableau public for visualization of the insights and solutons to the problem solved
