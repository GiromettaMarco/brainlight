# Core

## Tokens

split:
```
/({{)\s*(.*?)\s*(}})/
```

### PHP

```php
preg_split('/({{)\s*(.*?)\s*(}})/', $string, -1, PREG_SPLIT_DELIM_CAPTURE | PREG_SPLIT_NO_EMPTY);
```

### JS

```js
string.split(/({{)\s*(.*?)\s*(}})/);
```

## Tags

```
/^(!|\?|\/\?|#|\/#|>|\$|\/\$|&|-)*\s*([\S\s]*)$/
```
