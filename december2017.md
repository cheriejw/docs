## .NET
##### --- **12/11/2017** ---
[ASP.NET COURSES](https://www.asp.net/freecourses)

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