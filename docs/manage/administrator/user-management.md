# User Management

In this section, you will learn how to create and manage users.

## Create User

Here is a video on how to create and manage users for different operations within <code class="expression">space.vars.SITENAME</code>:

> **Note** : All the new users in <code class="expression">space.vars.SITENAME</code> have administrator-level permissions. With the administrator-level permissions, the users will have access to all features.

{% embed url="https://youtu.be/r8HbL_Kz-rQ" %}

To add a new user, follow the steps given below:

* Click **Administration**.
* The **Users** page will open. You can see the list of users already added.
* To add a new user, click the plus sign (+) on the top right corner of the screen.

<div align="center"><img src="../../../.gitbook/assets/User_Management_Image_1C.png" alt="" width="2000"></div>

* The Create User form will open. Fill the following details in the form:
  * First name of the user
  * Last name of the user
  * Email Address of the user
  * User name: Provide name as per the username attribute on Identity Provider.\
    **Note:** For Azure Active Directory, it has to be same as 'Unique User Identifier'. To get 'Unique User Identifier' refer to [Username Identifier for Azure Active Directory](user-management.md#username-identifer-for-azure-active-directory).

<div align="center"><img src="../../../.gitbook/assets/User_Management_Image_2CF123.png" alt="" width="1000"></div>

* You also need to fill the fields as shown in the image above.
* Click **Save**.

> **Note** : All the new users have administrator-level permissions. With the administrator-level permissions, the users will have access to all features.

## Appendix

### Username Identifier for Azure Active Directory

* After logging in the Azure Active Directory,
  1.  Go to **Enterprise applications**.

      <div align="center"><img src="../../../.gitbook/assets/Azure_Services.png" alt=""></div>
  2.  Select your application from **All applications**.

      <div align="center"><img src="../../../.gitbook/assets/Azure_Application.png" alt="" width="900"></div>
  3.  Select **Single sign-on** from left panel.

      <div align="center"><img src="../../../.gitbook/assets/Azure_SingleSignOn.png" alt=""></div>
  4.  Refer to section **User Attributes & Claims**.

      <div align="center"><img src="../../../.gitbook/assets/Azure_UserAttribute.png" alt="" width="800"></div>

> **Note** : The attribute which is specified in 'Unique User Identifer' should be used while defining the user's 'User name' in <code class="expression">space.vars.SITENAME</code>. For example, here 'user.mail' is the selected attribute and so this property of the user from Azure Active Directory is to be used while defining 'User name' in <code class="expression">space.vars.SITENAME</code>.
