
# Angular Testing und Debugging Schulung

## Themen

1. Erstellen einer neuen Komponente
2. Schreiben einer Fehlerbehandlungsklasse
3. Implementierung von Abhängigkeitsinjektionen

## 1. Erstellen einer neuen Komponente

### Live Coding Beispiel

```bash
ng generate component MyNewComponent
```

In der Datei `my-new-component.component.ts`:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-my-new-component',
  template: '<p>My new component works!</p>'
})
export class MyNewComponent {}
```

**Test:**

```typescript
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { MyNewComponent } from './my-new-component.component';

describe('MyNewComponent', () => {
  let component: MyNewComponent;
  let fixture: ComponentFixture<MyNewComponent>;

  beforeEach(() => {
    TestBed.configureTestingModule({
      declarations: [MyNewComponent]
    }).compileComponents();

    fixture = TestBed.createComponent(MyNewComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });

  it('should create', () => {
    expect(component).toBeTruthy();
  });
});
```

## 2. Schreiben einer Fehlerbehandlungsklasse

### Live Coding Beispiel

In der Datei `error-handler.service.ts`:

```typescript
import { ErrorHandler, Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root',
})
export class GlobalErrorHandler implements ErrorHandler {
  handleError(error: any): void {
    console.error('An error occurred:', error);
    // Weitere Fehlerbehandlung hier
  }
}
```

**Test:**

```typescript
import { TestBed } from '@angular/core/testing';
import { GlobalErrorHandler } from './error-handler.service';

describe('GlobalErrorHandler', () => {
  let service: GlobalErrorHandler;

  beforeEach(() => {
    TestBed.configureTestingModule({
      providers: [GlobalErrorHandler],
    });
    service = TestBed.inject(GlobalErrorHandler);
  });

  it('should handle errors', () => {
    spyOn(console, 'error');
    const error = new Error('Test Error');
    service.handleError(error);
    expect(console.error).toHaveBeenCalledWith('An error occurred:', error);
  });
});
```

## 3. Implementierung von Abhängigkeitsinjektionen

### Live Coding Beispiel

In der Datei `my-service.service.ts`:

```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class MyService {
  getData(): string {
    return 'Service Data';
  }
}
```

In der Datei `my-component.component.ts`:

```typescript
import { Component } from '@angular/core';
import { MyService } from './my-service.service';

@Component({
  selector: 'app-my-component',
  template: '<p>{{ data }}</p>'
})
export class MyComponent {
  data: string;

  constructor(private myService: MyService) {
    this.data = this.myService.getData();
  }
}
```

**Test:**

```typescript
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { MyComponent } from './my-component.component';
import { MyService } from './my-service.service';

describe('MyComponent', () => {
  let component: MyComponent;
  let fixture: ComponentFixture<MyComponent>;
  let myService: MyService;

  beforeEach(() => {
    const myServiceMock = {
      getData: () => 'Mocked Service Data'
    };

    TestBed.configureTestingModule({
      declarations: [MyComponent],
      providers: [{ provide: MyService, useValue: myServiceMock }]
    }).compileComponents();

    fixture = TestBed.createComponent(MyComponent);
    component = fixture.componentInstance;
    myService = TestBed.inject(MyService);
    fixture.detectChanges();
  });

  it('should create and display service data', () => {
    expect(component).toBeTruthy();
    expect(component.data).toBe('Mocked Service Data');
  });
});
```