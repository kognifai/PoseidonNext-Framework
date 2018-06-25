# Description
The cookie service provides methods to get, set and delete browser cookies.
# Usage
## Contract
```typescript
export class CookieService {
    public setCookie(name: string, value: string, days: number): void { ... }
    public getCookie(name: string): string { ... }
    public deleteCookie(name: string): void { ... }
}
```
## Injecting
Cookies service is standard JS service provided by Poseidon and can be used by injecting it into application services and components.
- package.json
```json
{
  "dependencies": {
    "@kognifai/poseidon-cookieservice": "^2.0.0"
  }
}
```
- app.module.ts
```typescript
import { CookieService } from '@kognifai/poseidon-cookieservice';
@NgModule({
  providers: [
    CookieService
  ]
})
export class AppModule {
```
- my.component.ts
```typescript
import { CookieService } from '@kognifai/poseidon-cookieservice';
@Component( ... )
export class MyComponent {
  constructor(private cookieService: CookieService) {
    this.cookieService.setCookie('cookieName', 'value', 3);
    let value: string = this.cookieService.getCookie('cookieName');
    this.cookieService.deleteCookie('cookieName');
  }
}
```