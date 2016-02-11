###### Prepared By: Charan Raj
###### Date  : 21-May-2015
###### SugarCRM version : 6.5

### Aim: 
This document will explain the process of Sending Confirmation Code (SMS) Functionally.

#### Step 1:(Prerequisites)
Need to include the following SMS Library files.

```
require_once("MangoLib/smsLib/NexmoResponseArray.php");
require_once("MangoLib/smsLib/NexmoMessage.php");
require_once("MangoLib/smsLib/MvaayooMessage.php");

```
#### Step 2:(Prerequisites)
Second we need to declare SMS Gateway Providers credentials in sugar config.php file.

```
 'smsGateway' =>array (
                  'Nexmo' => array (
                              'ApiKey' => 'e3194c05',
                              'ApiSecret' => 'b6473c3d',
                              //'FromUS' => '19705500049',
                              'FromUS' => '12184141097',
                  ),
                  'Mvaayoo' =>  array (
                    'ApiKey' => 'withcheer.venky@gmail.com',
                    'ApiSecret' => '123456',
                    'FromId' => 'TEST SMS',
                  ),
              )
```              
#### Step 3:(Prerequisites)
We need to save confirmation code message in sugar config.php file.

```
'text_msg' => array (   
                iPhone app',    
              ),
```

#### Step 4:(Implementation)
We are sending SMS confirmation code  to user when two actions occurred in mng_userd_devices module, the two actions are as follows.
1. When new record inserted into mng_user_devices module.
2.  When we set reset_flag to one.
When the above two actions occurs we  are triggering logic hooks file in mng_userd_devices module. The logic hooks file location was MangoLib/logichooks/HandleUserDeviceSave.php

#### Step 5:(Sending SMS) 
For sending SMS to users phone ,we are two SMS Gateways based on the user's country code. 
1. Mvaayoo (For only India Numbers).
2. Nexmo (For Countries Other than India).

#### 1.Mvaayoo SMS Gateway
If  users country code was 91(India) , we are invoking Mvaayo API to send SMS to India phone number. and the code as follows

```
$smsObject = new MvaayooMessage($GLOBALS['sugar_config']['smsGateway']['Mvaayoo']['ApiKey'],$GLOBALS['sugar_config']['smsGateway']['Mvaayoo']['ApiSecret']); 
$smsTo = '+'.$bean->country_code.$user_phonenumber;
$info = $smsObject->sendText($smsTo,$GLOBALS['sugar_config']['smsGateway']['Mvaayoo']['FromId'], $message );
```

#### 2. Nexmo SMS Gateway
If  users country code was other than 91(India) , we are invoking Nexmo Api to send SMS outside India.and the code as follows
```
$smsObject = new NexmoMessage($GLOBALS['sugar_config']['smsGateway']['Nexmo']['ApiKey'],$GLOBALS['sugar_config']['smsGateway']['Nexmo']['ApiSecret']); 
$smsTo = '+'.$bean->country_code.$user_phonenumber;
$info = $smsObject->sendText($smsTo,$GLOBALS['sugar_config']['smsGateway']['Nexmo']['FromUS'],$message);
```
