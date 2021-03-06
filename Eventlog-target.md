Writes log message to the Event Log. 

Supported in .NET and Mono
##Configuration Syntax
```xml
<targets>
  <target xsi:type="EventLog"
          name="String"
          layout="Layout"
          machineName="String"
          source="Layout" 
          category="Layout"
          eventId="Layout"
          log="String" />
<!-- note: source is a string in NLog before 4.0 -->

</targets>
```
Read more about using the [Configuration File](Configuration file).

##Parameters
###General Options
 * _name_ - Name of the target.

###Layout Options
 * _layout_ - Layout used to format log messages. [Layout](Layouts) Required. Default: ${longdate}|${level:uppercase=true}|${logger}|${message}

###Event Log Options
 * _machineName_ - Name of the machine on which Event Log service is running. Default: `.`  
 * _source_ - Value to be used as the event Source. By default this is the friendly name of the current AppDomain. From NLog 4.0 this is layoutable(Layouts). 
 * _category_ - [Layout](Layouts) that renders event Category.  The categories must be predefined for the specified _source_ and needs to be numeric.   
 * _eventId_ - [Layout](Layouts) that renders event ID. 
 * _log_ - Name of the Event Log to write to. This can be System, Application or any user-defined name. Default: Application

##note
When install/uninstalling, the event source is only created / removed when the _source_ doesn't contain layout renderers. 

##Example
```xml
<target xsi:type="EventLog"
            name="eventlog"
            source="test"
            layout="${message}${newline}${exception:format=ToString}"/>
```