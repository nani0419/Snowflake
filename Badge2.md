# Granting rights using code
```sql
grant imported privileges
on database SNOWFLAKE_SAMPLE_DATA
to role SYSADMIN;
```

# Create warehouse
```sql
create warehouse INTL_WH 
with 
warehouse_size = 'XSMALL' 
warehouse_type = 'STANDARD' 
auto_suspend = 600 --600 seconds/10 mins
auto_resume = TRUE;
```

# Create a File format
```sql
create or replace file format util_db.public.PIPE_DBLQUOTE_HEADER_CR 
  type = 'CSV' --use CSV for any flat file
  compression = 'AUTO' 
  field_delimiter = '|' --pipe or vertical bar
  record_delimiter = '\r' --carriage return
  skip_header = 1  --1 header row
  field_optionally_enclosed_by = '\042'  --double quotes
  trim_space = FALSE;
```
# Create or View Stages  
View Stages
```
show stages in account;
```
Create a Stage
```
create stage util_db.public.aws_s3_bucket url = 's3://uni-cmcw';
```
View what is there in stage
```
list @util_db.public.aws_s3_bucket;
```
Copy data to table from Stage
```
copy into intl_db.public.INT_STDS_ORG_3166
from @util_db.public.aws_s3_bucket
files = ( 'ISO_Countries_UTF8_pipe.csv')
file_format = ( format_name='util_db.public.PIPE_DBLQUOTE_HEADER_CR');
```