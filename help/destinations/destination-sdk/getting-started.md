---
description: Auf dieser Seite wird beschrieben, wie Sie sich authentifizieren und Adobe Experience Platform Destination SDK verwenden. Sie enthält Anweisungen zum Abrufen der Anmeldeinformationen für die Adobe I/O-Authentifizierung, eines Sandbox-Namens und der Zugriffskontrolle für die Zielerstellung.
title: Erste Schritte mit dem Destination SDK
exl-id: f22c37a8-202d-49ac-9af0-545dfa9af8fd
source-git-commit: 557db5b7eefdd7902895e428f7bc34e3ad8a6f58
workflow-type: tm+mt
source-wordcount: '612'
ht-degree: 100%

---

# Erste Schritte

## Übersicht {#overview}

Auf dieser Seite wird beschrieben, wie Sie sich authentifizieren und Adobe Experience Platform Destination SDK verwenden. Sie enthält Anweisungen zum Abrufen der Anmeldeinformationen für die Adobe I/O-Authentifizierung, eines Sandbox-Namens und der Zugriffskontrolle für die Zielerstellung.

## Terminologie {#terminology}

In diesem Handbuch werden spezifische Konzepte für Platform wie IMS-Organisation und Sandboxes verwendet. Definitionen hierzu und zu anderen Begriffen finden Sie im [Experience Platform-Glossar](https://experienceleague.adobe.com/docs/experience-platform/landing/glossary.html?lang=de).

## Erforderliche Authentifizierungsdaten erhalten {#obtain-authentication-credentials}

Das Destination SDK verwendet das [Adobe I/O](https://www.adobe.io/)-Gateway zur Authentifizierung. Um API-Aufrufe an Destination SDK-Endpunkte durchzuführen, müssen Sie bestimmte Kopfzeilen in Ihren API-Aufrufen bereitstellen. Arbeiten Sie mit dem Adobe Exchange-Team zusammen, um die Authentifizierung für die [Adobe Developer Console](https://developer.adobe.com/console) einzurichten.

Um Destination SDK-API-Endpunkte erfolgreich aufzurufen, folgen Sie dem [Tutorial zur Experience Platform-Authentifizierung](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de). Starten Sie das Tutorial über den Schritt [API-Schlüssel, ID der IMS-Organisation und Client-Geheimnis generieren](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#api-ims-secret). Das Adobe Exchange-Team übernimmt die vorherigen Schritte für Sie. Im Rahmen des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in Destination SDK-API-Aufrufen bereitgestellt, wie unten dargestellt:

* `x-api-key: {API_KEY}`, auch als Client-ID bezeichnet
* `x-gw-ims-org-id: {ORG_ID}`, auch als Organisations-ID bezeichnet
* `Authorization: Bearer {ACCESS_TOKEN}`. Das Zugriffs-Token hat eine Ablaufzeit von 24 Stunden, ausgedrückt in Millisekunden, sodass Sie es aktualisieren müssen. Um das Zugriffs-Token zu aktualisieren, wiederholen Sie die Schritte, die im Authentifizierungs-Tutorial beschrieben werden.

<!--

### Obtain `Authorization: Bearer {ACCESS_TOKEN}`

To obtain the `{ACCESS_TOKEN}`, you must generate a JWT token and exchange it for the access token. Follow the steps below:

1. Follow the instructions in the [Generate JWT section](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) in the credentials guide.
2. Follow the instructions in [Step 3: try it](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/AuthenticationOverview/ServiceAccountIntegration.md) in the Service account connection guide.

You now have the required authentication headers `x-api-key: {API_KEY}`, `x-gw-ims-org-id: {ORG_ID}`, and `Authorization: Bearer {ACCESS_TOKEN}`.

>[!NOTE]
>
>The access token has an expiration time of 24 hours, expressed in milliseconds, so you will have to refresh it. To refresh the access token, repeat the steps outlined in this section.

-->

## Zielinhaber und Sandboxes {#destination-ownership}

Alle Ressourcen in Experience Platform sind auf bestimmte virtuelle Sandboxes beschränkt. Für Anfragen zum Destination SDK sind Kopfzeilen erforderlich, die den Namen der Sandbox angeben, in der der Vorgang ausgeführt wird:

* `x-sandbox-name: {SANDBOX_NAME}`

Das Adobe Exchange-Team stellt Ihnen Ihren Sandbox-Namen zur Verfügung, den Sie in Aufrufen der Destination SDK-API-Endpunkte verwenden müssen.

## Rollenbasierte Zugriffskontrolle (RBAC) {#rbac}

Um Destination SDK-API-Endpunkte, die im Abschnitt [Referenzdokumentation](./configuration-options.md) beschrieben werden, zu nutzen, benötigen Sie die Zugriffskontrollberechtigung für die **[!UICONTROL Zielerstellung]**. Arbeiten Sie mit dem Adobe Exchange-Team zusammen, um diese Berechtigung in der [Adobe Admin Console](https://adminconsole.adobe.com/) zugewiesen zu bekommen.

![Berechtigung zur Zielerstellung](./assets/destination-authoring-permission.png)

Weitere Informationen finden Sie in den folgenden Dokumenten zur Zugriffskontrolle in Experience Platform:

* [Verwalten von Berechtigungen für ein Produktprofil](/help/access-control/ui/permissions.md)
* [Verfügbare Berechtigungen für Experience Platform](/help/access-control/home.md#permissions)
* [Dokumentation für die Adobe Admin Console](https://helpx.adobe.com/de/enterprise/using/admin-console.html)

## Weitere Überlegungen {#additional-considerations}

* Alle Änderungen, die Sie an Zielkonfigurationen vornehmen, unabhängig davon, ob Sie eine Zielkonfiguration erstellen oder bearbeiten, müssen von Adobe überprüft und genehmigt werden. Ihre Änderungen werden erst nach Abschluss der Überprüfung in Ihren Zielen angezeigt.
* Nur Benutzer, die derselben Organisation angehören und Zugriff auf die Sandbox haben, können die Zielkonfiguration bearbeiten.

## Nächste Schritte {#next-steps}

Wenn Sie die Schritte in diesem Artikel befolgt haben, haben Sie Authentifizierungsdaten für Adobe I/O, einen Sandbox-Namen und die Zugriffskontrolle für die Zielerstellung erhalten. Als Nächstes können Sie mithilfe des Destination SDK ein Ziel einrichten.

* Lesen Sie je nach Zieltyp die folgenden Konfigurationshandbücher:

   * [Verwenden des Destination SDK zum Konfigurieren eines Streaming-Ziels](./configure-destination-instructions.md)
   * [Verwenden des Destination SDK zum Konfigurieren eines dateibasierten Ziels](./configure-file-based-destination-instructions.md)

* Informationen zu allen Vorgängen finden Sie im Abschnitt [Dokumentation zur Zielerstellungs-API](https://www.adobe.io/experience-platform-apis/references/destination-authoring/).
* Verwenden Sie die [Postman-Sammlung der Zielerstellungs-API](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/experience-platform/Destination%20Authoring%20API.postman_collection.json), um Ihr Ziel mithilfe der Destination SDK-API-Endpunkte zu konfigurieren. Informationen zu den ersten Schritten mit Postman finden Sie unter [Schritte zum Importieren von Umgebungen und Sammlungen](https://learning.postman.com/docs/getting-started/importing-and-exporting-data/) und im [Videoleitfaden zum Erstellen der Postman-Umgebung](https://video.tv.adobe.com/v/28832).
