### Project Report: Hosting a React.js Application on GoDaddy using cPanel

#### Prerequisites

1. **Domain Registration:**
   - Register a domain on GoDaddy. Ensure you have access to the domain's cPanel.

2. **React.js Project Build:**
   - Ensure your project is built and the build artifacts are ready.

#### Steps to Host the Build on GoDaddy using cPanel

1. **Accessing cPanel:**
   - Log in to your GoDaddy account.
   - Navigate to your products and open cPanel for your hosting account.

2. **Upload Build Artifacts:**
   - In cPanel, go to the **File Manager**.
   - Navigate to the `public_html` directory (this is typically where your website files should go).
   - Upload the contents of the `build` directory from your React project to the `public_html` directory.

3. **Extract Files (if zipped):**
   - If you uploaded a zipped file, use the **Extract** function in the File Manager to extract the contents into the `public_html` directory.

4. **Set Environment Variables (if needed):**
   - In cPanel, navigate to the **Advanced** section and select **Cron Jobs**.
   - Add your environment variables at the top of your cron job command:

     ```bash
     export NODE_ENV=production
     export REACT_APP_API_URL=http://example.com/api
     ```

5. **Configure .htaccess for Single Page Application:**
   - Create or edit the `.htaccess` file in the `public_html` directory to handle routing for your React application:

     ```apache
     <IfModule mod_rewrite.c>
       RewriteEngine On
       RewriteBase /
       RewriteRule ^index\.html$ - [L]
       RewriteCond %{REQUEST_FILENAME} !-f
       RewriteCond %{REQUEST_FILENAME} !-d
       RewriteRule . /index.html [L]
     </IfModule>
     ```

6. **Verify Deployment:**
   - Once the files are uploaded and configurations are set, navigate to your domain (`http://yourdomain.tech`) to verify that your React application is being served correctly.

#### Conclusion

By following the steps outlined above, you will have successfully hosted your React.js application on GoDaddy using cPanel. The application will be accessible via your specified tech domain, providing a professional and accessible platform for your project.
