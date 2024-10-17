# Lösung für Übung 1: Integration von Unit- und End-to-End-Tests in eine CI/CD-Pipeline

## Lösungsvorschlag

Hier findest du eine detaillierte Schritt-für-Schritt-Anleitung zur Implementierung der CI/CD-Pipeline mit Unit- und End-to-End-Tests für das Angular-Projekt.

### 1. Klonen des Projekts

Zuerst klonen wir das Angular-Projekt und installieren alle benötigten Abhängigkeiten:

```bash
git clone https://github.com/example/angular-task-manager.git
cd angular-task-manager
npm install
```

### 2. Erstellen der .gitlab-ci.yml Datei
Erstelle oder bearbeite die .gitlab-ci.yml Datei im Root-Verzeichnis des Projekts. Die Datei sollte die Stages build, unit-test und e2e-test enthalten.

Hier ist ein vollständiger Lösungsvorschlag für die .gitlab-ci.yml Datei:

```yaml
stages:
  - build
  - unit-test
  - e2e-test

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

### 3. Optimierung: Hinzufügen von Caching
Um die Build-Zeit zu verkürzen, kannst du Caching für node_modules aktivieren. Hier ist eine optimierte Version der .gitlab-ci.yml Datei:

```yaml
stages:
  - build
  - unit-test
  - e2e-test

cache:
  paths:
    - node_modules/

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