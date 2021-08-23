# CRUD-Operation-uisng-JsonPowerDB
This projects demonstartes the use of JsonPowerDB database and performing POST operation to store new records in the database.<br>



## Tools/Technologies  Required
- HTML:To create a form and a webpage.
- Javascript: To aad functionality to the submit button.
- Bootstrap: Used to create form.
- JsonPowerDB: To create a database and storing data inside the database and retriving it.

## Operations that can be performed with this Form
- Create and/or data to the database.



## Explaination about  different operations
- Create and/or  Add items to  cart :(PUT REQUEST use to insert single record in the database)
```
 Syntax:
  {
    "token": <"connection-token">,
    "cmd": "PUT",
    <<"dbName": <"database-name">,>>
    <<"rel": <"relation-name">,>>
    <<"colsAutoIndex": <boolean-value>,>>
    <<"templateStr": <json-template-data>,>>
    "jsonStr": <json-data>
  }

```
- Update data in database:(UPDATE REQUEST)
```
 Syntax:
  {
    "token": <"connection-token">,
    "cmd": "UPDATE",
    <<"dbName": "database-name",>>
    <<"rel": "relation-name",>>
    "jsonStr": {
        <"record-no">: {
            <"column-name">: <"new-value">
        }
        <"record-no">: {
            <"column-name">: <"new-value">
        }
    }
  }
```

- Remove a recorde from the database:(REMOVE REQUEST)
```
  Syntax:
  {
    "token": <"connection-token">,
    "cmd": "REMOVE",
    <<"dbName": <"database-name">,>>
    <<"rel": <"relation-name">,>>
    "record": <record-number | [record-number1,...]>
  }
  ```
- GET REQUEST:(To get data from the database)
```
  Syntax:
  {
    "token": <"connection-token">,
    "cmd": "GET",
    "dbName": <"database-name">,
    "rel": <"relation-name">,
    "jsonStr": {
        <"column-name">:<"column-value">
    }
  }
```
## Benefits of Using JsonPowerDB
- Nimble, simple to use, In memory,real time.
- Server Side, Native -NOSQL
- Maximum data processing performance.
- Minimum development cost.
- 
## Code with explaination
- Validation Function: checks all the form fields contains data or they are empty before submission.
```Javascript
function validateAndGetFormData() { 
  var empIdVar = $("#empId").val(); 
  if (empIdVar === "") { 
  alert("Employee ID Required Value"); 
  $("#empId").focus(); 
  return ""; 
  } 
 
  var empNameVar = $("#empName").val(); 
  if (empNameVar === "") { 
  alert("Employee Name is Required Value"); 
  $("#empName").focus(); 
  return ""; 
  } 
 
  var empEmailVar = $("#empEmail").val(); 
  if (empEmailVar === "") { 
  alert("Employee Email is Required Value"); 
  $("#empEmail").focus(); 
  return ""; 
  } 
  var jsonStrObj = { 
  empId: empIdVar, 
  empName: empNameVar, 
  empEmail: empEmailVar, 
  }; 
 
  return JSON.stringify(jsonStrObj); 
  } 
```
- Create a PUT REQUEST Function: this function fetches the data from the form field and create it as a query that can be understood by the JsonPowerDB.

```Javascript
function createPUTRequest(connToken, jsonObj, dbName, relName) { 
  var putRequest = "{\n" 
  + "\"token\" : \"" 
  + connToken 
  + "\"," 
  + "\"dbName\": \"" 
  + dbName 
  + "\",\n" + "\"cmd\" : \"PUT\",\n" 
  + "\"rel\" : \"" 
  + relName + "\"," 
  + "\"jsonStr\": \n" 
  + jsonObj 
  + "\n" 
  + "}"; 
  return putRequest; 
  } 
```
- Save Employee Details in the database: use to save employee details
``` Javascript
    function saveEmployee() { 
 
  var jsonStr = validateAndGetFormData(); 
  if (jsonStr === "") { 
  return; 
  } 
 
  var putReqStr = createPUTRequest("90936861|-31948784479254024|90932362", 
  jsonStr, "SAMPLE", "EMP-REL"); 
 
  alert(putReqStr); 
  jQuery.ajaxSetup({async: false}); 
//  var resultObj = executeCommand(putReqStr, "http://api.login2explore.com:5577", "/api/iml"); 
  alert(JSON.stringify(resultObj)); 
  jQuery.ajaxSetup({async: true}); 
    
  resetForm(); 
  } 
 
```

- Reset Form Function:To reset the form to blank after submitting the details.
```Javascript
function resetForm() { 
  $("#empId").val("") 
  $("#empName").val(""); 
  $("#empEmail").val(""); 
  $("#empId").focus(); 
  } 
```

### Resources Used
- JsonPowerDB help manual to refer to the syntax and functions.
- Refrences from login2explore 
- Talend API tester

