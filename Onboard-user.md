Onboarding a User
====================


#### Uploading a List 

As an ESP, it may be useful to know the quality of a potential user's list(s) before accepting them as a customer. This set of instructions will provide a means of doing so.

Before upload a list, a few questions must first be answered about the list being uploaded:

1.   Does the csv have include a header on the first row?
If yes, the query parameter 'header' should be set to 'true', otherwise 'false'.

2.   What column is the email address in?
If the email address is in the first column, the query parameter 'email' should be set to '0'. If the email address is in the second column, it should be set to '1' etc.

3.   Is there data in each row (other than the email address) that you would like to store?
You might want to store additional data such as first name, last name, unqiue ID etc. If so, the query parameter 'metadata' should be set to 'true', otherwise 'false'.


After adding a list, individual member grades will be available via this endpoint: /list/{list_slug}/member/{member_slug}/

'member_slug' is a unique ID specific to members in a list. If you prefer to specify 'member_slug', set the 'slug_col' query parameter to the column containing your provided identifier in your csv(column 1 = 0). If this parameter is not provided, member slugs will be generated automatically.

Note: If you intend on accessing individual member grades and not ALL member grades, be sure to include member slugs in your csv. Otherwise, you will have to make a call to '/list/{list_slug}/member/' to retrieve the member_slugs we provide and you will be charged a remediation token for each member in the list.

Sample command:

    $ curl -X POST
    -H "Content-Type: text/csv
        Authorization: bearer {api_key}"
    "https://api.datavalidation.com/1.0/list/?header=true&email=0&metadata=true&slug_col=2"
    -d "email_address,first_name,ID,
        foo@example.com,foo,001,
        bar@example.com,bar,002,
        baz@example.com,baz,003,"

Sample output:

    {
        "list": [
            {
                "status": "new",
                "size": 0,
                "meta": {
                    "href": "https://api.datavalidation.com/1.0/list/Ko3yuDOI/",
                    "links": {
                        "jobs": "job/",
                        "batch_subscribe": "subscribe.csv",
                        "member": "member/{member_slug}/",
                        "job": "job/{job_slug}/",
                        "batch_unsubscribe": "unsubscribe.csv",
                        "export": "export.csv",
                        "members": "member/"
                    }
                },
                "slug": "Ko3yuDOI",
                "metadata": {}
            }
        ]
    }

**Be sure to store the slug, as this will be needed to access the list in the future.**


#### Running a Validation Job 

To begin processing a list, a job must be created to start validating members within a list.

Note: An Onboarding Token will be charged for each member in the list when a job is created.

Command:

    $ curl -X POST
    -H "Authorization: bearer {api_key}"
    "https://api.datavalidation.com/1.0/list/{list_slug}/job"

Sample output:

    {
        "job": [
            {
                "status": "New",
                "list_slug": "JItNx3th",
                "stats": {},
                "created": "2014-10-15 14:36:21.749000",
                "webhook": {
                    "status": null,
                    "complete": null
                },
                "priority": {
                    "mu": 10,
                    "sigma": 0
                },
                "original_chunks": null,
                "meta": {
                    "href": "https://api.datavalidation.com/1.0/list/JItNx3th/job/XdH8rZQk/"
                },
                "current_chunks": null,
                "pct_complete": 0,
                "slug": "XdH8rZQk"
            }
        ]
    }


If the list is large or we currently have a large number of list members to validate in our queue, it may take some time to validate the members in your list. 


To view the progress of a validation job, construct the following request using the job's slug from the above result:

Command:

    $ curl -X GET
    -H "Authorization: bearer {api_key}"
    "https://api.datavalidation.com/1.0/list/{list_slug}/job/{job_slug}/"


If the job is not finished, you should see a response similar to:

    {
        "job": [
            {
                "status": "New",
                "list_slug": "Ko3yuDOI",
                "stats": {},
                "created": "2014-10-15 15:29:28.335000",
                "webhook": {
                    "status": null,
                    "complete": null
                },
                "priority": {
                    "mu": 10,
                    "sigma": 0
                },
                "original_chunks": null,
                "meta": {
                    "href": "https://api.datavalidation.com/1.0/list/Ko3yuDOI/job/XLoklKeI/"
                },
                "current_chunks": null,
                "pct_complete": 0,
                "slug": "XLoklKeI"
            }
        ]
    }

Notice the 'pct_complete' field representing the current percent of completion.


#### Viewing List Grades 

This is an overview of an email list’s quality. It includes the total number of subscribers in each grade category, A+, A, B, D, and F, and an overall grade for the list. This report does not provide data on specific email addresses.

After a job is complete, repeating the GET request from above will yield a response similar to:
    
    {
        "job": [
            {
                "status": "Ready",
                "list_slug": "E5RIlS2B",
                "stats": {
                    "optout": {
                        "O4": 3
                    },
                    "grade": {
                        "D": 3
                    },
                    "hard": {
                        "H4": 3
                    },
                    "complain": {
                        "W4": 2,
                        "W3": 1
                    },
                    "trap": {
                        "T4": 2,
                        "T1": 1
                    },
                    "open": {
                        "R0": 3
                    },
                    "click": {
                        "K0": 3
                    },
                    "deceased": {
                        "D4": 3
                    }
                },
                "created": "2014-10-15 20:46:53.218000",
                "webhook": {
                    "status": null,
                    "complete": null
                },
                "priority": {
                    "mu": 10,
                    "sigma": 0
                },
                "original_chunks": 2,
                "meta": {
                    "href": "https://api.datavalidation.com/1.0/list/E5RIlS2B/job/zJSSU1HE/"
                },
                "current_chunks": 0,
                "pct_complete": 100,
                "slug": "zJSSU1HE"
            }
        ]
    } 