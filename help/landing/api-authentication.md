---
keywords: Experience Platform;Home;beliebte Themen;Authentifizieren;Zugriff
solution: Experience Platform
title: Experience Platform-APIs authentifizieren und aufrufen
topic-legacy: tutorial
type: Tutorial
description: Dieses Dokument bietet eine schrittweise Anleitung für den Zugriff auf ein Adobe Experience Platform-Entwicklerkonto, damit Sie Aufrufe an Experience Platform-APIs durchführen können.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
translation-type: tm+mt
source-git-commit: ef00f50ea2cda2c173208075123b3fe2b2d7ecd4
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 14%

---


# Experience Platform-APIs authentifizieren und aufrufen

Dieses Dokument bietet eine schrittweise Anleitung für den Zugriff auf ein Adobe Experience Platform-Entwicklerkonto, damit Sie Aufrufe an Experience Platform-APIs durchführen können. Am Ende dieses Lernprogramms haben Sie die folgenden Anmeldeinformationen generiert, die für alle Plattform-API-Aufrufe erforderlich sind:

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{IMS_ORG}`

Um die Sicherheit Ihrer Anwendungen und Benutzer zu gewährleisten, müssen alle Anfragen an Adobe I/O-APIs mit Standards wie OAuth und JSON Web Tokens (JWT) authentifiziert und autorisiert werden. Ein JWT wird zusammen mit kundenspezifischen Informationen verwendet, um Ihr persönliches Zugriffstoken zu generieren.

In diesem Lernprogramm wird beschrieben, wie Sie die erforderlichen Anmeldeinformationen für die Authentifizierung von Plattform-API-Aufrufen erfassen, wie im folgenden Flussdiagramm dargestellt:

![](./images/api-authentication/authentication-flowchart.png)

## Voraussetzungen 

Damit Experience Platform-APIs erfolgreich aufgerufen werden können, müssen Sie über Folgendes verfügen:

* Eine IMS-Organisation mit Zugriff auf Adobe Experience Platform.
* Ein Produktadministrator, der Sie als Entwickler und Benutzer für ein Profil hinzufügen kann.

Sie müssen auch über ein Adobe ID verfügen, um dieses Lernprogramm abzuschließen. Wenn Sie keine Adobe ID haben, können Sie wie folgt eine erstellen:

1. Wechseln Sie zu [Adobe Developer Console](https://console.adobe.io).
2. Wählen Sie **[!UICONTROL Neues Konto erstellen]**.
3. Schließen Sie den Anmeldevorgang ab.

## Entwickler- und Benutzerzugriff für die Experience Platform

Vor der Erstellung von Integrationen in der Adobe Developer Console muss Ihr Konto über Entwickler- und Benutzerberechtigungen für ein Experience Platform Product Profil in Adobe Admin Console verfügen.

### Entwicklerzugriff erlangen

Wenden Sie sich an einen [!DNL Admin Console]-Administrator in Ihrem Unternehmen, um Sie mit dem [[!DNL Admin Console]](https://adminconsole.adobe.com/) als Entwickler zu einem Experience Platform Product Profil hinzuzufügen. Spezifische Anweisungen zum Verwalten des Entwicklerzugriffs für Profil](https://helpx.adobe.com/de/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html) finden Sie in der [!DNL Admin Console]-Dokumentation.[

Nachdem Sie als Entwickler zugewiesen wurden, können Sie Beginn zum Erstellen von Integrationen in [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_de) erstellen. Diese Integrationen sind eine Pipeline von externen Apps und Diensten zu Adobe-APIs.

### Benutzerzugriff erlangen

Ihr [!DNL Admin Console]-Administrator muss Sie auch als Benutzer zum gleichen Profil hinzufügen. Weitere Informationen finden Sie im Handbuch [Verwalten von Benutzergruppen in [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html).

## Erstellen Sie einen API-Schlüssel, eine IMS-Organisations-ID und einen Clientschlüssel {#api-ims-secret}

>[!NOTE]
>
>Wenn Sie diesem Dokument im [Privacy Service-Entwicklerhandbuch](../privacy-service/api/getting-started.md) folgen, können Sie jetzt zu diesem Handbuch zurückkehren, um die eindeutigen Zugriffsberechtigungen für [!DNL Privacy Service] zu generieren.

Nachdem Sie über [!DNL Admin Console] Entwickler- und Benutzerzugriff auf die Plattform erhalten haben, müssen Sie als Nächstes Ihre `{IMS_ORG}`- und `{API_KEY}`-Anmeldedaten in der Adobe Developer Console generieren. Diese Anmeldeinformationen müssen nur einmal generiert werden und können in zukünftigen Plattform-API-Aufrufen wiederverwendet werden.

### hinzufügen der Experience Platform zu einem Projekt

Wechseln Sie zu [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) und melden Sie sich bei Ihrem Adobe ID an. Führen Sie anschließend die Schritte aus, die im Lernprogramm [Erstellen eines leeren Projekts](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in der Adobe Developer Console-Dokumentation beschrieben werden.

Nachdem Sie ein neues Projekt erstellt haben, wählen Sie im Bildschirm **[!UICONTROL Projektübersicht]** die Option **[!UICONTROL Hinzufügen-API]**.

![](./images/api-authentication/add-api.png)

Der Bildschirm **[!UICONTROL Hinzufügen eine API]** wird angezeigt. Wählen Sie das Produktsymbol für Adobe Experience Platform und dann **[!UICONTROL Experience Platform-API]**, bevor Sie **[!UICONTROL Weiter]** auswählen.

![](./images/api-authentication/platform-api.png)

Gehen Sie von hier aus wie im Lernprogramm unter [Hinzufügen einer API zu einem Projekt mithilfe eines Dienstkontos (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (beginnend mit dem Schritt &quot;API konfigurieren&quot;) beschrieben vor, um den Prozess abzuschließen.

>[!IMPORTANT]
>
>In einem bestimmten Schritt während des oben verknüpften Prozesses lädt Ihr Browser automatisch einen privaten Schlüssel und ein dazugehöriges öffentliches Zertifikat herunter. Beachten Sie, wo dieser private Schlüssel auf Ihrem Computer gespeichert ist, da er in einem späteren Schritt dieses Lernprogramms benötigt wird.

### Anmeldeinformationen sammeln

Nachdem die API zum Projekt hinzugefügt wurde, zeigt die Seite **[!UICONTROL Experience Platform-API]** für das Projekt die folgenden Anmeldeinformationen an, die für alle Aufrufe der Experience Platform-APIs erforderlich sind:

* `{API_KEY}` ([!UICONTROL Client-ID])
* `{IMS_ORG}` ([!UICONTROL Organisations-ID])

![](././images/api-authentication/api-key-ims-org.png)

Zusätzlich zu den oben genannten Anmeldeinformationen benötigen Sie für einen zukünftigen Schritt auch den generierten **[!UICONTROL geheimen Clientschlüssel]**. Wählen Sie **[!UICONTROL Clientgeheimnis abrufen]**, um den Wert anzuzeigen und ihn dann für die spätere Verwendung zu kopieren.

![](././images/api-authentication/client-secret.png)

## JSON-WebToken (JWT) {#jwt} erstellen

Der nächste Schritt besteht darin, ein JSON-Web-Token (JWT) zu erstellen, das auf Ihren Kontoanmeldeinformationen basiert. Dieser Wert wird verwendet, um Ihre `{ACCESS_TOKEN}`-Berechtigung für die Verwendung in Plattform-API-Aufrufen zu generieren, die alle 24 Stunden neu generiert werden müssen.

Wählen Sie **[!UICONTROL Dienstkonto (JWT)]** in der linken Navigation und dann **[!UICONTROL JWT erzeugen]**.

![](././images/api-authentication/generate-jwt.png)

Fügen Sie im Textfeld unter **[!UICONTROL Benutzerspezifische JWT]** erstellen den Inhalt des privaten Schlüssels ein, den Sie zuvor beim Hinzufügen der Plattform-API zu Ihrem Dienstkonto erstellt haben. Wählen Sie dann **[!UICONTROL Token generieren]**.

![](././images/api-authentication/paste-key.png)

Die Seite wird aktualisiert, um die generierte JWT zusammen mit einem Beispiel-Befehl cURL anzuzeigen, mit dem Sie ein Zugriffstoken generieren können. Für diese Übung wählen Sie **[!UICONTROL Kopieren]** neben **[!UICONTROL Generierte JWT]**, um das Token in die Zwischenablage zu kopieren.

![](././images/api-authentication/copy-jwt.png)

## Zugriffstoken erstellen

Nachdem Sie eine JWT generiert haben, können Sie sie in einem API-Aufruf verwenden, um Ihre `{ACCESS_TOKEN}` zu generieren. Im Gegensatz zu den Werten für `{API_KEY}` und `{IMS_ORG}` muss alle 24 Stunden ein neues Token generiert werden, um weiterhin Plattform-APIs verwenden zu können.

**Anfrage**

Die folgende Anforderung generiert ein neues `{ACCESS_TOKEN}` basierend auf den in der Payload angegebenen Anmeldeinformationen. Dieser Endpunkt akzeptiert nur Formulardaten als Nutzlast und muss daher eine `Content-Type`-Kopfzeile von `multipart/form-data` erhalten.

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
| `{SECRET}` | Das Clientgeheimnis, das Sie in einem [vorherigen Schritt](#api-ims-secret) abgerufen haben. |
| `{JWT}` | Die JWT, die Sie in einem [vorherigen Schritt](#jwt) generiert haben. |

>[!NOTE]
>
>Sie können denselben API-Schlüssel, denselben Clientschlüssel und denselben JWT verwenden, um ein neues Zugriffstoken für jede Sitzung zu erstellen. Dadurch können Sie die Erstellung von Zugriffstoken in Ihren Anwendungen automatisieren.

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
| `token_type` | Der Typ des zurückgegebenen Tokens. Bei Zugriffstoken ist dieser Wert immer `bearer`. |
| `access_token` | Das generierte `{ACCESS_TOKEN}`. Dieser Wert, dem das Wort `Bearer` vorangestellt wird, ist als `Authentication`-Kopfzeile für alle Plattform-API-Aufrufe erforderlich. |
| `expires_in` | Die Anzahl der Millisekunden, die bis zum Ablauf des Zugriffstokens verbleiben. Sobald dieser Wert 0 erreicht hat, muss ein neues Zugriffstoken generiert werden, um weiterhin Plattform-APIs verwenden zu können. |

## Zugriffsberechtigungen testen

Nachdem Sie alle drei erforderlichen Anmeldeinformationen gesammelt haben, können Sie versuchen, den folgenden API-Aufruf durchzuführen. Dieser Aufruf Liste alle standardmäßigen [!DNL Experience Data Model] (XDM) Klassen, die für Ihr Unternehmen verfügbar sind.

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

## Verwenden Sie Postman, um API-Aufrufe zu authentifizieren und zu testen

[](https://www.postman.com/) Postmanis ist ein beliebtes Tool, mit dem Entwickler RESTful-APIs erkunden und testen können. In diesem [Mittleren Beitrag](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) wird beschrieben, wie Sie Postman so einrichten können, dass die JWT-Authentifizierung automatisch durchgeführt wird und damit Plattform-APIs verwendet werden.

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie Ihre Zugriffsberechtigungen für Plattform-APIs gesammelt und erfolgreich getestet. Sie können nun die Beispiel-API-Aufrufe im Abschnitt [Dokumentation](../landing/documentation/overview.md) verfolgen.

Zusätzlich zu den Authentifizierungswerten, die Sie in diesem Tutorial gesammelt haben, benötigen viele Plattform-APIs auch eine gültige `{SANDBOX_NAME}`-Angabe als Kopfzeile. Weiterführende Informationen dazu finden Sie unter [Sandbox-Übersicht](../sandboxes/home.md).