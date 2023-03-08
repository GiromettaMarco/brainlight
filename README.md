# Brainlight

Brainlight is a lightweight templating system with minimal logic pattern.

It is designed to be implemented with multiple languages while keeping the same template syntax.

Brainlight syntax is tag based and these are the rules of a Brainlight template:

- [General rules](#general-rules)
- [Escaped variable](#escaped-variable)
- [Unescaped variable](#unescaped-variable)
- [Contextual variable](#contextual-variable)
- [Conditional statement](#conditional-statement)
- [Loop statements](#loop-statements)
- [Inclusion](#inclusion)
- [Extension and Slots](#extension-and-slots)

## General rules

Brainlight tags are delimited by double curly brackets.

The suggested Brainlight template file extension is ```.brain```

## Escaped variable

```
{{name}}
```

The escaped variable tag parses a variable by converting special characters to HTML entities, than prints the result.

## Unescaped variable

```
{{!name}}
```

Prints a variable without HTML escaping.

## Contextual variable

```
{{context->name}}
```

Prints a variable inside a context such as an object or an associative array.

It can be expressed both in the escaped and unescaped form.

## Conditional statement

```
{{?name}}
    ...
{{/?}}
```

Checks whether the variable is set and evaluable as 'true'. In such case, prints the content between opening and closing tag.

The following values are considered to be not set or 'false':

- The boolean 'false'
- A number equivalent to 0
- A character or string equivalent to "0"
- An empty string
- An empty array
- Any 'undefined' or 'null' variable

A condition must be closed with the ```{{/?}}``` tag.

## Loop statements

Loop statements print the content between its tags N number of times. The behavior of the statement changes based on the type of variable passed.

### Iteration

```
{{#integer}}
    <p>{{index}}</p>
{{/#}}
```

If an integer gets passed, N is equal to the integer. Also, a new variable ```index``` is created with the current iteration from 0 to N - 1.

### Foreach

```
{{#array as value}}
    <p>{{value}}</p>
{{/#}}
```

If an array gets passed, N is equal to the size of the array. An 'as' clause my be specified to create a variable with the current array element inside the iteration.

Loops must be closed with the ```{{/#}}``` tag.

## Inclusion

```
{{>partial}}
```

Include the contents of another template inside the current one.

The included template is identified by its name and dot notation could be used to access templates in sub directories:

```
{{>directory.partial}}
```

Variables may be passed while making an inclusion. An HTML attribute like syntax passes an hard-coded string:

```
{{>partial name="Alice"}}
```

The ```:``` character causes the content of the attribute to be evaluated as a variable name:

```
{{>partial :name="firstName"}}
```

## Extension and Slots

```
{{&parent}}
{{$slot}}
    <p>Content for parent.brain</p>
{{/$}}
```

The extension tag ```{{&parent}}``` sets up a template extension. This tag identifies a template and passess variables the same way as the inclusion tag.

The slot tag ```{{$slot}}``` creates a new variable with the content between tags as its value. This variable can be accessed by the extended template.

parent.brain:
```
{{!slot}}
```

A slot must be closed with the ```{{/$}}``` tag.

## License

Brainlight is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)
