
# Linting eines Angular-Projekts

## Themen

1. Installieren von ESLint und EditorConfig
2. Lint-Fehler im Projekt finden und beheben

## 1. Installieren von ESLint und EditorConfig

### Live Coding Beispiel

**Schritt 1:** ESLint installieren

```bash
ng add @angular-eslint/schematics
```

**Schritt 2:** Konfigurationsdatei `.eslintrc.json` anpassen:

```json
{
  "root": true,
  "ignorePatterns": ["projects/**/*"],
  "overrides": [
    {
      "files": ["*.ts"],
      "parserOptions": {
        "project": ["tsconfig.json"],
        "createDefaultProgram": true
      },
      "extends": [
        "plugin:@angular-eslint/recommended",
        "eslint:recommended"
      ],
      "rules": {
        // Fügen Sie hier weitere Regeln hinzu
      }
    }
  ]
}
```

**Schritt 3:** EditorConfig einrichten

Erstellen Sie eine `.editorconfig`-Datei im Stammverzeichnis des Projekts:

```
root = true

[*]
indent_style = space
indent_size = 2
end_of_line = lf
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
```

## 2. Lint-Fehler im Projekt finden und beheben

### Live Coding Beispiel

**Schritt 1:** Linting im Projekt ausführen

```bash
ng lint
```

Dies überprüft das Projekt auf Linting-Fehler gemäß der `.eslintrc.json`-Konfiguration.

**Schritt 2:** Typische Lint-Fehler beheben

**Beispiel 1:** Einfache Formatierungsfehler

```typescript
// Vorher
const myVar:number = 5;

// Nachher
const myVar: number = 5;
```

**Beispiel 2:** Fehlendes Zugriffsmodifikator

```typescript
// Vorher
class MyClass {
  myProperty = 'test';
}

// Nachher
class MyClass {
  public myProperty = 'test';
}
```

**Test:**

```bash
ng lint
```