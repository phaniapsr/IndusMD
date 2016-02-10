###### Author       : Sri Sai Venkatesh.
###### Date          : 18-Feb-2013
###### Description: This document comprise of total detail of hiding a sub panel.
###### Team         : EMR Team.
###### SugarCRM version : 6.5

## Purpose
This document comprise of total detail of hiding a sub panel.
###Below is the step wise process flow of hiding sub panels:
1. We need to write a custom script file in the path
  `custom/extension/modules/requried_module/Ext/Layoutdefs/filename.php`
2. In the above path file could be given any name as per developer wish.
3. Define the layout definition as unset for the sub panel that we want to hide.
4. Syntax of the layout definition for hiding subpanel is:
  ```unset($layout_defs[<parent module>]['subpanel_setup'][<sub panel module name>]);```
5. Save this php file and run repair and rebuilt from the admin section of sugar.
