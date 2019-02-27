#List of Job Search Api's(UK Region)

- Indeed(<http://opensource.indeedeng.io/api-documentation/docs/job-search/>)
- Adzura(<https://developer.adzuna.com/docs/search>)
- Reed.co.uk(<https://www.reed.co.uk/developers/Jobseeker>)
- Authentic Jobs API(<https://authenticjobs.com/api/docs#introduction>)
- AdView’s FeedAPI(<https://adview.online/publisher/intro/tech-feed-api.html>)
- GitHub Jobs API(<https://jobs.github.com/api>)
#1. Indeed

##Job Search API
Use the Job Search API to submit job searches and return results from your website.

###Prerequisite
Create a free Publisher account to receive a Publisher ID and access to job data. Once you create this account, Indeed provides reports and earnings for your traffic.

###Search request example
The following example shows a search request for Java developers (q) in Austin, TX (l):

	http://api.indeed.com/ads/apisearch?publisher=123412341234123&q=java+developer&l=austin%2C+tx&sort=&radius=&st=&jt=&start=&limit=&fromage=&filter=&latlong=1&co=us&chnl=&userip=1.2.3.4&useragent=Mozilla/%2F4.0%28Firefox%29&v=2
You must specify the following parameters in your search request:

	Parameter	Type	Required	Description
	publisher	string	Yes			Publisher ID. (Indeed assigns the Publisher ID after you create a Publisher account. Locate this ID on the XML Feed tab of your Publisher account.)
	v			int		Yes			Version of the API. (You must set this value to 2.)
	userip		string	Yes			The IP address of the end user who will view job results from your website.
	useragent	string	Yes			The browser of the end user who will view job results from your website. You can obtain this parameter using the User-Agent HTTP 		request header 		from the end user.(Refer to the complete list of parameters for more details on effectively customizing your search.)

##Search response examples
Note: If you don’t specify a response format, the API returns XML by default.


JSON example
Click to expand example

	{  
	    "version":2,
	    "query":"java",
	    "location":"austin, tx",
	    "dupefilter":true,
	    "highlight":false,
	    "radius":25,
	    "start":1,
	    "end":10,
	    "totalResults":547,
	    "pageNumber":0,
	    "results":[  
	        {  
	            "jobtitle":"Java Developer",
	            "company":"XYZ Corp.,",
	            "city":"Austin",
	            "state":"TX",
	            "country":"US",
	            "formattedLocation":"Austin, TX",
	            "source":"Dice",
	            "date":"Mon, 02 Aug 2017 16:21:00 GMT",
	            "snippet":"looking for an object-oriented Java Developer... Java Servlets,
	              HTML, JavaScript, AJAX, Struts, Struts2, JSF) desirable. Familiarity with
	              Tomcat and the Java...",
	            "url":"http://www.indeed.com/viewjob?jk=12345&indpubnum=8343699265155203",
	            "onmousedown":"indeed_clk(this, '0000');",
	            "latitude":30.27127,
	            "longitude":-97.74103,
	            "jobkey":"12345",
	            "sponsored":false,
	            "expired":false,
	            "indeedApply":true,
	            "formattedLocationFull":"Austin, TX",
	            "formattedRelativeTime":"11 hours ago"
	        }
	    ]
	}
#Request parameters
	Parameter	Type	Required	Description	Default
	publisher	string	Yes			Publisher ID. 
	v			int		Yes			Version of the API. 
	userip		string	Yes			The IP address of the end user who will view job results from your website.
	useragent	string	Yes			The browser of the end user who will view job results from your website. 
	callback	string	No			The name of JavaScript callback function for passing search results. This parameter applies only when format is json. 

Note: For security reasons, you must restrict the callback name to letters, numbers, and the underscore character.	Empty
q	string	No	Query. By default, terms are ANDed. 

	Tip: To format the search words for q, perform your search from the Job Search page. The URL displays the expected formatting for this parameter. For example, q=developer or q=java+developer.	Empty. Searches all jobs.
	l	string	No	Location. Use a postal code or a "city, state/province/region" combination. For example, l=Austin%2C+TX. 

Tip: Use the Job Search or Advanced Job Search page and inspect the URL to see how to encode your parameter values.	Empty. Searches all locations.
sort	string	No	Sort by relevance or date.	relevance
radius	int	No	Distance from the search location (point-to-point aerial transit path, or "as the bird flies"). 



Display meaningful results
Include the following response data on your website to ensure relevant results:

Title

Location

Job description snippet

Company name

#2. Adzura
##Overview
Adzuna has created a RESTful API. Currently, the API consists of list of endpoints that can be split into the following sections:

###Get ads
The search endpoints allow you to query our database of job, property or car ads.

###Get employment data
Four endpoints expose the latest trends in salaries and vacancies. Historical salary data shows how salaries are changing over time. The histogram returns the distribution of current salaries. And the regional data and top companies endpoints show the current number of vacancies by region or company.

###Categories
Use the categories endpoint to see the categories that Adzuna applies to jobs and properties

#Querying the API
The root URL of the API is located at:

	http://api.adzuna.com/v1/api
Notice that it needs to be appended with the version you're querying. You then concatenate the endpoint you want to query, for example to get Property listings in the UK:

	http://api.adzuna.com/v1/api/property/gb/search/1
... and finally you will always need to pass two obligatory parameters. The app_id and app_key, making the final call look like this:

	http://api.adzuna.com/v1/api/property/gb/search/1?app_id={YOUR_APP_ID}&app_key={YOUR_APP_KEY}

- app_id={YOUR_APP_ID}

- app_key={YOUR_APP_KEY}

	 app_id and app_key are available once you get registered into adzuna.com site 

Search
Use this endpoint to retrieve Adzuna's job, property and car advertisement listings.

Visit the Interactive Endpoint Documentation for full technical details and a playground to make test calls.

##Example #1: Simple jobs query
To get twenty "Javascript Developer" jobs in the whole of UK, in JSON format, issue a GET request to:

	-http://api.adzuna.com/v1/api/jobs/gb/search/1?app_id={YOUR API ID}&app_key={YOUR API KEY}&results_per_page=20&what=javascript%20developer&content-type=application/json
The response (certain long fields have been cropped in the example below) looks

something like:

	{  "__CLASS__": "Adzuna::API::Response::JobSearchResults",  "results": [
    {
      "salary_min": 50000,
      "longitude": -0.776902,
      "location": {
        "__CLASS__": "Adzuna::API::Response::Location",
        "area": [
          "UK",
          "South East England",
          "Buckinghamshire",
          "Marlow"
        ],
        "display_name": "Marlow, Buckinghamshire"
      },
      "salary_is_predicted": 0,
      "description": "JavaScript Developer Corporate ...",
      "__CLASS__": "Adzuna::API::Response::Job",
      "created": "2013-11-08T18:07:39Z",
      "latitude": 51.571999,
      "redirect_url": "http://adzuna.co.uk/jobs/land/ad/129698749...",
      "title": "Javascript Developer",
      "category": {
        "__CLASS__": "Adzuna::API::Response::Category",
        "label": "IT Jobs",
        "tag": "it-jobs"
      },
      "id": "129698749",
      "salary_max": 55000,
      "company": {
        "__CLASS__": "Adzuna::API::Response::Company",
        "display_name": "Corporate Project Solutions"
      },
      "contract_type": "permanent"
    },
    ... another 19 ads here ...
			]
		}


##Example #2: Complex jobs query
There are lots of parameters you can use to enhance your query. In this example, we want javascript developers with salaries over 50k (salary_min=50000), full time (full_time=1) and permanent (permanent=1) positions, to reduce ambiguity we exclude any ads that contain the keyword "Java" (what_exclude=java), we limit the results to London (where=london) and we sort by salary (sort_by=salary). The resulting GET call:

	http://api.adzuna.com:80/v1/api/jobs/gb/search/1?app_id={YOUR_APP_ID}&app_key={YOUR_APP_KEY}&results_per_page=20&what=javascript%20developer&what_exclude=java&where=london&sort_by=salary&salary_min=30000&full_time=1&permanent=1&content-type=application/json

will return:

	{"__CLASS__": "Adzuna::API::Response::JobSearchResults",
  	"results": [
    {
      "salary_min": 55000,
      "location": {
        "__CLASS__": "Adzuna::API::Response::Location",
        "area": [
          "UK",
          "London",
          "Central London",
          "The City"
        ],
        "display_name": "The City, Central London"
      },
      "salary_is_predicted": 0,
      "description": "...  and experience with more than one language a distinct advantage (python/ruby/perl/javascript/erlang).The Senior Developer Python will be involved in helping us to scale up and develop ...",
      "__CLASS__": "Adzuna::API::Response::Job",
      "created": "2013-10-23T19:32:43Z",
      "redirect_url": "http://adzuna.co.uk/jobs/land/ad/126977586?v=712F911142DFEF191FB2F0E068CD2734177B7F7E&utm_medium=api&utm_source=6eda9a47",
      "contract_time": "full_time",
      "title": "Senior Developer Python",
      "category": {
        "__CLASS__": "Adzuna::API::Response::Category",
        "label": "IT Jobs",
        "tag": "it-jobs"
      },
      "id": "126977586",
      "salary_max": 55000,
      "company": {
        "__CLASS__": "Adzuna::API::Response::Company",
        "display_name": "Exposed Solutions Limited"
      },
      "contract_type": "permanent"
    },
    ... up to another 19 ads here ...
 	 		]
		}

#3. Reed.co.uk Api
##Jobs - Search - Parameter
This API runs a search of all the jobs on the reed site and returns a list of jobs which match the parameters.

	Sign up (Register) for reed.co.uk to access the API Key.

Criteria Name			Possible Values
 	
-	employerId - id of employer posting job

-	employerProfileId -	profile id of employer posting job

-	keywords -	any search keywords

-	locationName -	the location of the job

-	distanceFromLocation -	distance from location name in miles (default is 10)

-	permanent -	true/false

-	contract -	true/false

-	temp -	true/false

-	partTime -	true/false

-	fullTime -	true/false

-	minimumSalary -	lowest possible salary e.g. 20000

-	maximumSalary -	highest possible salary e.g. 30000

-	postedByRecruitmentAgency -	true/false

-	postedByDirectEmployer- 	true/false

-	graduate -	true/false

-	resultsToTake -	maximum number of results to return (defaults and is limited to 100 results)

-	resultsToSkip -	number of results to skip (this can be used with resultsToTake for paging)

	Notes:
	Only one of employerId and employerProfileId can be set. Profile Id will be selected over Employer Id. Not all employers have a profile and therefore do not have a profile id.

##Jobs - Search - Returns
List of jobs matching the criteria. Each job contains the following information:

- Job 

- IdEmployer 

- IdEmployer
 
- NameEmployer 

- Profile 

- IdJob
 
- TitleDescriptionLocation 

- NameMinimum 

- SalaryMaximum 

- Salary


		Notes:
		If the job salary has been set as hidden on reed.co.uk, none of the salary information will show.

If a location is used which could apply to more than one place the best match is used for the search and a list of alternatives is provided.

##Jobs - Search - Implementation
Use the following url structure to access the API::

	 https://www.reed.co.uk/api/{versionnumber}/search?keywords={keywords}&loc ationName={locationName}&employerId={employerId}&distanceFromLocation={distance in miles}
Follow this structure for each parameter you wish to search with.

If you do not want to use any of these parameters simply leave them out. e.g

	https://www.reed.co.uk/api/1.0/search?keywords=accountant&location=london&employerid=123&distancefromlocation=15

If no jobs match the search parameters an empty list will be returned. If there is more than one location match, these will also be returned.

Important:
You will need to include your api key for all requests in a basic authentication http header as the username, leaving the password empty.


Notes:
If the job salary has been set as hidden on reed.co.uk, none of the salary information will show.

##Jobs - Details - Implementation
Use the following url to access this API:

	https://www.reed.co.uk/api/{version number}/jobs/{Job Id} e.g. https://www.reed.co.uk/api/1.0/jobs/132
If no jobs match a blank job will be returned.

Important:
You will need to include your api key for all requests in a basic authentication http header as the username, leaving the password empty.



#4. Authentic Jobs API

(Reference: <https://authenticjobs.com/api/docs#introduction>)

##Introduction

Provided below is documentation for the implementation and use of the official Authentic Jobs API. You need your own API key to use the Authentic Jobs API, and you can request an API key if you haven't already done so.

Every call to the AJ API consists of the following:
The base URL is: https://authenticjobs.com/api/
-	An API key, passed as the parameter api_key (e.g. api_key=a446a0eefe6f5699283g34f4d5b51fa0).
-	The method to call, passed as the parameter method (e.g. method=aj.jobs.search). See the methods article below for a list of available methods.
An (optional) response format, passed as the parameter format. Valid formats are: rest, json, and php. The default is XML.
All requests must currently be GET requests
All replies are in utf8


Response Formats
There are currently three valid response formats: XML, JSON, and PHP. The default format is XML.
	XML
	
	EXAMPLE
	<?xml version="1.0" encoding="utf-8" ?>
	<rsp stat="ok">
	<categories>
	  <category id="1" name="Design" />
	  <category id="2" name="Development" />
	</categories>
	</rsp>

	JSON
	EXAMPLE
	{
	  "categories": {
	    "category": [
	      {
	        "id": "1",
	        "name" :"Design"
	      },
	      {
	        "id": "2",
	        "name": "Development"
	      }
	    ]
	  },
	  "stat": "ok"
	}

##Job Search (aj.jobs.search)
Returns a list of current positions, filtered by optional parameters. The response is split into multiple pages, if necessary.

##Security
All methods require an API key, and each separate application should have its own key. Methods do not currently require signing, but some or all may in the future. To sign an api call, perform the following steps:

1. Take your list of parameters and sort it alphabetically. For example, if you’re passing the api_key, method, company, and perpage parameters, alphabetical order would be: api_key, company, method, perpage. All parameters must be included, with the exception of api_sig.

2. Concatenate together your sorted list of key/value parameters. For example, api_key=foo, method=aj.jobs.search, company=flickr, and perpage=api_keyfoocompanyflickrmethodaj.jobs.searchperpage100.

3. Append your shared secret to the end of your concatenated string. (Note: Shared secrets are currently not being distributed.)

4. Create an md5 signature of your string. This is your signature.

5. Append the signature to your API call as the api_sig parameter.

##Rules
-	Please try to not call a given method more than once per minute. For calls to methods that do not change often (e.g. aj.types.getList), heavy caching is recommended. Other methods should be cached as appropriate.
-	Please use a separate API key per application
-	Please do not give your API key or shared secret to anyone else
-	API keys can be disabled, and will be if they are causing problems
-	API keys for any websites that involve adult content will be terminated immediately
-	All applications must link back to the Authentic Jobs website in a prominent location

###PARAMETERS
-	Category :	The id of a job category to limit to. See aj.categories.getList
-	Type : 	The id of a job type to limit to. See aj.types.getList

-	Sort :		Accepted values are: date-posted-desc (the default) and date-posted-asc
-	Company :	Free-text matching against company names. Suggested values are the ids from aj.jobs.getCompanies

-	Location :	Free-text matching against company location names. Suggested values are the ids from aj.jobs.getLocation
-	Telecommuting :	Set to 1 if you only want telecommuting jobs
-	Keywords :	Keywords to look for in the title or description of the job posting. Separate multiple keywords with commas.
-	begin_date :	Unix timestamp. Listings posted before this time will not be returned
-	end_date :	Unix timestamp. Listings posted after this time will not be returned
-	page :	The page of listings to return. Defaults to 1.
-	Perpage  :	The number of listings per page. The default value is 10. The maximum value is 100.

		EXAMPLE
		https://authenticjobs.com/api/?api_key=a446a0eefe6f5699283g34f4d5b51fa0&method=aj.jobs.search&keywords=php,mysql&perpage=1
		<?xml version="1.0" encoding="utf-8" ?>
		<rsp stat="ok">
		<listings total="10" perpage="1" page="1" pages="10">
		  <listing id="1569" title="You bring the talent and we'll provide the adventure..." description="..." perks="..." howto_apply="..." post_date="2007-12-07 14:13:27">
		    <category id="1" name="Design" />
		    <type id="1" name="Full-time" />
		    <company id="yakabodinc" name="Yakabod, Inc." url="http://www.yakabod.com">
		      <location id="frederickmdus" name="Frederick, MD" city="Frederick" country="US" lat="39.4142688" lng="-77.4105409" state="MD" />
		    </company>
		  </listing>
		</listings>
		</rsp>



#5. AdView’s FeedAPI

###How Our FeedAPI Works
 
 
The process begins with a user making a request to see jobs, and we will send them your way. It’s simple, we retrieve the jobs and you display them. Just make sure to set up the correct tracking information, so we can pay you for the clicks you send.

 
	Note:
	AdView’s database is constantly being updated. Therefore, you shouldn’t download the jobs, store them in your database, and then display them on your website. This will break the tracking and we won’t be able to pay you. Instead, you should retrieve the jobs as your users search and display them in real time.

Have a look at the diagram below to understand the process:
![](adview_api.png)

 
##AdView’s FeedAPI. Your First Request
 
 
Open your browser, paste the following URL and press enter:

	https://adview.online/api/v1/jobs.xml?publisher=6&keyword=sales&location=london
 
The above URL is the same as:

	https://adview.online/api/v1/jobs.xml?
	publisher=6
	&keyword=sales
	&location=london

##Simple Response Example  

AdView API returns the jobs in chosen format, JSON or XML. Below is an simplified version of a job in XML format.


	<job>
	    <title>Telesales Sales Executive</title>
	    <company>AdView</company>
	    <location>London</location>
	    <postcode>WC2B</postcode>
	    <snippet> Responsibility and training and will be able to accelerate your.. </snippet>
	    <url>https://adview.online/dispatch/job/publisher/telesales-sales-executive-8?pid=7&psrc=feed&ptkn=9267e6154f</url>
	    <onmousedown>pnpClick(this,'58e4bca44c104');</onmousedown>
	    <job_type>temporary</job_type>
	    <salary>£20k - £25k pa + ote</salary>
	    <age> 10 hours ago</age>
	    <age_days>0</age_days>
	</job>
 
##Optional Parameters  
 
For the most part you will be using optional parameters to customize your search, as per user requirement. You would need to grab the user information and pass it onto the API, along with the specific parameter names. For instance, if a user searched for ‘engineer’, you would pass this information to the API in the ‘keyword’ parameter. Below is the list of parameters that the API accepts:

 
	Parameter_Name	Accepted Type	Description

	keyword	  		String			Retrieve job listings containing these term/s.
	location		String			Jobs in specified location. Your can provide any one of the following info: county, region, postcode or town.
	radius			Integer			This gets jobs within X miles radius. So for instance, you might want jobs within 10 miles, you can set it like so: radius=10. Accepted values range from 0 to 50. Note: If passed 0 then API will do exact match. 20 is default radius for all the queries.
	job_type		String			Type of job: permanent, temporary, contract, placement student, seasonal.
	salary_from		Integer			Get jobs that pay more than. People often want to filter the salaries, this sets a minimum amount for salary.
	salary_to		Integer			Get jobs that pay salary below.

	sort			String			Sort job either by ‘date’, ‘relevance’ or 'distance'.

	limit			Limit			How many jobs to fetch, max is 50 and default is 20. Tell AdView how many jobs you would like to get per request.
	user_agent		String			User browser user agent.
	
	channel			Integer			Channel name is used to categorise your tracking reports. You could be using the FeedAPI on different parts of your site, use channel names to differentiate the sections or pages and get individual reports.
	snippet			String			Set this parameter to either 'basic', 'highlight' or 'full' to change the snippet mode. Default is 'highlight’.
	mode			String			Default mode is ‘basic’. ‘advanced’ mode is also available. Refer to the Advanced vs Basic search mode diagram for more info.


#6. The GitHub Jobs API
The GitHub Jobs API allows you to search, and view jobs with JSON over HTTP.

To get the JSON representation of any search result or job listing, append .json to the URL you'd use on the HTML GitHub Jobs site.

For example, when searching for Python jobs near New York on the site I am taken to this url:

	https://jobs.github.com/positions?description=python&location=new+york

To get the JSON representation of those jobs I just use positions.json:

	https://jobs.github.com/positions.json?description=python&location=new+york

Pagination
The API also supports pagination. /positions.json, for example, will only return 50 positions at a time. You can paginate results by adding a page parameter to your queries.

Pagination starts by default at 0.

##Examples

	https://jobs.github.com/positions.json?description=ruby&page=1
	https://jobs.github.com/positions.json?page=1&search=code

GET /positions.json
Search for jobs by term, location, full time vs part time, or any combination of the three. All parameters are optional.

Parameters

	description — A search term, such as "ruby" or "java". This parameter is aliased to search.
	location 	— A city name, zip code, or other location search term.
	lat 		— A specific latitude. If used, you must also send long and must not send location.
	long		— A specific longitude. If used, you must also send lat and must not send location.
	full_time 	— If you want to limit results to full time positions set this parameter to 'true'.
##Examples

	https://jobs.github.com/positions.json?description=python&full_time=true&location=sf
	https://jobs.github.com/positions.json?search=node
	https://jobs.github.com/positions.json?lat=37.3229978&long=-122.0321823
GET /positions/ID.json
Retrieve the JSON representation of a single job posting.

Parameters

markdown — Set to 'true' to get the description and how_to_apply fields as Markdown.
Examples

	https://jobs.github.com/positions/21516.json
	https://jobs.github.com/positions/21516.json?markdown=true