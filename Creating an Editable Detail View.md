###### Prepared By: Jeyanth Somu Kumar G
###### Date  :            06/12/2011.
###### SugarCRM version : 6.5

### Aim: Creating an Editable Detail View

### Procedure:

#### Step 1: 
   Modify the sugarCRM default detail view tpl file, which is located in the includes folder. 
Replace the DetailView.tpl file code with the below code

Sample - Code

```

{{if !$colData.field.disable_edit}}    {{if $module != ""}}

       <div class='edit_block' style="display: none;" 

id='{{$fields[$colData.field.name].name}}_editblock'>

    {{if ($fields[$colData.field.name].required && 

!isset($colData.field.displayParams.required)) ||  (isset($colData.field.displayParams.required) 

&& $colData.field.displayParams.required && $fields[$colData.field.name].required !== false)}}
    
    <input type='hidden' 
    
    id='{{$fields[$colData.field.name].name}}_required' value='true'>

    {{else}}

    <input type='hidden' 

id='{{$fields[$colData.field.name].name}}_required' value=''>

    {{/if}}

    {{if $fields[$colData.field.name] && 

$fields[$colData.field.name].type == 'relate'}}

    <input type='hidden' 

id='{{$fields[$colData.field.name].name}}_module' 

value='{{$fields[$colData.field.name].module}}'>

    <input type='hidden' 

id='{{$fields[$colData.field.name].name}}_id_name' 

value='{{$fields[$colData.field.name].id_name}}'>

    {{/if}}

    

    

    {{if $fields[$colData.field.name] && 

$fields[$colData.field.name].name == 'email1'}}

    <input type='text' 

id='{{$fields[$colData.field.name].name}}' value=''>    

    {{elseif $fields[$colData.field.name] && 

$fields[$colData.field.name].name == 'duration_hours'}}

    {literal}<script type="text/javascript">function 

isValidDuration() { form = document.getElementById('DetailView'); if ( form.duration_hours.value 

+ form.duration_minutes.value <= 0 ) { 

alert('{/literal}{$MOD.NOTICE_DURATION_TIME}{literal}'); return false; } return true; 

}</script>{/literal}<input id="duration_hours" name="duration_hours" tabindex="1" size="2" 

maxlength="2" type="text" value="{$fields.duration_hours.value}" > <select 

name='duration_minutes' id='duration_minutes'><option value='0' {if 

$fields.duration_minutes.value  == 0} selected {/if}>00</option><option value='15' {if 

$fields.duration_minutes.value  == 15} selected {/if}>15</option><option value='30' {if 

$fields.duration_minutes.value  == 30} selected {/if}>30</option><option value='45' {if 

$fields.duration_minutes.value  == 45} selected {/if}>45</option></select> &nbsp;<span 

class="dateFormat">{$MOD.LBL_HOURS_MINUTES}</span>

    {{elseif $module == "Calls" && 

$fields[$colData.field.name] && $fields[$colData.field.name].name == 'direction'}}

    {{sugar_field parentFieldArray='fields' 

tabindex=$colData.field.tabindex vardef=$fields.direction displayType='EditView' 

displayParams=$colData.direction.displayParams formName=$form_name}}&nbsp;

    {{sugar_field parentFieldArray='fields' 

tabindex=$colData.field.tabindex vardef=$fields.status displayType='EditView' 

displayParams=$colData.status.displayParams formName=$form_name}}&nbsp;

    {{elseif $fields[$colData.field.name] && 

$fields[$colData.field.name].type == 'fullname'}}

    <input type='text' id='first_name' 

value='{$fields.first_name.value}' size=10>

    <input type='text' id='last_name' 

value='{$fields.last_name.value}' size=10>

    <button type='button' 

id='{{$fields[$colData.field.name].name}}'>{$APP.LBL_EDV_SAVE}</button>   

    {{elseif $fields[$colData.field.name] && 

$fields[$colData.field.name].name != 'date_entered' && $fields[$colData.field.name].name != 

'date_modified'}}

    {counter name="panelFieldCount"}

    {{$colData.displayParams}}

    {{sugar_field parentFieldArray='fields' 

tabindex=$colData.field.tabindex vardef=$fields[$colData.field.name] displayType='EditView' 

displayParams=$colData.field.displayParams typeOverride=$colData.field.type 

formName=$form_name}}

    {{/if}}

    </div>

    {{/if}}

:

 ```

#### Step 2: 
     Now write the YUI code for the edit behaviour of the fields in the Detail View.
   This is the way the code works.
