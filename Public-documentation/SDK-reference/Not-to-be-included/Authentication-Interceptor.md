# Description
The authentication interceptor uses the [```Authentication service```](https://kognifai.visualstudio.com/PoseidonNext/_wiki/wikis/PoseidonNext.wiki?wikiVersion=GBwikiMaster&pagePath=%2FPoseidon%20Next%2FSDK%20documentation%2FAuthentication%20Service) the get the access token of the user, after which it attaches it to the header of the http request.

# Usage
```typescript
public intercept(req: HttpRequest<any>, next: HttpHandler): Observable<HttpEvent<any>>;
```