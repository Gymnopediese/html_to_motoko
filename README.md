# Transform a html folder to a motoko folder
## command
`python main.py -s/--source <html folder> -d/--destination <motoko root>`
This will generate a folder with all the files converted to .mo.
## function
In the destination, in the file `__html__.mo` the following function is accessible :
``` mo
public func http_request(request : Request) : Response
```
## main.mo
Add the following to your main.mo in order for it to work :
``` mo
import Frontend "your/path/__html__.mo"
...
public query func http_request(request : Frontend.Request) : async Frontend.Response {
    return Frontend.http_request(request);
};
```
## main.mo ++
This code takes the response and modify it :
``` mo
public query func http_request(_request : Frontend.Request) : async Frontend.Response {

        var response : Frontend.Response = Frontend.http_request(_request);

        if (Text.contains(response.headers[0].1, #text "text")) {
            let text = Text.decodeUtf8(response.body);
            return switch text {
                case null response;
                case (?val) ({
                        body = Text.encodeUtf8(Replace.replace(val, name, Time.now() - birth));
                        headers = response.headers;
                        status_code = response.status_code;
                    });
            };
        };
        return response;
    };
```
My Replace.replace function will replace all the occurances of `__NAME__` and `__AGE__` with `name` and `Time.now() - birth` thus making my html code more dynamic
