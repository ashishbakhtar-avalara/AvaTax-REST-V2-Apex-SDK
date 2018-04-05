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
    //Sample Method to Test The AvaTax Credential
    public void testConnection()
    {
        // Create a client and set up authentication
        AVA_SFREST.AvaTaxClient Client = new AVA_SFREST.AvaTaxClient('MyTestApp', '1.0', AVA_SFREST.Environment.MachineName, AVA_SFREST.AvaTaxEnvironment.Sandbox)
            .WithSecurity('MyUsername', 'MyPassword');

        // Verify that we can ping successfully
        AVA_SFREST.PingResultModel pingResult = Client.Ping();

        // Verify that we can ping successfully
        if (result.statusCode == 200 || result.statusCode == 201)
        {
            ApexPages.addmessage(new ApexPages.message(ApexPages.severity.SUCCESS, 'Connected to AvaTax'));
        }
    }
    
    
    //Sample Method to Calculate The Tax
    public void calculateTax()
    {
        // Create a client and set up authentication
        AVA_SFREST.AvaTaxClient Client = new AVA_SFREST.AvaTaxClient('MyTestApp', '1.0', AVA_SFREST.Environment.MachineName, AVA_SFREST.AvaTaxEnvironment.Sandbox)
            .WithSecurity('MyUsername', 'MyPassword');

        //Create an Instance of CreateTransactionModel
        AVA_SFREST.CreateTransactionModel getTaxRequest = new AVA_SFREST.CreateTransactionModel();
        
        //Fetch the GetTaxRequest
        getTaxRequest = createTaxRequest(); // custom method to Create Tax Request
       
        //Create a Simple Transaction
        AVA_SFREST.TransactionModel result = Client.CreateTransaction('Addresses',getTaxRequest);
      
        // Verify transaction creation 
        if (result.statusCode == 200 || result.statusCode == 201)
        {
            ApexPages.addmessage(new ApexPages.message(ApexPages.severity.SUCCESS, 'Transaction Created in AvaTax'));
        }
    }
    
    //Create Tax Request 
    public AVA_SFREST.CreateTransactionModel createTaxRequest()
    {
        //Create Instance of CreateTransactionModel
        AVA_SFREST.CreateTransactionModel getTaxRequest = new AVA_SFREST.CreateTransactionModel();
        
        //Create Instance of AddressModel
        AddressesModel addresses = new AddressesModel();
		
        //Create Instance of AddressLocationInfo
        AddressLocationInfo singleLocation = new AddressLocationInfo();
        singleLocation.line1 ='900 winslow way e';
        singleLocation.city ='BI';
        singleLocation.postalCode ='98100';
        singleLocation.region  ='WA';
        singleLocation.country ='US';
            
        //Create Instance of LineItemModel
        LineItemModel line = new LineItemModel();
        line.lineNumber ='1';    
        line.quantity = '1';
        line.amount = 100;
        
        //Create LineItemModel List
        List<LineItemModel> lineList = new List<LineItemModel>();
        lineList.add(line);   
        
        //Map Instance of AddressLocationInfo to AddressModel
        addresses.singleLocation = singleLocation;
        
        //Map Instance of Addresses to getTaxRequest
        getTaxRequest.addresses =addresses;

        //Map Instance of lineList to getTaxRequest
        getTaxRequest.lines =lineList;
        
	//Map the Type of Document
        getTaxRequest.type ='SalesInvoice';
        
	//Map the Document date
	getTaxRequest.documentDate =system.today();
	
	//Map the Customer Code
	getTaxRequest.customerCode ='abc';
        
	//Map the CompanyCode
	getTaxRequest.companyCode ='Default';
        
	//return instance of getTaxRequest
        return getTaxRequest;
	
    }
}
```
