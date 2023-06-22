---
description: Auf dieser Seite wird der API-Aufruf zum Löschen einer Berechtigungskonfiguration mit dem Adobe Experience Platform Destination SDK veranschaulicht.
title: Löschen einer Berechtigungskonfiguration
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: ht
source-wordcount: '395'
ht-degree: 100%

---


# Löschen einer Berechtigungskonfiguration

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie zum Löschen einer Berechtigungskonfiguration mithilfe des API-Endpunkts `/authoring/credentials` verwenden können.

## Verwendung des API-Endpunkts `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>In den meisten Fällen ist es ***nicht*** erforderlich, den API-Endpunkt `/credentials` zu verwenden. Stattdessen können Sie die Authentifizierungsinformationen für Ihr Ziel über den Parameter `customerAuthenticationConfigurations` des Endpunkts `/destinations` konfigurieren.
> 
>Lesen Sie [Konfiguration der Kundenauthentifizierung](../functionality/destination-configuration/customer-authentication.md) für detaillierte Informationen zu den unterstützten Authentifizierungstypen.

Verwenden Sie diesen API-Endpunkt nur dann zum Erstellen einer Berechtigungskonfiguration, wenn ein globales Authentifizierungssystem zwischen Adobe und Ihrer Zielplattform besteht und die [!DNL Platform]-Kundinnen und -Kunden keine Authentifizierungsdaten bereitstellen müssen, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie mithilfe des API-Endpunkts `/credentials` eine Berechtigungskonfiguration erstellen.

Bei der Verwendung eines globalen Authentifizierungssystems müssen Sie `"authenticationRule":"PLATFORM_AUTHENTICATION"` in der Konfiguration des [Zielversands](../functionality/destination-configuration/destination-delivery.md) festlegen, wenn Sie [eine neue Zielkonfiguration erstellen](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit Berechtigungs-API-Vorgängen {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Löschen einer Berechtigungskonfiguration {#delete}

Sie können eine [vorhandene](create-credential-configuration.md) Berechtigungskonfiguration löschen, indem Sie eine `DELETE`-Anfrage an den Endpunkt `/authoring/credentials` mit der `{INSTANCE_ID}` der Berechtigungskonfiguration stellen, die Sie löschen möchten.

Wie Sie eine vorhandene Zielkonfiguration und die zugehörige `{INSTANCE_ID}` abrufen, erfahren Sie im Artikel über das [Abrufen einer Berechtigungskonfiguration](retrieve-credential-configuration.md).

**API-Format**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{INSTANCE_ID}` | Die `ID` der Berechtigungskonfiguration, die Sie löschen möchten. |

Die folgende Anfrage löscht eine Berechtigungskonfiguration, die durch den Parameter `{INSTANCE_ID}` bestimmt wird.

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

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie eine Berechtigungskonfiguration mithilfe des API-Endpunkts `/authoring/credentials` löschen. Lesen Sie [Verwenden des Destination SDK zum Konfigurieren Ihres Ziels](../guides/configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
