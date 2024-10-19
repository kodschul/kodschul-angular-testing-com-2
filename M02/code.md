
# Angular Testing und Debugging Schulung - Benutzerdefinierte Pipe

## Themen

1. Erstellen einer benutzerdefinierten Pipe
2. Pipe zum Filtern von Daten nach `locationId`
3. Fehlerhafte Pipe und wie man sie debuggt

## 1. Erstellen einer benutzerdefinierten Pipe

### Live Coding Beispiel

```bash
ng generate pipe CustomPipe
```

In der Datei `custom-pipe.pipe.ts`:

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'customPipe'
})
export class CustomPipe implements PipeTransform {
  transform(value: string): string {
    return value.toUpperCase();
  }
}
```

**Test:**

```typescript
import { CustomPipe } from './custom-pipe.pipe';

describe('CustomPipe', () => {
  const pipe = new CustomPipe();

  it('should transform text to uppercase', () => {
    expect(pipe.transform('hello')).toBe('HELLO');
  });
});
```

## 2. Pipe zum Filtern von Daten nach `locationId`

### Live Coding Beispiel

In der Datei `filter-by-location.pipe.ts`:

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'filterByLocation'
})
export class FilterByLocationPipe implements PipeTransform {
  transform(items: any[], locationId: number): any[] {
    if (!items || !locationId) {
      return items;
    }
    return items.filter(item => item.locationId === locationId);
  }
}
```

**Test:**

```typescript
import { FilterByLocationPipe } from './filter-by-location.pipe';

describe('FilterByLocationPipe', () => {
  const pipe = new FilterByLocationPipe();

  it('should filter items by locationId', () => {
    const items = [
      { name: 'Item 1', locationId: 1 },
      { name: 'Item 2', locationId: 2 }
    ];
    expect(pipe.transform(items, 1)).toEqual([{ name: 'Item 1', locationId: 1 }]);
  });

  it('should return empty array if no matching locationId', () => {
    const items = [
      { name: 'Item 1', locationId: 1 },
      { name: 'Item 2', locationId: 2 }
    ];
    expect(pipe.transform(items, 3)).toEqual([]);
  });
});
```

## 3. Fehlerhafte Pipe und wie man sie debuggt

### Beispiel für eine fehlerhafte Pipe

In der Datei `faulty-pipe.pipe.ts`:

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'faultyPipe'
})
export class FaultyPipe implements PipeTransform {
  transform(value: number): number {
    // Fehler: Division durch 0
    return value / 0;
  }
}
```

**Debugging:**

1. **Test erstellen**

```typescript
import { FaultyPipe } from './faulty-pipe.pipe';

describe('FaultyPipe', () => {
  const pipe = new FaultyPipe();

  it('should return Infinity for division by zero', () => {
    expect(pipe.transform(100)).toBe(Infinity);
  });
});
```

2. **Fehler beheben**

Aktualisieren der `faulty-pipe.pipe.ts`:

```typescript
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'faultyPipe'
})
export class FaultyPipe implements PipeTransform {
  transform(value: number): number {
    // Korrigierter Code: Vermeidung der Division durch 0
    return value !== 0 ? value / 2 : 0;
  }
}
```

**Test erneut ausführen, um sicherzustellen, dass der Fehler behoben wurde.**
