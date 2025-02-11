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
## identify which doctors has the most and least patients visit
  ## Problem if one doctor has significantly more visit than others , patient distribution is uneven
  ## which can lead to long wait time
   ## solution adjust visit scheduling so that high workload doctors can  get support
   ## introduce patients reassignment strategies for better balance

select 
d.doctor_id, d.name, count(visit_id) as total_visited
from visits v
join doctors d
on d.doctor_id = v.doctor_id
group by d.name , d.doctor_id
order by total_visited desc;

2.## determine peak visit day
 ## determine the busiest day of visits
 ## so we can optimise scheduling and improve  efficiency
 ## doctors should be available on Sundays and and Saturdays
 ## where visits drops on Thursdays, visits can be re-scheldued 
 
 Sql santax
 select 
 dayname(visit_date) as  Dates, count(*) as total_visit
  from visits
  group by dates
  order by total_visit desc;

3## find the revenue by departments
 ## problem- which department generate the most revenue
 ## solutions_highlights the department with the most revenue and allocate more budget to these  departments
 ## as they can generate more profit to the company
 ## improve more marketing for under performing departments.

 select
 d.department,d.name, round(sum(treatment_cost),2) as sum_billing
  from visits v
  join doctors d
  on v.doctor_id = d.doctor_id
  group by d.department,d.name
  order by  sum_billing desc
  limit 5;

4## whats the age distribution of patients
  ## what age groups visits the hospitals more
 ## adults care  service is high in demand  and wellness program should be promoted to help the young adults

    select  
   case 
   when  age between 0 and 12 then '0-12 (chlidren)'
   when age between 13 and 18 then '13-18 (teenagers' 
   when age between 19 and  35 then '19-35 ( young_adults)'
   when age between 36 and 60 then '36-60 (mid_adults)'
   else '60+(seniors)'
   end as age_group,
   count(patient_id) as total_patients
   from patients
   group by age_group
   order by  total_patients desc;

5 ## find patients who have not visited the doctor in over a year
  ##solutions set up  a reminder sms or email to inactive patients

   select  p.name, max(v.visit_date) as last_visit
   from visits v
   join patients p
   on v.patient_id = p.patient_id
   group by  p.name
   having datediff(curdate(), max(v.visit_date)) > 365;

6.   ## does doctors experience affect patients visits
   
   ## more experience doctors may attracts patients due to reputations
   ## and less experience doctors may have fewer patients  leading to under-utilizations
   ##?? does more experience lead to more patients, the answer is yes, judging form our visualization

7 ## which experience level is the most popular
 ## the seniors happens to be the most trusted ,the mid doctors made the most revenue showing the price is not equal to the work load
 ##hospital need to consider reducing the price in which the mids charge, new doctors needs more mentorships in order to gain more patients trust
 ## the seniors attracts the most patients judging by the total visit.

 select 
 case 
 when experience_years <5 then '0-4 years(new)'
 when experience_years between 5 and 10 then '5-10 years(mid)'
 else '10+ years(seniors)'
 end  as experience_group, 
 count(v.visit_id) as total_visit,
 round(avg(treatment_cost),2) as avg_treatment
  from doctors d
 join visits v
 on d.doctor_id = v.doctor_id
 group by experience_group
 order by total_visit desc;

 Updated my sql queeries to Tableau public for visualization of the insights and solutons to the problem solved

 visualization on tableau

 [view my tableau dashboard](https://public.tableau.com/app/profile/emmanuel.ugiagbe/viz/Doctorsperformanceproject/Dashboard1)
