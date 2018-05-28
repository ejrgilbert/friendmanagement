# Friend Management Api



### List of REST Endpoints and Explanation

1. Returns a list of friends of a person.
   * Path : `/friends`
   * Input :
   ```
   {
		"email":"abc@example.com"
   }
   ```
   * Sample Output :
   ```
   {
		"success": true,
		"friends":[
			"pqr@gmail.com",
			"lmn@gmail.com",			
		],
		"count":2
	}
	```
	* Defined Errors : 
	  * 4000 : Occurs when invalid email provided in the request.
	  * 40006 : Occurs when the email address in the request is not valid (Not matched with the Regex)
	  * 40004 : Occurs when the person given by the email does not exist
	  
2.  Returns list of common friends of two persons
    * Path : `/commonfriends`
    * Input :
    ```
    {
		"friends":[
			"abc@gmail.com",
			"pqr@gmail.com"
		]
    }
    ```
    * Output :
    ```
    {
		"success": true,
		"friends":[
			"lmn@gmail.com",
			"ijk@gmail.com"
		],
		"count":2
	}
	```
	* Defined Errors : 
	  * 4000 : Invalid request.
	  * 40006 : Request contains emails are invalid
	  * 40004 : Persons given by the email do not exist
	  * 40004 : The two email addresses in the input are the same
	  
3.  Establish Friendship between two persons
    * Path : `/friendrequest`
    * Input :
    ```
    {
		"friends":[
			"abc@gmail.com",
			"pqr@gmail.com"
		]
    }
    ```
    * Output :
    ```
    {
		"success": true
	}
	```
	* Defined Errors : 
	  * 4000 : Invalid request
	  * 40006 : Request contains emails are invalid
	  * 40004 : Persons given by the email do not exist
	  * 40004 : The two email addresses in the input are the same
	  * 40001 : Persons in the input are already friends
	  * 40002 : One of the person in the request have blocked the other person
	  
4.  Person subscribe to another Person
    * Path : `/subscribe`
    * Input :
    ```
    {
		"requestor":"abc@gmail.com",
		"target":"pqr@gmail.com"
    }
    ```
    * Output :
    ```
    {
		"success": true
	}
	```
	* Defined Errors : 
	  * 4000 : Invalid request
	  * 40006 : Request contains emails are invalid
	  * 40004 : Persons given by the email do not exist
	  * 40004 : The two email addresses in the input are the same
	  * 40001 : Persons in the input are already friends
	  * 40004 : Duplicate subscription, a person already subscribed to another

5.  Person block updates from another Person
    * Path : `/block`
    * Input :
    ```
    {
		"requestor":"example@example.com",
		"target":"example2@example.com"
    }
    ```
    * Output :
    ```
    {
		"success": true
	}
	```
	* Defined Errors : 
	  * 4000 : Invalid request
	  * 40006 : Request contains emails are invalid
	  * 40004 : Persons given by the email do not exist
	  * 40004 : The two email addresses in the input are the same
	  * 40001 : Persons in the input are already friends
	  * 40002 : The person already blocked updates from the user
	  
6.  Post an update which returns a list of emails that will receive the update.
    * Path : `/sendupdates`
    * Input :
    ```
    {
		"sender":"abc@gmail.com",
		"target":"Hello, how are you ! xyz@gmail.com"
    }
    ```
    * Output :
    ```
    {
		"success": true,
		"recipients":[
			"xyz@gmail.com",
			"pqr@gmail.com"			
		]
	}
	```
	* Defined Errors : 
	  * 4000 : Invalid request
	  * 40006 : Request contains emails are invalid
	  * 40004 : Persons given by the email do not exist
	  
### Other Errors

In any case any of the endpoint fails it outputs an error response instead. The error response has the below format

	```
	{
		"success": false,
		"errorCode": "000",
		"message":"Unknown Error"
	}
	```
   
### Database


