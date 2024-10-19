
# Angular Testing und Debugging Schulung - Unit-Tests und Observables

## Themen

1. Schreiben von Unit-Tests für verschiedene Dienste
2. Testen von Observables und deren Fehlerbehandlung

## 1. Schreiben von Unit-Tests für verschiedene Dienste

### Live Coding Beispiel

In der Datei `data.service.ts`:

```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class DataService {
  getData(): string {
    return 'Service Data';
  }
}
```

**Test:**

```typescript
import { TestBed } from '@angular/core/testing';
import { DataService } from './data.service';

describe('DataService', () => {
  let service: DataService;

  beforeEach(() => {
    TestBed.configureTestingModule({
      providers: [DataService]
    });
    service = TestBed.inject(DataService);
  });

  it('should be created', () => {
    expect(service).toBeTruthy();
  });

  it('should return data', () => {
    expect(service.getData()).toBe('Service Data');
  });
});
```

## 2. Testen von Observables und deren Fehlerbehandlung

### Live Coding Beispiel

In der Datei `observable-service.service.ts`:

```typescript
import { Injectable } from '@angular/core';
import { Observable, throwError, of } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class ObservableService {
  getObservableData(): Observable<string> {
    return of('Observable Data');
  }

  getObservableError(): Observable<never> {
    return throwError(() => new Error('Observable Error'));
  }
}
```

**Test:**

```typescript
import { TestBed } from '@angular/core/testing';
import { ObservableService } from './observable-service.service';
import { of, throwError } from 'rxjs';

describe('ObservableService', () => {
  let service: ObservableService;

  beforeEach(() => {
    TestBed.configureTestingModule({
      providers: [ObservableService]
    });
    service = TestBed.inject(ObservableService);
  });

  it('should return observable data', (done: DoneFn) => {
    service.getObservableData().subscribe({
      next: (data) => {
        expect(data).toBe('Observable Data');
        done();
      },
      error: done.fail
    });
  });

  it('should handle observable error', (done: DoneFn) => {
    service.getObservableError().subscribe({
      next: () => done.fail('Expected error, but got data'),
      error: (error) => {
        expect(error.message).toBe('Observable Error');
        done();
      }
    });
  });
});
```
