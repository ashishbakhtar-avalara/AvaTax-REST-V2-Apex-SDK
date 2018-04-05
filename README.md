# AvaTax-REST-V2-Apex-SDK

This GitHub repository is the Salesforce (or Apex) SDK for Avalara's world-class tax service, AvaTax. It uses the AvaTax REST v2 API, which is a fully REST implementation and provides a single client for all AvaTax functionality. For more information about AvaTax REST v2, please visit Avalara's Developer Network or view the online Swagger documentation.

# Build Status

Beta Package is available

# Installing the Apex SDK

To Install AvaTax APEX REST v2 SDK 

• Copy the URL 

Production: https://login.salesforce.com/packaging/installPackage.apexp?p0=04t1I000003FBr1

SandBox : https://test.salesforce.com/packaging/installPackage.apexp?p0=04t1I000003FBr1

• Paste the URL in web browser and Login into your Salesforce Org that must have this package to install SDK for that environment.

• Install the Package by selecting appropriate User option. 


# Using the Apex SDK

The Apex SDK uses a fluent interface to define a connection to AvaTax and to make API calls to calculate tax on transactions. Here's an example of how to connect to AvaTax in Apex:

```csharp
    public class Program
    {
    public void Main()
    {
        // Create a client and set up authentication
        AVA_SFREST.AvaTaxClient Client = new AVA_SFREST.AvaTaxClient("MyTestApp", "1.0", Environment.MachineName,   AvaTaxEnvironment.Sandbox)
            .WithSecurity("MyUsername", "MyPassword");
    
        // Verify that we can ping successfully
       AVA_SFREST.PingResultModel pingResult = Client.Ping();
       
        // Verify that we can ping successfully
        if(result.statusCode == 200 || result.statusCode == 201)
        {
        ApexPages.addmessage(new ApexPages.message(ApexPages.severity.SUCCESS,'Connected to AvaTax'));
        }
     }
    }
```
