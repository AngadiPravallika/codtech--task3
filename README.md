import boto3
from botocore.client import Config

# Wasabi credentials and endpoint
wasabi_access_key = '32JOF4S4U004HOKOS08L'
wasabi_secret_key = 'zckbUAdRnJ3PfKRl1lCzQy2ReboichU3PUKQbpNl'
wasabi_endpoint_url = 'https://s3.us-central-1.wasabisys.com'  # Adjust region endpoint if needed

# Initialize S3 client for Wasabi
s3 = boto3.client('s3',
                  endpoint_url=wasabi_endpoint_url,
                  aws_access_key_id=wasabi_access_key,
                  aws_secret_access_key=wasabi_secret_key,
                  config=Config(signature_version='s3v4'))

bucket_name = 'task1'
file_name = 'demo.txt'
file_content = 'Hello from IBM Cloud to Wasabi storage!'

try:
    # Upload file to Wasabi bucket
    s3.put_object(Bucket=bucket_name, Key=file_name, Body=file_content)
    print(f'Uploaded {file_name} to bucket {bucket_name}')

    # Download file from Wasabi bucket
    response = s3.get_object(Bucket=bucket_name, Key=file_name)
    content = response['Body'].read().decode('utf-8')
    print(f'Downloaded content: {content}')

except Exception as e:
    print(f'Error: {e}')
