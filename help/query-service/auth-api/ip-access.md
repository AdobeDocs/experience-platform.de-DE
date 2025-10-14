---
keywords: Experience Platform; Sicherheit; IP-Zugriff; QS-Auth; API-Handbuch; Abfrage-Service; IP-Bereiche
title: IP-Zugriffsendpunkt
description: Erfahren Sie, wie Sie IP-Bereiche für den Sandbox-Zugriff im Abfrage-Service mithilfe des IP-Zugriffs-API-Endpunkts verwalten.
role: Developer
exl-id: fc15ab50-c125-4f00-a311-81fd41697c7d
source-git-commit: d0f4a295928b000b6091172800e453d79dc44e3a
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 5%

---

# IP-Zugriffsendpunkt

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die das Add-on Data Distiller erworben haben. Weitere Informationen erhalten Sie bei Ihrer bzw. Ihrem Adobe-Support-Mitarbeitenden.

Um den Datenzugriff innerhalb einer angegebenen Abfrage-Service-Sandbox zu sichern, verwenden Sie den IP-Zugriffsendpunkt, um die zulässigen IP-Bereiche zu verwalten. Mit dieser API können Sie IP-Bereiche abrufen, konfigurieren oder löschen, die mit der ID Ihres Unternehmens verknüpft sind.

Mit der IP-Zugriffs-API können Sie die folgenden Aktionen ausführen:

- **Alle IP-Bereiche abrufen**
- **Neue IP-Bereiche festlegen**
- **Löschen vorhandener IP-Bereiche**

In diesem Dokument werden die Anfragen und Antworten behandelt, die Sie vom `/security/ip-access`-Endpunkt senden und empfangen können.

>[!NOTE]
>
>Sie müssen über ein Benutzer-Token verfügen, um diese API aufzurufen. Informationen [&#x200B; Erhalten der erforderlichen Werte für jede &#x200B;](./getting-started.md) Kopfzeilen finden Sie im Abschnitt Erste Schritte .

## Alle IP-Bereiche abrufen {#fetch-all-ip-ranges}

Rufen Sie eine Liste aller für Ihre Sandbox konfigurierten IP-Bereiche ab. Wenn keine IP-Bereiche festgelegt sind, sind standardmäßig alle IP-Adressen zulässig und die Antwort gibt in `allowedIpRanges` eine leere Liste zurück.

**API-Format**

```http
GET /security/ip-access
```

**Anfrage**

```shell
curl -X GET https://platform.adobe.io/data/foundation/queryauth/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit einer Liste der zulässigen IP-Bereiche der Sandbox zurückgegeben.

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

Die folgende Tabelle enthält eine Beschreibung und ein Beispiel der Eigenschaften des Antwortschemas:

| Eigenschaft | Beschreibung | Beispiel |
|------------------|---------------------------------------------|-----------------------------------------------------------------------------------------------|
| `imsOrg` | Organisations-ID für die Sandbox. | `{ORG_ID}` |
| `sandboxName` | Name der Sandbox, für die IP-Einschränkungen gelten. | `prod` |
| `channel` | Der Zugriffsmodus für IP-Einschränkungen. Derzeit ist der einzige akzeptierte Wert `data_distiller`. Dieser Wert gibt an, dass IP-Einschränkungen auf PSQL- oder JDBC-Verbindungen angewendet werden. | `data_distiller` |
| `allowedIpRanges` | Liste der zulässigen IPs im CIDR- oder festen IP-Format. Jeder Eintrag kann eine optionale Beschreibung enthalten. | `[{"ipRange": "136.23.110.0/23", "description": "VPN-1 gateway IPs"}]` |

>[!NOTE]
>
>Das Feld `allowedIpRanges` kann zwei Arten von IP-Spezifikationen enthalten:<br><ul><li>**CIDR.**: Standard-CIDR-Notation (z. B. `"136.23.110.0/23"`) zum Definieren von IP-Bereichen.</li><li>**Feste IP**: Einzelne IPs für einzelne Zugriffsberechtigungen (z. B. `"101.10.1.1"`).</li></ul>

## Neue IP-Bereiche festlegen

Bestehende IP-Bereiche überschreiben, indem eine neue Liste für die Sandbox festgelegt wird. Dieser Vorgang erfordert eine vollständige Liste der IP-Bereiche, einschließlich der unveränderten Bereiche.

**API-Format**

```http
PUT /security/ip-access
```

**Anfrage**

```shell
curl -X PUT https://platform.adobe.io/data/foundation/queryauth/security/ip-access \
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

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zu den neu konfigurierten IP-Bereichen zurückgegeben.

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

Entfernen Sie alle konfigurierten IP-Bereiche für die Sandbox. Diese Aktion löscht die IP-Bereiche und gibt die gelöschte IP-Liste zurück.

>[!NOTE]
>
>Der Löschvorgang gilt für die Organisations-ID (`imsOrg`) und betrifft alle für die Sandbox konfigurierten IP-Bereiche.

**API-Format**

```http
DELETE /security/ip-access
```

**Anfrage**

```shell
curl -X DELETE https://platform.adobe.io/data/foundation/queryauth/security/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}'
```

**Antwort**

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 mit Details zu den gelöschten IP-Bereichen zurückgegeben.

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
