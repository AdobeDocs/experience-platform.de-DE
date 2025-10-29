---
title: Freigeben privater Erweiterungspakete in der Reactor-API
description: Erfahren Sie, wie Sie andere Unternehmen autorisieren, private Erweiterungspakete in der Reactor-API freizugeben.
exl-id: 3300a630-6d22-46e1-8b1b-b5d12a3ea44c
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 3%

---

# Freigeben privater Erweiterungspakete

>[!NOTE]
>
>Benutzer mit der Berechtigung `develop_extensions` in der Organisation der Eigentümer von Erweiterungspaketen können Berechtigungen zur Verwendung von Erweiterungspaketen für dieses Erweiterungspaket erstellen, auflisten und löschen. Benutzer in einer autorisierten Organisation, die über die Berechtigung `manage_properties` verfügen, dürfen nur die Benutzungsberechtigungen für ihr Unternehmen für Erweiterungspakete auflisten und ihren Status auf `accepted` aktualisieren, wenn sie dieses Erweiterungspaket verwenden möchten, oder auf `rejected`, wenn sie es nicht verwenden möchten.

Besitzer von Erweiterungspaketen können anderen Unternehmen über die Reactor-API die Berechtigung zur Nutzung ihrer privaten Versionen erteilen. Jedes genehmigte Unternehmen erhält eine Nutzungslizenz für ein Erweiterungspaket, und diese Autorisierung gilt für alle aktuellen und künftigen privaten Versionen des Pakets.

Dieses Handbuch bietet einen allgemeinen Überblick darüber, wie Sie die Verwendungsautorisierungen von Erweiterungspaketen konfigurieren. Ausführlichere Anleitungen zum Verwalten von Berechtigungen in der Reactor-API, einschließlich einer Beispiel-JSON zur Autorisierungsstruktur, finden Sie im [Handbuch für Endpunkte zur Autorisierung der Verwendung von Erweiterungspaketen](../endpoints/extension-package-usage-authorizations.md).

## Erstellen einer Autorisierung {#create-authorization}

Um eine neue Autorisierung zu erstellen, benötigen Sie das `develop_extensions`. Das folgende Beispiel zeigt, wie Sie eine Autorisierung der Verwendung von Erweiterungspaketen für ein Erweiterungspaket mit der `authorized_org_id` des Unternehmens erstellen können, das Sie autorisieren möchten.

**API-Format**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parameter | Beschreibung |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Die `ID` des Erweiterungspakets, für das Sie eine Autorisierung erstellen möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende Anfrage erstellt ein neues Erweiterungspaket für die Autorisierung des angegebenen Unternehmens.

```shell
curl -X POST \
  https://reactor.adobe.io/extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "authorized_org_id": "{ORG_ID}"
          },
          "type": "extension_package_usage_authorizations"
        }
      } 
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `attributes.authorized_org_id` | Die `ID` der Organisation, die Sie autorisieren möchten. |

{style="table-layout:auto"}

Der ursprüngliche Status der Autorisierung befindet sich in der `pending_approval`. Vor Verwendung des Erweiterungspakets muss die Firma die Autorisierung genehmigen. Benutzer des Unternehmens können das private Erweiterungspaket durchsuchen, während die Autorisierung noch nicht genehmigt ist, sie können es jedoch nicht installieren und nicht in ihrem Erweiterungskatalog finden.

## Autorisierung genehmigen {#approve-authorization}

Um eine Autorisierung zu genehmigen, müssen Sie über die `manage_properties` verfügen. Als autorisiertes Unternehmen müssen Sie eine PATCH-Anfrage an die Autorisierung zur Verwendung des Erweiterungspakets senden, einschließlich der `ID` der Autorisierung, und den Status auf `approved` setzen.

**API-Format**

```http
PATCH //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | Die `ID` der Autorisierung, die Sie genehmigen möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende PATCH-Anfrage legt die `state` einer Autorisierung auf `approved` fest.

```shell
curl -X PATCH \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
  -d '{
        "data": {
          "attributes": {
            "state": "approved"
            },
            "id": ":extension_package_usage_authorization_id",
            "type": "extension_package_usage_authorizations"
        }
      }
```

Sobald die Autorisierung genehmigt wurde, können Sie als autorisiertes Unternehmen das Erweiterungspaket jetzt in Ihren Eigenschaften installieren.

>[!NOTE]
>
>Wird die Autorisierung abgelehnt, kann das autorisierte Unternehmen das Erweiterungspaket nicht verwenden.

## Autorisierung löschen {#delete-authorization}

Als Eigentümer eines Erweiterungspakets können Sie die Autorisierung jederzeit widerrufen, indem Sie die Autorisierung zur Verwendung des Erweiterungspakets löschen. Dadurch kann die autorisierte Firma keine privaten Versionen des Erweiterungspakets im Katalog anzeigen und in den Eigenschaften installieren. Bereits installierte private Versionen funktionieren jedoch nach dem Löschen weiterhin wie erwartet.

**API-Format**

```http
DELETE //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | Die `ID` der Autorisierung, die Sie löschen möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende DELETE-Anfrage entfernt Autorisierungsberechtigungen für ein Unternehmen.

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
```
