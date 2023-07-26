---
title: Erstellen einer Phoenix-Basisverbindung mit der Flow Service-API
description: Erfahren Sie, wie Sie mithilfe der Flow Service-API eine Phoenix-Datenbank mit Adobe Experience Platform verbinden.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: efffd6ce1ed541ce20ee6500e42165465f2fa6a0
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 41%

---

# Erstellen einer [!DNL Phoenix]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

In diesem Tutorial erfahren Sie, wie Sie eine Basisverbindung erstellen und Ihre [!DNL Phoenix] -Konto in Adobe Experience Platform mithilfe der [!DNL Flow Service] API.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Erfassung von Daten aus verschiedenen Quellen und bietet Ihnen gleichzeitig die Möglichkeit, eingehende Daten mithilfe von Experience Platform Services zu strukturieren, zu beschriften und zu erweitern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen aufteilen, um die Entwicklung und Weiterentwicklung von Programmen für digitale Erlebnisse zu erleichtern.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um eine erfolgreiche Verbindung zu [!DNL Phoenix] mithilfe der [!DNL Flow Service] API.

### Sammeln erforderlicher Anmeldeinformationen

Sie müssen die folgenden Authentifizierungsberechtigungen angeben, um Ihre [!DNL Phoenix] -Konto in die Experience Platform.

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `host` | Die IP-Adresse oder der Hostname der [!DNL Phoenix] Server. |
| `username` | Der Benutzername, mit dem Sie auf [!DNL Phoenix] Server. |
| `password` | Das dem Benutzer entsprechende Kennwort. |
| `port` | Der TCP-Port, der die [!DNL Phoenix] -Server verwendet , um auf Client-Verbindungen zu warten. Wenn Sie eine Verbindung zu [!DNL Azure HDInsights], und geben Sie dann den Anschluss als 443 an. Wenn dieser Parameter nicht angegeben wird, wird der Standardwert 8765 verwendet. |
| `httpPath` | Die Teil-URL, die der [!DNL Phoenix] Server. Geben Sie /hbasephoenix0 an, wenn Sie [!DNL Azure] HDInsights-Cluster. |
| `enableSsl` | Ein boolescher Wert. Gibt an, ob die Verbindungen zum Server mit SSL verschlüsselt werden. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Phoenix] ist: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Weitere Informationen zu den ersten Schritten finden Sie unter [diesem Phoenix-Dokument](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindung zu erstellen, stellen Sie eine POST-Anfrage an die `/connections` Endpunkt beim Bereitstellen [!DNL Phoenix] Authentifizierungsberechtigungen im Anfragetext.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL Phoenix]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "Phoenix test connection",
      "description": "Phoenix test connection",
      "auth": {
          "specName": "Basic Authentication",
      "params": {
          "host":  "{HOST}",
          "username": "{USERNAME}",
          "password":"{PASSWORD}",
          "port": {PORT},
          "httpPath": "{PATH}",
          "enableSsl": {SSL}
          }
      },
      "connectionSpec": {
          "id": "102706fb-a5cd-42ee-afe0-bc42f017ff43",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| --------- | ----------- |
| `auth.params.host` | Der Host der [!DNL Phoenix] Server. |
| `auth.params.username` | Der mit Ihrer [!DNL Phoenix] Verbindung herzustellen. |
| `auth.params.password` | Das Kennwort für Ihre [!DNL Phoenix] Verbindung herzustellen. |
| `auth.params.port` | Der TCP-Port für Ihre [!DNL Phoenix] Verbindung herzustellen. |
| `auth.params.httpPath` | Der teilweise HTTP-Pfad für Ihre [!DNL Phoenix] Verbindung herzustellen. |
| `auth.params.enableSsl` | Der boolesche Wert, der angibt, ob die Verbindungen zum Server mit SSL verschlüsselt werden. |
| `connectionSpec.id` | Die [!DNL Phoenix]-Verbindungsspezifikations-ID: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

**Antwort**

Eine erfolgreiche Antwort gibt Details der neu erstellten Verbindung zurück, einschließlich ihrer eindeutigen Kennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "0d982fff-c443-403e-982f-ffc443f03e37",
    "etag": "\"830082dc-0000-0200-0000-5e84ee560000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL Phoenix]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen Sie einen Datenfluss, um Datenbankdaten mit der [!DNL Flow Service] API](../../collect/database-nosql.md)
