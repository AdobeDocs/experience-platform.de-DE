---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Beschriftungen-Endpunkt
topic: developer guide
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 6%

---


# Beschriftungen-Endpunkt

Mit Datenverwendungsbeschriftungen können Sie Daten entsprechend den für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Mit dem `/labels` Endpunkt im [!DNL Policy Service API] können Sie Datenverwendungsbeschriftungen in Ihrer Erlebnisanwendung programmgesteuert verwalten.

>[!NOTE]
>
>Der `/labels` Endpunkt wird nur zum Abrufen, Erstellen und Aktualisieren von Beschriftungen für die Datenverwendung verwendet. Anweisungen zum Hinzufügen von Bezeichnungen zu Datensätzen und Feldern mithilfe von API-Aufrufen finden Sie im Handbuch zur [Verwaltung von Datenbezeichnungen](../labels/dataset-api.md).

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil des [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Bevor Sie fortfahren, lesen Sie bitte die [Anleitung](getting-started.md) zu den ersten Schritten für Links zur zugehörigen Dokumentation, eine Anleitung zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtige Informationen zu den erforderlichen Kopfzeilen, die zum erfolgreichen Aufrufen einer beliebigen [!DNL Experience Platform] API erforderlich sind.

## Retrieve a list of labels {#list}

Sie können alle `core` bzw. `custom` Bezeichnungen durch eine GET an `/labels/core` bzw. `/labels/custom`anfordern.

**API-Format**

```http
GET /labels/core
GET /labels/custom
```

**Anfrage**

Die folgende Anforderung Liste alle benutzerdefinierten Beschriftungen, die im Rahmen Ihres Unternehmens erstellt wurden.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt eine Liste von benutzerdefinierten Beschriftungen zurück, die vom System abgerufen werden. Da die obige Beispielanforderung ausgeführt wurde, zeigt `/labels/custom`die unten stehende Antwort nur benutzerdefinierte Beschriftungen an.

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
            "imsOrg": "{IMS_ORG}",
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
            "imsOrg": "{IMS_ORG}",
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

## Eine Beschriftung nachschlagen {#look-up}

Sie können eine bestimmte Beschriftung nachschlagen, indem Sie die `name` Eigenschaft dieser Beschriftung in den Pfad einer GET-Anforderung zur [!DNL Policy Service] API aufnehmen.

**API-Format**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{LABEL_NAME}` | The `name` property of the custom label you want to look up. |

**Anfrage**

Mit der folgenden Anforderung wird die benutzerdefinierte Beschriftung `L2`wie im Pfad angegeben abgerufen.

```shell
curl -X GET \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L2' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
    "imsOrg": "{IMS_ORG}",
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

## Erstellen oder Aktualisieren einer benutzerdefinierten Bezeichnung {#create-update}

Um eine benutzerdefinierte Bezeichnung zu erstellen oder zu aktualisieren, müssen Sie eine PUT an die [!DNL Policy Service] API senden.

**API-Format**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{LABEL_NAME}` | Die `name` Eigenschaft einer benutzerdefinierten Beschriftung. Wenn keine benutzerdefinierte Bezeichnung mit diesem Namen vorhanden ist, wird eine neue Bezeichnung erstellt. Wenn eine vorhanden ist, wird diese Bezeichnung aktualisiert. |

**Anfrage**

Mit der folgenden Anforderung wird ein neues Etikett erstellt, `L3`das Daten beschreiben soll, die Informationen zu den ausgewählten Zahlungsplänen der Kunden enthalten.

```shell
curl -X PUT \
  'https://platform.adobe.io/data/foundation/dulepolicy/labels/custom/L3' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}' \
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
| `name` | Eine eindeutige Zeichenfolgenkennung für die Bezeichnung. Dieser Wert wird für Nachschlagezwecke und die Anwendung der Beschriftung auf Datensätze und Felder verwendet. Es wird daher empfohlen, kurz und knapp zu sein. |
| `category` | Die Kategorie des Etiketts. Sie können zwar eigene Kategorien für benutzerdefinierte Beschriftungen erstellen, es wird jedoch dringend empfohlen, die Beschriftung `Custom` in der Benutzeroberfläche anzuzeigen. |
| `friendlyName` | Ein benutzerfreundlicher Name für die Beschriftung, der zu Anzeigezwecken verwendet wird. |
| `description` | (Optional) Eine Beschreibung der Beschriftung, um einen weiteren Kontext bereitzustellen. |

**Antwort**

Eine erfolgreiche Antwort gibt die Details der benutzerdefinierten Beschriftung zurück, wobei HTTP-Code 200 (OK) bei einer Aktualisierung einer bestehenden Beschriftung oder 201 (Erstellt) bei einer neuen Beschriftung.

```json
{
  "name": "L3",
  "category": "Custom",
  "friendlyName": "Payment Plan",
  "description": "Data containing information on selected payment plans.",
  "imsOrg": "{IMS_ORG}",
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

In diesem Handbuch wurde die Verwendung des `/labels` Endpunkts in der Policy Service API behandelt. Anweisungen zum Anwenden von Bezeichnungen auf Datensätze und Felder finden Sie im API-Handbuch [für](../labels/dataset-api.md)Datensatzbeschriftungen.