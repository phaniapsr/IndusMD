###### SugarCRM version : 6.5

### Aim: 
  To add a hyperlink to the fields of the custom built modules.

### Procedure:

  1. Create the custom modules and fields

  2. Go to "\sugarcrm\custom\modules\<module_name>\metadata\listviewdefs.php" in
  the Sugar CRM installation files

  3. You will see an array of all the fields created with descriptions of each attribute like this

        'NAME' => array(
        'width' => '20',
        'BILLING_ADDRESS_CITY' => array(
        'label' => 'LBL_LIST_ACCOUNT_NAME',
        'default' => true),
        'width' => '10',
        'label' => 'LBL_LIST_CITY',
        'default' => true
                ),
  1. Add the following code to the fields to which the hyperlink is to be added: 'link' =>
  true,

  2. If I want to make the 'NAME' field to be a hyperlink, the code will look like this
        'NAME' => array(
        'width' => '20',
        'label' => 'LBL_LIST_ACCOUNT_NAME',
        'link' => true,
        'default' => true
               ),

        'BILLING_ADDRESS_CITY' => array(
        'width' => '10',
        'label' => 'LBL_LIST_CITY',
        'default' => true
                             ),

   1. This will add the hyperlink to the field

### Observation:

   1. Sugar Community Edition does not automatically create hyperlinks to the List view field items

   2. For now, it has to be done manually

   3. It may be automated in new release versions of Sugar
