# Lösung zu Übung 2: Fortgeschrittene End-to-End-Testfälle implementieren

## Ziel
Diese Lösung zeigt, wie du die Angular-Komponente (Aufgabenplaner) erweiterst, um eine Filterfunktion hinzuzufügen, und wie du fortgeschrittene End-to-End (E2E) Tests mit Cypress implementierst, um diese Funktionalitäten zu testen.

---

## Lösungsschritte

### 1. Installation von Cypress
Stelle sicher, dass Cypress als E2E-Testing-Framework installiert ist:
```bash
ng add @cypress/schematic
```

### 2. Erweiterung der Anwendung
#### HTML-Erweiterung (task-planner.component.html)
- Füge einen Dropdown hinzu, um Aufgaben nach Status zu filtern:

```html
<select [(ngModel)]="filterOption" (change)="applyFilter()">
  <option value="all">All</option>
  <option value="completed">Completed</option>
  <option value="pending">Pending</option>
</select>
```

#### TypeScript-Erweiterung (task-planner.component.ts)
Implementiere die Filterfunktion:

```typescript
filterOption: string = 'all';

applyFilter() {
  switch (this.filterOption) {
    case 'completed':
      this.filteredTasks = this.tasks.filter(task => task.completed);
      break;
    case 'pending':
      this.filteredTasks = this.tasks.filter(task => !task.completed);
      break;
    default:
      this.filteredTasks = this.tasks;
  }
}
```

#### 3. Erweiterung der Page Object Class (task-planner.page.ts)

```typescript
export class TaskPlannerPage {
  navigateTo() {
    cy.visit('/'); // Passe den Pfad je nach Angular-Routing an
  }

  getTaskInput() {
    return cy.get('input[placeholder="New Task"]');
  }

  getAddButton() {
    return cy.get('button').contains('Add Task');
  }

  getTaskList() {
    return cy.get('ul li');
  }

  getFilterDropdown() {
    return cy.get('select');
  }

  selectFilter(option: string) {
    this.getFilterDropdown().select(option);
  }

  addTask(taskName: string) {
    this.getTaskInput().type(taskName);
    this.getAddButton().click();
  }
}
```

#### 4. Implementierung der E2E-Tests (task-planner.e2e-spec.ts)

```typescript
import { TaskPlannerPage } from './task-planner.page';

describe('Task Planner E2E Tests', () => {
  const page = new TaskPlannerPage();

  beforeEach(() => {
    page.navigateTo();
  });

  it('should add a task and display it', () => {
    page.addTask('E2E Test Task');
    page.getTaskList().should('have.length', 1);
    page.getTaskList().first().contains('E2E Test Task');
  });

  it('should mark a task as completed', () => {
    page.addTask('Complete this task');
    page.getTaskList().first().find('input[type="checkbox"]').click();
    page.getTaskList().first().find('span').should('have.class', 'completed');
  });

  it('should delete a task', () => {
    page.addTask('Task to be deleted');
    page.getTaskList().first().find('button').click();
    page.getTaskList().should('have.length', 0);
  });

  it('should filter tasks by completed status', () => {
    // Add tasks
    page.addTask('Task 1');
    page.addTask('Task 2');
    // Mark the first task as completed
    page.getTaskList().first().find('input[type="checkbox"]').click();

    // Select "Completed" filter and check the result
    page.selectFilter('completed');
    page.getTaskList().should('have.length', 1);
    page.getTaskList().first().contains('Task 1');

    // Select "Pending" filter and check the result
    page.selectFilter('pending');
    page.getTaskList().should('have.length', 1);
    page.getTaskList().first().contains('Task 2');
  });
});
```