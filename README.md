# projectwork
Project 2

yammer_users ---give me user level data
yammer_event--give me event level data
yammer _emails--give me email level data

/** question 1 -

select
   EXTRACT (week from occurred_at) AS weeknum,
    COUNT(DISTINCT user_id)
from 
    tutorial.yammer_events a
GROUP BY
  weeknum
  
/** question 2

/** yammer_users --> give me user lev
SELECT year, weeknum, num_active_user, SUM(num_active_user)OVER(ORDER BY year,weeknum ROWS BETWEEN UNBOUNDED PRECEDING AND CURRENT ROW) AS cum_active_users FROM ( SELECT EXTRACT(year from a.activated_at) AS year, EXTRACT(week from a.activated_at) AS weeknum, COUNT(DISTINCT user_id) AS num_active_user FROM tutorial.yammer_users a WHERE state='active' GROUP BY year, weeknum ORDER BY year, weeknum ) a


##question 3-

SELECT EXTRACT(year FROM occurred_at) AS year, EXTRACT(week from occurred_at) AS week, device, COUNT(distinct user_id) FROM tutorial.yammer_events WHERE event_type ='engagement' GROUP BY 1,2,3 ORDER by 1,2,3

## QUESTION 4 

SELECT 100.0 *SUM(CASE WHEN email_cat = 'email_open' THEN 1 ELSE 0 END)/SUM(CASE WHEN email_cat = 'email_sent' THEN 1 ELSE 0 END) AS email_open_rate, 100.0 *SUM(CASE WHEN email_cat = 'email_clicked' THEN 1 ELSE 0 END)/SUM(CASE WHEN email_cat = 'email_sent' THEN 1 ELSE 0 END) AS email_clicked_rate FROM ( SELECT *, CASE WHEN action IN ('sent_weekly_digest', 'sent_reengagement_email') THEN 'email_sent' WHEN action IN ('email_open') THEN 'email_open' WHEN action in ('email_clickthrough') THEN 'email_clicked' END AS email_cat FROM tutorial.yammer_emails ) a

