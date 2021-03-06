Sends log messages to a NLog Receiver Service (using WCF or Web Services).

Supported in .NET, Silverlight, Compact Framework and Mono.
##Configuration Syntax
```xml
<targets>
  <target xsi:type="LogReceiverService"
          name="String"
          endpointConfigurationName="String"
          endpointAddress="String"
          useBinaryEncoding="Boolean"
          clientId="Layout"
          includeEventProperties="Boolean">
    <parameter layout="Layout" name="String" type="System.Type"/><!-- repeated -->
  </target>
</targets>
```
Read more about using the [Configuration File](Configuration-file).
##Parameters
###General Options
_name_ - Name of the target.
###Connection Options
_endpointConfigurationName_ - Name of the endpoint configuration in WCF configuration file.  
> This parameter is not supported in:
> * NLog v2.0 for .NET Compact Framework 2.0
> * NLog v2.0 for .NET Compact Framework 3.5
> * NLog v2.0 for .NET Framework 2.0

_endpointAddress_ - Endpoint address. Required.
###Payload Options
_useBinaryEncoding_ - Indicates whether to use binary message encoding. [Boolean](Data-types)  
> This parameter is not supported in:
> * NLog v2.0 for .NET Compact Framework 2.0
> * NLog v2.0 for .NET Compact Framework 3.5
> * NLog v2.0 for .NET Framework 2.0
> * NLog v2.0 for Silverlight 2.0

_parameters_ - The list of parameters. [Collection](Data-types)  
Each collection item is represented by \<parameter /> element with the following attributes:
  * _layout_ - Layout that should be use to calcuate the value for the parameter. [Layout](Data-types) Required.
  * _name_ - Name of the parameter.
  * _type_ - Type of the parameter.System.Type

_clientId_ - Client ID. [Layout](Data-types)

_includeEventProperties_ - Indicates whether to include per-event properties in the payload sent to the server. [Boolean](Data-types)

##Examples
###Passing Parameters
Parameters are passed to the WCF LogReceiverService target using one or more configuration lines such as:
```xml
<parameter name="MyParameter" layout="My Value!" />
<parameter name="nlogdir" layout="${nlogdir}" />
```
These parameters are passed over the network to the service and can be accessed by emitting events from your receiver application.

###Application for receiving events
```csharp
namespace MyLogReceiverApp
{
   using System;
   using NLog;
   using NLog.LogReceiverService;

   /// <summary>
   /// Log service server object that logs messages.
   /// </summary>
   public class LogReceiverServer : ILogReceiverServer
   {
       public void ProcessLogMessages(NLogEvents nevents)
       {
           var events = nevents.ToEventInfo("Client.");
           Console.WriteLine("in: {0} {1}", nevents.Events.Length, events.Count);

           foreach (var ev in events)
           {
               var logger = LogManager.GetLogger(ev.LoggerName);
               logger.Log(ev);
           }
       }
   }
}
```
The line:

`logger.Log(ev);`

emits each event to the appropriate targets defined in the server side NLog.config file.

###Accessing Custom Values
On the server side NLog.config file, you may use the ${event-context} layout renderer to access any parameters passed from the client side config. A line such as:

```xml
<target name="c" xsi:type="ColoredConsole" layout="testing ${event-context:item=MyParameter}" />
```

would print to the console:

`testing My Value!`