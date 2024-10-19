
# Lösungsvorschlag für Übung 2: Anwenden von regulären Ausdrücken zum Filtern von Daten

## Lösung der Methode `filterUsersByEmailPattern`

Hier ist die Implementierung der Methode `filterUsersByEmailPattern` in der Klasse `UserService`. Diese Methode verwendet reguläre Ausdrücke, um Benutzer zu filtern, deren E-Mail-Adresse einem bestimmten Muster entspricht.

```typescript
import { Injectable } from '@angular/core';

export interface User {
  id: number;
  name: string;
  email: string;
}

@Injectable({
  providedIn: 'root'
})
export class UserService {
  private users: User[] = [
    { id: 1, name: 'Alice', email: 'alice@example.com' },
    { id: 2, name: 'Bob', email: 'bob@company.com' },
    { id: 3, name: 'Charlie', email: 'admin@domain.com' },
    { id: 4, name: 'David', email: 'user@domain.org' }
  ];

  constructor() {}

  filterUsersByEmailPattern(pattern: string): User[] {
    const regex = new RegExp(pattern);
    return this.users.filter(user => regex.test(user.email));
  }
}
```

### Erklärung
- Die Methode `filterUsersByEmailPattern` nimmt ein Pattern (Zeichenkette) als Parameter und erstellt daraus ein `RegExp`-Objekt.
- Anschließend wird die Liste der Benutzer (`users`) gefiltert, indem überprüft wird, ob die E-Mail-Adresse des Benutzers dem regulären Ausdruck entspricht.
- Die Methode gibt die gefilterte Liste der Benutzer zurück.