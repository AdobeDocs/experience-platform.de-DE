---
keywords: Experience Platform;Startseite;Imagemap;Zuordnungssatz;Zuordnung;
solution: Experience Platform
title: Übersicht über Zuordnungssätze
topic: Übersicht
description: Erfahren Sie, wie Sie Zuordnungssätze mit Adobe Experience Platform Data Prep verwenden.
translation-type: tm+mt
source-git-commit: 4c06f621eb6fba8daa6501d56255cddbbcfdbda2
workflow-type: tm+mt
source-wordcount: '960'
ht-degree: 2%

---


# Übersicht über Zuordnungssätze

Ein Zuordnungssatz ist ein Satz von Zuordnungen, mit denen Daten von einem Schema in ein anderes umgewandelt werden. Dieses Dokument enthält Informationen zur Zusammensetzung von Zuordnungssätzen, einschließlich Eingabe-Schema, Ausgabe-Schema und Zuordnungen.

## Erste Schritte

Dieser Überblick erfordert ein funktionierendes Verständnis der folgenden Komponenten von Adobe Experience Platform:

- [Datenvorgabe](./home.md): Data Prep ermöglicht es Datenentwicklern, Daten dem Experience Data Model (XDM) zuzuordnen, umzuformen und zu validieren.
- [Datenflüsse](../dataflows/home.md): Datenflüsse sind eine Darstellung von Datenaufträgen, die Daten über die Plattform verschieben. Datenflüsse werden über verschiedene Dienste konfiguriert und unterstützen Sie dabei, Daten von Quellschnittstellen zu Zielgruppen-Datensätzen, zu [!DNL Identity] und [!DNL Profile] und zu [!DNL Destinations] zu verschieben.
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): Die Methoden, mit denen Daten gesendet werden können  [!DNL Experience Platform].
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.

## Syntax des Zuordnungssatzes

Ein Zuordnungssatz besteht aus einer ID, einem Schema für die Eingabe, einem Schema für die Ausgabe und einer Liste zugehöriger Zuordnungen.

Die folgende JSON-Datei ist ein Beispiel für einen typischen Zuordnungssatz:

```json
{
    "id" : "cbb0da769faa48fcb29e026a924ba29d",
    "name" : "Demo Mapping Set",
    "inputSchema" : {
        "id": "a167ff2947ff447ebd8bcf7ef6756232",
        "version": 0
    },
    "outputSchema": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/6dd1768be928c36d58ad4897219bb52d491671f966084bc0",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        }
    },
    "mappings": [
        {
            "sourceType": "ATTRIBUTE",
            "source": "Id",
            "destination": "_id",
            "name" : "Id",
            "description" : "Identifier field"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "FirstName",
            "destination": "person.name.firstName"
        },
        {
            "sourceType": "ATTRIBUTE",
            "source": "LastName",
            "destination": "person.name.lastName"
        }
    ]
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `id` | Eine eindeutige ID für den Zuordnungssatz. |
| `name` | Der Name des Zuordnungssatzes. |
| `inputSchema` | Das XDM-Schema für die eingehenden Daten. |
| `outputSchema` | Das XDM-Schema, an das die Eingabedaten angepasst wurden. |
| `mappings` | Ein Array von field-to-field-Zuordnungen vom Quell-Schema zum Ziel-Schema. |
| `sourceType` | Für jede aufgelistete Zuordnung gibt das `sourceType`-Attribut den Typ der Quelle an, der zugeordnet werden soll. Kann einer von `ATTRIBUTE`, `STATIC` oder `EXPRESSION` sein: <ul><li> `ATTRIBUTE` wird für jeden Wert im Quellpfad verwendet. </li><li>`STATIC` wird für Werte verwendet, die in den Zielpfad injiziert werden. Dieser Wert bleibt konstant und wird vom Quell-Schema nicht beeinflusst.</li><li> `EXPRESSION` wird für einen Ausdruck verwendet, der während der Laufzeit aufgelöst wird. Eine Liste der verfügbaren Ausdruck finden Sie im Handbuch [Zuordnungsfunktionen](./functions.md).</li> </ul> |
| `source` | Für jede aufgelistete Zuordnung gibt das `source`-Attribut das Feld an, das Sie zuordnen möchten. Weitere Informationen zur Konfiguration der Quelle finden Sie im Abschnitt [sources](#sources). |
| `destination` | Für jede aufgelistete Zuordnung gibt das `destination`-Attribut das Feld oder den Pfad zum Feld an, in dem der aus dem `source`-Feld extrahierte Wert platziert wird. Weitere Informationen zur Konfiguration Ihrer Ziele finden Sie im Abschnitt [Ziel](#destination). |
| `mappings.name` | (*Optional*) Ein Name für die Zuordnung. |
| `mappings.description` | (*Optional*) Eine Beschreibung der Zuordnung. |

## Zuordnungsquellen konfigurieren

Bei einer Zuordnung kann das `source` ein Feld, ein Ausdruck oder ein statischer Wert sein. Je nach dem angegebenen Quelltyp kann der Wert auf verschiedene Arten extrahiert werden.

### Feld in Spaltendaten

Verwenden Sie beim Zuordnen eines Felds in Spaltendaten, z. B. einer CSV-Datei, den Quelltyp `ATTRIBUTE`. Wenn das Feld &quot;`.`&quot;in seinem Namen enthält, verwenden Sie &quot;`\`&quot;, um dem Wert zu entkommen. Ein Beispiel für diese Zuordnung finden Sie unten:

**CSV-Beispieldatei:**

```csv
Full.Name, Email
John Smith, js@example.com
```

**Musterzuordnung**

```json
{
    "source": "Full.Name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Transformierte Daten**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Feld in verschachtelten Daten

Verwenden Sie beim Zuordnen eines Felds in verschachtelten Daten, z. B. einer JSON-Datei, den Quelltyp `ATTRIBUTE`. Wenn das Feld &quot;`.`&quot;in seinem Namen enthält, verwenden Sie &quot;`\`&quot;, um dem Wert zu entkommen. Ein Beispiel für diese Zuordnung finden Sie unten:

**JSON-Beispieldatei**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Musterzuordnung**

```json
{
    "source": "customerInfo.name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Transformierte Daten**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Feld innerhalb eines Arrays

Beim Zuordnen eines Felds in einem Array können Sie einen bestimmten Wert mithilfe eines Indexes abrufen. Verwenden Sie dazu den Quelltyp `ATTRIBUTE` und den Index des Werts, den Sie zuordnen möchten. Ein Beispiel für diese Zuordnung finden Sie unten:

**JSON-Beispieldatei**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Musterzuordnung**

```json
{
    "source": "customerInfo.emails[0].email",
    "destination": "pi.email",
    "sourceType": "ATTRIBUTE"
}
```

**Transformierte Daten**

```json
{
    "pi": {
        "email": "js@example.com"
    }
}
```

### Array mit Array oder Objekt mit Objekt

Mit dem Quelltyp `ATTRIBUTE` können Sie einem Array oder einem Objekt auch direkt ein Array zuordnen. Ein Beispiel für diese Zuordnung finden Sie unten:

**JSON-Beispieldatei**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Musterzuordnung**

```json
{
    "source": "customerInfo.emails",
    "destination": "pi.emailList",
    "sourceType": "ATTRIBUTE"
}
```

**Transformierte Daten**

```json
{
    "pi": {
        "emailList": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

### Iterative Vorgänge auf Arrays

Mithilfe des Quelltyps `ATTRIBUTE` können Sie Arrays iterativ durchlaufen und mithilfe eines Platzhalterindex (`[*]`) einem Zielgruppe-Schema zuordnen. Ein Beispiel für diese Zuordnung finden Sie unten:

**JSON-Beispieldatei**

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Musterzuordnung**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**Transformierte Daten**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

### Konstantenwert

Wenn Sie eine Konstante oder einen statischen Wert zuordnen möchten, verwenden Sie den Quelltyp `STATIC`.  Bei Verwendung des Quelltyps `STATIC` stellt das `source` den hartkodierten Wert dar, den Sie dem `destination` zuweisen möchten. Ein Beispiel für diese Zuordnung finden Sie unten:

**JSON-Beispieldatei**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Musterzuordnung**

```json
{
    "source": "CUSTOMER",
    "destination": "userType",
    "sourceType": "STATIC"
}
```

**Transformierte Daten**

```json
{
    "userType:": "CUSTOMER"
}
```

### Ausdruck

Wenn Sie einen Ausdruck zuordnen möchten, verwenden Sie den Quelltyp `EXPRESSION`. Eine Liste der zulässigen Funktionen finden Sie im Handbuch [Zuordnungsfunktionen](./functions.md). Bei Verwendung des Quelltyps `EXPRESSION` stellt das `source` die Funktion dar, die Sie auflösen möchten. Ein Beispiel für diese Zuordnung finden Sie unten:

**JSON-Beispieldatei**

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "email": "js@example.com"
}
```

**Musterzuordnung**

```json
{
    "source": "concat(upper(lastName), upper(firstName), now())",
    "destination": "pi.created",
    "sourceType": "EXPRESSION"
}
```

**Transformierte Daten**

```json
{
    "pi": {
        "created": "SMITHJOHNFri Sep 25 15:17:31 PDT 2020"
    }
}
```

## Konfigurieren von Zuordnungszielen

Bei einer Zuordnung ist `destination` der Ort, an dem der aus dem `source` extrahierte Wert eingefügt wird.

### Feld auf der Stammebene

Wenn Sie den Wert `source` der Stammebene Ihrer transformierten Daten zuordnen möchten, führen Sie das folgende Beispiel aus:

**JSON-Beispieldatei**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Musterzuordnung**

```json
{
    "source": "customerInfo.name",
    "destination": "name",
    "sourceType": "ATTRIBUTE"
}
```

**Transformierte Daten**

```json
{
    "name": "John Smith"
}
```

### Verschachteltes Feld

Wenn Sie den Wert `source` einem verschachtelten Feld in Ihren transformierten Daten zuordnen möchten, führen Sie das folgende Beispiel aus:

**JSON-Beispieldatei**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Musterzuordnung**

```json
{
    "source": "name",
    "destination": "pi.name",
    "sourceType": "ATTRIBUTE"
}
```

**Transformierte Daten**

```json
{
    "pi": {
        "name": "John Smith"
    }
}
```

### Feld an einem bestimmten Array-Index

Wenn Sie den Wert `source` einem bestimmten Index in einem Array Ihrer transformierten Daten zuordnen möchten, führen Sie das folgende Beispiel aus:

**JSON-Beispieldatei**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Musterzuordnung**

```json
{
    "source": "customerInfo.name",
    "destination": "piList[0]",
    "sourceType": "ATTRIBUTE"
}
```

**Transformierte Daten**

```json
{
    "piList": ["John Smith"]
}
```

### Iterativer Array-Vorgang

Wenn Sie Arrays iterativ durchlaufen und die Werte der Zielgruppe zuordnen möchten, können Sie einen Platzhalterindex (`[*]`) verwenden. Ein Beispiel dafür ist unten dargestellt:

```json
{
    "customerInfo": {
        "emails": [
            {
                "name": "John Smith",
                "email": "js@example.com"
            },
            {
                "name": "Jane Smith",
                "email": "jane@example.com"
            }
        ]
    }
}
```

**Musterzuordnung**

```json
{
    "source": "customerInfo.emails[*].name",
    "destination": "pi[*].names",
    "sourceType": "ATTRIBUTE"
}
```

**Transformierte Daten**

```json
{
    "pi": [
        {
            "names": {
                "name": "John Smith"
            } 
        },
        {
            "names": {
                "name": "Jane Smith"
            }
        }
    ]
}
```

## Nächste Schritte

Durch Lesen dieses Dokuments sollten Sie nun verstehen, wie Zuordnungssätze erstellt werden, einschließlich der Konfiguration einzelner Zuordnungen innerhalb eines Zuordnungssatzes. Weitere Informationen zu anderen Data Prep-Funktionen finden Sie im Abschnitt [Übersicht über die Datenvorbereitung](./home.md). Um zu erfahren, wie Sie Zuordnungssätze in der Data Prep-API verwenden, lesen Sie bitte das [Data Prep-Entwicklerhandbuch](./api/overview.md).