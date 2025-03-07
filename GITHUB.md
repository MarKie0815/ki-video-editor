# GitHub Repository Anleitung

Dieses Dokument enthält Anweisungen zum Erstellen und Verwalten des GitHub-Repositories für dieses Projekt.

## Repository auf GitHub erstellen

1. Gehen Sie zu GitHub (https://github.com) und melden Sie sich an.
2. Klicken Sie auf "New" oder "+" → "New repository".
3. Geben Sie als Repository-Namen "video-editor-ki" ein.
4. Fügen Sie eine Beschreibung hinzu: "Video Editor mit KI-gestützter Spracherkennung"
5. Wählen Sie die Option "Public" oder "Private" je nach Ihren Anforderungen.
6. Lassen Sie die Option "Initialize this repository with a README" deaktiviert.
7. Klicken Sie auf "Create repository".

## Lokales Repository mit GitHub verbinden

Nachdem Sie das Repository auf GitHub erstellt haben, führen Sie folgende Befehle aus:

```bash
# Verbinden des lokalen Repositories mit dem Remote-Repository
git remote add origin https://github.com/MarKie0815/video-editor-ki.git

# Pushen des Codes zum Remote-Repository
git push -u origin main
```

## Aktualisieren des Repositories

Nach Änderungen am Code können Sie Ihre Änderungen wie folgt aktualisieren:

```bash
# Statusprüfung der Änderungen
git status

# Änderungen hinzufügen
git add .

# Commit mit Beschreibung erstellen
git commit -m "Beschreibung der Änderungen"

# Änderungen auf GitHub hochladen
git push
```

## Wichtiger Hinweis

Die folgenden Dateien und Verzeichnisse werden nicht auf GitHub gespeichert (in .gitignore aufgeführt):
- `.env` (enthält Ihren API-Schlüssel)
- `venv/` (virtuelle Umgebung)
- `input/`, `output/`, `edited/`, `temp/` (Videodateien und temporäre Dateien)
- `__pycache__/` (Python-Cache)
- `*.pyc`, `*.pyo` (kompilierte Python-Dateien)
- `.DS_Store` (macOS-spezifische Dateien)

## Branches und Collaboration

Für neue Features:
```bash
# Neuen Branch erstellen
git checkout -b feature/neues-feature

# Nach Abschluss wieder in den main-Branch wechseln
git checkout main

# Branch zusammenführen
git merge feature/neues-feature
```