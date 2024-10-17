# Übung 2: Abfangen von Fehlern in Unit-Tests

## Ziel
Lerne, wie du Fehler abfängst und debuggen kannst, wenn Unit-Tests fehlschlagen. Der Fokus liegt auf dem Umgang mit asynchronen Operationen und möglichen Fehlerquellen.

## Kontext
Du arbeitest an einer Angular-Anwendung, die Produktdaten von einer externen API lädt. Es gibt bereits eine Komponente `ProductServiceComponent`, die den `ProductService` nutzt, um diese Daten anzuzeigen. Die Komponente enthält jedoch einen Fehler, der während der Tests gefunden werden muss.

## Aufgabenstellung

### Vorgefertigter Code (mit Fehler):
```typescript
import { Component, OnInit } from '@angular/core';
import { ProductService } from './product.service';

@Component({
  selector: 'app-product-service',
  template: \`
    <div *ngIf="products">
      <div *ngFor="let product of products">
        <p>{{ product.name }}: {{ product.price }} €</p>
      </div>
    </div>
    <p *ngIf="error">Error loading products: {{ error }}</p>
  \`
})
export class ProductServiceComponent implements OnInit {
  products: any;
  error: string | null = null;

  constructor(private productService: ProductService) {}

  ngOnInit() {
    this.productService.getProducts()
      .subscribe(
        (data) => this.products = data,
        (err) => this.error = err.message // Fehler: Falscher Zugriff auf die Fehlermeldung
      );
  }
}
```

### Vorgefertigter Testfall:

```typescript
import { TestBed, ComponentFixture } from '@angular/core/testing';
import { ProductServiceComponent } from './product-service.component';
import { ProductService } from './product.service';
import { of, throwError } from 'rxjs';

describe('ProductServiceComponent', () => {
  let component: ProductServiceComponent;
  let fixture: ComponentFixture<ProductServiceComponent>;
  let productServiceMock: any;

  beforeEach(() => {
    productServiceMock = {
      getProducts: jasmine.createSpy('getProducts').and.returnValue(of([{ name: 'Product 1', price: 10 }]))
    };

    TestBed.configureTestingModule({
      declarations: [ProductServiceComponent],
      providers: [
        { provide: ProductService, useValue: productServiceMock }
      ]
    });

    fixture = TestBed.createComponent(ProductServiceComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });

  it('should display products', () => {
    const compiled = fixture.nativeElement;
    expect(compiled.querySelector('p').textContent).toContain('Product 1: 10 €');
  });

  it('should display an error message when the service fails', () => {
    productServiceMock.getProducts.and.returnValue(throwError({ message: 'API error' }));
    component.ngOnInit();
    fixture.detectChanges();
    const compiled = fixture.nativeElement;
    expect(compiled.querySelector('p').textContent).toContain('Error loading products: API error');
  });
});

```

### Aufgabe
- Fehler identifizieren: Der zweite Test schlägt fehl, da die Fehlermeldung nicht wie erwartet angezeigt wird. Identifiziere den Fehler im Code und korrigiere ihn.
- Fehlerbehebung: Passe den Code in der Komponente so an, dass die Fehlermeldung korrekt verarbeitet wird.
- Überprüfe die Tests erneut: Führe die Tests erneut aus und stelle sicher, dass sie nun erfolgreich durchlaufen.