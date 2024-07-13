### Project Report: Setting Up and Deploying a React.js Application on a Node.js Server

#### Prerequisites

1. **Create a CentOS Environment:**
   - Install CentOS on a virtual machine or physical server.

2. **Install NPM and Node.js:**
   - Ensure you have root or sudo access to perform installations.
   - Follow these steps to install Node.js and npm:

     ```bash
     # Update system packages
     sudo yum update -y

     # Add NodeSource repository for Node.js 16.x
     curl -fsSL https://rpm.nodesource.com/setup_16.x | sudo bash -

     # Install Node.js and npm
     sudo yum install -y nodejs
     ```

3. **Set Environment Variables:**
   - Define any necessary environment variables required by the project. This can be done in the `.bashrc` or `.bash_profile` file:

     ```bash
     # Open the .bashrc file
     nano ~/.bashrc

     # Add environment variables at the end of the file
     export NODE_ENV=production
     export REACT_APP_API_URL=http://example.com/api

     # Save and exit the file, then source it to apply changes
     source ~/.bashrc
     ```

#### Steps to Clone GitHub Repository and Build the Project

1. **Clone the GitHub Repository:**
   - Navigate to the directory where you want to clone the repository and use the `git clone` command:

     ```bash
     # Navigate to the desired directory
     cd /path/to/your/directory

     # Clone the repository
     git clone https://github.com/your-username/your-repository.git

     # Navigate to the project directory
     cd your-repository
     ```

2. **Install Project Dependencies:**
   - Use npm to install all required dependencies listed in the `package.json` file:

     ```bash
     # Install dependencies
     npm install
     ```

3. **Build the Project:**
   - Run the build command to create the production-ready build artifacts:

     ```bash
     # Build the project
     npm run build
     ```

   - The build artifacts will be created in the `build` folder within the project directory.

#### Conclusion

By following the steps outlined above, you will have successfully set up a CentOS environment with Node.js and npm, cloned the GitHub repository, installed the necessary dependencies, and built the project. This ensures that the application is ready to be deployed on a Node.js server.
