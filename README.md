# Transform a html folder to a motoko folder
## command
`python main.py -s <html folder> <motoko root>`
## function
in the target root, in the file `__html__.mo` the following function is accessible :
``` mo
public func http_request(request : Request) : Response
```
add the following to your main in order for it to work :
``` mo
import Frontend "your/path/__html__.mo"
...
public query func http_request(request : Frontend.Request) : async Frontend.Response {
    return Frontend.http_request(request);
};
```

