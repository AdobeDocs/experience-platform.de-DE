---
keywords: Experience Platform; Sicherheit; IP-Zugriff; QS-Auth; API-Handbuch; Query Service; IP-Bereiche
title: IP-Zugriffs-Endpunkt
description: Erfahren Sie, wie Sie IP-Bereiche für den Sandbox-Zugriff in Query Service mithilfe des IP Access API-Endpunkts verwalten.
role: Developer
source-git-commit: 23e5260133f0f16ac30d14346c227a21f251b7e1
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 3%

---

# IP-Zugriffs-Endpunkt

Um den Datenzugriff innerhalb einer angegebenen Query Service-Sandbox zu sichern, verwenden Sie den IP-Zugriffendpunkt, um zulässige IP-Bereiche zu verwalten. Mit dieser API können Sie IP-Bereiche abrufen, konfigurieren oder löschen, die mit der ID Ihres Unternehmens verknüpft sind.

Sie können mit der IP-Zugriffs-API die folgenden Aktionen durchführen:

- **Abrufen aller IP-Bereiche**
- **Festlegen neuer IP-Bereiche**
- **Vorhandene IP-Bereiche löschen**

Dieses Dokument behandelt die Anfragen und Antworten, die Sie vom `/security/ip-access` -Endpunkt aus senden und empfangen können.

>[!NOTE]
>
>Sie müssen über ein Benutzer-Token verfügen, um diese API aufrufen zu können. Informationen zum Erwerb der erforderlichen Werte für die einzelnen Header finden Sie im Leitfaden [Erste Schritte](./getting-started.md) .

## Abrufen aller IP-Bereiche {#fetch-all-ip-ranges}

Rufen Sie eine Liste aller für Ihre Sandbox konfigurierten IP-Bereiche ab. Wenn keine IP-Bereiche festgelegt sind, sind standardmäßig alle IPs zulässig und die Antwort gibt eine leere Liste in `allowedIpRanges` zurück.

**API-Format**

```http
GET /security/ip-access
```

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einer Liste der zulässigen IP-Bereiche der Sandbox zurück.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "101.10.1.1"}
  ]
}
```

Die folgende Tabelle enthält eine Beschreibung und ein Beispiel für die Eigenschaften des Antwortschemas:

| Eigenschaft | Beschreibung | Beispiel |
|------------------|---------------------------------------------|-----------------------------------------------------------------------------------------------|
| `imsOrg` | Organisations-ID für die Sandbox. | `{ORG_ID}` |
| `sandboxName` | Name der Sandbox, in der IP-Einschränkungen gelten. | `prod` |
| `channel` | Der Zugriffsmodus für IP-Einschränkungen. Derzeit ist der einzige akzeptierte Wert `data_distiller`. Dieser Wert bedeutet, dass IP-Einschränkungen auf PSQL- oder JDBC-Verbindungen angewendet werden. | `data_distiller` |
| `allowedIpRanges` | Liste der zulässigen IPs im CIDR- oder festem IP-Format. Jeder Eintrag kann eine optionale Beschreibung enthalten. | `[{"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"}]` |

>[!NOTE]
>
>Das Feld `allowedIpRanges` kann zwei Arten von IP-Spezifikationen enthalten:<br><ul><li>**CIDR**: Standardmäßige CIDR-Notation (z. B. `"136.23.110.0/23"`) zur Definition von IP-Bereichen.</li><li>**Feste IP-Adresse**: Einzelne IP-Adressen für individuelle Zugriffsberechtigungen (z. B. `"101.10.1.1"`).</li></ul>

## Einrichten neuer IP-Bereiche

Überschreiben Sie vorhandene IP-Bereiche, indem Sie eine neue Liste für die Sandbox festlegen. Für diesen Vorgang ist eine vollständige Liste der IP-Bereiche erforderlich, einschließlich der Bereiche, die unverändert bleiben.

**API-Format**

```http
PUT /security/ip-access
```

**Anfrage**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
     "ipRanges": [
       {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
       {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
       {"ipRange": "101.10.1.1"},
       {"ipRange": "163.77.30.9", "description": "Test server IP"}
     ]
   }'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu den neu konfigurierten IP-Bereichen zurück.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "allowedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```

## IP-Bereiche löschen {#delete-ip-ranges}

Entfernen Sie alle konfigurierten IP-Bereiche für die Sandbox. Durch diese Aktion werden die IP-Bereiche gelöscht und die gelöschte IP-Liste zurückgegeben.

>[!NOTE]
>
>Der Löschvorgang gilt für die Organisations-ID (`imsOrg`) und betrifft alle für die Sandbox konfigurierten IP-Bereiche.

**API-Format**

```http
DELETE /security/ip-access
```

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/query/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit Details zu den gelöschten IP-Bereichen zurück.

```json
{
  "imsOrg": "{ORG_ID}",
  "sandboxName": "prod",
  "channel": "data_distiller",
  "deletedIpRanges": [
    {"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"},
    {"ipRange": "17.102.17.0/23", "description": "VPN-2 gateway IPs"},
    {"ipRange": "101.10.1.1"},
    {"ipRange": "163.77.30.9", "description": "Test server IP"}
  ]
}
```

