---
date: "07 Dec 2020"
title: "Project 1: Database Structure and SQL Queries"
description: "Building a whole database using MySqlWorkbench, loading data and run queries"
featured_image: "/images/Project1Bg.jpg"
---

# Project Objective:
The goal of this project is to construct a well-functioning database containing at least 10 tables.
This database could be for a small business whether real existing organization or simulated business.
# Step1 : Building database
Using MySqlWorkbench, me and my team decided to create a database that manages operational
tasks for an imaginary realty office called (RentWithUS). Operational tasks that include building maintenance,
furniture procurement and overhead expenses, as well as revenue and rent payment accounting.
we built a relational database of 10 tables containing personal, descriptive and financial information wether about staff,
property, residents, revenue , expenses and leases.
 (Building, apartment, residents, expenditure, furniture,
  maintenance, office staff, payment, lease and rent).
### Tables
 1. **Building:** information about buildings
 2. **Apartment:** information about each apartment
 3. **Residents:** residents personal information
 4. **Expenditure:** expenses and their costs
 5. **Furniture:** furniture types and their conditions and locations
 6. **Maintenance:** maintenance jobs done to the property
 7. **Office staff:** office staff personal information
 8. **Payment:** rent payments
 9. **Lease:** lease types and their time periods
10. **Rent:** rents amounts depending on the lease type and apartment
### Tables Relations:
Database ERDiagram:

{{< figure src="/images/Project1Bg.jpg"  >}}

# Step 2: Forward-Engineer the ERDiagram:
MySqlWorkbench has a great tool (forward-Engineering) that translates a manually-built ERDiagram into SQL scripts to create the database.
It basically functions like SQL statements to build the database on the server.
# Step 3: Generating and Loading Data
Me and my team used [Mockaroo](https://www.mockaroo.com/) to generate simulated data. Then we loaded the data to SQL tables using Data Wizard tool in
MySqlWorkbench.

# Step 4: Asking Business Questions and Answer them Using SQL Scripts
##### Example:
###### Question
How many Maintenance Jobs were carried each Year per apartment? and what are their total costs? what is the average cost across all jobs?
###### Script
```SQL
select  m.ApartmentID,
        year(E.Date) as JobYear,
        count(m.MaintenanceID) as MatJobs,
        sum(E.amount) as totalcost,
        round((select sum(E.amount)/count(m.MaintenanceID) from Maintenance m
		 join Expenditure E on m.MaintenanceID = E.MaintenanceID),2) as AvgCost
from Maintenance m
join Expenditure E on m.MaintenanceID = E.MaintenanceID
group by m.ApartmentID, JobYear
order by m.ApartmentID, JobYear;
```

# A Taste of Visualization(Python):
##### Showing Number of Residents per Gender for each Apartment Type (1,2,3,4 bedrooms)
{{< figure src="/images/vis.jpg"  >}}
##### Python Script:
```Python
fig, ax = plt.subplots(figsize=(17, 9)) # set figure size
plt.bar(resrmfe['ApartmentType'], resrmfe['Numberofresidents'], width= 0.22,
            color='Brown', label = 'Female')  
plt.bar(resrmma['ApartmentType'], resrmma['Numberofresidents'], width = 0.11,
            color='Peru', label = 'Male')# set the axes for both geneders
plt.xlabel('Apartment Types', fontsize = 15) # x label
plt.ylabel('Number Of Residents' ,fontsize = 15) # y label
plt.xticks(resrmma['ApartmentType'], fontsize = 13, rotation = 45) # set x values
plt.yticks(fontsize = 13) # font size of y values
plt.legend(fontsize = 14) # legend lables
ax.set_facecolor("Honeydew") # color male bars
plt.title("Number of Residents Per Apartment's Type by Gender", fontsize = 18).set_position([0.5, 1.04]) # figure title
plt.show()
```
All files for this Project can be found in the github repository link below:

#### [Go to Github Repository](https://github.com/SamAlqarzi/Database-creation-withSQL)
### Credits To:
- **Jack Beck**
- **Jordan Waldroop**
- **Cody Rogers**
- **Isaac Everitt**
