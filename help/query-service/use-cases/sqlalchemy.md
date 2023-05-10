---
title: Plattformdaten mit Python und SQLAlchemiy verwalten
description: Erfahren Sie, wie Sie mit SQLAlchemy Ihre Platform-Daten mit Python anstelle von SQL verwalten können.
exl-id: 9fba942e-9b3d-4efe-ae94-aed685025dea
source-git-commit: 8644b78c947fd015f6a169c9440b8d1df71e5e17
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 7%

---

# Verwalten von Platform-Daten mithilfe von [!DNL Python] und [!DNL SQLAlchemy]

Erfahren Sie, wie Sie SQLAlchemie für mehr Flexibilität bei der Verwaltung Ihrer Adobe Experience Platform-Daten einsetzen können. Für diejenigen, die mit SQL nicht so vertraut sind, kann SQLAlchemy die Entwicklungszeit bei der Arbeit mit relationalen Datenbanken erheblich verbessern. Dieses Dokument enthält Anweisungen und Beispiele zum Verbinden [!DNL SQLAlchemy] zu Query Service hinzu und beginnen Sie mit der Verwendung von Python, um mit Ihren Datenbanken zu interagieren.

[!DNL SQLAlchemy] ist ein Objekt Relational Mapper (ORM) und ein [!DNL Python] Codebibliothek, mit der in einer SQL-Datenbank gespeicherte Daten in [!DNL Python] Objekte. Anschließend können Sie CRUD-Vorgänge für Daten ausführen, die im Platform Data Lake gespeichert sind, indem Sie [!DNL Python] Code. Dadurch entfällt die Notwendigkeit, Daten nur mit PSQL zu verwalten.

## Erste Schritte

Um die erforderlichen Anmeldeinformationen zum Verbinden von [!DNL SQLAlchemy] mit Experience Platform zu erhalten, benötigen Sie Zugriff auf den Arbeitsbereich „Abfragen“ in der Platform-Benutzeroberfläche. Wenden Sie sich an Ihren Organisationsadministrator, wenn Sie derzeit keinen Zugriff auf den Arbeitsbereich &quot;Abfragen&quot;haben.

## [!DNL Query Service] Anmeldeinformationen {#credentials}

Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei der Platform-Benutzeroberfläche an und wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Abfragen]** und dann **[!UICONTROL Anmeldeinformationen]** aus. Eine vollständige Anleitung zum Auffinden Ihrer Anmeldedaten finden Sie in der [Handbuch zu Anmeldeinformationen](../ui/credentials.md).

![Die Registerkarte &quot;Berechtigungen&quot;mit ablaufenden Anmeldeinformationen für Query Service wurde hervorgehoben.](../images/use-cases/credentials.png)

Obwohl Port 80 der empfohlene Anschluss für eine Verbindung mit Query Service ist, können Sie auch Port 5432 verwenden.

>[!IMPORTANT]
>
>Wenn Sie ablaufende Anmeldeinformationen (wie in der Abbildung oben gezeigt) verwenden, um eine Verbindung zu Query Service herzustellen, läuft die Sitzungsdauer für Ihre Verbindung nach dem in den Einstellungen Ihres Unternehmens festgelegten Zeitraum ab. Standardmäßig beträgt dieser Zeitraum 24 Stunden. Weitere Informationen finden Sie in der Dokumentation . [Client mit nicht ablaufenden Anmeldedaten verbinden](../ui/credentials.md#non-expiring-credentials)oder wie [die Sitzungsdauer für Ihre ablaufenden Anmeldedaten ändern](../ui/credentials.md#expiring-credentials).

Sobald Sie Zugriff auf Ihre QS-Anmeldeinformationen haben, öffnen Sie Ihre [!DNL Python] Editor der Wahl.

### Anmeldeinformationen in speichern [!DNL Python] {#store-credentials}

In [!DNL Python] Editor, importieren Sie die `urllib.parse.quote` und speichern Sie jede Berechtigungsvariable als Parameter. Die `urllib.parse` bietet eine Standardoberfläche, über die URL-Zeichenfolgen in Komponenten unterteilt werden können. Die Anführungsfunktion ersetzt Sonderzeichen in der URL-Zeichenfolge, damit die Daten für die Verwendung als URL-Komponenten sicher sind. Nachfolgend finden Sie ein Beispiel für den erforderlichen Code:

>[!TIP]
>
>Verwendung [!DNL Python]drei Anführungszeichen, um Ihre mehrzeilige Kennwortzeichenfolge einzugeben.

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
>Das Kennwort, das Sie für die Verbindung angeben [!DNL SQLAlchemy] zu Experience Platform läuft ab, wenn Sie ablaufende Anmeldedaten verwenden. Siehe [Abschnitt &quot;Anmeldeinformationen&quot;](#credentials) für weitere Informationen.

### Erstellen einer Engine-Instanz [#create-engine]

Importieren Sie nach der Erstellung der Variablen die `create_engine` und erstellen Sie eine Zeichenfolge, um Ihre Query Service-Anmeldedaten in SQLAlchemiy zu kompilieren und zu formatieren. Die `create_engine` -Funktion wird dann zum Erstellen einer Engine-Instanz verwendet.

>[!NOTE]
>
>`create_engine`gibt eine Instanz einer Engine zurück. Die Verbindung zu Query Service wird jedoch erst geöffnet, wenn eine Abfrage aufgerufen wird, für die eine Verbindung erforderlich ist.

SSL muss beim Zugriff auf Platform mit Clients von Drittanbietern aktiviert sein. Verwenden Sie als Teil Ihrer Engine die `connect_args` , um zusätzliche Suchbegriffargumente einzugeben. Es wird empfohlen, den SSL-Modus auf `require`. Siehe [Dokumentation zu SSL-Modi](../clients/ssl-modes.md) für weitere Informationen zu akzeptierten Werten.

Im folgenden Beispiel wird die [!DNL Python] Code, der zum Initialisieren einer Engine und einer Verbindungszeichenfolge erforderlich ist.

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
>Das Kennwort, das Sie für die Verbindung angeben [!DNL SQLAlchemy] zu Experience Platform läuft ab, wenn Sie ablaufende Anmeldedaten verwenden. Siehe [Abschnitt &quot;Anmeldeinformationen&quot;](#credentials) für weitere Informationen.

Sie können jetzt Platform-Daten mit [!DNL Python]. Das folgende Beispiel gibt ein Array von Query Service-Tabellennamen zurück.

```python
from sqlalchemy import inspect
insp = inspect(engine)
print(insp.get_table_names())
```
