# symfony-security-ldap-login

#### setup
create .env.local
````
AD_SEARCHDN=##########
AD_SEARCHPWD=##########
AD_HOST=##########
AD_PORT=##########
AD_DNSTRING=##########
````
#### setup db
````
./bin/console doctrine:migrations:migrate

./bin/consle doctrine:load:fixtures
````
#### and run
````
symfony serve -d
````

use postman and send json to your login endpoint
````
POST https://127.0.0.1:8000/login
{
    "username": "john",
    "password": "test"
}
````

#### 4 different branches with different behavior

##### branch main 
````
(enable_authenticator_manager = false)
json_login and json_login_ldap work with a 3 user provider.
````

###### branch enable_authenticator_manager_on
````
(enable_authenticator_manager = true)
json_login and json_login_ldap won't work with any of the user provider
````
###### branch enable_authenticator_manager_on_json_login_ldap_disabled
````
enable_authenticator_manager = true
json_login_ldap and users_from_ldap provider commented out
json_login works with user provider users_in_memory users_from_database
````

###### branch enable_authenticator_manager_on_only_with_json_login_ldap
````
enable_authenticator_manager = true
json_login and provider users_in_memory users_from_database are disabled
json_login_ldap works with user provider users_from_ldap 
````
