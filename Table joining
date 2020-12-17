# Part 1 Query 

# 1. Top_10_deals_in_2009_Q4_SouthernUSA

select	a11.ACCT_ID  ACCT_ID,
	max(a16.ACCT_DESC)  ACCT_DESC,
	a15.SALES_DIST_ID  SALES_DIST_ID,
	max(a15.SALES_DIST_DESC)  SALES_DIST_DESC,
	a11.SALES_REP_ID  SALES_REP_ID,
	max(a15.SALES_REP_NAME)  SALES_REP_NAME,
	a11.OPTY_ID  OPTY_ID,
	max(a14.OPTY_DESC)  OPTY_DESC,
	a14.OPTY_CLOSE_DATE  OPTY_CLOSE_DATE,
	a14.PRIMARY_COMP_ID  PRIMARY_COMP_ID,
	max(a17.COMPETITOR_NAME)  COMPETITOR_NAME,
	sum(a11.OPTY_SIZE)  WJXBFS1
from	F_OPTY_MNTH_HIST	a11
	join	(select	pa11.ACCT_ID  ACCT_ID,
		pa11.OPTY_ID  OPTY_ID,
		pa11.SALES_REP_ID  SALES_REP_ID
	from	(select	a11.ACCT_ID  ACCT_ID,
			a11.OPTY_ID  OPTY_ID,
			a11.SALES_REP_ID  SALES_REP_ID,
			rank () over( order by sum(a11.OPTY_SIZE) desc)  WJXBFS1
		from	F_OPTY_MNTH_HIST	a11
			join	L_CAL_MNTH	a12
			  on 	(a11.MNTH_ID = a12.MNTH_ID)
		where	(a11.OPTY_STAT_ID in (5)
		 and a12.QTR_ID in (20094))
		group by	a11.ACCT_ID,
			a11.OPTY_ID,
			a11.SALES_REP_ID
		)	pa11
	where	(pa11.WJXBFS1 <=  10.0)
	)	pa12
	  on 	(a11.ACCT_ID = pa12.ACCT_ID and 
	a11.OPTY_ID = pa12.OPTY_ID and 
	a11.SALES_REP_ID = pa12.SALES_REP_ID)
	join	L_CAL_MNTH	a13
	  on 	(a11.MNTH_ID = a13.MNTH_ID)
	join	L_OPTY	a14
	  on 	(a11.OPTY_ID = a14.OPTY_ID)
	join	L_SALES_REP	a15
	  on 	(a11.SALES_REP_ID = a15.SALES_REP_ID)
	join	L_ACCT	a16
	  on 	(a11.ACCT_ID = a16.ACCT_ID)
	join	L_COMPETITOR	a17
	  on 	(a14.PRIMARY_COMP_ID = a17.COMPETITOR_ID)
where	(a13.QTR_ID in (20094)
 and a11.OPTY_STAT_ID in (5))
 and SALES_DIST_ID in (3)
group by	a11.ACCT_ID,
	a15.SALES_DIST_ID,
	a11.SALES_REP_ID,
	a11.OPTY_ID,
	a14.OPTY_CLOSE_DATE,
	a14.PRIMARY_COMP_ID

[Analytical engine calculation steps:
	1.  Evaluate view filter
	2.  Perform cross-tabbing
]


# 2. Current_Pipeline_for_Southern_USA_(2010_Q1)


select	a14.SALES_DIST_ID  SALES_DIST_ID,
	max(a14.SALES_DIST_DESC)  SALES_DIST_DESC,
	pa11.SALES_REP_ID  SALES_REP_ID,
	max(a14.SALES_REP_NAME)  SALES_REP_NAME,
	a13.CURR_OPTY_STAT_ID  CURR_OPTY_STAT_ID,
	max(a15.CURR_OPTY_STAT_DESC)  CURR_OPTY_STAT_DESC,
	pa11.OPTY_ID  OPTY_ID,
	max(a13.OPTY_DESC)  OPTY_DESC,
	a14.SALES_REGN_ID  SALES_REGN_ID,
	max(a14.SALES_REGN_DESC)  SALES_REGN_DESC,
	max(pa11.WJXBFS1)  WJXBFS1
from	(select	a11.SALES_REP_ID  SALES_REP_ID,
		a11.OPTY_ID  OPTY_ID,
		a11.MNTH_ID  MNTH_ID,
		sum(a11.OPTY_SIZE)  WJXBFS1
	from	F_OPTY_MNTH_HIST	a11
		join	L_OPTY	a12
		  on 	(a11.OPTY_ID = a12.OPTY_ID)
		join	L_CAL_MNTH	a13
		  on 	(a11.MNTH_ID = a13.MNTH_ID)
	where	(a12.CURR_OPTY_STAT_ID in (2, 1, 3)
	 and a13.QTR_ID in (20101))
	group by	a11.SALES_REP_ID,
		a11.OPTY_ID,
		a11.MNTH_ID
	)	pa11
	join	(select	pc11.SALES_REP_ID  SALES_REP_ID,
		pc11.OPTY_ID  OPTY_ID,
		max(pc11.MNTH_ID)  WJXBFS1
	from	(select	a11.SALES_REP_ID  SALES_REP_ID,
		a11.OPTY_ID  OPTY_ID,
		a11.MNTH_ID  MNTH_ID,
		sum(a11.OPTY_SIZE)  WJXBFS1
	from	F_OPTY_MNTH_HIST	a11
		join	L_OPTY	a12
		  on 	(a11.OPTY_ID = a12.OPTY_ID)
		join	L_CAL_MNTH	a13
		  on 	(a11.MNTH_ID = a13.MNTH_ID)
	where	(a12.CURR_OPTY_STAT_ID in (2, 1, 3)
	 and a13.QTR_ID in (20101))
	group by	a11.SALES_REP_ID,
		a11.OPTY_ID,
		a11.MNTH_ID
	)	pc11
	group by	pc11.SALES_REP_ID,
		pc11.OPTY_ID
	)	pa12
	  on 	(pa11.MNTH_ID = pa12.WJXBFS1 and 
	pa11.OPTY_ID = pa12.OPTY_ID and 
	pa11.SALES_REP_ID = pa12.SALES_REP_ID)
	join	L_OPTY	a13
	  on 	(pa11.OPTY_ID = a13.OPTY_ID)
	join	L_SALES_REP	a14
	  on 	(pa11.SALES_REP_ID = a14.SALES_REP_ID)
	join	L_CURR_OPTY_STATUS	a15
	  on 	(a13.CURR_OPTY_STAT_ID = a15.CURR_OPTY_STAT_ID)
where a14.SALES_DIST_ID in (3)
group by	a14.SALES_DIST_ID,
	pa11.SALES_REP_ID,
	a13.CURR_OPTY_STAT_ID,
	pa11.OPTY_ID,
	a14.SALES_REGN_ID

[Analytical engine calculation steps:
	1.  Evaluate view filter
	2.  Calculate subtotal: <Total> 
	3.  Perform cross-tabbing
]


# 3. Current_Pipeline_vs__Quota_by_Sales_Region_and_District (2010 Q1 Southern USA)

select	coalesce(pa11.SALES_DIST_ID, pa12.SALES_DIST_ID, pa13.SALES_DIST_ID)  SALES_DIST_ID,
	max(a17.SALES_DIST_DESC)  SALES_DIST_DESC,
	a17.SALES_REGN_ID  SALES_REGN_ID,
	max(a17.SALES_REGN_DESC)  SALES_REGN_DESC,
	max(pa11.WJXBFS1)  WJXBFS1,
	max(pa12.WJXBFS1)  WJXBFS2,
	max(pa13.WJXBFS1)  WJXBFS3,
	max(pa13.WJXBFS2)  WJXBFS4,
	(ZEROIFNULL(max(pa11.WJXBFS1)) + ZEROIFNULL(max(pa13.WJXBFS3)))  WJXBFS5,
	((ZEROIFNULL(max(pa11.WJXBFS1)) + ZEROIFNULL(max(pa13.WJXBFS4))) - ZEROIFNULL(max(pa12.WJXBFS1)))  WJXBFS6,
	max(pa13.WJXBFS5)  WJXBFS7,
	max(pa14.WJXBFS1)  WJXBFS8,
	max(pa14.WJXBFS2)  WJXBFS9,
	max(pa14.WJXBFS3)  WJXBFSa
from	(select	a13.SALES_DIST_ID  SALES_DIST_ID,
		sum(a11.OPTY_SIZE)  WJXBFS1
	from	F_OPTY_MNTH_HIST	a11
		join	L_CAL_MNTH	a12
		  on 	(a11.MNTH_ID = a12.MNTH_ID)
		join	L_SALES_REP	a13
		  on 	(a11.SALES_REP_ID = a13.SALES_REP_ID)
	where	(a11.OPTY_STAT_ID in (5)
	 and a12.QTR_ID in (20101))
	group by	a13.SALES_DIST_ID
	)	pa11
	full outer join	(select	a12.SALES_DIST_ID  SALES_DIST_ID,
		sum(a11.SALES_REP_QTA)  WJXBFS1
	from	F_SALES_REP_QTA	a11
		join	L_SALES_REP	a12
		  on 	(a11.SALES_REP_ID = a12.SALES_REP_ID)
	where	a11.QTR_ID in (20101)
	group by	a12.SALES_DIST_ID
	)	pa12
	  on 	(pa11.SALES_DIST_ID = pa12.SALES_DIST_ID)
	full outer join	(select	pa11.SALES_DIST_ID  SALES_DIST_ID,
		pa11.WJXBFS1  WJXBFS1,
		pa11.WJXBFS2  WJXBFS2,
		pa11.WJXBFS3  WJXBFS3,
		pa11.WJXBFS4  WJXBFS4,
		pa12.WJXBFS1  WJXBFS5
	from	(select	pa11.SALES_DIST_ID  SALES_DIST_ID,
			sum(pa11.WJXBFS1)  WJXBFS1,
			sum(pa11.WJXBFS2)  WJXBFS2,
			sum(pa11.WJXBFS2)  WJXBFS3,
			sum(pa11.WJXBFS2)  WJXBFS4
		from	(select	a11.SALES_REP_ID  SALES_REP_ID,
				a14.SALES_DIST_ID  SALES_DIST_ID,
				a11.OPTY_STAT_ID  OPTY_STAT_ID,
				a11.OPTY_ID  OPTY_ID,
				a11.MNTH_ID  MNTH_ID,
				a11.LEAD_ID  LEAD_ID,
				a11.ACCT_ID  ACCT_ID,
				a11.OPTY_SIZE  WJXBFS1,
				a11.WGHT_OPTY_SIZE  WJXBFS2,
				a11.OPTY_ID  WJXBFS3
			from	F_OPTY_MNTH_HIST	a11
				join	L_OPTY	a12
				  on 	(a11.OPTY_ID = a12.OPTY_ID)
				join	L_CAL_MNTH	a13
				  on 	(a11.MNTH_ID = a13.MNTH_ID)
				join	L_SALES_REP	a14
				  on 	(a11.SALES_REP_ID = a14.SALES_REP_ID)
			where	(a12.CURR_OPTY_STAT_ID in (2, 1, 3)
			 and a13.QTR_ID in (20101))
			)	pa11
			join	(select	pc11.SALES_DIST_ID  SALES_DIST_ID,
				max(pc11.MNTH_ID)  WJXBFS1
			from	(select	a11.SALES_REP_ID  SALES_REP_ID,
				a14.SALES_DIST_ID  SALES_DIST_ID,
				a11.OPTY_STAT_ID  OPTY_STAT_ID,
				a11.OPTY_ID  OPTY_ID,
				a11.MNTH_ID  MNTH_ID,
				a11.LEAD_ID  LEAD_ID,
				a11.ACCT_ID  ACCT_ID,
				a11.OPTY_SIZE  WJXBFS1,
				a11.WGHT_OPTY_SIZE  WJXBFS2,
				a11.OPTY_ID  WJXBFS3
			from	F_OPTY_MNTH_HIST	a11
				join	L_OPTY	a12
				  on 	(a11.OPTY_ID = a12.OPTY_ID)
				join	L_CAL_MNTH	a13
				  on 	(a11.MNTH_ID = a13.MNTH_ID)
				join	L_SALES_REP	a14
				  on 	(a11.SALES_REP_ID = a14.SALES_REP_ID)
			where	(a12.CURR_OPTY_STAT_ID in (2, 1, 3)
			 and a13.QTR_ID in (20101))
			)	pc11
			group by	pc11.SALES_DIST_ID
			)	pa12
			  on 	(pa11.MNTH_ID = pa12.WJXBFS1 and 
			pa11.SALES_DIST_ID = pa12.SALES_DIST_ID)
		group by	pa11.SALES_DIST_ID
		)	pa11
		left outer join	(select	pa11.SALES_DIST_ID  SALES_DIST_ID,
			count(distinct pa11.WJXBFS3)  WJXBFS1
		from	(select	a11.SALES_REP_ID  SALES_REP_ID,
				a14.SALES_DIST_ID  SALES_DIST_ID,
				a11.OPTY_STAT_ID  OPTY_STAT_ID,
				a11.OPTY_ID  OPTY_ID,
				a11.MNTH_ID  MNTH_ID,
				a11.LEAD_ID  LEAD_ID,
				a11.ACCT_ID  ACCT_ID,
				a11.OPTY_SIZE  WJXBFS1,
				a11.WGHT_OPTY_SIZE  WJXBFS2,
				a11.OPTY_ID  WJXBFS3
			from	F_OPTY_MNTH_HIST	a11
				join	L_OPTY	a12
				  on 	(a11.OPTY_ID = a12.OPTY_ID)
				join	L_CAL_MNTH	a13
				  on 	(a11.MNTH_ID = a13.MNTH_ID)
				join	L_SALES_REP	a14
				  on 	(a11.SALES_REP_ID = a14.SALES_REP_ID)
			where	(a12.CURR_OPTY_STAT_ID in (2, 1, 3)
			 and a13.QTR_ID in (20101))
			)	pa11
		group by	pa11.SALES_DIST_ID
		)	pa12
		  on 	(pa11.SALES_DIST_ID = pa12.SALES_DIST_ID)
	)	pa13
	  on 	(coalesce(pa11.SALES_DIST_ID, pa12.SALES_DIST_ID) = pa13.SALES_DIST_ID)
	left outer join	(select	a14.SALES_DIST_ID  SALES_DIST_ID,
		(Case when max((Case when a12.CURR_OPTY_STAT_ID in (2) then 1 else 0 end)) = 1 then count(distinct (Case when a12.CURR_OPTY_STAT_ID in (2) then a11.OPTY_ID else NULL end)) else NULL end)  WJXBFS1,
		(Case when max((Case when a12.CURR_OPTY_STAT_ID in (1) then 1 else 0 end)) = 1 then count(distinct (Case when a12.CURR_OPTY_STAT_ID in (1) then a11.OPTY_ID else NULL end)) else NULL end)  WJXBFS2,
		(Case when max((Case when a12.CURR_OPTY_STAT_ID in (3) then 1 else 0 end)) = 1 then count(distinct (Case when a12.CURR_OPTY_STAT_ID in (3) then a11.OPTY_ID else NULL end)) else NULL end)  WJXBFS3
	from	F_OPTY_MNTH_HIST	a11
		join	L_OPTY	a12
		  on 	(a11.OPTY_ID = a12.OPTY_ID)
		join	L_CAL_MNTH	a13
		  on 	(a11.MNTH_ID = a13.MNTH_ID)
		join	L_SALES_REP	a14
		  on 	(a11.SALES_REP_ID = a14.SALES_REP_ID)
	where	(a13.QTR_ID in (20101)
	 and (a12.CURR_OPTY_STAT_ID in (2)
	 or a12.CURR_OPTY_STAT_ID in (1)
	 or a12.CURR_OPTY_STAT_ID in (3)))
	group by	a14.SALES_DIST_ID
	)	pa14
	  on 	(coalesce(pa11.SALES_DIST_ID, pa12.SALES_DIST_ID, pa13.SALES_DIST_ID) = pa14.SALES_DIST_ID)
	join	L_SALES_REP	a17
	  on 	(coalesce(pa11.SALES_DIST_ID, pa12.SALES_DIST_ID, pa13.SALES_DIST_ID) = a17.SALES_DIST_ID)
group by	coalesce(pa11.SALES_DIST_ID, pa12.SALES_DIST_ID, pa13.SALES_DIST_ID),
	a17.SALES_REGN_ID

[Analytical engine calculation steps:
	1.  Calculate metric: <% Quota Achieved (Current)> at original data level
	2.  Calculate metric: <% Quota Achieved vs. Revenue Projection> at original data level
	3.  Calculate subtotal: <Total> 
	4.  Calculate metric: <% Quota Achieved (Current)> at subtotal levels
	5.  Calculate metric: <% Quota Achieved vs. Revenue Projection> at subtotal levels
	6.  Evaluate thresholds
	7.  Perform cross-tabbing
]

# Part 2 

# (d) Go back to the browser and click OK to enter the SQL Assistant interface. 
# You can query the data warehouse here called db samwh9. 
# You can run simple queries to examine the data and the structure of the tables.

# (e) Execute the three SQL queries you created in 1 on this interface to check the results.
# Confirm that the results are the same as in 1.

 -- Please see attached files "answerset.csv Q1, 2, 3" and "Q1,2,3, SQL" screenshots



# (f) Click on the ‘+‘ sign on the left panel next to db samwh9 and inspect the table schemas. 
# Take any one of the three queries and explain in plain English how it works to give you the desired result.

# pick query 2 - Current_Pipeline_for_Southern_USA_(2010_Q1)

select	a14.SALES_DIST_ID  SALES_DIST_ID,     -- select statements to that use function (max) to display caluclations, sales region and district ID, 
	max(a14.SALES_DIST_DESC)  SALES_DIST_DESC,   -- current oppportunities, status, and sales representative 
	pa11.SALES_REP_ID  SALES_REP_ID,
	max(a14.SALES_REP_NAME)  SALES_REP_NAME,
	a13.CURR_OPTY_STAT_ID  CURR_OPTY_STAT_ID,
	max(a15.CURR_OPTY_STAT_DESC)  CURR_OPTY_STAT_DESC,
	pa11.OPTY_ID  OPTY_ID,
	max(a13.OPTY_DESC)  OPTY_DESC,
	a14.SALES_REGN_ID  SALES_REGN_ID,
	max(a14.SALES_REGN_DESC)  SALES_REGN_DESC,
	max(pa11.WJXBFS1)  WJXBFS1
    
    
from	(select	a11.SALES_REP_ID  SALES_REP_ID,  
		a11.OPTY_ID  OPTY_ID,
		a11.MNTH_ID  MNTH_ID,
		sum(a11.OPTY_SIZE)  WJXBFS1
        
	from	F_OPTY_MNTH_HIST	a11   -- from statement - the table is a fact table "F_OPTY_MNTH_HIST"
		join	L_OPTY	a12                  -- join  dimension tables "L_OPTY" and "L_CAL_MNTH"
		  on 	(a11.OPTY_ID = a12.OPTY_ID)   -- with opportunity ID 
		join	L_CAL_MNTH	a13              
		  on 	(a11.MNTH_ID = a13.MNTH_ID)    -- join month ID with a month ID 
	where	(a12.CURR_OPTY_STAT_ID in (2, 1, 3)  -- WHERE the current opoporuntity status includes only ID 2,1,3 
	 and a13.QTR_ID in (20101))                 -- and the quarter ID is 20101 which is year 2010 quarter 1 
	group by	a11.SALES_REP_ID,         -- group by sales ID , opportunity ID
		a11.OPTY_ID,
		a11.MNTH_ID
	)	pa11
    
    
	join	(select	pc11.SALES_REP_ID  SALES_REP_ID,    -- another join  
		pc11.OPTY_ID  OPTY_ID,
		max(pc11.MNTH_ID)  WJXBFS1
	from	(select	a11.SALES_REP_ID  SALES_REP_ID,
		a11.OPTY_ID  OPTY_ID,
		a11.MNTH_ID  MNTH_ID,
		sum(a11.OPTY_SIZE)  WJXBFS1
	from	F_OPTY_MNTH_HIST	a11
		join	L_OPTY	a12
		  on 	(a11.OPTY_ID = a12.OPTY_ID)
		join	L_CAL_MNTH	a13
		  on 	(a11.MNTH_ID = a13.MNTH_ID)
	where	(a12.CURR_OPTY_STAT_ID in (2, 1, 3)
	 and a13.QTR_ID in (20101))
	group by	a11.SALES_REP_ID,
		a11.OPTY_ID,
		a11.MNTH_ID
	)	pc11
	group by	pc11.SALES_REP_ID,
		pc11.OPTY_ID
	)	pa12
	  on 	(pa11.MNTH_ID = pa12.WJXBFS1 and 
	pa11.OPTY_ID = pa12.OPTY_ID and 
	pa11.SALES_REP_ID = pa12.SALES_REP_ID)
    
    -- OTHER quick joins 
	join	L_OPTY	a13                    
	  on 	(pa11.OPTY_ID = a13.OPTY_ID)
	join	L_SALES_REP	a14
	  on 	(pa11.SALES_REP_ID = a14.SALES_REP_ID)
	join	L_CURR_OPTY_STATUS	a15
	  on 	(a13.CURR_OPTY_STAT_ID = a15.CURR_OPTY_STAT_ID)
where a14.SALES_DIST_ID in (3)    -- where statement that only display the district ID - 3 which is Southern USA 
group by	a14.SALES_DIST_ID,
	pa11.SALES_REP_ID,
	a13.CURR_OPTY_STAT_ID,
	pa11.OPTY_ID,
	a14.SALES_REGN_ID


# Offer intuition on how the query is constructed 
# one para brief explanation of how you think the query is achieving one of the results
# trace how one or two of the numbers have been computed

-- db_samwh9 is a complicated schema as we can see from the tables' prefix F and L which stands for
-- fact and dimensions. The query aggregate data from multiple table and there are many joins between tables as well as many subqueries.
-- Also,when I first run the query 2 on TNU SQL assistant,I couldn't get the same results as the report generated by the OLAP tools.
-- I epected only 1 row but 8 rows were displayed. Thus, I added a "where" statement in order to show the results of the Southern USA district only. 



