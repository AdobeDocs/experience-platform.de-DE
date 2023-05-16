---
description: Auf dieser Seite wird der API-Aufruf zum Löschen einer vorhandenen Zielgruppenvorlage über Adobe Experience Platform Destination SDK veranschaulicht.
title: Löschen von Zielgruppenvorlagen
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 42%

---


# Löschen von Zielgruppenvorlagen

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie zum Löschen einer Zielgruppenvorlage verwenden können. Verwenden Sie dazu die `/authoring/audience-templates` API-Endpunkt.

Eine ausführliche Beschreibung der Funktionen, die Sie über diesen Endpunkt konfigurieren können, finden Sie unter [Zielgruppen-Metadatenverwaltung](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Alle von Destination SDK unterstützten Parameternamen und Werte sind **Groß-/Kleinschreibung**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit API-Vorgängen für Zielgruppenvorlagen {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Löschen von Zielgruppenvorlagen {#delete}

Sie können eine [vorhandene](create-audience-template.md) Zielgruppenvorlage `DELETE` Anfrage an `/authoring/audience-templates` Endpunkt mit der `{INSTANCE_ID}`der Zielgruppenvorlage, die Sie löschen möchten.

So rufen Sie eine vorhandene Zielgruppenvorlage und die zugehörigen `{INSTANCE_ID}`, siehe Artikel zu [Abrufen einer Zielgruppenvorlage](retrieve-audience-template.md).

**API-Format**

```http
DELETE /authoring/audience-templates/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{INSTANCE_ID}` | Die `ID` der Zielgruppenvorlage, die Sie löschen möchten. |

+++Anfrage

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/audience-templates/{INSTANCE_ID} \
 -H 'Authorization: Bearer {ACCESS_TOKEN}' \
 -H 'x-gw-ims-org-id: {ORG_ID}' \
 -H 'x-api-key: {API_KEY}' \
 -H 'x-sandbox-name: {SANDBOX_NAME}' \
```

+++

+++Antwort

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zusammen mit einer leeren HTTP-Antwort zurück.

+++

## Umgang mit API-Fehlern {#error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie eine Zielgruppenvorlage mithilfe der `/authoring/audience-templates` API-Endpunkt. Lesen Sie [Verwenden des Destination SDK zum Konfigurieren Ihres Ziels](../guides/configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
