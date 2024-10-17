# Übung 3: Eine einfache Fehlerbehandlungsklasse schreiben

## Ziel
In dieser Übung sollst du eine Fehlerbehandlungsklasse schreiben, die alle HTTP-Fehler abfängt und eine benutzerfreundliche Fehlermeldung zurückgibt.

## Beschreibung
Du arbeitest an einer Angular-Komponente `DataComponent`, die Daten von einer externen API abruft. Deine Aufgabe besteht darin, eine Fehlerbehandlungsklasse `ErrorHandlerService` zu erstellen, die alle HTTP-Fehler zentral abfängt. Die Komponente soll nach der Implementierung eine benutzerfreundliche Fehlermeldung anzeigen, falls die API nicht verfügbar ist oder ein anderer Fehler auftritt.

## Schritte

1. Erstelle die Komponente `DataComponent`, die Daten von einer externen API abruft und anzeigt.
2. Erstelle den Service `ErrorHandlerService`, der für das Abfangen und Behandeln von HTTP-Fehlern verantwortlich ist.
3. Fange die HTTP-Fehler in der `DataComponent` ab und zeige eine benutzerfreundliche Fehlermeldung im Frontend an.

### data.component.ts (Unvollständiger Code)

```typescript
import { Component, OnInit } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { catchError } from 'rxjs/operators';
import { throwError } from 'rxjs';

@Component({
  selector: 'app-data',
  templateUrl: './data.component.html',
  styleUrls: ['./data.component.css']
})
export class DataComponent implements OnInit {
  data: any;
  errorMessage: string | null = null;

  constructor(private http: HttpClient) {}

  ngOnInit() {
    this.http.get('https://jsonplaceholder.typicode.com/posts')  // API-Endpoint für die Daten
      .pipe(
        catchError(error => {
          return throwError(() => new Error('Failed to fetch data'));
        })
      )
      .subscribe({
        next: (response) => this.data = response,
        error: (err) => this.errorMessage = err.message
      });
  }
}
```

### Aufgaben:
1. Implementiere die Fehlerbehandlungsklasse ErrorHandlerService, die alle HTTP-Fehler zentral abfängt.
2. Integriere den Service in die Komponente DataComponent, um die Fehlerbehandlung zu verbessern.
3. Teste die Anwendung, indem du sie ausführst und sicherstellst, dass Fehler richtig abgefangen und angezeigt werden.

### Hinweise:
- Du kannst die HTTP-Fehler abfangen und im Frontend eine benutzerfreundliche Meldung anzeigen.