# Transform a html folder to a motoko folder
## command
`python main.py -s/--source <html folder> -d/--destination <motoko root>`
this will generate a folder with all the files converted to .mo 
## function
in the destination, in the file `__html__.mo` the following function is accessible :
``` mo
public func http_request(request : Request) : Response
```
## main.mo
add the following to your main.mo in order for it to work :
``` mo
import Frontend "your/path/__html__.mo"
...
public query func http_request(request : Frontend.Request) : async Frontend.Response {
    return Frontend.http_request(request);
};
```

