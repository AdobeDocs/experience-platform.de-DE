---
title: Authentifizierung
description: Erfahren Sie, wie Sie die Authentifizierung für die Adobe Experience Platform Edge Network Server-API konfigurieren.
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: 3bf13c3f5ac0506ac88effc56ff68758deb5f566
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 24%

---

# Authentifizierung {#authentication}

## Übersicht

Der [!DNL Edge Network Server API] verarbeitet sowohl authentifizierte als auch nicht authentifizierte Datenerfassung, je nach Ereignisquelle und API-Erfassungsdomäne.

Für jede Anfrage überprüft der [!DNL Server API] die Einstellung &quot;datastream [!DNL access type]&quot;. Mit dieser Einstellung können Kunden einen Datastream so konfigurieren, dass entweder authentifizierte Daten oder sowohl authentifizierte als auch nicht authentifizierte Daten akzeptiert werden. Standardmäßig werden beide Datentypen akzeptiert.

Weitere Informationen zum Konfigurieren des Zugriffstyps auf den Datastream finden Sie in der Dokumentation zum Erstellen und Konfigurieren eines Datastreams ](../datastreams/overview.md#create).[

Nachstehend finden Sie eine Zusammenfassung des Verhaltens, die auf der Konfiguration des Datastreams [!DNL Access Type] und dem Endpunkt basiert, an den die Anfrage gesendet wird.

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| mix (Standard) | Authentifiziert keine Anforderung | Authentifizierungsanfrage |
| authentifiziert | Authentifizierungsanfrage | Authentifizierungsanfrage |

API-Aufrufe von einem privaten Server mit `server.adobedc.net` sollten immer authentifiziert werden.

## Voraussetzungen {#prerequisites}

Bevor Sie Aufrufe an [!DNL Server API] vornehmen können, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

* Sie haben ein Organisationskonto mit Zugriff auf Adobe Experience Platform.
* Für Ihr Experience Platform-Konto sind die Rollen `developer` und `user` für das Adobe Experience Platform API-Produktprofil aktiviert. Wenden Sie sich an Ihren Administrator von [Admin Console](../access-control/home.md) , um diese Rollen für Ihr Konto zu aktivieren.
* Du hast einen Adobe ID. Wenn Sie keine Adobe ID haben, wechseln Sie zum Ordner [Adobe Developer Console](https://developer.adobe.com/console) und erstellen Sie ein neues Konto.

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

Um die Schreibberechtigungen für Datensätze zu konfigurieren, wechseln Sie zur Admin Console [1}, suchen Sie das Produktprofil, das an Ihren API-Schlüssel angehängt ist, und legen Sie die folgenden Berechtigungen fest:](https://adminconsole.adobe.com)

* Wählen Sie im Abschnitt [!UICONTROL Sandboxes] die Sandbox des Datenspeichers aus.
* Wählen Sie im Abschnitt [!UICONTROL Datenverwaltung] die Berechtigung **[!UICONTROL Datensätze verwalten]** aus.

## Fehlerbehebung bei Autorisierungsfehlern {#troubleshooting-authorization}

| Fehler-Code | Fehlermeldung | Beschreibung |
| --- | --- | --- |
| `EXEG-0500-401` | Ungültiges Autorisierungs-Token | Diese Fehlermeldung wird in den folgenden Situationen angezeigt:  <ul><li>Der Header-Wert `authorization` fehlt.</li><li>Der Header-Wert `authorization` enthält nicht das erforderliche `Bearer` -Token.</li><li>Das angegebene Autorisierungs-Token hat ein ungültiges Format.</li><li>Der Datastream erfordert Authentifizierung, aber die Anfrage fehlt an den erforderlichen Kopfzeilen.</li></ul> |
| `EXEG-0501-401` | Ungültiger Benutzerautorisierungs-Token | Diese Fehlermeldung wird in den folgenden Situationen angezeigt: <ul><li>Dem API-Aufruf fehlt der erforderliche `x-user-token` -Header.</li><li>Das angegebene Benutzer-Token hat ein ungültiges Format.</li></ul> |
| `EXEG-0502-401` | Ungültiges Autorisierungs-Token | Diese Fehlermeldung wird angezeigt, wenn das bereitgestellte Autorisierungstoken ein gültiges Format (JWT) aufweist, die Signatur jedoch ungültig ist. Im Tutorial [Authentifizierung ](../landing/api-authentication.md) erfahren Sie, wie Sie ein gültiges JWT-Token abrufen. |
| `EXEG-0503-401` | Ungültiges Autorisierungs-Token | Diese Fehlermeldung wird angezeigt, wenn das angegebene Autorisierungstoken abgelaufen ist. Führen Sie das [Authentifizierungs-Tutorial](../landing/api-authentication.md) durch, um ein neues Token zu generieren. |
| `EXEG-0504-401` | Erforderlicher Produktkontext fehlt | Diese Fehlermeldung wird in den folgenden Situationen angezeigt:  <ul><li>Das Entwicklerkonto hat keinen Zugriff auf den Adobe Experience Platform-Produktkontext.</li><li>Das Unternehmenskonto hat noch keinen Anspruch auf Adobe Experience Platform.</li></ul> |
| `EXEG-0505-401` | Erforderlicher Gültigkeitsbereich für Autorisierungs-Token fehlt | Dieser Fehler gilt nur für die Authentifizierung von Dienstkonten. Die Fehlermeldung wird angezeigt, wenn das im Aufruf enthaltene Dienstautorisierungstoken zu einem Dienstkonto gehört, das keinen Zugriff auf den IMS-Bereich `acp.foundation` hat. |
| `EXEG-0506-401` | Sandbox nicht zum Schreiben verfügbar | Diese Fehlermeldung wird angezeigt, wenn das Entwicklerkonto keinen `WRITE` -Zugriff auf die Experience Platform-Sandbox hat, in der der Datastream definiert ist. |
