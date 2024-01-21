# de-projects02
#### Problem
- Create dynamic file details table in sql db and stored procedure
- Get meta data structure of source and look up the right structure in sql db to write to the right table (execute SCD pipelines on conditions of meta data structure matching between source (container) and destination (sql db)
- Create data flow for slowly changing dimension tables type 2 -> add active status column, active start time and active end time), at the same time keep history
- source: data lake gen 2
- sink: sql database

#### Solution
- Create data flow -> 
- create columns ID_Hash and SCD_Hash in sqldb and storage account
- check new data in source based on ID_Hash and SCD_Hash and filter on new data only -> create surrogate key based on max skey of sqldb skey -> select relevant columns based on rule (get rid of ID_Hash and SCD_Hash) </p>
    ->> insert datasest
- check changes in sqldb vs. source and update sqldb based on ID_Hash -> derive columns active/activeEndTime -> select relevant columns -> update dataset
- => union check new data and check changes based on name
- => sink to destination with insert and update enabled

#### Unit test
- check 1: not changed file
- check 2: upserted file
