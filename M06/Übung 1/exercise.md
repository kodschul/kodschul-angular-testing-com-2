# Übung 1: Erstellen und Testen einer interaktiven Komponente mit Seitenobjekten

## Ziel
In dieser Übung wirst du eine interaktive Angular-Komponente erstellen, die als **Aufgabenplaner** dient. Diese Komponente erlaubt es Nutzern, Aufgaben hinzuzufügen, zu löschen und als abgeschlossen zu markieren. Anschließend schreibst du Unit-Tests für diese Komponente und verwendest das **Page Object Pattern**, um die Tests zu strukturieren.

## Schritte

### 1. Erstelle eine neue Angular-Komponente
- Erstelle eine neue Komponente namens `TaskPlanner`:
  ```bash
  ng generate component TaskPlanner
  ```

### 2. HTML-Struktur für die Komponente
- Implementiere die HTML-Struktur in der Datei `task-planner.component.html`:
  - Ein Eingabefeld für neue Aufgaben.
  - Ein Button, um Aufgaben hinzuzufügen.
  - Eine Liste zur Anzeige der Aufgaben mit Checkboxen, um Aufgaben als abgeschlossen zu markieren, und Buttons, um Aufgaben zu löschen.

### 3. CSS für die Komponente
- Füge CSS in `task-planner.component.css` hinzu, um abgeschlossene Aufgaben durchzustreichen. Verwende eine Klasse `.completed`.

### 4. Implementiere das Verhalten der Komponente
- Definiere das Verhalten in `task-planner.component.ts`:
  - Die Komponente sollte eine Methode zum Hinzufügen einer neuen Aufgabe und eine Methode zum Löschen einer Aufgabe enthalten.
  - Verwende **Angular Forms** (`ngModel`), um die Eingabefelder mit der Komponente zu verbinden.

### 5. Erstelle eine Page Object Class
- Erstelle eine Page Object Class namens `TaskPlannerPage` im Testverzeichnis (z.B. `src/test/task-planner.page.ts`).
- Diese Klasse sollte Methoden bereitstellen, um mit der Komponente zu interagieren:
  - Eingabefeld für Aufgaben.
  - Button zum Hinzufügen von Aufgaben.
  - Zugriff auf die Aufgabenliste.

### 6. Implementiere Unit-Tests
- Implementiere Unit-Tests für die `TaskPlannerComponent` in der Datei `task-planner.component.spec.ts`.
- Die Tests sollten folgendes überprüfen:
  - Ob die Komponente erfolgreich erstellt wird.
  - Ob eine Aufgabe hinzugefügt werden kann.
  - Ob eine Aufgabe gelöscht werden kann.

---

## Hinweise
- Stelle sicher, dass du das `FormsModule` importierst, um das **Two-Way Binding** (`[(ngModel)]`) zu nutzen.
- Verwende das **Page Object Pattern**, um die Teststruktur sauber und wiederverwendbar zu gestalten.

---

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
