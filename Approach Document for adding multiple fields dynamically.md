## Purpose
This document explains the stepwise approach for creating multiple text fields dynamically in the edit view of the page. 

### Step 1
Create a custom field using studio with the data type text field. In this case i have created a text field named ‘multi’ in custom module multi fields.

### Step 2
Create a file Save.php in modules/<module name>/ directory. Place the code in the file.

```
  <?php 
        if(!defined('sugarEntry') || !sugarEntry) die('Not A Valid Entry Point');
        require_once('modules/<module name>/<module name>FormBase.php');
        $multiForm = new <module name>FormBase();
        $prefix = empty($_REQUEST['dup_checked']) ? '' : '<module name>';
        $multiForm>handleSave($prefix, true, false);
  ?>
```
Here we are calling handleSave function to customize the saving functionality.

### Step 3
Now we have to create a file named <module name>FormBase.php and place the below code.
```
<?php
class multifieldsFormBase {
	function handleSave($prefix, $redirect=true, $useRequired=false){
		global $theme, $current_user;
		require_once('include/formbase.php');
		global $timedate;
		$focus = new multifields();
		$con='';
		// Here we are generating a ',' separated string with all the muilti fields
		if(isset($_POST[multi])){
			for($i=0;$i<count($_POST[multi]);$i++)
				if($_POST[multi][$i]!=''&&$con=='')
					$con=$_POST[multi][$i];
					else if($_POST[multi][$i]!='')
						$con=$con.','.$_POST[multi][$i];
						if($con!='')
							$focus->multi=$con;
		}
		// Needs to get remaining fields data
		$focus->name=$_POST[name];
		$focus->description=$_POST[description];
		$focus->assigned_user_name=$_POST[assigned_user_name];
		$focus->assigned_user_id=$_POST[assigned_user_id];
		$focus->id=$_POST[record];
		if (isset($GLOBALS['check_notify'])) {
				$check_notify = $GLOBALS['check_notify'];
			}
		else {
			$check_notify = FALSE;
		}
		$focus->save($check_notify);
		$return_id = $focus->id;
		if(!$focus->ACLAccess('Save')){
			ACLController::displayNoAccess(true);
			sugar_cleanup(true);
		}
		if($redirect){
			$this->handleRedirect($return_id);
		}else{
			return $focus;
		}
	}

	function handleRedirect($return_id){
	    if(isset($_POST['return_module']) && $_POST['return_module'] != "") {
		$return_module = $_POST['return_module'];
	    }
	    else {
		$return_module = " multifields";
	    }
		if(isset($_POST['return_action']) && $_POST['return_action'] != "") {
			if($_REQUEST['return_module'] == 'Emails') {
	   		    $return_action = $_REQUEST['return_action'];
			}
	   		// if we create a new record "Save", we want to redirect to the DetailView
			elseif($_REQUEST['action'] == "Save" && $_REQUEST['return_module'] != "Home") {
			    $return_action = 'DetailView';
			}
			else {
	   		    // if we "Cancel", we go back to the list view.
	   		    $return_action = $_REQUEST['return_action'];
	   		}
	   	}
	   	else {
	    	$return_action = "DetailView";
		}
		if(isset($_POST['return_id']) && $_POST['return_id'] != "") {
			$return_id = $_POST['return_id'];
		}
			hocation: index.php?action=$return_action&module=$return_module&record=$return_id");
		}
}
?>

```
*Note: > handleSave function code varies according to the fields we have in the module. 
       > In the above code multifields need to replace with the module name*
