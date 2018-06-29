#Warstories with Postgres Autovacuum

##Abstract

GO-JEK is the market leader in Indonesia across multiple sectors including Ride Hailing and Food. We do more than 100+ million bookings a month. A majority of these bookings are created and managed in a single Order Management System and stored in a table called bookings. These bookings are updated multiple times with actions like pickup, complete etc. As a result this table sees very heavy writes 

In this talk, we will talk about what the problem exactly is and when can it occur, why it happened to us, and then what we did to fix it in the short and long term.


## Narrative

1. How we found out about the problem ?
 	* We had an OMS where whose DB size was increasing, we were looking to manage that. As part of doing that analysis we ran analysis queries and discovered that the age of unfrozen rows was above 1Billion.

2. We did not quite understand what it was, so we digged around trying to understand more and following is a high level overview.
 	* Explain the why does it happen ?

3. Why did it happen to us ? Flashback time !
	* Give business context and talk about numbers

4. How did we investigate the problem ?
	* Looked at our DB configs. Seemed fine.
	* Investigated our Postgres configs, seemed to be underprovisioned.

5. How did we solve it in the short term ?
	* Upgraded configs, explain constraints of not wanting to restart the database.
	* Looked at configs only requiring a reload.
	* Upgraded them and did a reload.
	* Operation Successful !! Swag !
	* Other Configs that we upgraded and restarted.

6. What can you do ?
	* Monitoring
	* Distribute the data and keep different data retention policies
	* To Delete:
		* Use partman. However may not possible in all scenarios especially for Legacy DBs with various queries.
		* Run a data deletion job. Ensure that it doesnt cause wraparound :D 

 	