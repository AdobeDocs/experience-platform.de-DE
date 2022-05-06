---
keywords: Experience Platform; Startseite; beliebte Themen; Marketing-Automatisierung
solution: Experience Platform
title: Erkunden eines Marketingautomatisierungssystems mithilfe der Flow Service-API
topic-legacy: overview
description: In diesem Tutorial wird die Flow Service-API verwendet, um Marketing-Automatisierungssysteme zu untersuchen.
exl-id: 250c1ba0-1baa-444f-ab2b-58b3a025561e
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 38%

---

# Erkunden Sie ein Marketing-Automatisierungssystem mit dem [!DNL Flow Service] API

[!DNL Flow Service] wird verwendet, um Kundendaten aus verschiedenen Quellen innerhalb von Adobe Experience Platform zu sammeln und zu zentralisieren. Der Dienst bietet eine Benutzeroberfläche und eine RESTful-API, über die alle unterstützten Quellen verbunden werden können.

In diesem Tutorial wird die [!DNL Flow Service] API zur Erforschung von Systemen zur Marketing-Automatisierung.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service] API.

### Sammeln erforderlicher Anmeldeinformationen

Für dieses Tutorial benötigen Sie eine gültige Verbindung zur Marketing-Automatisierungsanwendung eines Drittanbieters, aus der Sie Daten erfassen möchten. Eine gültige Verbindung umfasst die Verbindungsspezifikations-ID und die Verbindungs-ID Ihrer Anwendung. Weitere Informationen zum Erstellen einer Verbindung zur Marketing-Automatisierung und zum Abrufen dieser Werte finden Sie im Abschnitt [Marketing-Automatisierungsquelle mit Platform verbinden](../../api/create/marketing-automation/hubspot.md) Tutorial.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

### Sammeln von Werten für erforderliche Kopfzeilen

Um [!DNL Platform]-APIs aufzurufen, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de) abschließen. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Header in allen [!DNL Experience Platform]-API-Aufrufen bereitgestellt, wie unten dargestellt:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Alle Ressourcen in [!DNL Experience Platform], einschließlich der Ressourcen, die zu [!DNL Flow Service] gehören, werden in bestimmten virtuellen Sandboxes isoliert. Bei allen Anfragen an [!DNL Platform]-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* x-sandbox-name: `{SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* Content-Type: `application/json`

## Datentabellen durchsuchen

Mithilfe der Basisverbindung für Ihr Marketing-Automatisierungssystem können Sie Ihre Datentabellen durch Ausführen von GET-Anfragen untersuchen. Verwenden Sie den folgenden Aufruf, um den Pfad der Tabelle zu finden, die Sie untersuchen oder in die Sie aufnehmen möchten [!DNL Platform].

**API-Format**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=root
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die Kennung der Basisverbindung für Ihr Marketing-Automatisierungssystem. |

**Anfrage**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=root' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort ist eine Reihe von Tabellen von zu Ihrem Marketing-Automatisierungssystem. Finden Sie den Tisch, den Sie mitbringen möchten [!DNL Platform] und nimmt Kenntnis von `path` -Eigenschaft, da Sie sie im nächsten Schritt bereitstellen müssen, um ihre Struktur zu überprüfen.

```json
[
    {
        "type": "table",
        "name": "Hubspot.All_Deals",
        "path": "Hubspot.All_Deals",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Authors",
        "path": "Hubspot.Blog_Authors",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Blog_Comments",
        "path": "Hubspot.Blog_Comments",
        "canPreview": true,
        "canFetchSchema": true
    },
    {
        "type": "table",
        "name": "Hubspot.Contacts",
        "path": "Hubspot.Contacts",
        "canPreview": true,
        "canFetchSchema": true
    },
]
```

## Tabellenstruktur Inspect

Um die Tabellenstruktur in Ihrem Marketing-Automatisierungssystem zu überprüfen, führen Sie eine GET-Anfrage aus und geben Sie dabei den Pfad einer Tabelle als Abfrageparameter an.

**API-Format**

```https
GET /connections/{BASE_CONNECTION_ID}/explore?objectType=table&object={TABLE_PATH}
```

| Parameter | Beschreibung |
| --- | --- |
| `{BASE_CONNECTION_ID}` | Die Verbindungs-ID für Ihr Marketing-Automatisierungssystem. |
| `{TABLE_PATH}` | Der Pfad einer Tabelle in Ihrem Marketing-Automatisierungssystem. |

**Anfrage**

```shell
curl -X GET \
    'http://platform.adobe.io/data/foundation/flowservice/connections/2fce94c1-9a93-4971-8e94-c19a93097129/explore?objectType=table&object=Hubspot.Contacts' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {ORG_ID}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt die Struktur einer Tabelle zurück. Details zu den einzelnen Spalten der Tabelle befinden sich in Elementen der `columns` Array.

```json
{
    "format": "flat",
    "schema": {
        "columns": [
            {
                "name": "Properties_Firstname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Properties_Lastname_Value",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
            {
                "name": "Added_At",
                "type": "string",
                "meta:xdmType": "date-time",
                "xdm": {
                    "type": "string",
                    "format": "date-time"
                }
            },
            {
                "name": "Portal_Id",
                "type": "string",
                "xdm": {
                    "type": "string"
                }
            },
        ]
    }
}
```

## Nächste Schritte

In diesem Tutorial haben Sie Ihr Marketing-Automatisierungssystem untersucht und den Pfad der Tabelle gefunden, die Sie einführen möchten [!DNL Platform]und Informationen über seine Struktur erhalten. Sie können diese Informationen im nächsten Tutorial zu [Daten aus Ihrem Marketing-Automatisierungssystem erfassen und in Platform einbringen](../collect/marketing-automation.md).
