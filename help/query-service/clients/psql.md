---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Anbinden an PSQL
topic: connect
translation-type: tm+mt
source-git-commit: 3b710e7a20975880376f7e434ea4d79c01fa0ce5
workflow-type: tm+mt
source-wordcount: '170'
ht-degree: 71%

---


# Anbinden an PSQL

PSQL is a command-line interface that comes when you install [!DNL Postgres] on your machine. Sie können es installieren, indem Sie die nachfolgenden Anweisungen befolgen.

## Installieren von Postgres auf einem Mac

Öffnen Sie ein Terminal-Fenster und geben Sie die folgenden drei Befehle ein:

```shell
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

```shell
brew install postgres
```

```shell
which psql
```

Diese Befehle sollten folgende Ausgabe liefern:

```shell
/usr/local/bin/psql
```

## Install [!DNL Postgres] on a PC

Download and install [!DNL Postgres] from this [location](https://www.postgresql.org/download/windows/).

Bearbeiten Sie die Pfadvariable:

![Bild](../images/clients/psql/path.png)

Add the two lines shown that include &quot;[!DNL Postgres].&quot;

Speichern Sie Ihre Updates, öffnen Sie eine Eingabeaufforderung und geben Sie Folgendes ein:

```shell
psql -V
```

Die Ausgabe sollte in etwa wie folgt lauten:

```shell
psql (PostgreSQL) 9.5.14
```

## PSQL verbinden und [!DNL Query Service]

Return to the [!DNL Platform] UI on the *[!UICONTROL Connect BI Tools]* page.

Click **[!UICONTROL copy]** for *[!UICONTROL PSQL Command]*.

![Bild](../images/clients/psql/connect-bi.png)

>[!IMPORTANT]: Verwenden Sie auf einem PC einen Texteditor, um in der Zeichenfolge des Befehls die Zeilenumbrüche zu entfernen, und kopieren Sie dann die Zeichenfolge.

Fügen Sie die Befehlszeichenfolge in das Fenster eines Terminals bzw. einer Eingabeaufforderung ein und drücken Sie die Eingabetaste.

Die Ausgabe sollte in folgt lauten:

```shell
psql (10.5, server 0.1.0)
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-GCM-SHA384, bits: 256, compression: off)
Type "help" for help.
all=>
```

Wird für die Versionsnummer nicht mindestens 10.5 angegeben, müssen Sie Version 10.5 oder höher herunterladen.