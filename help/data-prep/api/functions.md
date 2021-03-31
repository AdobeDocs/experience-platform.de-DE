---
keywords: Experience Platform;Startseite;beliebte Themen;Datenvorbereitung;API-Leitfaden;Schemas
solution: Experience Platform
title: Schemas-API-Endpunkt
topic: Schemas
description: 'Sie können den Endpunkt "Funktionen"in der Adobe Experience Platform API verwenden, um Ihre Zuordnungsfunktionen und verfügbaren Zuordnungssatzfunktionen für die Liste zu validieren. '
translation-type: tm+mt
source-git-commit: 60c80a73deb8c77f19d5963cc3319d46143fb4c3
workflow-type: tm+mt
source-wordcount: '211'
ht-degree: 12%

---


# Funktionsendpunkte

Mit Zuordnungsfunktionen können Sie Ihre Daten zwischen Quell- und Ziel-Schemas transformieren. Sie können den `/languages/el`-Endpunkt verwenden, um Ihre Ausdruck zu validieren und eine Liste aller verfügbaren Zuordnungsfunktionen zu erhalten.

## Ausdruck überprüfen

Sie können überprüfen, ob Ihr aktueller Ausdruck gültig ist, indem Sie eine POST an den `/languages/el/validate`-Endpunkt anfordern.

**API-Format**

```
POST /languages/el/validate
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/conversion/languages/el/validate \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'Content-Type: application/json' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '
  {
    "expression": "concat(\"Hi\", \",\", \"there\", \"!\")"
  }'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit dem Überprüfungsstatus des Ausdrucks zurück.

```json
{
    "validationStatus": "succeeded",
    "error": "none"
}
```

## Funktionen zum Zuordnen von Listen

Sie können eine Liste aller verfügbaren Zuordnungsfunktionen abrufen, indem Sie eine GET an den `/languages/el/functions`-Endpunkt anfordern.

**API-Format**

```
GET /languages/el/functions
```

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/functions \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit einer Liste aller verfügbaren Zuordnungsfunktionen zurück.

>[!NOTE]
>
>Diese Antwort wurde aus Platzgründen abgeschnitten.

```json
[
    {
        "category": "Date / Time",
        "function": "date",
        "description": "Function that converts date string into a ZonedDateTime object.",
        "syntax": "ZonedDateTime date(String, String, ZonedDateTime)",
        "returns": "Returns the date object that is formatted in given format or a default date if the expression evaluates to a null date.",
        "returnType": "java.time.ZonedDateTime",
        "example": "",
        "result": "",
        "params": [],
        "since": 1
    },
    {
        "category": "Hierarchies - Arrays",
        "function": "first",
        "description": "Function to retrieve the first element of the given array.",
        "syntax": "T first(T...)",
        "returns": "The first element or null if the array is null or empty.",
        "returnType": "java.lang.Object",
        "example": "first(\"1\", \"2\", \"3\")",
        "result": "\"1\"",
        "params": [
            {
                "name": "values",
                "description": "Zero or more arguments",
                "type": "object",
                "dataType": "[Ljava.lang.Object;",
                "position": 1
            }
        ],
        "since": 1
    }
]
```

## Liste-Zuordnungsset-Operatoren

Sie können eine Liste aller verfügbaren Zuordnungsset-Operatoren abrufen, indem Sie eine GET an den `/languages/el/operators`-Endpunkt anfordern.

**API-Format**

```
GET /languages/el/operators
```

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/conversion/languages/el/operators \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \ 
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt HTTP-Status 200 mit einer Liste aller verfügbaren Zuordnungsset-Operatoren zurück.

>[!NOTE]
>
>Diese Antwort wurde aus Platzgründen abgeschnitten.

```json
[
    {
        "operatorSymbol": "+",
        "methodName": "add",
        "numberOfOperands": 2,
        "description": "Simple arithmetic addition",
        "example": "1 + 2"
    },
    {
        "operatorSymbol": "/",
        "methodName": "divide",
        "numberOfOperands": 2,
        "description": "Simple arithmetic division",
        "example": "1 / 2"
    },
    {
        "operatorSymbol": "~",
        "methodName": "complement",
        "numberOfOperands": 1,
        "description": "The usual ~ operator is used, e.g.\n~33\n, ~0010 0001 = 1101 1110 = -34.",
        "example": "~44"
    },
    {
        "operatorSymbol": "-",
        "methodName": "negate",
        "numberOfOperands": 1,
        "description": "The unary - operator is used. For example\n-12",
        "example": "-12"
    },
    {
        "operatorSymbol": "!",
        "methodName": "not",
        "numberOfOperands": 1,
        "description": "The usual ! operator can be used as well as the word not, e.g.\n!cond1\nand\nnot cond1\nare equivalent",
        "example": "!cond1"
    }
]
```
