---
keywords: Experience Platform;Home;beliebte Themen;Microsoft Dynamics;Mikrosoft dynamik;Dynamik;Dynamik
solution: Experience Platform
title: Erstellen einer Microsoft Dynamics Source-Verbindung mithilfe der Flow Service API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie mithilfe der Flow Service API eine Verbindung zwischen Platform und einem Microsoft Dynamics-Konto herstellen.
exl-id: 423c6047-f183-4d92-8d2f-cc8cc26647ef
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 27%

---

# Erstellen einer [!DNL Microsoft Dynamics]-Quellverbindung mit der [!DNL Flow Service]-API

[!DNL Flow Service] wird zur Erfassung und Zentralisierung von Kundendaten aus unterschiedlichen Quellen innerhalb von Adobe Experience Platform verwendet. Der Dienst stellt eine Benutzeroberfläche und eine RESTful-API bereit, über die alle unterstützten Quellen verbunden werden können.

Dieses Lernprogramm verwendet die API [!DNL Flow Service], um Sie durch die Schritte zu führen, die notwendig sind, um die Plattform mit einem [!DNL Microsoft Dynamics]-Konto (nachstehend &quot;Dynamics&quot; genannt) zu verbinden, das die Flow Service API verwendet.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Plattformdiensten zu strukturieren, zu kennzeichnen und zu verbessern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Anwendungen für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Plattform mit der [!DNL Flow Service]-API erfolgreich mit einem Dynamics-Konto zu verbinden.

### Erforderliche Anmeldedaten sammeln

Damit [!DNL Flow Service] eine Verbindung zu [!DNL Dynamics] herstellen kann, müssen Sie Werte für die folgenden Verbindungseigenschaften angeben:

| Berechtigung | Beschreibung |
| ---------- | ----------- |
| `serviceUri` | Die Dienst-URL Ihrer [!DNL Dynamics]-Instanz. |
| `username` | Der Benutzername für Ihr [!DNL Dynamics]-Benutzerkonto. |
| `password` | Das Kennwort für Ihr [!DNL Dynamics]-Konto. |
| `servicePrincipalId` | Die Client-ID Ihres [!DNL Dynamics]-Kontos. Diese ID ist bei der Verwendung der Dienstprinzipal- und der schlüsselbasierten Authentifizierung erforderlich. |
| `servicePrincipalKey` | Der Hauptgeheimschlüssel des Dienstes. Diese Berechtigung ist bei der Verwendung der Dienstprinzipal- und der schlüsselbasierten Authentifizierung erforderlich. |

Weitere Informationen zum Einstieg finden Sie unter [this [!DNL Dynamics] Dokument](https://docs.microsoft.com/en-us/powerapps/developer/common-data-service/authenticate-oauth).

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../../../../landing/troubleshooting.md#how-do-i-format-an-api-request) im Handbuch zur Fehlerbehebung für Experience Platform.

### Sammeln von Werten für erforderliche Kopfzeilen

Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](https://www.adobe.com/go/platform-api-authentication-en) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Alle Ressourcen in Experience Platform, einschließlich der Ressourcen von [!DNL Flow Service], werden zu bestimmten virtuellen Sandboxen isoliert. Bei allen Anfragen an Platform-APIs ist eine Kopfzeile erforderlich, die den Namen der Sandbox angibt, in der der Vorgang ausgeführt werden soll:

* `x-sandbox-name: {SANDBOX_NAME}`

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* `Content-Type: application/json`

## Verbindung erstellen

Eine Verbindung gibt eine Quelle an und enthält Ihre Anmeldeinformationen für diese Quelle. Pro [!DNL Dynamics]-Konto ist nur eine Verbindung erforderlich, da sie zum Erstellen mehrerer Datenflüsse verwendet werden kann, um verschiedene Daten einzubringen.

### Eine [!DNL Dynamics]-Verbindung mit einfacher Authentifizierung erstellen

Um eine [!DNL Dynamics]-Verbindung mit einfacher Authentifizierung zu erstellen, stellen Sie eine POST an die [!DNL Flow Service]-API, während Sie Werte für `serviceUri`, `username` und `password` angeben.

**API-Format**

```http
POST /connections
```

**Anfrage**

Um eine [!DNL Dynamics]-POST zu erstellen, muss die eindeutige Verbindungs-ID als Teil der Verbindungsanforderung angegeben werden. Die Verbindungs-Spezifikations-ID für [!DNL Dynamics] ist `38ad80fe-8b06-4938-94f4-d4ee80266b07`.

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using basic auth",
        "auth": {
            "specName": "Basic Authentication for Dynamics-Online",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "username": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.serviceUri` | Der Dienst-URI, der Ihrer [!DNL Dynamics]-Instanz zugeordnet ist. |
| `auth.params.username` | Der mit Ihrem [!DNL Dynamics]-Konto verknüpfte Benutzername. |
| `auth.params.password` | Das Ihrem [!DNL Dynamics]-Konto zugeordnete Kennwort. |
| `connectionSpec.id` | Die Verbindungsspezifikation `id` Ihres [!DNL Dynamics]-Kontos, die im vorherigen Schritt abgerufen wurde. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung einschließlich der eindeutigen Kennung (`id`) zurück. Diese ID ist erforderlich, um Ihr CRM-System im nächsten Schritt zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

### Eine [!DNL Dynamics]-Verbindung mit einer Service-Prinzipal-Key-basierten Authentifizierung erstellen

Um eine [!DNL Dynamics]-Verbindung mit der Hauptschlüssel-basierten Authentifizierung des Dienstes zu erstellen, stellen Sie eine POST an die [!DNL Flow Service]-API, während Sie Werte für `serviceUri`, `servicePrincipalId` und `servicePrincipalKey` eingeben.

**API-Format**

```http
POST /connections
```

**Anfrage**

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d '{
        "name": "Dynamics connection",
        "description": "Dynamics connection using key-based authentication",
        "auth": {
            "specName": "Service Principal Key Based Authentication",
            "params": {
                "serviceUri": "{SERVICE_URI}",
                "servicePrincipalId": "{SERVICE_PRINCIPAL_ID}",
                "servicePrincipalKey": "{SERVICE_PRINCIPAL_KEY}"
            }
        },
        "connectionSpec": {
            "id": "38ad80fe-8b06-4938-94f4-d4ee80266b07",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.serviceUri` | Der Dienst-URI, der Ihrer [!DNL Dynamics]-Instanz zugeordnet ist. |
| `auth.params.servicePrincipalId` | Die Client-ID Ihres [!DNL Dynamics]-Kontos. Diese ID ist bei der Verwendung der Dienstprinzipal- und der schlüsselbasierten Authentifizierung erforderlich. |
| `auth.params.servicePrincipalKey` | Der Hauptgeheimschlüssel des Dienstes. Diese Berechtigung ist bei der Verwendung der Dienstprinzipal- und der schlüsselbasierten Authentifizierung erforderlich. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung einschließlich der eindeutigen Kennung (`id`) zurück. Diese ID ist erforderlich, um Ihr CRM-System im nächsten Schritt zu untersuchen.

```json
{
    "id": "4cb0c374-d3bb-4557-b139-5712880adc55",
    "etag": "\"9e0052a2-0000-0200-0000-5e35tb330000\""
}
```

## Nächste Schritte

In diesem Lernprogramm haben Sie eine [!DNL Dynamics]-Verbindung mit der [!DNL Flow Service]-API erstellt und den eindeutigen ID-Wert der Verbindung erhalten. Sie können diese ID im nächsten Lernprogramm verwenden, um zu lernen, wie Sie CRM-Systeme mithilfe der Flow Service API](../../explore/crm.md) untersuchen.[
