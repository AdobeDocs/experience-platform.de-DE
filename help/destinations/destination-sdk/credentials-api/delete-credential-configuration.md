---
description: Auf dieser Seite wird der API-Aufruf zum Löschen einer Anmeldedaten-Konfiguration mit dem Adobe Experience Platform Destination SDK veranschaulicht.
title: Löschen einer Anmeldedaten-Konfiguration
exl-id: a540e349-043c-4f04-8ca8-f650b9943492
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 96%

---

# Löschen einer Anmeldedaten-Konfiguration

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie zum Löschen einer Anmeldedaten-Konfiguration mithilfe des API-Endpunkts `/authoring/credentials` verwenden können.

## Verwendung des API-Endpunkts `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>In den meisten Fällen ist es ***nicht*** erforderlich, den API-Endpunkt `/credentials` zu verwenden. Stattdessen können Sie die Authentifizierungsinformationen für Ihr Ziel über den Parameter `customerAuthenticationConfigurations` des Endpunkts `/destinations` konfigurieren.
> 
>Lesen Sie [Konfiguration der Kundenauthentifizierung](../functionality/destination-configuration/customer-authentication.md) für detaillierte Informationen zu den unterstützten Authentifizierungstypen.

Verwenden Sie diesen API-Endpunkt nur dann zum Erstellen einer Berechtigungskonfiguration, wenn ein globales Authentifizierungssystem zwischen Adobe und Ihrer Zielplattform besteht und die [!DNL Experience Platform]-Kundinnen und -Kunden keine Authentifizierungs-Anmeldedaten bereitstellen müssen, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie mithilfe des API-Endpunkts `/credentials` eine Anmeldedaten-Konfiguration erstellen.

Bei der Verwendung eines globalen Authentifizierungssystems müssen Sie `"authenticationRule":"PLATFORM_AUTHENTICATION"` in der Konfiguration des [Zielversands](../functionality/destination-configuration/destination-delivery.md) festlegen, wenn Sie [eine neue Zielkonfiguration erstellen](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit Anmeldedaten-API-Vorgängen {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Löschen einer Anmeldedaten-Konfiguration {#delete}

Sie können eine [vorhandene](create-credential-configuration.md) Anmeldedaten-Konfiguration löschen, indem Sie eine `DELETE`-Anfrage an den Endpunkt `/authoring/credentials` mit der `{INSTANCE_ID}` der Anmeldedaten-Konfiguration stellen, die Sie löschen möchten.

Wie Sie eine vorhandene Zielkonfiguration und die zugehörige `{INSTANCE_ID}` abrufen, erfahren Sie im Artikel über das [Abrufen einer Anmeldedaten-Konfiguration](retrieve-credential-configuration.md).

**API-Format**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{INSTANCE_ID}` | Die `ID` der Anmeldedaten-Konfiguration, die Sie löschen möchten. |

Die folgende Anfrage löscht eine Anmeldedaten-Konfiguration, die durch den Parameter `{INSTANCE_ID}` bestimmt wird.

+++Anfrage

```shell
curl -X DELETE https://platform.adobe.io/data/core/activation/authoring/credentials/{INSTANCE_ID} \
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

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status](../../../landing/troubleshooting.md#api-status-codes)Codes und [Fehler in der Anfragekopfzeile](../../../landing/troubleshooting.md#request-header-errors) im Handbuch zur Fehlerbehebung bei Experience Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie eine Anmeldedaten-Konfiguration mithilfe des API-Endpunkts `/authoring/credentials` löschen. Lesen Sie [Verwenden des Destination SDK zum Konfigurieren Ihres Ziels](../guides/configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
