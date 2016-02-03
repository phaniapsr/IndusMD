## Aim: This document explains various types of logichooks available in SugarCRM for altering general logic flow 
#### There are basically 3 types of hooks in sugarCRM:
 1. Application hooks(eg: after_ui_frame, after_ui_footer etc)
 2. User hooks(eg: before_login, before_logout, after_login, after_logout etc)
 3. Module hooks(eg: after_save, before_save, after_retrieve, before_retrieve etc )
#### Adding hooks to sugarcrm:

###### Step 1: 
   There is an empty folder named custom in root folder of sugarcrm application.The
custom hooks are separate from core sugarcrm business logic.

###### Step 2: 
   Let's say we need to create a business hooks for Accounts module,create a folder
called modules in custom folder.create a folder with module name Accounts in module folder

###### Step 3:
   create a php file called logic_hooks.php in Accounts folder.The code in the file looks as shown below
```
<?php
 if (!defined('sugarEntry') || !sugarEntry) die('Not A Valid Entry   Point');
 $hook_array = array();
 $hook_array['after_save'] = array();
 $hook_array['after_save'][] = array(1, 'sav', 'custom/modules/Accounts/sav.php', 'sav', 'sav');
?>
```
The $hook_array variable stores the event for which you want to apply a particular hook.Here the event is after_save

###### The array() declaration above has 5 parameters:
  * First parameter is a processing index
  * Second parameter is string to identify the hook
  * Third parameter is a php file where logic is present
  * Fourth parameter is a class name in the php file
  * Fifth parameter is a method name in the class which has the logic

###### Step 4
  create the file sav.php which has business logic in it as shown below:
```
<?php
 if (!defined('sugarEntry') || !sugarEntry) die('Not A Valid Entry Point');
 class SaveHandler
 {
      function saveHandler(&$bean, $event, $arguments){
          //simple alert box pops up for the hook event
          die('<script language="javascript">alert("Account hook by Docfiles")</script>;');
      }
 }
```
The class name is sugar logic save which has a method method save event
The method signature for business logic method is
method_name(&$bean,$event,$arguments)
* First parameter is the reference to the $this bean
* Second parameter is the string for the current event(eg: before_save etc)
* Third parameter is the array of arguments for the event.

###### Step 5:
  Make sure the permissions are changed for logic_hooks.php and the business logic class file so that it is accessed by the web server or else sugarcrm can't read these files.
