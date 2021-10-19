---
keywords: Experience Platform;Home;beliebte Themen; Dateiübertragungsprotokoll; Dateiübertragungsprotokoll
solution: Experience Platform
title: Erstellen einer FTP-Basisverbindung mithilfe der Flow Service API
topic-legacy: overview
type: Tutorial
description: Erfahren Sie, wie Sie Adobe Experience Platform mithilfe der Flow Service API mit einem FTP-Server (File Transfer Protocol) verbinden.
exl-id: a7bef346-b357-49bc-ac54-ac8b42adac50
source-git-commit: 13bd1254dfe89004465174a7532b4f6aaef54c09
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 13%

---

# Erstellen Sie eine FTP-Basisverbindung mit [!DNL Flow Service] API

>[!NOTE]
>
>Der FTP-Anschluss befindet sich in der Beta-Version. Die Funktionen und Dokumentation können sich ändern. Siehe [Quellübersicht](../../../../home.md#terms-and-conditions) für weitere Informationen zur Verwendung von Beta-gekennzeichneten Steckverbindern.

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

Dieses Tutorial führt Sie durch die Schritte zum Erstellen einer Basisverbindung für [!DNL FTP] (Dateiübertragungsprotokoll) mit [[!DNL Flow Service] API](https://www.adobe.io/experience-platform-apis/references/flow-service/).

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Adobe Experience Platform voraus:

* [Quellen](../../../../home.md): [!DNL Experience Platform] ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten zu strukturieren, zu kennzeichnen und zu verbessern, indem Sie [!DNL Platform] Dienstleistungen.
* [Sandboxes](../../../../../sandboxes/home.md): [!DNL Experience Platform] bietet virtuelle Sandboxes, die eine einzelne [!DNL Platform]-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um erfolgreich eine Verbindung zu einer [!DNL FTP] Server, der [!DNL Flow Service] API.

### Erforderliche Anmeldedaten sammeln

In der Reihenfolge [!DNL Flow Service] Verbindung herstellen zu [!DNL FTP], müssen Sie Werte für die folgenden Verbindungseigenschaften bereitstellen:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `host` | Der Name oder die IP-Adresse, die Ihrer/Ihrem [!DNL FTP] Server. |
| `username` | Der Benutzername mit Zugriff auf Ihre [!DNL FTP] Server. |
| `password` | Das Kennwort für Ihre [!DNL FTP] Server. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Verbindungseigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für das Erstellen der Basis- und Quellverbindungen. Verbindungsspezifikations-ID für [!DNL FTP] ist: `fb2e94c9-c031-467d-8103-6bd6e0a432f2`. |

### Verwenden von Plattform-APIs

Informationen dazu, wie Sie erfolgreich Aufrufe von Plattform-APIs durchführen, finden Sie im Handbuch zu [Erste Schritte mit Plattform-APIs](../../../../../landing/api-guide.md).

## Basisverbindung erstellen

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Plattform gespeichert, einschließlich der Authentifizierungsinformationen Ihrer Quelle, des aktuellen Zustands der Verbindung und Ihrer eindeutigen Basis-Verbindungs-ID. Die Basis-Verbindungs-ID ermöglicht es Ihnen, Dateien von der Quelle aus zu erkunden und zu navigieren und die spezifischen Elemente zu identifizieren, die Sie aufnehmen möchten, einschließlich Informationen zu den Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST an `/connections` Endpunkt beim Bereitstellen von [!DNL FTP] Authentifizierungsdaten als Teil der Anforderungsparameter.

**API-Format**

```http
POST /connections
```

**Anfrage**

Die folgende Anforderung erstellt eine Basisverbindung für [!DNL FTP]:

```shell
curl -X POST \
    'https://platform.adobe.io/data/foundation/flowservice/connections' \
    -H 'Authorization: Bearer {ACCESS_TOKEN}' \
    -H 'x-api-key: {API_KEY}' \
    -H 'x-gw-ims-org-id: {IMS_ORG}' \
    -H 'x-sandbox-name: {SANDBOX_NAME}' \
    -H 'Content-Type: application/json' \
    -d  '{
        "name": "FTP connector with password",
        "description": "FTP connector password",
        "auth": {
            "specName": "Basic Authentication for FTP",
            "params": {
                "host": "{HOST}",
                "userName": "{USERNAME}",
                "password": "{PASSWORD}"
            }
        },
        "connectionSpec": {
            "id": "fb2e94c9-c031-467d-8103-6bd6e0a432f2",
            "version": "1.0"
        }
    }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.host` | Der Hostname des FTP-Servers. |
| `auth.params.username` | Der Ihrem FTP-Server zugeordnete Benutzername. |
| `auth.params.password` | Das mit Ihrem FTP-Server verknüpfte Kennwort. |
| `connectionSpec.id` | Spezifikations-ID der FTP-Serververbindung: `fb2e94c9-c031-467d-8103-6bd6e0a432f2` |

**Antwort**

Eine erfolgreiche Antwort gibt die eindeutige Kennung zurück (`id`) der neu erstellten Verbindung. Diese ID ist erforderlich, um Ihren FTP-Server im nächsten Tutorial zu erkunden.

```json
{
    "id": "bf367b0d-3d9b-4060-b67b-0d3d9bd06094",
    "etag": "\"1700cc7b-0000-0200-0000-5e3b3fba0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine FTP-Verbindung erstellt, indem Sie [!DNL Flow Service] API und den eindeutigen ID-Wert der Verbindung erhalten haben. Sie können diese Verbindungs-ID verwenden, um [Cloud-Datenspeicherung mithilfe der Flow Service API erkunden](../../explore/cloud-storage.md).
