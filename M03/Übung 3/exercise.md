# Übung: Testen von Observables und deren Fehlerbehandlung im Bestellungsdienst

## Kontext
Der `OrderService` verwaltet Bestellungen und nutzt Observables, um Bestelldaten abzurufen. Ihr sollt sicherstellen, dass die Methode `getOrderById` korrekt funktioniert und sowohl erfolgreiche als auch fehlerhafte API-Antworten richtig verarbeitet.

**Hinweis**: In dieser Übung wird eine funktionierende API verwendet, die Bestelldaten zurückgibt. Ihr müsst sicherstellen, dass der Service korrekt mit der API interagiert und die Daten verarbeitet.

## Aufgaben

1. **Setup**: Erstellt eine Testumgebung für den `OrderService` und verwendet den `HttpClient` mit dem `HttpClientTestingModule`.
2. **Testfall 1**: Schreibt einen Test, um zu überprüfen, ob `getOrderById` eine Bestellung korrekt zurückgibt, wenn die API eine gültige Antwort sendet.
3. **Testfall 2**: Simuliert eine 500-Fehlerantwort und stellt sicher, dass der Dienst eine benutzerfreundliche Fehlermeldung zurückgibt.
4. **Testfall 3**: Implementiert einen Test, der prüft, ob ein ungültiger Bestell-ID-Wert (z.B. `null`) korrekt abgefangen wird und der Dienst eine entsprechende Fehlermeldung ausgibt.

## Vorgefertigter Code

```typescript
// order.service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable, throwError } from 'rxjs';
import { catchError } from 'rxjs/operators';

interface Order {
  id: number;
  product: string;
  quantity: number;
}

@Injectable({
  providedIn: 'root'
})
export class OrderService {
  private apiUrl = 'https://fakestoreapi.com/carts';

  constructor(private http: HttpClient) {}

  getOrderById(id: number): Observable<Order> {
    if (!id) {
      return throwError('Invalid order ID');
    }
    return this.http.get<Order>(`${this.apiUrl}/${id}`)
      .pipe(
        catchError(error => {
          console.error('Error fetching order', error);
          return throwError('An error occurred while fetching the order.');
        })
      );
  }
}