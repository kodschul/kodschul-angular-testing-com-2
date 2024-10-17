# Übung 1: Fehlerhafte Komponente erstellen und beheben

## Ziel
Erstelle eine Angular-Komponente, um eine Liste von Produkten anzuzeigen, behebe jedoch die Fehler im Code, damit die Komponente ordnungsgemäß funktioniert.

## Beschreibung
Du hast eine Komponente `ProductComponent`, die eine Liste von Produkten rendern soll. Es gibt jedoch einige Fehler im Code, die behoben werden müssen, bevor die Komponente ordnungsgemäß funktioniert.

## Schritte

1. Erstelle eine Angular-Komponente `ProductComponent`, die eine Liste von Produkten im Template anzeigt.

2. Der folgende Code enthält einige Fehler. Überprüfe den Code sorgfältig und behebe alle Fehler, damit die Komponente die Produkte korrekt anzeigt.

### product.component.ts (Fehlerhafter Code)

```typescript
import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-product',
  templateUrl: './product.component.html',
  styleUrls: ['./product.component.css']
})
export class ProductComponent implements OnInit {
  products = [
    { name: 'Laptop', price: 1200 },
    { name: 'Phone', price: 800 }
  ];

  constructor() {}

  ngOnInit() {
    this.products.forEach(product => product.cost = product.price);
  }
}
```

## Aufgaben:

1. Analysiere den obenstehenden Code und finde die Fehler in der Implementierung.
2. Behebe die Fehler, sodass die Komponente die Namen und Preise der Produkte korrekt rendert.
3. Stelle sicher, dass die ProductComponent in der Anwendung eingebunden ist und auf der Seite angezeigt wird.

## Hinweise:
- Schaue dir die Typendefinitionen und die Objektstruktur genau an, um die Fehler zu finden.
- Überprüfe die Angular Console im Browser für mögliche Fehlerhinweise.