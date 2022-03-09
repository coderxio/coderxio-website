---
layout: post
title:  RIP SSMS, hello SQL notebooks
author: Dalton Fabian
description: Notebooks aren’t just for Python anymore.
image: /assets/images/not-how-this-works.jpg
date:   2021-05-23 06:00:00 -0600
categories: sql
tags: ssms azure data python notebooks ads
published: true
---

I work on a data science team for a large health system, which means I have a ton of data that I need to explore for new machine learning projects and clinical tools. SQL is the primary language used to work with data in relational databases from the electronic health record (EHR) and SQL Server Management Studio (SSMS) is a tool that a lot of programmers use to write SQL.

SSMS is a great tool for running successive queries but doesn’t make it easy to see the output of previous queries or reference previous results in new queries. I used SSMS as my own code editor until I went to a talk that introduced me to Azure Data Studio (ADS) and SQL notebooks. I was familiar with the concept of Jupyter notebooks since they are all the rage in data science and are used to help explain the data science process and share reproducible results in R or Python, two data science programming languages. The SQL notebooks feature along with other features like saved code snippets, multi-cursor support, and an integrated command line made the switch incredibly easy!

![Servers](/assets/images/servers.jpg)

*Where all the data sleep at night.*
{: .fs-2}

Notebooks help with exploratory work and sharing reproducible results because each code cell and output is saved and visible to anyone viewing the file as you can see in the image below, a redacted example of a query I mention below. This can help others see what steps you took in your analysis but it's also a great feature to be able to use as a reference yourself if code in later cells depends on the information you found earlier in your work. Notebooks are traditionally used in Python (Jupyter notebook) or R (R Markdown files/notebooks but even Jupyter notebooks support R notebooks) environments. Query languages like SQL also benefit from a notebook because a lot of SQL work (especially in data science) is exploratory. Not only will a SQL notebook help you explore and investigate your data, it can also leave a trace of the different steps you tried so you can review it with another person.

![SQL notebook example](/assets/images/ads.png)

*SQL notebook example: first query results on top, second query results on bottom. Also, dark mode by default ftw.*
{: .fs-2}

If notebooks already exist for other languages and are heavily used in R and Python, why not just do your exploration in R or Python notebooks? This answer is a pretty easy one - SQL is much faster to execute than R/Python and the vast majority of data that I work with day-in and day-out is in database tables, which requires SQL! Most of my work involves structured data, not data like images, videos, and Excel (which is structured to a degree but not represented in the same way as a database table). Using R and Python would also involve connecting to a SQL database and running SQL code to "download" the data so you might as well skip the extra steps that need to be done to connect to a database in R/Python and starting writing code quicker!

In this article, I'll share some specific examples of why I love ADS's SQL notebooks features and highlight times when they are helpful.

## Data exploration with SQL notebooks

The primary use case for SQL notebooks in ADS is when I am looking for data that I have never used before or am trying to remind myself how data is represented in database tables that I don't use very often. The notebook helps me to "track" my steps over time and refer back to specific codes or pieces of data.

For example, a few months ago I was trying to find how to get a list of all employees at my health system who were Care Managers at some point in their employment. This could include employees who were currently Care Managers as well as employees who used to be Care Managers but had since either left the organization or switched to a new role at the health system.

The first part of that list was easy to find (current Care Managers) because a certain table has the employee's info and their current work assignment. The table for historical jobs is laid out much differently, with all current and previous positions, instead of one row per employee. Armed with a list of employee names who were currently Care Managers and some who were formerly Care Managers, I searched the "employee information" table using a query like the one below. This was a table with the employee's name and employment dates, including their termination date if they have left the health system. I needed to do this because I needed their employee_id to find data about them later. In most database tables, each patient or person is identified by an ID, rather than their name.

The problem with that though was Care Management leaders knew the Care Managers by name and not employee ID because they were normal people and cared about personal relationships ;) I was able to use the SQL LIKE operator to accomplish this task because the employee information table is the one table with the employee name.

```sql
SELECT employee_name, employee_id
FROM jobs
WHERE employee_name LIKE '%last1, first1%'
   OR employee_name LIKE '%last2, first2%'
...
```

When I ran the above code in a SQL notebook, the output for the 5 or so employees I looked up will stay up on the screen. Normally in a tool like SSMS (a common tool for SQL), the next code I run would overwrite the results from above. Based on that, you might be thinking, "well, why not just have two editors open or take advantage of the side-by-side query windows that ADS or SSMS let you have open?" Personally, the notebooks work better so I can have the full SQL code available and not get cut off because the line was too long. The SQL notebook will also let you view the results of 3+ queries. The side-by-side editor windows can get far too cramped with 2 queries open at once, let alone 3 or more!

Next in my process, I wanted to take each employee_id and look up the job histories I mentioned before. Let's say two of the current/former Care Managers had IDs of "123" and "456". When exploring how the job history table worked, I would run a query like below.

```sql
SELECT *
FROM job_history
WHERE employee_id = '123'
```

When doing this in a notebook, the result of the query appeared on the page and kept the first query output on the screen also. The magic of this reveals itself when you are finished looking up employee_id "123" and want to look up employee_id "456". If I didn't use a notebook, I would have to go back and re-run the first query that I shared with you to find out the employee_id of the employee who was "456". I would have to run it again because employee_id's in real life are not nice, easy 3 digit codes so there would be no way that I would remember that the second Care Manager of interest's employee_id was "456". I would re-run the first query and then copy and paste "456" where "123" was in the second query. With a notebook, the output of the first query was still there so it was as easy as copy and pasting from the already visible output.

This process could carry out even further but I hope you've seen the benefit of a notebook for SQL when you're exploring new data. It will save you time by preventing you from having to re-run the same queries constantly.

## Troubleshooting with SQL notebooks

The other situation in which I find myself using SQL notebooks most often is when troubleshooting errors in the output of SQL queries or a database table that is already made. When we write and deploy SQL into our data pipeline for our machine learning work, sometimes weird results will pop up out of nowhere.

A common case of this happens when a table that is supposed to have one row per patient comes back with multiple rows per patient. This can throw off either our machine learning algorithm output or visualization that uses the table. A specific example that will come up is when we are trying to get the last appointment for someone or the next appointment. In our electronic health record (EHR), some patients will have two appointments at the exact same time in the same clinic which usually means that two healthcare professionals are assisting with the appointment or one is meant to see the patient right after the other. When we try to get the last or next appointment, if we're not careful, the two appointments at the same time will both be pulled in and the patient will have two rows in the data. The only difference in this end table is the columns of data for the last appointment which may include the provider's name and location; all other fields for the two rows of the patient will be the same.

When the above happens, it's never just one row affected and it could even be different data points that would be off for different patients. One patient might have two rows because of their next appointment, another might have two rows because of a recent discharge that was coded funny. If there's one thing I've learned, it's to make our SQL code robust to try to weed out these issues. To fix these problems, I'll often use a SQL notebook to look at the rows that had duplicates. The first step is to find those patients with multiple rows and get their patient ID or MRN by writing code like the block below.

```sql
SELECT patient_id, COUNT(*) 
FROM output_table 
GROUP BY patient_id 
HAVING COUNT(*) > 1
```

The output of this list will give me the list of patients I need to look at to find the issue. Again, with this being a SQL notebook, I only need to run the above code once and can use the output frequently. I might first take the patient from that query with an ID of "678" and look at their rows with the following code.

```sql
SELECT * FROM output_table WHERE patient_id = '678'
```

Then I could scroll horizontally until I find the differences between the rows. I can document that discrepancy but I'll also need to look at the other patients from the original query to see if they all suffer from the same issue. If I was using a regular query, I'd have to go back and run the COUNT(*) query again because the patient-specific query would have overwritten it on the screen. With the notebook, all I have to do is copy and paste the new patient ID from the first query output into the patient-specific query.

## Wrap Up

In this article, I hope that you've seen real-life use cases on when SQL notebooks can be handy to help you explore data you've never seen before as well as troubleshoot errors in your SQL output that cause duplication, among other things. If you want to try out these SQL notebooks, I'd recommend downloading Azure Data Studio since that's the only place that I know has them (would love other suggestions if you find other editors with them 🙂).

Happy coding!

---

**CodeRx** is a collective of pharmacists and other healthcare professionals that have an interest, skill set, or passion in coding, data, or tech. If you're interested in learning more, follow along at [CodeRx.io](https://coderx.io/), check out our [GitHub repo](https://github.com/coderxio/dailymed-api), or join our [Slack channel](https://join.slack.com/t/coderx/shared_invite/zt-5b8e9kr4-PsKAVe4crGmECQyyxDIJgQ).
