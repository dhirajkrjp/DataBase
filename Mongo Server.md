**MongoDB Community Server**: what it is, which version to install, how to install it on your computer, how to start/stop the server, how to connect with `mongosh` and Compass, and how to create and use your first database.

 I'm assuming **Windows** below. If you're on macOS or Ubuntu/Linux, tell me and I'll give you the exact installation steps for that OS.

 ## 1\. What is MongoDB Server?

 MongoDB has a few different pieces, and it's easy to confuse them.

```
MongoDB Community Server
        │
        ├── mongod
        │     └── Actual MongoDB database server
        │
        └── Database files
```

 Then you have tools that connect to that server:

```
                    ┌── mongosh
                    │
MongoDB Server ◄────┤
                    │
                    └── MongoDB Compass
```

 And eventually your backend connects to the same server:

```
Node.js + Express
       │
       │ MongoDB Driver
       ▼
MongoDB Server
       │
       ▼
Database
       │
       ▼
Collections
       │
       ▼
Documents
```

 So **MongoDB Server is the actual database engine**.

---

 # 2\. Which MongoDB version should you install?

 For learning and local development, install the current **MongoDB Community Server** release rather than an old tutorial-specific version.

 Use the official MongoDB download page:

 MongoDB Community Server download

 On the download page you'll typically select:

```
Version: Current stable release
Platform: Windows
Package: MSI
```

 For example, if the current stable release shown by MongoDB is `8.x`, install that rather than deliberately installing MongoDB 6.x or 7.x just because an old tutorial uses it.

 The exact version number can change over time.

---

 # 3\. MongoDB Server vs MongoDB Compass

 Install both, but understand that they are different.

 ### MongoDB Community Server

 This is the database:

```
MongoDB Server
```

 It runs in the background.

 ### MongoDB Compass

 This is a GUI:

```
MongoDB Compass
```

 It lets you visually inspect and manage your databases.

 You can have:

```
MongoDB Server
       ▲
       │
       ├── mongosh
       │
       ├── Compass
       │
       └── Node.js backend
```

---

 # 4\. Download MongoDB Server

 Go to:

 MongoDB Community Server downloads

 Choose:

```
MongoDB Community Server
```

 Then:

```
Version: current stable
Platform: Windows
Package: MSI
```

 Download the `.msi`.

 It will look roughly like:

```
mongodb-windows-x86_64-8.x.x-signed.msi
```

 The exact filename/version will differ.

---

 # 5\. Start the installer

 Double-click the `.msi` file.

 You'll get the MongoDB setup wizard.

 Click:

```
Next
```

 Accept the license agreement.

 Then:

```
Next
```

---

 # 6\. Choose Complete installation

 You'll normally see installation options similar to:

```
Complete
Custom
```

 Choose:

```
Complete
```

 For a beginner/local development machine, this is the simplest option.

 Then click:

```
Next
```

---

 # 7\. MongoDB Service configuration

 This is an important screen.

 MongoDB can run as a **Windows Service**.

 You should generally enable:

```
Install MongoD as a Service
```

 You may see options similar to:

```
Service Configuration

(●) MongoD Service

Service Name:
MongoDB

(●) Run service as Network Service user
```

 For a normal local development installation, the defaults are generally fine.

 This means Windows can automatically run MongoDB in the background.

---

 # 8\. MongoDB Compass installation

 Depending on the installer/version, you may see an option related to MongoDB Compass.

 If offered:

```
Install MongoDB Compass
```

 you can enable it.

 If it isn't offered, download Compass separately:

 MongoDB Compass official download

 Then click:

```
Install
```

 Wait for the installation to complete.

---

 # 9\. Where does MongoDB get installed?

 The exact directory can vary by version and installation choice, but on Windows you will commonly encounter paths under:

```
C:\Program Files\MongoDB\
```

 For example:

```
C:\Program Files\MongoDB\Server\8.x\
```

 Inside you'll find directories such as:

```
bin
```

 The `bin` directory contains MongoDB executables.

 Conceptually:

```
MongoDB
└── Server
    └── 8.x
        └── bin
            ├── mongod.exe
            └── mongos.exe
```

---

 # 10\. What is `mongod`?

 This is one of the most important things to understand.

```
mongod
```

 is the MongoDB server process.

 Think of:

```
mongod = MongoDB database server
```

 When `mongod` is running, MongoDB is available to accept connections.

---

 # 11\. What is `mongosh`?

 This is different.

```
mongosh
```

 is the MongoDB Shell.

 Think:

```
mongod = server
mongosh = command-line client
```

 The relationship is:

```
             connection
mongosh ─────────────────► mongod
                              │
                              ▼
                           MongoDB
```

 Recent MongoDB installations may not bundle `mongosh` with the server installer, so if:

```
mongosh
```

 doesn't work after installing the server, install MongoDB Shell separately from MongoDB's official tools/download resources.

---

 # 12\. Check whether MongoDB Server is running

 Because you installed MongoDB as a Windows Service, it may already be running.

 Press:

```
Windows + R
```

 Type:

```
services.msc
```

 Press Enter.

 You'll see the Windows Services application.

 Look for something like:

```
MongoDB
```

 or:

```
MongoDB Server
```

 The status should ideally be:

```
Running
```

---

 # 13\. Start MongoDB manually through Services

 If MongoDB isn't running:

 Right-click the MongoDB service.

 Choose:

```
Start
```

 You should then see:

```
Status: Running
```

 Now your MongoDB server is running locally.

---

 # 14\. Stop MongoDB

 If you ever need to stop it:

```
Services
   ↓
MongoDB
   ↓
Right click
   ↓
Stop
```

 You normally don't need to stop MongoDB every time you finish programming.

 If it's installed as a service, Windows can manage it for you.

---

 # 15\. Connect using MongoDB Shell

 Open PowerShell or Command Prompt.

 Run:

```
mongosh
```

 If everything is working, you should see a connection similar to:

```
Connecting to: mongodb://127.0.0.1:27017/
```

 The important part is:

```
mongodb://127.0.0.1:27017/
```

 or:

```
mongodb://localhost:27017/
```

---

 # 16\. What is port 27017?

 MongoDB's standard port is:

```
27017
```

 So:

```
localhost:27017
```

 means:

```
Your computer
     │
     └── MongoDB
           │
           └── Port 27017
```

 Your MongoDB connection string is commonly:

```
mongodb://localhost:27017
```

---

 # 17\. Verify the server

 Inside `mongosh`, run:

```
db
```

 You may see:

```
test
```

 Then:

```
show dbs
```

 You might see:

```
admin
config
local
```

 Don't worry if you don't see your application database yet.

 MongoDB creates a database when you actually store data in it.

---

 # 18\. Create your first database

 Run:

```
use my_app
```

 You'll see:

```
switched to db my_app
```

 But remember:

```
use my_app
```

 doesn't necessarily create a persistent database immediately.

 You need to insert data.

---

 # 19\. Create your first collection

 You can explicitly create one:

```
db.createCollection("users")
```

 You'll get:

```
{ ok: 1 }
```

 Check:

```
show collections
```

 Result:

```
users
```

 Your structure is now:

```
MongoDB Server
    │
    └── my_app
          │
          └── users
```

---

 # 20\. Insert your first document

 Run:

```
db.users.insertOne({
    name: "John",
    email: "john@example.com",
    age: 25
})
```

 MongoDB returns something similar to:

```
{
  acknowledged: true,
  insertedId: ObjectId('...')
}
```

 Your database now contains data.

 Therefore:

```
show dbs
```

 should now include:

```
my_app
```

---

 # 21\. View your document

 Run:

```
db.users.find()
```

 You'll see something like:

```
[
  {
    _id: ObjectId('68...'),
    name: 'John',
    email: 'john@example.com',
    age: 25
  }
]
```

 Congratulations — you've created and used your first MongoDB database.

---

 # 22\. Understanding the structure

 You currently have:

```
MongoDB Server
│
└── my_app                ← Database
     │
     └── users            ← Collection
          │
          └── Document    ← User
```

 The document:

```
{
  "_id": "...",
  "name": "John",
  "email": "john@example.com",
  "age": 25
}
```

---

 # 23\. Add more users

```
db.users.insertMany([
    {
        name: "Alice",
        email: "alice@example.com",
        age: 22
    },
    {
        name: "Bob",
        email: "bob@example.com",
        age: 30
    }
])
```

 Now:

```
db.users.find()
```

 will show all three users.

---

 # 24\. Search for a user

```
db.users.findOne({
    name: "Alice"
})
```

 Or:

```
db.users.find({
    age: 30
})
```

---

 # 25\. Update a user

```
db.users.updateOne(
    {
        name: "Alice"
    },
    {
        $set: {
            age: 23
        }
    }
)
```

 Check:

```
db.users.findOne({
    name: "Alice"
})
```

---

 # 26\. Delete a user

```
db.users.deleteOne({
    name: "Bob"
})
```

 Then:

```
db.users.find()
```

---

 # 27\. Now use MongoDB Compass

 Open:

```
MongoDB Compass
```

 You'll see a connection field.

 Enter:

```
mongodb://localhost:27017
```

 Then click:

```
Connect
```

 You should see:

```
Databases
│
├── admin
├── config
├── local
└── my_app
```

 Click:

```
my_app
```

 Then:

```
users
```

 You should see your documents visually.

---

 # 28\. Why use Compass if `mongosh` works?

 Both connect to the same MongoDB server.

 ### `mongosh`

 Good for learning commands:

```
db.users.find()
```

 ### Compass

 Good for visually examining:

```
Databases
Collections
Documents
Indexes
Queries
Aggregations
```

 So I recommend learning both.

---

 # 29\. The most important concept

 Compass is **not your database**.

 `mongosh` is **not your database**.

 Your database is managed by the MongoDB server.

 Think:

```
                  MongoDB Server
                        │
             ┌──────────┼──────────┐
             │          │          │
             ▼          ▼          ▼
          mongosh    Compass    Backend
```

 All three can connect to the same server.

---

 # 30\. Connect your Node.js backend

 Now we get to the important part.

 Your backend will connect to:

```
mongodb://localhost:27017
```

 Install Node.js from:

 Node.js official website

 Check:

```
node --version
npm --version
```

---

 # 31\. Create backend

```
mkdir mongo-backend
cd mongo-backend
npm init -y
```

 Install:

```
npm install express mongodb dotenv
```

 Create:

```
mongo-backend/
│
├── node_modules/
├── package.json
├── package-lock.json
├── .env
├── .gitignore
└── server.js
```

---

 # 32\. Create `.env`

```
PORT=5000
MONGODB_URI=mongodb://localhost:27017
DATABASE_NAME=my_app
```

 And `.gitignore`:

```
node_modules/
.env
```

---

 # 33\. Connect backend to MongoDB

 `server.js`:

```
const express = require("express");
const { MongoClient } = require("mongodb");
require("dotenv").config();

const app = express();

app.use(express.json());

const client = new MongoClient(process.env.MONGODB_URI);

const db = client.db(process.env.DATABASE_NAME);

async function startServer() {
    try {
        await client.connect();

        console.log("MongoDB connected successfully");

        app.listen(process.env.PORT, () => {
            console.log(
                `Server running on http://localhost:${process.env.PORT}`
            );
        });
    } catch (error) {
        console.error("MongoDB connection failed:", error);
        process.exit(1);
    }
}

startServer();
```

 Run:

```
node server.js
```

 You should see:

```
MongoDB connected successfully
Server running on http://localhost:5000
```

 Now you have:

```
                 Your Computer
┌─────────────────────────────────────────┐
│                                         │
│  Node.js Backend                        │
│       │                                 │
│       │ mongodb://localhost:27017       │
│       ▼                                 │
│  MongoDB Server                         │
│       │                                 │
│       ▼                                 │
│  my_app                                 │
│       │                                 │
│       ▼                                 │
│  users                                  │
│                                         │
└─────────────────────────────────────────┘
```

---

 # 34\. Create API to read users

 Add:

```
app.get("/users", async (req, res) => {
    try {
        const users = await db
            .collection("users")
            .find()
            .toArray();

        res.json(users);
    } catch (error) {
        console.error(error);

        res.status(500).json({
            error: "Failed to fetch users"
        });
    }
});
```

 Now open:

```
http://localhost:5000/users
```

 The backend retrieves:

```
Express
   ↓
MongoDB Driver
   ↓
my_app
   ↓
users
   ↓
documents
```

 and returns them as JSON.

---

 # 35\. Create users through the backend

 Add:

```
app.post("/users", async (req, res) => {
    try {
        const { name, email, age } = req.body;

        const result = await db.collection("users").insertOne({
            name,
            email,
            age
        });

        res.status(201).json({
            message: "User created",
            id: result.insertedId
        });
    } catch (error) {
        console.error(error);

        res.status(500).json({
            error: "Failed to create user"
        });
    }
});
```

 Now the architecture is:

```
Frontend/Postman
       │
       │ POST /users
       ▼
Express
       │
       ▼
MongoDB Driver
       │
       ▼
MongoDB Server
       │
       ▼
my_app.users
```

---

 # 36\. Don't expose MongoDB directly to the frontend

 This is important.

 Don't build:

```
React
  │
  └──────────► MongoDB
```

 Instead:

```
React
  │
  │ HTTP
  ▼
Node.js / Express
  │
  │ MongoDB Driver
  ▼
MongoDB
```

 Your database should be accessed by your backend.

---

 # 37\. What happens when you restart your computer?

 If MongoDB is installed as a Windows Service and configured to start automatically, Windows can start MongoDB for you.

 You can verify:

```
Windows
   ↓
services.msc
   ↓
MongoDB
   ↓
Running
```

 Then your backend can connect to:

```
mongodb://localhost:27017
```

---

 # 38\. What if `mongosh` says command not found?

 This usually means either:

 - MongoDB Shell isn't installed, or
- its installation directory isn't in your PATH.

 First check whether `mongosh` is installed.

 MongoDB provides MongoDB Shell separately from the server in current distribution practices. Use MongoDB's official download page:

 MongoDB Shell download

 Install it and reopen PowerShell/Command Prompt.

 Then:

```
mongosh
```

---

 # 39\. What if MongoDB isn't running?

 Try:

```
Windows + R
```

 Then:

```
services.msc
```

 Find:

```
MongoDB
```

 If stopped:

```
Right click → Start
```

 Then retry:

```
mongosh
```

---

 # 40\. What if port 27017 is already being used?

 MongoDB normally uses:

```
27017
```

 If another application is already using that port, MongoDB may fail to start.

 The error will usually mention something like:

```
Address already in use
```

 For a beginner, don't change the MongoDB port unless you actually have a conflict.

---

 # 41\. How to know whether MongoDB is working

 There are four useful checks.

 ### Check 1 — Windows Service

```
services.msc
```

 MongoDB:

```
Running
```

 ### Check 2 — Shell

```
mongosh
```

 ### Check 3 — Compass

 Connect:

```
mongodb://localhost:27017
```

 ### Check 4 — Backend

 Run:

```
node server.js
```

 and see:

```
MongoDB connected successfully
```

 If all four work, your local setup is healthy.

---

 # 42\. Your MongoDB command cheat sheet

 ### Start using database

```
use my_app
```

 ### Show databases

```
show dbs
```

 ### Show collections

```
show collections
```

 ### Create collection

```
db.createCollection("users")
```

 ### Insert one

```
db.users.insertOne({
    name: "John",
    email: "john@example.com"
})
```

 ### Insert many

```
db.users.insertMany([
    {
        name: "John"
    },
    {
        name: "Alice"
    }
])
```

 ### Find everything

```
db.users.find()
```

 ### Find one

```
db.users.findOne({
    name: "John"
})
```

 ### Update

```
db.users.updateOne(
    { name: "John" },
    { $set: { age: 30 } }
)
```

 ### Delete

```
db.users.deleteOne({
    name: "John"
})
```

---

 # 43\. Your complete local setup

 Once everything is installed, this is what you have:

```
Windows
│
├── MongoDB Community Server
│      │
│      └── mongod
│             │
│             └── localhost:27017
│
├── MongoDB Shell
│      │
│      └── mongosh
│
├── MongoDB Compass
│      │
│      └── GUI
│
└── Node.js
       │
       └── Express Backend
              │
              └── MongoDB Driver
                     │
                     ▼
               MongoDB Server
```

 And your database:

```
MongoDB Server
│
└── my_app
    │
    └── users
        │
        ├── John
        ├── Alice
        └── David
```

---

 # 44\. What you should learn next

 Once you can successfully do:

```
Install MongoDB
      ↓
Start MongoDB
      ↓
mongosh
      ↓
use my_app
      ↓
create users
      ↓
insert documents
      ↓
find documents
      ↓
update documents
      ↓
delete documents
      ↓
Compass
      ↓
Node.js
      ↓
Express
      ↓
MongoDB Driver
      ↓
REST API
```

 then move to:

```
1. MongoDB queries
2. ObjectId
3. Embedded documents
4. Arrays
5. References
6. Indexes
7. Aggregation
8. Mongoose
9. Validation
10. Authentication
11. Authorization
12. Transactions
13. MongoDB Atlas
14. Production deployment
```

 ### One important distinction

 For your local machine, you **do not need MongoDB Atlas** to learn MongoDB.

 You can completely learn and develop locally with:

```
MongoDB Community Server
+
mongosh
+
MongoDB Compass
+
Node.js
+
Express
```

 Then later move the same application from:

```
mongodb://localhost:27017
```

 to a hosted MongoDB Atlas connection when you're ready for deployment.
