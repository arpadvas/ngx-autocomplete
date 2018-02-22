# @avas/NgxAutocomplete

Warning: This project is under development so is not ready for production.

## Feautures

HTTPClient support
Reactive form support
Static array and API call support
Highlight matches (case insensitive)
Keyboard support
AOT compatible

## Installation
```
npm install @avas/ngx-autocomplete --save
```

## Inputs

* **type**<_string_> - The input field type (text be default).
* **placeholder**<_string_> - The input field placeholder.
* **apiString**<_string_> - API URL to be called.
* **paramName**<_string_> - The keyword string will be attached as query string parameter with the given name.
* **suggestionPropName**<_string_> - By default the response coming from the API is handled as an array of string. If suggestionPropName is provided then response will be handled as an array of objects and the given property will be mapped.
* **payloadPropName**<_string_> - The property name of the response payload. If not provided then the response will be handled as the payload itself.
* **staticDataSource**<_any[]_> - Array of string or objects. If second then suggestionPropName must be provided.
* **control**<FormControl> - The ngx-autocomplete selector must be part of a reactive form.

## Usage

First import NgxAutocompleteModule to your module:

```typescript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { NgxAutocompleteModule } from './ngx-autocomplete/ngx-autocomplete.module';
import { FormsModule, ReactiveFormsModule } from '@angular/forms';
import { HttpClientModule } from '@angular/common/http';


@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    HttpClientModule,
    FormsModule,
    ReactiveFormsModule,
    NgxAutocompleteModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

```typescript
import { Component } from '@angular/core';
import { FormGroup, FormBuilder } from '@angular/forms';

export class AppComponent {

  myForm: FormGroup;
  weekdays: any[] = [
    {
      name: 'Monday'
    },
    {
      name: 'Tuesday'
    },
    {
      name: 'wednesday'
    }
  ];

  constructor(
    private formBuilder: FormBuilder
  ) {
    this.createForm();
  }

  createForm() {
    this.myForm = this.formBuilder.group({
      keyword: ''
       });
  }

}
```

with static array source:
```html
<form [formGroup]="myForm">
  <ngx-autocomplete formControlName="keyword"
                    [control]="myForm.controls.keyword"
                    [staticDataSource]="weekdays"
                    suggestionPropName="name"></ngx-autocomplete>
</form>
```

with API call:
```html

<form [formGroup]="myForm">
  <ngx-autocomplete formControlName="keyword"
                    [control]="myForm.controls.keyword"
                    apiString="http://localhost:3000/api/ascent/queryascents"
                    paramName="keyword"
                    payloadPropName="payload"
                    suggestionPropName="name"></ngx-autocomplete>
</form>
```

## Override built-in styles

Use ::ng-deep selector to override built-in element or class styles. For example:

```css
ngx-autocomplete ::ng-deep input {
     /* your style comes here */
}
```
```css
ngx-autocomplete ::ng-deep .highlighted {
    /* your style comes here */
}
```

