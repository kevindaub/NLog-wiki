Converts the result of another layout output to upper case. 

Supported in .NET, Silverlight, Compact Framework and Mono.

##Configuration Syntax
```
${uppercase:uppercase=Boolean:inner=Layout:culture=Culture}
```

or by using ambient property to modify output of other layout renderer:

```
${other:uppercase=Boolean}
```

##Parameters
###Transformation Options
* _uppercase_ - Indicates whether upper case conversion should be applied. Boolean Default: True
* _inner_ - Wrapped layout. Layout
* _culture_ - Culture used for rendering. Culture