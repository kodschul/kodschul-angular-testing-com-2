# Übung 1: Integration von Unit- und End-to-End-Tests in eine CI/CD-Pipeline

## Ziel
In dieser Übung wirst du eine CI/CD-Pipeline für ein Angular-Projekt erstellen, die sowohl Unit-Tests als auch End-to-End (E2E)-Tests ausführt. Diese Pipeline soll automatisch bei jedem Commit ausgeführt werden, um sicherzustellen, dass alle Komponenten und Funktionalitäten der Anwendung korrekt funktionieren.

## Kontext
Du arbeitest an einem Angular-Projekt, das einen Aufgabenmanager erstellt (ähnlich wie eine To-Do-Liste). Die Anwendung bietet Funktionen wie das Hinzufügen, Bearbeiten und Löschen von Aufgaben. Um die Qualität des Codes sicherzustellen, sollen Unit- und End-to-End-Tests in die CI/CD-Pipeline integriert werden.

## Schritte

1. **Klonen des Projekts**:
   Klone das Angular-Projekt und installiere alle benötigten Abhängigkeiten:
   ```bash
   git clone https://github.com/example/angular-task-manager.git
   cd angular-task-manager
   npm install
   ```

2. **Vorbereitung der Tests**:

    - Stelle sicher, dass Unit-Tests für Komponenten wie TaskComponent und TaskService vorhanden sind.
    - E2E-Tests sind bereits mit Protractor konfiguriert. Vergewissere dich, dass die Konfiguration für einen Headless-Browser bereit ist.

3. Erstellen und Anpassen der .gitlab-ci.yml Datei:

    - Erstelle eine .gitlab-ci.yml Datei im Root-Verzeichnis des Projekts.
    - Füge die folgenden Stages hinzu:
        - Build Stage: Um das Projekt zu kompilieren.
        - Unit-Test Stage: Um Unit-Tests auszuführen.
        - E2E-Test Stage: Um die E2E-Tests im Headless-Modus auszuführen.

4. Pipeline testen:

    - Führe einen Commit durch und pushe die Änderungen in dein GitLab-Repository.
    - Überprüfe in GitLab, ob die Pipeline die Tests wie erwartet ausführt.

5. Fehlerbehebung:

    - Falls die Tests fehlschlagen, überprüfe die Logs in GitLab und behebe die Fehler entsprechend (z.B. fehlende Abhängigkeiten oder Probleme mit der Browser-Konfiguration).

## Zusätzliche Hinweise
- Stelle sicher, dass die Konfiguration für die E2E-Tests in der Datei e2e/protractor-ci.conf.js korrekt für einen Headless-Browser eingerichtet ist.
- Überprüfe, ob alle Abhängigkeiten in der package.json vorhanden sind, insbesondere für die Tests (z.B. karma, jasmine, protractor).