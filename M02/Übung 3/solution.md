
# Lösungsvorschlag für Übung 3: Verstehen von Angular-Dekoratoren und deren Nutzung

## Lösung der `ProductComponent`

Hier ist die vollständige Implementierung der `ProductComponent`, die den `@Input()`- und `@Output()`-Dekorator verwendet, um ein Produkt zu empfangen und das Speichern-Event auszulösen.

### `product.component.ts`

```typescript
import { Component, Input, Output, EventEmitter } from '@angular/core';

@Component({
  selector: 'app-product',
  templateUrl: './product.component.html',
  styleUrls: ['./product.component.css']
})
export class ProductComponent {
  @Input() product: any; // Produktobjekt als Input erhalten
  @Output() save = new EventEmitter<any>(); // EventEmitter für das Speichern-Event

  onSave() {
    // Logik für das Speichern-Event
    this.save.emit(this.product);
  }
}
```

### Erklärung
- Der `@Input()`-Dekorator wird verwendet, um das Produkt von einer übergeordneten Komponente zu empfangen.
- Der `@Output()`-Dekorator wird verwendet, um ein Event zu emittieren, wenn der Benutzer auf "Speichern" klickt.
- Die Methode `onSave()` wird durch einen Button-Klick aufgerufen und löst das Event aus, wobei das Produkt als Payload gesendet wird.

## Lösung des `ProductService`

Hier ist die Implementierung des `ProductService`, der den `@Injectable()`-Dekorator verwendet und Methoden zum Speichern und Laden von Produktdaten bereitstellt.

### `product.service.ts`

```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class ProductService {
  saveProduct(product: any) {
    console.log('Produkt gespeichert:', product);
    // Hier könnte der Code zum Speichern des Produkts in einer Datenbank stehen
  }

  loadProduct(id: number) {
    console.log('Produkt geladen:', id);
    // Rückgabe eines Beispielprodukts
    return { id, name: 'Beispielprodukt', price: 100 };
  }
}
```

### Erklärung
- Der `@Injectable()`-Dekorator stellt sicher, dass der Service in der gesamten Anwendung verwendet werden kann.
- Die Methode `saveProduct()` simuliert das Speichern eines Produkts (in einer echten Anwendung würde dies in einer Datenbank oder via API erfolgen).
- Die Methode `loadProduct()` simuliert das Laden eines Produkts basierend auf einer ID und gibt ein Beispielprodukt zurück.
