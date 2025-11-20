slip 1
-------------------------------------------------------
<!DOCTYPE html>
<html>
<head>
    <style>
        Body {
            font-family: Arial, sans-serif;
        }
        H1 {
            Font-size: 6pt;
            Color: black;
        }
        Form {
            Background-color: lightblue;
        }
    </style>
</head>
<body>
    <h1><b>Project Management</b></h1>
    <form action=””> <label for=”projectname”>Project Name:</label>
        <input type=”text” id=”projectname” name=”projectname”><br><br>
        <label for=”assignedto”>Assigned to:</label>
        <input type=”text” id=”assignedto” name=”assignedto”><br><br>
        <label for=”startdate”>Start Date:</label>
        <input type=”date” id=”startdate” name=”startdate”><br><br>
        <label for=”enddate”>End Date:</label>
        <input type=”date” id=”enddate” name=”enddate”><br><br>
        <label for=”priority”>Priority:</label>
        <select id=”priority” name=”priority”>
            <option value=”high”>High</option>
            <option value=”average”>Average</option>
            <option value=”low”>Low</option>
        </select><br><br>
        <label for=”description”>Description:</label>
        <textarea id=”description” name=”description” rows=”4” cols=”50”></textarea><br><br>
        <input type=”submit” value=”Submit”>
        <input type=”submit” value=”clear”>
    </form>
</body>
</html>


1. Model the following Property system as a document database
We will use two collections:
Collection 1: Owners
{
_id: 1,
ownerName: "Mr.Patil",
contact: "9876543210"
}
Collection 2: Properties
{
_id: 101,
area: "Nashik",
rate: 95000,
ownerId: 1
}
One owner can have many properties → ownerId is used to link.
_-------------
2. Assume appropriate attributes and collections
Owner attributes
ownerNamecontact
email
Property attributes
area
rate
size
ownerId
-----------
3. Insert at least 05 documents in each collection
---
Owners Collection (5 Documents)
{
_id: 1,
ownerName: "Mr.Patil",
contact: "9876543210",email: "patil@gmail.com"
} {
_id: 2,
ownerName: "Mr.Shinde",
contact: "9876500000",
email: "shinde@gmail.com"
} {
_id: 3,
ownerName: "Mr.Kulkarni",
contact: "9876512345",
email: "kulkarni@gmail.com"
} {
_id: 4,
ownerName: "Mrs.Jadhav",
contact: "9876523456",
email: "jadhav@gmail.com"
} {
_id: 5,
ownerName: "Mr.Desai",
contact: "9876534567",
email: "desai@gmail.com"
}
---
Properties Collection (5 Documents){
_id: 101,
area: "Nashik",
rate: 95000,
size: "800 sqft",
ownerId: 1
} {
_id: 102,
area: "Pune",
rate: 150000,
size: "1200 sqft",
ownerId: 1
} {
_id: 103,
area: "Mumbai",
rate: 300000,
size: "1000 sqft",
ownerId: 2
} {
_id: 104,
area: "Nashik",
rate: 80000,
size: "600 sqft",
ownerId: 3
} {
_id: 105,area: "Aurangabad",
rate: 70000,
size: "500 sqft",
ownerId: 4
}
-----------------
Q.2) 4. ANSWER THE QUERIES
---
(a) Display area-wise property details
MongoDB Query:
db.properties.aggregate([
{ $group: { _id: "$area", properties: { $push: "$$ROOT" } } }
])
OUTPUT:
{
_id: "Nashik",
properties: [
{ _id: 101, rate: 95000, size: "800 sqft", ownerId: 1 },
{ _id: 104, rate: 80000, size: "600 sqft", ownerId: 3 }
]
}{
_id: "Pune",
properties: [
{ _id: 102, rate: 150000, size: "1200 sqft", ownerId: 1 }
]
} {
_id: "Mumbai",
properties: [
{ _id: 103, rate: 300000, size: "1000 sqft", ownerId: 2 }
]
} {
_id: "Aurangabad",
properties: [
{ _id: 105, rate: 70000, size: "500 sqft", ownerId: 4 }
]
} -
_-----------
(b) Display property owned by 'Mr.Patil' having minimum rate
Step 1: Find ownerId
OwnerId = 1
MongoDB Query
db.properties.find({ ownerId: 1 }).sort({ rate: 1 }).limit(1)OUTPUT
{
_id: 101,
area: "Nashik",
rate: 95000,
size: "800 sqft",
ownerId: 1
}
---
(c) Give the details of owner whose property is at “Nashik”
MongoDB Query:
db.properties.aggregate([
{ $match: { area: "Nashik" } },
{
$lookup: {
from: "owners",
localField: "ownerId",
foreignField: "_id",
as: "ownerDetails"
}
}
])
OUTPUT:{
_id: 101,
area: "Nashik",
rate: 95000,
ownerDetails: [
{ _id: 1, ownerName: "Mr.Patil", contact: "9876543210" }
]
} {
_id: 104,
area: "Nashik",
rate: 80000,
ownerDetails: [
{ _id: 3, ownerName: "Mr.Kulkarni", contact: "9876512345" }
]
}
---
(d) Display area of property whose rate is less than 100000
MongoDB Query:
db.properties.find(
{ rate: { $lt: 100000 } },
{ area: 1, rate: 1, _id: 0 }
)
OUTPUT:{ area: "Nashik", rate: 95000 }
{ area: "Nashik", rate: 80000 }
{ area: "Aurangabad", rate: 70000 }


---------------------------------------------------------------------------  
slip 2
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bootstrap Container Example</title>
    <!-- Bootstrap CSS -->
    <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
    <div class="container mt-5">
        <div class="row">
            <div class="col-md-4">
                <div class="card">
                    <div class="card-body">
                        <h5 class="card-title">Column 1</h5>
                        <p class="card-text">Content for column 1.</p>
                    </div>
                </div>
            </div>
            <div class="col-md-4">
                <div class="card">
                    <div class="card-body">
                        <h5 class="card-title">Column 2</h5>
                        <p class="card-text">Content for column 2.</p>
                    </div>
                </div>
            </div>
            <div class="col-md-4">
                <div class="card">
                    <div class="card-body">
                        <h5 class="card-title">Column 3</h5>
                        <p class="card-text">Content for column 3.</p>
                    </div>
                </div>
            </div>
        </div>
    </div>
    <!-- Bootstrap JS (Optional, for certain components) -->
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.bundle.min.js"></script>
</body>
</html>

Attributes assumed (as required)
City attributes → cityName, state
Publisher attributes → publisherName, state
Newspaper attributes → language, sale, publisherId, cityId
---
3. Insert at least 5 documents in each collection
---
Cities Collection (5 Documents){
_id: 1,
cityName: "Nashik",
state: "Maharashtra"
} {
_id: 2,
cityName: "Pune",
state: "Maharashtra"
} {
_id: 3,
cityName: "Mumbai",
state: "Maharashtra"
} {
_id: 4,
cityName: "Ahmedabad",
state: "Gujrat"
} {
_id: 5,
cityName: "Surat",
state: "Gujrat"
}
---Publishers Collection (5 Documents)
{
_id: 1,
publisherName: "Sakal Publications",
state: "Maharashtra",
contact: "9998887771"
} {
_id: 2,
publisherName: "Lokmat Group",
state: "Maharashtra",
contact: "8887776661"
} {
_id: 3,
publisherName: "Gujrat Times Media",
state: "Gujrat",
contact: "7776665551"
} {
_id: 4,
publisherName: "Divya Bhaskar",
state: "Gujrat",
contact: "9991115555"
} {
_id: 5,publisherName: "Maharashtra Times",
state: "Maharashtra",
contact: "9090909090"
}
---
Newspapers Collection (5 Documents)
{
_id: 101,
newspaperName: "Sakal",
language: "Marathi",
publisherId: 1,
sale: 50000,
cityId: 1
} {
_id: 102,
newspaperName: "Lokmat",
language: "Marathi",
publisherId: 2,
sale: 65000,
cityId: 2
} {
_id: 103,
newspaperName: "Divya Bhaskar",language: "Gujarati",
publisherId: 4,
sale: 55000,
cityId: 4
} {
_id: 104,
newspaperName: "Gujrat Times",
language: "Gujarati",
publisherId: 3,
sale: 60000,
cityId: 5
} {
_id: 105,
newspaperName: "Maharashtra Times",
language: "Marathi",
publisherId: 5,
sale: 70000,
cityId: 3
}
---
Q2). ANSWER THE QUERIES
---(a) List all newspapers available in NASHIK city
MongoDB Query
db.newspapers.find({ cityId: 1 })
EXACT OUTPUT
{ _id: 101, newspaperName: "Sakal", language: "Marathi", sale: 50000, cityId: 1 }
---
(b) List all newspapers of Marathi language
MongoDB Query
db.newspapers.find({ language: "Marathi" })
EXACT OUTPUT
{ _id: 101, newspaperName: "Sakal", language: "Marathi", sale: 50000 }
{ _id: 102, newspaperName: "Lokmat", language: "Marathi", sale: 65000 }
{ _id: 105, newspaperName: "Maharashtra Times", language: "Marathi", sale: 70000 }
---(c) Count no. of publishers of Gujrat state
MongoDB Query
db.publishers.count({ state: "Gujrat" })
EXACT OUTPUT
2
---
(d) Write a cursor to show newspapers with highest sale in Maharashtra state
MongoDB Cursor
var cur = db.newspapers.aggregate([
{
$lookup: {
from: "cities",
localField: "cityId",
foreignField: "_id",
as: "cityDetails"
}
},
{ $unwind: "$cityDetails" },
{ $match: { "cityDetails.state": "Maharashtra" } },
{ $sort: { sale: -1 } },{ $limit: 1 }
]);
while(cur.hasNext()) {
printjson(cur.next());
}
---
EXACT OUTPUT
{
_id: 105,
newspaperName: "Maharashtra Times",
language: "Marathi",
sale: 70000,
cityDetails: {
cityName: "Mumbai",
state: "Maharashtra"
}
}
---------------------------------------------------------------------------  
slip 3
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css">
    <title>Image Thumbnails</title>
</head>
<body>
    <div class="container mt-5">
        <h2 class="mb-4">Image Thumbnails</h2>
        <div class="row">
            <!-- Image 1 -->
            <div class="col-md-4">
                <div class="thumbnail">
                    <img src="path/to/image1.jpg" alt="Image 1" class="img-fluid">
                    <div class="caption">
                        <h4>Image 1</h4>
                    </div>
                </div>
            </div>
            <!-- Image 2 -->
            <div class="col-md-4">
                <div class="thumbnail">
                    <img src="path/to/image2.jpg" alt="Image 2" class="img-fluid">
                    <div class="caption">
                        <h4>Image 2</h4>
                    </div>
                </div>
            </div>
            <!-- Image 3 -->
            <div class="col-md-4">
                <div class="thumbnail">
                    <img src="path/to/image3.jpg" alt="Image 3" class="img-fluid">
                    <div class="caption">
                        <h4>Image 3</h4>
                    </div>
                </div>
            </div>
        </div>
    </div>
</body>
</html>

1. Model the system as a Document Database
Collections Used:
Department Collection
dept_id
dept_name
location
Employee Collection
emp_id
emp_name
salary
dept_id
---
2. Attributes AssumedEmployees linked to departments using dept_id.
---
3. Insert at least 5 documents
---
Department Collection
{ dept_id: 1, dept_name: "HR", location: "Mumbai" }
{ dept_id: 2, dept_name: "Sales", location: "Pune" }
{ dept_id: 3, dept_name: "IT", location: "Nashik" }
{ dept_id: 4, dept_name: "Finance", location: "Mumbai" }
{ dept_id: 5, dept_name: "Marketing", location: "Nagpur" }
---
Employee Collection
{ emp_id: 101, emp_name: "Amit", salary: 40000, dept_id: 2 }
{ emp_id: 102, emp_name: "Sneha", salary: 55000, dept_id: 2 }
{ emp_id: 103, emp_name: "Rahul", salary: 65000, dept_id: 3 }
{ emp_id: 104, emp_name: "Kiran", salary: 30000, dept_id: 1 }
{ emp_id: 105, emp_name: "Priya", salary: 75000, dept_id: 3 }Q2). ANSWER THE QUERIES
---
(a) Display name of employee who has highest salary
Query:
db.employee.find().sort({ salary: -1 }).limit(1)
Exact Output:
{ emp_id: 105, emp_name: "Priya", salary: 75000, dept_id: 3 }
---
(b) Display biggest department with max no. of employees
Query:
db.employee.aggregate([
{ $group: { _id: "$dept_id", count: { $sum: 1 } } },
{ $sort: { count: -1 } },
{ $limit: 1 }
])Exact Output:
Assume dept 3 has 2 employees (Rahul and Priya), others 1 each.
{ _id: 3, count: 2 }
---
(c) Cursor showing department-wise employee information
Cursor:
var cur = db.employee.aggregate([
{
$lookup: {
from: "department",
localField: "dept_id",
foreignField: "dept_id",
as: "deptDetails"
}
},
{ $unwind: "$deptDetails" },
{
$project: {
emp_name: 1,
salary: 1,
"deptDetails.dept_name": 1
}}
]);
while(cur.hasNext()) {
printjson(cur.next());
}
---
Exact Output:
{ emp_name: "Amit", salary: 40000, deptDetails: { dept_name: "Sales" } }
{ emp_name: "Sneha", salary: 55000, deptDetails: { dept_name: "Sales" } }
{ emp_name: "Rahul", salary: 65000, deptDetails: { dept_name: "IT" } }
{ emp_name: "Kiran", salary: 30000, deptDetails: { dept_name: "HR" } }
{ emp_name: "Priya", salary: 75000, deptDetails: { dept_name: "IT" } }
---
(d) List all employees who work in Sales dept and salary > 50000
Query:
db.employee.find({
dept_id: 2,
salary: { $gt: 50000 }
})Exact Output:
{ emp_id: 102, emp_name: "Sneha", salary: 55000, dept_id: 2 }
---
Final Output Summary
Query Exact Output
Highest Salary Employee Priya (75000)
Biggest Department Dept 3 → Employee count = 2
Dept-wise Employee Info Prints 5 JSON documents
Sales dept salary
---------------------------------------------------------------------------  
slip 4
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Bootstrap Table Example</title>
    <!-- Bootstrap CSS -->
    <link href="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
    <div class="container mt-5">
        <!-- Container with margin-top (mt-5) -->
        <h2 class="mb-4">User Information Table</h2>
        <table class="table">
            <!-- Bootstrap Table -->
            <thead>
                <!-- Table Header -->
                <tr>
                    <th scope="col">First Name</th>
                    <th scope="col">Last Name</th>
                    <th scope="col">Email ID</th>
                </tr>
            </thead>
            <tbody>
                <!-- Table Body -->
                <tr>
                    <td>John</td>
                    <td>Doe</td>
                    <td>john.doe@example.com</td>
                </tr>
                <tr>
                    <td>Jane</td>
                    <td>Smith</td>
                    <td>jane.smith@example.com</td>
                </tr>
                <!-- Add more rows as needed -->
            </tbody>
        </table>
        <!-- End of Bootstrap Table -->
    </div>
    <!-- End of Container -->
    <!-- Bootstrap JS (Optional, for certain components) -->
    <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.5.2/js/bootstrap.bundle.min.js"></script>
</body>
</html>

Q
2). Assume appropriate attributes and collections as per the query requirements
=>
1. Hospitals Collection
Attributes:
_id : unique hospital IDname : hospital name
city : hospital city
specializations : list of specializations
doctors : list of doctor IDs
---
2. Doctors Collection
Attributes:
_id : doctor ID
name : doctor name
specializations : list of expertise
hospital_ids : list of hospitals where doctor provides service
---3. Reviews Collection
Attributes:
_id : review ID
person_name : reviewer
rating : rating
review : feedback text
hospital_id : which hospital is reviewed
3. List the names of hospitals with Orthopedic specialization
=>
Query:
db.hospitals.find(
{ specializations: "Orthopedic" },
{ hospital_name: 1, _id: 0 }
)
Output:
City HospitalSunrise Hospital
Lotus Hospital
4]List the names of all hospitals located in Nashik
=>
db.hospitals.find(
{ city: "Nashik" },
{ hospital_name: 1, _id: 0 }
)
Output:
City Hospital
Sunrise Hospital
MediCare Hospital
5]List the names of hospitals where Dr. Deshmukh visits
=>
db.hospitals.find(
{ doctor_ids: 103 },
{ hospital_name: 1, _id: 0 }
)
Output:
Sunrise Hospital6] List the names of hospitals whose rating >= 4
=>
db.hospitals.find(
{ hospital_id: { $in: [1, 2, 3, 5, 6, 7, 9, 10] } },
{ hospital_name: 1, _id: 0 }
)
Output:
City Hospital
Sunrise Hospital
Apollo Clinic
---------------------------------------------------------------------------  
slip 5
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>List of Persons</title>
    <style>
        table {
            border-collapse: collapse;
            width: 50%;
            margin: 20px;
            border: 1px solid #ddd;
            border-radius: 10px;
        }
        th,
        td {
            border: 1px solid #ddd;
            text-align: center;
            padding: 10px;
        }
        th {
            background-color: #f2f2f2;
        }
    </style>
</head>
<body>
    <h2>List of Persons</h2>
    <table>
        <thead>
            <tr>
                <th>Srno</th>
                <th>Person Name</th>
                <th>Age</th>
                <th>Country</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>1</td>
                <td>John Doe</td>
                <td>30</td>
                <td>USA</td>
            </tr>
            <tr>
                <td>2</td>
                <td>Jane Smith</td>
                <td>25</td>
                <td>Canada</td>
            </tr>
            <tr>
                <td>3</td>
                <td>Bob Johnson</td>
                <td>35</td>
                <td>UK</td>
            </tr>
        </tbody>
    </table>
</body>
</html>



---------------------------------------------------------------------------  
slip 7
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>3D Text Effect</title>
    <style>
        body {
            font-family: 'Arial', sans-serif;
            background-color: #f0f0f0;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
        }
        .three-d-text {
            font-size: 3em;
            font-weight: bold;
            color: #3498db;
            text-shadow: 4px 4px 0 #2980b9, 7px 7px 0 #2c3e50;
            transition: transform 0.3s ease-in-out;
        }
        .three-d-text:hover {
            transform: translate(3px, 3px);
        }
    </style>
</head>
<body>
    <div class="three-d-text">Hover me!</div>
</body>
</html>



1. Insert 5 documents in the Customers collection:
db.customers.insertMany([
{ _id: 1, first_name: "Sanjay", last_name: "Sharma", email: "sanjay@example.com", branch: "Nashik",
account_ids: [1, 2] },
{ _id: 2, first_name: "Priya", last_name: "Kumar", email: "priya@example.com", branch: "Nashik",
account_ids: [3] },
{ _id: 3, first_name: "Ravi", last_name: "Desai", email: "ravi@example.com", branch: "Mumbai",
account_ids: [4] },
{ _id: 4, first_name: "Sneha", last_name: "Patel", email: "sneha@example.com", branch: "Pune",
account_ids: [5] },
{ _id: 5, first_name: "Sita", last_name: "Verma", email: "sita@example.com", branch: "Nashik",
account_ids: [6] }
]);
2. Insert 5 documents in the Accounts collection:
db.accounts.insertMany([
{ _id: 1, customer_id: 1, account_type: "Saving", balance: 5000, date_opened: new Date("2020-01-
01") },
{ _id: 2, customer_id: 1, account_type: "Current", balance: 15000, date_opened: new Date("2021-06-
15") },
{ _id: 3, customer_id: 2, account_type: "Saving", balance: 8000, date_opened: new Date("2020-01-
01") },
{ _id: 4, customer_id: 3, account_type: "Loan", balance: 200000, date_opened: new Date("2019-05-
10") },
{ _id: 5, customer_id: 4, account_type: "Saving", balance: 10000, date_opened: new Date("2020-07-
20") },
{ _id: 6, customer_id: 5, account_type: "Saving", balance: 6000, date_opened: new Date("2020-01-
01") }
]);
a. List names of all customers whose first name starts with an “S”
db.customers.find({ first_name: { $regex: "^S", $options: "i" } }).forEach(customer => {
print("Customer Name: " + customer.first_name + " " + customer.last_name);
});
b. List all customers who opened an account on 1/1/2020 in a specific branch (e.g., "Nashik")
var specificBranch = "Nashik";
db.accounts.find({ date_opened: new Date("2020-01-01") }).forEach(account => {
var customer = db.customers.findOne({ _id: account.customer_id, branch: specificBranch });
if (customer) {
print("Customer Name: " + customer.first_name + " " + customer.last_name);
}
});
c. List the names of customers where acctype = “Saving”
db.accounts.find({ account_type: "Saving" }).forEach(account => {
var customer = db.customers.findOne({ _id: account.customer_id });
print("Customer Name: " + customer.first_name + " " + customer.last_name);
});
d. Count the total number of loan account holders in a specific branch (e.g., "Nashik")
var branch = "Nashik";
var loanAccountHolders = new Set();
db.accounts.find({ account_type: "Loan" }).forEach(account => {
var customer = db.customers.findOne({ _id: account.customer_id, branch: branch });
if (customer) {
loanAccountHolders.add(customer._id);
}
});
print("Total number of loan account holders in " + branch + ": " + loanAccountHolders.size);
---------------------------------------------------------------------------  
slip 9
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Registration Form</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 20px;
        }
        form {
            max-width: 600px;
            margin: 0 auto;
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
        }
        input,
        select {
            width: 100%;
            padding: 10px;
            margin-bottom: 16px;
            border: 1px solid #ccc;
            border-radius: 4px;
            box-sizing: border-box;
        }
        input[type="submit"] {
            background-color: #4caf50;
            color: #fff;
            cursor: pointer;
        }
        input[type="submit"]:hover {
            background-color: #45a049;
        }
    </style>
</head>
<body>
    <form action="#" method="post">
        <h2>Student Registration Form</h2>
        <label for="fullName">Full Name:</label>
        <input type="text" id="fullName" name="fullName" required>
        <label for="email">Email:</label>
        <input type="email" id="email" name="email" required>
        <label for="dateOfBirth">Date of Birth:</label>
        <input type="date" id="dateOfBirth" name="dateOfBirth" required>
        <label for="gender">Gender:</label>
        <select id="gender" name="gender" required>
            <option value="male">Male</option>
            <option value="female">Female</option>
            <option value="other">Other</option>
        </select>
        <label for="course">Select Course:</label>
        <select id="course" name="course" required>
            <option value="computerScience">Computer Science</option>
            <option value="engineering">Engineering</option>
            <option value="biology">Biology</option>
            <!-- Add more options as needed -->
        </select>
        <label for="searchCollege">Search for College:</label>
        <input type="search" id="searchCollege" name="searchCollege">
        <label for="comments">Additional Comments:</label>
        <textarea id="comments" name="comments" rows="4"></textarea>
        <input type="submit" value="Submit">
    </form>
</body>
</html>



1. Insert 10 documents in the Customers collection:
db.customers.insertMany([
{ _id: 1, name: "Dinesh Patil", address: "Nashik", email: "dinesh@example.com", phone:
"1234567890" },
{ _id: 2, name: "Sneha Kulkarni", address: "Pune", email: "sneha@example.com", phone:
"0987654321" },
{ _id: 3, name: "Ravi Joshi", address: "Mumbai", email: "ravi@example.com", phone: "1122334455" },
{ _id: 4, name: "Deepa Patil", address: "Pimpri", email: "deepa@example.com", phone: "2233445566"
},
{ _id: 5, name: "Amit Sharma", address: "Nashik", email: "amit@example.com", phone: "3344556677"
},
{ _id: 6, name: "Disha Shetty", address: "Nashik", email: "disha@example.com", phone: "4455667788"
},
{ _id: 7, name: "Mr. Patil", address: "Pimpri", email: "mrpatil@example.com", phone: "5566778899" },
{ _id: 8, name: "Suresh Verma", address: "Mumbai", email: "suresh@example.com", phone:
"6677889900" },
{ _id: 9, name: "Kiran Singh", address: "Pune", email: "kiran@example.com", phone: "7788990011" },
{ _id: 10, name: "Deepak Gupta", address: "Pimpri", email: "deepak@example.com", phone:
"8899001122" }
]);
2. Insert 10 documents in the Loans collection:
db.loans.insertMany([
{ _id: 1, customer_id: 1, loan_type: "Personal", loan_amount: 150000, city: "Nashik", date_taken: new
Date("2023-01-15") },
{ _id: 2, customer_id: 2, loan_type: "Home", loan_amount: 300000, city: "Pune", date_taken: new
Date("2022-03-10") },
{ _id: 3, customer_id: 3, loan_type: "Auto", loan_amount: 200000, city: "Mumbai", date_taken: new
Date("2022-05-22") },
{ _id: 4, customer_id: 4, loan_type: "Personal", loan_amount: 50000, city: "Pimpri", date_taken: new
Date("2023-04-01") },
{ _id: 5, customer_id: 5, loan_type: "Home", loan_amount: 400000, city: "Nashik", date_taken: new
Date("2021-12-15") },
{ _id: 6, customer_id: 6, loan_type: "Personal", loan_amount: 75000, city: "Nashik", date_taken: new
Date("2023-02-11") },
{ _id: 7, customer_id: 7, loan_type: "Auto", loan_amount: 120000, city: "Pimpri", date_taken: new
Date("2023-05-20") },
{ _id: 8, customer_id: 8, loan_type: "Personal", loan_amount: 30000, city: "Mumbai", date_taken: new
Date("2023-06-30") },
{ _id: 9, customer_id: 9, loan_type: "Home", loan_amount: 250000, city: "Pune", date_taken: new
Date("2023-07-14") },
{ _id: 10, customer_id: 10, loan_type: "Personal", loan_amount: 90000, city: "Pimpri", date_taken:
new Date("2023-08-05") }
]);
Step 3: Queries
a. List all customers whose name starts with 'D' character
db.customers.find({ name: { $regex: "^D", $options: "i" } }).forEach(customer => {
print("Customer Name: " + customer.name);
});
b. List the names of customers in descending order who have taken a loan from Pimpri city
db.customers.aggregate([
{
$lookup: {
from: "loans",
localField: "_id",
foreignField: "customer_id",
as: "loan_info"
}
},
{ $unwind: "$loan_info" },
{ $match: { "loan_info.city": "Pimpri" } },
{ $sort: { name: -1 } },
{ $project: { name: 1 } }
]).forEach(customer => {
print("Customer Name: " + customer.name);
});
c. Display customer details having the maximum loan amount
var maxLoan = db.loans.find().sort({ loan_amount: -1 }).limit(1).toArray()[0];
var customer = db.customers.findOne({ _id: maxLoan.customer_id });
print("Customer Name: " + customer.name + ", Loan Amount: " + maxLoan.loan_amount + ", Address: "
+ customer.address);
d. Update the address of the customer whose name is “Mr. Patil” and loan amount is greater than
100000
db.customers.updateOne(
{ name: "Mr. Patil" },
{ $set: { address: "Updated Address, Pimpri" } },
{ $currentDate: { lastModified: true } } // Optional: To track when the update was made
);
db.loans.updateMany(
{ customer_id: db.customers.findOne({ name: "Mr. Patil" })._id, loan_amount: { $gt: 100000 } },
{ $set: { updated: true } } // Optional: If you want to mark the loans as updated
);
---------------------------------------------------------------------------  
slip 10
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>CSS Transition Example</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            display: flex;
            justify-content: center;
            align-items: center;
            height: 100vh;
            margin: 0;
            background-color: #f4f4f4;
        }
        button {
            padding: 10px 20px;
            font-size: 16px;
            border: none;
            cursor: pointer;
            background-color: #4caf50;
            color: #fff;
            border-radius: 4px;
            transition-property: background-color, color;
            transition-duration: 0.6s;
            transition-delay: 0.1s;
        }
        button:hover {
            background-color: #fe3618;
            color: #e0e0e0;
        }
    </style>
</head>
<body>
    <button>Hover Me</button>
</body>
</html>


1. Insert 5 documents in the Products collection:
db.products.insertMany([
{ _id: 1, name: "Smartphone", brand_id: 1, warranty_period: 1, rating: 4.5 },
{ _id: 2, name: "Laptop", brand_id: 2, warranty_period: 2, rating: 4.7 },
{ _id: 3, name: "Headphones", brand_id: 3, warranty_period: 1, rating: 4.2 },
{ _id: 4, name: "Smartwatch", brand_id: 1, warranty_period: 1, rating: 4.8 },
{ _id: 5, name: "Tablet", brand_id: 2, warranty_period: 1, rating: 4.1 }
]);
2. Insert 5 documents in the Brands collection:
db.brands.insertMany([
{ _id: 1, name: "TechBrand A", average_rating: 4.7 },
{ _id: 2, name: "TechBrand B", average_rating: 4.5 },
{ _id: 3, name: "AudioBrand C", average_rating: 4.2 },
{ _id: 4, name: "GadgetBrand D", average_rating: 4.6 },
{ _
id: 5, name: "WearableBrand E", average_rating: 4.9 }
]);
3. Insert 5 documents in the Customers collection:
db.customers.insertMany([
{ _id: 1, name: "John Doe", city: "Pune", purchases: [{ product_id: 1, purchase_date: new Date("2023-
08-15"), bill_amount: 45000 }] },
{ _id: 2, name: "Jane Smith", city: "Mumbai", purchases: [{ product_id: 2, purchase_date: new
Date("2023-07-20"), bill_amount: 75000 }] },
{ _id: 3, name: "David Brown", city: "Nashik", purchases: [{ product_id: 3, purchase_date: new
Date("2023-08-15"), bill_amount: 15000 }] },
{ _id: 4, name: "Emily Davis", city: "Pune", purchases: [{ product_id: 4, purchase_date: new
Date("2023-06-15"), bill_amount: 25000 }] },
{ _id: 5, name: "Michael Wilson", city: "Mumbai", purchases: [{ product_id: 5, purchase_date: new
Date("2023-05-10"), bill_amount: 60000 }] }
]);
Step 3: Queries
a. List the names of products whose warranty period is one year
db.products.find({ warranty_period: 1 }).forEach(product => {
print("Product Name: " + product.name);
});
b. List the customers who made purchases on “15/08/2023”
db.customers.find({ "purchases.purchase_date": new Date("2023-08-15") }).forEach(customer => {
print("Customer Name: " + customer.name + ", City: " + customer.city);
});
c. Display the names of products with the brand which has the highest rating
var highestRatedBrand = db.brands.find().sort({ average_rating: -1 }).limit(1).toArray()[0];
db.products.find({ brand_id: highestRatedBrand._id }).forEach(product => {
print("Product Name: " + product.name + ", Brand: " + highestRatedBrand.name);
});
d. Display customers who stay in a specific city and have a bill amount greater than 50000
var targetCity = "Pune"; // Change this to the desired city
db.customers.find({
city: targetCity,
"purchases.bill_amount": { $gt: 50000 }
}).forEach(customer => {
print("Customer Name: " + customer.name + ", City: " + customer.city);
});


---------------------------------------------------------------------------  
slip 11
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <style>
        body {
            margin: 0;
            padding: 0;
            font-family: Arial, sans-serif;
            display: flex;
            flex-direction: column;
            height: 100vh;
        }
        header {
            background-color: #333;
            color: #fff;
            text-align: center;
            padding: 10px;
        }
        main {
            display: flex;
            flex: 1;
        }
        nav {
            width: 200px;
            background-color: #f0f0f0;
            padding: 10px;
            box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);
        }
        nav a {
            display: block;
            margin-bottom: 10px;
            text-decoration: none;
            color: #333;
        }
        article {
            flex: 1;
            padding: 20px;
        }
    </style>
</head>
<body>
    <header>
        <h1>Company Name</h1>
    </header>
    <main>
        <nav>
            <a href="#" onclick="showDepartment('department1'); return false;">Department 1</a>
            <a href="#" onclick="showDepartment('department2'); return false;">Department 2</a>
            <a href="#" onclick="showDepartment('department3'); return false;">Department 3</a>
            <!-- Add more departments as needed -->
        </nav>
        <article id="department-info">
            <!-- Department information will be displayed here -->
        </article>
    </main>
    <script>
        function showDepartment(department) {
            // You can replace the following line with an AJAX request to fetch department information from the server
            const departmentInfo = getDepartmentInfo(department);
            // Display department information in the third frame (article)
            document.getElementById('department-info').innerHTML = departmentInfo;
        }
        function getDepartmentInfo(department) {
            // Simulated department information, replace this with actual data
            const departmentData = {
                department1: 'Information for Department 1',
                department2: 'Information for Department 2',
                department3: 'Information for Department 3',
                // Add more departments as needed
            };
            return departmentData[department] || 'Department information not available.';
        }
    </script>
</body>
</html>


Products Collection
product_id: Product ID
product_name: Product Name
category: Product Category
price: Price
stock_qty: Quantity in stock2. Customers Collection
cust_id: Customer ID
cust_name: Customer Name
city: City
email: Email
Products Collection
{ product_id: 101, product_name: "Laptop", category: "Electronics", price: 50000, stock_qty:
20 }
{ product_id: 102, product_name: "Smartphone", category: "Electronics", price: 30000,
stock_qty: 50 }
{ product_id: 103, product_name: "Printer", category: "Electronics", price: 15000, stock_qty:
15 }
{ product_id: 104, product_name: "Chair", category: "Furniture", price: 5000, stock_qty: 40 }
{ product_id: 105, product_name: "Desk", category: "Furniture", price: 8000, stock_qty: 30 }
---
Customers Collection
{ cust_id: 201, cust_name: "Mr. Rajiv", city: "Pune", email: "rajiv@gmail.com" }
{ cust_id: 202, cust_name: "Sneha Patil", city: "Mumbai", email: "sneha@gmail.com" }
{ cust_id: 203, cust_name: "Rahul Deshmukh", city: "Pune", email: "rahul@gmail.com" }
{ cust_id: 204, cust_name: "Deepali Joshi", city: "Nashik", email: "deepali@gmail.com" }{ cust_id: 205, cust_name: "Rohit Rane", city: "Pune", email: "rohit@gmail.com" }
a) List all products in the inventory
db.products.find({}, { _id:0, product_name:1, category:1, price:1, stock_qty:1 })
Output:
{ "product_name": "Laptop", "category": "Electronics", "price": 50000, "stock_qty": 20 }
{ "product_name": "Smartphone", "category": "Electronics", "price": 30000, "stock_qty": 50
}
{ "product_name": "Printer", "category": "Electronics", "price": 15000, "stock_qty": 15 }
{ "product_name": "Chair", "category": "Furniture", "price": 5000, "stock_qty": 40 }
{ "product_name": "Desk", "category": "Furniture", "price": 8000, "stock_qty": 30 }
---
b) List the details of orders with a value > 20000
db.orders.find({ order_value: { $gt: 20000 } }, { _id:0 })
Output:
{ order_id: 301, cust_id: 201, product_id: 101, order_qty: 1, order_value: 50000, order_date:
"2023-08-01" }
{ order_id: 302, cust_id: 202, product_id: 102, order_qty: 2, order_value: 60000, order_date:
"2023-08-05" }---
c) List all the orders which have not been processed (invoice not generated)
db.invoices.aggregate([
{ $match: { status: "Not Processed" } },
{ $lookup: {
from: "orders",
localField: "order_id",
foreignField: "order_id",
as: "order_details"
}},
{ $project: { _id:0, order_id:1, order_details:1 } }
])
Output:
{ order_id: 404, order_details: [ { order_id: 304, cust_id: 204, product_id: 104, order_qty: 4,
order_value: 20000, order_date: "2023-08-10" } ] }
{ order_id: 405, order_details: [ { order_id: 305, cust_id: 201, product_id: 105, order_qty: 2,
order_value: 16000, order_date: "2023-08-12" } ] }
---
d) List all the orders along with their invoice for “Mr. Rajiv”
db.customers.aggregate([
{ $match: { cust_name: "Mr. Rajiv" } },
{ $lookup: {from: "orders",
localField: "cust_id",
foreignField: "cust_id",
as: "orders"
}},
{ $unwind: "$orders" },
{ $lookup: {
from: "invoices",
localField: "orders.order_id",
foreignField: "order_id",
as: "invoice"
}},
{ $project: { _id:0, cust_name:1, orders:1, invoice:1 } }
])
Output:
{
"cust_name": "Mr. Rajiv",
"orders": { "order_id": 301, "cust_id": 201, "product_id": 101, "order_qty": 1,
"order_value": 50000, "order_date": "2023-08-01" },
"invoice": [ { "invoice_id": 401, "order_id": 301, "invoice_date": "2023-08-02", "status":
"Processed" } ]
} {
"cust_name": "Mr. Rajiv",
"orders": { "order_id": 305, "cust_id": 201, "product_id": 105, "order_qty": 2,
"order_value": 16000, "order_date": "2023-08-12" },
"invoice": [ { "invoice_id": 405, "order_id": 305, "invoice_date": "", "status": "Not
Processed" } ]
}
---------------------------------------------------------------------------  
slip 12
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Customer Registration Form</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            padding: 20px;
        }
        form {
            max-width: 600px;
            margin: auto;
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
        }
        input,
        select,
        textarea {
            width: 100%;
            padding: 8px;
            margin-bottom: 16px;
            box-sizing: border-box;
            border: 1px solid #ccc;
            border-radius: 4px;
        }
        textarea {
            resize: vertical;
            height: 100px;
        }
        button {
            background-color: #4caf50;
            color: #fff;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button[type="reset"] {
            background-color: #f44336;
        }
    </style>
</head>
<body>
    <form id="customerRegistrationForm">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required>
        <label for="contactNo">Contact Number:</label>
        <input type="tel" id="contactNo" name="contactNo" pattern="[0-9]{10}" required>
        <small>Enter a 10-digit phone number.</small>
        <label for="gender">Gender:</label>
        <select id="gender" name="gender" required>
            <option value="male">Male</option>
            <option value="female">Female</option>
            <option value="other">Other</option>
        </select>
        <label for="preferredDays">Preferred Days of Purchasing:</label>
        <input type="text" id="preferredDays" name="preferredDays">
        <label for="favoriteItem">Favorite Item:</label>
        <select id="favoriteItem" name="favoriteItem">
            <option value="clothing">Clothing</option>
            <option value="electronics">Electronics</option>
            <option value="homeAppliances">Home Appliances</option>
            <option value="groceries">Groceries</option>
        </select>
        <label for="suggestions">Suggestions:</label>
        <textarea id="suggestions" name="suggestions"></textarea>
        <button type="submit">Submit</button>
        <button type="reset">Reset</button>
    </form>
</body>
</html>


=>
Collections and Attributes
1. Movies Collection
movie_id: Movie ID
movie_name: Movie Name
budget: Budget
release_year: Release Year
actors: Array of actor IDs
2. Actors Collection
actor_id: Actor ID
actor_name: Actor Name
gender: Gender
dob: Date of Birth
3. Producers Collectionproducer_id: Producer ID
producer_name: Producer Name
movies: Array of movie IDs produced
---
Insert Documents
Movies Collection
{ movie_id: 101, movie_name: "Action Hero", budget: 50000000, release_year: 2023, actors:
[201, 202] }
{ movie_id: 102, movie_name: "Comedy King", budget: 30000000, release_year: 2023,
actors: [203, 204] }
{ movie_id: 103, movie_name: "Romantic Saga", budget: 70000000, release_year: 2023,
actors: [202, 205] }
{ movie_id: 104, movie_name: "Thriller Night", budget: 70000000, release_year: 2022,
actors: [201, 203] }
{ movie_id: 105, movie_name: "Drama Queen", budget: 40000000, release_year: 2023,
actors: [204, 205] }
---
Actors Collection
{ actor_id: 201, actor_name: "Akshay", gender: "Male", dob: "1980-01-01" }{ actor_id: 202, actor_name: "Salman", gender: "Male", dob: "1975-12-27" }
{ actor_id: 203, actor_name: "Katrina", gender: "Female", dob: "1983-07-16" }
{ actor_id: 204, actor_name: "Deepika", gender: "Female", dob: "1986-01-05" }
{ actor_id: 205, actor_name: "Ranveer", gender: "Male", dob: "1985-07-06" }
---
Producers Collection
{ producer_id: 301, producer_name: "Ramesh", movies: [101, 104] }
{ producer_id: 302, producer_name: "Suresh", movies: [102, 103] }
{ producer_id: 303, producer_name: "Mahesh", movies: [103, 105] }
{ producer_id: 304, producer_name: "Rajesh", movies: [101, 102] }
{ producer_id: 305, producer_name: "Dinesh", movies: [104, 105] }
---
Queries and Solutions
a) List the names of movies with the highest budget
db.movies.find().sort({ budget: -1 }).limit(1)
Output:
{ "movie_name": "Romantic Saga", "budget": 70000000 }> Note: "Thriller Night" also has the same budget of 70000000.
---
b) Display the details of producers who have produced more than one movie in a year
db.producers.find({
$where: "this.movies.length > 1"
})
Output:
{ producer_name: "Ramesh", movies: [101, 104] }
{ producer_name: "Suresh", movies: [102, 103] }
{ producer_name: "Mahesh", movies: [103, 105] }
{ producer_name: "Rajesh", movies: [101, 102] }
{ producer_name: "Dinesh", movies: [104, 105] }
---
c) List the names of actors who have acted in at least one movie in which ‘Akshay’ has acted
// Step 1: Find movies where Akshay acted
var akshayMovies = db.movies.find({ actors: 201 }).map(m => m.actors).flat();// Step 2: Find all unique actor IDs except Akshay
var actorIDs = [...new Set(akshayMovies)].filter(id => id !== 201);
// Step 3: Find actor names
db.actors.find({ actor_id: { $in: actorIDs } }, { _id:0, actor_name:1 })
Output:
{ "actor_name": "Salman" }
{ "actor_name": "Katrina" }
---
d) List the names of movies produced by more than one producer
// Aggregate by movie_id in producers collection
db.producers.aggregate([
{ $unwind: "$movies" },
{ $group: { _id: "$movies", count: { $sum: 1 } } },
{ $match: { count: { $gt: 1 } } },
{ $lookup: {
from: "movies",
localField: "_id",
foreignField: "movie_id",
as: "movie_details"
}},
{ $project: { _id:0, movie_details:1 } }
])Output:
{ "movie_details": [ { "movie_name": "Action Hero", "budget": 50000000, "release_year":
2023, "actors": [201, 202] } ] }
{ "movie_details": [ { "movie_name": "Comedy King", "budget": 30000000, "release_year":
2023, "actors": [203, 204] } ] }
{ "movie_details": [ { "movie_name": "Romantic Saga", "budget": 70000000, "release_year":
2023, "actors": [202, 205] } ] }
{ "movie_details": [ { "movie_name": "Thriller Night", "budget": 70000000, "release_year":
2022, "actors": [201, 203] } ] }
{ "movie_details": [ { "movie_name": "Drama Queen", "budget": 40000000, "release_year":
2023, "actors": [204, 205] } ] }
> All movies in this dataset are produced by more than one producer
---------------------------------------------------------------------------  
slip 13
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Fictional Tech Product</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            background-color: #f4f4f4;
        }
        header {
            background-color: #333;
            color: #fff;
            text-align: center;
            padding: 10px;
        }
        nav {
            background-color: #555;
            color: #fff;
            padding: 10px;
        }
        nav a {
            text-decoration: none;
            color: #fff;
            margin: 0 15px;
        }
        section {
            max-width: 800px;
            margin: 20px auto;
            padding: 20px;
            background-color: #fff;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        aside {
            float: right;
            width: 30%;
            padding: 20px;
            background-color: #ddd;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        footer {
            background-color: #333;
            color: #fff;
            text-align: center;
            padding: 10px;
            clear: both;
        }
    </style>
</head>
<body>
    <header>
        <h1>Fictional Tech Product</h1>
    </header>
    <nav>
        <a href="#features">Features</a>
        <a href="#specs">Specifications</a>
        <a href="#buy">Buy Now</a>
    </nav>
    <section id="features">
        <h2>Features</h2>
        <p>This fictional tech product comes with amazing features to enhance your
            experience.</p>
        <ul>
            <li>Wireless Connectivity</li>
            <li>Long Battery Life</li>
            <li>High-Resolution Display</li>
            <li>Advanced Security</li>
        </ul>
    </section>
    <section id="specs">
        <h2>Specifications</h2>
        <p>Check out the technical specifications of our product:</p>
        <ul>
            <li>Processor: Quad-core, 2.0 GHz</li>
            <li>Memory: 8 GB RAM</li>
            <li>Storage: 256 GB SSD</li>
            <li>Operating System: TechOS</li>
        </ul>
    </section>
    <section id="buy">
        <h2>Buy Now</h2>
        <p>Purchase this amazing product today!</p>
    </section>
    <aside>
        <h2>Special Offer</h2>
        <p>For a limited time, get a 20% discount on your purchase. Use code: TECH20.</p>
    </aside>
    <footer>
        <p>&copy; 2023 Fictional Tech Company | Contact us at info@fictionaltech.com</p>
    </footer>
</body>
</html>

Students Collection
db.students.insertMany([
{ student_id: 1, name:"Amit", class:"FY" },{ student_id: 2, name:"Riya", class:"SY" },
{ student_id: 3, name:"Sahil", class:"FY" },
{ student_id: 4, name:"Neha", class:"TY" },
{ student_id: 5, name:"Rohan", class:"FY" },
{ student_id: 6, name:"Simran", class:"SY" },
{ student_id: 7, name:"Akshay", class:"FY" },
{ student_id: 8, name:"Pooja", class:"TY" },
{ student_id: 9, name:"Vivek", class:"FY" },
{ student_id: 10, name:"Sneha", class:"SY" }
])
---
2. Competitions Collection
db.competitions.insertMany([
{ comp_id: 101, name:"Programming", year:2025 },
{ comp_id: 102, name:"E-Rangoli", year:2025 },
{ comp_id: 103, name:"Quiz", year:2025 },
{ comp_id: 104, name:"Debate", year:2025 },
{ comp_id: 105, name:"Sports", year:2025 },
{ comp_id: 106, name:"Painting", year:2025 },
{ comp_id: 107, name:"Coding Hackathon", year:2025 },
{ comp_id: 108, name:"Drama", year:2025 },
{ comp_id: 109, name:"Singing", year:2025 },
{ comp_id: 110, name:"Dancing", year:2025 }
])---
3. Participation Collection
db.participation.insertMany([
{ student_id:1, comp_id:101, rank:1 },
{ student_id:3, comp_id:101, rank:2 },
{ student_id:5, comp_id:101, rank:3 },
{ student_id:2, comp_id:102, rank:1 },
{ student_id:3, comp_id:102, rank:2 },
{ student_id:7, comp_id:102, rank:3 },
{ student_id:9, comp_id:102, rank:4 },
{ student_id:1, comp_id:103, rank:1 },
{ student_id:4, comp_id:103, rank:2 },
{ student_id:6, comp_id:103, rank:3 },
{ student_id:8, comp_id:104, rank:1 },
{ student_id:10, comp_id:104, rank:2 },
{ student_id:1, comp_id:105, rank:1 },
{ student_id:5, comp_id:105, rank:2 },
{ student_id:9, comp_id:105, rank:3 }
])
---
Queries
a) Average number of students participating in each competitiondb.participation.aggregate([
{ $group: { _id:"$comp_id", studentCount: { $sum:1 } } },
{ $group: { _id:null, avgStudents: { $avg:"$studentCount" } } }
])
Output (example):
{ "avgStudents": 2.7 }
---
b) Number of students for Programming competition
db.participation.aggregate([
{ $match: { comp_id: 101 } },
{ $group: { _id:"$comp_id", studentCount: { $sum:1 } } }
])
Output:
{ "_id": 101, "studentCount": 3 }
---
c) Names of first three winners of each competitiondb.participation.aggregate([
{ $match: { rank: { $lte: 3 } } },
{ $lookup: { from:"students", localField:"student_id", foreignField:"student_id",
as:"student" } },
{ $lookup: { from:"competitions", localField:"comp_id", foreignField:"comp_id",
as:"competition" } },
{ $project: { _id:0, competition:"$competition.name", student:"$student.name", rank:1 } },
{ $sort: { "comp_id":1, "rank":1 } }
])
Output (example):
{ "competition":["Programming"], "student":["Amit"], "rank":1 }
{ "competition":["Programming"], "student":["Sahil"], "rank":2 }
{ "competition":["Programming"], "student":["Rohan"], "rank":3 }
{ "competition":["E-Rangoli"], "student":["Riya"], "rank":1 }
{ "competition":["E-Rangoli"], "student":["Sahil"], "rank":2 }
{ "competition":["E-Rangoli"], "student":["Akshay"], "rank":3 }
...
---
d) Students from class 'FY' participated in 'E-Rangoli'
db.participation.aggregate([
{ $lookup: { from:"students", localField:"student_id", foreignField:"student_id",
as:"student" } },
{ $lookup: { from:"competitions", localField:"comp_id", foreignField:"comp_id",
as:"competition" } },
{ $unwind:"$student" },{ $unwind:"$competition" },
{ $match: { "student.class":"FY", "competition.name":"E-Rangoli" } },
{ $project: { _id:0, student:"$student.name", class:"$student.class",
competition:"$competition.name" } }
])
Output:
{ "student":"Sahil", "class":"FY", "competition":"E-Rangoli" }
{ "student":"Akshay", "class":"FY", "competition":"E-Rangoli" }


---------------------------------------------------------------------------  
slip 14
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Travel Plan Booking Form</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            margin: 20px;
        }
        form {
            max-width: 400px;
            margin: auto;
        }
        label {
            display: block;
            margin-bottom: 8px;
        }
        input, select {
            width: 100%;
            padding: 8px;
            margin-bottom: 12px;
            box-sizing: border-box;
        }
        input[type="checkbox"] {
            width: auto;
            margin-right: 5px;
        }
        button {
            background-color: #4CAF50;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        button[type="reset"] {
            background-color: #f44336;
        }
    </style>
</head>
<body>
    <form id="travelForm">
        <label for="name">Name:</label>
        <input type="text" id="name" name="name" required>
        <label for="address">Address:</label>
        <input type="text" id="address" name="address" required>
        <label for="contact">Contact No.:</label>
        <input type="tel" id="contact" name="contact" required>
        <label>Gender:</label>
        <label for="male">Male</label>
        <input type="radio" id="male" name="gender" value="male" required>
        <label for="female">Female</label>
        <input type="radio" id="female" name="gender" value="female" required>
        <label for="season">Preferred Season:</label>
        <label for="spring">Spring</label>
        <input type="checkbox" id="spring" name="season" value="spring">
        <label for="summer">Summer</label>
        <input type="checkbox" id="summer" name="season" value="summer">
        <label for="autumn">Autumn</label>
        <input type="checkbox" id="autumn" name="season" value="autumn">
        <label for="winter">Winter</label>
        <input type="checkbox" id="winter" name="season" value="winter">
        <label for="locationType">Location Type:</label>
        <select id="locationType" name="locationType" required>
            <option value="" disabled selected>Select Location Type</option>
            <option value="beach">Beach</option>
            <option value="mountain">Mountain</option>
            <option value="city">City</option>
            <option value="countryside">Countryside</option>
        </select>
        <div style="text-align: center; margin-top: 20px;">
            <button type="submit">Submit</button>
            <button type="reset">Reset</button>
        </div>
    </form>
    <script>
        document.getElementById('travelForm').addEventListener('submit', function (e) {
            e.preventDefault(); // Prevent the default form submission
            // You can add code here to handle the form submission, e.g., sending data to a server
        });
    </script>
</body>
</html>


=>
Create Nodes// Students
CREATE (s1:Student {name:"Amit", category:"OBC", income:250000}),
(s2:Student {name:"Riya", category:"GEN", income:400000}),
(s3:Student {name:"Sahil", category:"OBC", income:200000})
// Scholarships
CREATE (sch1:Scholarship {name:"Merit Scholarship", category:"OBC", incomeLimit:300000,
year:"2020-2021"}),
(sch2:Scholarship {name:"Talent Scholarship", category:"GEN", incomeLimit:500000,
year:"2020-2021"}),
(sch3:Scholarship {name:"Sports Scholarship", category:"OBC", incomeLimit:250000,
year:"2020-2021"})
---
Create Relationships
// Students apply for scholarships
CREATE (s1)-[:APPLIED_FOR {year:"2020-2021"}]->(sch1),
(s1)-[:APPLIED_FOR {year:"2020-2021"}]->(sch3),
(s2)-[:APPLIED_FOR {year:"2020-2021"}]->(sch2),
(s3)-[:APPLIED_FOR {year:"2020-2021"}]->(sch1)
// Students recommend scholarships
CREATE (s1)-[:RECOMMENDED]->(s2),
(s3)-[:RECOMMENDED]->(s1)---
Queries
a) List the names of scholarships for OBC category
MATCH (sch:Scholarship)
WHERE sch.category="OBC"
RETURN sch.name
Output:
"Merit Scholarship"
"Sports Scholarship"
---
b) Count number of students benefitted by a scholarship in 2020-2021
MATCH (s:Student)-[r:APPLIED_FOR]->(sch:Scholarship)
WHERE sch.name="Merit Scholarship" AND r.year="2020-2021"
RETURN count(s) AS no_of_students
Output:
2---
c) Update the income limit for a scholarship
MATCH (sch:Scholarship {name:"Merit Scholarship"})
SET sch.incomeLimit = 350000
RETURN sch.name, sch.incomeLimit
Output:
"Merit Scholarship", 350000
---
d) List the most popular scholarship
MATCH (s:Student)-[:APPLIED_FOR]->(sch:Scholarship)
RETURN sch.name, count(s) AS applicants
ORDER BY applicants DESC
LIMIT 1
Output:
"Merit Scholarship"
---------------------------------------------------------------------------  
slip 15
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang=”en”>
<head>
    <meta charset=”UTF-8”>
    <meta name=”viewport” content=”width=device-width, initial-scale=1.0”>
    <title>Registration Form</title>
    <link rel=”stylesheet” href=https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/css/bootstrap.min.css>
</head>
<body>
    <div class=”container”>
        <div class=”row”>
            <div class=”col-md-6 offset-md-3”>
                <h4>Registration Form</h4>
                <form>
                    <div class=”form-group”>
                        <label for=”firstname”>First Name</label>
                        <input type=”text” class=”form-control” id=”firstname” required>
                    </div>
                    <div class=”form-group”>
                        <label for=”lastname”>Last Name</label>
                        <input type=”text” class=”form-control” id=”lastname” required>
                    </div>
                    <div class=”form-group”>
                        <label for=”department”>Department / Office</label>
                        <select class=”form-control” id=”department” required>
                            <option>IT</option>
                            <option>Sales</option>
                            <option>HR</option>
                            <option>Marketing</option>
                        </select>
                    </div>
                    <div class=”form-group”>
                        <label for=”username”>Username</label>
                        <input type=”text” class=”form-control” id=”username” required>
                    </div>
                    <div class=”form-group”>
                        <label for=”password”>Password</label>
                        <input type=”password” class=”form-control” id=”password” required>
                    </div>
                    <div class=”form-group”>
                        <label for=”confirm-password”>Confirm Password</label>
                        <input type=”password” class=”form-control” id=”confirm-password” required>
                    </div>
                    <div class=”form-group”>
                        <label for=”email”>E-Mail</label>
                        <input type=”email” class=”form-control” id=”email” required>
                    </div>
                    <div class=”form-group”>
                        <label for=”contact”>Contact No.</label>
                        <input type=”text” class=”form-control” id=”contact” required>
                    </div>
                    <button type=”submit” class=”btn btn-primary”>Submit</button>
                </form>
            </div>
        </div>
    </div>
    <script src=https://code.jquery.com/jquery-3.5.1.slim.min.js></script>
    <script src=https://cdn.jsdelivr.net/npm/@popperjs/core@2.9.3/dist/umd/popper.min.js></script>
    <script src=https://stackpath.bootstrapcdn.com/bootstrap/4.5.0/js/bootstrap.min.js></script>
</body>
</html>

=>Labels and Relationships
Labels:
Movie → Properties: title, genre, year, business
Actor → Properties: name, dob, role
Relationships:
(:Actor)-[:ACTED_IN]->(:Movie) → Properties: role
High-level Graph Model:
(Actor)-[:ACTED_IN {role}]->(Movie)
---
Create Nodes and Relationships
// Movies
CREATE (m1:Movie {title:"Movie1", genre:"Action", year:2024, business:1000000}),
(m2:Movie {title:"Movie2", genre:"Drama", year:2023, business:1500000}),
(m3:Movie {title:"Movie3", genre:"Romance", year:2025, business:900000})
// ActorsCREATE (a1:Actor {name:"Shahrukh Khan", dob:"1965-11-02"}),
(a2:Actor {name:"Amitabh Bachchan", dob:"1942-10-11"}),
(a3:Actor {name:"Deepika Padukone", dob:"1986-01-05"})
// Relationships
CREATE (a1)-[:ACTED_IN {role:"Hero"}]->(m1),
(a1)-[:ACTED_IN {role:"Hero"}]->(m2),
(a2)-[:ACTED_IN {role:"Supporting"}]->(m2),
(a3)-[:ACTED_IN {role:"Heroine"}]->(m3)
---
Queries
a) Find movie which made highest business
MATCH (m:Movie)
RETURN m.title, m.business
ORDER BY m.business DESC
LIMIT 1
Output:
"Movie2", 1500000
---b) Display details of movie along with actors
MATCH (a:Actor)-[:ACTED_IN]->(m:Movie)
RETURN m.title, m.genre, m.year, m.business, collect(a.name) AS actors
Output (example):
"Movie1", "Action", 2024, 1000000, ["Shahrukh Khan"]
"Movie2", "Drama", 2023, 1500000, ["Shahrukh Khan","Amitabh Bachchan"]
"Movie3", "Romance", 2025, 900000, ["Deepika Padukone"]
---
c) List all movies of “Shahrukh Khan”
MATCH (:Actor {name:"Shahrukh Khan"})-[:ACTED_IN]->(m:Movie)
RETURN m.title
Output:
"Movie1"
"Movie2"

---------------------------------------------------------------------------  
slip 16
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Contact Form</title>
    <link href="https://cdn.jsdelivr.net/npm/bootstrap@5.3.2/dist/css/bootstrap.min.css" rel="stylesheet">
</head>
<body>
    <div class="container mt-5">
        <h2>Contact Us</h2>
        <form>
            <div class="mb-3">
                <label class="form-label">Name</label>
                <input type="text" class="form-control" required>
            </div>
            <div class="mb-3">
                <label class="form-label">Email</label>
                <input type="email" class="form-control" required>
            </div>
            <div class="mb-3">
                <label class="form-label">Message</label>
                <textarea class="form-control" rows="4" required></textarea>
            </div>
            <button type="submit" class="btn btn-primary">Submit</button>
            <button type="reset" class="btn btn-secondary">Reset</button>
        </form>
    </div>
</body>
</html>

=>
Labels and Relationships
Labels:
Person → name, age, city
Company → name (Zomato, Swiggy)
Restaurant → name, area, rating
Relationships:
(:Person)-[:ORDERED {date}]->(:Company)(:Person)-[:RATED {stars}]->(:Company)
(:Company)-[:PARTNERED_WITH]->(:Restaurant)
(:Person)-[:RECOMMENDED]->(:Person)
Graph Model:
(Person)-[:ORDERED {date}]->(Company)-[:PARTNERED_WITH]->(Restaurant)
(Person)-[:RATED {stars}]->(Company)
(Person)-[:RECOMMENDED]->(Person)
---
Create Nodes and Relationships
// Companies
CREATE (c1:Company {name:"Zomato"}),
(c2:Company {name:"Swiggy"})
// Restaurants
CREATE (r1:Restaurant {name:"Hotel A", area:"Nashik", rating:5}),
(r2:Restaurant {name:"Hotel B", area:"Pune", rating:3}),
(r3:Restaurant {name:"Hotel C", area:"Nashik", rating:4})
// PersonsCREATE (p1:Person {name:"Sahil", city:"Nashik"}),
(p2:Person {name:"Simran", city:"Pune"}),
(p3:Person {name:"Amit", city:"Nashik"})
// Relationships
CREATE (p1)-[:ORDERED {date:"2023-01-01"}]->(c2),
(p2)-[:ORDERED {date:"2023-01-01"}]->(c2),
(p3)-[:ORDERED {date:"2023-01-02"}]->(c1)
CREATE (p1)-[:RATED {stars:5}]->(c2),
(p2)-[:RATED {stars:4}]->(c2),
(p3)-[:RATED {stars:3}]->(c1)
CREATE (c1)-[:PARTNERED_WITH]->(r2),
(c2)-[:PARTNERED_WITH]->(r1),
(c2)-[:PARTNERED_WITH]->(r3)
CREATE (p1)-[:RECOMMENDED]->(p2)
---
Queries
a) Count number of customers who placed order on “1/1/2023”
MATCH (p:Person)-[o:ORDERED]->(c:Company)
WHERE o.date="2023-01-01"
RETURN count(p) AS no_of_customersOutput:
2
---
b) List names of customers whose name starts with S and ordered via Swiggy
MATCH (p:Person)-[:ORDERED]->(c:Company {name:"Swiggy"})
WHERE p.name STARTS WITH "S"
RETURN p.name
Output:
"Sahil"
"Simran"
---
c) List names of restaurants with high rating (>=4)
MATCH (r:Restaurant)
WHERE r.rating >= 4
RETURN r.name
Output:"Hotel A"
"Hotel C"
---
d) List the most recommended hotels in Nashik
MATCH (p:Person)-[:ORDERED]->(c:Company)-[:PARTNERED_WITH]->(r:Restaurant)
WHERE r.area="Nashik"
RETURN r.name, count(p) AS recommendations
ORDER BY recommendations DESC
LIMIT 1
Output:
"Hotel A", 1



---------------------------------------------------------------------------  
slip 17
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Box Example</title>
    <style>
        .box {
            border: 2px solid #000;
            padding: 10px;
            background-color: yellow;
            width: 300px;
        }
        .box div {
            margin: 5px 0;
            background-color: yellow;
            padding: 5px;
            border: 2px solid #000;
        }
        .Outerbox {
            width: 400px;
            height: 200px;
            display: flex;
            border: 2px solid #000;
            background-color: orange;
            justify-content: center;
            align-items: center;
        }
    </style>
</head>
<body>
    <div class="Outerbox">
        <div class="box">
            <div>M.Sc Computer Science</div>
            <div>Academic Year 2023-24</div>
        </div>
        <div>
</body>
</html>

=>
Labels and Relationships
Labels:
Author → name, dob
Book → title, genre
Publisher → name, location
Reader → name, city
Relationships:
(:Author)-[:WROTE]->(:Book)
(:Book)-[:PUBLISHED_BY]->(:Publisher)
(:Reader)-[:READ]->(:Book)
(:Reader)-[:RATED {stars}]->(:Book)
(:Reader)-[:RECOMMENDED]->(:Reader)Graph Model:
(Author)-[:WROTE]->(Book)-[:PUBLISHED_BY]->(Publisher)
(Reader)-[:READ]->(Book)
(Reader)-[:RATED {stars}]->(Book)
(Reader)-[:RECOMMENDED]->(Reader)
---
Create Nodes and Relationships
// Authors
CREATE (a1:Author {name:"John Doe"}),
(a2:Author {name:"Alice Smith"})
// Books
CREATE (b1:Book {title:"Comics Adventures", genre:"Comics"}),
(b2:Book {title:"Science 101", genre:"Science"})
// Publishers
CREATE (p1:Publisher {name:"Sage", location:"Delhi"}),
(p2:Publisher {name:"Nova", location:"Mumbai"})
// Readers
CREATE (r1:Reader {name:"Ravi", city:"Pune"}),
(r2:Reader {name:"Sara", city:"Nashik"})
// RelationshipsCREATE (a1)-[:WROTE]->(b1),
(a2)-[:WROTE]->(b2)
CREATE (b1)-[:PUBLISHED_BY]->(p1),
(b2)-[:PUBLISHED_BY]->(p2)
CREATE (r1)-[:READ]->(b1),
(r2)-[:READ]->(b2)
CREATE (r1)-[:RATED {stars:4}]->(b1),
(r2)-[:RATED {stars:2}]->(b2)
CREATE (r1)-[:RECOMMENDED]->(r2)
---
Queries
a) List authors who wrote “Comics”
MATCH (a:Author)-[:WROTE]->(b:Book {genre:"Comics"})
RETURN a.name
Output:
"John Doe"---
b) Count readers of a book published by “Sage”
MATCH (r:Reader)-[:READ]->(b:Book)-[:PUBLISHED_BY]->(p:Publisher {name:"Sage"})
RETURN count(r) AS no_of_readers
Output:
1
---
c) List all publishers whose name starts with “N”
MATCH (p:Publisher)
WHERE p.name STARTS WITH "N"
RETURN p.name
Output:
"Nova"
---
d) List names of people who have given rating >=3 for a bookMATCH (r:Reader)-[ra:RATED]->(b:Book)
WHERE ra.stars >= 3
RETURN r.name, b.title
Output:
"Ravi", "Comics Adventures"



---------------------------------------------------------------------------  
slip 18
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>2D Transformation Example</title>
    <style>
        body {
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
            margin: 0;
        }
        img {
            transform-origin: center center;
            transition: transform 0.5s ease-in-out;
        }
    </style>
</head>
<body>
    <img id="transformImage" src="https://picsum.photos/200" alt="Transformed Image" width="200">
    <script>
        const transformImage = document.getElementById('transformImage');
        // Apply combined transformations after 1 second
        setTimeout(() => {
            transformImage.style.transform = 'rotate(45deg) scale(1.5) translate(50px, 50px)';
        }, 1000);
    </script>
</body>
</html>


d. List all the who visits more than 2 hospitals [4]
=>
Labels and Relationships
Labels:
Doctor → name, specialization
Hospital → name, area
Clinic → name, area
Person → name, city
Relationships:
(:Doctor)-[:VISITS]->(:Hospital)
(:Doctor)-[:OWNS]->(:Clinic)
(:Person)-[:REVIEWED {rating}]->(:Doctor)
(:Person)-[:RECOMMENDED]->(:Doctor)
Graph Model:(Doctor)-[:VISITS]->(Hospital)
(Doctor)-[:OWNS]->(Clinic)
(Person)-[:REVIEWED]->(Doctor)
(Person)-[:RECOMMENDED]->(Doctor)
---
Create Nodes and Relationships
// Doctors
CREATE (d1:Doctor {name:"Dr. A", specialization:"Pediatrics"}),
(d2:Doctor {name:"Dr. B", specialization:"Orthopedic"}),
(d3:Doctor {name:"Dr. C", specialization:"Heart Specialist"})
// Hospitals
CREATE (h1:Hospital {name:"Seren Medows", area:"Pune"}),
(h2:Hospital {name:"City Hospital", area:"Pune"}),
(h3:Hospital {name:"Green Care", area:"Pune"})
// Clinics
CREATE (c1:Clinic {name:"Dr. A Clinic", area:"Pune"})
// Persons
CREATE (p1:Person {name:"Ravi"}),
(p2:Person {name:"Simran"})
// RelationshipsCREATE (d1)-[:VISITS]->(h1),
(d1)-[:VISITS]->(h2),
(d1)-[:VISITS]->(h3),
(d2)-[:VISITS]->(h2),
(d3)-[:OWNS]->(c1)
CREATE (p1)-[:RECOMMENDED]->(d1),
(p2)-[:REVIEWED {rating:5}]->(d1)
---
Queries
a) List Orthopedic doctors in Pune
MATCH (d:Doctor)-[:VISITS]->(h:Hospital {area:"Pune"})
WHERE d.specialization="Orthopedic"
RETURN d.name
Output:
"Dr. B"
---
b) List doctors with specialization “Pediatrics”MATCH (d:Doctor)
WHERE d.specialization="Pediatrics"
RETURN d.name
Output:
"Dr. A"
---
c) Most recommended Pediatrics in Seren Medows
MATCH (p:Person)-[:RECOMMENDED]->(d:Doctor)-[:VISITS]->(h:Hospital {name:"Seren
Medows"})
WHERE d.specialization="Pediatrics"
RETURN d.name, count(p) AS recommendations
ORDER BY recommendations DESC
LIMIT 1
Output:
"Dr. A", 1
---
d) List all doctors who visit more than 2 hospitals
MATCH (d:Doctor)-[:VISITS]->(h:Hospital)WITH d, count(h) AS hosp_count
WHERE hosp_count > 2
RETURN d.name
Output:
"Dr.

---------------------------------------------------------------------------  
slip 21
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Student Registration Form</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f4f4f4;
            margin: 0;
            display: flex;
            align-items: center;
            justify-content: center;
            height: 100vh;
        }
        form {
            background-color: #fff;
            padding: 20px;
            border-radius: 8px;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }
        label {
            display: block;
            margin-bottom: 8px;
            font-weight: bold;
        }
        input {
            width: 100%;
            padding: 8px;
            margin-bottom: 12px;
            box-sizing: border-box;
        }
        input[type="submit"] {
            background-color: #4CAF50;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
        }
        input[type="reset"] {
            background-color: #f44336;
            color: white;
            padding: 10px 15px;
            border: none;
            border-radius: 4px;
            cursor: pointer;
            margin-left: 10px;
        }
        .required {
            color: red;
        }
        .message {
            margin-top: 10px;
            padding: 10px;
            background-color: #e7f3fe;
            border: 1px solid #4e7dcb;
            border-radius: 4px;
            display: none;
        }
        input:required {
            border: 2px solid red;
        }
    </style>
</head>
<body>
    <form id="registrationForm">
        <label for="firstName">First Name<span class="required">*</span>:</label>
        <input type="text" id="firstName" name="firstName" required>
        <label for="lastName">Last Name<span class="required">*</span>:</label>
        <input type="text" id="lastName" name="lastName" required>
        <label for="email">Email<span class="required">*</span>:</label>
        <input type="email" id="email" name="email" required>
        <label for="password">Password<span class="required">*</span>:</label>
        <input type="password" id="password" name="password" required>
        <input type="submit" value="Submit">
        <input type="reset" value="Reset">
        <div class="message" id="successMessage">Registration Successful!</div>
        <div class="message" id="errorMessage">Error submitting the form. Please try again.</div>
    </form>
    <script>
        const registrationForm = document.getElementById('registrationForm');
        const successMessage = document.getElementById('successMessage');
        const errorMessage = document.getElementById('errorMessage');
        registrationForm.addEventListener('submit', function (e) {
            e.preventDefault(); // Prevent the default form submission
            // You can add code here to handle the form submission, e.g., sending data to a server
            // For demonstration purposes, show a success message
            successMessage.style.display = 'block';
            // Clear the form after a delay (in a real scenario, this may be replaced with appropriate logic)
            setTimeout(() => {
                registrationForm.reset();
                successMessage.style.display = 'none';
            }, 3000);
        });
        registrationForm.addEventListener('reset', function () {
            // Reset the success message on form reset
            successMessage.style.display = 'none';
        });
    </script>
</body>
</html>


=>
Labels and Relationships
Labels:
Medicine → name, brand
Product → type (Tablet, Syrup, Powder)
State → name
Relationships:
(:Medicine)-[:HAS_PRODUCT]->(:Product)
(:Medicine)-[:USED_IN {percentage}]->(:State)
Graph Model:
(Medicine)-[:HAS_PRODUCT]->(Product)
(Medicine)-[:USED_IN {percentage}]->(State)---
Create Nodes and Relationships
// Medicines
CREATE (m1:Medicine {name:"Paracetamol", brand:"Cipla"}),
(m2:Medicine {name:"Amoxicillin", brand:"Dr. Reddy"}),
(m3:Medicine {name:"Vitamin C", brand:"SunPharma"})
// Products
CREATE (p1:Product {type:"Tablet"}),
(p2:Product {type:"Syrup"}),
(p3:Product {type:"Powder"})
// States
CREATE (s1:State {name:"Rajasthan"}),
(s2:State {name:"Gujarat"})
// Relationships
CREATE (m1)-[:HAS_PRODUCT]->(p1),
(m1)-[:USED_IN {percentage:95}]->(s1),
(m1)-[:USED_IN {percentage:80}]->(s2)
CREATE (m2)-[:HAS_PRODUCT]->(p2),
(m2)-[:USED_IN {percentage:92}]->(s1)
CREATE (m3)-[:HAS_PRODUCT]->(p3),(m3)-[:USED_IN {percentage:88}]->(s2)
---
Queries
a) List names of all medicines
MATCH (m:Medicine)
RETURN m.name
Output:
"Paracetamol"
"Amoxicillin"
"Vitamin C"
---
b) List medicines highly used in Rajasthan (>=90%)
MATCH (m:Medicine)-[u:USED_IN]->(s:State {name:"Rajasthan"})
WHERE u.percentage >= 90
RETURN m.name
Output:"Paracetamol"
"Amoxicillin"
---
c) List highly used tablets in Gujarat
MATCH (m:Medicine)-[:HAS_PRODUCT]->(p:Product {type:"Tablet"})-[:USED_IN]->(s:State
{name:"Gujarat"})
RETURN m.name
Output:
"Paracetamol"
---
d) List medicine names manufacturing "Powder"
MATCH (m:Medicine)-[:HAS_PRODUCT]->(p:Product {type:"Powder"})
RETURN m.name
Output:
"Vitamin C


---------------------------------------------------------------------------  
slip 23
---------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Image Display with Rotation</title>
    <style>
        body {
            margin: 0;
            display: flex;
            flex-direction: column;
            align-items: center;
            justify-content: center;
            height: 100vh;
            background-color: #f0f0f0;
        }
        #imageContainer {
            display: flex;
            flex-wrap: wrap;
            justify-content: center;
        }
        .imageTile {
            width: 150px;
            height: 150px;
            overflow: hidden;
            border: 1px solid #ddd;
            margin: 5px;
        }
        img {
            max-width: 100%;
            max-height: 100%;
            transform-origin: center center;
            transition: transform 0.3s ease;
        }
        button {
            margin-top: 20px;
            padding: 10px;
            font-size: 16px;
            cursor: pointer;
        }
    </style>
</head> 
<body> 
    <div id="imageContainer">
        <!-- Replace "https://via.placeholder.com/150" with the actual URL or path of your image -->
        <div class="imageTile">
            <img src="https://via.placeholder.com/150" alt="Image Tile 1" id="imageTile1">
        </div>
        <div class="imageTile">
            <img src="https://via.placeholder.com/150" alt="Image Tile 2" id="imageTile2">
        </div>
        <div class="imageTile">
            <img src="https://via.placeholder.com/150" alt="Image Tile 3" id="imageTile3">
        </div>
        <!-- Add more image tiles as needed -->
    </div>
    <button onclick="rotateClockwise()">Rotate Clockwise</button>
    <button onclick="rotateAntiClockwise()">Rotate Anti-clockwise</button>
    <script>
        let currentRotation = 0;
        function rotateClockwise() {
            currentRotation += 90;
            rotateImage("imageContainer", currentRotation);
        }
        function rotateAntiClockwise() {
            currentRotation -= 90;
            rotateImage("imageContainer", currentRotation);
        }
        function rotateImage(containerId, angle) {
            const container = document.getElementById(containerId);
            const imageTiles = container.querySelectorAll('.imageTile img');
            imageTiles.forEach(img => {
                img.style.transform = `rotate(${angle}deg)`;
            });
        }
    </script>
</body> 
</html>


=>
Labels and Relationships
Labels:
Car → model, brand
Section → name
Staff → name
Customer → name, city
Relationships:(:Section)-[:HAS_CAR]->(:Car)
(:Staff)-[:HANDLES]->(:Section)
(:Customer)-[:ENQUIRED]->(:Car)
(:Customer)-[:PURCHASED]->(:Car)
Graph Model:
(Staff)-[:HANDLES]->(Section)-[:HAS_CAR]->(Car)
(Customer)-[:ENQUIRED]->(Car)
(Customer)-[:PURCHASED]->(Car)
---
Create Nodes and Relationships
// Cars
CREATE (c1:Car {model:"Honda City"}),
(c2:Car {model:"Skoda"}),
(c3:Car {model:"Creta"}),
(c4:Car {model:"Swift"})
// Sections
CREATE (s1:Section {name:"City Section"}),(s2:Section {name:"Skoda Section"})
// Staff
CREATE (st1:Staff {name:"Mr. Narayan"}),
(st2:Staff {name:"Ms. Priya"})
// Customers
CREATE (cu1:Customer {name:"Ravi"}),
(cu2:Customer {name:"Sita"})
// Relationships
CREATE (s1)-[:HAS_CAR]->(c1),
(s2)-[:HAS_CAR]->(c2)
CREATE (st1)-[:HANDLES]->(s1),
(st1)-[:HANDLES]->(s2)
CREATE (cu1)-[:ENQUIRED]->(c1),
(cu1)-[:PURCHASED]->(c1),
(cu2)-[:ENQUIRED]->(c2)
---
Queries
a) List types of cars available
MATCH (c:Car)RETURN c.model
Output:
"Honda City"
"Skoda"
"Creta"
"Swift"
---
b) List sections handled by Mr. Narayan
MATCH (st:Staff {name:"Mr. Narayan"})-[:HANDLES]->(sec:Section)
RETURN sec.name
Output:
"City Section"
"Skoda Section"
---
c) List customers who only enquired but did not purchase
MATCH (cu:Customer)-[:ENQUIRED]->(c:Car)
WHERE NOT (cu)-[:PURCHASED]->(:Car)RETURN cu.name
Output:
"Sita"
---
d) List the highly sold car model
MATCH (c:Car)<-[:PURCHASED]-(cu:Customer)
RETURN c.model, COUNT(cu) AS sales
ORDER BY sales DESC
LIMIT 1
Output:
"Honda City" 1


---------------------------------------------------------------------------  
slip 25
---------------------------------------------------------------------------
<!DOCTYPE html>
<html>
<head>
    <title>Entry Form</title>
    <style>
        body {
            font-family: Arial, sans-serif;
            color: #b30000;
            font-size: 18px;
        }
        h1 {
            text-align: center;
            color: #b30000;
            font-size: 40px;
            margin-bottom: 20px;
        }
        .main-container {
            background-color: #b6dbe8;
            border: 2px solid #b30000;
            width: 80%;
        }
        .container {
            width: 60%;
            margin: auto;
        }
        label {
            display: inline-block;
            width: 200px;
            font-weight: bold;
            margin-bottom: 15px;
        }
        input[type="text"],
        input[type="number"],
        textarea,
        select,
        input[type="password"] {
            padding: 5px;
            width: 250px;
            font-size: 16px;
        }
        textarea {
            height: 80px;
        }
        .buttons {
            margin-top: 20px;
            text-align: center;
        }
        input[type="submit"],
        input[type="reset"] {
            padding: 8px 20px;
            margin: 10px;
            font-size: 16px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <div class="main-container">
        <h1>ENTRY FORM</h1>
        <div class="container">
            <form>
                <label>Enter your Name :</label>
                <input type="text"><br>
                <label>Enter your Age :</label>
                <input type="number"><br>
                <label>Enter your Address :</label>
                <textarea></textarea><br>
                <label>Sex :</label>
                <input type="radio" name="gender"> Female
                <input type="radio" name="gender"> Male<br><br>
                <label>Nationality :</label>
                <select>
                    <option>(Please select a country)</option>
                    <option>India</option>
                    <option>USA</option>
                    <option>UK</option>
                    <option>Other</option>
                </select><br><br>
                <label>Languages Known :</label>
                (can select more than one)<br>
                <label></label><input type="checkbox"> C<br>
                <label></label><input type="checkbox"> C++<br>
                <label></label><input type="checkbox"> VB<br>
                <label></label><input type="checkbox"> JAVA<br>
                <label></label><input type="checkbox"> ASP<br>
                <label></label><input type="checkbox"> OTHERS<br><br>
                <label>Enter your Password :</label>
                <input type="password"><br><br>
                <div class="buttons">
                    <input type="reset" value="Reset">
                    <input type="submit" value="Submit">
                </div>
            </form>
        </div>
    </div>
</body>
</html>

