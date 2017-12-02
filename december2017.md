## .NET
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