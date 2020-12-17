# devtest
######################################################################
##Procedure Header
# Name:
#   REST API with Python requests
# Purpose:
#   Automate test cases for APIs listed below (both positive and negative cases)
#   (procedure)
#       The website https://reqres.in
# NOTE:Understand the list of REST api endpoints listed there.
#
#TEST STEPS:
#1)GET- LIST USERS :Request List Users Data With GET
#2)POST-CREATE :Create User Data With POST 
#3)PUT-UPDATE :Modify Created User Data with PUT
#4)DELETE-DELETE : Deleted listed users
#5)Check/Handle all HTTP Errors
#
# Return values:
#       [OK] / [ERROR] / [SKIP]
#
######################################################################
import requests

print ("============ REST API POSITIVE TESTS =============")

#Request List Users Data With GET

url = "https://reqres.in/api/users?page=2"
response = requests.get(url)         

if (response.status_code == 200):
    print("PASS:GET-LIST USERS request was Successfull!",response.status_code)
else:
    print ("FAILED:GET-LIST USERS request:",response.status_code)
#print(response.text)
print(response.json())

#Create data with POST 
#User created success : 201 request code

data = {"name": "Nagesh", "job": "QA", "email": "nagesh.k@reqres.in"}
response = requests.post(url="https://reqres.in/api/users", data=data)

if (response.status_code == 201):
    print("PASS:POST-CREATE request was Successfull!",response.status_code)
else:
    print ("FAILE:POST-CREATE request:",response.status_code)

data = response.json()
print(data)

# Modify Data With PUT :User updated success : 200 request code

Updateddata = {"name": "Nagesh", "job": "Qc","email": "nagesh@reqres.com"}
response = requests.put(url="https://reqres.in/api/users", data=Updateddata)

if (response.status_code == 200):
    print("PASS:PUT-UPDATE request was Successfull!",response.status_code)
else:
    print ("FAILED:PUT-UPDATE request:",response.status_code)

data = response.json()
print(data)

#Making a DELETE request ,User delete success : 204 request code

response = requests.delete(url)
   
if (response.status_code == 204):
    print("PASS: DELETE-DELETE request was Successfull!",response.status_code)
else:
    print ("FAILED:DELETE-DELETE request:",response.status_code)

#print(response.json())
print ("================== REST API NEGATIVE TESTS ===================")
print (" --------- Check HTTP Error & Exception Handling all HTTP Errors -----------")                          

#Check for HTTP Errors With Python Requests
response = requests.get("https://reqres.in")
if (response.status_code == 200):
    print("The request was a success no Errors!")
    # Code here will only run if the request is successful
elif (response.status_code == 404):
    print("Result not found!")

#Exceptional handle all HTTP Errors,ConnectionError,Timeout Error

url2 ="https://reqres.in"
try: 
    response = requests.get(url2,timeout=3) 
    response.raise_for_status()                 # Raise error in case of failure 
except requests.exceptions.HTTPError as httpErr: 
    print ("Http Error:",httpErr) 
except requests.exceptions.ConnectionError as connErr: 
    print ("Error Connecting:",connErr) 
except requests.exceptions.Timeout as timeOutErr: 
    print ("Timeout Error:",timeOutErr) 
except requests.exceptions.RequestException as reqErr: 
    print ("Something Else:",reqErr) 
except requests.exceptions : 
    raise
finally:
    print ("Finally Cleanup")
   

