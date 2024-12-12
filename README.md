# Restful Booker API Performance Testing
This project evaluates the performance and reliability of the Restful Booker API under various conditions. Using Apache JMeter, this test plan is configured to simulate HTTP requests such as GET, POST, PUT, PATCH, and DELETE, targeting key API endpoints.

_**This test suite is designed to:**_
- Assess the system's responsiveness by measuring metrics like response time and throughput.
- Identify performance bottlenecks under increasing levels of concurrent user traffic.
- Ensure the API can handle typical operations like creating, updating, retrieving, and deleting bookings efficiently.

**Prerequisites**
1. _**System Requirements:**_
   - Operating System: Windows, Linux, or macOS
   - Java 8 or higher installed (required for JMeter)
2. _**Tools**_
   - Apache JMeter:  If you haven't already, [download and install Apache JMeter](https://jmeter.apache.org/download_jmeter.cgi).
3. _**Setup and Execution**_
   - Step 1: Clone the Repository:
     ``` clone
     git clone https://github.com/mdnazrulislam7255/Booikng_API_Load_Testing.git
     ```
   - Step 2: Configure JMeter
     Open the Restful_Booker.jmx file in Apache JMeter.
     Update the HTTP Request Defaults element to set the API base URL and authentication details (if applicable).
3. **_Import jmx file:_**
   - Open Jmeter.
   - Click on the Import button.
   - Select the file from the repository.

_**Usage**_ <br>

_**Select file:**_ <br>
      In Apache JMeter, select the appropriate jmx file. <br>

_**Run project:**_ <br>                         																				
      Select the imported jmx file. <br>
      Select any one of the listener . <br>
      Click Start Test to run the project.<br>
      
_**View Results:**_ <br>
       Once the tests are complete, view the results in the listener like View Results Tree or Aggregate Report. <br>
       Detailed test results can be viewed for each request.

## The script includes:
- Thread Groups: Configured with variable user loads and ramp-up times to simulate real-world usage patterns.
- HTTP Requests: Precisely configured for each API endpoint to validate CRUD operations.
- Assertions: Validates response status codes, response times, and data integrity.
- Listeners: Collect detailed test metrics and generate visual performance reports.

## Key API operations tested:
- GET /booking: Retrieve all bookings.
- POST /booking: Create new bookings with randomized data.
- GET /booking/{id}: Fetch details of a specific booking.
- PUT /booking/{id}: Update booking information.
- PATCH /booking/{id}: Modify specific fields in a booking.
- DELETE /booking/{id}: Remove a booking.

# Base URL
The base URL is: https://restful-booker.herokuapp.com

# End points
## _Health Check_
Protocol :_ https _                                                                                                                                                                       
Server Name or IP: _restful-booker.herokuapp.com_                                                                                                                                         
HTTP Request method: _GET_                                                                                                                                                                
Path: _/ping_                                                                                                                                                                             
Request body: ```none```                                                                                                                                                                  
Response body: ```Created```                                                                                                                                                             

## _Create Booking Token_
Protocol : _https_                                                                                                                                                                        
Server Name or IP: _restful-booker.herokuapp.com_                                                                                                                                         
HTTP Request method: _POST_                                                                                                                                                               
Path: _/auth_                                                                                                                                                                             
HTTP Header Manager: Content-Type: _application/json_                                                                                                                                  
JSON Extractor:
- Variables: _tokenID_                                                                                                                                                                    
- JSON path expression:_ $.token_
                                                                                                                                                         
Request body:                                                                                                                                                                             
``` console
{
    "username" : "admin",
    "password" : "password123"
}
```
Response body:
``` console
{"token":"1ce98290ae3d1f2"}
```

## _Create Booking_
Protocol : _https_                                                                                                                                                                        
Server Name or IP: _restful-booker.herokuapp.com_                                                                                                                                         
HTTP Request method: _POST_                                                                                                                                                               
Path: _/booking_                                                                                                                                                                          
HTTP Header Manager: Content-Type: _application/json_                                                                                                                                  
JSON Extractor:
- Variables: _booking_ID_                                                                                                                                                                 
- JSON path expression: _$.bookingid_

Request body:                                                                                                                                                                             
``` console
{
    "firstname" : "Jim",
    "lastname" : "Brown",
    "totalprice" : 111,
    "depositpaid" : true,
    "bookingdates" : {
        "checkin" : "2018-01-01",
        "checkout" : "2019-01-01"
    },
    "additionalneeds" : "Breakfast"
}
```
Response body:
``` console
{"bookingid":4477,"booking":{"firstname":"Jim","lastname":"Brown","totalprice":111,"depositpaid":true,"bookingdates":{"checkin":"2018-01-01","checkout":"2019-01-01"},"additionalneeds":"Breakfast"}}
```

## _Get Booking_
Protocol : _https_                                                                                                                                                                        
Server Name or IP: _restful-booker.herokuapp.com_                                                                                                                                         
HTTP Request method: _GET_                                                                                                                                                               
Path: booking/${booking_ID}                                                                                                                                                               
HTTP Header Manager: Content-Type: _application/json_                                                                                                                                         
Request body:
``` none```                                                                                                                                                                               
Response body:
``` console
{"firstname":"Jim","lastname":"Brown","totalprice":111,"depositpaid":true,"bookingdates":{"checkin":"2018-01-01","checkout":"2019-01-01"},"additionalneeds":"Breakfast"}
```

## _Update Booking_
Protocol : _https_                                                                                                                                                                        
Server Name or IP: _restful-booker.herokuapp.com_                                                                                                                                        
HTTP Request method: _PUT_                                                                                                                                                              
Path: _booking/${booking_ID}_                                                                                                                                                             
HTTP Header Manager:                                                                                                                                                                      
- Content-Type: application/json                                                                                                                                                          
- Cookie: token=${tokenID}                                                                                                                                                                

Request body:                                                         
                                                                                                                                                                             
``` console
{
    "firstname" : "Nazrul",
    "lastname" : "Islam",
    "totalprice" : 111,
    "depositpaid" : true,
    "bookingdates" : {
        "checkin" : "2018-01-01",
        "checkout" : "2019-01-01"
    },
    "additionalneeds" : "Breakfast"
}
```
Response body:
``` console
{"firstname":"Nazrul","lastname":"Islam","totalprice":111,"depositpaid":true,"bookingdates":{"checkin":"2018-01-01","checkout":"2019-01-01"},"additionalneeds":"Breakfast"}
```
## _Update Booking Partially_
Protocol : _https_
Server Name or IP: _restful-booker.herokuapp.com_                                                                                                                                         
HTTP Request method: _PATCH_                                                                                                                                                              
Path: booking/${booking_ID}                                                                                                                                                               
HTTP Header Manager:
- Content-Type: application/json
- Cookie: token=${tokenID}

Request body:                                                                                                                                                                             
``` console
{
  "firstname" : "Nafsi",
  "totalprice" : 500
}
```
Response body:
``` console
{"firstname":"Nafsi","lastname":"Islam","totalprice":500,"depositpaid":true,"bookingdates":{"checkin":"2018-01-01","checkout":"2019-01-01"},"additionalneeds":"Breakfast"}
```

_### **Delete Booking **_                                                                                                                                                                 
Protocol : _https_                                                                                                                                                                        
Server Name or IP: _restful-booker.herokuapp.com_                                                                                                                                         
HTTP Request method: _DELETE_                                                                                                                                                             
Path: _booking/${booking_ID}_                                                                                                                                                             
HTTP Header Manager:                                                                                                                                                                      - Content-Type: _application/json_
- Cookie: _token=${tokenID}_

Request body: ``` none```                                                                                                                                                                 
Response body: ``` Created```                                                                                                                                                             

### Run Command:
  Run Command for Report: Run from Jmeter bin folder where the project file is located
``` console
 jmeter -n -t Restful_Booker.jmx -l reports\Restful_Booker.jtl
```
``` console
 jmeter -g reports\Restful_Booker.jtl -o reports\Restful_Booker.html
```
### Reports
Test 1:
- Number of threads: _1400_; 
- Ramo-up period(seconds): _300_ ; 
- Loop count: _1_
                                                                                                                                                                      
![image](https://github.com/user-attachments/assets/4bf62d8e-f668-4190-a715-d232a0ce464b)
![image](https://github.com/user-attachments/assets/71dd4b46-2394-41bb-b46c-6dc743bbdd3f)
![image](https://github.com/user-attachments/assets/e6b43ba1-a0d5-4aaa-8a86-f4ffd45a81e1)


Test 2:
- Number of threads: _2500_; 
- Ramo-up period(seconds): _500_ ; 
- Loop count: _1_
![image](https://github.com/user-attachments/assets/caeff1d6-42c3-462d-8919-11fc82be5279)
![image](https://github.com/user-attachments/assets/574ad21d-94a9-4c07-843e-c95b278f4887)
![image](https://github.com/user-attachments/assets/a3e8eb84-357f-4feb-8c9d-3de9ea8135be)
![image](https://github.com/user-attachments/assets/a39c23e7-a01b-4c14-b4e1-77e385754137)





### Contact
For questions or support, contact the development team at: Email: _nazrul15-7255@diu.edu.bd_
