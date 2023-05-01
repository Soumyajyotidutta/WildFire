## Documentation -> Playground Analysis

### Follow Playground Analysis - kaggleUSA.ipynb 

	1. Load data -> kaggle 2.3 Million US Wildfires (1992-2020) 6th Edition {link: https://www.kaggle.com/datasets/behroozsohrabi/us-wildfire-records-6th-edition}

	2. Parameters: ['FIRE_YEAR', 'DISCOVERY_DOY', 'DISCOVERY_TIME', 
                    'NWCG_CAUSE_CLASSIFICATION', 'NWCG_GENERAL_CAUSE', 
                    'CONT_DATE', 'CONT_DOY', 'CONT_TIME', 'FIRE_SIZE', 'FIRE_SIZE_CLASS', 'LATITUDE'			, 'LONGITUDE', 'STATE']
	3. Average duration of fire: basis [Fires -> row 0,1, ....., n] 
	4. Add season by meteorogical information [for better understanding of behavior w.r.t season]
	5. Assign state codes
	7. Intermediate helper functions / operations
	6. Correlation matrix 
	7. Calculate number of total fires for each year since 1992
	8. Plot w.r.t states -> CA is done for playground analysis
	9. Plot correlation matrix (a) Entire USA  (b) CA
	10. Function to return the State Code Associated where Wild Fires are most present
	11. Top states in terms of wildfire incidents [Yearwise] -> plot
	12. Correlation matrix for top five states -> plot
	13. Divide states by east and west coast -> Plot correlation matrix
	14. Average duration and average size of fires
	15. Year vs Count of fires for top ten states -> Plot
	16. Average duration and average size of fires -> Plot these with reference to fire years [X axis]
	17. Correlation matrix for top 10 states -> plot
