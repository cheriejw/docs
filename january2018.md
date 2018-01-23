## **Any programming language of course serves two goals:**
- Provide instructions to the computer.
- Leave a record of the intentions of the programmer.
---

## Java
[Switch with String](https://stackoverflow.com/questions/338206/why-cant-i-switch-on-a-string?rq=1)

## C#
[C#, .NET, ASP.NET](https://softwareengineering.stackexchange.com/questions/44810/relationship-between-c-net-asp-asp-net-etc)
>Though C# as a language was originally developed at Microsoft as part of .NET Framework, it was later standardised by ECMA, meaning that independent standard-compliant implementations of the language can be developed, and indeed they were. The most prominent of those is Mono.

[Switch Statement Fallthrough in C# Language Design](https://stackoverflow.com/questions/174155/switch-statement-fallthrough-in-c)
>**In summary therefore:**
-- C# no longer relates to unoptimised compiler output as directly as C code did 40 years ago (nor does C these days), which makes one of the inspirations of fall-through irrelevant.
-- C# remains compatible with C in not just having implicit break, for easier learning of the language by those familiar with similar languages, and easier porting.
-- C# removes a possible source of bugs or misunderstood code that has been well-documented as causing problems for the last four decades.
-- C# makes existing best-practice with C (document fall through) enforceable by the compiler.
-- C# makes the unusual case the one with more explicit code, the usual case the one with the code one just writes automatically.
-- C# uses the same goto-based approach for hitting the same block from different case labels as is used in C. It just generalises it to some other cases.
-- C# makes that goto-based approach more convenient, and clearer, than it is in C, by allowing  case statements to act as labels.-
**All in all, a pretty reasonable design decision**



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
