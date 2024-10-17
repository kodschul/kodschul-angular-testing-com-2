# Übung: Testen eines Datenservices mit Observables

## Kontext
Der Datenservice `ProductService` lädt Produktdaten aus einer API. Ihr müsst sicherstellen, dass die Methode `getProducts` die Daten korrekt abruft und verarbeitet. Außerdem soll getestet werden, ob die Methode bei einem Fehler eine entsprechende Fehlermeldung ausgibt.

**Hinweis**: In dieser Übung wird eine funktionierende API verwendet, die eine Liste von Produkten zurückgibt. Ihr müsst sicherstellen, dass der Service korrekt mit der API interagiert und die Daten verarbeitet.

## Aufgaben

1. **Setup**: Erstellt eine Testumgebung für den `ProductService` und verwendet den `HttpClient` mit dem `HttpClientTestingModule`.
2. **Testfall 1**: Schreibt einen Test, um zu überprüfen, ob `getProducts` ein Array von Produkten zurückgibt, wenn die API erfolgreich antwortet.
3. **Testfall 2**: Simuliert eine Fehlermeldung von der API (404 Not Found) und stellt sicher, dass die Methode `getProducts` entsprechend reagiert und eine Fehlermeldung zurückgibt.
4. **Testfall 3**: Implementiert einen Test, der prüft, ob bei einem leeren API-Response das Observable korrekt leer bleibt.

## Vorgefertigter Code

```typescript
// product.service.ts
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable, throwError } from 'rxjs';
import { catchError } from 'rxjs/operators';

interface Product {
  id: number;
  name: string;
  price: number;
}

@Injectable({
  providedIn: 'root'
})
export class ProductService {
  private apiUrl = 'https://fakestoreapi.com/products';

  constructor(private http: HttpClient) {}

  getProducts(): Observable<Product[]> {
    return this.http.get<Product[]>(this.apiUrl)
      .pipe(
        catchError(error => {
          console.error('Error fetching products', error);
          return throwError('Error fetching products, please try again later.');
        })
      );
  }
}