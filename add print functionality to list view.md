### Aim:
 To add Print functionality to a List View button.

#### Steps:
1. Add Print button to the List View as previously mentioned in other document

2. Go to <sugar_root>/include/ListView/ListViewDisplay.php

3. Locate the function buildPrintLink()

4.Add this code to it
       
       ```
       1. function buildPrintLink($totalCount)
          {
            $script = '<input class="button" type="button" value="Print" onclick=
            "var t = 0; var c=document.MassUpdate[\'mass[]\'];for(var                         
            i=0;i<c.length;i++){c[i].checked?t++:null;};if(t!=1)alert(\'Please select
            one record\');else {for(var i=0;i<c.length;i++){if(c[i].checked) {var
            id=c[i].value;test(id,\''.$_REQUEST['module'].'\');}}}"/>';
        return $script;
            } // fn
            
        ```    
5. Add a javascript function to the end of the document
```
    1. <script type="text/javascript">
         function test(id,module)
         {
           //alert('Reached the test function');
          //alert(id);
         //alert(module);
string =
"\index.php?module="+module+"&offset=1&stamp=1265273590019894500&return_module="+module+"&action=DetailView&record="+id+"&print=true\,\'printwin\',\'menubar=1,status=0,resizable=1,scrollbars=1,toolbar=0,location=1\'";
window.open(string);
      }
</script>
```

#### Observation:

1. The functionality of the buttons on List Views can be altered by changing the
appropriate functions in include/ListView/ListViewDisplay.php

2. There is no need to 'Repair' the Sugar database again. Just need to refresh the
pages to reflect the changes

3. Here we are adding/altering a core document in Sugar. So, not sure if it is upgradesafe.
4. 
4. For now, it only prints one record at a time
