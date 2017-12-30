## .NET
https://www.hanselman.com/blog/WhatNETDevelopersOughtToKnowToStartIn2017.aspx
http://www.hanselman.com/blog/WhatGreatNETDevelopersOughtToKnowMoreNETInterviewQuestions.aspx

http://dotnetpattern.com/threading-interview-questions-series-part-1

https://softwareengineering.stackexchange.com/questions/95212/when-to-favor-asp-net-webforms-over-mvc

http://dapper-tutorial.net/result-multi-mapping

## SQL
[Aggregate vs Analytic Functions](https://my.vertica.com/docs/7.2.x/HTML/index.htm#Authoring/AnalyzingData/SQLAnalytics/AnalyticFunctionsVersusAggregateFunctions.htm)
[Vector vs Scalar](http://infocenter.sybase.com/help/index.jsp?topic=/com.sybase.infocenter.dc32300.1570/html/sqlug/sqlug639.htm)
[RANK() OVER](https://www.techonthenet.com/oracle/functions/rank.php)
>Aggregate functions can be applied to all the rows in a table, in which case they produce a single value, a scalar aggregate. They can also be applied to all the rows that have the same value in a specified column or expression (using the group by and, optionally, the having clause), in which case, they produce a value for each group, a vector aggregate. The results of the aggregate functions are shown as new columns.

**Default constructor or oject initializer!**
https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/classes-and-structs/how-to-initialize-objects-by-using-an-object-initializer

##### --- **12/29/2017** ---
>The only difference is that .HTM is used as an alternate to .HTML for some operating systems and servers that do not accept four-letter extensions.

[Session VS ViewState](https://stackoverflow.com/questions/2883149/viewstate-vs-session-maintaining-object-through-page-lifecycle)
[Dynamically created controls and postback. (Rendering something new via event handler.)](https://stackoverflow.com/questions/4216329/asp-net-dynamically-created-controls-and-postback)

##### --- **12/21/2017** ---
>The virtual keyword is used to modify a method, property, indexer, or event declaration and allow for it to be overridden in a derived class. 

https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/out
https://stackoverflow.com/questions/5995317/how-to-convert-c-sharp-nullable-int-to-int
`v2 = v1 ?? default(int);`
https://stackoverflow.com/questions/585859/what-is-the-difference-between-protected-and-protected-internal
- protected:
The type or member can be accessed only by code in the same class or struct, or in a class that is derived from that class.

- internal:
The type or member can be accessed by any code in the same assembly, but not from another assembly.

sqlDa.Fill(ds, ds.AlertTemplatePreview.TableName); only worked when I named the Ds table a different name on the designer. I.e. when i named it AlertTemplatePreviewDs it didn't even work wiht ds, ds.AlertTemplatePreviewDs... odd.

https://stackoverflow.com/questions/585859/what-is-the-difference-between-protected-and-protected-internal

##### --- **12/15/2017** ---
**DataSet**
Goes in order it is put in. Column names don't really matter, which is why the column was wrong last time.

**NULLABLE TYPE?**
https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/nullable-types/how-to-identify-a-nullable-type

**Async**
https://forums.asp.net/t/1230943.aspx?The+Update+method+can+only+be+called+on+UpdatePanel+with+ID+UpdatePanel1+before+Render
>I can see clearly the problem in your code. You are using async operation (in this case BeginGetResponse) which will not block main thread while the operation is in progress. This means Page lifecycle will continue to progress, it will even render the results and quit BEFORE you will get the response from remote web server, and it's logical that calling UpdatePanel1.Update at this point will throw an exception.
The approach you chose to not to block (freeze) UI while calling remote server will not work anyway, because it only makes sense to use this approach in ASP.NET if you have several - 2 or more simultaneous time-expensive operations to perform(let's say two or more calls to remote server). You anyway will have to wait untill call completes and freeze the main thread untill that.
What will happen if main thread renders the response and calls it to browser before completeon of async operation? Nothing - rendered page can not be re-rendered or undone - it will already be sent over TCP network to internet and will exist in form of thousand of TCP packets.
I think to achieve what you want to do - you should implement the following model: 1) first of all you will have to make more than one AJAX call to the server - first to launch BeginGetResponse of WebRequest object, and second request to retrieve the results. 2) second request may be done on every time interval (reoccuring) - this is known as polling model. 3) results of async operation can be stored in some persistense medium - for example in database, or XML file.
I would recommend to look at my blog post about the exactly what you want to achieve, you can see it here : [Displaying Progress Bar for Long-Running Processes on Server using ASP.NET AJAX](http://blog.devarchive.net/2008/01/displaying-progress-bar-for-long.html)

**Injecting Javascript**
Took me forever to get the right script. I'm noob.
```java
public void Refresh_Click(object sender, EventArgs e)
{
    ScriptManager.RegisterClientScriptBlock(Page, GetType(), "script", "document.getElementById('" + lnkRefresh.ClientID + "').style.visibility = 'hidden'; window.setTimeout(function() { document.getElementById('" + lnkRefresh.ClientID + "').style.visibility = '' },2000);", true);
    LoadAndBindRdeLogFromViewState();
    uPanelRdeLog.Update();
}
```

**Used a Property (Tried)**
``` java
private System.Timers.Timer RefreshTimer
{
    get
    {
        System.Timers.Timer refreshTimer = new System.Timers.Timer(5000) { Enabled = false, AutoReset = false };
        refreshTimer.Elapsed += (Object src, System.Timers.ElapsedEventArgs eea) => { lnkRefresh.Visible = true; uPanelAlertLog.Update(); };
        return refreshTimer;
    }
}
```

[delegate, anons, lambdas](http://www.c-sharpcorner.com/UploadFile/d6fefe/delegate-anonymous-function-and-lambda-expression-in-C-Sharp/)

[constructor types](http://www.dotnetcurry.com/csharp/1193/csharp-constructor-types-interview-question)

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
