---
title: Authentifizierung
description: Erfahren Sie, wie Sie die Authentifizierung für die Adobe Experience Platform Edge Network Server-API konfigurieren.
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 20%

---

# Authentifizierung {#authentication}

## Übersicht

Die [!DNL Edge Network Server API] verarbeitet sowohl authentifizierte als auch nicht authentifizierte Datenerfassung, je nach Ereignisquelle und API-Erfassungsdomäne.

Für jede Anfrage wird die Variable [!DNL Server API] überprüft den Datastream [!DNL access type] -Einstellung. Mit dieser Einstellung können Kunden einen Datastream so konfigurieren, dass entweder authentifizierte Daten oder sowohl authentifizierte als auch nicht authentifizierte Daten akzeptiert werden. Standardmäßig werden beide Datentypen akzeptiert.

Weitere Informationen zum Konfigurieren des Zugriffstyps auf den Datastream finden Sie in der Dokumentation zum [Erstellen und Konfigurieren eines Datenspeichers](../datastreams/overview.md#create).

Nachstehend finden Sie eine Zusammenfassung des Verhaltens, basierend auf dem Datastream [!DNL Access Type] Konfiguration und dem Endpunkt, an den die Anfrage empfangen wird.

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| mix (Standard) | Authentifiziert keine Anforderung | Authentifizierungsanfrage |
| Authentifiziert | Authentifizierungsanfrage | Authentifizierungsanfrage |

API-Aufrufe von einem privaten Server auf `server.adobedc.net` sollte immer authentifiziert werden.

## Voraussetzungen {#prerequisites}

Bevor Sie Aufrufe an die [!DNL Server API]müssen Sie die folgenden Voraussetzungen erfüllen:

* Sie haben ein Organisationskonto mit Zugriff auf Adobe Experience Platform.
* Ihr Experience Platform-Konto verfügt über die `developer` und `user` Rollen, die für das Adobe Experience Platform API-Produktprofil aktiviert sind. Wenden Sie sich an [Admin Console](../access-control/home.md) Administrator, um diese Rollen für Ihr Konto zu aktivieren.
* Du hast einen Adobe ID. Wenn Sie keine Adobe ID haben, navigieren Sie zum [Adobe Developer-Konsole](https://developer.adobe.com/console) und erstellen Sie ein neues Konto.

## Sammeln von Anmeldeinformationen {#credentials}

Um Platform-APIs aufrufen zu können, müssen Sie zunächst das [Authentifizierungs-Tutorial](../landing/api-authentication.md) abschließen. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Experience Platform-API-Aufrufen bereitgestellt, wie unten dargestellt:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Ressourcen in Experience Platform lassen sich in spezifischen virtuellen Sandboxes isolieren. Bei Anfragen an Platform-APIs können Sie den Namen und die Kennung der Sandbox angeben, in der der Vorgang ausgeführt werden soll. Dies sind optionale Parameter.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Weitere Informationen zu Sandboxes in Experience Platform finden Sie in der [Sandbox-Übersichtsdokumentation](../sandboxes/home.md).

Bei allen Anfragen, die eine Payload enthalten (POST, PUT, PATCH), ist eine zusätzliche Medientyp-Kopfzeile erforderlich:

* Content-Type: `application/json`

## Konfigurieren von Schreibberechtigungen für Datensätze {#dataset-write-permissions}

Um die Schreibberechtigungen für Datensätze zu konfigurieren, navigieren Sie zum [Admin Console](https://adminconsole.adobe.com), suchen Sie das Produktprofil, das an Ihren API-Schlüssel angehängt ist, und legen Sie die folgenden Berechtigungen fest:

* Im [!UICONTROL Sandboxes] auswählen, wählen Sie die Sandbox des Datenspeichers aus.
* Im [!UICONTROL Data Management] auswählen, wählen Sie die **[!UICONTROL Datensätze verwalten]** -Berechtigung.

## Fehlerbehebung bei Autorisierungsfehlern {#troubleshooting-authorization}

| Fehler-Code | Fehlermeldung | Beschreibung |
| --- | --- | --- |
| `EXEG-0500-401` | Ungültiges Autorisierungs-Token | Diese Fehlermeldung wird in den folgenden Situationen angezeigt:  <ul><li>Die `authorization` -Kopfzeilenwert fehlt.</li><li>Die `authorization` Der Kopfzeilenwert enthält nicht die erforderliche `Bearer` Token.</li><li>Das angegebene Autorisierungstoken hat ein ungültiges Format.</li><li>Der Datastream erfordert Authentifizierung, aber die Anfrage fehlt an den erforderlichen Kopfzeilen.</li></ul> |
| `EXEG-0501-401` | Ungültiges Benutzerautorisierungstoken | Diese Fehlermeldung wird in den folgenden Situationen angezeigt: <ul><li>Dem API-Aufruf fehlt die erforderliche `x-user-token` -Kopfzeile.</li><li>Das angegebene Benutzer-Token hat ein ungültiges Format.</li></ul> |
| `EXEG-0502-401` | Ungültiges Autorisierungs-Token | Diese Fehlermeldung wird angezeigt, wenn das bereitgestellte Autorisierungstoken ein gültiges Format (JWT) aufweist, die Signatur jedoch ungültig ist. Überprüfen Sie die [Authentifizierungs-Tutorial](../landing/api-authentication.md) , um zu erfahren, wie Sie ein gültiges JWT-Token erhalten. |
| `EXEG-0503-401` | Ungültiges Autorisierungs-Token | Diese Fehlermeldung wird angezeigt, wenn das angegebene Autorisierungstoken abgelaufen ist. Durchsuchen Sie die [Authentifizierungs-Tutorial](../landing/api-authentication.md) , um ein neues Token zu generieren. |
| `EXEG-0504-401` | Erforderlicher Produktkontext fehlt | Diese Fehlermeldung wird in den folgenden Situationen angezeigt:  <ul><li>Das Entwicklerkonto hat keinen Zugriff auf den Adobe Experience Platform-Produktkontext.</li><li>Das Unternehmenskonto hat noch keinen Anspruch auf Adobe Experience Platform.</li></ul> |
| `EXEG-0505-401` | Der erforderliche Umfang des Autorisierungstokens fehlt | Dieser Fehler gilt nur für die Authentifizierung von Dienstkonten. Die Fehlermeldung wird angezeigt, wenn das im Aufruf enthaltene Dienstautorisierungstoken zu einem Dienstkonto gehört, das keinen Zugriff auf die `acp.foundation` IMS-Umfang. |
| `EXEG-0506-401` | Sandbox kann nicht geschrieben werden | Diese Fehlermeldung wird angezeigt, wenn das Entwicklerkonto nicht über `WRITE` Zugriff auf die Experience Platform-Sandbox, in der der Datastream definiert ist. |
