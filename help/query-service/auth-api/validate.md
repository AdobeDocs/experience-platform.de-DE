---
keywords: Experience Platform; Sicherheit; IP-Zugriff; Validierung; API-Handbuch; Query Service; IP-Verifizierung
title: IP-Validierungsendpunkt
description: Erfahren Sie, wie Sie den IP-Zugriff für Sandboxes in Query Service mithilfe des IP-Validierungs-API-Endpunkts überprüfen.
role: Developer
exl-id: 4ce9ab1c-e333-4ed5-a430-43ffec36a46d
source-git-commit: bf696c8836407a2fea82e9078201cb1f5004bcf8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 4%

---

# IP-Validierungsendpunkt

>[!AVAILABILITY]
>
>Diese Funktion steht Kunden zur Verfügung, die das Data Distiller-Add-on erworben haben. Weitere Informationen erhalten Sie bei Ihrer bzw. Ihrem Adobe-Support-Mitarbeitenden.

Verwenden Sie den IP-Validierungs-API-Endpunkt, um zu überprüfen, ob eine bestimmte IP-Adresse berechtigt ist, in Query Service auf eine bestimmte Sandbox zuzugreifen. Diese Prüfung bestätigt, ob Zugriffsbeschränkungen gelten oder ob eine IP-Adresse berechtigt ist, auf Daten in einer Sandbox zuzugreifen.

## Überprüfen der IP-Adresse für den Sandbox-Zugriff {#validate-ip-for-sandbox-access}

Verwenden Sie den IP-Validierungsendpunkt, um zu überprüfen, ob eine bestimmte IP-Adresse Zugriff auf Daten für die angegebene Sandbox hat. Wenn für die Sandbox keine IP-Einschränkungen konfiguriert sind, sind standardmäßig alle IP-Adressen zulässig. Wenn IP- oder CIDR-Beschränkungen bestehen, überprüft diese API, ob die angegebene IP-Adresse mit den konfigurierten Bereichen übereinstimmt.

>[!NOTE]
>
>Sie können auf diesen Endpunkt mit **Benutzer-Token** oder **Dienst-Token** zugreifen. Es sind keine spezifischen Rollenanforderungen erforderlich.

**API-Format**

```http
POST /security/validate/ip-access
```

**Anfrage**

```shell
curl -X POST https://platform.adobe.io/data/foundation/query/security/validate/ip-access \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'Content-Type: application/json' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
 -d '{
       "ipAddress": "197.2.0.2"
     }'
```

**Antwort**

Eine erfolgreiche Antwort gibt den HTTP-Status 200 mit einem booleschen Wert zurück, der angibt, ob die IP zulässig ist.

>[!NOTE]
>
>Das Feld `isAllowed` in der Antwort gibt `true` zurück, wenn die bereitgestellte IP Zugriff auf die Sandbox hat, andernfalls `false`. Diese API unterstützt die dynamische Validierung des Zugriffs und die Gewährleistung der Sicherheitskonformität für Sandbox-Umgebungen.

```json
{
"isAllowed": true
}
```
