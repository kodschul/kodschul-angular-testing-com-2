# Lösung zu Übung 1: Erstellen und Testen einer interaktiven Komponente mit Seitenobjekten

## Ziel
Diese Lösung zeigt, wie eine interaktive Angular-Komponente (Aufgabenplaner) erstellt wird, die Aufgaben hinzufügt, löscht und als abgeschlossen markiert. Dazu werden Unit-Tests und eine Page Object Class verwendet.

---

## Lösungsschritte

### 1. Erstellen der Komponente
Erstelle eine neue Komponente `TaskPlanner`:
```bash
ng generate component TaskPlanner
```

### 2. HTML-Struktur (task-planner.component.html)

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

### 3. CSS (task-planner.component.css)

```css
.completed {
  text-decoration: line-through;
}
```

### 4. TypeScript-Logik (task-planner.component.ts)

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

### 5. Page Object Class (task-planner.page.ts)

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

  addTask(taskName: string) {
    this.getTaskInput().type(taskName);
    this.getAddButton().click();
  }
}
```

### 6. Unit-Tests (task-planner.component.spec.ts)

```typescript
import { ComponentFixture, TestBed } from '@angular/core/testing';
import { FormsModule } from '@angular/forms';
import { TaskPlannerComponent } from './task-planner.component';

describe('TaskPlannerComponent', () => {
  let component: TaskPlannerComponent;
  let fixture: ComponentFixture<TaskPlannerComponent>;

  beforeEach(async () => {
    await TestBed.configureTestingModule({
      declarations: [TaskPlannerComponent],
      imports: [FormsModule]
    }).compileComponents();

    fixture = TestBed.createComponent(TaskPlannerComponent);
    component = fixture.componentInstance;
    fixture.detectChanges();
  });

  it('should create', () => {
    expect(component).toBeTruthy();
  });

  it('should add a task', () => {
    component.newTask = 'Test Task';
    component.addTask();
    expect(component.tasks.length).toBe(1);
    expect(component.tasks[0].name).toBe('Test Task');
  });

  it('should remove a task', () => {
    component.newTask = 'Task to remove';
    component.addTask();
    const task = component.tasks[0];
    component.removeTask(task);
    expect(component.tasks.length).toBe(0);
  });
});
```