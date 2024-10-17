# Lösung: Testen eines Datenservices mit einer funktionierenden API

## Lösungsvorschlag für die Aufgaben

### Setup
Die Testumgebung für den `ProductService` wird eingerichtet. Der `HttpClient` wird mit dem `HttpClientTestingModule` gemockt, um HTTP-Anfragen zu simulieren und zu testen, wie der Service auf verschiedene Antworten der API reagiert.

### Lösungscode

```typescript
// product.service.spec.ts
import { TestBed } from '@angular/core/testing';
import { HttpClientTestingModule, HttpTestingController } from '@angular/common/http/testing';
import { ProductService } from './product.service';

describe('ProductService', () => {
  let service: ProductService;
  let httpMock: HttpTestingController;

  beforeEach(() => {
    TestBed.configureTestingModule({
      imports: [HttpClientTestingModule],
      providers: [ProductService]
    });

    service = TestBed.inject(ProductService);
    httpMock = TestBed.inject(HttpTestingController);
  });

  afterEach(() => {
    httpMock.verify(); // Verifiziert, dass keine ungewollten Anfragen offen sind
  });

  // Testfall 1: Überprüfung der getProducts Methode bei erfolgreicher API-Antwort
  it('should return an array of products when the API call is successful', () => {
    const mockProducts = [
      { id: 1, name: 'Product 1', price: 100 },
      { id: 2, name: 'Product 2', price: 200 }
    ];

    service.getProducts().subscribe(products => {
      expect(products.length).toBe(2);
      expect(products).toEqual(mockProducts);
    });

    const req = httpMock.expectOne('https://fakestoreapi.com/products');
    expect(req.request.method).toBe('GET');
    req.flush(mockProducts);
  });

  // Testfall 2: Überprüfung der getProducts Methode bei einer Fehlerantwort der API
  it('should return an error message when the API call fails with 404', () => {
    service.getProducts().subscribe(
      () => fail('should have failed with a 404 status'),
      (error) => {
        expect(error).toBe('Error fetching products, please try again later.');
      }
    );

    const req = httpMock.expectOne('https://fakestoreapi.com/products');
    req.flush('Error message', { status: 404, statusText: 'Not Found' });
  });

  // Testfall 3: Überprüfung der getProducts Methode bei einem leeren API-Response
  it('should return an empty array when the API response is empty', () => {
    service.getProducts().subscribe(products => {
      expect(products.length).toBe(0);
    });

    const req = httpMock.expectOne('https://fakestoreapi.com/products');
    req.flush([]); // Leere Antwort
  });
});
