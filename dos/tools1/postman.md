# dos:devopssec
## tools
### postman
#### test
- const responseJson = pm.response.json();
- console.log(responseJson.access_token);
- pm.environment.set("token", responseJson.access_token);
- console.log(pm.environment.get("token"));
- pm.globals.set("token", responseJson.access_token);
- pm.globals.get("token");
- console.log(pm.globals.get("token"));

#### Variables

##### Getting variables in the Request Builder
- Request URL: http://{{domain}}/users/{{userId}}
Headers (key:value): X-{{myHeaderName}}:foo
Request body: {"id": "{{userId}}", "name": "John Doe"}


##### Global variables
- 
    ```
        Setting
    pm.globals.set('myVariable', MY_VALUE);
    Getting
    pm.globals.get('myVariable');
    Alternatively, depending on the scope:
    pm.variables.get('myVariable');
    Removing
    Remove one variable
    pm.globals.unset('myVariable');
    Remove ALL global variables (rather unusual)
    pm.globals.clear();
    
    ```


##### Collection variables
-   Setting
    pm.collectionVariables.set('myVariable', MY_VALUE);
    Getting
    pm.collectionVariables.get('myVariable');
    Removing
    pm.collectionVariables.unset('myVariable');


##### Environment variables
- When to use:
• storing environment specific information
• URLs, authentication credentials
• passing data to other requests

- Setting
pm.environment.set('myVariable', MY_VALUE);
Getting
pm.environment.get('myVariable');
Depending on the closest scope:
pm.variables.get('myVariable');
Removing
Remove one variable
pm.environment.unset("myVariable");
Remove ALL environment variables
pm.environment.clear();

##### Data variables
##### Local variables
- When to use:
• whenever you would like to override all other variable scopes—for whatever reason. Not sure though then
this is needed.
- Setting
pm.variables.set('myVariable', MY_VALUE);
Getting
pm.variables.get('myVariable', MY_VALUE);
##### Dynamic variables
##### Logging / Debugging variables
- var myVar = pm.globals.get("myVar");
console.log(myVar);
#####


####  Assertions

##### e assertions inside a pm.test callback.
- pm.test("Your test name", function () {
var jsonData = pm.response.json();
pm.expect(jsonData.value).to.eql(100);
});
- pm.response.to.have.status(200);
- pm.expect(pm.response.code).to.be.oneOf([201,202]);

- Response time pm.expect(pm.response.responseTime).to.be.below(9);
##### Headers Cookies

- pm.response.to.have.header('X-Cache');
- pm.expect(pm.response.headers.get('X-Cache')).to.eql('HIT');
- pm.expect(pm.cookies.has('sessionId')).to.be.true;
- pm.expect(pm.cookies.get('sessionId')).to.eql('ad3se3ss8sg7sg3');

##### Body
- pm.response.to.have.body("OK");
pm.response.to.have.body('{"success"=true}');
- pm.expect(pm.response.text()).to.include('Order placed.');
- const response = pm.response.json();
- pm.expect(response.age).to.eql(30);
pm.expect(response.name).to.eql('John');
pm.expect(response.products.0.category).to.eql('Detergent');
- Convert XML body to JSON:
const response = xml2Json(responseBody);



##### Skipping tests Failing tests

- pm.test.skip("Status code is 200", () => {
pm.response.to.have.status(200);
});
- pm.expect.fail('This failed because ...');

#### Postman Sandbox

##### pm.sendRequest
- pm.sendRequest('https://httpbin.org/get', (error, response) => {
if (error) throw new Error(error);
console.log(response.json());
});
- const payload = { name: 'John', age: 29};
const options = {
method: 'POST',
url: 'https://httpbin.org/post',
header: 'X-Foo:foo',
body: {
mode: 'raw',
raw: JSON.stringify(payload)
}
};
pm.sendRequest(options, (error, response) => {
if (error) throw new Error(error);
console.log(response.json());
});

- Form-data POST request (Postman will add the multipart/form-data header):
const options = {
'method': 'POST',
'url': 'https://httpbin.org/post',
'body': {
'mode': 'formdata',
'formdata': [
{'key':'foo', 'value':'bar'},
{'key':'bar', 'value':'foo'}
]
}
};
pm.sendRequest(options, (error, response) => {
if (error) throw new Error(error);
console.log(response.json());
});

##### Postman Echo & Workflows
- pm.sendRequest('https://postman-echo.com/time/now', function (err, res) {
if (err) { console.log(err); }
else {
var currentTime = res.stream.toString();
console.log(currentTime);
pm.environment.set("currentTime", currentTime);
}
});
- Set which will be the next request to be executed
postman.setNextRequest(“Request name");
Stop executing requests / stop the collection run
postman.setNextRequest(null);




#### Request creation 

##### QA1
- How can I create or modify the request body?
You can use console.log(pm.request.body) to understand the current data structure of the request body. With the
method pm.request.body.update you can update the request.
- How can I modify the request headers?
You can modify the request headers from the Pre-request script as follows
- Add header
pm.request.headers.add({
key: 'X-Foo',
value: 'Postman'
});
Remove header
pm.request.headers.remove('User-Agent'); // may not always work
Update header
pm.request.headers.upsert(
{
key: "User-Agent",
value: "Not Postman"
}
);
- How to generate random data?
{
"GroupName":"GroupName_{{$guid}}",
"Description": "Example_API_Admin-Group_Description"
}
- How to trigger another request from pre-request script?
n from the pre-request script using postman.
postman.setNextRequest('Your request name as saved in Postman');
var options = { method: 'GET',
url: 'http://www.mocky.io/v2/5a849eee300000580069b022'
};
pm.sendRequest(options, function (error, response) {
    if (error) throw new Error(error);
var jsonData = response.json();
pm.globals.set('name', jsonData.name);
});

##### Dynamic variables
- Variable
        ```
    name
    Description Example
    $guid Generates a GUID (Globally Unique Identifier) in
    v4
    15aacbb1-1615-47d8-b001-
    e5411a044761
    $timestamp Returns the current timestamp 1561013396
    $randomInt Generates random integer between 0 and 1000 764
        ```

##### QA2
- How to send request with XML body from a script?
const xmlBody = `<?xml version="1.0"?>
<catalog>
<book id="bk101">
<author>Gambardella, Matthew</author>
<title>XML Developer's Guide</title>
<genre>Computer</genre>
<price>{{price}}</price>
<publish_date>2000-10-01</publish_date>
<description>An in-depth look at creating applications
with XML.</description>
</book>
</catalog>`;
const options = {
'method': 'POST',
'url': 'httpbin.org/post',
'header': {
'Content-Type': 'application/xml'
},
body: pm.variables.replaceIn(xmlBody) // replace any Postman variables
}
pm.sendRequest(options, function (error, response) {
if (error) throw new Error(error);
console.log(response.body);
});

- How to pass arrays and objects between requests?
var jsonData = pm.response.json();
pm.environment.set('myData', JSON.stringify(jsonData));
- How to add a delay between Postman requests?
setTimeout(() => {}, 10000);

##### JavaScript libraries
- Built-in JavaScript libraries
- Read more: https://github.com/cheeriojs/cheerio :y for working with the DOM model
- Read more: https://momentjs.com/docs working with dates
- Read more: https://www.npmjs.com/package/crypto-js  implements different crypto functions
- NodeJS modules that are available inside Postman: • path • assert • buffer • util • url • punycode • querystring • string_decoder • stream • timers • events
- How to read links from response and execute a request for each of them?
links.forEach(function(link) {
pm.test("Status code is 404", function () {
pm.sendRequest(link, function (err, res) {
pm.expect(res).to.have.property('code', 404);
});});});

#### references

- https://postman-quick-reference-guide.readthedocs.io/_/downloads/en/latest/pdf/
- https://fakerjs.dev/api/date.html