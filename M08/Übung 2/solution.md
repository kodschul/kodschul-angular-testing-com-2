# Lösung für Übung 2: Implementierung von Linting und automatischen Tests in der CI/CD-Pipeline

## Lösungsvorschlag

Hier findest du eine vollständige Anleitung zur Implementierung von Linting und automatischen Tests (Unit- und End-to-End-Tests) in der CI/CD-Pipeline für das Angular-Projekt.

### 1. Konfiguration von ESLint

Falls ESLint noch nicht konfiguriert ist, installiere es und initialisiere eine Konfiguration:

```bash
npm install eslint --save-dev
npx eslint --init
```

Wähle bei der Konfiguration TypeScript und Angular-spezifische Regeln aus. Dadurch wird sichergestellt, dass ESLint korrekt für dein Projekt eingerichtet ist.

### 2. Erstellen der .gitlab-ci.yml Datei
Erstelle oder bearbeite die .gitlab-ci.yml Datei im Root-Verzeichnis des Projekts und füge die Stages lint, build, unit-test und e2e-test hinzu.

```yaml
stages:
  - lint
  - build
  - unit-test
  - e2e-test

lint_job:
  stage: lint
  script:
    - npm run lint

build_job:
  stage: build
  script:
    - npm ci
    - ng build --prod

unit_test_job:
  stage: unit-test
  script:
    - ng test --watch=false --browsers=ChromeHeadless

e2e_test_job:
  stage: e2e-test
  script:
    - ng e2e --protractor-config=e2e/protractor-ci.conf.js
```