# DbTrace
Aspectize Extension to trace to Azure Storage.
By default, trace is done to a file in your Application Directory. Using DBTrace allows you to store Trace in your Data Storage.

# 1 - Download

Download extension package from aspectize.com:
- in the portal, goto extension section
- browse extension, and find DbTrace
- download package and unzip it into your local WebHost Applications directory; you should have a DbTrace directory next to your app directory.

# 2 - Configuration

Add DbTrace as Shared Application in your application configuration file and configure app.
In your Visual Studio Project, find the file Application.js in the Configuration folder.

Add BootstrapSwitch in the Directories list :
```javascript
app.Directories = "DbTrace";

app.TraceEnabled = true;
app.TraceServiceName = "MyDbTraceService";
```

Add a new configured service in your Application

In your Visual Studio Project, find the file Services.js in the Configuration folder.

```javascript
var myDbTraceService = Aspectize.ConfigureNewService("MyDbTraceService", aas.ConfigurableServices.AzureTraceService);
myDbTraceService.DataServiceName = "MyDataService";
myDbTraceService.FileServiceName = "MyFileService";
```

The Configurable Service has the following parameters:
DataServiceName; name of your DataBaseService used to store Trace Information.
FileServiceName; name of file Service to store Exception Information, in case Trace message is bigger than 32ko (yes, it happens...)

# 3 - Use Trace

```
Context.Trace("...");
```

