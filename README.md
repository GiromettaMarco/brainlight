# Brainlight

Brainlight is a lightweight templating system with minimal logic pattern.

Brainlight is designed to be implemented with multiple languages while keeping the same template syntax.

```
{{&layout}}

{{$content}}

    <h4>{{author}}</h4>

    {{#author>books @ book}}
        <p>{{book>name}}</p>
    {{/#}}

    {{?author>url}}
        {{>links :url=author>url}}
    {{/?}}

{{/$}}
```

- [General rules](#general-rules)
- [Printing variables](#printing-variables)
- [Contextual variables](#contextual-variables)
- [Conditional statement](#conditional-statement)
- [For loop](#for-loop)
- [Foreach loop](#foreach-loop)
- [Inclusion](#inclusion)
- [Extension and Slots](#extension-and-slots)
- [Passing Variables](#passing-variables)
- [Advanced Inclusions and extensions](#advanced-inclusions-and-extensions)

## General rules

Brainlight is has a tag based syntax. Tags are delimited by double curly brackets: ```{{tag}}}```

In most cases, tag can be expressed with of without spaces: ```{{ tag }}}```

The suggested file extension for templates is ```.brain```

## Printing variables

```
{{name}}
```

The escaped variable tag parses a variable by converting special characters to HTML entities, than prints the result.

To print a value without escaping:

```
{{!name}}
```

## Contextual variables

```
{{book>genre>name}}
```

To access variables inside a context use the ```>``` symbol. A context could be an object or an associative array according to the language.

Contextual access can be used every time a tag makes reference to a variable.

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

## For loop

```
{{#count}}
    <p>{{index}}</p>
{{/#}}
```

A for loop statement prints the content between its tags N number of times, where N is the integer value of the variable passed.

Inside the loop an ```index``` variable contains the current iteration number.

For loops must be closed with the ```{{/#}}``` tag.

### Foreach loop

```
{{#array @ key>value}}
    <p>{{key}} => {{value}}</p>
{{/#}}
```

When a loop tag contains an ```@``` clause, it is considered to be a foreach loop.

The first argument must be an array or an iterable object, according to the language practice. The content between tags gets printed N number of times, where N is the array size.

The ```@``` clause could be expressed in the form of ```@ value``` or ```@ key>value```, which makes the value or key and value of the current array element accessible inside the loop.

Foreach loops must be closed with the ```{{/#}}``` tag.

## Inclusion

```
{{>partial}}
```

The inclusion tag includes the contents of another template inside the current one.

The included template is identified by its name and dot notation can be used to access templates in sub directories:

```
{{>directory.partial}}
```

## Extension and Slots

```
{{&parent}}
{{$slot}}
    <p>Content for parent.brain</p>
{{/$}}
```

The extension tag ```{{&parent}}``` sets up a template extension. This tag identifies a template the same way as the inclusion tag.

The slot tag ```{{$slot}}``` creates a new variable with the content between tags as its value. This variable can be accessed by the extended template.

parent.brain:
```
{{!slot}}
```

A slot must be closed with the ```{{/$}}``` tag.

## Passing variables

While performing an inclusion or an extension, variables can be passed with an HTML attribute like syntax.

### Hard-coded string

```
{{>partial name="Alice"}}
```

### Booleans and integers

```
{{>partial age=25 present=true}}
```

### Variable renaming

```
{{>partial :name=student>name}}
```

### Shorthand

```
{{>partial :name}}
```

Passes a variable directly at the same way as:

```
{{>partial :name=name}}
```

## Advanced inclusions and extensions

```
{{&+parent}}
{{$slot}}
    {{>+partial}}
{{/$}}
```

When the language supports it, templates can be referenced with additional logic using the ```{{>+}}``` (advanced inclusion) and ```{{&+}}``` (advanced extension) tags.

## License

Brainlight is open-sourced software licensed under the [MIT license](http://opensource.org/licenses/MIT)
