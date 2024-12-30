---
keywords: Experience Platform; Sicherheit; IP-Zugriff; Validierung; API-Handbuch; Abfrage-Service; IP-Verifizierung
title: IP-Validierungsendpunkt
description: Erfahren Sie, wie Sie den IP-Zugriff für Sandboxes im Abfrage-Service mithilfe des API-Endpunkts für die IP-Validierung validieren.
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
>Diese Funktion steht Kunden zur Verfügung, die das Add-on Data Distiller erworben haben. Weitere Informationen erhalten Sie bei Ihrer bzw. Ihrem Adobe-Support-Mitarbeitenden.

Verwenden Sie den API-Endpunkt für die IP-Validierung, um zu überprüfen, ob eine angegebene IP-Adresse für den Zugriff auf eine bestimmte Sandbox im Abfrage-Service zulässig ist. Diese Prüfung bestätigt, ob Zugriffsbeschränkungen gelten oder ob eine IP-Adresse Zugriff auf Daten innerhalb einer Sandbox hat.

## IP für den Sandbox-Zugriff validieren {#validate-ip-for-sandbox-access}

Verwenden Sie den IP-Validierungs-Endpunkt , um zu überprüfen, ob eine bestimmte IP-Adresse Zugriff auf Daten der angegebenen Sandbox hat. Wenn für die Sandbox keine IP-Einschränkungen konfiguriert sind, sind standardmäßig alle IP-Adressen zulässig. Wenn IP- oder CIDR-Einschränkungen vorhanden sind, überprüft diese API, ob die angegebene IP-Adresse mit konfigurierten Bereichen übereinstimmt.

>[!NOTE]
>
>Sie können auf diesen Endpunkt entweder mit **Benutzer-Token** oder **Service-Token** zugreifen. Spezifische Rollenanforderungen sind nicht erforderlich.

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

Eine erfolgreiche Antwort gibt den HTTP-Status-Code 200 mit einem booleschen Wert zurück, der angibt, ob die IP zulässig ist.

>[!NOTE]
>
>Das `isAllowed` Feld in der Antwort gibt `true` zurück, wenn die angegebene IP auf die Sandbox zugreifen darf und andernfalls `false`. Diese API unterstützt die dynamische Validierung des Zugriffs und gewährleistet die Einhaltung von Sicherheitsvorschriften für Sandbox-Umgebungen.

```json
{
"isAllowed": true
}
```
