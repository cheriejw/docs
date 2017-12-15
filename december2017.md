## .NET

http://www.c-sharpcorner.com/UploadFile/d6fefe/delegate-anonymous-function-and-lambda-expression-in-C-Sharp/

http://www.dotnetcurry.com/csharp/1193/csharp-constructor-types-interview-question

Initialize/Instanciate with `new Thing() {ThingsProp = x, ThingsProp2 = y};`

##### --- **12/13/2017** ---
Page_Load is called every action. Every postback?
Show is only called once, at beginning of page.

Set `EnableViewState` Property to true and it adjusted width to parent view.
Gets or sets a value indicating whether the server control persists its view state, and the view state of any child controls it contains, to the requesting client.(Inherited from Control.)

**Build Files**
Inside the project file / bin is where the built dll should be. The dll is what is served by IIS.
##### --- **12/12/2017** ---
[**Custom Components**](http://www.drdobbs.com/custom-components-in-aspnet-using-c/184401682)
aspx can have many ascx, like components.

`<%@ Register TagPrefix="uc1" TagName="Note" Src="Note.ascx" %>`
At the top of ascx. Using `<uc1:Note ID="ucNote" runat="server" EnableViewState="False" Singular="Transaction" Visible="false"></uc1:Note>` in code like a component. Component created in registered src file: `Note.ascx`.

Transalate what the following means architecturally:
`view/send alert = ECA.AlertLogControl (renders dgridand links, also async rendered) -> ECA.ViewAlert upon calling showAlert() -> calling ECS.Alert.EmailPurchaseRecipt() to "validate"
(which also sets the reciept) and sets typeof(PurchaseRecipt) which is where alertevent 28 came from, 2 is in EmailMultiCheckRecipt. -> ECS.Alert.EmailReciept with that alertevent 28, after filling recipt object calls ECA. which loads recipt and then on "//Generate Alert" checks recipttype(can only be multicheck or purchase) -> Uses ECAlert Alert obj with castings from guid to it and other object things... (havent explored much yet) -> back to ECS.Alert.EmailReciept -> back to ECA alertguid in session state if it can and ECA.ViewAlert will take guid to get reciept. : object alertEmailGuid = Session[emailReceiptGuid.ToString()];
hidEmailGuid.Value = emailReceiptGuid.ToString();
AlertEmail alertEmail = alertEmailGuid as AlertEmail;
if (alertEmail != null)
{
ShowEmailAlert(alertEmail.EmailMessage); //in same class
btnSend.Text = "Send";
}
`
**#FinTech**
> A remittance is a payment that gets sent somewhere else. If you get a bill in the mail, you will usually have at least a week to send your remittance. To "remit" is to send money or make a payment and what you send is called remittance.

##### --- **12/11/2017** ---
SqlDataAdapter.Fill(ds) make stored proceedure call.

>the as operator performs only reference conversions, nullable conversions, and boxing conversions.
 Boxing is the act of treating a value type as reference type (which in practice, involves copying the contents of that value type (from stack) to the heap and returning a reference to that object).
[ASP.NET COURSES](https://www.asp.net/freecourses)

[Async](https://docs.microsoft.com/en-us/dotnet/csharp/async)

[**Page Life Cycle**](https://msdn.microsoft.com/en-us/library/ms178472.aspx#login_control_events)
There is one cs file in the entire Page folder, named 'BasePage.cs' that inherits from `System.Web.UI.Page`. where the protected virtual void Page_Load method is with no references in my ascx file. The abstract ascx file that all the other pages inherit from inherits from `System.Web.UI.Control`.

[**Partial-Page Rendering**](https://www.codeproject.com/Tips/656031/How-to-enable-partial-rendering-with-the-AJAX-Upda)
Coworker said our page was async, so I looked up where this would be possible.
In ascx page we use [AJAX Update Panel](https://msdn.microsoft.com/en-us/library/cc295545.aspx) with `<asp:ScriptManager ID="smScriptManager" EnablePartialRendering="true" runat="server">` in the aspx we grab from. 

##### --- **12/1/2017** ---
**Data Layer**
While working on DataSets, code behind page couldn't find my new DataSets I had just made. The solution to this was removing the `Ds/DataSetNameDs.cs` file that was under the `DataSetNameDs` (file?) the .cs file had something like:
```c
namespace Admin.Db.Ds
{
}

namespace Admin.Db.Ds {
    public partial class DataSetNameDs {
    }
}
namespace Admin.Db.Ds {
    public partial class DataSetNameDs {
    }
}
```
I did not understand, but I left it there. Could not be finding dataset because it was looking into this name space and it is empty. After removal maybe it looks at the other DataSet files.

**Interpolated Strings**
Upgraded use of String.Format to interpolated strings that I found doing a tutorial.
```c++
ErrMsg = String.Format("Invalid Distribution Account: Your input '{0}' does not match validation rule '{1}' for type '{2}'.", acctNum, row.ValidationDescr, row.RemitDistributionTypeDescr);

ErrMsg = $"Invalid Distribution Account: Your input '{acctNum}' does not match validation rule '{row.ValidationDescr}' for type '{row.RemitDistributionTypeDescr}'.";
```
Easeier on the eyes.
