
# Angular Testing und Debugging Schulung - Pipes

## Themen

1. Schreiben von Unit-Tests für eine benutzerdefinierte Pipe
2. Verwendung von Angular TestBed für Komponenten-Tests

## 1. Schreiben von Unit-Tests für eine benutzerdefinierte Pipe

### Live Coding Beispiel

In der Datei `capitalize.pipe.ts`:

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'capitalize'
})
export class CapitalizePipe implements PipeTransform {
  transform(value: string): string {
    return value.charAt(0).toUpperCase() + value.slice(1);
  }
}
```

**Test:**

In der Datei `capitalize.pipe.spec.ts`:

```typescript
import { CapitalizePipe } from './capitalize.pipe';

describe('CapitalizePipe', () => {
  let pipe: CapitalizePipe;

  beforeEach(() => {
    pipe = new CapitalizePipe();
  });

  it('should capitalize the first letter of a string', () => {
    expect(pipe.transform('angular')).toBe('Angular');
  });

  it('should return an empty string if input is empty', () => {
    expect(pipe.transform('')).toBe('');
  });
});
```

## 2. Verwendung von Angular TestBed für Komponenten-Tests

### Live Coding Beispiel

In der Datei `my-pipe-test.component.ts`:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-my-pipe-test',
  template: '<p>{{ "angular" | capitalize }}</p>'
})
export class MyPipeTestComponent {}
```

In der Testdatei `my-pipe-test.component.spec.ts`:

```typescript
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { MyPipeTestComponent } from './my-pipe-test.component';
import { CapitalizePipe } from './capitalize.pipe';

describe('MyPipeTestComponent', () => {
  let component: MyPipeTestComponent;
  let fixture: ComponentFixture<MyPipeTestComponent>;

  beforeEach(() => {
    TestBed.configureTestingModule({
      declarations: [MyPipeTestComponent, CapitalizePipe]
    }).compileComponents();

    fixture = TestBed.createComponent(MyPipeTestComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });

  it('should create the component', () => {
    expect(component).toBeTruthy();
  });

  it('should render capitalized text', () => {
    const compiled = fixture.nativeElement;
    expect(compiled.querySelector('p').textContent).toBe('Angular');
  });
});
```