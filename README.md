# EXPERIMENT NO. 6
***Sabarish A***
***(212225230232)***
## LOGIN INTO AWS AND IMPLEMENT IDENTITY MANAGEMENT USING AMAZON IAM

------------------------------------------------------------------------

## AIM

To create and configure IAM users and groups in AWS, assign permissions
using IAM policies, enable console access, and verify role-based access
to Amazon S3.

------------------------------------------------------------------------

## REQUIREMENTS

-   AWS Account
-   Internet Connection
-   Web Browser
-   Amazon S3 Bucket

------------------------------------------------------------------------

# PROCEDURE

## Step 1: Login to AWS Management Console

1.  Open a web browser.
2.  Go to the AWS Management Console.
3.  Sign in using the AWS account credentials.
4.  Search for **IAM** using the AWS search bar.
5.  Open **IAM (Identity and Access Management)**.

### Screenshot


<img width="1609" height="910" alt="image" src="https://github.com/user-attachments/assets/034d6d10-48c6-4df4-b8b2-3fa415206bb9" />

------------------------------------------------------------------------

## Step 2: Create an IAM Group

1.  In the IAM dashboard, select **User groups** from the left-side
    menu.

2.  Click **Create group**.

3.  Enter the group name:

    `cloudSecurity_2026`

4.  Do not add users at this stage if the user will be created
    separately.

5.  Click **Create user group**.

The group `cloudSecurity_2026` is now created.

### Screenshot --- IAM Group Created


<img width="1601" height="907" alt="image" src="https://github.com/user-attachments/assets/0b99608e-19be-4008-a5cf-bcd324d62e5e" />

------------------------------------------------------------------------

## Step 3: Attach an IAM Policy to the Group

1.  Open the **cloudSecurity_2026** group.

2.  Select the **Permissions** tab.

3.  Click **Add permissions**.

4.  Select **Attach policies directly**.

5.  Search for:

    `AmazonS3ReadOnlyAccess`

6.  Select the checkbox for **AmazonS3ReadOnlyAccess**.

7.  Click **Next** and then **Add permissions**.

The group now has read-only access to Amazon S3.

### Screenshot --- Policy Attached


<img width="1606" height="906" alt="image" src="https://github.com/user-attachments/assets/6c1b2f7e-9d1f-4593-8e29-063a00b42937" />

------------------------------------------------------------------------

## Step 4: Create an IAM User

1.  From the IAM navigation menu, select **Users**.

2.  Click **Create user**.

3.  Enter the username:

    `student01`

4.  Click **Next**.

### Screenshot --- IAM User Created


<img width="1602" height="905" alt="image" src="https://github.com/user-attachments/assets/417c9601-06bc-4a63-aac7-8e5cbca28716" />

------------------------------------------------------------------------

## Step 5: Add the User to the IAM Group

1.  On the **Permissions** page, select **Add user to group**.

2.  Select:

    `cloudSecurity_2026`

3.  Click **Next**.

4.  Review the configuration.

5.  Click **Create user**.

The user is now a member of the `cloudSecurity_2026` group.

### Screenshot --- User Added to Group

<img width="1422" height="804" alt="image" src="https://github.com/user-attachments/assets/f4ba29d0-ae6d-4a78-84f2-fafdf575a2fc" />


------------------------------------------------------------------------

## Step 6: Verify User Permissions

1.  Open **IAM → Users**.

2.  Click **student01**.

3.  Open the **Permissions** tab.

4.  Verify that the following policy is displayed:

    `AmazonS3ReadOnlyAccess`

5.  Check the **Attached via** column.

6.  It should indicate that the policy is attached through:

    `Group: cloudSecurity_2026`

### Permission Flow

``` text
student01
    ↓
cloudSecurity_2026
    ↓
AmazonS3ReadOnlyAccess
    ↓
Amazon S3 Read-only Access
```

### Screenshot --- User Permissions


<img width="1429" height="798" alt="image" src="https://github.com/user-attachments/assets/4b19062c-9c80-4c3c-bdf0-304d0473e317" />

------------------------------------------------------------------------

## Step 7: Enable Console Access

Initially, console access for `student01` may be disabled.

1.  Open **IAM → Users → student01**.
2.  Select **Security credentials**.
3.  Locate **Console access / AWS Management Console access**.
4.  Enable console access.
5.  Create a console password for `student01`.
6.  Complete the configuration.

> **Note:** Do not share the password with other users.

### Screenshot --- Security Credentials / Console Access


<img width="1610" height="914" alt="image" src="https://github.com/user-attachments/assets/718d8cec-610f-4134-96e1-ba30589a8f78" />

------------------------------------------------------------------------

## Step 8: Obtain the AWS Account ID

The IAM user login requires the AWS account ID.

1.  The AWS account ID is a 12-digit number.
2.  It can be found in the AWS account information.
3.  Use **your own AWS account ID** when performing the experiment.



------------------------------------------------------------------------

## Step 9: Login as the IAM User

1.  Sign out from the current AWS administrator/root session.

2.  Open a new browser window or Incognito/Private window.

3.  Open the AWS sign-in page.

4.  Select **IAM user login**.

5.  Enter the AWS account ID.

6.  Enter the IAM username:

    `student01`

7.  Enter the password created in Step 7.

8.  Click **Sign in**.

The AWS Management Console should now open under the IAM user
`student01`.

### Screenshot --- IAM User Console


<img width="1601" height="907" alt="image" src="https://github.com/user-attachments/assets/c2805bb4-b987-4a1d-84a4-a5468a828dbe" />

------------------------------------------------------------------------

## Step 10: Verify Amazon S3 Access

1.  After logging in as `student01`, search for **S3**.
2.  Open **Amazon S3**.
3.  Select **General purpose buckets**.
4.  Verify that the previously created S3 bucket is visible.
5.  Open the bucket.
6.  Verify that the user can view the bucket and its objects.

This confirms that the IAM policy is providing S3 read access.

### Screenshot --- S3 Bucket Access


<img width="1429" height="800" alt="image" src="https://github.com/user-attachments/assets/b26b7dad-cb94-4f45-a995-0e358bff97dd" />

------------------------------------------------------------------------

## Step 11: Verify Least-Privilege Access

The user `student01` has been assigned:

`AmazonS3ReadOnlyAccess`

Therefore, the user should have **read access** but should not have
permission to perform S3 **write/delete operations**.

For testing:

1.  Open the S3 bucket as `student01`.
2.  Observe the available operations.
3.  Do not delete any existing object.
4.  If you test an upload operation, do not use an important file.
5.  The actual permission check occurs when AWS attempts the S3
    operation.
6.  A read-only user should receive an **Access Denied** response for
    unauthorized write/delete operations.



------------------------------------------------------------------------


# EXPECTED RESULT

The IAM group `cloudSecurity_2026` is successfully created and assigned
the `AmazonS3ReadOnlyAccess` policy. The IAM user `student01` is
successfully created, added to the group, and provided with AWS
Management Console access. The user can log in to AWS and access the
assigned S3 resources according to the permissions inherited from the
group.

------------------------------------------------------------------------

# RESULT

Thus, **Identity and Access Management (IAM) was successfully
implemented in AWS** by creating an IAM group, assigning an S3 read-only
policy, creating an IAM user, enabling console access, and verifying
permission-based access to Amazon S3.

------------------------------------------------------------------------


