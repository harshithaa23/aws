# Deployment Guide for Hosting a Static Website on Amazon S3

This guide provides step-by-step instructions for hosting a static website on AWS using Amazon S3.

---

## Prerequisites
1. **AWS Account**: Ensure you have access to the AWS Management Console.
2. **Website Files**: You should have an `index.html` file and other static assets ready for upload.

---

## Steps for Deployment

### 1. Create an S3 Bucket
1. Log in to the **AWS Management Console**.
2. Search for **S3** in the services search bar and open it.
3. Click **Create Bucket**.
4. Fill out the following details:
   - **Bucket Name**: Use a unique name, e.g., `my-static-website-name`.
   - **Region**: Choose the region closest to you for better latency and cost-effectiveness.  
     Example: `Asia Pacific (Mumbai)` if you're based near Bangalore.
5. Enable **ACLs (Access Control Lists)** by choosing `ACLs enabled` under **Object Ownership**.
6. Uncheck **Block all public access** and acknowledge the warning.
7. Enable **Bucket Versioning**.
8. Click **Create Bucket**.

---

### 2. Upload Website Files
1. Go to the newly created bucket and click the **Objects** tab.
2. Click **Upload** and:
   - Select the `index.html` file.
   - Upload the unzipped folder containing your website's images or assets.
3. Click **Upload** and wait for the success message.

---

### 3. Enable Static Website Hosting
1. Go to the bucket’s **Properties** tab.
2. Scroll down to the **Static website hosting** section and click **Edit**.
3. Configure the settings as follows:
   - **Enable static web hosting**: Select `Host a static website`.
   - **Index document**: Enter `index.html`.
4. Save changes.
5. Note the **Bucket website endpoint URL** displayed under this section.

---

### 4. Make Files Public
1. Navigate to the **Objects** tab of your bucket.
2. Select all uploaded files and folders.
3. From the **Actions** dropdown, choose `Make public using ACL`.
4. Confirm and wait for the green success banner.

---

### 5. Test Your Website
1. Open the **Bucket website endpoint URL** in your browser.
2. Ensure that your website loads correctly.
3. If an error occurs, verify:
   - Files are public.
   - The index file name matches the configuration.

---

### 6. (Optional) Add Bucket Policies
To enhance access control:
1. Go to the bucket’s **Permissions** tab.
2. Add a **Bucket Policy** to prevent accidental deletions or control access further.

Example policy to prevent deletion of `index.html`:
```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Effect": "Deny",
      "Action": "s3:DeleteObject",
      "Resource": "arn:aws:s3:::my-static-website-name/index.html",
      "Principal": "*"
    }
  ]
}
