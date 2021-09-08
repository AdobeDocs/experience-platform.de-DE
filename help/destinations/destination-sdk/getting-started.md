---
description: Auf dieser Seite wird beschrieben, wie Sie sich authentifizieren und mit der Verwendung des Adobe Experience Platform Destination SDK beginnen. Es enthält Anweisungen zum Abrufen der Anmeldeinformationen für die Adobe I/O-Authentifizierung, eines Sandbox-Namens und der Zugriffssteuerungsberechtigung für die Zielerstellung.
title: Erste Schritte mit Destination SDK
source-git-commit: 19307fba8f722babe5b6d57e80735ffde00fc851
workflow-type: tm+mt
source-wordcount: '525'
ht-degree: 7%

---

# Erste Schritte

## Übersicht {#overview}

Auf dieser Seite wird beschrieben, wie Sie sich authentifizieren und mit der Verwendung des Adobe Experience Platform Destination SDK beginnen. Es enthält Anweisungen zum Abrufen der Anmeldeinformationen für die Adobe I/O-Authentifizierung, eines Sandbox-Namens und der Zugriffssteuerungsberechtigung für die Zielerstellung.

## Terminologie {#terminology}

In diesem Handbuch werden plattformspezifische Konzepte wie IMS-Organisation und Sandboxes verwendet. Im [Experience Platform-Glossar](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html) finden Sie Definitionen zu diesen und anderen Begriffen.

## Erforderliche Authentifizierungsberechtigungen abrufen {#obtain-authentication-credentials}

Das Ziel-SDK verwendet das Gateway [Adobe I/O](https://www.adobe.io/) für die Authentifizierung. Um API-Aufrufe an Ziel-SDK-Endpunkte durchzuführen, müssen Sie bestimmte Kopfzeilen in Ihren API-Aufrufen bereitstellen. Arbeiten Sie mit dem Adobe Exchange-Team zusammen, um die Authentifizierung für Sie in der [Adobe Developer Console](http://console.adobe.io/) einzurichten.

Um erfolgreich Aufrufe an Ziel-SDK-API-Endpunkte durchzuführen, folgen Sie dem [Tutorial zur Experience Platform-Authentifizierung](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de). Starten Sie das Tutorial im Schritt &quot;[API-Schlüssel, IMS-Organisations-ID und Client-Geheimnis](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html#api-ims-secret) generieren&quot;. Das Adobe Exchange-Team übernimmt die vorherigen Schritte für Sie. Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in Ziel-SDK-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `x-api-key: {API_KEY}`, auch als Client-ID bezeichnet
* `x-gw-ims-org-id: {IMS_ORG}`, auch als Organisations-ID bezeichnet
* `Authorization: Bearer {ACCESS_TOKEN}`. Das Zugriffstoken hat eine Ablaufzeit von 24 Stunden, ausgedrückt in Millisekunden, sodass Sie es aktualisieren müssen. Um das Zugriffstoken zu aktualisieren, wiederholen Sie die Schritte, die im Authentifizierungs-Tutorial beschrieben werden.

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {IMS_ORG}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## Zieleigentum und Sandboxes {#destination-ownership}

Alle Ressourcen in Experience Platform sind auf bestimmte virtuelle Sandboxes beschränkt. Für Anforderungen an das Ziel-SDK sind Kopfzeilen erforderlich, die den Namen der Sandbox angeben, in der der Vorgang ausgeführt wird:

* `x-sandbox-name: {SANDBOX_NAME}`

Das Adobe Exchange-Team stellt Ihnen Ihren Sandbox-Namen zur Verfügung, den Sie bei Aufrufen an die Ziel-SDK-API-Endpunkte verwenden müssen.

## Rollenbasierte Zugriffssteuerung (RBAC) {#rbac}

Um die in der [Referenzdokumentation](./configuration-options.md) beschriebenen Ziel-SDK-API-Endpunkte zu verwenden, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Destination Authoring]**. Wenden Sie sich an das Adobe Exchange-Team, um diese Berechtigung Ihnen in [Adobe Admin Console](https://adminconsole.adobe.com/) zuweisen zu können.

![Berechtigung zur Zielbearbeitung](./assets/destination-authoring-permission.png)

Weitere Informationen finden Sie in den folgenden Dokumenten zur Zugriffskontrolle der Experience Platform:

* [Berechtigungen für ein Produktprofil verwalten](/help/access-control/ui/permissions.md)
* [Verfügbare Berechtigungen für die Experience Platform](/help/access-control/home.md#permissions)
* [Adobe Admin Console-Dokumentation](https://helpx.adobe.com/de/enterprise/using/admin-console.html)

## Weitere Überlegungen {#additional-considerations}

* Alle Änderungen, die Sie an Zielkonfigurationen vornehmen, unabhängig davon, ob Sie eine Zielkonfiguration erstellen oder bearbeiten, müssen von Adobe überprüft und genehmigt werden. Ihre Änderungen werden erst nach Abschluss der Überprüfung in Ihren Zielen angezeigt.
* Nur Benutzer, die derselben Organisation angehören und Zugriff auf die Sandbox haben, können die Zielkonfiguration bearbeiten.

## Nächste Schritte {#next-steps}

Indem Sie die Schritte in diesem Artikel ausgeführt haben, haben Sie Authentifizierungsberechtigungen für Adobe I/O, einen Sandbox-Namen und die Zugriffssteuerungsberechtigung für die Zielerstellung erhalten. Als Nächstes können Sie ein Ziel mithilfe des Destination SDK einrichten. Lesen Sie [Verwenden Sie das Ziel-SDK, um Ihr Ziel](./configure-destination-instructions.md) für die nächsten Schritte zu konfigurieren.
