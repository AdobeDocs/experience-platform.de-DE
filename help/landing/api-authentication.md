---
keywords: Experience Platform;Startseite;beliebte Themen;Authentifizierung;Zugriff
solution: Experience Platform
title: Experience Platform-APIs authentifizieren und aufrufen
topic-legacy: tutorial
type: Tutorial
description: Dieses Dokument bietet eine schrittweise Anleitung für den Zugriff auf ein Adobe Experience Platform-Entwicklerkonto, damit Sie Aufrufe an Experience Platform-APIs durchführen können.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: ef00f50ea2cda2c173208075123b3fe2b2d7ecd4
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 19%

---


# Experience Platform-APIs authentifizieren und aufrufen

Dieses Dokument bietet eine schrittweise Anleitung für den Zugriff auf ein Adobe Experience Platform-Entwicklerkonto, damit Sie Aufrufe an Experience Platform-APIs durchführen können. Am Ende dieses Tutorials haben Sie die folgenden Anmeldeinformationen generiert, die für alle Platform-API-Aufrufe erforderlich sind:

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{IMS_ORG}`

Um die Sicherheit Ihrer Anwendungen und Benutzer zu gewährleisten, müssen alle Anfragen an Adobe I/O-APIs mit Standards wie OAuth und JSON Web Tokens (JWT) authentifiziert und autorisiert werden. Ein JWT wird zusammen mit clientspezifischen Informationen verwendet, um Ihr persönliches Zugriffstoken zu generieren.

In diesem Tutorial wird beschrieben, wie Sie die erforderlichen Anmeldeinformationen zum Authentifizieren von Platform-API-Aufrufen erfassen, wie im folgenden Flussdiagramm beschrieben:

![](./images/api-authentication/authentication-flowchart.png)

## Voraussetzungen

Um Experience Platform-APIs erfolgreich aufrufen zu können, benötigen Sie Folgendes:

* Eine IMS-Organisation mit Zugriff auf Adobe Experience Platform.
* Ein Admin Console-Administrator, der Sie als Entwickler und Anwender für ein Produktprofil hinzufügen kann.

Sie müssen auch über eine Adobe ID verfügen, um dieses Tutorial abzuschließen. Wenn Sie keine Adobe ID haben, können Sie wie folgt eine erstellen:

1. Wechseln Sie zu [Adobe Developer Console](https://console.adobe.io).
2. Wählen Sie **[!UICONTROL Neues Konto erstellen]**.
3. Schließen Sie den Anmeldevorgang ab.

## Entwickler- und Benutzerzugriff für Experience Platform erlangen

Vor der Erstellung von Integrationen in der Adobe Developer Console muss Ihr Konto über Entwickler- und Benutzerberechtigungen für ein Experience Platform-Produktprofil in Adobe Admin Console verfügen.

### Entwicklerzugriff erlangen

Wenden Sie sich an einen [!DNL Admin Console]-Administrator in Ihrem Unternehmen, um Sie als Entwickler einem Experience Platform-Produktprofil mit [[!DNL Admin Console]](https://adminconsole.adobe.com/) hinzuzufügen. Spezifische Anweisungen zum Verwalten des Entwicklerzugriffs für Produktprofile](https://helpx.adobe.com/de/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html) finden Sie in der [!DNL Admin Console]-Dokumentation .[

Nachdem Sie als Entwickler zugewiesen wurden, können Sie mit der Erstellung von Integrationen in [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) beginnen. Bei diesen Integrationen handelt es sich um eine Pipeline von externen Apps und Diensten zu Adobe-APIs.

### Benutzerzugriff erlangen

Ihr [!DNL Admin Console]-Administrator muss Sie auch als Benutzer zum selben Produktprofil hinzufügen. Weitere Informationen finden Sie im Handbuch [Verwalten von Benutzergruppen in [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) .

## API-Schlüssel, Kennung der IMS-Organisation und Client-Geheimnis generieren {#api-ims-secret}

>[!NOTE]
>
>Wenn Sie diesem Dokument im [Privacy Service-Entwicklerhandbuch](../privacy-service/api/getting-started.md) folgen, können Sie jetzt zu diesem Handbuch zurückkehren, um die eindeutigen Zugriffsberechtigungen für [!DNL Privacy Service] zu generieren.

Nachdem Sie Entwickler- und Benutzerzugriff auf Platform über [!DNL Admin Console] erhalten haben, müssen Sie als Nächstes Ihre `{IMS_ORG}`- und `{API_KEY}`-Anmeldedaten in der Adobe Developer Console generieren. Diese Anmeldeinformationen müssen nur einmal generiert werden und können in zukünftigen Platform-API-Aufrufen wiederverwendet werden.

### Experience Platform zu einem Projekt hinzufügen

Wechseln Sie zur [Adobe-Entwicklerkonsole](https://www.adobe.com/go/devs_console_ui) und melden Sie sich mit Ihrer Adobe ID an. Führen Sie anschließend die Schritte aus, die im Tutorial [Erstellen eines leeren Projekts](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in der Dokumentation zu Adobe Developer Console beschrieben werden.

Nachdem Sie ein neues Projekt erstellt haben, wählen Sie **[!UICONTROL API]** hinzufügen im Bildschirm **[!UICONTROL Project Overview]** aus.

![](./images/api-authentication/add-api.png)

Der Bildschirm **[!UICONTROL API hinzufügen]** wird angezeigt. Wählen Sie das Produktsymbol für Adobe Experience Platform und dann **[!UICONTROL Experience Platform-API]** aus, bevor Sie **[!UICONTROL Weiter]** auswählen.

![](./images/api-authentication/platform-api.png)

Führen Sie von hier aus die im Tutorial zum Hinzufügen einer API zu einem Projekt mithilfe eines Dienstkontos (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (beginnend mit dem Schritt &quot;API konfigurieren&quot;) beschriebenen Schritte aus, um den Prozess abzuschließen.[

>[!IMPORTANT]
>
>In einem bestimmten Schritt während des oben verknüpften Prozesses lädt Ihr Browser automatisch einen privaten Schlüssel und ein damit verknüpftes öffentliches Zertifikat herunter. Beachten Sie, wo dieser private Schlüssel auf Ihrem Computer gespeichert ist, da er in einem späteren Schritt in diesem Tutorial erforderlich ist.

### Sammeln von Anmeldeinformationen

Nachdem die API zum Projekt hinzugefügt wurde, zeigt die Seite **[!UICONTROL Experience Platform API]** für das Projekt die folgenden Anmeldeinformationen an, die für alle Aufrufe an Experience Platform-APIs erforderlich sind:

* `{API_KEY}` ([!UICONTROL Client-ID])
* `{IMS_ORG}` ([!UICONTROL Organisations-ID])

![](././images/api-authentication/api-key-ims-org.png)

Zusätzlich zu den oben genannten Anmeldedaten benötigen Sie auch das generierte **[!UICONTROL Client Secret]** für einen zukünftigen Schritt. Wählen Sie **[!UICONTROL Client-Geheimnis abrufen]** aus, um den Wert anzuzeigen, und kopieren Sie ihn dann zur späteren Verwendung.

![](././images/api-authentication/client-secret.png)

## JSON-Web-Token (JWT) generieren {#jwt}

Der nächste Schritt besteht darin, ein JSON Web Token (JWT) basierend auf Ihren Kontoanmeldeinformationen zu generieren. Dieser Wert wird verwendet, um Ihre `{ACCESS_TOKEN}`-Anmeldedaten für die Verwendung in Platform-API-Aufrufen zu generieren, die alle 24 Stunden neu generiert werden müssen.

Wählen Sie im linken Navigationsbereich **[!UICONTROL Dienstkonto (JWT)]** und dann **[!UICONTROL JWT]** generieren aus.

![](././images/api-authentication/generate-jwt.png)

Fügen Sie in das unter **[!UICONTROL Benutzerdefiniertes JWT]** generieren bereitgestellte Textfeld den Inhalt des privaten Schlüssels ein, den Sie zuvor beim Hinzufügen der Platform-API zu Ihrem Dienstkonto generiert haben. Wählen Sie dann **[!UICONTROL Generate Token]** aus.

![](././images/api-authentication/paste-key.png)

Die Seite wird aktualisiert und zeigt das generierte JWT sowie einen cURL-Beispielbefehl an, mit dem Sie ein Zugriffstoken generieren können. Wählen Sie für diese Anleitung **[!UICONTROL Copy]** neben **[!UICONTROL Generated JWT]** aus, um das Token in die Zwischenablage zu kopieren.

![](././images/api-authentication/copy-jwt.png)

## Zugriffstoken generieren

Nachdem Sie ein JWT generiert haben, können Sie es in einem API-Aufruf verwenden, um Ihr `{ACCESS_TOKEN}` zu generieren. Im Gegensatz zu den Werten für `{API_KEY}` und `{IMS_ORG}` muss alle 24 Stunden ein neues Token generiert werden, um weiterhin Platform-APIs verwenden zu können.

**Anfrage**

Die folgende Anfrage generiert ein neues `{ACCESS_TOKEN}` basierend auf den in der Payload angegebenen Anmeldeinformationen. Dieser Endpunkt akzeptiert nur Formulardaten als Payload und muss daher eine `Content-Type`-Kopfzeile von `multipart/form-data` erhalten.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `{API_KEY}` | Die `{API_KEY}` ([!UICONTROL Client-ID]), die Sie in einem [vorherigen Schritt](#api-ims-secret) abgerufen haben. |
| `{SECRET}` | Das Client-Geheimnis, das Sie in einem [vorherigen Schritt](#api-ims-secret) abgerufen haben. |
| `{JWT}` | Das JWT, das Sie in einem [vorherigen Schritt](#jwt) generiert haben. |

>[!NOTE]
>
>Sie können denselben API-Schlüssel, dasselbe Client-Geheimnis und dasselbe JWT verwenden, um ein neues Zugriffstoken für jede Sitzung zu generieren. Auf diese Weise können Sie die Erstellung von Zugriffstoken in Ihren Anwendungen automatisieren.

**Antwort**

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399992
}
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `token_type` | Der Typ des zurückgegebenen Tokens. Für Zugriffstoken ist dieser Wert immer `bearer`. |
| `access_token` | Die generierte `{ACCESS_TOKEN}`. Dieser Wert, dem das Wort `Bearer` vorangestellt ist, ist als `Authentication`-Kopfzeile für alle Platform-API-Aufrufe erforderlich. |
| `expires_in` | Die Anzahl der Millisekunden, die bis zum Ablauf des Zugriffstokens verbleiben. Sobald dieser Wert 0 erreicht, muss ein neues Zugriffstoken generiert werden, um weiterhin Platform-APIs verwenden zu können. |

## Zugriffsberechtigungen testen

Nachdem Sie alle drei erforderlichen Anmeldeinformationen gesammelt haben, können Sie versuchen, den folgenden API-Aufruf durchzuführen. Dieser Aufruf listet alle standardmäßigen [!DNL Experience Data Model] (XDM)-Klassen auf, die für Ihr Unternehmen verfügbar sind.

**Anfrage**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwort**

Wenn Ihre Antwort der unten gezeigten ähnelt, sind Ihre Anmeldedaten gültig und funktionieren. (Diese Antwort wurde aus Platzgründen abgeschnitten.)

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

## Verwenden von Postman zum Authentifizieren und Testen von API-Aufrufen

[](https://www.postman.com/) Postmanis ist ein beliebtes Tool, mit dem Entwickler RESTful-APIs untersuchen und testen können. In diesem [Mittlerer Beitrag](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) wird beschrieben, wie Sie Postman so einrichten können, dass automatisch eine JWT-Authentifizierung erfolgt und Platform-APIs verwendet werden.

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie Ihre Zugangsdaten für Platform-APIs gesammelt und erfolgreich getestet. Sie können nun den Beispiel-API-Aufrufen folgen, die in der [Dokumentation](../landing/documentation/overview.md) bereitgestellt werden.

Zusätzlich zu den Authentifizierungswerten, die Sie in diesem Tutorial gesammelt haben, benötigen viele Platform-APIs auch eine gültige `{SANDBOX_NAME}` -Angabe als Kopfzeile. Weiterführende Informationen dazu finden Sie unter [Sandbox-Übersicht](../sandboxes/home.md).