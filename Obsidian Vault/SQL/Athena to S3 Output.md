# Athena to S3 output
#athena #s3 

Get s3 link to athena query output
```python
S3_PREFIX = "https://s3.console.aws.amazon.com/s3/object/"

def athena_to_s3(athena_download_link):
    """
    Get s3 link to athena query output.
    
    Args:
        athena_download_link: link to download athena output to csv
    
    Note - how to get athena_download_link:
    
        We wish to access the link that shows when you hover over the Download button of an athena query's output

        1. Run your athena query
        2. Right click on the "Download button"
        3. Click "Inspect"
        4. Right click on the highlighted cell
            - Should look like something similar to the following: <span title="s3://aws-athena-query-results-eu-west-1-709880522225/bc9812ea-87b8-40d3-b54f-18dae15a0fd1.csv">Download results</span>
        5. Click "Edit as HTML"
        6. Copy the title string 
            - From the above example, you'd copy "s3://aws-athena-query-results-eu-west-1-709880522225/bc9812ea-87b8-40d3-b54f-18dae15a0fd1.csv"
    """
    s3_suffix = athena_download_link.replace("s3://", "")
    print(S3_PREFIX + s3_suffix)
```

Output: https://s3.console.aws.amazon.com/s3/object/aws-athena-query-results-eu-west-1-709880522225/bc9812ea-87b8-40d3-b54f-18dae15a0fd1.csv

# Reading file from S3
TODO: need to find out what IAM User I have / how to create one
[Reading a Specific File from an S3 bucket Using Python](https://www.sqlservercentral.com/articles/reading-a-specific-file-from-an-s3-bucket-using-python)
* [AWS Account and Access Keys](https://docs.aws.amazon.com/powershell/latest/userguide/pstools-appendix-sign-up.html)

[Read file content from S3 bucket with boto3](https://stackoverflow.com/questions/36205481/read-file-content-from-s3-bucket-with-boto3)

