# Übung 2: Implementierung von Linting und automatischen Tests in der CI/CD-Pipeline

## Ziel
In dieser Übung wirst du Linting und automatische Tests (Unit- und End-to-End-Tests) in eine CI/CD-Pipeline für ein Angular-Projekt integrieren. Die Pipeline soll sicherstellen, dass jede Änderung am Code auf Syntax- und Stilfehler geprüft und anschließend getestet wird, bevor sie ins Haupt-Repository gemergt wird.

## Kontext
Du arbeitest an einem Angular-Projekt, das eine Anwendung zur Verwaltung von Aufgaben (Task-Manager) beinhaltet. Um die Codequalität zu sichern, möchtest du eine Pipeline erstellen, die Linting und Tests automatisch bei jedem Commit ausführt. Hierbei verwendest du `eslint` für das Linting und Angular-Standardtests für Unit- und E2E-Tests.

## Schritte

1. **Konfiguration von ESLint**:
   - Falls ESLint noch nicht im Projekt konfiguriert ist, installiere es und initialisiere eine Konfiguration:
     ```bash
     npm install eslint --save-dev
     npx eslint --init
     ```
   - Richte ESLint so ein, dass es TypeScript-Dateien und Angular-spezifische Regeln überprüft.

2. **Erstellen der `.gitlab-ci.yml` Datei**:
   - Erstelle oder bearbeite die `.gitlab-ci.yml` Datei im Root-Verzeichnis des Projekts.
   - Füge die folgenden Stages hinzu:
     - **Lint Stage**: Um den Code auf Syntax- und Stilfehler zu überprüfen.
     - **Build Stage**: Um das Angular-Projekt zu kompilieren.
     - **Unit-Test Stage**: Um Unit-Tests mit Karma und Jasmine auszuführen.
     - **E2E-Test Stage**: Um End-to-End-Tests (E2E) mit Protractor durchzuführen.

3. **Hinzufügen der Linting-Stage**:
   - Füge der `.gitlab-ci.yml` Datei eine Lint-Stage hinzu, die den Befehl `npm run lint` ausführt.

4. **Hinzufügen der Build-, Unit-Test- und E2E-Test-Stages**:
   - Erweitere die Pipeline, indem du Stages für das Kompilieren (`ng build`), Unit-Tests (`ng test`) und E2E-Tests (`ng e2e`) hinzufügst.
   - Stelle sicher, dass die Unit-Tests im Headless-Modus laufen (`--browsers=ChromeHeadless`) und dass die E2E-Tests mit der richtigen Protractor-Konfiguration ausgeführt werden (`--protractor-config=e2e/protractor-ci.conf.js`).

5. **Commit und Pipeline testen**:
   - Committe die `.gitlab-ci.yml` Datei und pushe die Änderungen in dein GitLab-Repository:
     ```bash
     git add .gitlab-ci.yml
     git commit -m "Add linting and testing stages to CI/CD pipeline"
     git push origin main
     ```
   - Überprüfe, ob die Pipeline korrekt ausgeführt wird und alle Stages (Lint, Build, Unit-Test und E2E-Test) erfolgreich abgeschlossen werden.

## Zusätzliche Hinweise
- Überprüfe, ob alle Abhängigkeiten in der `package.json` vorhanden sind, insbesondere `eslint` für Linting und die Angular-CLI für Builds und Tests.
- Stelle sicher, dass die Protractor-Konfiguration in der Datei `e2e/protractor-ci.conf.js` korrekt eingerichtet ist, um die Tests im Headless-Modus auszuführen.
