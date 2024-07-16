---
title: Erstellen einer PathFactory-Basisverbindung mit der Flow Service-API
description: Erfahren Sie, wie Sie Ihr PathFactory-Konto mithilfe der Flow Service-API gegen Experience Platform authentifizieren.
badge: Beta
exl-id: 2bdfe38b-d3f7-480f-87c6-0b98b9521be2
source-git-commit: ca17854830edabaf2bd74265258d6f0096f2888e
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 46%

---

# Erstellen einer [!DNL PathFactory]-Basisverbindung mithilfe der [!DNL Flow Service]-API

Eine Basisverbindung stellt die authentifizierte Verbindung zwischen einer Quelle und Adobe Experience Platform dar.

In diesem Dokument erfahren Sie, wie Sie mit der [[!DNL Flow Service] API](<https://www.adobe.io/experience-platform-apis/references/flow-service/>) eine Basisverbindung für [!DNL PathFactory] erstellen.

## Erste Schritte

Dieses Handbuch setzt ein Verständnis der folgenden Komponenten von Experience Platform voraus:

* [Quellen](../../../../home.md): Experience Platform ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Platform-Services zu strukturieren, zu kennzeichnen und anzureichern.
* [Sandboxes](../../../../../sandboxes/home.md): Experience Platform bietet virtuelle Sandboxes, die eine einzelne Platform-Instanz in separate virtuelle Umgebungen unterteilen, damit Sie Programme für digitale Erlebnisse entwickeln und weiterentwickeln können.

### Verwenden von Platform-APIs

Informationen darüber, wie Sie Platform-APIs erfolgreich aufrufen können, finden Sie im Handbuch unter [Erste Schritte mit Platform-APIs](../../../../../landing/api-guide.md).

Im folgenden Abschnitt finden Sie weitere Informationen, die Sie benötigen, um mithilfe der [!DNL Flow Service] -API erfolgreich eine Verbindung zu [!DNL PathFactory] herstellen zu können.

### Erforderliche Anmeldedaten sammeln {#gather-credentials}

Um auf Ihr PathFactory-Konto in Platform zuzugreifen, müssen Sie die folgenden Werte angeben:

| Anmeldedaten | Beschreibung |
| ---------- | ----------- |
| Benutzername | Ihr [!DNL PathFactory] -Konto-Benutzername. Dies ist für die Identifikation Ihres Kontos im System unerlässlich. |
| Kennwort | Das Ihrem [!DNL PathFactory]-Konto zugeordnete Kennwort. Stellen Sie sicher, dass dies geschützt ist, um einen unbefugten Zugriff zu verhindern. |
| Domain | Die mit Ihrem [!DNL PathFactory] -Konto verknüpfte Domäne. Dies bezieht sich normalerweise auf die eindeutige Kennung in Ihrer [!DNL PathFactory]-URL. |
| Zugriffs-Token | Ein eindeutiges Token für die API-Authentifizierung, um eine sichere Kommunikation zwischen Ihren Systemen und [!DNL PathFactory] sicherzustellen. |
| API-Endpunkte | Bestimmte API-Endpunkte für den Zugriff auf Daten: Besucher, Sitzungen und Seitenansichten. Jeder Endpunkt entspricht verschiedenen Datensätzen, die Sie abrufen können. **Hinweis:** Diese sind durch [!DNL PathFactory] vordefiniert und spezifisch für die Daten, auf die Sie zugreifen möchten: <ul><li>**Besucherendpunkt**: `/api/public/v3/data_lake_apis/visitors.json`</li><li>**Sitzungsendpunkt**: `/api/public/v3/data_lake_apis/sessions.json`</li><li>**Endpunkt &quot;Seitenansichten&quot;**: `/api/public/v3/data_lake_apis/page_views.json`</li></ul> |

Weitere Informationen zum Sichern und Verwenden Ihrer Anmeldeinformationen sowie zum Abrufen und Aktualisieren Ihres Zugriffstokens finden Sie im [[!DNL PathFactory] Support-Center](https://support.pathfactory.com/categories/adobe/). Diese Ressource enthält umfassende Anleitungen zur Verwaltung Ihrer Anmeldedaten und zur Sicherstellung einer effektiven und sicheren API-Integration.

## Erstellen einer Basisverbindung

Bei einer Basisverbindung werden Informationen zwischen Ihrer Quelle und Platform gespeichert, einschließlich der Authentifizierungsdaten Ihrer Quelle, des aktuellen Verbindungsstatus und Ihrer eindeutigen Kennung der Basisverbindung. Mit der Kennung der Basisverbindung können Sie Dateien aus Ihrer Quelle heraus analysieren und darin navigieren und die spezifischen Elemente identifizieren, die Sie erfassen möchten, einschließlich Informationen zu ihren Datentypen und Formaten.

Um eine Basis-Verbindungs-ID zu erstellen, stellen Sie eine POST-Anfrage an den `/connections` -Endpunkt und geben Sie dabei Ihre [!DNL PathFactory]-Authentifizierungsdaten als Teil des Anfragetexts an.

**API-Format**

```https
POST /connections
```

**Anfrage**

Die folgende Anfrage erstellt eine Basisverbindung für [!DNL PathFactory]:

```shell
curl -X POST \
  'https://platform.adobe.io/data/foundation/flowservice/connections' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H 'x-sandbox-name: {SANDBOX_NAME}' \
  -H 'Content-Type: application/json' \
  -d '{
      "name": "PathFactory base connection",
      "description": "PathFactory base connection",
      "auth": {
          "specName": "Basic Authentication",
          "params": {
              "host": "acme-ab12c3d4e5fg6hijk7lmnop8qrst"
              "clientId": "pathfactory",
              "clientSecret": "xxxx"
          }
      },
      "connectionSpec": {
          "id": "ea1c2a08-b722-11eb-8529-0242ac130003",
          "version": "1.0"
      }
  }'
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `auth.params.clientId` | Die mit Ihrer [!DNL PathFactory] -Anwendung verknüpfte Client-ID. |
| `auth.params.clientSecret` | Das Client-Geheimnis, das Ihrer [!DNL PathFactory]-Anwendung zugeordnet ist. |
| `connectionSpec.id` | Die [!DNL PathFactory] Verbindungsspezifikations-ID: `ea1c2a08-b722-11eb-8529-0242ac130003`. |

**Antwort**

Eine erfolgreiche Antwort gibt die neu erstellte Verbindung zurück, einschließlich der eindeutigen Verbindungskennung (`id`). Diese ID ist erforderlich, um Ihre Daten im nächsten Tutorial zu untersuchen.

```json
{
    "id": "2fce94c1-9a93-4971-8e94-c19a93097129",
    "etag": "\"d403848a-0000-0200-0000-5e978f7b0000\""
}
```

## Nächste Schritte

In diesem Tutorial haben Sie eine [!DNL PathFactory]-Basisverbindung mithilfe der [!DNL Flow Service]-API erstellt. Sie können diese Basisverbindungs-ID in den folgenden Tutorials verwenden:

* [Erkunden von Struktur und Inhalten Ihrer Datentabellen mithilfe der  [!DNL Flow Service] -API](../../explore/tabular.md)
* [Erstellen eines Datenflusses, um Daten zur Marketing-Automatisierung mithilfe der  [!DNL Flow Service] -API auf Platform zu übertragen](../../collect/marketing-automation.md)
