---
description: Auf dieser Seite wird der API-Aufruf zum Löschen einer Adobe Experience Platform Destination SDK zur Konfiguration von Anmeldedaten veranschaulicht.
title: Berechtigungskonfiguration löschen
source-git-commit: 9e1ae44f83b886f0b5dd5a9fc9cd9b7db6154ff0
workflow-type: tm+mt
source-wordcount: '395'
ht-degree: 36%

---


# Berechtigungskonfiguration löschen

>[!IMPORTANT]
>
>**API-Endpunkt**: `platform.adobe.io/data/core/activation/authoring/credentials`

Auf dieser Seite werden die API-Anfrage und die Payload erläutert, die Sie zum Löschen einer Berechtigungskonfiguration mit der `/authoring/credentials` API-Endpunkt.

## Verwendung des API-Endpunkts `/credentials` {#when-to-use}

>[!IMPORTANT]
>
>In den meisten Fällen ist es ***nicht*** erforderlich, den API-Endpunkt `/credentials` zu verwenden. Stattdessen können Sie die Authentifizierungsinformationen für Ihr Ziel über den `customerAuthenticationConfigurations`-Parameter des `/destinations`-Endpunkts konfigurieren.
> 
>Lesen [Konfiguration der Kundenauthentifizierung](../functionality/destination-configuration/customer-authentication.md) für detaillierte Informationen zu den unterstützten Authentifizierungstypen.

Verwenden Sie diesen API-Endpunkt, um eine Berechtigungskonfiguration nur dann zu erstellen, wenn ein globales Authentifizierungssystem zwischen Adobe und Ihrer Zielplattform vorhanden ist und die [!DNL Platform] Der Kunde muss keine Authentifizierungsberechtigungen bereitstellen, um eine Verbindung zu Ihrem Ziel herzustellen. In diesem Fall müssen Sie mithilfe der `/credentials` API-Endpunkt.

Bei der Verwendung eines globalen Authentifizierungssystems müssen Sie `"authenticationRule":"PLATFORM_AUTHENTICATION"` im [Zielversand](../functionality/destination-configuration/destination-delivery.md) Konfiguration, wenn [Erstellen einer neuen Zielkonfiguration](../authoring-api/destination-configuration/create-destination-configuration.md).

>[!IMPORTANT]
>
>Alle von Destination SDK unterstützten Parameternamen und Werte sind **Groß-/Kleinschreibung**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Erste Schritte mit API-Vorgängen für Anmeldedaten {#get-started}

Bevor Sie fortfahren, lesen Sie [Erste Schritte](../getting-started.md). Dort finden Sie die nötigen Informationen für den erfolgreichen Aufruf der API, einschließlich Details für den Abruf der erforderlichen Authoring-Berechtigung für Ziele und zu den erforderlichen Kopfzeilen.

## Berechtigungskonfiguration löschen {#delete}

Sie können eine [vorhandene](create-credential-configuration.md) Berechtigungskonfiguration durch `DELETE` Anfrage an `/authoring/credentials` Endpunkt mit der `{INSTANCE_ID}`der Konfiguration der Berechtigung, die Sie löschen möchten.

So rufen Sie eine vorhandene Zielkonfiguration und die zugehörigen `{INSTANCE_ID}`, siehe Artikel zu [Abrufen einer Berechtigungskonfiguration](retrieve-credential-configuration.md).

**API-Format**

```http
DELETE /authoring/credentials/{INSTANCE_ID}
```

| Parameter | Beschreibung |
| --------- | ----------- |
| `{INSTANCE_ID}` | Die `ID` der Konfiguration der Berechtigung, die Sie löschen möchten. |

Die folgende Anfrage löscht eine durch die `{INSTANCE_ID}` Parameter.

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

Eine erfolgreiche Antwort gibt den HTTP-Status 200 zusammen mit einer leeren HTTP-Antwort zurück.

+++

## Umgang mit API-Fehlern {#error-handling}

Destination SDK-API-Endpunkte folgen den allgemeinen Grundsätzen von Experience Platform API-Fehlermeldungen. Siehe [API-Status-Codes](../../../landing/troubleshooting.md#api-status-codes) und [Fehler im Anfrage-Header](../../../landing/troubleshooting.md#request-header-errors) in der Anleitung zur Fehlerbehebung für Platform.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Dokuments wissen Sie jetzt, wie Sie eine Berechtigungskonfiguration mit der `/authoring/credentials` API-Endpunkt. Lesen Sie [Verwenden des Destination SDK zum Konfigurieren Ihres Ziels](../guides/configure-destination-instructions.md), um zu verstehen, wo dieser Schritt in den Prozess der Konfiguration Ihres Ziels passt.
