Filters log entries based on a condition. 

Supported in .NET, Silverligt, Compact Framework and Mono.
##Configuration Syntax
```
<targets>
  <target xsi:type="FilteringWrapper" name="String" condition="Condition">
    <target xsi:type="wrappedTargetType" ...target properties... />
  </target>
</targets>
```
##Parameters
###General Options
_name_ - Name of the target.
###Filtering Options
_condition_ - Condition expression. Log events who meet this condition will be forwarded to the wrapped target. Condition Required.