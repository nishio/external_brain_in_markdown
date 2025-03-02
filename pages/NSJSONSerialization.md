
:

```
    NSString* jsonPath = @"/Users/nishio/Dropbox/lacaille.json";
    NSData *data = [NSData dataWithContentsOfFile:jsonPath]; 
    NSError *error = nil;
    id json = [NSJSONSerialization JSONObjectWithData:data
                                              options:kNilOptions
                                                error:&error];
```


![image](https://gyazo.com/2e10fc31dfcbda29626d139d326dd975/thumb/1000)

[[ObjectiveC]]
[[JSON]]
