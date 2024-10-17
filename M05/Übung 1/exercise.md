# Übung: Schreiben eines End-to-End-Tests für eine Filtereingabe

## Ziel der Übung
Schreibe einen End-to-End-Test (E2E), der eine Filterfunktion in einer Angular-Anwendung überprüft. Du testest, ob die Anwendung die Elemente auf der Seite korrekt filtert, basierend auf einer Benutzereingabe.

## Voraussetzungen
- Du benötigst ein Grundgerüst einer Angular-Anwendung. Hier ist ein Beispiel-Code für eine einfache Angular-App mit einer Filterfunktion:

### App-Komponenten-Code (`app.component.ts`):
```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-root',
  template: \`
    <input type="text" (input)="filter($event.target.value)" placeholder="Filter items"/>
    <ul>
      <li *ngFor="let item of filteredItems">{{ item }}</li>
    </ul>
  \`
})
export class AppComponent {
  items = ['Apple', 'Banana', 'Orange', 'Mango'];
  filteredItems = [...this.items];

  filter(query: string) {
    this.filteredItems = this.items.filter(item =>
      item.toLowerCase().includes(query.toLowerCase())
    );
  }
}
```
- Stelle sicher, dass Protractor oder Cypress für End-to-End-Tests eingerichtet ist. Falls du Protractor verwendest, ist dieser bereits standardmäßig in Angular CLI integriert.

## Aufgaben
1. Starte den Entwicklungsserver deiner Angular-Anwendung mit ng serve.
2. Erstelle einen neuen E2E-Test in der Datei app.e2e-spec.ts.
3. Schreibe einen Test, der die folgenden Szenarien abdeckt:
    - Der Nutzer gibt „Apple“ in das Filterfeld ein und überprüft, ob nur „Apple“ angezeigt wird.
    - Der Nutzer gibt „an“ ein und überprüft, ob „Banana“ und „Orange“ angezeigt werden.
    - Der Nutzer gibt einen Wert ein, der keine Übereinstimmung findet, und überprüft, dass die Liste leer ist.

## Hinweise
- Verwende in deinem Test das by.css()-Selektor-Tool, um auf die Eingabe und Listenelemente zuzugreifen.
- Nutze Protractor/Cypress Assertions, um die Filterfunktion zu überprüfen.