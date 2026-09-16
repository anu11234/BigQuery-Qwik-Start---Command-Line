# BigQuery: Qwik Start - Command Line || **GSP071**

**Command:**

```bash
# Get your active Project ID
PROJECT_ID=$(gcloud config get-value project)

# Task 3: Run queries on public dataset
bq query --use_legacy_sql=false \
'SELECT word, SUM(word_count) AS count FROM `bigquery-public-data`.samples.shakespeare WHERE word LIKE "%raisin%" GROUP BY word'

bq query --use_legacy_sql=false \
'SELECT word FROM `bigquery-public-data`.samples.shakespeare WHERE word = "huzzah"'

# Task 4: Create dataset, download data, and load table
bq mk --location=US babynames

wget http://www.ssa.gov/OACT/babynames/names.zip
unzip -o names.zip

bq load --source_format=CSV \
babynames.names2010 yob2010.txt name:string,gender:string,count:integer

# Task 5: Query custom dataset
bq query "SELECT name,count FROM babynames.names2010 WHERE gender = 'F' ORDER BY count DESC LIMIT 5"
bq query "SELECT name,count FROM babynames.names2010 WHERE gender = 'M' ORDER BY count ASC LIMIT 5"

# Task 7: Clean up dataset
bq rm -r -f babynames

echo "==> Lab tasks completed successfully! You can now click all 'Check my progress' buttons."
