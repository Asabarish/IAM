# EXPERIMENT NO. 6

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

![AWS Management Console](experiment6_assets/04-aws-console-home.jpeg)

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

![IAM Group Created](experiment6_assets/01-iam-group-created.jpeg)

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

![Amazon S3 Read Only
Policy](experiment6_assets/02-s3-readonly-policy-attached.jpeg)

------------------------------------------------------------------------

## Step 4: Create an IAM User

1.  From the IAM navigation menu, select **Users**.

2.  Click **Create user**.

3.  Enter the username:

    `student01`

4.  Click **Next**.

### Screenshot --- IAM User Created

![IAM User Created](experiment6_assets/03-iam-user-created.jpeg)

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

> **Attach screenshot here if a separate group-membership screenshot is
> required.**

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

> **Attach screenshot here.**

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

![Student01 Security
Credentials](experiment6_assets/05-student01-security-credentials.jpeg)

------------------------------------------------------------------------

## Step 8: Obtain the AWS Account ID

The IAM user login requires the AWS account ID.

1.  The AWS account ID is a 12-digit number.
2.  It can be found in the AWS account information.
3.  Use **your own AWS account ID** when performing the experiment.

### Screenshot --- AWS Account Information

> **Attach screenshot here if required.**
>
> **Do not publish passwords, secret access keys, or other sensitive
> credentials in the repository.**

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

![Student01 AWS
Console](experiment6_assets/06-student01-console-login.jpeg)

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

![S3 Bucket Access](experiment6_assets/07-s3-bucket-access.jpeg)

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

> **Important:** The S3 console may display an Upload button even when
> the user does not have permission to complete the upload. The presence
> of the button alone does not prove that upload permission exists.

### Screenshot --- Least-Privilege / Access Denied

> **Attach screenshot here if you performed the permission test.**

------------------------------------------------------------------------

# SCREENSHOT CHECKLIST

    No. Screenshot                              Status
  ----- --------------------------------------- ---------------------
      1 AWS Management Console / IAM            ✅ Added
      2 IAM Group Created                       ✅ Added
      3 AmazonS3ReadOnlyAccess Attached         ✅ Added
      4 IAM User `student01` Created            ✅ Added
      5 User Added to `cloudSecurity_2026`      ⬜ Add if available
      6 User Permissions / Attached via Group   ⬜ Add if available
      7 Security Credentials / Console Access   ✅ Added
      8 AWS Account Information                 ⬜ Add if required
      9 IAM User Console Login                  ✅ Added
     10 S3 Bucket Access                        ✅ Added
     11 Least-Privilege / Access Denied Test    ⬜ Add if performed

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

## FILE STRUCTURE

``` text
Experiment-6/
│
├── README.md
│
└── experiment6_assets/
    ├── 01-iam-group-created.jpeg
    ├── 02-s3-readonly-policy-attached.jpeg
    ├── 03-iam-user-created.jpeg
    ├── 04-aws-console-home.jpeg
    ├── 05-student01-security-credentials.jpeg
    ├── 06-student01-console-login.jpeg
    └── 07-s3-bucket-access.jpeg
```

> **GitHub tip:** Keep the `experiment6_assets` folder in the same
> repository as `README.md` so all screenshots display automatically.
