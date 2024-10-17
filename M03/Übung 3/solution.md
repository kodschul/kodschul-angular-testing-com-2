# Lösung: Testen eines Bestellungsdienstes mit einer funktionierenden API

## Lösungsvorschlag für die Aufgaben

### Setup
Die Testumgebung für den `OrderService` wird eingerichtet. Der `HttpClient` wird mit dem `HttpClientTestingModule` gemockt, um HTTP-Anfragen zu simulieren und zu testen, wie der Service auf verschiedene Antworten der API reagiert.

### Lösungscode

```typescript
// order.service.spec.ts
import { TestBed } from '@angular/core/testing';
import { HttpClientTestingModule, HttpTestingController } from '@angular/common/http/testing';
import { OrderService } from './order.service';

describe('OrderService', () => {
  let service: OrderService;
  let httpMock: HttpTestingController;

  beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [HttpClientTestingModule],
      providers: [OrderService]
    });

    service = TestBed.inject(OrderService);
    httpMock = TestBed.inject(HttpTestingController);
  });

  afterEach(() => {
    httpMock.verify(); // Verifiziert, dass keine ungewollten Anfragen offen sind
  });

  // Testfall 1: Überprüfung der getOrderById Methode bei erfolgreicher API-Antwort
  it('should return an order when the API call is successful', () => {
    const mockOrder = { id: 1, product: 'Product 1', quantity: 2 };

    service.getOrderById(1).subscribe(order => {
      expect(order).toEqual(mockOrder);
    });

    const req = httpMock.expectOne('https://fakestoreapi.com/carts/1');
    expect(req.request.method).toBe('GET');
    req.flush(mockOrder);
  });

  // Testfall 2: Überprüfung der getOrderById Methode bei einer Fehlerantwort der API
  it('should return an error message when the API call fails with 500', () => {
    service.getOrderById(1).subscribe(
      () => fail('should have failed with a 500 status'),
      (error) => {
        expect(error).toBe('An error occurred while fetching the order.');
      }
    );

    const req = httpMock.expectOne('https://fakestoreapi.com/carts/1');
    req.flush('Error message', { status: 500, statusText: 'Server Error' });
  });

  // Testfall 3: Überprüfung der getOrderById Methode bei einer ungültigen Bestell-ID
  it('should return an error when the ID is invalid', () => {
    service.getOrderById(null).subscribe(
      () => fail('should have failed with an invalid ID'),
      (error) => {
        expect(error).toBe('Invalid order ID');
      }
    );
  });
});
