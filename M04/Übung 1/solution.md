# Lösungsvorschlag für Übung 1: Testen einer Pipe und einer benutzerdefinierten Komponente

## Lösung für die Pipe: CurrencyConverterPipe

### Code der Pipe
Die Pipe `CurrencyConverterPipe` konvertiert einen Betrag in Euro anhand eines Wechselkurses:

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'currencyConverter'
})
export class CurrencyConverterPipe implements PipeTransform {
  transform(value: number, rate: number): string {
    return `${(value * rate).toFixed(2)} €`;
  }
}
```

### Unit-Tests für die Pipe
Hier sind Unit-Tests, die sicherstellen, dass die Pipe korrekt funktioniert:

```typescript
import { CurrencyConverterPipe } from './currency-converter.pipe';

describe('CurrencyConverterPipe', () => {
  let pipe: CurrencyConverterPipe;

  beforeEach(() => {
    pipe = new CurrencyConverterPipe();
  });

  it('should convert 10 EUR to 11 USD when rate is 1.1', () => {
    expect(pipe.transform(10, 1.1)).toBe('11.00 €');
  });

  it('should convert 20 EUR to 22 USD when rate is 1.1', () => {
    expect(pipe.transform(20, 1.1)).toBe('22.00 €');
  });

  it('should handle zero as input value', () => {
    expect(pipe.transform(0, 1.1)).toBe('0.00 €');
  });
});

```

### Lösung für die Komponente: ProductListComponent
Die Komponente ProductListComponent zeigt eine Liste von Produkten und verwendet die CurrencyConverterPipe:

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-product-list',
  template: `
    <div *ngFor="let product of products">
      <p>{{ product.name }}: {{ product.price | currencyConverter: exchangeRate }}</p>
    </div>
  `
})
export class ProductListComponent {
  products = [
    { name: 'Product 1', price: 10 },
    { name: 'Product 2', price: 15 }
  ];
  exchangeRate = 1.1; // Wechselkurs Euro zu USD
}

```

### Unit-Tests für die Komponente
Hier sind Unit-Tests, die sicherstellen, dass die Komponente korrekt funktioniert und die Pipe richtig angewendet wird:

```typescript
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { ProductListComponent } from './product-list.component';
import { CurrencyConverterPipe } from './currency-converter.pipe';
import { By } from '@angular/platform-browser';

describe('ProductListComponent', () => {
  let component: ProductListComponent;
  let fixture: ComponentFixture<ProductListComponent>;

  beforeEach(() => {
    TestBed.configureTestingModule({
      declarations: [ProductListComponent, CurrencyConverterPipe]
    });

    fixture = TestBed.createComponent(ProductListComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });

  it('should display the products with converted prices', () => {
    const productElements = fixture.debugElement.queryAll(By.css('p'));
    expect(productElements.length).toBe(2);
    expect(productElements[0].nativeElement.textContent).toContain('Product 1: 11.00 €');
    expect(productElements[1].nativeElement.textContent).toContain('Product 2: 16.50 €');
  });
});

```