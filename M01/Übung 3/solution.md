# Lösung für Übung 3: Eine einfache Fehlerbehandlungsklasse schreiben

## Ziel
Die Aufgabe bestand darin, eine Fehlerbehandlungsklasse zu implementieren, die HTTP-Fehler zentral abfängt und benutzerfreundliche Fehlermeldungen anzeigt.

## Fehlerbehandlungsklasse: `ErrorHandlerService`

### 1. Erstellen der Fehlerbehandlungsklasse

Zuerst wird die Fehlerbehandlungsklasse erstellt, um HTTP-Fehler abzufangen und eine benutzerfreundliche Fehlermeldung zu liefern. Der Service überprüft, ob der Fehler clientseitig oder serverseitig aufgetreten ist, und gibt eine entsprechende Nachricht zurück.

#### error-handler.service.ts

```typescript
import { Injectable } from '@angular/core';
import { HttpErrorResponse } from '@angular/common/http';
import { throwError } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class ErrorHandlerService {
  handleError(error: HttpErrorResponse) {
    let errorMessage = 'An unknown error occurred!';
    if (error.error instanceof ErrorEvent) {
      // Client-side error
      errorMessage = `Error: ${error.error.message}`;
    } else {
      // Server-side error
      errorMessage = `Error Code: ${error.status}\nMessage: ${error.message}`;
    }
    console.error(errorMessage);
    return throwError(() => new Error(errorMessage));
  }
}
```

### 2. Integration der Fehlerbehandlung in die Komponente
Die Fehlerbehandlungsklasse wird nun in der DataComponent verwendet. Die Methode handleError wird aufgerufen, um alle HTTP-Fehler abzufangen und eine benutzerfreundliche Nachricht zurückzugeben.

#### data.component.ts (Korrigierter Code)

```typescript
import { Component, OnInit } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { catchError } from 'rxjs/operators';
import { ErrorHandlerService } from './error-handler.service';  // Importiere den ErrorHandlerService
import { throwError } from 'rxjs';

@Component({
  selector: 'app-data',
  templateUrl: './data.component.html',
  styleUrls: ['./data.component.css']
})
export class DataComponent implements OnInit {
  data: any;
  errorMessage: string | null = null;

  constructor(private http: HttpClient, private errorHandler: ErrorHandlerService) {}  // Injektion des ErrorHandlerService

  ngOnInit() {
    this.http.get('https://jsonplaceholder.typicode.com/posts')
      .pipe(
        catchError(error => this.errorHandler.handleError(error))  // Fehlerbehandlung über den ErrorHandlerService
      )
      .subscribe({
        next: (response) => this.data = response,
        error: (err) => this.errorMessage = err.message  // Zeige die Fehlermeldung im Frontend an
      });
  }
}
```

### 3. Anzeige der Fehlermeldung im Frontend
Im Template der Komponente wird die Fehlermeldung angezeigt, falls ein Fehler auftritt.

#### data.component.html

```html
<!-- data.component.html -->
<div *ngIf="errorMessage">
  <p>Error: {{ errorMessage }}</p>
</div>

<div *ngIf="data">
  <ul>
    <li *ngFor="let post of data">
      {{ post.title }}
    </li>
  </ul>
</div>
```