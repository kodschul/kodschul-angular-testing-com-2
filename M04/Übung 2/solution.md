# Lösungsvorschlag für Übung 2: Abfangen von Fehlern in Unit-Tests

## Lösung für die Komponente: ProductServiceComponent

### Korrigierter Code
Der Fehler in der Komponente lag im Umgang mit dem Fehlerobjekt (`err`) im `subscribe`-Callback. Um die Fehlermeldung korrekt anzuzeigen, muss der Zugriff auf die Fehlermeldung angepasst werden.

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
        (err) => this.error = err.error?.message || 'Unknown error' // Korrektur: Zugriff auf die Fehlermeldung angepasst
      );
  }
}
```

## Unit-Tests für die korrigierte Komponente
### Anpassung der Tests
Die Tests bleiben größtenteils gleich, allerdings sollten sie nun ohne Anpassung funktionieren, da die Komponente korrekt implementiert ist.

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
    productServiceMock.getProducts.and.returnValue(throwError({ error: { message: 'API error' } })); // Fehler korrekt simuliert
    component.ngOnInit();
    fixture.detectChanges();
    const compiled = fixture.nativeElement;
    expect(compiled.querySelector('p').textContent).toContain('Error loading products: API error');
  });
});

```