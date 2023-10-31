---
description: Auf dieser Seite wird der API-Aufruf zum Löschen einer vorhandenen Zielgruppenvorlage über Adobe Experience Platform Destination SDK veranschaulicht.
title: Löschen einer Zielgruppenvorlage
exl-id: 6eb07e3c-3269-4368-9b11-04bd993cc4ab
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 100%

---

# Löschen einer Zielgruppenvorlage

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/audience-templates`

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie zum Löschen einer Zielgruppenvorlage mithilfe des API-Endpunkts`/authoring/audience-templates` verwenden können.

Eine ausführliche Beschreibung der Funktionen, die Sie über diesen Endpunkt konfigurieren können, finden Sie unter [Verwaltung von Zielgruppen-Metadaten](../functionality/audience-metadata-management.md).

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit API-Vorgängen für Zielgruppenvorlagen {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Löschen einer Zielgruppenvorlage {#delete}

Sie können eine [vorhandene](create-audience-template.md) Zielgruppenvorlage löschen, indem Sie eine `DELETE`-Anfrage an den Endpunkt `/authoring/audience-templates` mit der `{INSTANCE_ID}` der Zielgruppenvorlage stellen, die Sie löschen möchten.

Wie Sie eine vorhandene Zielgruppenvorlage und die zugehörige `{INSTANCE_ID}` abrufen, erfahren Sie im Artikel zum [Abrufen einer Zielgruppenvorlage](retrieve-audience-template.md).

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

Bei einer erfolgreichen Antwort wird der HTTP-Status 200 zusammen mit einer leeren HTTP-Antwort zurückgegeben.

+++

## Umgang mit API-Fehlern {#error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie eine Nachrichtenumwandlungsvorlage mit dem `/authoring/audience-templates` API-Endpunkt löschen. Lesen Sie [Verwenden des Destination SDK zum Konfigurieren Ihres Ziels](../guides/configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
