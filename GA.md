# Aerohive Guest Manament APIs

The Aerohive Guest Management APIs are designed to allow programatic access to the guest management platform built into Hive Manager and provide the following functionality:

  - Query the Identity Database for a specific user, phone number, email, user group
  - Query the Identity Database for a user group
  - Create a new user
  - Update user information
  - Extend the expiration of a user's credetials
  - Distribute credentials to a user via SMS or email
  - Delete user credentials

### Setup
The Guest Management functions *must* be enabled in Hive Manager in order to use the APIs. To do so, log into Hive Manager and click configure, then users. To do so, reference [configuring a User Group]. A [video tutorial] is also available to guide you throgh the process.

### The API Calls
>In order to make API calls to the Aerohive Guest Management platform, you must have an API Access Token. If you have not already obtained one, read the section on [authentication] before proceeding further.

##### Query Credentials
Query Credentials is designed to return credentials matching a specific search query. Search parameters include:
- memberOf (*Employee* group the user is a member of)
- adUser (Active Dorectory user name)
- creator (User who created the credentials, in case of lobby use or employee sponsorship)
- loginName
- firstName
- lastName
- phone
- userGroup (the *user* group a credential is tied to)

To query the Guest Access database for a specific username (dororke) type the following into the terminal window (substituting your account values for things like 'YOUR-VHM-ID'):

```sh
$ curl -X GET -H "X-AH-API-CLIENT-SECRET: daffa2ecd066ef09da98e4527749dee2" \
-H "X-AH-API-CLIENT-ID: 19a087a8" \
-H "X-AH-API-CLIENT-REDIRECT-URI: https://mysite.com" \
-H "Authorization: Bearer AHkUZggSUlyAoe2PPhav8AwQ9JhdbWv819a087a8" \
"http://cloud-va.aerohive.com/xapi/v1/identity/credentials?ownerId=1265"
```

This text you see here is *actually* written in Markdown! To get a feel for Markdown's syntax, type some text into the left window and watch the results in the right.

### Version
0.82


   [configuring a User Group]: <http://docs.aerohive.com/330000/docs/help/english/ng/learning-whats-new.htm#gui/configuration/configuring-user-group.htm>
   [authentication]: <https://developer.aerohive.com/docs/authentication>
   [video tutorial]: <https://training.aerohive.com/#/courses/course/207185>

