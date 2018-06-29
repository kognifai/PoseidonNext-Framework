# Description
The initialize service performs login, loads navigation items and does initial redirection for Poseidon applications. It should be invoked on app startup.
# Usage
## Contract
```typescript
export class InitializeService {
   public initialize(): Observable<void> { ... }
}
```
## Injecting
Initialize service is standard Angular service provided by Poseidon and can be used by injecting it into application services and components.
- package.json
```json
{
  "dependencies": {
    "@kognifai/poseidon-ng-initialize-service": "^2.0.0-beta.1",
  }
}
```
- app.module.ts
```typescript
import { InitializeService } from '@kognifai/poseidon-ng-initialize-service';
@NgModule({
  providers: [InitializeService]
})
export class AppModule {
```
- app.component.ts
```typescript
import { InitializeService } from '@kognifai/poseidon-ng-initialize-service';
@Component( ... )
export class AppComponent implements OnInit {
  constructor(private initializeService: InitializeService) { }
  public ngOnInit() {
    this.initializeService.initialize().subscribe(
      () => { /* next - shouldn't happen  */ },
      error => { console.log('Initialize error.'); },
      () => {
        // initialization finished
      }
    );
  }
}
```