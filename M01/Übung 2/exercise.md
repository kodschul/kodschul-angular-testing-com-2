# Übung 2: Fehler bei der Injektion von Abhängigkeiten identifizieren und lösen

## Ziel
In dieser Übung geht es darum, ein Problem bei der Injektion eines Services in eine Angular-Komponente zu identifizieren und zu beheben.

## Beschreibung
Die Komponente `UserComponent` soll Benutzerdaten von einem Service `UserService` abrufen und anzeigen. Leider funktioniert die Abhängigkeitsinjektion nicht korrekt, und die Komponente kann den Service nicht verwenden.

## Schritte

1. Erstelle eine Komponente `UserComponent`, die Benutzerdaten über einen Service anzeigt.

2. Der folgende Code enthält Fehler. Überprüfe den Code sorgfältig und behebe die Probleme bei der Injektion des Services und der Datenanzeige.

### user.component.ts (Fehlerhafter Code)

```typescript
import { Component, OnInit } from '@angular/core';
import { UserService } from './user.service';

@Component({
  selector: 'app-user',
  templateUrl: './user.component.html',
  styleUrls: ['./user.component.css']
})
export class UserComponent implements OnInit {
  users: any[];

  constructor(private service: UserService) {}

  ngOnInit() {
    this.users = this.service.getUsers();
  }
}
```

### user.service.ts (Fehlerhafter Code)

```typescript
import { Injectable } from '@angular/core';

@Injectable({
  providedIn: 'root'
})
export class UserService {
  getUsers() {
    return [];
  }
}

```

## Aufgaben:
1. Finde und behebe den Fehler bei der Injektion des UserService in UserComponent.
2. Stelle sicher, dass der UserService Benutzerdaten zurückgibt und diese korrekt in der Komponente angezeigt werden.
3. Teste die Anwendung, um sicherzustellen, dass die Benutzerliste korrekt gerendert wird.

## Hinweise:
- Schaue dir die Angular-Dokumentation zur Abhängigkeitsinjektion (Dependency Injection) an, falls du dir unsicher bist.
- Überprüfe die Konsole auf Fehler oder Warnungen, die auf Probleme bei der Injektion hinweisen könnten.