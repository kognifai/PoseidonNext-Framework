# Sample usage

Below are the usages of Message Service.

```ts
import { NgModule } from '@angular/core';
import { CommonModule } from '@angular/common';
import { FormsModule } from '@angular/forms';
import { RouterModule, Routes } from '@angular/router';

import { MessageTestComponent } from './messageTest.component';
import { MessageService } from '@kognifai/poseidon-message-service';

const routes: Routes = [
  { path: '', component: MessageTestComponent }
];

@NgModule({
  declarations: [
    MessageTestComponent
  ],
  imports: [
    CommonModule,
    FormsModule,
    RouterModule.forChild(routes)
  ],
  exports: [MessageTestComponent],
  providers: [MessageService]
})
export class MessageTestModule { }

```

And its component as follows

```ts
import { Component } from '@angular/core';
import { MessageModule } from '@kognifai/poseidon-ng-message-component';
import { MessageService } from '@kognifai/poseidon-message-service';

@Component({
  selector: 'app-message-service-test-page',
  templateUrl: './messageTest.component.html',
  styleUrls: ['./messageTest.component.css']
})
export class MessageTestComponent {
  constructor(private messageservice: MessageService) { }

  info() {
    /** Method call with modalbody, title, no default callback and custom buttons */
    this.messageservice.info('I am an information message', 'Information', '', [{
      caption: 'Yes',
      callback: () => {
        alert('I am a callback function ');
      }
    },
    {
      caption: 'No',
      callback: this.sampleCallback
    }
    ]);
  }

  success() {
    /** Method call with modalbody, title,  callback and one custom button */
    this.messageservice.success('I am a success message', 'Success', this.sampleCallback, [
      {
        caption: 'Yes',
        callback: () => {
          alert('I am a callback');
        }
      }
    ]);
  }
  error() {
    /** Method call with modalbody, no title, no default callback and custom buttons */
    this.messageservice.error('I am an error message', '', '', [{
      caption: 'Yes',
      callback: () => {
        alert('I am a callback');
      }
    },
    ]);
  }
  warning() {
    /** Method call with modalbody */
    this.messageservice.warning('I am a warning message');
  }
  toastSuccess() {
    /** Toaster with body only */
    this.messageservice.toastSuccess('I am a success notification');
  }
  toastInfo() {
    /** Toaster with body, title and timeout */
    this.messageservice.toastInfo('I am an information notification', 'Information', 20000);
  }
  toastError() {
    /** Toaster with body and title */
    this.messageservice.toastError('I am an error notification', 'Error');
  }
  toastWarning() {
    /** Toaster with body title and overridden timeout */
    this.messageservice.toastWarning('I am a warning notification', 'Warning', 20000);
  }
  /** The below method is  for demonstrating callbacks only */
  sampleCallback() {
    alert('I am a callback');
  }
}

```