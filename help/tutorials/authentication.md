---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Experience Platform-APIs authentifizieren und aufrufen
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '850'
ht-degree: 42%

---


# Authentifizierung und Zugriff auf [!DNL Experience Platform] APIs

This document provides a step-by-step tutorial for gaining access to an Adobe Experience Platform developer account in order to make calls to [!DNL Experience Platform] APIs.

## Authentifizieren, um API-Aufrufe tätigen zu können

Um die Sicherheit Ihrer Anwendungen und Benutzer zu gewährleisten, müssen alle Anfragen an Adobe I/O-APIs mit Standards wie OAuth und JSON Web Tokens (JWT) authentifiziert und autorisiert werden. Die JWT wird dann zusammen mit kundenspezifischen Informationen verwendet, um Ihr persönliches Zugriffstoken zu generieren.

In dieser Anleitung werden die Authentifizierungsschritte durch Erstellung eines Zugriffstokens beschrieben, wie im folgenden Flussdiagramm dargestellt:
![](images/authentication/authentication-flowchart.png)

## Voraussetzungen

In order to successfully make calls to [!DNL Experience Platform] APIs, you require the following:

* Eine IMS-Organisation mit Zugriff auf Adobe Experience Platform
* Ein registriertes Adobe ID-Konto
* Einen Admin Console-Administrator, der Sie als **Entwickler** und **Benutzer** für ein Produkt hinzufügt.

In den folgenden Abschnitten werden die Schritte zum Erstellen einer Adobe ID sowie zum Einrichten eines Entwicklers und Benutzers für eine Organisation erläutert.

### Adobe ID erstellen

Wenn Sie keine Adobe ID haben, können Sie wie folgt eine erstellen:

1. Zur [Adobe Developer Console wechseln](https://console.adobe.io)
2. Klicken Sie auf **[!UICONTROL Neues Konto erstellen]**.
3. Schließen Sie den Anmeldevorgang ab.

## Become a developer and user for [!DNL Experience Platform] for an organization

Vor der Erstellung von Integrationen in Adobe I/O muss Ihr Konto über Entwicklerberechtigungen für ein Produkt in einer IMS-Organisation verfügen. Ausführliche Informationen zu Entwicklerkonten in der Admin Console finden Sie im [Support-Dokument](https://helpx.adobe.com/de/enterprise/using/manage-developers.html) für das Verwalten von Entwicklern.

**Entwicklerzugriff erlangen**

Contact an [!DNL Admin Console] administrator in your Organization to add you as a developer for one of your Organization&#39;s products using the [!DNL Admin Console](https://adminconsole.adobe.com/).

![](images/authentication/assign-developer.png)

Der Administrator muss Sie als Entwickler mindestens einem Produktprofil zuweisen, damit Sie fortfahren können.

![](images/authentication/add-developer.png)

Nachdem Sie als Entwickler zugewiesen sind, verfügen Sie über Zugriffsberechtigungen und können Integrationen in [Adobe I/O](https://www.adobe.com/go/devs_console_ui) erstellen. Bei diesen Integrationen handelt es sich um eine Pipeline von externen Apps und Diensten zur Adobe-API.

**Benutzerzugriff erlangen**

Your [!DNL Admin Console] administrator must also add you to the product as a user.

![](images/authentication/assign-users.png)

Ähnlich wie beim Hinzufügen eines Entwicklers muss der Administrator Sie mindestens einem Profil zuweisen, damit Sie fortfahren können.

![](images/authentication/assign-user-details.png)

## Erstellen von Zugriffsberechtigungen in der Adobe Developer Console

>[!NOTE]
>
>Wenn Sie diesem Dokument aus dem [Privacy Service-Entwicklerhandbuch](../privacy-service/api/getting-started.md)folgen, können Sie jetzt zu diesem Handbuch zurückkehren, um die Zugriffsberechtigungen zu generieren, für die Sie [!DNL Privacy Service]eindeutig sind.

Mit Adobe Developer Console müssen Sie die folgenden drei Zugriffsberechtigungen generieren:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Ihre `{IMS_ORG}` und `{API_KEY}` nur einmal generiert werden müssen und können in zukünftigen [!DNL Platform] API-Aufrufen wiederverwendet werden. Ihre `{ACCESS_TOKEN}` Daten sind jedoch nur vorübergehend und müssen alle 24 Stunden neu generiert werden.

Die Schritte werden nachfolgend detailliert beschrieben.

### Einmalige Einrichtung

Go to [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) and sign in with your Adobe ID. Führen Sie anschließend die Schritte aus, die im Lernprogramm zum [Erstellen eines leeren Projekts](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in der Dokumentation zur Adobe Developer Console beschrieben sind.

Nachdem Sie ein neues Projekt erstellt haben, klicken Sie im Bildschirm &quot; **[!UICONTROL Projektübersicht]** &quot;auf _Hinzufügen API_ .

![](images/authentication/add-api-button.png)

Der _Hinzufügen eines API_ -Bildschirms wird angezeigt. Klicken Sie auf das Produktsymbol für die Adobe Experience Platform und wählen Sie dann die **[!UICONTROL Experience Platformen-API]** , bevor Sie auf **[!UICONTROL Weiter]** klicken.

![](images/authentication/add-platform-api.png)

Nachdem Sie [!DNL Experience Platform] als API ausgewählt haben, die dem Projekt hinzugefügt werden soll, führen Sie die Schritte aus, die im Lernprogramm zum [Hinzufügen einer API zu einem Projekt mithilfe eines Dienstkontos (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (beginnend mit dem Schritt &quot;API konfigurieren&quot;) beschrieben sind, um den Prozess abzuschließen.

Nachdem die API zum Projekt hinzugefügt wurde, zeigt die Seite &quot; _Projektübersicht_ &quot;die folgenden Anmeldeinformationen an, die für alle Aufrufe von [!DNL Experience Platform] APIs erforderlich sind:

* `{API_KEY}` (Client-ID)
* `{IMS_ORG}` (Organisations-ID)

![](./images/authentication/api-key-ims-org.png)

### Authentifizierung für jede Sitzung

Die letzte erforderliche Berechtigung, die Sie erfassen müssen, ist Ihre `{ACCESS_TOKEN}`. Im Gegensatz zu den Werten für `{API_KEY}` und `{IMS_ORG}`muss alle 24 Stunden ein neues Token generiert werden, um weiterhin mit [!DNL Platform] APIs arbeiten zu können.

Um ein neues zu erstellen, führen Sie die Schritte `{ACCESS_TOKEN}`zum [Generieren eines JWT-Tokens](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/credentials.md) im Handbuch mit den Anmeldeinformationen für die Developer Console aus.

## Zugriffsberechtigungen testen

Nachdem Sie alle drei erforderlichen Anmeldeinformationen gesammelt haben, können Sie versuchen, den folgenden API-Aufruf durchzuführen. Dieser Aufruf Liste alle [!DNL Experience Data Model] (XDM-) Klassen im `global` Container der Schema-Registrierung:

**API-Format**

```http
GET /global/classes
```

**Anfrage**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwort**

Wenn Ihre Antwort der unten stehenden ähnelt, sind Ihre Anmeldeinformationen gültig und funktionieren. (Diese Antwort wurde aus Platzgründen abgeschnitten.)

```JSON
{
  "results": [
    {
        "title": "XDM ExperienceEvent",
        "$id": "https://ns.adobe.com/xdm/context/experienceevent",
        "meta:altId": "_xdm.context.experienceevent",
        "version": "1"
    },
    {
        "title": "XDM Individual Profile",
        "$id": "https://ns.adobe.com/xdm/context/profile",
        "meta:altId": "_xdm.context.profile",
        "version": "1"
    }
  ]
}
```

## Postman für JWT-Authentifizierung und API-Aufrufe verwenden

[Postman](https://www.getpostman.com/) ist ein beliebtes Tool zum Arbeiten mit RESTful-APIs. In diesem [Beitrag](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) wird beschrieben, wie Sie Postman so einrichten, dass automatisch eine JWT-Authentifizierung vorgenommen und für die Nutzung von Adobe Experience Platform-APIs verwendet wird.

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie Ihre Zugriffsberechtigungen für [!DNL Platform] APIs gesammelt und erfolgreich getestet. Sie können nun die in der gesamten [Dokumentation](../landing/documentation/overview.md)bereitgestellten Beispiel-API-Aufrufe verwenden.

Zusätzlich zu den Authentifizierungswerten, die Sie in diesem Tutorial gesammelt haben, benötigen viele [!DNL Platform] APIs auch eine gültige Kopfzeile, `{SANDBOX_NAME}` die als Kopfzeile bereitgestellt werden muss. Weiterführende Informationen dazu finden Sie unter [Sandbox-Übersicht](../sandboxes/home.md).