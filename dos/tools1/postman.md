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
