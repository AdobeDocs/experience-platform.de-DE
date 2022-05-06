---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Beschriftungs-API-Endpunkt
topic-legacy: developer guide
description: Erfahren Sie, wie Sie mit der Richtlinien-Service-API Datennutzungsbeschriftungen in Experience Platform verwalten.
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '506'
ht-degree: 100%

---

# Beschriftungs-Endpunkt

Mit Datennutzungsbeschriftungen können Sie Datensätze anhand der für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Mit dem `/labels`-Endpunkt in [!DNL Policy Service API] können Sie Datennutzungsbeschriftungen in Ihrem Experience-Programm programmgesteuert verwalten.

>[!NOTE]
>
>Der `/labels`-Endpunkt wird nur zum Abrufen, Erstellen und Aktualisieren von Datennutzungsbeschriftungen verwendet. Anleitungen zum Hinzufügen von Beschriftungen zu Datensätzen und Feldern mithilfe von API-Aufrufen finden Sie im Handbuch zum [Verwalten von Datensatzbeschriftungen](../labels/dataset-api.md).

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil von [[!DNL Policy Service API]](https://www.adobe.io/experience-platform-apis/references/policy-service/). Bevor Sie fortfahren, schauen Sie bitte im Handbuch in [Erste Schritte](getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die für das Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Abrufen einer Beschriftungsliste {#list}

Sie können alle `core` oder `custom` Beschriftungen durch eine GET-Anfrage an `/labels/core` bzw. `/labels/custom` auflisten.

**API-Format**

```http
GET /labels/core
GET /labels/custom
```

**Anfrage**

Mit der folgenden Anfrage werden alle benutzerdefinierten Beschriftungen aufgelistet, die im Rahmen Ihres Unternehmens erstellt wurden.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von benutzerdefinierten Beschriftungen zurück, die vom System abgerufen werden. Da die obige Beispielanforderung an `/labels/custom` erfolgte, zeigt die unten stehende Antwort nur benutzerdefinierte Beschriftungen an.

```json
{
    "_page": {
        "count": 2
    },
    "_links": {
        "page": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom?{?limit,start,property}",
            "templated": true
        }
    },
    "children": [
        {
            "name": "L1",
            "category": "Custom",
            "friendlyName": "Banking Information",
            "description": "Data containing banking information for a customer.",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594396718731,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594396718731,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L1"
                }
            }
        },
        {
            "name": "L2",
            "category": "Custom",
            "friendlyName": "Purchase History Data",
            "description": "Data containing information on past transactions",
            "imsOrg": "{ORG_ID}",
            "sandboxName": "{SANDBOX_NAME}",
            "created": 1594397415663,
            "createdClient": "{CLIENT_ID}",
            "createdUser": "{USER_ID}",
            "updated": 1594397728708,
            "updatedClient": "{CLIENT_ID}",
            "updatedUser": "{USER_ID}",
            "_links": {
                "self": {
                    "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
                }
            }
        }
    ]
}
```

## Nachschlagen einer Kennzeichnung {#look-up}

Sie können eine bestimmte Kennzeichnung nachschlagen, indem Sie die Eigenschaft `name` dieser Kennzeichnung in den Pfad einer GET-Anfrage an die [!DNL Policy Service]-API aufnehmen.

**API-Format**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{LABEL_NAME}` | Die Eigenschaft `name` der benutzerdefinierten Kennzeichnung, die Sie nachschlagen möchten. |

**Anfrage**

Die folgende Anfrage ruft die benutzerdefinierte Kennzeichnung `L2` ab, wie im Pfad angegeben.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Details der benutzerdefinierten Beschriftung zurück.

```json
{
    "name": "L2",
    "category": "Custom",
    "friendlyName": "Purchase History Data",
    "description": "Data containing information on past transactions",
    "imsOrg": "{ORG_ID}",
    "sandboxName": "{SANDBOX_NAME}",
    "created": 1594397415663,
    "createdClient": "{CLIENT_ID}",
    "createdUser": "{USER_ID}",
    "updated": 1594397728708,
    "updatedClient": "{CLIENT_ID}",
    "updatedUser": "{USER_ID}",
    "_links": {
        "self": {
            "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L2"
        }
    }
}
```

## Erstellen oder Aktualisieren einer benutzerdefinierten Kennzeichnung {#create-update}

Um eine benutzerdefinierte Kennzeichnung zu erstellen oder zu aktualisieren, müssen Sie eine PUT-Anfrage an die [!DNL Policy Service]-API richten.

**API-Format**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{LABEL_NAME}` | Die Eigenschaft `name` einer benutzerdefinierten Kennzeichnung. Wenn keine benutzerdefinierte Beschriftung mit diesem Namen vorhanden ist, wird eine neue Beschriftung erstellt. Wenn eine vorhanden ist, wird diese Beschriftung aktualisiert. |

**Anfrage**

Mit der folgenden Anfrage wird eine neue Kennzeichnung (`L3`) erstellt, die Daten beschreiben soll, die Informationen zu den ausgewählten Zahlungsplänen der Kunden enthalten.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -d '{
        "name": "L3",
        "category": "Custom",
        "friendlyName": "Payment Plan",
        "description": "Data containing information on selected payment plans."
      }'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `name` | Eine eindeutige Zeichenfolgenkennung für die Beschriftung. Dieser Wert wird für Nachschlagezwecke und zum Anwenden der Beschriftung auf Datensätze und Felder verwendet. Es wird daher empfohlen, einen kurzen und knappen Wert zu wählen. |
| `category` | Die Kategorie der Beschriftung. Sie können zwar eigene Kategorien für benutzerdefinierte Kennzeichnungen erstellen, es wird jedoch dringend empfohlen, `Custom` zu verwenden, wenn die Kennzeichnung in der Benutzeroberfläche angezeigt werden soll. |
| `friendlyName` | Ein benutzerfreundlicher Name für die Beschriftung, der zu Anzeigezwecken verwendet wird. |
| `description` | (Optional) Eine Beschreibung der Beschriftung, um mehr Kontext bereitzustellen. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der benutzerdefinierten Beschriftung zurück, wobei HTTP-Code 200 (OK) bei einer Aktualisierung einer bestehenden Beschriftung oder 201 (Erstellt) bei einer neuen Beschriftung angezeigt wird.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{ORG_ID}",
  "sandboxName": "{SANDBOX_NAME}",
  "created": 1529696681413,
  "createdClient": "{CLIENT_ID}",
  "createdUser": "{USER_ID}",
  "updated": 1529697651972,
  "updatedClient": "{CLIENT_ID}",
  "updatedUser": "{USER_ID}",
  "_links": {
    "self": {
      "href": "https://platform.adobe.io:443/data/foundation/dulepolicy/labels/custom/L3"
    }
  }
}
```

## Nächste Schritte

In diesem Handbuch wurde die Verwendung des Endpunkts `/labels` in der Richtlinien-Service-API behandelt. Anleitungen zum Anwenden von Kennzeichnungen auf Datensätze und Felder finden Sie im [Handbuch zur Datensatzkennzeichnungs-API](../labels/dataset-api.md).
