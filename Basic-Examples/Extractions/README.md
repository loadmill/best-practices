# Working with parameters
Working with parameters is the best practice recommended. When a flow is created, extracting parameters allows you to apply correlations between requests i.e. a certain value from one request's response can be extracted and used in the next ones.

## Extracting parameters
Consider an extraction field as a small code editor, so its not only that you can assign static values to it i.e. `param = foo` but you can also use functions and math operations to get the wanted value i.e. `param = func()`. 

## Notes
- When using math operations (`+`, `-`, `*`, `/`), surrounding the operator by space is required
> `__add('1' + '1')`,  ~`__add('1'+'1')`~
- When passing arguments to a function (`__func(arg1,arg2)`), it is not allowed to include spaces between the arguments.
> `__add(arg1,arg2)`, ~`__add(arg1, arg2)`~
- When using basic math operations, numbers should be surrounded by **single** quotes, not double.
> `__add('1' + '1')`, ~`__add("1" + "1")`~

- Global parameters are ones that are defined outside of the flows panel, under 'PARAMETERS'. They are global in the scope of the suite i.e every flow can use them **and modify them** as well.
> Modifying a global parameter will change it's value for all next flows as they are **global**. (...psst, you were using a global parameter this whole time inside the url of most of the requests)