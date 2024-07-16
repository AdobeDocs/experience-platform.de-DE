---
title: Plattformdaten mit Python und SQLAlchemiy verwalten
description: Erfahren Sie, wie Sie mit SQLAlchemy Ihre Platform-Daten mit Python anstelle von SQL verwalten können.
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: 8644b78c947fd015f6a169c9440b8d1df71e5e17
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 7%

---

# Verwalten von Platform-Daten mit [!DNL Python] und [!DNL SQLAlchemy]

Erfahren Sie, wie Sie SQLAlchemie für mehr Flexibilität bei der Verwaltung Ihrer Adobe Experience Platform-Daten einsetzen können. Für diejenigen, die mit SQL nicht so vertraut sind, kann SQLAlchemy die Entwicklungszeit bei der Arbeit mit relationalen Datenbanken erheblich verbessern. In diesem Dokument finden Sie Anweisungen und Beispiele zum Verbinden von [!DNL SQLAlchemy] mit Query Service und zum Verwenden von Python für die Interaktion mit Ihren Datenbanken.

[!DNL SQLAlchemy] ist ein Objekt Relational Mapper (ORM) und eine [!DNL Python] Code-Bibliothek, die in einer SQL-Datenbank gespeicherte Daten in [!DNL Python] -Objekte übertragen können. Anschließend können Sie CRUD-Vorgänge für Daten ausführen, die im Platform Data Lake gespeichert sind, indem Sie den Code [!DNL Python] verwenden. Dadurch entfällt die Notwendigkeit, Daten nur mit PSQL zu verwalten.

## Erste Schritte

Um die erforderlichen Anmeldeinformationen zum Verbinden von [!DNL SQLAlchemy] mit Experience Platform zu erhalten, benötigen Sie Zugriff auf den Arbeitsbereich „Abfragen“ in der Platform-Benutzeroberfläche. Wenden Sie sich an Ihren Organisationsadministrator, wenn Sie derzeit keinen Zugriff auf den Arbeitsbereich &quot;Abfragen&quot;haben.

## [!DNL Query Service] Anmeldedaten {#credentials}

Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei der Platform-Benutzeroberfläche an und wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Abfragen]** und dann **[!UICONTROL Anmeldeinformationen]** aus. Eine vollständige Anleitung zum Auffinden Ihrer Anmeldedaten finden Sie im [Benutzerhandbuch zu Anmeldedaten](../ui/credentials.md).

![Die Registerkarte &quot;Berechtigungen&quot;mit ablaufenden Anmeldeinformationen für Query Service wurde hervorgehoben.](../images/use-cases/credentials.png)

Obwohl Port 80 der empfohlene Anschluss für eine Verbindung mit Query Service ist, können Sie auch Port 5432 verwenden.

>[!IMPORTANT]
>
>Wenn Sie ablaufende Anmeldeinformationen (wie in der Abbildung oben gezeigt) verwenden, um eine Verbindung zu Query Service herzustellen, läuft die Sitzungsdauer für Ihre Verbindung nach dem in den Einstellungen Ihres Unternehmens festgelegten Zeitraum ab. Standardmäßig beträgt dieser Zeitraum 24 Stunden. In der Dokumentation erfahren Sie, wie Sie [einen Client mit nicht ablaufenden Anmeldedaten verbinden](../ui/credentials.md#non-expiring-credentials) oder wie Sie [ die Sitzungsdauer für Ihre ablaufenden Anmeldedaten ändern](../ui/credentials.md#expiring-credentials).

Sobald Sie Zugriff auf Ihre QS-Anmeldeinformationen haben, öffnen Sie den gewünschten [!DNL Python]-Editor.

### Anmeldeinformationen in [!DNL Python] speichern {#store-credentials}

Importieren Sie in Ihren [!DNL Python]-Editor die Bibliothek `urllib.parse.quote` und speichern Sie jede Berechtigungsvariable als Parameter. Das Modul `urllib.parse` bietet eine Standardschnittstelle, um URL-Zeichenfolgen in Komponenten zu unterteilen. Die Anführungsfunktion ersetzt Sonderzeichen in der URL-Zeichenfolge, damit die Daten für die Verwendung als URL-Komponenten sicher sind. Nachfolgend finden Sie ein Beispiel für den erforderlichen Code:

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
>Das Passwort, das Sie zum Verbinden von [!DNL SQLAlchemy] mit Experience Platform angeben, läuft ab, wenn Sie ablaufende Anmeldedaten verwenden. Weitere Informationen finden Sie im Abschnitt [Anmeldedaten](#credentials) .

### Erstellen einer Engine-Instanz [#create-engine]

Nachdem die Variablen erstellt wurden, importieren Sie die Funktion `create_engine` und erstellen Sie eine Zeichenfolge, um Ihre Query Service-Anmeldedaten in SQLAlchemiy zu kompilieren und zu formatieren. Die Funktion `create_engine` wird dann zum Erstellen einer Engine-Instanz verwendet.

>[!NOTE]
>
>`create_engine`gibt eine Instanz einer Engine zurück. Die Verbindung zu Query Service wird jedoch erst geöffnet, wenn eine Abfrage aufgerufen wird, für die eine Verbindung erforderlich ist.

SSL muss beim Zugriff auf Platform mit Clients von Drittanbietern aktiviert sein. Verwenden Sie als Teil Ihrer Engine den `connect_args` , um zusätzliche Suchbegriffargumente einzugeben. Es wird empfohlen, den SSL-Modus auf `require` festzulegen. Weitere Informationen zu akzeptierten Werten finden Sie in der Dokumentation zu [SSL-Modi](../clients/ssl-modes.md) .

Im folgenden Beispiel wird der Code [!DNL Python] angezeigt, der zum Initialisieren einer Engine und einer Verbindungszeichenfolge erforderlich ist.

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
>Das Passwort, das Sie zum Verbinden von [!DNL SQLAlchemy] mit Experience Platform angeben, läuft ab, wenn Sie ablaufende Anmeldedaten verwenden. Weitere Informationen finden Sie im Abschnitt [Anmeldedaten](#credentials) .

Sie können jetzt Platform-Daten mit [!DNL Python] abfragen. Das folgende Beispiel gibt ein Array von Query Service-Tabellennamen zurück.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
