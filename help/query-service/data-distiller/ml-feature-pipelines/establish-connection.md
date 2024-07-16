---
title: Verbindung zu Data Distiller über ein Jupyter-Notebook herstellen
description: Erfahren Sie, wie Sie von einem Jupyter-Notebook aus eine Verbindung mit Data Distiller herstellen.
exl-id: e6238b00-aaeb-40c0-a90f-9aebb1a1c421
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# Verbindung zu Data Distiller über ein Jupyter-Notebook herstellen

Um Ihre Pipelines für maschinelles Lernen mit hochwertigen Kundenerlebnisdaten anzureichern, müssen Sie zunächst von [!DNL Jupyter Notebooks] aus eine Verbindung mit Data Distiller herstellen. In diesem Dokument werden die Schritte zum Herstellen einer Verbindung mit Data Distiller über ein [!DNL Python] -Notebook in Ihrer Umgebung für maschinelles Lernen beschrieben.

## Erste Schritte

In diesem Handbuch wird davon ausgegangen, dass Sie mit interaktiven [!DNL Python] Notebooks vertraut sind und Zugriff auf eine Notebook-Umgebung haben. Das Notebook kann in einer Cloud-basierten Umgebung für maschinelles Lernen oder lokal mit [[!DNL Jupyter Notebook]](https://jupyter.org/) gehostet werden.

### Verbindungsberechtigungen abrufen {#obtain-credentials}

Um eine Verbindung zu Data Distiller und anderen Adobe Experience Platform-Diensten herzustellen, benötigen Sie eine Experience Platform-API-Berechtigung. API-Anmeldeinformationen können in der [Adobe Developer Console](https://developer.adobe.com/console/home) von einem Entwickler-Benutzer erstellt werden, der Zugriff auf die Experience Platform hat. Es wird empfohlen, eine Oauth2-API-Berechtigung speziell für Datenwissenschafts-Workflows zu erstellen und einen Adobe-Systemadministrator Ihres Unternehmens zu haben, die Berechtigung einer Rolle mit entsprechenden Berechtigungen zuzuweisen.

Detaillierte Anweisungen zum Erstellen einer API-Berechtigung und zum Abrufen der erforderlichen Berechtigungen finden Sie unter [Authentifizieren und Zugreifen auf Experience Platform-APIs](../../../landing/api-authentication.md) .

Zu den empfohlenen Berechtigungen für die Datenwissenschaft gehören:

- Sandbox(s), die für die Datenwissenschaft verwendet wird (normalerweise `prod`)
- Datenmodellierung: [!UICONTROL Schemaverwaltung]
- Datenverwaltung: [!UICONTROL Datensätze verwalten]
- Datenerfassung: [!UICONTROL Quellen anzeigen]
- Ziele: [!UICONTROL Verwalten und Aktivieren von Datensatzzielen]
- Query Service: [!UICONTROL Abfragen verwalten]

Standardmäßig ist der Zugriff auf gekennzeichnete Daten durch eine Rolle (und API-Anmeldeinformationen, die dieser Rolle zugewiesen sind) blockiert. Vorbehaltlich der Data Governance-Richtlinien der Organisation kann ein Systemadministrator der Rolle Zugriff auf bestimmte gekennzeichnete Daten gewähren, die für die Nutzung der Datenwissenschaft als angemessen erachtet werden. Platform-Kunden sind dafür verantwortlich, den Zugriff auf Beschriftungen und Richtlinien entsprechend zu verwalten, um die relevanten Vorschriften und organisatorischen Richtlinien zu erfüllen.

### Anmeldeinformationen in einer separaten Konfigurationsdatei speichern {#store-credentials}

Um Ihre Anmeldedaten sicher zu halten, sollten Sie vermeiden, Anmeldeinformationen direkt in Ihren Code zu schreiben. Behalten Sie stattdessen die Anmeldeinformationen in einer separaten Konfigurationsdatei und lesen Sie die Werte, die für die Verbindung mit der Experience Platform und Data Distiller erforderlich sind.

Sie können beispielsweise eine Datei mit dem Namen `config.ini` erstellen und die folgenden Informationen (zusammen mit allen anderen Informationen, wie z. B. Datensatz-IDs, die für das Speichern zwischen Sitzungen nützlich sind) einschließen:

```ini
[Credential]
ims_org_id=<YOUR_IMS_ORG_ID>
sandbox_name=<YOUR_SANDBOX_NAME>
client_id=<YOUR_CLIENT_ID>
client_secret=<YOUR_CLIENT_SECRET>
scopes=openid, AdobeID, read_organizations, additional_info.projectedProductContext, session
tech_acct_id=<YOUR_TECHNICAL_ACCOUNT_ID>
```

Im Notebook können Sie dann die Anmeldeinformationen mithilfe des `configParser` -Pakets aus der standardmäßigen [!DNL Python] -Bibliothek in den Speicher lesen:

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)
```

Anschließend können Sie in Ihrem Code auf die Berechtigungswerte wie folgt verweisen:

```python
org_id = config.get('Credential', 'ims_org_id')
```

## Installieren der APP-Python-Bibliothek {#install-python-library}

[aepp](https://github.com/adobe/aepp/tree/main) ist eine von Adobe verwaltete Open-Source-Bibliothek [!DNL Python], die Funktionen zum Herstellen einer Verbindung zu Data Distiller und zum Senden von Abfragen sowie zum Senden von Anfragen an andere Experience Platform-Dienste bietet. Die Bibliothek &quot;`aepp`&quot; wiederum nutzt für interaktive Data Distiller-Abfragen das PostgreSQL-Datenbankadapterpaket `psycopg2` . Es ist möglich, nur mit `psycopg2` eine Verbindung zu Data Distiller herzustellen und Experience Platform-Datensätze abzufragen. `aepp` bietet jedoch mehr Komfort und zusätzliche Funktionen, um Anfragen an alle Experience Platform-API-Dienste zu senden.

Um `aepp` und `psycopg2` in Ihrer Umgebung zu installieren oder zu aktualisieren, können Sie den Zauberbefehl `%pip` in Ihrem Notebook verwenden:

```python
%pip install --upgrade aepp
%pip install --upgrade psycopg2-binary
```

Anschließend können Sie die `aepp` -Bibliothek mit Ihren Anmeldedaten konfigurieren, indem Sie den folgenden Code verwenden:

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)

# Configure aepp with your credentials
import aepp

aepp.configure(
  org_id=config.get('Credential', 'ims_org_id'),
  sandbox=config.get('Credential', 'sandbox_name'),
  client_id=config.get('Credential', 'client_id'), 
  secret=config.get('Credential', 'client_secret'),
  scopes=config.get('Credential', 'scopes'),
  tech_id=config.get('Credential', 'tech_acct_id')
)
```

## Herstellen einer Verbindung zu Data Distiller {#create-connection}

Nachdem `aepp` mit Ihren Anmeldedaten konfiguriert wurde, können Sie wie folgt eine Verbindung zu Data Distiller herstellen und eine interaktive Sitzung starten:

```python
from aepp import queryservice

dd_conn = queryservice.QueryService().connection()
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

Anschließend können Sie die Datensätze in Ihrer Experience Platform-Sandbox abfragen. Angesichts der ID eines Datensatzes, den Sie abfragen möchten, können Sie den entsprechenden Tabellennamen aus dem Catalog Service abrufen und Abfragen auf der Tabelle ausführen:

```python
table_name = 'ecommerce_events'
simple_query = f'''SELECT * FROM {table_name} LIMIT 5'''
dd_cursor.query(simple_query)
```

### Verbindung zu einem Datensatz herstellen, um die Abfrageleistung zu beschleunigen {#connect-to-single-dataset}

Standardmäßig stellt die Data Distiller-Verbindung eine Verbindung zu allen Datensätzen in Ihrer Sandbox her. Um Abfragen zu beschleunigen und die Ressourcennutzung zu reduzieren, können Sie stattdessen eine Verbindung zu einem bestimmten Datensatz herstellen, der von Interesse ist. Ändern Sie dazu den `dbname` im Data Distiller-Verbindungsobjekt in `{sandbox}:{table_name}`:

```python
from aepp import queryservice

sandbox = config.get('Credential', 'sandbox_name')
table_name = 'ecommerce_events'

dd_conn = queryservice.QueryService().connection()
dd_conn['dbname'] = f'{sandbox}:{table_name}'
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie erfahren, wie Sie in Ihrer Umgebung für maschinelles Lernen von einem [!DNL Python] -Notebook aus eine Verbindung mit Data Distiller herstellen können. Der nächste Schritt beim Erstellen von Funktions-Pipelines aus Experience Platform, um benutzerdefinierte Modelle in Ihrer maschinellen Lernumgebung zu speisen, besteht darin, Ihre Datensätze zu untersuchen und zu analysieren](./exploratory-analysis.md).[
