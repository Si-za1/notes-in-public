---
title: SQL
draft: false
tags:
  - data
---
# My approach to solve the mystery 

First from the table *crime_report_scene -> gathering information*
So from there I found out 2 information
- there were 2 witnesses present on the day. 
- for one address was given and for another the first name and address

And using that, I took the first approach to understand more from the table person, I tried to find people present in the address provided, but, it was a futile effort as it had almost 50 people present there, starting from there would have given me trouble. 

Then from there I went with the another information which was I had first name and the address given, so from there I found the person, the id and all the information that will help me to proceed further.

And now, there was a table called Interview, from that, I went to see her transcript 
and from there I found another information as a clue, that was the murderer was there on jan 09 when she was working out at her gym.

Now, from here, I went to the table that contained the gym information.
### Investigate gym attendance on Jan 09

**Query used:**

`select g.person_id, g.name, g.id, gf.check_in_date, gf.check_in_date, gf.check_out_time from get_fit_now_member as g left join get_fit_now_check_in as gf    on g.id = gf.membership_id where gf.check_in_date = 20180109;`

Now, from this I found a really crucial information, that led me to investigate the event table, and then find the information further 

**Query used:**
`select p.id, p.name, count(*) as number_of_times`
`from person as p` 
`join facebook_event_checkin as f` 
  `on f.person_id = p.id`
`where f.date between 20171201 and 20171231` 
  `and f.event_name like "SQL%"`
`group by p.id, p.name`
`having count(*) = 3;`

Now, all the remaining thing was to do, was to verify the information for which i needed to traceback and connect it with the first table i.e. Person and the Driver's License.

`select p.id, p.name , d.gender, d.height , d.hair_color`
`from person as p`
`join drivers_license as d` 
`on p.license_id = d.id`
`where p.id IN (99716, 24556);`

**Conclusion:**

- Only **Miranda Priestly** matches:
    
    - Female
        
    - Red hair
        
    - Consistent with Jeremy’s statement

## Final Deduction

By progressively narrowing:

- Witness → gym presence → interview clues → event attendance → physical attributes  
    **Miranda Priestly** satisfies **all constraints** and is identified as the murderer.