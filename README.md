## Integrating services with cal.com

### Installing Cal.Com docker version

1) ``` git clone https://github.com/calcom/docker.git ```
2) copy .env.example as .env in the same directory 

3) Now we have to fill the .env file with necessary database information along with send grid information

4) Then do docker-compose pull

5) Before running docker-compose up get the credentials of google calendar which is in down part of readme.

6) Set Calendso_ENCRYPTION and NEXTAUTH_SECRET as 
```  dd if=/dev/urandom bs=1K count=1 | md5sum ```

7) Set 
EMAIL_SERVER_HOST as smtp.sendgrid.net

EMAIL_SERVER_USER as 'apikey' and password as the actual api key

8) Also these information should be filled out

SENDGRID_API_KEY= apikeyvalue
SENDGRID_EMAIL=any email
EMAIL_FROM=no-reply@ether.ai

9) Set OIDC as 
SAML_DATABASE_URL=postgresql://postgres:postgres@database:5432/calsaml
SAML_ADMINS='your email'

But you have to manually create saml database 'calsaml' by going into running docker container as :

```
docker exec -it database /bin/bash
psql -U postgres
#inside psql
CREATE DATABASE calsaml;
```

10) Then Run docker-compose up and access cal.com from localhost:3000
11) I have attached a demo env as well in github
### Getting credential of  Google Calendar 
#### For integrating google calendar follow these steps:
1) Go to google console site and add calendar as service 
https://console.cloud.google.com/apis/library?project=tactile-stack-402311

2) Then go to oauth consent screen and select user type as external

3) Fill the app name and developers contact information in second page and continue

4) Then select add scopes and filter calendar . You should see various option and only select 
../auth/calendar.readonly 
.../auth/calendar.events

5) Onto next page select add test users and add your email account which u would be using to login with cal.com 

6) Then after it is created go to credentials page and then create new oauth client id.

7) Then download all the credentials as json format which we will be using in .env file of cal.com


8) The credentials is added in GOOGLE_API_CREDENTIALS as format
GOOGLE_API_CREDENTIALS={"web":{"client_id":}}



