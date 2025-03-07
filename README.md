# Video Editor mit KI-gestützter Spracherkennung

Ein Python-basiertes Tool zur automatischen Bearbeitung von Videos basierend auf Spracherkennung. Das Tool erkennt Sprachsegmente, transkribiert diese und erstellt ein bearbeitetes Video, das nur die relevanten Sprachsegmente enthält.

## Features

- Automatische Sprachsegmenterkennung
- Transkription der Sprachsegmente mit OpenAI Whisper
- KI-basierte Filterung von redundanten Segmenten
- Beibehaltung der originalen Video- und Audioqualität
- Unterstützung für verschiedene Videoformate (MP4, AVI, MOV, MKV)
- Automatische Korrektur der Videorotation
- Generierung von Transkripten

## Voraussetzungen

- Python 3.8 oder höher
- FFmpeg
- OpenAI API Key

## Installation

1. Repository klonen:
```bash
git clone https://github.com/MarKie0815/video-editor-ki.git
cd video-editor-ki
```

2. Virtuelle Umgebung erstellen und aktivieren:
```bash
python -m venv venv
source venv/bin/activate  # Unter Windows: venv\Scripts\activate
```

3. Abhängigkeiten installieren:
```bash
pip install -r requirements.txt
```

4. Umgebungsvariablen konfigurieren:
```bash
cp .env.example .env
```
Tragen Sie Ihren OpenAI API Key in der `.env` Datei ein:
```
OPENAI_API_KEY=Ihr-API-Key
INPUT_FOLDER=input
```

## Verwendung

1. Erstellen Sie einen `input` Ordner und legen Sie dort Ihre Videodateien ab:
```bash
mkdir input
```

2. Führen Sie das Script aus:
```bash
python main.py
```

Das Script wird:
- Sprachsegmente in den Videos erkennen
- Diese mit Whisper transkribieren
- Redundante Segmente mit GPT-4 filtern
- Ein bearbeitetes Video erstellen
- Ein Transkript generieren

Die bearbeiteten Videos finden Sie im `edited` Ordner, die Transkripte im `output` Ordner.

### Erweiterte Funktionen

#### Statusbericht

Das Tool zeigt vor und nach der Verarbeitung einen detaillierten Statusbericht an:
- ✓ Erfolgreich verarbeitete Videos
- ○ Ausstehende Videos
- ⊘ Videos, die keine Bearbeitung benötigen
- ◎ Archivierte Videos (nicht mehr im Input-Ordner)
- ✗ Videos mit Fehlern

#### Vermeidung doppelter Verarbeitung

Videos, die bereits verarbeitet wurden, werden automatisch übersprungen. Ein Video gilt als verarbeitet, wenn:
- Die bearbeitete Videodatei im `edited` Ordner existiert
- Das Transkript im `output` Ordner existiert

#### Videos ohne Bearbeitung markieren

Sie können Videos markieren, die keine Bearbeitung benötigen:
1. Erstellen Sie eine Datei `no_edit.txt` im `input` Ordner
2. Fügen Sie die Dateinamen der Videos ein (ein Dateiname pro Zeile)

Diese Videos werden im Statusbericht angezeigt, aber nicht verarbeitet.

#### Temporäre Dateien

Standardmäßig werden temporäre Dateien für jedes Video in `temp/[video_name]/` gespeichert. Sie können dies ändern mit:

```bash
# Temporäre Dateien löschen nach der Verarbeitung
KEEP_TEMP_FILES=false python main.py

# Temporäre Dateien behalten (Standard)
python main.py
```

#### Projektumgebung zurücksetzen

Sie können die Projektumgebung zurücksetzen:

```bash
# Zurücksetzen, aber Input-Dateien behalten
python main.py --reset

# Vollständiges Zurücksetzen (auch Input-Dateien)
python main.py --reset --all
```

Dies löscht:
- Bearbeitete Videos im `edited` Ordner
- Temporäre Dateien im `temp` Ordner
- Transkripte im `output` Ordner
- "Keine Bearbeitung"-Markierungen
- Optional: Input-Dateien

#### Netzwerkfehler und Unterbrechungen

Das Tool ist robust gegenüber Netzwerkproblemen:

- **Automatische Wiederholungsversuche**: Bei Netzwerkfehlern werden API-Anfragen automatisch wiederholt (bis zu 3 Mal)
- **Exponentielles Backoff**: Zunehmende Wartezeiten zwischen Wiederholungsversuchen
- **Timeout-Handling**: Verhindert, dass das Programm bei langsamen Verbindungen hängen bleibt
- **Prozessunterbrechung**: Sie können die Verarbeitung jederzeit mit `Strg+C` unterbrechen und später fortsetzen

Bei einer Unterbrechung bleiben alle temporären Dateien erhalten, sodass die Verarbeitung beim nächsten Start an der letzten erfolgreichen Stelle fortgesetzt werden kann.

## Konfiguration

Die Konfiguration erfolgt über die `config.py` Datei:

- `input_folder`: Ordner für die Eingabevideos (Standard: "input")
- `output_folder`: Ordner für die Transkripte (Standard: "output")
- `supported_formats`: Unterstützte Videoformate (Standard: .mp4, .avi, .mov, .mkv)

## Technische Details

Das Tool verwendet:
- `webrtcvad` für die Sprachsegmenterkennung
- OpenAI Whisper für die Transkription
- GPT-4 für die Filterung von Redundanzen
- FFmpeg für die Videobearbeitung
- MoviePy für die Audioextraktion
- pydub für die Audioverarbeitung

## Fehlerbehandlung

Das Tool implementiert verschiedene Fehlerklassen:
- `VideoProcessingError`: Allgemeine Videoverarbeitungsfehler
- `AudioExtractionError`: Fehler bei der Audioextraktion
- `TranscriptionError`: Fehler bei der Transkription
- `VideoCreationError`: Fehler bei der Videoerstellung

## Lizenz

Dieses Projekt steht unter der MIT-Lizenz - siehe die [LICENSE](LICENSE) Datei für Details.

## Autor

Marcel Kiepe