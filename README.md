Download Link: https://assignmentchef.com/product/solved-web322-assignment-3
<br>



Build upon the foundation established in Assignment 2 by providing new routes / views to support adding new people and uploading images.

Specification:

For this assignment, we will be enhancing the functionality of Assignment 2 to include new routes &amp; logic to handle file uploads and add people.  We will also add new routes &amp; functionality to execute more focused queries for data (ie: fetch a person by id, all cars by a make or vin number, etc)

<h1>Part 1: Adding / Updating Static (.html) Files &amp; Directories</h1>




<h2><u>Step 1:</u> Modifying home.html &amp; about.html</h2>

<ul>

 <li>Open the home.html file from within the “views” folder</li>

 <li>Add the following two entries to the &lt;ul class=”nav navbar-nav”&gt; element:

  <ul>

   <li>&lt;li&gt;&lt;a href=”/people/add”&gt;Add People&lt;/a&gt;&lt;/li&gt; o &lt;li&gt;&lt;a href=”/pictures/add”&gt;Add Picture&lt;/a&gt;&lt;/li&gt;</li>

  </ul></li>

 <li>Add the following entry as the first child element of the &lt;ul class=”nav navbar-nav navbar-right”&gt; element

  <ul>

   <li>&lt;li&gt;&lt;a href=”/pictures”&gt;Pictures&lt;/a&gt;&lt;/li&gt;</li>

  </ul></li>

 <li>Your “Home” page should now have a menu bar that looks like the following:</li>

</ul>







<ul>

 <li>Update your “About” page with the same changes. When complete, it should look like the following:</li>

</ul>







<h2><u>Step 2:</u> Adding new routes in server.js to support the new views</h2>

   Inside your server.js file add the following routes (HINT: do not forget __dirname &amp; path.join):

<ul>

 <li>GET /people/add

  <ul>

   <li>This route simply sends the file “/views/addPeople.html “</li>

  </ul></li>

 <li>GET /images/add

  <ul>

   <li>This route simply sends the file “/views/addImage.html</li>

  </ul></li>

</ul>

<h2><u>Step 3:</u> Adding new file 1: addPeople.html</h2>

<ul>

 <li>Create a new file in your “views” directory called “addPeople.html” and open it for editing</li>

 <li>Copy the contents of “home.html” and paste it in as a starting point.</li>

 <li>Ensure that the “Add People” item in the &lt;ul class=”nav navbar-nav”&gt; …&lt;/ul&gt; element is the only &lt;li&gt; with the class “active” (this will make sure the correct navigation element is “highlighted”)</li>

 <li>Remove all html code inside the &lt;div class=”row”&gt; … &lt;/div&gt;</li>

 <li>Inside the (now empty) &lt;div class=”row”&gt; … &lt;/div&gt; element, use the html from the sample solution</li>

</ul>

( <u>https://secret-brook-17817.herokuapp.com/people/add</u>) to reconstruct the “Add People” form (HINT: You can right-click the page to “view source” – the html you want is within the &lt;div class=”row”&gt; …&lt;/div&gt; element)

<h2><u>Step 4:</u> Adding new file 2: addImage.html</h2>

<ul>

 <li>Create a new file in your “views” directory called “addImage.html” and open it for editing</li>

 <li>Copy the contents of “home.html” and paste it in as a starting point.</li>

 <li>Ensure that the “Add Image” item in the &lt;ul class=”nav navbar-nav”&gt; …&lt;/ul&gt; element is the only &lt;li&gt; with the class “active” (this will make sure the correct navigation element is “highlighted”)</li>

 <li>Remove all html code inside the &lt;div class=”row”&gt; … &lt;/div&gt;</li>

 <li>Inside the (now empty) &lt;div class=”row”&gt; … &lt;/div&gt; element, use the html from the sample solution</li>

</ul>

( <u>https://secret-brook-17817.herokuapp.com/pictures/add</u>) to reconstruct the “Add Image” form (HINT: You can right-click the page to “view source” – the html you want is within the &lt;div class=”row”&gt; …&lt;/div&gt; element)

<h2><u>Step 5:</u> Adding a home for the uploaded Images</h2>

<ul>

 <li>Create a new folder in your “public” folder called “pictures”</li>

 <li>Within the newly created “pictures” folder, create an “uploaded” folder</li>

</ul>




<h1>Part 2: Adding Routes / Middleware to Support Image Uploads</h1>




<h2><u>Step 1:</u> Adding multer</h2>

<ul>

 <li>Use npm to install the “multer” module</li>

 <li>Inside your server.js file “require” the “multer” module as “multer”</li>

 <li>Define a “storage” variable using “multer.diskStorage” with the following options (HINT: see “Step 5: (server) Setup…” in the <u>week 5 course notes</u> for additional information)

  <ul>

   <li>destination “./public/pictures/uploaded”</li>

   <li>filename function (req, file, cb) {       cb(null, Date.now() + path.extname(file.originalname));</li>

  </ul></li>

</ul>

}

<ul>

 <li>Define an “upload” variable as multer({ storage: storage });</li>

</ul>




<h2><u>Step 2:</u> Adding the “Post” route</h2>

    Add the following route:

o POST /pictures/add

<ul>

 <li>This route uses the middleware: upload.single(“pictureFile”)</li>

 <li>When accessed, this route will redirect to “/pictures” (defined below)</li>

</ul>

<h2><u>Step 3:</u> Adding “Get” route / using the “fs” module</h2>

<ul>

 <li>Before we can add the below route, we must include the “fs” module in our server.js file (previously only in our data-service.js module)</li>

 <li>Next, Add the following route:</li>

</ul>

o GET /pictures

   This route will return a JSON formatted string (res.json()) consisting of a single “pictures” property, which contains the contents of the “./public/pictures/uploaded” directory as an array, ie { “images”: [“1518109363742.jpg”, “1518109363743.jpg”] }.  HINT:  You can make use of the fs.readdir method, as outlined in <u>this example from code-maven.com</u>

<h2><u>Step 4:</u> Verify your Solution</h2>

At this point, you should now be able to upload images using the “/pictures/add” route and see the full file listing on the “/pictures” route in the format: { “pictures”: [“1518109363742.jpg”, “1518109363743.jpg”] } .




<h1>Part 3: Adding Routes / Middleware to Support Adding People</h1>




<h2><u>Step 1:</u> Adding body-parser</h2>

<ul>

 <li>Use npm to install the “body-parser” module</li>

 <li>Inside your server.js file “require” the “body-parser” module as “bodyParser”</li>

 <li>Add the bodyParser.urlencoded({ extended: true }) middleware (using app.use())</li>

</ul>

<h2><u>Step 2:</u> Adding “Post” route</h2>

    Add the following route:

o POST /people/add

<ul>

 <li>This route makes a call to the (promise-driven) addPeople(peopleData) function from your dataservice.js module (function to be defined below). It will provide req.body as the parameter, ie “data.addPeople(req.body)”.</li>

 <li>When the addPeople function resolves successfully, redirect to the “/people” route. Here we can verify that the new person was added</li>

</ul>

<h2><u>Step 3:</u> Adding “addPeople” function within data-service.js</h2>

     Create the function “addPeople(peopleData)” within data-service.js according to the following specification:

(HINT: do not forget to add it to module.exports) o Like all functions within data-service.js, this function must return a Promise

<ul>

 <li>Explicitly set the id property of peopleData to be the length of the “people” array plus one (1). This will have the effect of setting the first new person’s id to 1001, and so on.</li>

 <li>Push the updated peopleData object into the “people” array and resolve the promise.</li>

</ul>

<h2><u>Step 4:</u> Verify your Solution</h2>

At this point, you should now be able to add new people using the “/people/add” route and see the full people listing on the “/people” route.




Part 4: Adding New Routes &amp; queries

<h1>A) “People”</h1>




<h2><u>Step 1:</u> Update the “/people” route</h2>

 In addition to providing all of the “people”, this route must now also support the following optional filters (via the query string) o /people?vin=value

 return a JSON string consisting of all people where value is equal to a certain vin number (hint: use “3G5DB03E13S795969” to get “Catriona Farherty”)- this can be accomplished by calling the getPeopleByVin(vin) function of your data-service (defined below)

o /people

 return a JSON string consisting of all people without any filter (We have already made this in assignment 2)

<h2><u>Step 2:</u> Add the “/person/value” route</h2>

 This route will return a JSON formatted string containing the person whose id matches the value.  For example, once the assignment is complete, localhost:8080/person/61 would return the person: Catriona Farherty – – this can be accomplished by calling the getPeopleById (id) function of your dataservice (defined below).













<h1>B) “Cars”</h1>




<h2><u>Step 1:</u> Update the “/cars” route</h2>

 In addition to providing all of the “cars”, this route must now also support the following optional filters (via the query string) o /cars?vin=value

 return a JSON string consisting of all cars where value is equal to a certain vin number(hint: use “3G5DB03E13S795969” to get “1992 Infiniti Q”)- this can be accomplished by calling the getCarsByVin(vin) function of your data-service (defined below)

<ul>

 <li>/cars?make=value</li>

</ul>

 return a JSON string consisting of all cars where value is equal to a car’s make (hint:

use “Ford” to get a list of all the ford cars)- this can be accomplished by calling the getCarsByMake(make) function of your data-service (defined below)

<ul>

 <li>/cars?year=value</li>

</ul>

 return a JSON string consisting of all cars where value is equal to a car’s year (hint: use “1997” to get a list of all the cars made in 1997)- this can be accomplished by calling the getCarsByYear(year) function of your data-service (defined below)

<ul>

 <li>/cars</li>

</ul>

 return a JSON string consisting of all cars without any filter (We have already made this in assignment 2)




<h2>Part 5: Updating “data-service.js” to support the new “People” and “Cars” routes</h2>




Note: All of the below functions must return a promise (continuing with the pattern from the rest of the dataservice.js module)




<h3><u>Step 1:</u> Add the getPeopleByVin(Vin) Function</h3>

<ul>

 <li>This function will provide an array of “people” objects whose vin property matches the vin parameter, use the resolve method to return the array.</li>

 <li>If for some reason, the length of the array is 0 (no results returned), this function must invoke the reject method and pass a meaningful message, ie: “no results returned”.</li>

</ul>

<h3><u>Step 2:</u> Add the getCarsByVin(vin) Function</h3>

<ul>

 <li>This function will provide an array of “cars” objects whose vin property matches the vin parameter, use the resolve method to return the array.</li>

 <li>If for some reason, the length of the array is 0 (no results returned), this function must invoke the reject method and pass a meaningful message, ie: “no results returned”.</li>

</ul>

<h3><u>Step 3:</u> Add the getCarsByMake(make) Function</h3>

<ul>

 <li>This function will provide an array of “cars” objects whose make property matches the make parameter, use the resolve method to return the array.</li>

 <li>If for some reason, the length of the array is 0 (no results returned), this function must invoke the reject method and pass a meaningful message, ie: “no results returned”.</li>

</ul>

<h3><u>Step 4:</u> Add the getCarsByYear(year) Function</h3>

<ul>

 <li>This function will provide an array of “cars” objects whose year property matches the year parameter, use the resolve method to return the array.</li>

 <li>If for some reason, the length of the array is 0 (no results returned), this function must invoke the reject method and pass a meaningful message, ie: “no results returned”.</li>

</ul>

<h3><u>Step 5:</u> Add the getPeopleById(id) Function</h3>

<ul>

 <li>This function will provide a single “person” object whose id property matches the id parameter (ie: if id is 261 then the “people” object returned will be “Coleen Challender”) using the resolve method of the returned promise.</li>

 <li>If for some reason, the length of the array is 0 (no results returned), this function must invoke the reject method and pass a meaningful message, ie: “no results returned”.</li>

</ul>




<h2>Part 6: Pushing to Heroku</h2>

Once you are satisfied with your application, deploy it to Heroku:

<ul>

 <li>Ensure that you have checked in your latest code using git (from within Visual Studio Code)</li>

 <li>Open the integrated terminal in Visual Studio Code</li>

 <li>Log in to your Heroku account using the command heroku login</li>

 <li>Create a new app on Heroku using the command heroku create</li>

 <li>Push your code to Heroku using the command git push heroku master</li>

 <li>IMPORTANT NOTE: Since we are using an “unverified” free account on Heroku, we are limited to only 5 apps, so if you have been experimenting on Heroku and have created 5 apps already, you must delete one (or verify your account with a credit card). Once you have received a grade for Assignment 1, it is safe to delete this app (login to the Heroku website, click on your app and then click the Delete app… button under “Settings”).</li>

</ul>




<h3><u>Testing</u>: Sample Solution</h3>




To see a completed version of this app running, visit: <u>https://secret-brook-17817.herokuapp.com</u>







Please note: This solution is visible to ALL students and professors at Seneca College.  It is your responsibility as a student of the college not to post inappropriate content / images to the shared solution.  It is meant purely as an exemplar and any misuse will not be tolerated.


