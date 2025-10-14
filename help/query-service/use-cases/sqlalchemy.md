---
title: Verwalten von Experience Platform-Daten mithilfe von Python und SQLAlchemy
description: Erfahren Sie, wie Sie mit SQLAlchemy Ihre Experience Platform-Daten mit Python anstelle von SQL verwalten können.
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '578'
ht-degree: 0%

---

# Verwalten von Experience Platform-Daten mithilfe von [!DNL Python] und [!DNL SQLAlchemy]

Erfahren Sie, wie Sie SQLAlchemy für mehr Flexibilität bei der Verwaltung Ihrer Adobe Experience Platform-Daten verwenden. Für diejenigen, die mit SQL nicht so vertraut sind, kann SQLAlchemy die Entwicklungszeit bei der Arbeit mit relationalen Datenbanken erheblich verbessern. Dieses Dokument enthält Anweisungen und Beispiele zum Verbinden von [!DNL SQLAlchemy] mit dem Abfrage-Service und zum Beginnen der Verwendung von Python für die Interaktion mit Ihren Datenbanken.

[!DNL SQLAlchemy] ist ein Object Relational Mapper (ORM) und eine [!DNL Python] Code-Bibliothek, die in einer SQL-Datenbank gespeicherte Daten in [!DNL Python] Objekte übertragen kann. Sie können dann CRUD-Vorgänge für Daten durchführen, die im Data Lake von Experience Platform gespeichert sind, indem Sie [!DNL Python] Code verwenden. Dadurch entfällt die Notwendigkeit, Daten nur noch mit PSQL zu verwalten.

## Erste Schritte

Um die erforderlichen Anmeldeinformationen zum Verbinden von [!DNL SQLAlchemy] mit Experience Platform zu erhalten, benötigen Sie Zugriff auf den Arbeitsbereich „Abfragen“ in der Experience Platform-Benutzeroberfläche. Wenden Sie sich an den Admin Ihrer Organisation, wenn Sie derzeit keinen Zugriff auf den Arbeitsbereich „Abfragen“ haben.

## [!DNL Query Service] {#credentials}

Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei der Experience Platform-Benutzeroberfläche an und wählen **[!UICONTROL Abfragen]** im linken Navigationsbereich aus, gefolgt von **[!UICONTROL Anmeldeinformationen]**. Eine vollständige Anleitung zum Auffinden Ihrer Anmeldedaten finden Sie im [Anmeldedaten-Handbuch](../ui/credentials.md).

![Die Registerkarte „Anmeldeinformationen“ mit hervorgehobenen ablaufenden Anmeldeinformationen für den Abfrage-Service.](../images/use-cases/credentials.png)

Obwohl Port 80 der empfohlene Port für eine Verbindung mit dem Abfrage-Service ist, können Sie auch Port 5432 verwenden.

>[!IMPORTANT]
>
>Wenn Sie ablaufende Anmeldeinformationen verwenden (wie im Bild oben gezeigt), um eine Verbindung zum Abfrage-Service herzustellen, läuft die Sitzungsdauer für Ihre Verbindung nach dem in den Einstellungen Ihres Unternehmens festgelegten Zeitraum ab. Standardmäßig beträgt dieser Zeitraum 24 Stunden. In der Dokumentation erfahren Sie, wie Sie [einen Client mit nicht ablaufenden Anmeldeinformationen verbinden](../ui/credentials.md#non-expiring-credentials) oder [die Sitzungsdauer für Ihre ablaufenden Anmeldeinformationen ändern](../ui/credentials.md#expiring-credentials).

Sobald Sie Zugriff auf Ihre QS-Anmeldedaten haben, öffnen Sie Ihren [!DNL Python] Editor Ihrer Wahl.

### Speichern von Anmeldeinformationen in [!DNL Python] {#store-credentials}

Importieren Sie in Ihrem [!DNL Python]-Editor die `urllib.parse.quote`-Bibliothek und speichern Sie jede Berechtigungsvariable als Parameter. Das `urllib.parse` Modul bietet eine Standardschnittstelle zum Unterteilen von URL-Zeichenfolgen in Komponenten. Die Anführungsfunktion ersetzt Sonderzeichen in der URL-Zeichenfolge, um die Daten zur Verwendung als URL-Komponenten sicher zu machen. Ein Beispiel für den erforderlichen Code finden Sie unten:

>[!TIP]
>
>Verwenden Sie die dreifachen Anführungszeichen von [!DNL Python], um Ihre mehrzeilige Kennwortzeichenfolge einzugeben.

```python
from urllib.parse import quote

host = "<YOUR_HOST>"

port = "<YOUR_PORT>"

dbname = "<YOUR_DATABASE>"

user = "<YOUR_USERNAME>"

password = quote('''
<YOUR_PASSWORD>
''')
```

>[!NOTE]
>
>Das Kennwort für die Verbindung von [!DNL SQLAlchemy] mit Experience Platform läuft ab, wenn Sie ablaufende Anmeldeinformationen verwenden. Weitere Informationen finden [&#x200B; im Abschnitt &#x200B;](#credentials) .

### Erstellen einer Engine-Instanz [#create-engine]

Nachdem die Variablen erstellt wurden, importieren Sie die Funktion `create_engine` und erstellen Sie eine Zeichenfolge, um Ihre Anmeldeinformationen für den Abfrage-Service in SQLAlchemy zu kompilieren und zu formatieren. Die `create_engine` Funktion wird dann verwendet, um eine Engine-Instanz zu erstellen.

>[!NOTE]
>
>`create_engine`Gibt eine Instanz einer Engine zurück. Es öffnet jedoch die Verbindung zum Abfrage-Service erst, wenn eine Abfrage aufgerufen wird, für die eine Verbindung erforderlich ist.

SSL muss beim Zugriff auf Experience Platform über Drittanbieter-Clients aktiviert sein. Verwenden Sie als Teil Ihrer Engine die `connect_args` , um zusätzliche Keyword-Argumente einzugeben. Es wird empfohlen, den SSL-Modus auf `require` festzulegen. Weitere Informationen zu den akzeptierten Werten finden [&#x200B; in &#x200B;](../clients/ssl-modes.md) Dokumentation zu SSL-Modi .

Im folgenden Beispiel wird der [!DNL Python] Code angezeigt, der zum Initialisieren einer Engine und einer Verbindungszeichenfolge erforderlich ist.

```python
from sqlalchemy import create_engine

db_string = "postgresql://{user}:{password}@{host}:{port}/{dbname}".format(
    user=user,
    password=password,
    host=host,
    port = port,
    dbname = dbname
)

engine = create_engine(db_string, connect_args={'sslmode':'require'})
```

>[!NOTE]
>
>Das Kennwort für die Verbindung von [!DNL SQLAlchemy] mit Experience Platform läuft ab, wenn Sie ablaufende Anmeldeinformationen verwenden. Weitere Informationen finden [&#x200B; im Abschnitt &#x200B;](#credentials) .

Sie können jetzt Experience Platform-Daten mit [!DNL Python] abfragen. Das folgende Beispiel gibt ein Array von Query Service-Tabellennamen zurück.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
