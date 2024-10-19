
# Übung 3: Verstehen von Angular-Dekoratoren und deren Nutzung

## Ziel
In dieser Übung wirst du verschiedene Angular-Dekoratoren wie `@Input()`, `@Output()`, `@Component()`, und `@Injectable()` anwenden und besser verstehen. Du wirst eine Komponente und einen Service implementieren, die miteinander interagieren, und Events korrekt behandeln.

## Aufgabenstellung
1. Implementiere in der Datei `product.component.ts` eine Angular-Komponente (`ProductComponent`), die ein Produktobjekt als Input erhält und bearbeitet. Verwende dafür den `@Input()`-Dekorator.
2. Füge einen `@Output()`-Dekorator hinzu, um ein Event (`save`) auszulösen, wenn der Benutzer das Produkt speichert.
3. Implementiere eine `ProductService`-Klasse mit dem `@Injectable()`-Dekorator, die eine Methode bereitstellt, um Produktdaten zu speichern und zu laden.

### Hinweise
- Stelle sicher, dass die Komponente und der Service korrekt verbunden sind und die Events wie erwartet ausgelöst werden.
- Verwende die Unit-Tests, um typische Fehler zu identifizieren und zu beheben.

Viel Erfolg!
