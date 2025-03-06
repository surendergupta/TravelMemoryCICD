# Travel Memory

Added .env file in backend folder
`.env` file to work with the backend:

Set this two variable in .env file. URL contain your mongodb url string
```
MONGO_URI='ENTER_YOUR_URL'
PORT=3000
```

Create the tripdetails collection and put below json data insert
Data format to be added: 

```json
{
    "tripName": "Incredible India",
    "startDateOfJourney": "19-03-2022",
    "endDateOfJourney": "27-03-2022",
    "nameOfHotels":"Hotel Namaste, Backpackers Club",
    "placesVisited":"Delhi, Kolkata, Chennai, Mumbai",
    "totalCost": 800000,
    "tripType": "leisure",
    "experience": "Lorem Ipsum, Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum,Lorem Ipsum, ",
    "image": "https://t3.ftcdn.net/jpg/03/04/85/26/360_F_304852693_nSOn9KvUgafgvZ6wM0CNaULYUa7xXBkA.jpg",
    "shortDescription":"India is a wonderful country with rich culture and good people.",
    "featured": true
}
```

### Create two instances for frontend and backend. Steps for creating two AWS EC2 Instances are:
    1.1 Click the Launch instance button on EC2 Dashboard from left sidebar and Launch instance area section.
    1.2 In Name and tags section put the name of instance like frontend-tm-suri and got to next section
    1.3 In Application and OS Images (Amazon Machine Image) section inside Quick Start select ubuntu OS and Amazon Machine Image (AMI) select Ubuntu Server 22.04 LTS and goto next section
    1.4 In Instance type section select any one type configuration as required for server and price based. Like we choose t3.nano and goto next section
    1.5 In Key pair (login) section create a new key pair or existing key pair as required. SSH login its required and goto next section
    1.6 In Network settings section check the Allow SSH traffic from Anywhere IP (0.0.0.0/0). You can also select custom IP and My IP. Check Allow HTTPS traffic from the internet Tick and check Allow HTTP traffic from the internet Tick
    1.7 In Summary Section enter Number of instances 2 but 1 is default and click on Launch Instance button.
### Created instance page successfully like (i-02bf2a29cef0b2be5, i-04a5488bfd757ada8) click anyone instance id to show instance list that created by you (filter by key-pair) and two instance of one change name frontend-tm-suri to backend-tm-suri and save it
### Click on backend instance ID like (i-04a5488bfd757ada8) and show next screen Instance summary for i-04a5488bfd757ada8 (backend-tm-suri) click connect 
### Next screen Connect to instance click connect 
### Next Open Terminal type some commands
    5.1 sudo apt-get update
    5.2 sudo apt-get install -y ca-certificates curl gnupg
    5.3 sudo mkdir -p /etc/apt/keyrings
    5.4 curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
    5.5 NODE_MAJOR=18
    5.6 echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
    5.7 sudo apt-get update
    5.8 sudo apt install nodejs -y
    5.9 node -v (v18.19.0)
    5.10 npm -v (10.2.3)
    5.11 git clone https://github.com/surendergupta/TravelMemory.git
    5.12 cd TravelMemory/backend/
    5.13 nano .env 
        (
            create and open .env file put this 
            MONGO_URI='mongodb+srv://surendergupta:ceOC9UhUh5trGjEE@taskmanagementcluster.tsyynim.mongodb.net/travelMemory'
            PORT=3000
            and save it
        )
    5.14 npm install
6. Goto Instance summary for i-04a5488bfd757ada8 (backend-tm-suri) and search Security tab and find the Security Group link and click it 
7. Open Security Group sg-035183f234ae009d6 - launch-wizard-64 and Inbound Rules tab section click Edit inbound rules button
8. Next Edit inbound rules Section Click on Add Rule Type: Custom TCP, Port: 3000, Source: 0.0.0.0/0 and save the rule. Go back to terminal
9. To start nodejs backend server continues type: node index.js &
10. Message show Server started at http://localhost:3000 change localhost to public ip address of instance http://44.211.55.91:3000
11. If open url http://44.211.55.91:3000 and show Cannot GET / its means successfully running backend.
12. Back to Instance list created by you and click on frontend-tm-suri instance id (i-02bf2a29cef0b2be5) and show next screen Instance summary for i-04a5488bfd757ada8 (backend-tm-suri) click connect 
13. Next screen Connect to instance click connect and Next Open Terminal type some commands
    13.1 sudo apt-get update
    13.2 sudo apt-get install -y ca-certificates curl gnupg
    13.3 sudo mkdir -p /etc/apt/keyrings
    13.4 curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
    13.5 NODE_MAJOR=18
    13.6 echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
    13.7 sudo apt-get update
    13.8 sudo apt install nodejs -y
    13.9 node -v (v18.19.0)
    13.10 npm -v (10.2.3)
    13.11 git clone https://github.com/surendergupta/TravelMemory.git
    13.12 cd TravelMemory/frontend/
    13.13 npm install
    13.14 nano src/url.js and update backend url for connectivity and save the file
    13.15 npm start
    13.16 show message like
        You can now view frontend in the browser.

        Local:            http://localhost:3000
        On Your Network:  http://10.2.9.204:3000

        Note that the development build is not optimized.
        To create a production build, use npm run build.

        webpack compiled successfully

    13.17 Now Open http://35.170.33.8:3000/ if open open successfully complete otherwise check error or backend url file in src directory update it its works.

14. For database of Mongoose goto https://www.mongodb.com/atlas/database. If already have account login otherwise signup.
15. After Login create cluster and setup Database Access, Setup Network Access for security purpose. Also create collection with name tripdetails and put json data above we write.
16. click on connect from Database Deployment section, Now Open Popup select compass and copy connection string like ; mongodb+srv://<username>:<password>@taskmanagementcluster.tsyynim.mongodb.net/
17. In connection string add database name after slash at the end is done database setup complete.

Installation nginx Server on frontend and backend both
1. sudo apt-get update
2. sudo apt-get install nginx -y
3. sudo systemctl status nginx
