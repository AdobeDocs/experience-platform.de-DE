---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Bezeichnungen-API-Endpunkt
topic-legacy: developer guide
description: Erfahren Sie, wie Sie mit der Policy Service API Datenverwendungsbeschriftungen in Experience Platform verwalten.
exl-id: 9a01f65c-01f1-4298-bdcf-b7e00ccfe9f2
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '510'
ht-degree: 6%

---

# Beschriftungen-Endpunkt

Mit Datenverwendungsbeschriftungen können Sie Daten entsprechend den für diese Daten geltenden Nutzungsrichtlinien kategorisieren. Mit dem `/labels`-Endpunkt in [!DNL Policy Service API] können Sie Datenverwendungsbeschriftungen in Ihrer Erlebnisanwendung programmgesteuert verwalten.

>[!NOTE]
>
>Der `/labels`-Endpunkt wird nur zum Abrufen, Erstellen und Aktualisieren von Datenverwendungsbeschriftungen verwendet. Anweisungen zum Hinzufügen von Bezeichnungen zu Datasets und Feldern mithilfe von API-Aufrufen finden Sie im Handbuch [Verwalten von Datensatzbeschriftungen](../labels/dataset-api.md).

## Erste Schritte

Der in diesem Handbuch verwendete API-Endpunkt ist Teil von [[!DNL Policy Service API]](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml). Bevor Sie fortfahren, lesen Sie bitte im Handbuch [Erste Schritte](getting-started.md) nach Links zu entsprechenden Dokumentationen, einem Leitfaden zum Lesen der Beispiel-API-Aufrufe in diesem Dokument und wichtigen Informationen zu erforderlichen Kopfzeilen, die für das erfolgreiche Aufrufen einer [!DNL Experience Platform]-API erforderlich sind.

## Abrufen einer Liste von Beschriftungen {#list}

Sie können alle Bezeichnungen `core` oder `custom` durch eine GET an `/labels/core` bzw. `/labels/custom` Liste haben.

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

Eine erfolgreiche Antwort gibt eine Liste von benutzerdefinierten Beschriftungen zurück, die vom System abgerufen werden. Da die obige Beispielanforderung an `/labels/custom` erfolgte, zeigt die unten stehende Antwort nur benutzerdefinierte Bezeichnungen an.

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

## Suchen Sie eine Beschriftung {#look-up}

Sie können eine bestimmte Beschriftung nachschlagen, indem Sie die `name`-Eigenschaft dieser Beschriftung in den Pfad einer GET-Anforderung zur [!DNL Policy Service]-API aufnehmen.

**API-Format**

```http
GET /labels/core/{LABEL_NAME}
GET /labels/custom/{LABEL_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{LABEL_NAME}` | Die `name`-Eigenschaft der benutzerdefinierten Beschriftung, die Sie nachschlagen möchten. |

**Anfrage**

Die folgende Anforderung ruft die benutzerdefinierte Beschriftung `L2` ab, wie im Pfad angegeben.

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

## Erstellen oder aktualisieren Sie eine benutzerdefinierte Beschriftung {#create-update}

Um eine benutzerdefinierte Bezeichnung zu erstellen oder zu aktualisieren, müssen Sie eine PUT an die [!DNL Policy Service]-API anfordern.

**API-Format**

```http
PUT /labels/custom/{LABEL_NAME}
```

| Parameter | Beschreibung |
| --- | --- |
| `{LABEL_NAME}` | Die `name`-Eigenschaft einer benutzerdefinierten Bezeichnung. Wenn keine benutzerdefinierte Bezeichnung mit diesem Namen vorhanden ist, wird eine neue Bezeichnung erstellt. Wenn eine vorhanden ist, wird diese Bezeichnung aktualisiert. |

**Anfrage**

Mit der folgenden Anforderung wird ein neues Etikett (`L3`) erstellt, das Daten beschreiben soll, die Informationen zu den ausgewählten Zahlungsplänen der Kunden enthalten.

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
| `category` | Die Kategorie des Etiketts. Sie können zwar eigene Kategorien für benutzerdefinierte Beschriftungen erstellen, es wird jedoch dringend empfohlen, `Custom` zu verwenden, wenn die Beschriftung in der Benutzeroberfläche angezeigt werden soll. |
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

In diesem Handbuch wurde die Verwendung des Endpunkts `/labels` in der Policy Service API behandelt. Anweisungen zum Anwenden von Bezeichnungen auf Datensätze und Felder finden Sie im Handbuch [Datenbezeichnungen-API](../labels/dataset-api.md).
