## .NET
**Data Layer -- 12/1/2017**
While working on DataSets, code behind page couldn't find my new DataSets I had just made. The solution to this was removing the `Ds/DataSetNameDs.cs` file that was under the `DataSetNameDs` (file?) the .cs file had something like:
```c
namespace Ensenta.Admin.Db.Ds
{
}

namespace Ensenta.Admin.Db.Ds {
    
    
    public partial class RemitFieldSummaryDs {
    }
}
namespace Ensenta.Admin.Db.Ds {
    
    
    public partial class RemitFieldSummaryDs {
    }
}
```
I did not understand, but I left it there. Could not be finding dataset because it was looking into this name space and it is empty. After removal maybe it looks at the other DataSet files.