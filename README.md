# Introduction
Welcome to the API testing suite for the restful-booker.herokuapp.com API. This repository contains a Postman collection and environment designed to facilitate API testing for various functionalities related to Booking information. The API allows operations such as fetching booking details, create booking, get booking info, get booking info update, update booking, delete bboking.

# Summery    
I have Completed an API test of Token, Create booking, get booking info, get booking info update, update booking, delete https://restful-booker.herokuapp.com
   
<p align="center">
  <img src="https://github.com/umacb/CVPR/assets/113898629/89dae655-0897-43d0-8ed7-7a172340f0e0" />
</p>
 

Here in this API student details viewed and different tests were performed like GET, POST, PUT, DELETE.

**Summary:** Test Scripts 4 and Total 16 assertions were done. All of them passed with 0 skipped tests. The number of iteration was 1.



# Requirements  
**Java**  
https://www.oracle.com/java/technologies/downloads/   
**Postman**   
https://www.postman.com/   
**Node JS**   
https://nodejs.org/en/    



# Assertions Details    
#### Token
**Test Script**
```bash
var token = pm.response.json()
pm.environment.set("token", token.token)
```

#### Create Booking
**Body**
```bash
{
	"firstname" : "{{firstName}}",
	"lastname" : "{{lastName}}",
	"totalprice" : {{totalPrice}},
	"depositpaid" : {{depositPaid}},
	"bookingdates" : {
    	"checkin" :  "{{checkIn}}",
    	"checkout" : "{{checkOut}}"
	},
	"additionalneeds" : "Breakfast"
}
```
**Test Script**
```bash
var jsonData = pm.response.json()
pm.environment.set("id",jsonData.bookingid)
```
**Pre-Request Script**

```bash
var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
console.log("First Name value:" + firstName)
pm.environment.set("firstName", firstName)

var lastName = pm.variables.replaceIn("{{$randomLastName}}")
console.log("Last Name value:" + lastName)
pm.environment.set("lastName", lastName)

var randomPriceString = pm.variables.replaceIn("{{$randomPrice}}")
const totalPrice = parseInt(randomPriceString, 10);
console.log("Total Price value:"+ totalPrice)
pm.environment.set("totalPrice", totalPrice)

var depositPaid = pm.variables.replaceIn("{{$randomBoolean}}")
console.log("Deposit paid value:" + depositPaid)
pm.environment.set("depositPaid", depositPaid)

const moment = require('moment')
const today = moment()
console.log(today.format("YYYY-MM-DD"))
pm.environment.set("checkIn",today.format("YYYY-MM-DD"))

const today1 = moment()
console.log(today1.format("YYYY-MM-DD"))
pm.environment.set("checkOut",today1.add(30,'d').format("YYYY-MM-DD"))
```
#### Get Booking Info
**Test Script**
```bash


var statuscode = pm.response.code
console.log(statuscode)

if(statuscode=200){

var jsonData = pm.response.json()
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("FirstName Validation", function () {
    pm.expect(jsonData.firstname).to.eq(pm.environment.get("firstName"))
})

pm.test("LastName Validation", function()
{
    pm.expect(jsonData.lastname).to.eql(pm.environment.get("lastName"))
})

pm.test("Total Price Validation", function(){
    pm.expect(jsonData.totalprice).to.eql(pm.environment.get("totalPrice"))
})

pm.test("Deposit Paid Validation", function(){
   pm.expect(String(jsonData.depositpaid)).to.eql(pm.environment.get("depositPaid"))
})

pm.test("Check In Validation", function(){
    pm.expect(jsonData.bookingdates.checkin).to.eql(pm.environment.get("checkIn"))
})

pm.test("Check Out Validation", function(){
    pm.expect(jsonData.bookingdates.checkout).to.eql(pm.environment.get("checkOut"))
})

pm.test("Additional Needs", function(){
    pm.expect(jsonData.additionalneeds).to.eql("Breakfast")
})
}else if(statuscode=404)
{pm.test("Not found", function () {
    pm.response.to.have.status(404);})
}

else{pm.test("Something is wrong...")
}

```  

#### Get Booking Info Update
**Test Script**
```bash


var statuscode = pm.response.code
console.log(statuscode)

if(statuscode=200){

var jsonData = pm.response.json()
pm.test("Status code is 200", function () {
    pm.response.to.have.status(200);
});

pm.test("FirstName Validation", function () {
    pm.expect(jsonData.firstname).to.eq(pm.environment.get("firstName"))
})

pm.test("LastName Validation", function()
{
    pm.expect(jsonData.lastname).to.eql(pm.environment.get("lastName"))
})

pm.test("Total Price Validation", function(){
    pm.expect(jsonData.totalprice).to.eql(pm.environment.get("totalPrice"))
})

pm.test("Deposit Paid Validation", function(){
   pm.expect(String(jsonData.depositpaid)).to.eql(pm.environment.get("depositPaid"))
})

pm.test("Check In validation", function(){
    pm.expect(jsonData.bookingdates.checkin).to.eql(pm.environment.get("checkIn"))
})

pm.test("Check Out", function(){
    pm.expect(jsonData.bookingdates.checkout).to.eql(pm.environment.get("checkOut"))
})

pm.test("Additional Needs", function(){
    pm.expect(jsonData.additionalneeds).to.eql("Breakfast")
})
}
else if(statuscode=404)
{pm.test("Not found", function () {
    pm.response.to.have.status(404);})
}
else{pm.test("Something is wrong...")
}

```   

#### Update Booking
**Body**
```bash
{
	"firstname" : "{{firstName}}",
	"lastname" : "{{lastName}}",
	"totalprice" : {{totalPrice}},
	"depositpaid" : {{depositPaid}},
	"bookingdates" : {
    	"checkin" : "{{checkIn}}",
    	"checkout" : "{{checkOut}}"
	},
	"additionalneeds" : "Breakfast"
}
```
**Pre-Request Script**
```bash

var firstName = pm.variables.replaceIn("{{$randomFirstName}}")
console.log("First Name value:" + firstName)
pm.environment.set("firstName", firstName)

var lastName = pm.variables.replaceIn("{{$randomLastName}}")
console.log("Last Name value:" + lastName)
pm.environment.set("lastName", lastName)

var randomPriceString = pm.variables.replaceIn("{{$randomPrice}}")
const totalPrice = parseInt(randomPriceString, 10);
console.log("Total Price value:"+ totalPrice)
pm.environment.set("totalPrice", totalPrice)

var depositPaid = pm.variables.replaceIn("{{$randomBoolean}}")
console.log("Deposit paid value:" + depositPaid)
pm.environment.set("depositPaid", depositPaid)

const moment = require('moment')
const today = moment()
console.log(today.format("YYYY-MM-DD"))
//var checkIn = pm.variables.replaceIn("{{$randomDatePast}}")
//console.log("CheckIn value:" + checkIn)
pm.environment.set("checkIn",today.format("YYYY-MM-DD"))

const today1 = moment()
console.log(today.format("YYYY-MM-DD"))
//var checkIn = pm.variables.replaceIn("{{$randomDatePast}}")
//console.log("CheckIn value:" + checkIn)
pm.environment.set("checkIn",today.add(25, 'd').format("YYYY-MM-DD"))

```
# Create Test Suites   

### Using Newman   


  Newman is a command-line Collection Runner for Postman. It enables you to run and test a Postman Collection directly from the command line.
#### Install Command    
```bash
npm install -g newman    
```
#### Run Command    
- newman run “Path/CollectionName.json” -e Path/EnvironmentName.json
- newman run “Collection Link” -e “Path”/EnvironmentName.json    

#### Create HTML Report  
 
#### Install Command      
```bash
npm install -g newman-reporter-html
```
**or**   
```bash
npm install -g newman-reporter-htmlextra    
```
#### Run Command      
- newman run “Collection Link” -e “Path”/EnvironmentName.json -r cli,html    
**or**    
- newman run “Collection Link” -e “Path”/EnvironmentName.json -r cli,htmlextra

- #### Newman File htmlextra
 <p align="center">
  <img src="https://github.com/umacb/CVPR/assets/113898629/da68ab3a-9f5f-4032-8ec0-0a29e0193db3"/></p>



