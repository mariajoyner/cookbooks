Email Assurance for ESP Cookbook
====================

Contents
---------------------

#### Documentation

-   Getting Started
-   Onboard a User
-   Remediate a User's List
-   Manage a User's List


#### References

-   Definition of Terms
-   Grades
-   Webhooks (doesn't yet exist)
-   Testing (doesn't yet exist)
-   API Changelog (doesn't yet exist)
-   API Libraries [current API docs](https://github.com/synappio/synappio-client/blob/master/api-docs/batch.yaml)
-   Full API Reference (doesn't yet exist)


#### Subscriptions (doesn't yet exist)

-   Overview (doesn't yet exist)
-  	Monitoring (doesn't yet exist)
-   Remediating (doesn't yet exist)


#### FAQ (doesn't yet exist)

-   Integration (doesn't yet exist)
-   Billing (doesn't yet exist)
-   Support (doesn't yet exist)




Documentation
---------------------

### Getting Started

Overview: This API is designed to....

##### Basic usage of the API

###### Create a new list

This can be used when onboarding a new user, or when an existing user uploads a new email list. Note: Creating a new list will consume an onboarding token per subscriber on the list. 

###### Retrieve lists

This can be used to retrieve list level data, such as the Email Assurance Report. It can also be used to retrieve all lists in a user's account, or all lists ESP wide. 

###### Retrieve an individual list by its slug

This can be used to check the status of an individual list. 

###### Delete an individual list and all its subscribers

This can be used to delete an individual list and all its members.

###### Add members to a list

This can be used when new subscribers are added to an existing list.

###### Export list subscribers to get grades for all members on a list

Retrieve the entire list of subscribers with this function.
Note: Export list subscribers will consume a remediation token per subscriber on the list.

###### Get the members of a list

Access all of the subscribers on a single list.

###### Create a new list member 

Add a single member to a list.

###### Get single member grade

Get the grade for a single email address.
Note: Getting a single member grade will consume a remediation token per member.

###### Update a single member's date

Update the data for a single member.

###### Delete a member from a list

Delete a single member from the list.

###### Batch delete members from a list

##### Subscription usage of API

*   Retrieve list grade update daily
*   Retrieve list grade and subscriber grade update daily
*   Batch unsubscribe F results daily 
*   Retrieve an Email Assurance Report for entire ESP database
*   Retrieve subscriber email assurance grades for entire ESP database
*   Unsubscribe emails from a list based on grade vs deleting from DV system

##### Recommended for ESPs

*   Create a Safe to Send segment for A+ and A grades 
*   Sort list members by Email Assurance Grade 
*   Update a list grade after remediation by creating a job

### Onboard a User

From zero to retrieving stats


### Onboard a User with Remediation

From zero to retrieving stats to remediate


### Remediate a New List

### Remediate an Existing List


### Manage a User's List

-add a single member

-remove a single member

-batch add members

-batch delete members





References
---------------------

### Definition of Terms

>Email Assurance Report
>	
>Email Assurance Grade

#### Email Assurance Report

[Go to API Documentation on retrieving reports.]()

This report is an overview of an email list’s quality. It includes the total number of subscribers in each grade category, A+, A, B, D, and F, and an overall grade for the list. This report does not provide data on specific email addresses. 

**Uses of this report:** 

*   When onboarding a new user - retrieve Email Assurance Reports on all of the lists a prospective/new user intends to use. These reports can be used to determine whether to accept the user as a trusted sender. If the user has several problematic lists, remediation can be recommended prior to deploying mail. If the user has highly questionable lists, it can be required that these lists be removed and not used in the ESP platform. 

*   Prior to deploying email from a previously inactive user account - after a user has not deployed email for at least 3 months, retrieve an Email Assurance Report on the list prior to allowing the email to be deployed. If the data is acceptable, the user can move forward without remediation. If not, the user can be recommended remediation prior to deploying the campaign. 

*   When a current user imports a new list - retrieve an Email Assurance Report prior to allowing email to be deployed. If the data is acceptable, the user can move forward without remediation. If not, the user can be recommended remediation prior to deploying the campaign. If the list is too risky, it can be disallowed altogether. 

*   Embed the data to allow users to always see the Email Assurance Report - users can always know the list quality so it is not a surprise if remediation is recommended.

#### Email Assurance Grade

[Go to API Documentation on retrieving grades.]()

This grade — A+, A, B, D, or F— indicates an emails likelihood to be deliverable. Additional deliverability data is provided with the grade. Email Assurance Grade data is provided with the usage of a remediation token, or subscription.  
     
   A+ indicates engagement history such as click or optin. 
   A indicates successful delivery history or a positive SMTP response. 
   B indicates an accepts all domain. 
   D indicates no response from a server, or temporary failure. 
   F indicates an undeliverable address due to history of bounces, or a negative SMTP response. 

**Uses of the grades:**

*   Determine what grades a user can deploy email to - A+ and A results are deliverable based on our most recent data. If a user is a trusted sender, perhaps B results can be allowed. D results should not be deployed email. F results should be unsubscribed.

*   Automatically unsubscribe F results 

*   Create a Safe to Send Segment - place A+ and A results in this segment 

#### Monitoring

#### Email Assurance (Monitoring and Remediation) 

#### Remediation

#### Onboard a user

### Email Assurance Grades

### Webhooks

### Testing

### API Changelog



Subscriptions
---------------------

### Overview
### Monitoring
###	Remediating


FAQ
---------------------

Integration

Billing

Support

