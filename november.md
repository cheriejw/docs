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

## ASP.NET

ASP in ASP.NET was a language. Classic ASP it is called; "ASP uses server-side scripting to generate content that is sent to the client's web browser. The ASP interpreter reads and executes all script code between <% and %> tags, the result of which is content generation. These scripts were written using VBScript, JScript, or PerlScript." [ASP.NET is a framework.](https://stackoverflow.com/questions/4208227/is-asp-net-a-scripting-language-or-a-framework)
