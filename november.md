### Microservices vs Monolithic
Found [this Youtube video](https://www.youtube.com/watch?v=oRIYtOsAlzkv) covering Microservice vs Monolithic architectechture pretty well. It refers to back-end.

### Javascript
Something a coworker had trouble with, caused a syntax error when he was trying to utilize ES6 destructuring. Found from [these](https://hacks.mozilla.org/2015/05/es6-in-depth-destructuring/) [sources](http://exploringjs.com/es6/ch_destructuring.html).
```javascript
const test= { test1:'dfjlakj', test2:'fsdfs', test3:'dsfasf'};
var test1, test2, test3;

//{test1, test2, test3} = test
({test1, test2, test3} = test)

console.log('HELLO', test1, test2, test3); //HELLO dfjlakj fsdfs dsfasf
```
> This happens because the JavaScript grammar tells the engine to parse any statement starting with { as a block statement (for example, { console } is a valid block statement). The solution is to either wrap the whole expression in parentheses: ({ safe } = {});

Also found this [nifty ES6 repl.](https://es6console.com/ja0e4m0i/)

### Journal
While exploring more of the company's c# code base... which making a page consists if 3 steps. Making a DataSet object, going to our datalayer which consists of methods that essencially call stored proceedures to put into out DataSet objects to make one of such methods, and making the webform usercontrol that inherits from a base class. the base class implements a lifecycle for the page to render.

while doing the markup portion of the usercontrol i https://msdn.microsoft.com/en-us/library/system.web.ui.webcontrols.boundcolumn(v=vs.110).aspx looked up a few things. i wanted to know what style options i could have for the itemstyle. datagrid class has itemstyle property. the tag names are called elements... with.. the props.. which are... ATTRIBUTES. attributes are also the methods in teh square brackets... that  https://docs.microsoft.com/en-us/dotnet/csharp/programming-guide/concepts/attributes/
SQL parameters use @. more into the datalayer which is why variables are camelcased when coworks blindly name. sql namiv ocnvention tour namig convention.. for c#

## ASP.NET

Today I learned that ASP in ASP.NET was a language. Classiac ASP it is called; "ASP uses server-side scripting to generate content that is sent to the client's web browser. The ASP interpreter reads and executes all script code between <% and %> tags, the result of which is content generation. These scripts were written using VBScript, JScript, or PerlScript." [ASP.NET is a framework.] (https://stackoverflow.com/questions/4208227/is-asp-net-a-scripting-language-or-a-framework)
