# Übung 3: Anwendung von Linting-Tools auf das Angular-Projekt

In dieser Übung wirst du **Linting** auf das bestehende Angular-Projekt (Task Planner) anwenden, um Code-Qualitätsprobleme und Stilabweichungen zu identifizieren und zu beheben. Das Ziel ist es, alle gefundenen Linting-Fehler zu analysieren und zu korrigieren, um den Code gemäß den Best Practices für Angular und TypeScript zu optimieren.

## Aufgabenstellung

1. **Installation und Konfiguration von ESLint**
   - Stelle sicher, dass `ESLint` als Linting-Tool im Projekt installiert ist. Falls ESLint noch nicht installiert ist, führe den folgenden Befehl aus:
     ```bash
     ng add @angular-eslint/schematics
     ```
   - Überprüfe die Konfiguration in der `.eslintrc.json` Datei und passe gegebenenfalls die Regeln an.

2. **Ausführen des Linters**
   - Führe den Linter über die Angular CLI aus, um alle aktuellen Linting-Fehler im Projekt anzuzeigen:
     ```bash
     ng lint
     ```
   - Analysiere die Ausgabe und notiere dir die gemeldeten Fehler und Warnungen.

3. **Fehleranalyse und -behebung**
   - Gehe alle gemeldeten Fehler durch und behebe diese schrittweise.
     - Entferne unbenutzte Variablen und Importe.
     - Stelle sicher, dass alle Variablen und Funktionen korrekt typisiert sind.
     - Passe den Code an, um den empfohlenen Stilregeln zu entsprechen (z.B. Einrückungen, Semikolons, Klammer-Stil).

4. **Automatisierte Linting-Korrekturen**
   - Führe automatisierte Korrekturen durch den Linter aus:
     ```bash
     ng lint --fix
     ```
   - Überprüfe die vorgenommenen Änderungen und stelle sicher, dass der Code weiterhin korrekt funktioniert.

5. **Überprüfung der Korrekturen**
   - Führe den Linter erneut aus:
     ```bash
     ng lint
     ```
   - Stelle sicher, dass alle Fehler behoben sind und keine neuen Fehler auftreten.

6. **Testen der Anwendung**
   - Starte die Anwendung:
     ```bash
     ng serve
     ```
   - Teste alle Funktionalitäten, um sicherzustellen, dass die Anwendung nach den Änderungen korrekt funktioniert.

## Zusatzaufgabe

- Aktualisiere die Linting-Regeln in der `.eslintrc.json` Datei, um strengere Regeln hinzuzufügen (z.B. verpflichtende Nutzung von Typen oder die Vermeidung des `any` Typs).
- Führe den Linter erneut aus und behebe alle neuen Fehler, um die Codequalität weiter zu verbessern.

---

## Benötigte Dateien

Falls du die Anwendung nicht erstellt hast, findest du hier die Grundstruktur:

### **task-planner.component.html**
```html
<h2>Task Planner</h2>
<input type="text" [(ngModel)]="newTask" placeholder="New Task" />
<button (click)="addTask()">Add Task</button>

<ul>
  <li *ngFor="let task of tasks">
    <input type="checkbox" [(ngModel)]="task.completed" />
    <span [class.completed]="task.completed">{{ task.name }}</span>
    <button (click)="removeTask(task)">Delete</button>
  </li>
</ul>
```

### task-planner.component.ts

```typescript
import { Component } from '@angular/core';

interface Task {
  name: string;
  completed: boolean;
}

@Component({
  selector: 'app-task-planner',
  templateUrl: './task-planner.component.html',
  styleUrls: ['./task-planner.component.css']
})
export class TaskPlannerComponent {
  newTask: string = '';
  tasks: Task[] = [];

  addTask() {
    if (this.newTask) {
      this.tasks.push({ name: this.newTask, completed: false });
      this.newTask = '';
    }
  }

  removeTask(task: Task) {
    this.tasks = this.tasks.filter(t => t !== task);
  }
}
```

### task-planner.component.css

```css
.completed {
  text-decoration: line-through;
}
```