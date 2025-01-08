# Cuis-Smalltalk-URI

See also <https://codeberg.org/auverlot/Cuis-Smalltalk-URI>.

## Construction

```smalltalk
| uri |
uri := URI new
    scheme: #https;
    userinfo: 'john:1234';
    host: 'www.domain.com';
    port: 8080;
    path: '/folder/file';
    query: {'id' -> 42. 'name' -> 'john.doe'};
    fragment: 'row=1';
    yourself.
uri asString "https://john:1234@www.domain.com:8080/folder/file?id=42&name=john.doe#row=1"
```

## Parsing

```smalltalk
| uri |
uri := URI fromString: 'https://john:1234@www.domain.com:8080/folder/file?id=42&name=john.doe#row=1'.
uri scheme. "#https"
uri username. "john"
uri password. "1234"
uri host. "www.domain.com"
uri port. "8080"
uri path asString. "/folder/file"
uri query. "id=42&name=john.doe"
uri fragment "row=1"
```

## Query Dictionaries

```smalltalk
| uri query |
uri := URI fromString: 'https://john:1234@www.domain.com:8080/folder/file?id=42&name=john.doe#row=1'.
query := uri queryDictionary.
query at: 'id'. "42"
query at: 'name' "john.doe"
```

## Relative URIs

```smalltalk
| baseUri relativeUri targetUri |
baseUri := URI fromString: 'https://john:1234@www.domain.com:8080/folder/file?id=42&name=john.doe#row=1'.
relativeUri := URI fromString: 'anotherFile#row=2'.
targetUri := relativeUri relativeTo: baseUri.
targetUri asString "https://john:1234@www.domain.com:8080/folder/anotherFile#row=2"
```
