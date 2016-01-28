## Aim :
  Create Dynamically UI and Text Fields using XML.
## Description:
  When a user login into iPad using his login credentials, a request (uisng SOAP or HTTP) 
is sent to web server. Depending upon the user type web server responses with few details 
mentioned below:
* UI interface(Ex: Tab View, Split View, Modal View...) of the App.
* View(Ex: View, Table View....) of each page.
* Number of Fields in each page/tab.
* Accessibility of each field.
## Approach:
   Web server sends the type of UI and the number of items/pages in UI is send through 
XML. Need to parse the XML response and display UI interface and its related fields.
# Sample XML file is shown below:

<?xml version="1.0" encoding="UTF-8" ?>
`<MangoUserDataFile>
  <Device>iPad</Device>
  <Version>3.0</Version> 
 <UserName>XYZ</UserName>
 <UserType>Admin</UserType>
 <Module>TabView</Module>
`<tab id="1"> `
   <item>
    <name>Home</name>
    <value>WebView</value>
</item> 
</tab>
<tab id="2">
<item>
  <name>Search</name>
  <value>view</value>          
 </item>
</tab> 
</MangoUserDataFile> `
 In the above XML, the attribute “tab” represents the Tab and “id” represent the order of the tab. 
“name” is the name of the tab and “value” represents the type of view. 
 When a particular page/Tab is clicked then a new request is sent to web server and the 
response will contains the number of fields and its accessibility. The response is in XML format 
and the sample looks like
` <?xml version="1.0" encoding="UTF-8" ?>
  <MangoUserDataFile>
  <Device>iPad</Device>
  <Version>3.0</Version> 
  <UserName>XYZ</UserName>
  <UserType>Admin</UserType>
  <Module>Page1</Module>
  <property id="textfield">
  <item>
  <name>Field1</name>
  <value>Admin</value>
  <length>20</length>
  <editable>True</editable>
  <sequence>1</sequence>
  <section>1</section>
  </item>`
`<item>
    <name>Field2</name>
    <value>text2</value>
    <length>20</length>
    <editable>True</editable>
    <sequence>1</sequence>
    <section>1</section>
   </item> `
`<item>
     <name>Field3</name> 
     <value>text3</value>
     <length>20</length>
     <editable>True</editable>
     <sequence>1</sequence>
     <section>1</section>
     </item> `
 `<item>
      <name>Field4</name>
      <value>text4</value>
      <length>20</length>
      <editable>True</editable>
      <sequence>1</sequence>
      <section>1</section>
     </item>`
`<item>
      <name>Field5</name>
      <value>text5</value>
      <length>20</length>
      <editable>False</editable>
      <sequence>1</sequence>
      <section>1</section>
    </item>
` </property>
       <property id="button">
    <item>
       <name>button1</name>
       <value>button1</value>
       <length>20</length>
       <editable>True</editable>
       <sequence>1</sequence>
       <section>1</section>
     </item>
  `<item>
       <name>button2</name>
       <value>button2</value>
       <length>20</length>
       <editable>True</editable>
       <sequence>1</sequence>
       <section>1</section>
     </item>
  `<item>
       <name>button3</name>
       <value>button3</value>
       <length>20</length> 
       <editable>True</editable>
       <sequence>1</sequence>
       <section>1</section>
    </item>
     </property>`
  ` <property id="barbutton">
      <item>
        <name>right</name>
        <value>next</value>
        <length>6</length>
        <editable>True</editable>
        <sequence>1</sequence>
        <section>1</section>
        </item>
      </property>
  ` <property id="bool">
     <item>
        <name>Field1</name>
        <value>1</value>
        <length>1</length>
        <editable>True</editable>
        <sequence>1</sequence>
        <section>1</section>
      </item>
    </property> 
    <property id="switch">
    <item>
      <name>India Wins</name>
      <value>YES</value>
      <length>1</length>
      <editable>NO</editable>
      <sequence>1</sequence>
      <section>1</section>
     </item>
    </property>
</MangoUserDataFile> 
  In above XML,”id” in property will represents type of filed and the remaining will tells about its 
functionality.
# Functionality:
  Uisng NSXML parser we will parse teh XML and store it in a mutable array. This array contains 
dictionary .
#Note: We need to create all views or fields progmatically. We can't use Interface builder to 
create UI or fields.
## Create Tab view programmatically:
tab=[[UITabBarController alloc]init];
NSMutableArray *tabViewControl = [[NSMutableArray alloc]init];
.
.
.
[tabViewControl addObject:viewNav];
[tab setViewControllers:tabViewControl];
[self.view addSubview:tab.view];
## Create Text Field programmatically:
 UILabel *lblMyLable = [[[UILabel alloc] initWithFrame:CGRectMake(10 + k, (j* 100) + 100, 150, 
40)]autorelease];
 llblMyLable.lineBreakMode = UILineBreakModeWordWrap;
 llblMyLable.numberOfLines = 0;//Dynamic
 llblMyLable.tag=1301;
 llblMyLable.backgroundColor = [UIColor clearColor];
 llblMyLable.text = fieldsDict.name;
 [[self.view addSubview:lblMyLable];
UITextField * textFieldRounded = [[UITextField alloc] initWithFrame:CGRectMake(80 + k,(j *100)+ 100, 150, 40)];
  textFieldRounded.borderStyle = UITextBorderStyleRoundedRect;
  textFieldRounded.textColor = [UIColor blackColor]; //text color
  textFieldRounded.font = [UIFont systemFontOfSize:17.0];  //font size
//textFieldRounded.placeholder = @"<enter text>";  //place holder
 textFieldRounded.text = fieldsDict.value;
 textFieldRounded.userInteractionEnabled=NO;
 textFieldRounded.backgroundColor = [UIColor greenColor]; //background color 
 textFieldRounded.autocorrectionType = UITextAutocorrectionTypeNo;    // no auto correction support
 textFieldRounded.keyboardType = UIKeyboardTypeDefault;  // type of the keyboard
 textFieldRounded.returnKeyType = UIReturnKeyDone;  // type of the return key
 textFieldRounded.clearButtonMode = UITextFieldViewModeWhileEditing;    // has a clear 'x' button to the right
## Create BUTTON programmatically:
     UIButton *myButton = [UIButton buttonWithType:UIButtonTypeRoundedRect];
     myButton.frame = CGRectMake((j *200) + 50, 750, 150, 40); 
     [myButton setTitle:fieldsDict.value forState:UIControlStateNormal];
     [self.view addSubview:myButton];
     UILabel *lblMyLable2 = [[[UILabel alloc] initWithFrame:CGRectMake(50,10, 130,30)]autorelease];
     //lblMyLable2.lineBreakMode = UILineBreakModeWordWrap;
     lblMyLable2.backgroundColor = [UIColor clearColor];
     llblMyLable2.text = fieldsDict.name;
     [self.view addSubview:lblMyLable2]; `
##  Create SWITCH programmatically:
   UISwitch *switchBtn;
   switchBtn=[[UISwitch alloc]initWithFrame:CGRectMake(150, 10, 130, 40)];
   BOOL status = [fieldsDict.value boolValue];
    [switchBtn setOn:status animated:YES];
    switchBtn.enabled = [fieldsDict.editable boolValue];
    [self.view addSubview:switchBtn];
