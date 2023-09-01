# 1. Download folder source from Driver disk to my local

# 2. Create python3 virtualenvironment for this project

# 3. Connect to postgres DB with SDK tools
**restore db file**
    psql -U postgres  -f db_postgres.sql

    pg_restore -U postgres -f db_postgres.sql
    pg_dump -U postgres -f db_postgres.sql
**transfer content to a new db**
    createdb -U postgres -T template0 mydatabase
    Get-Content db_postgres.sql | psql -U postgres --set ON_ERROR_STOP=on mydatabase

**connect to a new database**
    psql -U postgres mydatabase

    \dt
    SELECT * FROM pg_catalog.pg_tables WHERE schemaname != 'pg_catalog' AND schemaname != 'information_schema';
!!!        ------------------> 0 ROWS // Empty Result  ["Something_was_wrong"]


**Other way**
    createdb -U postgres mydb
    pg_restore -U postgres -h localhost -d mydb db_postgres.sql
    psql -U postgres -d mydb
    SELECT * FROM pg_catalog.pg_tables WHERE schemaname != 'pg_catalog' AND schemaname != 'information_schema';
    \dt test_task.*
    \dn    # to see all schemas

    SET search_path TO test_task;
    \dt    # to see all tables


host == localhost
user == postgres
pass == 1
db == mydb
schema == test_task
tables == [accounts, posts, sources_for_followers]


# 4. First checking Data 

posts.    [profile_id]   ==  accounts.              [id]
accounts. [_id]          ==  sources_for_followers. [_id]

In accounts we can change ["id"] to ["profile_id"]
In posts    we can change ["id"] to ["post_id"]


+ 3 <alt_id> from ACCOUNTS (maybe different post tag) == 3 <profile_id> from POSTS
Need to change with np.where <profile_id> in POSTS to <alt_id> because values not matched


   **We have:**

29 media sources 
~ 1100 posts 
~ 5 months period in Data

Create 8 Reports in "Analyze_Data_withPandas.ipynb" in the end
Create query to Postgres to extract all Data in "Sql_query.ipynb"