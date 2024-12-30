---
title: Erstellen einer Phoenix-Basisverbindung mithilfe der Flow Service-API
description: Erfahren Sie, wie Sie mithilfe der Flow Service-API eine Phoenix-Datenbank mit Adobe Experience Platform verbinden.
exl-id: b69d9593-06fe-4fff-88a9-7860e4e45eb7
source-git-commit: 9ca4f19f7b59f075250bce7035303e11d3f3710f
workflow-type: tm+mt
source-wordcount: '558'
ht-degree: 38%

---

# Erstellen einer [!DNL Phoenix]-Basisverbindung mithilfe der [!DNL Flow Service]-API

>[!WARNING]
>
>Die [!DNL Phoenix] wird Ende Juni 2025 eingestellt.

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

In diesem Tutorial erfahren Sie, wie Sie mithilfe der [!DNL Flow Service]-API eine Basisverbindung erstellen und Ihr [!DNL Phoenix]-Konto mit Adobe Experience Platform verbinden.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Experience Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service]-API eine Verbindung zu [!DNL Phoenix] herstellen zu können.

### Sammeln erforderlicher Anmeldedaten

Sie müssen die folgenden Authentifizierungsdaten angeben, um Ihr [!DNL Phoenix]-Konto mit Experience Platform zu verbinden.

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| `host` | Die IP-Adresse oder der Hostname des [!DNL Phoenix]. |
| `username` | Der Benutzername, mit dem Sie auf [!DNL Phoenix] Server zugreifen. |
| `password` | Das Kennwort für den Benutzer. |
| `port` | Der TCP-Port, den der [!DNL Phoenix]-Server verwendet, um auf Client-Verbindungen zu warten. Wenn Sie eine Verbindung zu [!DNL Azure HDInsights] herstellen, geben Sie den Port als 443 an. Wenn dieser Parameter nicht angegeben wird, ist der Standardwert 8765. |
| `httpPath` | Die dem [!DNL Phoenix]-Server entsprechende Teil-URL. Geben Sie /hbasephoenix0 an, wenn Sie [!DNL Azure] HDInsights-Cluster verwenden. |
| `enableSsl` | Ein boolescher Wert. Gibt an, ob die Verbindungen zum Server mit SSL verschlüsselt werden. |
| `connectionSpec.id` | Die Verbindungsspezifikation gibt die Connector-Eigenschaften einer Quelle zurück, einschließlich der Authentifizierungsspezifikationen für die Erstellung der Basis- und Quellverbindungen. Die Verbindungsspezifikations-ID für [!DNL Phoenix] lautet: `102706fb-a5cd-42ee-afe0-bc42f017ff43` |

Weitere Informationen zu den ersten Schritten finden Sie [diesem Phoenix-Dokument](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

### Verwenden von Platform-APIs

Informationen zum Aufrufen von Platform-APIs finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungs-Anmeldedaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basisverbindung zu erstellen, stellen Sie eine POST-Anfrage an den `/connections`-Endpunkt, während Sie im Anfragetext Ihre [!DNL Phoenix] Authentifizierungsdaten angeben.

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
| `auth.params.host` | Der Host des [!DNL Phoenix]. |
| `auth.params.username` | Der Benutzername, der Ihrer [!DNL Phoenix]-Verbindung zugeordnet ist. |
| `auth.params.password` | Das Passwort für Ihre [!DNL Phoenix]. |
| `auth.params.port` | Der TCP-Port für Ihre [!DNL Phoenix]. |
| `auth.params.httpPath` | Der teilweise HTTP-Pfad für Ihre [!DNL Phoenix]. |
| `auth.params.enableSsl` | Der boolesche Wert, der angibt, ob die Verbindungen zum Server mit SSL verschlüsselt werden. |
| `connectionSpec.id` | Die Spezifikations-ID der [!DNL Phoenix]-Verbindung: `102706fb-a5cd-42ee-afe0-bc42f017ff43`. |

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
* [Erstellen eines Datenflusses, um Datenbankdaten mithilfe der -API  [!DNL Flow Service]  Platform zu übertragen](../../collect/database-nosql.md)
