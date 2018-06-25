# Description
Poseidon message component contains modal and toast messages. It is controlled by the [Message Service](https://kognifai.visualstudio.com/Kognifai%20Core/_wiki/wikis/PoseidonNext.wiki?wikiVersion=GBwikiMaster&pagePath=%2FPoseidon%20Next%2FPublic%20documentation%2FSDK%20reference%2FMessage%20Service)
# Usage
The component is standard Angular component inside its own module. It has to be added to application's main page.
- package.json
```json
{
  "dependencies": {
    "@kognifai/poseidon-message-service": "~2.0.0-rc.0",
  }
}
```
- message.module.ts
```typescript
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';
import { MessageService } from '@kognifai/poseidon-message-service';
import { MessageComponent } from './message.component';

@NgModule({
  declarations: [
    MessageComponent
  ],
  imports: [
    CommonModule,
    FormsModule
  ],
  providers: [MessageService],
  exports: [MessageComponent]
})
export class MessageModule { }

```
- main.component.html
```html
<app-message></app-message>
```