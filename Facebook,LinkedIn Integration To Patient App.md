###### Author        : Venu
###### Date          : 23-July-2012.
###### Description   : Approach document for facebook,linkedin integration to patient app.
###### Team          : IPhone Team.
###### SugarCRM version : 6.5

## Steps for creating meetings:

#### Step 1:
User Visits the IPhone Patient App

        1. User enters Login ID and Password.

        2. Clicks on Login.

#### Step 2:
        
        1. User click on Communication icon on the Dashboard screen

        2. User then clicks on Meetings icon on Communication screen.

        3. User is now in Meeting List View.
 
#### Step 3: 

        1. User clicks on Add New button on Meetings list view screen.

        2. User is now redirected to the new Meeting detail view screen.

#### Step 4:

The Meetings Detail view is divided into Three screens.

**_Screen 1:_**

      1. General Meeting fields (This will capture  all the information of meeting to be scheduled ).

      2. User clicks on Next button 

**_Screen 2:_**

      1.  User see the  Invites  Screen (This will include contacts selection from Iphone,Facebook,LinkedIn & EMR).

      2. User clicks on Post button. 

**_Screen 3:_**

      1. Now user see the check boxes option for posting data

            - Checkbox-Facebook

            - Checkbox-EMR(This will always checked).User can not edit this

            - Checkbox-LinkedIn
            
#### Step 5:

User fills all the necessary information and clicks on Post Button.

         1. The data and contact information of invitee module saved into EMR.

         2. The data is then Posted into corresponding Social Network Selected by the User.

         Eg: If user select Facebook checkbox then data posted on user facebook wall. 

## Steps for Retrieving meetings :

#### Step 1: 

  User clicks on Meetings icon on Communication screen. 

#### Step 2: 

    User can see all the meetings of EMR.

#### Step 3:

    1.  User clicks any meeting from Meetings list.

    2.  User can now  see the  meetings detail view, each meeting will include details like invite details & invitees count etc.

#### Step 4:  
   If user invites other contacts  the invite button will be active in meetings detail view.

#### Step 5:

   In meeting detail view, below we will show list of contacts with attending contacts who have 
accepted.There will be a tick mark to show that person is accepted.

## Steps for handling User Creation in EMR for External Invitees :

#### Step 1: 
    The Invites gets saved in the Invitees sub panel of particular Meeting.

#### Step 2: 

    Whenever a new entry is made in Invitees Module. 

*An internal process runs within EMR which as follows:*

     1. An Entry is will be made to Users Module, which means a user is created with the details present in Invites record.

     2.  Our Users module will have two more fields to capture LinkedIn Id and Facebook Id. 

#### Step 3: 

*The creation of User will be pass through a set of validations*

      1. Check Unique Email in Users Module if email present in record. (OR).

      2. Check Unique Phone Number if phone number present in record.(OR).

      3. Check Unique LN Id if LinkedIn id present in the record.(OR).

      4. Check Unique FB Id if Facebook id present in record.(OR).

IF none of these conditions matches a new entry is made to Users. 

#### Step 4: 

   If  all the above conditions of Step 3 fails , the user will be treated as a new User and his record will be created  with following set of Credentials.

      1. If Invitees record have Emails , then Username will be his Email itself .

      2. if Invitees record have dont have emails, the Username will be his First name + (some appending text).

      3. In case of Passwords all will have passwords as <First Name>123. 

#### Step 5 : 

  When a new entry is made into Users again a internal process of EMR executes and makes an entry into Master Instance. 
