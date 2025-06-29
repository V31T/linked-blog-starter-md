### aniruddha offboarding meeting notes
- point of call: so future engineers know what his code does
	- merging salesforce and hubspot functionality into 1 single branch, 
		- done in: flow-salesforce-crm-integrations
			-  is a merge of the main salesforce and hubspot branches 
				- everything in HUBSPOT was working
				- Salesforce access token error, post request on postman for salesforce api we were getting access token errors, in salesforce there are salesforce tokens that validate access point, but is only valid for 10 minutes. After those 10 minutes a refresh token should be generated 
					- the access token would work for the 10 minutes but then the refresh token would not work
- next steps: make sure flow-salesforce-integration works


TLDR: flow-salesforce-crm-integrations is just a branch that contains the code in flow-salesforce-integrations and flow-hubspot. the problem; flow-salesforce-crm-integrations is just really old code, we need to check how old the code is and if there is new code. 
- according to aniruddha we should just delete the branch because since his offboarding there has been a lot more code added to flow-salesforce-integrations and flow-hubspot 
- the real next steps: compare ....crm-integrations with ...hubspot and ...salesforce-integrations 

# STVCMB-121: flow-salesforce-crm-integrations branch (deleted)

About the branch: The `flow-salesforce-crm-integrations` branch was created to merge both salesforce and hubspot functionality into 1 single branch to be tested before merging both into the main/dev branch. 

Notes:
- the branch was last worked on by Aniruddha about 6 months ago and functionality of the branch was not known.
- The hubspot functionality did work back then but the salesforce integration did not.
- Regarding salesforce functionality, 
	- "Salesforce access token error, post request on postman for salesforce api we were getting access token errors, in salesforce there are salesforce tokens that validate access point, but is only valid for 10 minutes. After those 10 minutes a refresh token should be generated" 
		- TLDR: Access Token error on Salesforce behalf 
- According to Aniruddha we should just delete the branch.

Our findings:
- The code is severely outdated
- Hubspot functionality still works but many new developments have been made in the hubspot-specific branch and these functionalities are already in main
- There serves no changes regarding the salesforce branch so we can assume that this branch is outdated when it comes to salesforce development as well.
- There is no point in having to "test" salesforce and hubspot integrations together because they are mutually exclusive and do not overlap in functionality (i.e. one is not dependent on the other so if we test them separately it is perfectly fine.)

Next steps:
- Branch Deletion (FINISHED)