# Lösung für Übung 2: Fehler bei der Injektion von Abhängigkeiten identifizieren und lösen

## Ziel
In dieser Aufgabe wurde ein Problem bei der Injektion eines Services in eine Angular-Komponente analysiert und gelöst, damit die Komponente Benutzerdaten korrekt anzeigen kann.

## Fehleranalyse und Lösung

### 1. Fehler bei der Abhängigkeitsinjektion
Der Fehler in der Komponente `UserComponent` resultierte daraus, dass der `UserService` korrekt importiert und in den Konstruktor injiziert wurde, jedoch keine Daten zurückgab. Außerdem wurde der Service möglicherweise nicht richtig in der Angular-App registriert.

### 2. Behebung des Fehlers
- **Korrektur des `UserService`**: Der `UserService` gibt eine leere Liste zurück. Um den Fehler zu beheben, muss der Service eine Liste von Dummy-Benutzern zurückgeben.
- **Prüfung der Deklaration des Services**: Der Service ist bereits mit `providedIn: 'root'` korrekt deklariert, sodass keine Änderungen erforderlich sind.
- **Injektion des Services in die Komponente**: Die Injektion des Services ist korrekt, es war nur die Logik im Service zu überarbeiten.

### Korrigierter Code

#### user.service.ts (Korrigierter Code)

```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class UserService {
  getUsers() {
    // Korrektur: Rückgabe einer Liste von Dummy-Benutzern
    return [
      { name: 'Max Mustermann', email: 'max@example.com' },
      { name: 'Erika Musterfrau', email: 'erika@example.com' }
    ];
  }
}
```

#### user.component.ts (Korrigierter Code)

```typescript
import { Component, OnInit } from '@angular/core';
import { UserService } from './user.service';  // Service wird importiert

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.css']
})
export class UserComponent implements OnInit {
  users: any[];

  constructor(private service: UserService) {}  // Korrekte Injektion des Services

  ngOnInit() {
    // Der Service liefert nun Benutzer, die korrekt angezeigt werden
    this.users = this.service.getUsers();
  }
}
```

### 3. Anzeige der Benutzerdaten im Template
Um sicherzustellen, dass die Benutzerdaten korrekt angezeigt werden, wird im HTML-Template eine For-Schleife verwendet, um die Benutzernamen und E-Mail-Adressen zu rendern.

```html
<!-- user.component.html -->
<div *ngFor="let user of users">
  <p>{{ user.name }} - {{ user.email }}</p>
</div>
```