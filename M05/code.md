
# Angular Testing und Debugging Schulung - E2E und Benutzerinteraktion

## Themen

1. Schreiben eines End-to-End-Tests für eine Filtereingabe
2. Testen einer kompletten Benutzerinteraktion

## 1. Schreiben eines End-to-End-Tests für eine Filtereingabe

### Live Coding Beispiel

Angenommen, wir haben eine Komponente mit einer Filtereingabe, die eine Liste von Einträgen anzeigt.

**Komponente:** `filter-list.component.ts`

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-filter-list',
  template: `
    <input type="text" (input)="filter($event.target.value)" placeholder="Filter..." />
    <ul>
      <li *ngFor="let item of filteredItems">{{ item }}</li>
    </ul>
  `
})
export class FilterListComponent {
  items = ['Apple', 'Banana', 'Cherry', 'Date', 'Elderberry'];
  filteredItems = [...this.items];

  filter(query: string) {
    this.filteredItems = this.items.filter(item => item.toLowerCase().includes(query.toLowerCase()));
  }
}
```

**E2E Test mit Protractor:**

In der Datei `filter-list.e2e-spec.ts`:

```typescript
import { browser, by, element } from 'protractor';

describe('FilterListComponent', () => {
  beforeEach(() => {
    browser.get('/filter-list');
  });

  it('should filter the list based on input', () => {
    const input = element(by.css('input'));
    const listItems = element.all(by.css('li'));

    input.sendKeys('a');
    expect(listItems.count()).toBe(3); // 'Apple', 'Banana', 'Date'

    input.clear();
    input.sendKeys('ch');
    expect(listItems.count()).toBe(1); // 'Cherry'
  });
});
```

## 2. Testen einer kompletten Benutzerinteraktion

### Live Coding Beispiel

Angenommen, wir haben eine einfache To-Do-App, in der der Benutzer Einträge hinzufügen und entfernen kann.

**Komponente:** `todo.component.ts`

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-todo',
  template: `
    <input #taskInput type="text" placeholder="Neue Aufgabe" />
    <button (click)="addTask(taskInput.value)">Hinzufügen</button>
    <ul>
      <li *ngFor="let task of tasks; let i = index">
        {{ task }} <button (click)="removeTask(i)">Entfernen</button>
      </li>
    </ul>
  `
})
export class TodoComponent {
  tasks: string[] = [];

  addTask(task: string) {
    if (task) {
      this.tasks.push(task);
    }
  }

  removeTask(index: number) {
    this.tasks.splice(index, 1);
  }
}
```

**E2E Test mit Protractor:**

In der Datei `todo.e2e-spec.ts`:

```typescript
import { browser, by, element } from 'protractor';

describe('TodoComponent', () => {
  beforeEach(() => {
    browser.get('/todo');
  });

  it('should add and remove tasks', () => {
    const input = element(by.css('input'));
    const addButton = element(by.buttonText('Hinzufügen'));
    const taskList = element.all(by.css('li'));

    input.sendKeys('Test Aufgabe 1');
    addButton.click();
    expect(taskList.count()).toBe(1);

    input.sendKeys('Test Aufgabe 2');
    addButton.click();
    expect(taskList.count()).toBe(2);

    const removeButton = taskList.get(0).element(by.buttonText('Entfernen'));
    removeButton.click();
    expect(taskList.count()).toBe(1);
  });
});
```