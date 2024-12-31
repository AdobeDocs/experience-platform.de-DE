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

Die [!DNL Edge Network Server API] verarbeitet die Datenerfassung sowohl authentifizierter als auch nicht authentifizierter Daten, je nach Ereignisquelle und API-Erfassungsdomäne.

Für jede Anfrage überprüft der [!DNL Server API] die Einstellung für die Datenstrom-[!DNL access type] . Mit dieser Einstellung können Kundinnen und Kunden einen Datenstrom so konfigurieren, dass er entweder authentifizierte Daten oder sowohl authentifizierte als auch nicht authentifizierte Daten akzeptiert. Standardmäßig werden beide Datentypen akzeptiert.

Einzelheiten zum Konfigurieren des Zugriffstyps auf den Datenstrom finden Sie in der Dokumentation zum [Erstellen und Konfigurieren eines Datenstroms](../datastreams/overview.md#create).

Nachstehend finden Sie eine Zusammenfassung des Verhaltens, basierend auf der Konfiguration der Datenstrom-[!DNL Access Type] und dem Endpunkt, an dem die Anfrage empfangen wird.

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| Gemischt (Standard) | Anfrage wird nicht authentifiziert | Authentifiziert eine Anfrage |
| Authentifiziert | Authentifiziert eine Anfrage | Authentifiziert eine Anfrage |

API-Aufrufe von einem privaten Server auf `server.adobedc.net` sollten immer authentifiziert werden.

## Voraussetzungen {#prerequisites}

Bevor Sie die [!DNL Server API] aufrufen können, müssen Sie die folgenden Voraussetzungen erfüllen:

* Sie haben ein Organisationskonto mit Zugriff auf Adobe Experience Platform.
* Für Ihr Experience Platform-Konto sind die Rollen `developer` und `user` für das Adobe Experience Platform-API-Produktprofil aktiviert. Wenden Sie sich an Ihren [Admin Console](../access-control/home.md)-Administrator, um diese Rollen für Ihr Konto zu aktivieren.
* Sie haben eine Adobe ID. Wenn Sie keine Adobe ID haben, gehen Sie zur [Adobe Developer Console](https://developer.adobe.com/console) und erstellen Sie ein neues Konto.

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

Zum Konfigurieren der Schreibberechtigungen für Datensätze wechseln Sie zur Admin Console [](https://adminconsole.adobe.com) suchen Sie das Produktprofil, das an Ihren API-Schlüssel angehängt ist, und legen Sie die folgenden Berechtigungen fest:

* Wählen [!UICONTROL  im Abschnitt ] die Datenstrom-Sandbox aus.
* Wählen Sie [!UICONTROL  Abschnitt ] die Berechtigung **[!UICONTROL Datensätze verwalten]** aus.

## Fehlerbehebung bei Autorisierungsfehlern {#troubleshooting-authorization}

| Fehler-Code | Fehlermeldung | Beschreibung |
| --- | --- | --- |
| `EXEG-0500-401` | Ungültiges Autorisierungs-Token | Diese Fehlermeldung wird in einer der folgenden Situationen angezeigt:  <ul><li>Der `authorization` Kopfzeilenwert fehlt.</li><li>Der `authorization` Kopfzeilenwert enthält nicht das erforderliche `Bearer`-Token.</li><li>Das angegebene Autorisierungs-Token hat ein ungültiges Format.</li><li>Der Datenstrom erfordert eine Authentifizierung, aber der Anfrage fehlen erforderliche Kopfzeilen.</li></ul> |
| `EXEG-0501-401` | Ungültiger Benutzerautorisierungs-Token | Diese Fehlermeldung wird in einer der folgenden Situationen angezeigt: <ul><li>Im API-Aufruf fehlt die erforderliche `x-user-token`-Kopfzeile.</li><li>Das angegebene Benutzer-Token hat ein ungültiges Format.</li></ul> |
| `EXEG-0502-401` | Ungültiges Autorisierungs-Token | Diese Fehlermeldung wird angezeigt, wenn das angegebene Autorisierungs-Token ein gültiges Format (JWT) hat, seine Signatur jedoch ungültig ist. Sehen Sie sich das [Authentifizierungs-Tutorial](../landing/api-authentication.md) an, um zu erfahren, wie Sie ein gültiges JWT-Token abrufen. |
| `EXEG-0503-401` | Ungültiges Autorisierungs-Token | Diese Fehlermeldung wird angezeigt, wenn das angegebene Autorisierungs-Token abgelaufen ist. Gehen Sie das [Authentifizierungs-Tutorial](../landing/api-authentication.md) um ein neues Token zu generieren. |
| `EXEG-0504-401` | Erforderlicher Produktkontext fehlt | Diese Fehlermeldung wird in einer der folgenden Situationen angezeigt:  <ul><li>Das Entwicklerkonto hat keinen Zugriff auf den Adobe Experience Platform-Produktkontext.</li><li>Das Unternehmenskonto ist noch nicht zum Adobe von Experience Platform berechtigt.</li></ul> |
| `EXEG-0505-401` | Erforderlicher Gültigkeitsbereich für Autorisierungs-Token fehlt | Dieser Fehler gilt nur für die Authentifizierung des Service-Kontos. Die Fehlermeldung wird angezeigt, wenn das im Aufruf enthaltene Autorisierungs-Token für den Service zu einem Service-Konto gehört, das keinen Zugriff auf den `acp.foundation` IMS-Bereich hat. |
| `EXEG-0506-401` | Sandbox nicht zum Schreiben verfügbar | Diese Fehlermeldung wird angezeigt, wenn das Entwicklerkonto keinen `WRITE` auf die Experience Platform-Sandbox hat, in der der Datenstrom definiert ist. |
