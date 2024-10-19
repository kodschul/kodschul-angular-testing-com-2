
# Übung 1: Schreiben einer benutzerdefinierten Pipe

## Ziel
In dieser Übung wirst du eine benutzerdefinierte Pipe in Angular implementieren, die eine Zeichenkette auf eine bestimmte Länge kürzt und optional ein Suffix wie z.B. "..." anhängt.

## Aufgabenstellung
1. Erstelle eine benutzerdefinierte Pipe namens `TruncatePipe` in Angular. Diese Pipe soll eine Zeichenkette (`string`) als Eingabe nehmen und sie auf eine angegebene Länge kürzen (z.B. 10 Zeichen).
2. Wenn die Zeichenkette gekürzt wurde, soll ein ellipsis (`...`) oder ein optionaler, selbst festgelegter String als Suffix angehängt werden.
3. Verwende die Pipe in einer Komponente (`WordListComponent`), um eine Liste von Sätzen in der HTML-Datei zu kürzen.

## Vorgaben
Die folgenden Dateien sind bereits vorbereitet. Verwende diese Dateien für deine Implementierung:

### 1. `src/app/components/word-list.component.ts`

Hier findest du eine Komponente, die eine Liste von Sätzen darstellt. Die Pipe soll verwendet werden, um die Sätze in der HTML-Vorlage zu kürzen.

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

### 2. `src/app/components/word-list.component.html`

Verwende die Pipe `truncate` in der HTML-Vorlage, um die Sätze in der Liste zu kürzen.

```html
<ul>
  <li *ngFor="let sentence of sentences">
    {{ sentence | truncate: 20 }}
  </li>
</ul>
```

### Hinweise
- Verwende die `transform`-Methode der Pipe, um die Logik für das Kürzen der Zeichenkette zu implementieren.
- Achte darauf, dass die Pipe auch optional ein Suffix wie `"..."` an die gekürzte Zeichenkette anhängen kann.
- Teste die Pipe, indem du sie in der Komponente `WordListComponent` anwendest und überprüfe, ob die Sätze wie gewünscht gekürzt werden.

Viel Erfolg!