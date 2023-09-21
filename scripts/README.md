## Overview for the process of ingredientizing data 

01_unmatched_foodcodes_fndds_asa_export:
  * Load in FNDDS Ingredients database and dietary recalls and rename columns for merging data (FoodCode)
  * Remove recall line items without a foodcode (default is 9 in ASA system)
  * Merge diet recalls with FNDDS data
  * Determine the number of FoodCodes mapping from ASA24 to FNDDS (note: the ASA24 versions used were 2014 and 2016 [these years correspond to FNDDS versions 4.1 and 2011–2012 respectively], hence as FNDDS 2017-2018 was updated some FoodCodes are discontinued or modified)
  * Save the discontinued FoodCodes and replace with the updated foodcodes for the newer version. If you are using different versions of ASA24 / FNDDS, you can find a cross-walk to access the appropriate data for example:
  * https://www.ars.usda.gov/ARSUserFiles/80400530/apps/Discontinued_Food_Codes_between_FNDDS_2015-2016_and_FNDDS_2017-2018_102020.xlsx

02_ingredientize_mixed_foods
  * Following manual update of the missing FoodCodes, load in the data to replace FoodCodes that were changed across versions
  * Merge diet recalls with the updated FoodCodes and check for missing codes (this may occur depending on what years ASA24/FNDDS are used as some FoodCodes are discontinued and not replaced with a new code)
  * Save the 'ingredientized' dataset

03_ingredient_code_remap
  * Load in the 'ingredientized' data for additional processing to convert ingredient codes with 8-digits (representing a FoodCode) into the correct 5-digit ingredient code
  * This uses a series of merging the 8-digit code in the ingredient code column with the 8-digit code in the FoodCode column
  * Each of the merged datasets containing a layer of the 'ingredient subcodes' are combined manually and to create the final mapping: ingred_code_remapped_102021.csv

04_map_ingredient_nutrient_values
  * Load in the FNDDS ingredient nutrient data (https://www.ars.usda.gov/ARSUserFiles/80400530/apps/2017-2018%20FNDDS%20At%20A%20Glance%20-%20Ingredient%20Nutrient%20Values.xlsx) to extract carbohydrate values for determining the percent of carbs consumed mappable to the DFG1. Participants with <75% were removed for our study
  * Calculations are performed to quantify carbohydrates consumed and calorie intakes at the ingredient level

05_merge_asa24_glycopedia_all_matches
  * Load diet recalls, carb consumeds, and glycopedia data and merge DFG1 with diet recalls. Here participants with <75% of calories consumed from carbs mappable to DFG1 were removed
  * Calculations are performed to adjust monosaccharide intakes per 1000 kcal
