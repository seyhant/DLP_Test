#!./venv/bin/python
#
# Google DLP API Basic Test , based on Google Examples and Internet Reserach 
# Key Information : Google Cloud Documentation, Release 0.28.1 , API Reference Page 277
# Goal get basic access and test DLP basic 

import httplib2
import sys
import argparse
# using google.auth as oauth2client is depreciated 
import google.auth


#from google.auth.cloud import dlp_v2beta1
from google.cloud import dlp_v2beta1

from google.oauth2 import service_account

# Json File for Service Access : 
# JSON File created gcloud consol : API & Dienste -> Zugangsdaten -> Anmeldedaten erstellen 
# Download des JSON File -> File for the credentatials 
credentials = service_account.Credentials.from_service_account_file('/Users/buchmann/development/gdpr/GDPR-61fd2643450e.json')

def main():


  
  # Build the service , add credentials from Services JSON file , as default Environment variables didn't work 

  client = dlp_v2beta1.DlpServiceClient(credentials=credentials)
# Data for DLP Inspection just for test, used Google Example
  name = 'EMAIL_ADDRESS'
  info_types_element = {'name': name}
  info_types = [info_types_element]
  inspect_config = {'info_types': info_types}
  type_ = 'text/plain'
  value = 'My email is example@example.com.'
  items_element = {'type': type_, 'value': value}
  items = [items_element]
#DLP Findings 
  response = client.inspect_content(inspect_config, items)
  print(response)


if __name__ == '__main__':
  main()