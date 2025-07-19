Photo Sharing Website

Overview
The Photo Sharing Website is a cloud-based project built on AWS using services like S3, EC2, and DynamoDB. It allows users to upload photos via a static frontend hosted on S3. The uploaded photos are stored in an S3 bucket, while metadata (like filename and upload timestamp) is saved in DynamoDB.

This project demonstrates the power of AWS cloud computing and is suitable for beginners and intermediate learners exploring AWS and cloud-based web applications.


Features
Frontend: Static website hosted on S3 with HTML, CSS, and JavaScript.
Backend: Flask app hosted on an EC2 instance to handle image uploads and metadata storage.
Storage: S3 bucket for storing uploaded photos.
Database: DynamoDB for storing photo metadata (e.g., filenames, timestamps).

Architecture
Frontend:
Hosted on S3 as a static website.
Includes an upload form for photos.

Backend:
Flask app deployed on an EC2 instance.
Handles /upload endpoint for photo uploads.

Storage:
S3 bucket to store photos.

Database:
DynamoDB table to store photo metadata.


Project Workflow : 
Users upload photos via the frontend.
The backend:
Uploads the photo to the S3 bucket.
Saves metadata (filename, upload timestamp) to DynamoDB.
The frontend displays the uploaded photos.

Getting Started
1. AWS Setup
   
2. Create an S3 Bucket
Go to the AWS S3 Console.
Create a bucket:
Bucket Name: A globally unique name (e.g., my-photo-sharing-app)
Uncheck Block all public access for public hosting

3. Enable Static Website Hosting:
Set the index document to index.html.
Copy the Static Website Endpoint for later use.

   Add a Bucket Policy for public access:
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-photo-sharing-app/*"
    }
  ]
}

5. Create a DynamoDB Table
Go to the AWS DynamoDB Console.
Create a table:
Table Name: PhotoMetadata.
Partition Key: filename (String).
Save and verify the table is active.

6.Launch an EC2 Instance
Go to the AWS EC2 Console and launch an instance:
AMI: Amazon Linux 2.
Instance Type: t2.micro.
Key Pair: Create or select an existing key pair.
Security Group:
Allow port 22 (SSH).
Allow port 5000 (HTTP) for backend communication.

7.Attach an IAM role with:
AmazonS3FullAccess.
AmazonDynamoDBFullAccess.

8. CONNECT VIA SSH
9. Install Python and required packages:
  sudo yum update -y
  sudo yum install python3 -y
  pip3 install flask flask-cors boto3

10.Deploy the Backend in the ec2 machine 
Create a directory for the backend:
mkdir ~/photo-sharing-backend
cd ~/photo-sharing-backend

11. Create the app.py file:
    vi or nano  app.py
    Paste the Flask code you can see this code in app.py in repo

12. Run the Flask app:
    command to run : python3 app.py

13.Test the backend:
   curl -X POST -F "file=@example.jpg" http://<EC2-Public-IP>:5000/upload ## download any imgae from web and copy here also you can change your port number 

14.Deploy the Frontend

Prepare frontend files:
index.html: Main webpage.
style.css: Styling.
script.js: JavaScript for interacting with the backend.
Replace <EC2-Public-IP> in script.js with your EC2 instance's public IP.

Upload files to your S3 bucket:
Go to S3 Console > Objects.
Drag and drop the frontend files.
Make the files public.   

15.Test the Application:
Access the S3 Static Website Endpoint in your browser.
Upload a photo.
Verify:
The photo appears in the S3 bucket.
Metadata is stored in DynamoDB.
Success message is displayed on the webpage.

16. 
Here's a detailed README.md content template for your Photo Sharing Website project using S3, EC2, and DynamoDB. This guide will help others understand, replicate, and learn from your project.

Photo Sharing Website
Overview
The Photo Sharing Website is a cloud-based project built on AWS using services like S3, EC2, and DynamoDB. It allows users to upload photos via a static frontend hosted on S3. The uploaded photos are stored in an S3 bucket, while metadata (like filename and upload timestamp) is saved in DynamoDB.

This project demonstrates the power of AWS cloud computing and is suitable for beginners and intermediate learners exploring AWS and cloud-based web applications.

Features
Frontend: Static website hosted on S3 with HTML, CSS, and JavaScript.
Backend: Flask app hosted on an EC2 instance to handle image uploads and metadata storage.
Storage: S3 bucket for storing uploaded photos.
Database: DynamoDB for storing photo metadata (e.g., filenames, timestamps).
Architecture
Frontend:

Hosted on S3 as a static website.
Includes an upload form for photos.
Backend:

Flask app deployed on an EC2 instance.
Handles /upload endpoint for photo uploads.
Storage:

S3 bucket to store photos.
Database:

DynamoDB table to store photo metadata.
Project Workflow
Users upload photos via the frontend.
The backend:
Uploads the photo to the S3 bucket.
Saves metadata (filename, upload timestamp) to DynamoDB.
The frontend displays the uploaded photos.
Getting Started
1. AWS Setup
1.1 Create an S3 Bucket
Go to the AWS S3 Console.

Create a bucket:

Bucket Name: A globally unique name (e.g., my-photo-sharing-app).
Uncheck Block all public access for public hosting.
Enable Static Website Hosting:

Set the index document to index.html.
Copy the Static Website Endpoint for later use.
Add a Bucket Policy for public access:

json
Copy code
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-photo-sharing-app/*"
    }
  ]
}
1.2 Create a DynamoDB Table
Go to the AWS DynamoDB Console.
Create a table:
Table Name: PhotoMetadata.
Partition Key: filename (String).
Save and verify the table is active.
1.3 Launch an EC2 Instance
Go to the AWS EC2 Console and launch an instance:

AMI: Amazon Linux 2.
Instance Type: t2.micro.
Key Pair: Create or select an existing key pair.
Security Group:
Allow port 22 (SSH).
Allow port 5000 (HTTP) for backend communication.
Attach an IAM role with:

AmazonS3FullAccess.
AmazonDynamoDBFullAccess.
SSH into the instance:

bash
Copy code
ssh -i your-key.pem ec2-user@<EC2-Public-IP>
Install Python and required packages:

bash
Copy code
sudo yum update -y
sudo yum install python3 -y
pip3 install flask flask-cors boto3
2. Deploy the Backend
Create a directory for the backend:

bash
Copy code
mkdir ~/photo-sharing-backend
cd ~/photo-sharing-backend
Create the app.py file:

bash
Copy code
nano app.py
Paste the Flask code provided earlier.

Run the Flask app:

bash
Copy code
python3 app.py
Test the backend:

bash
Copy code
curl -X POST -F "file=@example.jpg" http://<EC2-Public-IP>:5000/upload
3. Deploy the Frontend
Prepare frontend files:

index.html: Main webpage.
style.css: Styling.
script.js: JavaScript for interacting with the backend.
Replace <EC2-Public-IP> in script.js with your EC2 instance's public IP.

Upload files to your S3 bucket:

Go to S3 Console > Objects.
Drag and drop the frontend files.
Make the files public.

Test the Application
Access the S3 Static Website Endpoint in your browser.
Upload a photo.
Verify:
The photo appears in the S3 bucket.
Metadata is stored in DynamoDB.
Success message is displayed on the webpage.


Here's a detailed README.md content template for your Photo Sharing Website project using S3, EC2, and DynamoDB. This guide will help others understand, replicate, and learn from your project.

Photo Sharing Website
Overview
The Photo Sharing Website is a cloud-based project built on AWS using services like S3, EC2, and DynamoDB. It allows users to upload photos via a static frontend hosted on S3. The uploaded photos are stored in an S3 bucket, while metadata (like filename and upload timestamp) is saved in DynamoDB.

This project demonstrates the power of AWS cloud computing and is suitable for beginners and intermediate learners exploring AWS and cloud-based web applications.

Features
Frontend: Static website hosted on S3 with HTML, CSS, and JavaScript.
Backend: Flask app hosted on an EC2 instance to handle image uploads and metadata storage.
Storage: S3 bucket for storing uploaded photos.
Database: DynamoDB for storing photo metadata (e.g., filenames, timestamps).
Architecture
Frontend:

Hosted on S3 as a static website.
Includes an upload form for photos.
Backend:

Flask app deployed on an EC2 instance.
Handles /upload endpoint for photo uploads.
Storage:

S3 bucket to store photos.
Database:

DynamoDB table to store photo metadata.
Project Workflow
Users upload photos via the frontend.
The backend:
Uploads the photo to the S3 bucket.
Saves metadata (filename, upload timestamp) to DynamoDB.
The frontend displays the uploaded photos.
Getting Started
1. AWS Setup
1.1 Create an S3 Bucket
Go to the AWS S3 Console.

Create a bucket:

Bucket Name: A globally unique name (e.g., my-photo-sharing-app).
Uncheck Block all public access for public hosting.
Enable Static Website Hosting:

Set the index document to index.html.
Copy the Static Website Endpoint for later use.
Add a Bucket Policy for public access:

json
Copy code
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Allow",
      "Principal": "*",
      "Action": "s3:GetObject",
      "Resource": "arn:aws:s3:::my-photo-sharing-app/*"
    }
  ]
}
1.2 Create a DynamoDB Table
Go to the AWS DynamoDB Console.
Create a table:
Table Name: PhotoMetadata.
Partition Key: filename (String).
Save and verify the table is active.
1.3 Launch an EC2 Instance
Go to the AWS EC2 Console and launch an instance:

AMI: Amazon Linux 2.
Instance Type: t2.micro.
Key Pair: Create or select an existing key pair.
Security Group:
Allow port 22 (SSH).
Allow port 5000 (HTTP) for backend communication.
Attach an IAM role with:

AmazonS3FullAccess.
AmazonDynamoDBFullAccess.
SSH into the instance:

bash
Copy code
ssh -i your-key.pem ec2-user@<EC2-Public-IP>
Install Python and required packages:

bash
Copy code
sudo yum update -y
sudo yum install python3 -y
pip3 install flask flask-cors boto3
2. Deploy the Backend
Create a directory for the backend:

bash
Copy code
mkdir ~/photo-sharing-backend
cd ~/photo-sharing-backend
Create the app.py file:

bash
Copy code
nano app.py
Paste the Flask code provided earlier.

Run the Flask app:

bash
Copy code
python3 app.py
Test the backend:

bash
Copy code
curl -X POST -F "file=@example.jpg" http://<EC2-Public-IP>:5000/upload
3. Deploy the Frontend
Prepare frontend files:

index.html: Main webpage.
style.css: Styling.
script.js: JavaScript for interacting with the backend.
Replace <EC2-Public-IP> in script.js with your EC2 instance's public IP.

Upload files to your S3 bucket:

Go to S3 Console > Objects.
Drag and drop the frontend files.
Make the files public.

4. Test the Application
Access the S3 Static Website Endpoint in your browser.
Upload a photo.
Verify:
The photo appears in the S3 bucket.
Metadata is stored in DynamoDB.
Success message is displayed on the webpage.

Folder Structure in the machine : 

photo-sharing-backend/
├── app.py         # Flask app for handling uploads
photo-sharing-frontend/
├── index.html     # Main HTML file
├── style.css      # CSS for styling
├── script.js      # JavaScript for API calls

Troubleshooting:
403 Forbidden on S3 Website
Ensure the bucket policy allows public access.
Make the uploaded files public.

Error: Failed to Fetch
Check the backend URL in script.js.
Ensure the Flask app is running and accessible on port 5000.

500 Internal Server Error
Check Flask logs for errors.
Verify DynamoDB table configuration and IAM role permissions.

Future Enhancements
Use HTTPS for secure communication.
Add user authentication.
Deploy using Docker containers and Kubernetes for scalability.

Contributors
VINODGOUDA M 
    

