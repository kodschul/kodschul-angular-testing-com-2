# Lösung für Übung 1: Fehlerhafte Komponente erstellen und beheben

## Ziel
Die Aufgabe bestand darin, eine Angular-Komponente zu erstellen, die eine Liste von Produkten anzeigt und vorhandene Fehler zu beheben, um sicherzustellen, dass die Produkte korrekt gerendert werden.

## Fehleranalyse und Lösung

### 1. Problem mit der Eigenschaft `cost`
In der ursprünglichen Version des Codes wurde in der `ngOnInit`-Methode eine Eigenschaft `cost` für die Produkte gesetzt, die jedoch nicht in den Objekten vorhanden ist. Stattdessen wird bereits die richtige Eigenschaft `price` verwendet, die für den Preis des Produkts steht.

### 2. Behebung des Fehlers
Der Fehler tritt auf, weil die Eigenschaft `cost` nicht existiert und es unnötig ist, diese hinzuzufügen, da die Eigenschaft `price` bereits vorhanden ist und korrekt verwendet werden kann. Der Code in der `ngOnInit`-Methode ist überflüssig und kann entfernt werden.

### Korrigierter Code

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
    // Kein Bedarf, zusätzliche Eigenschaft hinzuzufügen oder zu ändern
    // Produkte sind korrekt definiert und bereit zur Anzeige
  }
}
```

### 3. Sicherstellen, dass die Produkte korrekt angezeigt werden
Im HTML-Template sollte sichergestellt werden, dass die Produkte korrekt gerendert werden. Eine einfache For-Schleife kann verwendet werden, um die Namen und Preise der Produkte aufzulisten.

```typescript
<!-- product.component.html -->
<div *ngFor="let product of products">
  <p>{{ product.name }}: {{ product.price | currency }}</p>
</div>
```