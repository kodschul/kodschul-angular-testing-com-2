# Übung: Testen einer kompletten Benutzerinteraktion

## Ziel der Übung
Schreibe einen End-to-End-Test (E2E), der eine vollständige Benutzerinteraktion in einer Angular-Anwendung simuliert. Du testest, ob ein Benutzer eine Aufgabe in der Anwendung erfolgreich abschließen kann, z.B. das Hinzufügen und Entfernen eines Artikels aus einer Liste.

## Voraussetzungen
- Nutze das folgende Grundgerüst für eine Angular-Anwendung, um mit der Übung zu beginnen:

### App-Komponenten-Code (`app.component.ts`):
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: \`
    <input type="text" [(ngModel)]="newItem" placeholder="Add item"/>
    <button (click)="addItem()">Add</button>
    <ul>
      <li *ngFor="let item of items; let i = index">
        {{ item }}
        <button (click)="removeItem(i)">Remove</button>
      </li>
    </ul>
  \`
})
export class AppComponent {
  items = ['Apple', 'Banana', 'Orange', 'Mango'];
  newItem: string = '';

  addItem() {
    if (this.newItem) {
      this.items.push(this.newItem);
      this.newItem = '';
    }
  }

  removeItem(index: number) {
    this.items.splice(index, 1);
  }
}
```
- Stelle sicher, dass Protractor oder Cypress für End-to-End-Tests eingerichtet ist. Falls du Protractor verwendest, ist dieser bereits standardmäßig in Angular CLI integriert.

## Aufgaben
1. Starte den Entwicklungsserver deiner Angular-Anwendung mit ng serve.
2. Erstelle einen neuen E2E-Test in der Datei app.e2e-spec.ts.
3. Schreibe einen Test, der die folgenden Szenarien abdeckt:
    - Der Nutzer gibt „Grapes“ in das Eingabefeld ein und klickt auf „Add“, um den Artikel hinzuzufügen. Der Test überprüft, ob „Grapes“ in der Liste erscheint.
    - Der Nutzer entfernt den Artikel „Banana“ aus der Liste und überprüft, dass er nicht mehr angezeigt wird.
    - Der Nutzer fügt mehrere Artikel hinzu und entfernt sie, um die Funktionalität weiter zu testen.

## Hinweise
- Verwende in deinem Test das by.css()-Selektor-Tool, um auf die Eingabe und Listenelemente zuzugreifen.
- Nutze Protractor/Cypress Assertions, um die Filterfunktion zu überprüfen.