# Assignments

Tokens:
```
/\S*"[^"]*"|[^"\s]+/g
```

## String

```
/^([a-zA-Z0-9_]+)="([^"]*)"$/
```

## Bool and Int

```
/^([a-zA-Z0-9_]+)=([0-9]*|true|false)$/
```

## Variable

```
/^:([a-zA-Z0-9_]+)=(.+)$/
```

## Shorthand

```
/^:([a-zA-Z0-9_]+)$/
```
