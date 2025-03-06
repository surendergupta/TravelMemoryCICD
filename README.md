# Travel Memory

## Backend Setup

### Add .env file in the backend folder
Create a `.env` file in the `backend/` directory and set the following environment variables:

```ini
MONGO_URI='ENTER_YOUR_URL'
PORT=3000
```

### Create `tripdetails` Collection
Insert the following JSON data into the `tripdetails` collection:

```json
{
    "tripName": "Incredible India",
    "startDateOfJourney": "19-03-2022",
    "endDateOfJourney": "27-03-2022",
    "nameOfHotels": "Hotel Namaste, Backpackers Club",
    "placesVisited": "Delhi, Kolkata, Chennai, Mumbai",
    "totalCost": 800000,
    "tripType": "leisure",
    "experience": "Lorem Ipsum...",
    "image": "https://t3.ftcdn.net/jpg/03/04/85/26/360_F_304852693_nSOn9KvUgafgvZ6wM0CNaULYUa7xXBkA.jpg",
    "shortDescription": "India is a wonderful country with rich culture and good people.",
    "featured": true
}
```

---

## AWS EC2 Instances Setup

### Create Two EC2 Instances (Frontend & Backend)
1. Click **Launch Instance** in the EC2 Dashboard.
2. Set the instance name (e.g., `frontend-tm-suri`).
3. Select **Ubuntu Server 22.04 LTS** under **Amazon Machine Image (AMI)**.
4. Choose an instance type (e.g., `t3.nano`).
5. Configure Key Pair (create or use an existing one for SSH access).
6. Modify network settings:
    - Allow **SSH traffic** from Anywhere (`0.0.0.0/0`).
    - Allow **HTTP & HTTPS traffic** from the internet.
7. Set **Number of Instances** to **2** and launch the instances.
8. Rename one instance to `backend-tm-suri`.

---

## Backend Instance Setup (`backend-tm-suri`)

### Connect to the Instance

```sh
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
NODE_MAJOR=18
echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
sudo apt-get update
sudo apt install nodejs -y
node -v  # should return v18.x.x
npm -v   # should return 10.x.x

git clone https://github.com/surendergupta/TravelMemory.git
cd TravelMemory/backend/
nano .env
```

Add the following inside `.env`:

```ini
MONGO_URI='mongodb+srv://surendergupta:ceOC9UhUh5trGjEE@taskmanagementcluster.tsyynim.mongodb.net/travelMemory'
PORT=3000
```

Save the file and install dependencies:

```sh
npm install
```

### Configure Security Group
1. Go to **EC2 Dashboard** → **Instances**.
2. Select `backend-tm-suri` and open **Security** tab.
3. Click on the **Security Group** link.
4. Edit **Inbound Rules**:
    - Add Rule: **Custom TCP**, Port: `3000`, Source: `0.0.0.0/0`.
5. Save the changes.

### Start Backend Server

```sh
node index.js &
```

Check if the server is running:

```sh
http://<backend-public-ip>:3000
```

If you see `Cannot GET /`, it means the backend is running successfully.

---

## Frontend Instance Setup (`frontend-tm-suri`)

### Connect to the Instance

```sh
sudo apt-get update
sudo apt-get install -y ca-certificates curl gnupg
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://deb.nodesource.com/gpgkey/nodesource-repo.gpg.key | sudo gpg --dearmor -o /etc/apt/keyrings/nodesource.gpg
NODE_MAJOR=18
echo "deb [signed-by=/etc/apt/keyrings/nodesource.gpg] https://deb.nodesource.com/node_$NODE_MAJOR.x nodistro main" | sudo tee /etc/apt/sources.list.d/nodesource.list
sudo apt-get update
sudo apt install nodejs -y
node -v  # should return v18.x.x
npm -v   # should return 10.x.x

git clone https://github.com/surendergupta/TravelMemory.git
cd TravelMemory/frontend/
npm install
```

### Update Backend URL

Edit `src/url.js` and update the backend URL:

```sh
nano src/url.js
```

Replace with:

```js
export const API_URL = "http://<backend-public-ip>:3000";
```

Save the file and start the frontend:

```sh
npm start
```

If successful, open:

```sh
http://<frontend-public-ip>:3000/
```

---

## MongoDB Atlas Setup
1. Go to [MongoDB Atlas](https://www.mongodb.com/atlas/database) and log in.
2. Create a **Cluster**.
3. Set up **Database Access** and **Network Access**.
4. Create a collection `tripdetails` and insert the JSON data above.
5. Click **Connect** → Select **Compass** → Copy Connection String:

```sh
mongodb+srv://<username>:<password>@taskmanagementcluster.tsyynim.mongodb.net/travelMemory
```

6. Add this connection string to `.env` in the backend.

---

## Install Nginx for Frontend & Backend

Run the following on both instances:

```sh
sudo apt-get update
sudo apt-get install nginx -y
sudo systemctl status nginx
```

Nginx setup will be required to serve the frontend and reverse proxy the backend.

---

**Setup Completed Successfully! 🎉**
