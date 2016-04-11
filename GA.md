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
$ curl -X GET -H "X-AH-API-CLIENT-SECRET: YOUR-CLIENT SECRET" \
-H "X-AH-API-CLIENT-ID: YOUR-CLIENT-ID" \
-H "X-AH-API-CLIENT-REDIRECT-URI: YOUR-REDIRECT-URL" \
-H "Authorization: Bearer YOUR-ACCESS-TOKEN" \
"http://cloud-va.aerohive.com/xapi/v1/identity/credentials?ownerId=YOUR-OWNER-ID"
```

##### [Create Credentials] 
Create Credentials allows you to add a new user to the identity database. It is completed with a POST request. You must supply the following in the JSON body: [Create Swagger]
- deliverMethod: ['NO_DELIVERY', 'EMAIL', 'SMS', 'EMAIL_AND_SMS']
- policy: ['PERSONAL', 'GUEST']

The following are optionally delivered in the JSON body:
- deliverMethod: ['NO_DELIVERY', 'EMAIL', 'SMS', 'EMAIL_AND_SMS']
- email (string, optional): The email of the credential
- firstName (string, optional): The first name of the credential
- lastName (string, optional): The last name of the credential
- groupId (integer): The user group in which the credential is to be created
- organization (string, optional): Home organization
- phone (string, optional): The phone number of the credential
- purpose: the reason this credential is created

```sh
$ curl -X POST --header "Content-Type: application/json" --header "Accept: application/json" -d "{
deliverMethod: \"EMAIL_AND_SMS\",
email (string, optional): \"Dororke@aerohive.com\" ,
firstName (string, optional): \"Daniel\",
lastName (string, optional): \"O'Rorke\",
groupId (integer): 12345,
organization: \"Aerohive Networks\",
phone (string, optional): \"4085551234\",
policy: ['GUEST'],
purpose: \"the reason this credential is created\"
}" "https://cloud-va.aerohive.com/xapi/v1/identity/credentials?ownerId=YOUR-OWNER-ID&memberOf=Aerohive%20Staff&adUser=AEROHIVE%5CDANIELO"
```

##### Delete Credentials
User Credentials may be deleted by sending a DELETE command to the credentials endpoint with the ID numbers of the user records you wish to delete. [Delete Swagger]
```sh
curl -X DELETE --header "Accept: */*" "https://cloud-va.aerohive.com/xapi/v1/identity/credentials?ownerId=YOUR-OWNER-ID&ids=23456789&ids=34567890&ids=45678901&memberOf=Aerohive%20Staff&adUser=Aerohive%5Cdanielo"
```


View the [Swagger Documentation] on all the Identity APIs including: 
- Query
- Create
- Delete
- Update
- Deliver
- Renew

### Version
0.82


   [configuring a User Group]: <http://docs.aerohive.com/330000/docs/help/english/ng/learning-whats-new.htm#gui/configuration/configuring-user-group.htm>
   [authentication]: <https://developer.aerohive.com/docs/authentication>
   [video tutorial]: <https://training.aerohive.com/#/courses/course/207185>
   [Delete Swagger]: <https://developer.aerohive.com/docs/api-documentation#!/identity/removeCredentialsUsingDELETE>
   [Swagger Documentation]: <https://developer.aerohive.com/docs/api-documentation#!/identity>

