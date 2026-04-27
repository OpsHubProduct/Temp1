# Rules Management

## View Rules

To view Rules, go to Administration > Rules Management. This would lead to a page that lists multiple rules that are already configured for different systems integrated using <code class="expression">space.vars.SITENAME</code>.

<div align="center"><img src="../../../.gitbook/assets/Rules_Management.png" alt="" width="1000"></div>

### Filters

* **Filter by rule name**: Search configured rules using the search available in the header navigation bar
* **Filter by rule state**: Click on the Active, All, or Inactive button to filter by the status

### Actions

* **View rule's xml**: Click the rule's name to view the rule's xml
* **Export rules**: Roll over the vertical ellipses icon ![](../../../.gitbook/assets/fa_vertical_ellipses1a.png) against the rule that you want to export and then select _Export rule_
* **Activate/Inactivate rules**: Select the _Status_ button against the rule for which you want to toggle the status. The status will change from _Active_ to _Inactive_ or from _Inactive_ to _Active_
* **Actions over multiple rules**: Select multiple rules and then roll over the cursor to point to the vertical ellipses icon ![](../../../.gitbook/assets/fa_vertical_ellipses1a.png) on the table header to see the operations that you could perform on multiple selected rules.

***

## Upload Rule

To upload a new rule, follow the steps given below:

* Click on **"Administration"**
* Click on ![](../../../.gitbook/assets/Rules_Management_icon.png) given on the left panel. You can see the list of rules that are already uploaded
* To upload a new rule, click on ![](../../../.gitbook/assets/Plus.png) given on the top right corner of the screen

<div align="center"><img src="../../../.gitbook/assets/Rules_Management_Upload.png" alt="" width="1000"></div>

* The Upload form will open. Fill the following details in the form:
  * **System Name**: It gives option to select the system from all the SCM systems mentioned in the dropdown
  * **Rule Name**: It represents the name of the rule which will be uploaded
  * **Rule XML**: Upload the XML file using the _Choose File_ option
  * **Weight**: It defines the priority of rule. Higher the weight, higher will be the priority given to the rule
  * **Status**: It represents whether the rule is active or inactive

<div align="center"><img src="../../../.gitbook/assets/Rules_Management_UploadForm.png" alt="" width="1000"></div>

* Click on **Save**
* Click on **Reset** to fill the form again

***

## Edit Rule

* To edit a rule, follow the steps given below:
  * Click on **"Administration"**
  * Click on ![](../../../.gitbook/assets/Rules_Management_icon.png) given on the left panel. You can see the list of rules that are already uploaded
  * To edit a rule, roll over the vertical ellipses icon ![Ellipses](../../../.gitbook/assets/fa_vertical_ellipses1a.png) against the rule that you want to edit
  * Click on&#x20;

<div align="center"><img src="../../../.gitbook/assets/Rules_Management_Edit.png" alt="" width="2200"></div>

* The Edit form will open. Edit the details in the form. Refer to the image below:

<div align="center"><img src="../../../.gitbook/assets/Rules_Management_EditForm1.png" alt="" width="900"></div>

<div align="center"><img src="../../../.gitbook/assets/Rules_Management_EditForm2.png" alt="" width="900"></div>

* Click on **"Save"**
* Click on **"Reset"** to set the previously saved value

***

## Delete Rule

* To delete the rule which is active, first you need to inactivate the rule
* To delete a rule, roll over the vertical ellipses icon ![](../../../.gitbook/assets/fa_vertical_ellipses1a.png) against the rule that you want to delete
* Click on&#x20;

<div align="center"><img src="../../../.gitbook/assets/Rules_Management_Delete.png" alt="" width="1000"></div>

* You will not be able to recover the rule once you delete it

<div align="center"><img src="../../../.gitbook/assets/Rules_Management_DeletePopup.png" alt="" width="600"></div>

* Click on **"Yes, delete it"** to delete the rule
* Click on **"Cancel"** to cancel the process
