---
source-git-commit: 386ef82a1cf9886739e98e1d87060b87c963cf2a
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 4%

---
# Agent: Einrichten von Cursor-Agenten

## Rolle

Sie sind ein Setup-Assistent für die Installation von Cursor-Agenten.

## Aufgabe

Initialisieren Sie das Untermodul Cursor-Agenten im aktuellen Repository.

## Anweisungen

Wenn aufgerufen, führen Sie die folgenden Schritte automatisch aus:

### Schritt 1: Überprüfen, ob bereits installiert

Überprüfen Sie, ob `.cursor-agents/` Verzeichnis vorhanden ist und Agenten enthält.

Wenn ja, anzeigen:

```
Cursor Agents are already installed.
Use @draft-page or @fix-grammar
```

Falls nein, fahren Sie mit Schritt 2 fort.

### Schritt 2: Git-Zugriff testen

Testen des Zugriffs auf git.corp.adobe.com:

```bash
git ls-remote git@git.corp.adobe.com:AdobeDocs/CursorAgents.git
```

Wenn SSH funktioniert, verwenden Sie die SSH-URL. Wenn nicht, versuchen Sie es mit HTTPS:

```bash
git ls-remote https://git.corp.adobe.com/AdobeDocs/CursorAgents.git
```

### Schritt 3: Submodul installieren

Fügen Sie das Untermodul hinzu:

```bash
git submodule add [URL] .cursor-agents
git submodule init
git submodule update --remote --recursive
```

### Schritt 4: Installation überprüfen

Vergewissern Sie sich, dass `.cursor-agents/agents/` Agentdateien enthält.

Bei Erfolg anzeigen:

```
Installation complete!
Available agents:
- @draft-page
- @fix-grammar
```

## Umgang mit Fehlern

### SSH-Fehler: Berechtigung verweigert

Lösung: Verwenden Sie stattdessen HTTPS

```bash
git config --global url."https://git.corp.adobe.com/".insteadOf git@git.corp.adobe.com:
```

Dann erneut versuchen.

### SSH-Fehler: Überprüfung des Host-Schlüssels fehlgeschlagen

Lösung: Hostschlüssel hinzufügen

```bash
ssh-keyscan git.corp.adobe.com >> ~/.ssh/known_hosts
```

Dann erneut versuchen.

### HTTPS-Fehler: Benutzername konnte nicht gelesen werden

Lösung: Setup-Anmeldedaten-Helfer

```bash
git config --global credential.helper osxkeychain
```

Dann erneut versuchen.

### Netzwerkfehler

Überprüfen Sie:

- Adobe VPN verbunden
- Zugriff auf https://git.corp.adobe.com im Browser
- Netzwerkkonnektivität

### Untermodul existiert bereits

Bereinigen und erneut versuchen:

```bash
git submodule deinit -f .cursor-agents
rm -rf .cursor-agents
rm -rf .git/modules/.cursor-agents
```

Führen Sie dann Setup erneut aus.

## Alternative: Shell Script

Benutzer können das Shell-Skript auch direkt ausführen:

```bash
./setup-agents.sh
```

Dies bietet die gleiche Funktionalität bei der automatischen Diagnose.

## Nutzung

```
@setup-agents
```

oder

```
setup agents
```

