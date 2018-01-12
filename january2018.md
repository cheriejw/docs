
## C#
[C# Colon](https://stackoverflow.com/questions/17034475/in-c-sharp-what-category-does-the-colon-fall-into-and-what-does-it-really)
```CS
Console.WriteLine(value: "Foo"); 
//prints Foo
Console.WriteLine(vale: "Foo");
//Error(s): (15:31) The best overload for 'WriteLine' does not have a parameter named 'vale'
```

[Datagrid, ItemDataBound, access selected.](https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.datagrid.itemdatabound(v=vs.110).aspx)
## SQL

##### --- **1/8/2018** ---
> Dates are inefficient, going by topic now.

##### --- **1/5/2018** ---
> The moral of the story is ASMX is simple and because it is simple, it isn’t very powerful.  Take the time to learn about WCF because this is the future of the .Net platform, thus it will be time wisely spent.
[WCF VS ASMX](http://keithelder.net/2008/10/17/wcf-vs-asmx-webservices/)
[S.O.](https://stackoverflow.com/questions/2448472/what-are-the-differences-between-wcf-and-asmx-web-services)

ASMX is:
- easy and simple to write and configure
- only available in IIS
- only callable from HTTP

WCF can be:
- hosted in IIS, a Windows Service, a Winforms application, a console app - you have total freedom
- used with HTTP (REST and SOAP), TCP/IP, MSMQ and many more protocols