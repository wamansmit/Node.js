Deploying a React.js project on a Node.js server on CentOS involves several steps. Here's a step-by-step guide:

### Step 1: Prepare the Server
1. **Update the System**:
   ```bash
   sudo yum update -y
   ```

2. **Install Node.js**:
   ```bash
   curl -sL https://rpm.nodesource.com/setup_16.x | sudo bash -
   sudo yum install -y nodejs
   ```

3. **Install Git** (if not already installed):
   ```bash
   sudo yum install git -y
   ```

### Step 2: Clone Your React.js Project
1. **Navigate to the desired directory**:
   ```bash
   cd /path/to/your/directory
   ```

2. **Clone your project repository**:
   ```bash
   git clone https://github.com/yourusername/your-repository.git
   cd your-repository
   ```

### Step 3: Build the React Application
1. **Install project dependencies**:
   ```bash
   npm install
   ```

2. **Build the project**:
   ```bash
   npm run build
   ```
   This will create a `build` directory with the production-ready files.

### Step 4: Serve the React Application with Node.js
1. **Create a simple Node.js server**:
   
   Create a file named `server.js` in the root of your project directory with the following content:
   ```javascript
   const express = require('express');
   const path = require('path');
   
   const app = express();
   const port = process.env.PORT || 3000;
   
   app.use(express.static(path.join(__dirname, 'build')));
   
   app.get('*', (req, res) => {
       res.sendFile(path.join(__dirname, 'build', 'index.html'));
   });
   
   app.listen(port, () => {
       console.log(`Server is running on port ${port}`);
   });
   ```

2. **Install Express**:
   ```bash
   npm install express
   ```

### Step 5: Start the Node.js Server
1. **Start the server**:
   ```bash
   node server.js
   ```
   
   To keep the server running in the background, you can use a process manager like `pm2`.

### Step 6: Install and Configure `pm2`
1. **Install `pm2`** globally:
   ```bash
   sudo npm install pm2@latest -g
   ```

2. **Start your application with `pm2`**:
   ```bash
   pm2 start server.js
   ```

3. **Set `pm2` to start on boot**:
   ```bash
   pm2 startup systemd
   ```
   Follow the on-screen instructions to run the command it generates.

4. **Save the current process list**:
   ```bash
   pm2 save
   ```

### Step 7: Configure Firewall (Optional)
1. **Allow traffic on the required port (e.g., 3000)**:
   ```bash
   sudo firewall-cmd --zone=public --add-port=3000/tcp --permanent
   sudo firewall-cmd --reload
   ```

### Step 8: Configure a Reverse Proxy (Optional)
For a more robust setup, you might want to use Nginx as a reverse proxy in front of your Node.js server.

1. **Install Nginx**:
   ```bash
   sudo yum install nginx -y
   ```

2. **Configure Nginx**:
   Open the Nginx configuration file:
   ```bash
   sudo vi /etc/nginx/nginx.conf
   ```

   Add the following configuration inside the `http` block:
   ```nginx
   server {
       listen 80;
       server_name your_domain_or_IP;

       location / {
           proxy_pass http://localhost:3000;
           proxy_http_version 1.1;
           proxy_set_header Upgrade $http_upgrade;
           proxy_set_header Connection 'upgrade';
           proxy_set_header Host $host;
           proxy_cache_bypass $http_upgrade;
       }
   }
   ```

3. **Start and enable Nginx**:
   ```bash
   sudo systemctl start nginx
   sudo systemctl enable nginx
   ```

### Step 9: Access Your Application
Open a web browser and navigate to `http://your_domain_or_IP` to see your deployed React.js application.

By following these steps, you should have a fully deployed React.js application served by a Node.js server on CentOS.
