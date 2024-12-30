---
title: Verbinden von einem Jupyter-Notebook mit Data Distiller
description: Erfahren Sie, wie Sie von einem Jupyter-Notebook aus eine Verbindung zu Data Distiller herstellen.
exl-id: e6238b00-aaeb-40c0-a90f-9aebb1a1c421
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 0%

---

# Verbinden von einem Jupyter-Notebook mit Data Distiller

Um Ihre Pipelines für maschinelles Lernen mit hochwertigen Kundenerlebnisdaten anzureichern, müssen Sie zunächst eine Verbindung zu Data Distiller von [!DNL Jupyter Notebooks] herstellen. In diesem Dokument werden die Schritte zum Herstellen einer Verbindung zu Data Distiller von einem [!DNL Python]-Notebook in Ihrer maschinellen Lernumgebung beschrieben.

## Erste Schritte

In diesem Handbuch wird davon ausgegangen, dass Sie mit interaktiven [!DNL Python]-Notebooks vertraut sind und Zugriff auf eine Notebook-Umgebung haben. Das Notebook kann in einer Cloud-basierten Umgebung für maschinelles Lernen oder lokal mit [[!DNL Jupyter Notebook]](https://jupyter.org/) gehostet werden.

### Abrufen von Verbindungsberechtigungen {#obtain-credentials}

Um eine Verbindung zu Data Distiller und anderen Adobe Experience Platform-Services herzustellen, benötigen Sie Experience Platform-API-Anmeldedaten. API-Anmeldeinformationen können in der [Adobe Developer Console](https://developer.adobe.com/console/home) von einer Person erstellt werden, die Entwicklerzugriff auf die Experience Platform hat. Es wird empfohlen, eine OAuth2-API-Berechtigung speziell für datenwissenschaftliche Workflows zu erstellen und einen Adobe-Systemadministrator Ihres Unternehmens anzuweisen, die Berechtigung einer Rolle mit entsprechenden Berechtigungen zuzuweisen.

Detaillierte [ zum Erstellen von API Anmeldeinformationen und zum Abrufen der erforderlichen Berechtigungen finden Sie unter ](../../../landing/api-authentication.md)Authentifizieren und Zugreifen auf Experience Platform-APIs“.

Zu den empfohlenen Berechtigungen für Data Science gehören:

- Sandbox(es), die für die Datenwissenschaft verwendet werden (normalerweise `prod`)
- Datenmodellierung: [!UICONTROL Schemata verwalten]
- Daten-Management: [!UICONTROL Datensätze verwalten]
- Datenaufnahme: [!UICONTROL Quellen anzeigen]
- Ziele: [!UICONTROL Datensatzziele verwalten und aktivieren]
- Abfrage-Service: [!UICONTROL Abfragen verwalten]

Standardmäßig wird einer Rolle (und den dieser Rolle zugewiesenen API-Anmeldeinformationen) der Zugriff auf alle gekennzeichneten Daten verweigert. Abhängig von den Data Governance-Richtlinien des Unternehmens kann ein Systemadministrator der Rolle Zugriff auf bestimmte gekennzeichnete Daten gewähren, die für die Verwendung in der Datenwissenschaft als geeignet erachtet werden. Platform-Kundinnen und -Kunden sind dafür verantwortlich, die Richtlinien für den Zugriff auf Kennzeichnungen und die Einhaltung relevanter Vorschriften und organisatorischer Richtlinien angemessen zu verwalten.

### Speichern von Anmeldeinformationen in einer separaten Konfigurationsdatei {#store-credentials}

Um Ihre Anmeldeinformationen sicher zu halten, sollten Sie es vermeiden, Anmeldeinformationen direkt in Ihren Code zu schreiben. Bewahren Sie stattdessen die Anmeldeinformationen in einer separaten Konfigurationsdatei auf und lesen Sie die Werte ein, die zum Herstellen einer Verbindung mit der Experience Platform und Data Distiller erforderlich sind.

Beispielsweise können Sie eine Datei mit dem Namen `config.ini` erstellen und die folgenden Informationen (sowie alle anderen Informationen wie Datensatz-IDs, die zwischen Sitzungen gespeichert werden sollten) einfügen:

```ini
[Credential]
ims_org_id=<YOUR_IMS_ORG_ID>
sandbox_name=<YOUR_SANDBOX_NAME>
client_id=<YOUR_CLIENT_ID>
client_secret=<YOUR_CLIENT_SECRET>
scopes=openid, AdobeID, read_organizations, additional_info.projectedProductContext, session
tech_acct_id=<YOUR_TECHNICAL_ACCOUNT_ID>
```

In Ihrem -Notebook können Sie dann die Informationen zu den Anmeldeinformationen mithilfe des `configParser`-Pakets aus der standardmäßigen [!DNL Python]-Bibliothek in den Speicher lesen:

```python
from configparser import ConfigParser

# Create a ConfigParser object to read and store information from config.ini
config = ConfigParser()
config_path = '<PATH_TO_YOUR_CONFIG.INI_FILE>'
config.read(config_path)
```

Anschließend können Sie wie folgt auf Werte der Anmeldeinformationen in Ihrem Code verweisen:

```python
org_id = config.get('Credential', 'ims_org_id')
```

## Installieren der AEP Python-Bibliothek {#install-python-library}

[aepp](https://github.com/adobe/aepp/tree/main) ist eine von Adobe verwaltete Open-Source-[!DNL Python], die Funktionen zum Herstellen einer Verbindung mit Data Distiller und zum Senden von Abfragen sowie zum Anfordern an andere Experience Platform-Services bereitstellt. Die `aepp`-Bibliothek wiederum basiert auf dem PostgreSQL-Datenbankadapterpaket, das für interaktive Daten-Distiller-Abfragen `psycopg2` ist. Es ist möglich, nur mit `psycopg2` eine Verbindung zu Data Distiller herzustellen und Experience Platform-Datensätze abzufragen, `aepp` bietet jedoch mehr Komfort und zusätzliche Funktionen, um Anfragen an alle Experience Platform-API-Services zu senden.

Um `aepp` und `psycopg2` in Ihrer Umgebung zu installieren oder zu aktualisieren, können Sie den `%pip` magic-Befehl in Ihrem Notebook verwenden:

```python
%pip install --upgrade aepp
%pip install --upgrade psycopg2-binary
```

Anschließend können Sie die `aepp`-Bibliothek mit Ihren Anmeldedaten mithilfe des folgenden Codes konfigurieren:

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

## Erstellen einer Verbindung mit Data Distiller {#create-connection}

Nachdem `aepp` mit Ihren Anmeldeinformationen konfiguriert wurde, können Sie den folgenden Code verwenden, um eine Verbindung zu Data Distiller herzustellen und eine interaktive Sitzung zu starten:

```python
from aepp import queryservice

dd_conn = queryservice.QueryService().connection()
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

Anschließend können Sie die Datensätze in Ihrer Experience Platform-Sandbox abfragen. Angesichts der ID eines Datensatzes, den Sie abfragen möchten, können Sie den entsprechenden Tabellennamen aus dem Katalog-Service abrufen und Abfragen für die Tabelle ausführen:

```python
table_name = 'ecommerce_events'
simple_query = f'''SELECT * FROM {table_name} LIMIT 5'''
dd_cursor.query(simple_query)
```

### Herstellen einer Verbindung zu einem einzelnen Datensatz für eine schnellere Abfrageleistung {#connect-to-single-dataset}

Standardmäßig stellt die Data Distiller-Verbindung eine Verbindung zu allen Datensätzen in Ihrer Sandbox her. Für schnellere Abfragen und eine reduzierte Ressourcennutzung können Sie stattdessen eine Verbindung zu einem bestimmten Datensatz von Interesse herstellen. Sie können dies tun, indem Sie die `dbname` im Data Distiller-Verbindungsobjekt in `{sandbox}:{table_name}` ändern:

```python
from aepp import queryservice

sandbox = config.get('Credential', 'sandbox_name')
table_name = 'ecommerce_events'

dd_conn = queryservice.QueryService().connection()
dd_conn['dbname'] = f'{sandbox}:{table_name}'
dd_cursor = queryservice.InteractiveQuery2(dd_conn)
```

## Nächste Schritte

Durch das Lesen dieses Dokuments haben Sie gelernt, wie Sie in Ihrer maschinellen Lernumgebung von einem [!DNL Python]-Notebook aus eine Verbindung zu Data Distiller herstellen können. Der nächste Schritt beim Erstellen von Funktions-Pipelines vom Experience Platform zur Bereitstellung benutzerdefinierter Modelle in Ihrer maschinellen Lernumgebung besteht darin, [Datensätze zu durchsuchen und zu analysieren](./exploratory-analysis.md).
