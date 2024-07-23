---
title: Freigeben privater Erweiterungspakete in der Reactor-API
description: Erfahren Sie, wie Sie anderen Unternehmen gestatten, private Erweiterungspakete in der Reactor-API freizugeben.
source-git-commit: ea9a2bb00d3ce59e28ea4cda0d30945e77aa95cb
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 3%

---


# Freigeben privater Erweiterungspakete

>[!NOTE]
>
>Benutzer mit der Berechtigung &quot;`develop_extensions`&quot;in der Eigentümerorganisation des Erweiterungspakets können die Nutzungsberechtigungen für dieses Erweiterungspaket erstellen, auflisten und löschen. Benutzer in einer autorisierten Organisation, die über die Berechtigung `manage_properties` verfügen, dürfen die Nutzungsberechtigungen für das Erweiterungspaket für ihre Organisation nur auflisten und ihren Status auf `accepted` aktualisieren, wenn sie dieses Erweiterungspaket verwenden möchten, oder auf `rejected` , wenn sie es nicht verwenden möchten.

Inhaber von Erweiterungspaketen können anderen Unternehmen die Erlaubnis erteilen, ihre privaten Versionen über die Reactor-API zu nutzen. Für jedes genehmigte Unternehmen wird eine Nutzungslizenz für ein Erweiterungspaket erteilt. Diese Autorisierung gilt für alle aktuellen und zukünftigen privaten Versionen des Pakets.

Dieses Handbuch bietet einen allgemeinen Überblick darüber, wie Sie Nutzungsberechtigungen für Erweiterungspakete konfigurieren. Ausführlichere Anleitungen zum Verwalten von Berechtigungen in der Reactor-API, einschließlich Beispiel-JSON der Struktur einer Autorisierung, finden Sie im [Endpunkt zur Autorisierung der Package-Nutzung durch Erweiterungspakete](../endpoints/extension-package-usage-authorizations.md).

## Autorisierung erstellen {#create-authorization}

Um eine neue Autorisierung zu erstellen, müssen Sie über die Berechtigung `develop_extensions` verfügen. Das folgende Beispiel zeigt, wie Sie eine Nutzungsautorisierung für ein Erweiterungspaket mit dem `authorized_org_id` des Unternehmens erstellen können, das Sie autorisieren möchten.

**API-Format**

```http
POST /extension_packages/{EXTENSION_PACKAGE_ID}/extension_package_usage_authorizations
```

| Parameter | Beschreibung |
| --- | --- |
| `EXTENSION_PACKAGE_ID` | Die `ID` des Erweiterungspakets, für das Sie eine Autorisierung erstellen möchten. |

{style="table-layout:auto"}

**Anfrage**

Mit der folgenden Anfrage wird eine neue Autorisierung des Erweiterungspakets für das angegebene Unternehmen erstellt.

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

Der Anfangsstatus der Autorisierung befindet sich im Schritt `pending_approval` . Vor der Verwendung des Erweiterungspakets muss das Unternehmen die Genehmigung erteilen. Benutzer des Unternehmens können das private Erweiterungspaket durchsuchen, während die Autorisierung noch aussteht, es jedoch nicht installieren kann und nicht in ihrem Erweiterungskatalog zu finden ist.

## Genehmigung {#approve-authorization}

Um eine Autorisierung zu genehmigen, müssen Sie über die `manage_properties` -Rechte verfügen. Als autorisiertes Unternehmen müssen Sie eine PATCH-Anfrage an die Autorisierung der Package-Nutzung der Erweiterung senden, einschließlich der `ID` der Autorisierung und den auf `approved` festgelegten Status festlegen.

**API-Format**

```http
PATCH //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | Die `ID` der Autorisierung, die Sie genehmigen möchten. |

{style="table-layout:auto"}

**Anfrage**

Die folgende PATCH-Anfrage setzt die `state` einer Autorisierung auf `approved`.

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

Nachdem die Autorisierung als autorisiertes Unternehmen genehmigt wurde, können Sie jetzt das Erweiterungspaket in Ihren Eigenschaften installieren.

>[!NOTE]
>
>Wird die Genehmigung abgelehnt, kann das autorisierte Unternehmen das Erweiterungspaket nicht verwenden.

## Autorisierung löschen {#delete-authorization}

Als Eigentümer eines Erweiterungspakets können Sie die Autorisierung jederzeit widerrufen, indem Sie die Autorisierung zur Verwendung des Erweiterungspakets löschen. Dadurch wird verhindert, dass das autorisierte Unternehmen private Versionen des Erweiterungspakets im Katalog anzeigt und in seinen Eigenschaften installiert. Bereits installierte private Versionen funktionieren jedoch nach dem Löschen weiterhin wie erwartet.

**API-Format**

```http
DELETE //extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID}
```

| Parameter | Beschreibung |
| --- | --- |
| `EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID` | Die `ID` der Autorisierung, die Sie löschen möchten. |

{style="table-layout:auto"}

**Anfrage**

Mit der folgenden DELETE-Anfrage werden die Autorisierungsberechtigungen für ein Unternehmen entfernt.

```shell
curl -X DELETE \
  https://reactor.adobe.io/extension_package_usage_authorizations/{EXTENSION_PACKAGE_USAGE_AUTHORIZATION_ID} \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-Api-Key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {ORG_ID}' \
  -H "Content-Type: application/vnd.api+json" \
```
