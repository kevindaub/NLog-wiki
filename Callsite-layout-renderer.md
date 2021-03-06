The call site (class name, method name and source information). 

Supported in .NET, Silverlight and Mono.

##Configuration Syntax
```
${callsite:className=Boolean:fileName=Boolean:includeSourcePath=Boolean
          :methodName=Boolean:cleanNamesOfAnonymousDelegates=Boolean:skipFrame=Integer}
```

##Parameters
###Rendering Options
* **className** - Indicates whether to render the class name.Boolean Default: True
* **fileName** - Indicates whether to render the source file name and line number.Boolean Default: False

  > This parameter is not supported in:
  > * NLog v2.0 for Silverlight 2.0
  > * NLog v2.0 for Silverlight 3.0
  > * NLog v2.0 for Silverlight 4.0
  > * NLog v2.0 for Silverlight for Windows Phone 7
  > * NLog v2.0 for Silverlight for Windows Phone 7.1

* **includeSourcePath** - Indicates whether to include source file path.Boolean Default: True

  > This parameter is not supported in:
  > * NLog v2.0 for Silverlight 2.0
  > * NLog v2.0 for Silverlight 3.0
  > * NLog v2.0 for Silverlight 4.0
  > * NLog v2.0 for Silverlight for Windows Phone 7
  > * NLog v2.0 for Silverlight for Windows Phone 7.1

* **methodName** - Indicates whether to render the method name.Boolean Default: True
* **cleanNamesOfAnonymousDelegates** - Indicates whether the method name will be cleaned up if it is detected as an anonymous delegate. Boolean Default: False
* **skipFrames** - The number of frames to skip. Integer Default: 0

##Notes
please note that the method name won't work well with async methods - it will always show `MoveNext`. Too bad we cannot fix this shortcoming. See [GitHub issue #255](https://github.com/NLog/NLog/issues/255).