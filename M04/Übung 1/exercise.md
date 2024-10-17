# Übung 1: Testen einer Pipe und einer benutzerdefinierten Komponente

## Ziel
Lerne, wie man eine benutzerdefinierte Pipe und eine Komponente testet, indem du Unit-Tests schreibst und sicherstellst, dass beide korrekt funktionieren.

## Kontext
Du arbeitest in einem Team, das eine Angular-Anwendung zur Verwaltung von Produkten entwickelt. Die Anwendung enthält eine Pipe, die die Preise der Produkte in verschiedene Währungen umrechnet, sowie eine Komponente, die eine Liste dieser Produkte anzeigt.

## Aufgabenstellung

### 1. Erstellen der Pipe
- Erstelle eine Pipe `CurrencyConverterPipe`, die einen Betrag in Euro entgegennimmt und diesen in eine andere Währung umrechnet. Der Wechselkurs wird als Parameter übergeben.

### 2. Erstellen der Komponente
- Erstelle eine Komponente ProductListComponent, die eine Liste von Produkten anzeigt. Jedes Produkt hat einen Namen und einen Preis in Euro, der mithilfe der CurrencyConverterPipe in USD umgerechnet wird.

### 3. Unit-Tests schreiben
- Teste die Pipe: Schreibe Tests, die sicherstellen, dass die CurrencyConverterPipe korrekt funktioniert und verschiedene Währungsumrechnungen durchführt.
- Teste die Komponente: Schreibe Tests für ProductListComponent, die überprüfen, ob die Produkte korrekt angezeigt werden und die Pipe richtig funktioniert.