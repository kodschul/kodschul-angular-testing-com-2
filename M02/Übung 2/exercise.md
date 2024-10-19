
# Übung 2: Anwenden von regulären Ausdrücken zum Filtern von Daten

## Ziel
In dieser Übung wirst du eine Methode implementieren, die reguläre Ausdrücke verwendet, um eine Liste von Benutzern nach bestimmten Kriterien zu filtern. Du wirst dabei lernen, wie du mit regulären Ausdrücken in einem Angular-Service arbeitest und Unit-Tests erstellst, um die Funktionalität zu überprüfen.

## Aufgabenstellung
1. Implementiere eine Methode `filterUsersByEmailPattern` in der Klasse `UserService`. Diese Methode soll eine Liste von Benutzern durchgehen und diejenigen Benutzer zurückgeben, deren E-Mail-Adresse einem angegebenen Muster (Regex) entspricht.
2. Verwende einen regulären Ausdruck, um E-Mail-Adressen zu filtern, die z.B. mit `admin` beginnen oder auf `.com` enden.
3. Teste die Methode mit Unit-Tests in der Datei `user.service.spec.ts`, um sicherzustellen, dass sie korrekt funktioniert.

## Vorgaben
Die folgenden Dateien sind bereits vorbereitet. Verwende diese Dateien für deine Implementierung:

### 1. `src/app/services/user.service.ts`

Hier ist die Struktur der Service-Klasse, die die Methode enthalten soll. Ergänze die Methode `filterUsersByEmailPattern`, um die Benutzerliste basierend auf dem Regex-Pattern zu filtern.

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
    // Implementiere hier die Logik zum Filtern der Benutzer
    return [];
  }
}
```

### 2. `src/app/services/user.service.spec.ts`

Hier sind vorbereitete Unit-Tests, die zunächst fehlschlagen, da die Implementierung fehlt. Ergänze den `UserService` so, dass die Tests erfolgreich sind.

```typescript
import { UserService } from './user.service';

describe('UserService', () => {
  let service: UserService;

  beforeEach(() => {
    service = new UserService();
  });

  it('should filter users by email pattern: admin', () => {
    const result = service.filterUsersByEmailPattern('^admin');
    expect(result.length).toBe(1);
    expect(result[0].email).toBe('admin@domain.com');
  });

  it('should filter users by email pattern: .com$', () => {
    const result = service.filterUsersByEmailPattern('.com$');
    expect(result.length).toBe(2);
  });

  it('should return an empty array for unmatched pattern', () => {
    const result = service.filterUsersByEmailPattern('no-match');
    expect(result.length).toBe(0);
  });
});
```

### Hinweise
- Verwende in der Methode `filterUsersByEmailPattern` den `RegExp`-Konstruktor von JavaScript, um den regulären Ausdruck dynamisch zu erstellen und die Benutzerliste zu durchsuchen.
- Teste die Methode mit verschiedenen Regex-Mustern, um sicherzustellen, dass sie flexibel genug ist und wie erwartet funktioniert.

Viel Erfolg!
