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
 select 
 dayname(visit_date) as  Dates, count(*) as total_visit
  from visits
  group by dates
  order by total_visit desc;

3## find the revenue by departments
 ## problem- which department generate the most revenue
   select
 d.department, round(sum(treatment_cost),2) as sum_billing
  from visits v
  join doctors d
  on v.doctor_id = d.doctor_id
  group by d.department
  order by  sum_billing desc
  limit 5;

4## whats the age distribution of patients
  ## what age groups visits the hospitals more
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

 [view my tableau dashboard](https://public.tableau.com/app/profile/emmanuel.ugiagbe/viz/Doctorsperformanceproject101/Dashboard1)

 RECOMENDATIONS

Adjust visit scheduling so that high workload doctors can  get support and  introduce patients reassignment strategies for better work balance to reduce long wait time

Doctors should be made readily  available on Sundays and and Saturdays as weekends appears to be the busiest days of visit.
 where visits drops on Thursdays, visits can be re-scheldued to improve  visit efficiency

General medicine appears to be the department  with the most revenue, allocation of more budget to this department should be considerd, the pediatric should also be a department the hospital look deep into as it appears to generate a substential ammount of revenue as they generate more profits also improve more marketing for under performing departments.

The seniors happens to be the groups that visits the hospital most frequently therefore adult care  service is high in demand and should be paid good attention to, wellness program should be promoted to help the young adults keep fit and understand how to care for the body

The gospital should endeavour to  set up  a reminder sms or email to inactive patients

 The  seniors happens to be the most trusted ,the mid doctors made the most revenue showing the price is not equal to the workload
 Hospital need to consider reducing the price in which the mids charge and crate more intership programs for the new doctors overseen by the seniors 
Patients value Experience






