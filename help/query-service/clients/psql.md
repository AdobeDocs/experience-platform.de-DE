---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Verbindung mit PSQL
topic: connect
translation-type: tm+mt
source-git-commit: f5bc9beb59e83b0411d98d901d5055122a124d07
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 1%

---


# Verbindung mit PSQL

PSQL ist eine Befehlszeilenschnittstelle, die bei der Installation von Postgres auf Ihrem Computer verwendet wird. Sie können es installieren, indem Sie diese Anweisungen befolgen.

## Installieren von Postgres auf einem Mac

Öffnen Sie ein Terminalfenster und geben Sie die folgenden drei Befehle aus:

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```shell
brew install postgres
```

```shell
which psql
```

Nachdem Sie diese Befehle ausgegeben haben, sollten Sie Folgendes sehen:

```shell
/usr/local/bin/psql
```

## Installieren von Postgres auf einem PC

Laden Sie Postgres von diesem [Speicherort](https://www.postgresql.org/download/windows/)herunter und installieren Sie es.

Bearbeiten Sie die Pfadvariable:

![Bild](../images/clients/psql/path.png)

Hinzufügen die beiden angezeigten Zeilen, die &quot;Postgres&quot;enthalten.

Speichern Sie Ihre Updates, öffnen Sie eine Eingabeaufforderung und geben Sie Folgendes ein:

```shell
psql -V
```

Sie sollten so etwas sehen:

```shell
psql (PostgreSQL) 9.5.14
```

## Connect SQL und Abfrage-Dienst

Kehren Sie auf der Seite &quot;Connect BI Tools&quot;zur Plattform-Benutzeroberfläche zurück.

Klicken Sie auf **Kopieren** für &quot;PSQL-Befehl&quot;.

![Bild](../images/clients/psql/connect-bi.png)

>[!IMPORTANT]: Wenn Sie sich auf einem PC befinden, verwenden Sie einen Texteditor, um die Zeilenumbrüche in der Befehlszeichenfolge zu entfernen, und kopieren Sie dann die Zeichenfolge.

Fügen Sie die Befehlszeichenfolge in ein Terminal- oder Befehlsfenster ein und drücken Sie die Eingabetaste.

Das Ergebnis sollte wie folgt aussehen:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Wenn Sie nicht mindestens Version 10.5 sehen, müssen Sie diese Version oder neuer herunterladen.