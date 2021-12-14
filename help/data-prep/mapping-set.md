---
keywords: Experience Platform;Startseite;Mapper;Zuordnungssatz;Zuordnung;
solution: Experience Platform
title: Übersicht über Zuordnungssätze
topic-legacy: overview
description: Erfahren Sie, wie Sie Zuordnungssätze mit der Funktion zur Datenvorbereitung von Adobe Experience Platform verwenden.
exl-id: b45545b7-3ae7-400d-b6fd-b2cb76061093
source-git-commit: 27e5c64f31b9a68252d262b531660811a0576177
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 100%

---

# Übersicht über Zuordnungssätze

Ein Zuordnungssatz ist ein Satz von Zuordnungen, der Daten von einem Schema in ein anderes verwandelt. In diesem Dokument erfahren Sie, woraus Zuordnungssätze bestehen, einschließlich Eingabeschema, Ausgabeschema und Zuordnungen.

## Erste Schritte

Diese Übersicht setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

- [Datenvorbereitung](./home.md): Die Datenvorbereitung ermöglicht es Dateningenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, zu verwandeln und zu validieren.
- [Datenflüsse](../dataflows/home.md): Datenflüsse sind eine Darstellung von Datenvorgängen, die Daten über Platform verschieben. Datenflüsse werden über verschiedene Dienste hinweg konfiguriert und helfen beim Verschieben von Daten aus Quell-Connectoren in Zieldatensätze, in [!DNL Identity] und [!DNL Profile] sowie in [!DNL Destinations].
- [[!DNL Adobe Experience Platform Data Ingestion]](../ingestion/home.md): Die Methoden, mit denen Daten an [!DNL Experience Platform] gesendet werden können.
- [[!DNL Experience Data Model (XDM) System]](../xdm/home.md): Das standardisierte Framework, mit dem [!DNL Experience Platform] Kundenerlebnisdaten organisiert.

## Syntax von Zuordnungssätzen

Ein Zuordnungssatz besteht aus einer Kennung, einem Namen, einem Eingabeschema, einem Ausgabeschema und einer Liste der zugehörigen Zuordnungen.

Die folgende JSON-Datei ist ein Beispiel für einen typischen Zuordnungssatz:

```json
{
    "id": "cbb0da769faa48fcb29e026a924ba29d",
    "name": "Demo Mapping Set",
    "inputSchema": {
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
            "name": "Id",
            "description": "Identifier field"
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
| `id` | Eine eindeutige Kennung für den Zuordnungssatz. |
| `name` | Der Name des Zuordnungssatzes. |
| `inputSchema` | Das XDM-Schema für die eingehenden Daten. |
| `outputSchema` | Das XDM-Schema, mit dem die Eingabedaten entsprechend konvertiert werden. |
| `mappings` | Ein Array mit Feld-zu-Feld-Zuordnungen vom Quellschema zum Zielschema. |
| `sourceType` | Für jede aufgelistete Zuordnung gibt deren `sourceType`-Attribut den Typ der Quelle an, die zugeordnet werden soll. Kann `ATTRIBUTE`, `STATIC` oder `EXPRESSION` sein: <ul><li> `ATTRIBUTE` wird für jeden Wert verwendet, der im Quellpfad gefunden wird. </li><li>`STATIC` wird für Werte verwendet, die in den Zielpfad eingefügt werden. Dieser Wert bleibt konstant und wird vom Quellschema nicht beeinflusst.</li><li> `EXPRESSION` wird für einen Ausdruck verwendet, der während der Laufzeit aufgelöst wird. Eine Liste der verfügbaren Ausdrücke finden Sie im [Handbuch für Zuordnungsfunktionen](./functions.md).</li> </ul> |
| `source` | Für jede aufgelistete Zuordnung gibt das `source`-Attribut das Feld an, das Sie zuordnen möchten. Weitere Informationen zum Konfigurieren Ihrer Quelle finden Sie im Abschnitt [Quellen](#sources). |
| `destination` | Für jede aufgelistete Zuordnung gibt das `destination`-Attribut das Feld oder den Pfad zum Feld an, in dem der aus dem Feld `source` extrahierte Wert platziert werden wird. Weitere Informationen zum Konfigurieren Ihrer Ziele finden Sie im Abschnitt [Ziele](#destination). |
| `mappings.name` | (*Optional*) Ein Name für die Zuordnung. |
| `mappings.description` | (*Optional)* Eine Beschreibung der Zuordnung. |

## Konfigurieren von Zuordnungsquellen

Bei einer Zuordnung kann `source` ein Feld, ein Ausdruck oder ein statischer Wert sein. Je nach vorhandenem Quelltyp kann der Wert auf verschiedene Arten extrahiert werden.

### Feld in Spaltendaten

Verwenden Sie beim Zuordnen eines Felds in Spaltendaten (z. B. einer CSV-Datei) den Quelltyp `ATTRIBUTE`. Wenn das Feld `.` in seinem Namen enthält, verwenden Sie `\`, um den Wert mit einem Escape-Zeichen zu versehen. Ein Beispiel für diese Zuordnung ist unten dargestellt:

**CSV-Beispieldatei:**

```csv
Full.Name, Email
John Smith, js@example.com
```

**Beispielzuordnung**

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

Verwenden Sie beim Zuordnen eines Felds in verschachtelten Daten (z. B. einer JSON-Datei) den Quelltyp `ATTRIBUTE`. Wenn das Feld `.` im Namen enthält, verwenden Sie `\`, um den Wert mit einem Escape-Zeichen zu versehen. Ein Beispiel für diese Zuordnung ist unten dargestellt:

**JSON-Beispieldatei**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Beispielzuordnung**

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

### Feld in einem Array

Beim Zuordnen eines Felds in einem Array können Sie einen bestimmten Wert mithilfe eines Index abrufen. Verwenden Sie dazu den Quelltyp `ATTRIBUTE` und den Index des Werts, den Sie zuordnen möchten. Ein Beispiel für diese Zuordnung ist unten dargestellt:

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

**Beispielzuordnung**

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

### Array zu Array oder Objekt zu Objekt

Mit dem Quelltyp `ATTRIBUTE` können Sie ein Array auch direkt einem Array bzw. ein Objekt einem Objekt zuordnen. Ein Beispiel für diese Zuordnung ist unten dargestellt:

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

**Beispielzuordnung**

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

### Iterative Vorgänge bei Arrays

Mit dem Quelltyp `ATTRIBUTE` können Sie Arrays iterativ durchlaufen und mithilfe eines Platzhalterindex (`[*]`) einem Zielschema zuordnen. Ein Beispiel für diese Zuordnung ist unten dargestellt:

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

**Beispielzuordnung**

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

Wenn Sie eine Konstante oder einen statischen Wert zuordnen möchten, verwenden Sie den Quelltyp `STATIC`.  Bei Verwendung des Quelltyps `STATIC` stellt `source` den hart-codierten Wert dar, den Sie `destination` zuweisen möchten. Ein Beispiel für diese Zuordnung ist unten dargestellt:

**JSON-Beispieldatei**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Beispielzuordnung**

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

### Ausdrücke

Wenn Sie einen Ausdruck zuordnen möchten, verwenden Sie den Quelltyp `EXPRESSION`. Eine Liste der zulässigen Funktionen finden Sie im [Handbuch für Zuordnungsfunktionen](./functions.md). Bei Verwendung des Quelltyps `EXPRESSION` stellt `source` die Funktion dar, die Sie auflösen möchten. Ein Beispiel für diese Zuordnung ist unten dargestellt:

**JSON-Beispieldatei**

```json
{
    "firstName": "John",
    "lastName": "Smith",
    "email": "js@example.com"
}
```

**Beispielzuordnung**

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

In einer Zuordnung ist `destination` der Ort, an dem der aus `source` extrahierte Wert eingefügt wird.

### Feld auf der Stammebene

Wenn Sie den Wert `source` der Stammebene Ihrer umgewandelten Daten zuordnen möchten, führen Sie folgendes Beispiel aus:

**JSON-Beispieldatei**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Beispielzuordnung**

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

Wenn Sie den Wert `source` in Ihren umgewandelten Daten einem verschachtelten Feld zuordnen möchten, führen Sie folgendes Beispiel aus:

**JSON-Beispieldatei**

```json
{
    "name": "John Smith",
    "email": "js@example.com"
}
```

**Beispielzuordnung**

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

### Feld in einem bestimmten Array-Index

Wenn Sie den Wert `source` in Ihren umgewandelten Daten einem bestimmten Index in einem Array zuordnen möchten, führen Sie folgendes Beispiel aus:

**JSON-Beispieldatei**

```json
{
    "customerInfo": {
        "name": "John Smith",
        "email": "js@example.com"
    }
}
```

**Beispielzuordnung**

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

### Iterative Array-Operation

Wenn Sie Arrays iterativ durchlaufen und die Werte dem Ziel zuordnen möchten, können Sie einen Platzhalterindex (`[*]`) verwenden. Ein Beispiel dafür ist unten dargestellt:

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

**Beispielzuordnung**

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

Durch Lesen dieses Dokuments sollten Sie nun wissen, wie sich Zuordnungssätze erstellen lassen, einschließlich der Konfiguration einzelner Zuordnungen innerhalb eines Zuordnungssatzes. Weitere Informationen zu anderen Datenvorbereitungsfunktionen finden Sie in der [Übersicht zur Datenvorbereitung](./home.md). Informationen zur Verwendung von Zuordnungssätzen in der Datenvorbereitungs-API finden Sie im [Entwicklerhandbuch für die Datenvorbereitung](./api/overview.md).
