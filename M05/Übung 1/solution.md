# Lösungsvorschlag: Schreiben eines End-to-End-Tests für eine Filtereingabe

## Überblick
Der End-to-End-Test (E2E) überprüft, ob die Filterfunktion in unserer Angular-Anwendung korrekt funktioniert. Der Test simuliert die Eingabe von Text in das Filterfeld und prüft, ob die Anwendung die angezeigten Elemente entsprechend der Eingabe filtert.

## Voraussetzungen
Stelle sicher, dass Protractor korrekt eingerichtet ist und die Angular-Anwendung läuft. Verwende `ng serve`, um den Entwicklungsserver zu starten.

## Beispiel-Lösung für den End-to-End-Test

### E2E-Test (`app.e2e-spec.ts`):
```typescript
import { browser, by, element } from 'protractor';

describe('Filter input test', () => {
  beforeEach(() => {
    browser.get('/');
  });

  it('should filter the list when the user types', () => {
    const input = element(by.css('input'));
    const listItems = element.all(by.css('li'));

    // Test: Der Nutzer gibt 'Apple' in das Filterfeld ein
    input.sendKeys('Apple');
    expect(listItems.count()).toEqual(1);
    expect(listItems.first().getText()).toEqual('Apple');

    // Test: Der Nutzer gibt 'an' in das Filterfeld ein
    input.clear().then(() => {
      input.sendKeys('an');
      expect(listItems.count()).toEqual(2);
      expect(listItems.get(0).getText()).toEqual('Banana');
      expect(listItems.get(1).getText()).toEqual('Orange');
    });

    // Test: Der Nutzer gibt einen Wert ein, der keine Übereinstimmung findet
    input.clear().then(() => {
      input.sendKeys('xyz');
      expect(listItems.count()).toEqual(0);
    });
  });
});
```