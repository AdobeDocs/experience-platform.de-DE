---
title: Verbindung zu Data Distiller über ein Jupyter-Notebook herstellen
description: Erfahren Sie, wie Sie von einem Jupyter-Notebook aus eine Verbindung mit Data Distiller herstellen.
exl-id: e6238b00-aaeb-40c0-a90f-9aebb1a1c421
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 1%

---

# Verbindung zu Data Distiller über ein Jupyter-Notebook herstellen

Um Ihre Pipelines für maschinelles Lernen mit hochwertigen Kundenerlebnisdaten anzureichern, müssen Sie zunächst eine Verbindung zu Data Distiller über herstellen [!DNL Jupyter Notebooks]. In diesem Dokument werden die Schritte zum Herstellen einer Verbindung mit Data Distiller über eine [!DNL Python] Notebook in Ihrer Arbeitsumgebung für maschinelles Lernen.

## Erste Schritte

In diesem Handbuch wird davon ausgegangen, dass Sie mit interaktiven [!DNL Python] Notebooks und Zugriff auf eine Notebook-Umgebung. Das Notebook kann in einer Cloud-basierten Umgebung für maschinelles Lernen oder lokal mit [[!DNL Jupyter Notebook]](https://jupyter.org/).

### Verbindungsberechtigungen abrufen {#obtain-credentials}

Um eine Verbindung zu Data Distiller und anderen Adobe Experience Platform-Diensten herzustellen, benötigen Sie eine Experience Platform-API-Berechtigung. API-Anmeldeinformationen können im  [Adobe Developer-Konsole](https://developer.adobe.com/console/home) durch einen Entwickler-Zugriff auf die Experience Platform. Es wird empfohlen, eine Oauth2-API-Berechtigung speziell für Datenwissenschafts-Workflows zu erstellen und einen Adobe-Systemadministrator Ihres Unternehmens zu haben, die Berechtigung einer Rolle mit entsprechenden Berechtigungen zuzuweisen.

Siehe [Experience Platform-APIs authentifizieren und aufrufen](../../../landing/api-authentication.md) für detaillierte Anweisungen zum Erstellen einer API-Berechtigung und zum Abrufen der erforderlichen Berechtigungen.

Zu den empfohlenen Berechtigungen für die Datenwissenschaft gehören:

- Sandbox(s), die für die Datenwissenschaft verwendet wird (normalerweise `prod`)
- Datenmodellierung: [!UICONTROL Verwalten von Schemas]
- Data Management: [!UICONTROL Datensätze verwalten]
- Datenerfassung: [!UICONTROL Quellen anzeigen]
- Ziele: [!UICONTROL Verwalten und Aktivieren von Datensatzzielen]
- Query Service: [!UICONTROL Abfragen verwalten]

Standardmäßig ist der Zugriff auf gekennzeichnete Daten durch eine Rolle (und API-Anmeldeinformationen, die dieser Rolle zugewiesen sind) blockiert. Vorbehaltlich der Data Governance-Richtlinien der Organisation kann ein Systemadministrator der Rolle Zugriff auf bestimmte gekennzeichnete Daten gewähren, die für die Nutzung der Datenwissenschaft als angemessen erachtet werden. Platform-Kunden sind dafür verantwortlich, den Zugriff auf Beschriftungen und Richtlinien entsprechend zu verwalten, um die relevanten Vorschriften und organisatorischen Richtlinien zu erfüllen.

### Anmeldeinformationen in einer separaten Konfigurationsdatei speichern {#store-credentials}

Um Ihre Anmeldedaten sicher zu halten, sollten Sie vermeiden, Anmeldeinformationen direkt in Ihren Code zu schreiben. Behalten Sie stattdessen die Anmeldeinformationen in einer separaten Konfigurationsdatei und lesen Sie die Werte, die für die Verbindung mit der Experience Platform und Data Distiller erforderlich sind.

Als Beispiel können Sie eine Datei mit dem Namen `config.ini` und enthalten die folgenden Informationen (zusammen mit allen anderen Informationen, wie z. B. Datensatz-IDs, die für das Speichern zwischen Sitzungen nützlich wären):

```ini
[Credential]
ims_org_id=<YOUR_IMS_ORG_ID>
sandbox_name=<YOUR_SANDBOX_NAME>
client_id=<YOUR_CLIENT_ID>
client_secret=<YOUR_CLIENT_SECRET>
scopes=openid, AdobeID, read_organizations, additional_info.projectedProductContext, session
tech_acct_id=<YOUR_TECHNICAL_ACCOUNT_ID>
```

Im Notebook können Sie dann die Anmeldeinformationen mithilfe der `configParser` Paket aus dem Standard [!DNL Python] -Bibliothek:

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

[aepp](https://github.com/adobe/aepp/tree/main) ist eine von Adobe verwaltete Open-Source-Software [!DNL Python] -Bibliothek, die Funktionen zum Herstellen einer Verbindung zu Data Distiller und zum Senden von Abfragen bereitstellt, z. B. zum Erstellen von Anforderungen an andere Experience Platform-Dienste. Die `aepp` Bibliothek wiederum basiert auf dem PostgreSQL-Datenbankadapterpaket  `psycopg2` für interaktive Data Distiller-Abfragen. Es ist möglich, eine Verbindung zu Data Distiller herzustellen und Experience Platform-Datensätze abzufragen mit `psycopg2` allein, aber `aepp` bietet mehr Komfort und zusätzliche Funktionen, um Anfragen an alle Experience Platform-API-Dienste zu stellen.

Installieren oder Aktualisieren `aepp` und `psycopg2` In Ihrer Umgebung können Sie die `%pip` Magie-Befehl in Ihrem Notebook:

```python
%pip install --upgrade aepp
%pip install --upgrade psycopg2-binary
```

Anschließend können Sie die `aepp` -Bibliothek mit Ihren Anmeldedaten unter Verwendung des folgenden Codes:

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

Einmal `aepp` mit Ihren Anmeldedaten konfiguriert ist, können Sie den folgenden Code verwenden, um eine Verbindung zu Data Distiller herzustellen und eine interaktive Sitzung wie folgt zu starten:

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

Standardmäßig stellt die Data Distiller-Verbindung eine Verbindung zu allen Datensätzen in Ihrer Sandbox her. Um Abfragen zu beschleunigen und die Ressourcennutzung zu reduzieren, können Sie stattdessen eine Verbindung zu einem bestimmten Datensatz herstellen, der von Interesse ist. Dazu können Sie die Variable `dbname` im Data Distiller-Verbindungsobjekt zu `{sandbox}:{table_name}`:

```python
from aepp import queryservice

sandbox = config.get('Credential', 'sandbox_name')
table_name = 'ecommerce_events'

dd_conn = queryservice.QueryService().connection()
dd_conn['dbname'] = f'{sandbox}:{table_name}'
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie erfahren, wie Sie über eine [!DNL Python] Notebook in Ihrer Arbeitsumgebung für maschinelles Lernen. Der nächste Schritt beim Erstellen von Feature Pipelines aus dem Experience Platform, um benutzerdefinierte Modelle in Ihrer maschinellen Lernumgebung zu speisen, besteht darin, [Datensätze untersuchen und analysieren](./exploratory-analysis.md).
