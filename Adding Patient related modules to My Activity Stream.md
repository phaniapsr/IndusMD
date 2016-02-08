#### Aim: Adding modules to My Activity Stream.

#### Step 1: 
  Create a folder name SugarFeeds in the respective module for which the data has to be displayed in My Activity Stream.

#### Step 2: 
   In the above created folder create a new file with naming convensions as ’moduleFeed.php’ 

#### Step 3:  
   Add the following code in the above file

**_Code:_**

```

<?php
  require_once('modules/SugarFeed/feedLogicBase.php');
    class DoctorFeed extends FeedLogicBase
     { 
       public $module = 'mango_doctor'; 
      public function pushFeed($bean, $event, $arguments) 
           {
            $text = '';
           if(empty($bean->fetched_row)){
           $text = 'Created Doctor [' . $bean->module_dir . ':' . $bean->id . ':' . $bean->name.']';
            }
        if(!empty($text)){
                SugarFeed::pushFeed2($text, $bean);
           } 
       }
    }

```
##### Step 4:
    We need to enable the Feed in the SugarFeeds admin panel.
