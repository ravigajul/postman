# postman
This is a repository for postman collections and useful resources
# NewMan : It’s a CLI for running postman collections in a terminal which helps further for CICD.
## Dependencis : Node.js and NPM

# Intall NewMan
* Npm install -g newman

# Run a collection using newman CLI
# 1. Newman run <<link to the collection>> // we can get the link by right clicking on collections in postman -->share collection -->collection link-->collection link 
 
	Ex: newman run https://www.getpostman.com/collections/f81a23f887c2e42e610e
	
	Note: If any changes are done to the collection in postman, the link should be updated in order for us to see the appropriate results in Newman as per the changes. 

# 2. The above process of getting updated link is not suggested when you are working in a team. Best way is to export the collection and run it with collection name.
		a. Right click on collection and export the collection as <<test.json>>
		b. Go to cmd and go to folder where collection is present and run the below command
		c. Newman run test.json
# 3. Generate API Key
		a. Click on user -->Acccount Settings -->Postman API Keys-->Generate API key or directly access using below.
		b. https://web.postman.co/settings/me/api-keys\
# 4. Get the List of collections
		a. Run the below command.Follow this link to create below link -
		Generate an API key
		From <https://github.com/postmanlabs/newman#using-newman-with-the-postman-api> 
		
	newman run https://api.getpostman.com/collections/6503bbaf-0bf2-ecd4-9a26-02e95f4ab915?apikey=PMAK-609a586545cb530040789de5-83ba771fd6dcd30645239bd9c46f4344d7
	Note: This process is auto synced to postman profile hence no need of exporting after any changes etc 
# 5. Using Newman with postman
	1 Generate an API key
	2 Fetch a list of your collections from: https://api.getpostman.com/collections?apikey=$apiKey
	3 Get the collection link via it's uid: https://api.getpostman.com/collections/$uid?apikey=$apiKey
	4 Obtain the environment URI from: https://api.getpostman.com/environments?apikey=$apiKey
	5 Using the collection and environment URIs acquired in steps 3 and 4, run the collection as follows:
	$ newman run "https://api.getpostman.com/collections/$uid?apikey=$apiKey" \
	    --environment "https://api.getpostman.com/environments/$uid?apikey=$apiKey"
	
	Note: It is uid that is to be replace in above command and not id
	
	newman run  "https://api.getpostman.com/collections/15403473-296ab3b8-9d13-407b-a3b4-9c10815e4c79?apikey=PMAK-609a586545cb530040789de5-d8cdefdd16fbcac8e11c86c324a1876b61" \
	    --environment "https://api.getpostman.com/environments/15403473-d65a1a64-3fbc-4be6-bfb5-b9db561596ec?apikey=PMAK-609a586545cb530040789de5-d8cdefdd16fbcac8e11c86c324a1876b61"
# 6. Run the report to generate HTML Extra Report
	newman run  "https://api.getpostman.com/collections/15403473-6503bbaf-0bf2-ecd4-9a26-02e95f4ab915?apikey=PMAK-609a586545cb530040789de5-d8cdefdd16fbcac8e11c86c324a1876b61" \
	    --environment "https://api.getpostman.com/environments/15403473-d65a1a64-3fbc-4be6-bfb5-b9db561596ec?apikey=PMAK-609a586545cb530040789de5-d8cdefdd16fbcac8e11c86c324a1876b61"  -r htmlextra

	newman run  "https://api.getpostman.com/collections/15403473-6503bbaf-0bf2-ecd4-9a26-02e95f4ab915?apikey=PMAK-609a586545cb530040789de5-d8cdefdd16fbcac8e11c86c324a1876b61" \
	    --environment "https://api.getpostman.com/environments/15403473-d65a1a64-3fbc-4be6-bfb5-b9db561596ec?apikey=PMAK-609a586545cb530040789de5-d8cdefdd16fbcac8e11c86c324a1876b61"  --reporters cli,htmlextra
# 7. Setting runtime environment variables
	var jsonData = pm.response.json();
	postman.setEnvironmentVariable("authtoken","Token "+jsonData.user.token)
	
# 8. Scope of variables 
	

# 9. Pm.variables.get("key") // This is a scoped getter.This will get the value from the narrowed scope that postman determines as good as {{accessToken}}.
# 10. Pm.globals.get("Key") //This will fetch the value from global scope
# 11. Pm.environments.get("key") //This will fetch the value from environment scope.
# 12. To send a request from pre-request step generate the required code by clicking code beside cookies under send button in postman and select node.js-Request
# 13. Import a request from a curl command.
		a. Go to angular.realworld.io
		b. Create an article
		c. Check the network tab of developer tool and see XHR call
		d. Right click on the command and copy as curl(bash)
		e. Import as raw text in postman
# 14. Generate a java script equivalent code in pre-request script
		a.  Beside save button click on the code </> icon and select node-js request from drop down and the code is avaialble to copy paste and use.
		b. Generate a send request code from snippet and it will work
		
# 15. General Troubleshooting
		a. Check if the service is up and running in browser
		b. Check if right protocol is used (http/https)
		c. Check that the url is correctly spelled
		d. Disable SSL certificates as applicable
# 16. Path Params are defined like http://example.com/:id
		a. Here :id is path param. Multiple path params are separated  by "/" :id makes its editable in postman params
		b. Any thing following "?" is a query param. Multiple query params are separated by "&"
# 17. Basic Work Flow in postman
		a. Postman.setNextRequest("Request 3") //this will ensure the next request3 is executed after the current request.
		b. Postman.setNextRequest(null) //this will stop the execution further after current request.
		c. If postman.setNextRequest(null) is not present in the redirected requests, it will continue its natural flow and might endup in endless loop
		d. To overcome the above loop we can use if condition with a global variable to track howmany times it ran.
# 18. Pm.info.requestName //this will return the request name as String
# 19. Pm.info.requestid //this will return the id of the request as a string.
# 20. Pm.iterationData.get("<<name of the variable>>") // this can be used for assertions in tests with external data
# 21. Parsing Response
		a. pm.respone.json()  //get the json response body
		b. xml2Json(responseBody) // get xml response body as json
		c. cheerio(pm.response.text()) // get html response body
		d. pm.response.text() //get plain-text response body
		e. csv-parse/lib/sync //get csv response body
# 22. Chai Assertion Library
		a. https://www.chaijs.com/api/bdd/
			i. Ex: expect({a: 1, b: 2}).to.not.have.any.keys('c', 'd');
		b. Pm.expect(a).to.eql(b) //this will check if the object values are equal
		c. Pm.expect(a).to.equal(b) //this will check if both objects (references) are same
		d. Pm.expect(a).to.not.eql(b) //this will check if the object values are equal
		e. Pm.expect(true).to.be.true
# 23. Papa Parse for CSV parsing
# 24. For Loop
	For(let filter of jsondata.filters){
	Console.log(filter)
	}
# 25. If the json property itself is some random value like 5sdferwer34sdfe then use the below syntax to retrieve its vlaue
		a.  json['5sdferwer34sdfe '] //this will work
		b. Json.5sdferwer34sdfe  //this will fail
# 26. Fetching a dynamic property
		a. Use .hasOwnProperty with a conditional statement to identify 
# 27. Alternate way to find an item instead of looping
		a. Const person = response.find(item=>item.name==="jane")
# 28. Headers
	This is how you retrieve a header from the response:
	pm.response.headers.get('X-Cache') 
	and in a test:
	Header exists: pm.response.to.have.header(X-Cache'); 
	Header has value: pm.expect(pm.response.headers.get('X-Cache')).to.eql('HIT'); 
# 29. Cookies
	In a similar fashion you can test cookies as well.
	Cookie exists:
	pm.expect(pm.cookies.has('sessionId')).to.be.true; 
	Cookie has value:
	pm.expect(pm.cookies.get('sessionId')).to.eql(’ad3se3ss8sg7sg3'); 
# 30. Authentication Types
		a. Basic Auth
			i. In Authorization tab select Type as Basic auth and enter username and password
			ii. In headers automatically Authorization : <base64 encoded string equivalent of Basic  username:password is generated>
				Ex: Basic postman:password get converted to Basic cG9zdG1hbjpwYXNzd29yZA== 
	Note: Encoding/Decoding can be checked at https://codebeautify.org/base64-decode
	
# Important Resources
* https://postman-quick-reference-guide.readthedocs.io/en/latest/cheatsheet.html
* https://designer.mocky.io/design
* https://www.chaijs.com/api/bdd/
* https://requestbin.com/
* https://learning.postman.com/docs/running-collections/using-newman-cli/command-line-integration-with-newman/#:~:text=The%20easiest%20way%20to%20run,to%20share%20as%20a%20file.&text=You%20can%20also%20pass%20a%20collection%20as%20a%20URL%20by%20sharing%20it.
* https://github.com/postmanlabs/newman
* https://swapi.dev/
* https://learning.postman.com/docs/developer/echo-api/
* https://codebeautify.org/base64-decode
* https://datatracker.ietf.org/doc/html/rfc6749#section-1.3.1
* https://github.com/public-apis/public-apis
