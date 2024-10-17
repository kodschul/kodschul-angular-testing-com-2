# Übung: Unit-Tests für einen Authentifizierungsdienst schreiben

## Kontext
Ihr sollt einen Authentifizierungsdienst testen, der Benutzeranmeldungen verwaltet und einen Token zurückgibt. Dieser Dienst nutzt einen HTTP-Client, um Anfragen an eine funktionierende API zu senden. Es ist wichtig, sicherzustellen, dass der Dienst korrekt auf verschiedene API-Antworten reagiert.

**Hinweis**: In dieser Übung wird eine funktionierende API verwendet, die Benutzerdaten und Token zurückgibt. Ihr müsst sicherstellen, dass der Service korrekt mit der API interagiert und die Daten verarbeitet.

## Aufgaben

1. **Setup**: Erstellt eine Testumgebung für den `AuthService` mit Angular’s `TestBed` und mockt den `HttpClient` mithilfe von `HttpClientTestingModule`.
2. **Testfall 1**: Schreibt einen Test, um zu überprüfen, ob die `login`-Methode einen Token zurückgibt, wenn die API erfolgreich antwortet.
3. **Testfall 2**: Simuliert eine Fehlerantwort von der API und stellt sicher, dass der Dienst entsprechend reagiert und eine Fehlermeldung zurückgibt.
4. **Testfall 3**: Testet, ob die `logout`-Methode den Benutzer korrekt abmeldet, indem sie den Token entfernt.

## Vorgefertigter Code

```typescript
// auth.service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable, throwError } from 'rxjs';
import { map, catchError } from 'rxjs/operators';

@Injectable({
  providedIn: 'root'
})
export class AuthService {
  private apiUrl = 'https://reqres.in/api/login';

  constructor(private http: HttpClient) {}

  login(username: string, password: string): Observable<string> {
    return this.http.post<{ token: string }>(`${this.apiUrl}`, { email: username, password: password })
      .pipe(
        map(response => response.token),
        catchError(error => {
          console.error('Login failed', error);
          return throwError('Login failed, please try again later.');
        })
      );
  }

  logout(): void {
    // Implementiere die Logik zum Abmelden des Benutzers
  }
}