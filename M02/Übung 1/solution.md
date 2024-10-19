
# Lösungsvorschlag für Übung 1: Schreiben einer benutzerdefinierten Pipe

## Lösung der `TruncatePipe`

Hier ist die Implementierung der `TruncatePipe`, die eine Zeichenkette kürzt und ein optionales Suffix anhängt.

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'truncate'
})
export class TruncatePipe implements PipeTransform {
  transform(value: string, maxLength: number, suffix: string = '...'): string {
    if (!value) return '';
    if (value.length <= maxLength) return value;
    return value.substring(0, maxLength) + suffix;
  }
}
```

### Erklärung
- Die Pipe prüft zunächst, ob der Wert (`value`) existiert. Ist dies nicht der Fall, wird eine leere Zeichenkette zurückgegeben.
- Wenn die Länge der Zeichenkette kleiner oder gleich der maximal erlaubten Länge (`maxLength`) ist, wird die ursprüngliche Zeichenkette zurückgegeben.
- Wenn die Zeichenkette gekürzt werden muss, wird sie auf die angegebene Länge geschnitten und das Suffix (standardmäßig `"..."`) wird angehängt.

## Verwendung der Pipe in der `WordListComponent`

Die `WordListComponent` verwendet die `TruncatePipe`, um die angezeigten Sätze zu kürzen. Hier ist der vollständige Code der Komponente und der HTML-Vorlage:

### `word-list.component.ts`

```typescript
import { Component } from '@angular/core';

@Component({
  selector: 'app-word-list',
  templateUrl: './word-list.component.html',
  styleUrls: ['./word-list.component.css']
})
export class WordListComponent {
  sentences: string[] = [
    'Angular is a platform for building mobile and desktop web applications.',
    'Use Angular to quickly build and deploy applications.',
    'This is a sample sentence to test the truncate pipe.'
  ];
}
```

### `word-list.component.html`

```html
<ul>
  <li *ngFor="let sentence of sentences">
    {{ sentence | truncate: 20 }}
  </li>
</ul>
```

### Erklärung
- Die Komponente enthält eine Liste von Sätzen (`sentences`), die in der HTML-Vorlage iteriert wird.
- Jeder Satz wird durch die `TruncatePipe` geleitet und auf maximal 20 Zeichen gekürzt.
- Wenn ein Satz mehr als 20 Zeichen hat, wird `"..."` als Suffix angehängt.