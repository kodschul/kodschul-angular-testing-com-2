# Übung 2: Fortgeschrittene End-to-End-Testfälle implementieren

## Ziel
In dieser Übung erweiterst du die Angular-Komponente des Aufgabenplaners mit zusätzlichen Interaktionen und implementierst fortgeschrittene End-to-End (E2E) Tests. Du überprüfst, ob die Anwendung korrekt mit dem Browser interagiert und alle Funktionalitäten wie erwartet funktionieren.

---

## Schritte

### 1. Installiere Cypress für E2E-Tests
- Stelle sicher, dass Cypress als E2E-Testing-Framework installiert ist:
  ```bash
  ng add @cypress/schematic
  ```

### 2. Erweiterung der Anwendung
- Implementiere eine Filterfunktion, die es ermöglicht, nur abgeschlossene oder noch offene Aufgaben anzuzeigen.
- Füge einen Dropdown in der task-planner.component.html hinzu, der die Filteroptionen ("All", "Completed", "Pending") anbietet.
### 3. Page Object Class erweitern
- Erweitere die Page Object Class (task-planner.page.ts) um Methoden, die den Filter-Dropdown und die Interaktionen damit kapseln.
    - Füge eine Methode hinzu, um eine Filteroption auszuwählen.
    - Füge eine Methode hinzu, um die Anzahl der angezeigten Aufgaben zu überprüfen.
### 4. Implementiere E2E-Tests
- Erstelle eine neue Testdatei (task-planner.e2e-spec.ts) und importiere die Page Object Class.
- Implementiere die folgenden Tests:
    - Test 1: Überprüfe, ob eine Aufgabe hinzugefügt und in der Liste angezeigt wird.
    - Test 2: Überprüfe, ob eine Aufgabe als abgeschlossen markiert werden kann.
    - Test 3: Überprüfe, ob eine Aufgabe gelöscht werden kann.
    - Test 4: Überprüfe, ob der Filter korrekt funktioniert:
        - Wähle "Completed" und überprüfe, ob nur abgeschlossene Aufgaben angezeigt werden.
        - Wähle "Pending" und überprüfe, ob nur offene Aufgaben angezeigt werden.

## Hinweise
- Verwende das Page Object Pattern, um die Teststruktur sauber und modular zu halten.
- Stelle sicher, dass der Aufgabenplaner richtig im Browser geladen wird, bevor die Tests ausgeführt werden.
- Der Filter-Dropdown sollte wie folgt aussehen

```html
<select [(ngModel)]="filterOption" (change)="applyFilter()">
  <option value="all">All</option>
  <option value="completed">Completed</option>
  <option value="pending">Pending</option>
</select>
```

## Beispiel-Dateistruktur

```plaintext
src/
│
├── app/
│   ├── task-planner/
│   │   ├── task-planner.component.html
│   │   ├── task-planner.component.ts
│   │   ├── task-planner.component.css
│   │   └── task-planner.component.spec.ts
│
└── test/
    ├── task-planner.page.ts
    └── task-planner.e2e-spec.ts
```