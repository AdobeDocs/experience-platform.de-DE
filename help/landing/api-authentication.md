---
keywords: Experience Platform;Home;beliebte Themen;Authentifizieren;Zugriff
solution: Experience Platform
title: Experience Platform-APIs authentifizieren und aufrufen
topic-legacy: tutorial
type: Tutorial
description: Dieses Dokument bietet eine schrittweise Anleitung für den Zugriff auf ein Adobe Experience Platform-Entwicklerkonto, damit Sie Aufrufe an Experience Platform-APIs durchführen können.
exl-id: dfe8a7be-1b86-4d78-a27e-87e4ed8b3d42
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 19%

---


# Experience Platform-APIs authentifizieren und aufrufen

Dieses Dokument bietet eine schrittweise Anleitung für den Zugriff auf ein Adobe Experience Platform-Entwicklerkonto, damit Sie Aufrufe an Experience Platform-APIs durchführen können. Am Ende dieses Tutorials haben Sie die folgenden Anmeldedaten erstellt, die für alle Platform API-Aufrufe erforderlich sind:

* `{ACCESS_TOKEN}`
* `{API_KEY}`
* `{IMS_ORG}`

Um die Sicherheit Ihrer Anwendungen und Benutzer zu gewährleisten, müssen alle Anfragen an Adobe I/O-APIs mit Standards wie OAuth und JSON Web Tokens (JWT) authentifiziert und autorisiert werden. Ein JWT wird zusammen mit kundenspezifischen Informationen verwendet, um Ihr persönliches Zugriffstoken zu generieren.

In diesem Tutorial wird erläutert, wie die erforderlichen Anmeldedaten zur Authentifizierung von Platform API-Aufrufen gesammelt werden, wie im folgenden Flussdiagramm beschrieben:

![](./images/api-authentication/authentication-flowchart.png)

## Voraussetzungen

Um erfolgreich Aufrufe von Experience Platform-APIs durchführen zu können, müssen Sie über Folgendes verfügen:

* Eine IMS-Organisation mit Zugriff auf Adobe Experience Platform.
* Ein Administrator der Admin Console, der Sie als Entwickler und Benutzer eines Produkt-Profils hinzufügen kann.

Sie müssen auch über ein Adobe ID verfügen, um dieses Tutorial abzuschließen. Wenn Sie keine Adobe ID haben, können Sie wie folgt eine erstellen:

1. Gehe zu [Adobe Developer Console](https://console.adobe.io).
2. Auswählen **[!UICONTROL Neues Konto erstellen]**.
3. Beenden Sie den Anmeldevorgang.

## Entwickler- und Benutzerzugriff für Experience Platform erlangen

Vor dem Erstellen von Integrationen in der Adobe Developer Console muss Ihr Konto über Entwickler- und Benutzerberechtigungen für ein Experience Platform-Produkt-Profil in Adobe Admin Console verfügen.

### Entwicklerzugriff erlangen

Kontakt [!DNL Admin Console] Administrator in Ihrem Unternehmen, um Sie als Entwickler einem Experience Platform-Produkt-Profil hinzuzufügen, indem Sie [[!DNL Admin Console]](https://adminconsole.adobe.com/). Siehe [!DNL Admin Console] Dokumentation für spezifische Anweisungen zum [Entwicklerzugriff für Produkt-Profil verwalten](https://helpx.adobe.com/de/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html).

Sobald Sie als Entwickler zugewiesen sind, können Sie Beginn beim Erstellen von Integrationen in [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui). Diese Integrationen sind eine Pipeline von externen Apps und Diensten zu Adobe-APIs.

### Benutzerzugriff erlangen

Ihre [!DNL Admin Console] Administrator muss Sie auch als Benutzer demselben Produkt-Profil hinzufügen. Siehe Leitfaden zu [Benutzergruppen verwalten in [!DNL Admin Console]](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/user-groups.ug.html) für weitere Informationen.

## API-Schlüssel, IMS-Org-ID und Client-Geheimnis erstellen {#api-ims-secret}

>[!NOTE]
>
>Wenn Sie diesem Dokument folgen von [Privacy Service-API-Handbuch](../privacy-service/api/getting-started.md), können Sie jetzt zu diesem Handbuch zurückkehren, um die Zugriffsberechtigungen zu generieren, die für [!DNL Privacy Service].

Nachdem Sie dem Entwickler und dem Benutzer Zugriff auf die Plattform gewährt haben über [!DNL Admin Console]. Der nächste Schritt ist die Erstellung Ihrer `{IMS_ORG}` und `{API_KEY}` Anmeldedaten in der Adobe Developer Console. Diese Anmeldedaten müssen nur einmal generiert werden und können in zukünftigen API-Aufrufen verwendet werden.

### Experience Platform zu einem Projekt Hinzufügen

Wechseln Sie zur [Adobe-Entwicklerkonsole](https://www.adobe.com/go/devs_console_ui) und melden Sie sich mit Ihrer Adobe ID an. Führen Sie anschließend die Schritte aus, die im Tutorial [Erstellen eines leeren Projekts](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in der Dokumentation zu Adobe Developer Console beschrieben werden.

Sobald Sie ein neues Projekt erstellt haben, wählen Sie **[!UICONTROL hinzufügen-API]** zu **[!UICONTROL Projektübersicht]** Bildschirm.

![](./images/api-authentication/add-api.png)

Der Bildschirm **[!UICONTROL API hinzufügen]** wird angezeigt. Wählen Sie das Produktsymbol für Adobe Experience Platform aus und wählen Sie dann **[!UICONTROL Experience Platform-API]** vor Auswahl **[!UICONTROL Weiter]**.

![](./images/api-authentication/platform-api.png)

Folgen Sie hier den Schritten, die im Tutorial zu [Hinzufügen einer API zu einem Projekt mit einem Dienstkonto (JWT)](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/services-add-api-jwt.md) (ab Schritt &quot;API konfigurieren&quot;), um den Prozess abzuschließen.

>[!IMPORTANT]
>
>In einem bestimmten Schritt während des oben verknüpften Prozesses lädt Ihr Browser automatisch einen privaten Schlüssel und ein damit verbundenes öffentliches Zertifikat herunter. Beachten Sie, wo dieser private Schlüssel auf Ihrem Computer gespeichert ist, da er in einem späteren Schritt in diesem Tutorial benötigt wird.

### Anmeldedaten sammeln

Sobald die API dem Projekt hinzugefügt wurde, wird die **[!UICONTROL Experience Platform-API]** auf der Projektseite werden die folgenden Anmeldedaten angezeigt, die bei allen Aufrufen von Experience Platform-APIs erforderlich sind:

* `{API_KEY}` ([!UICONTROL Client-ID])
* `{IMS_ORG}` ([!UICONTROL Organisations-ID])

![](././images/api-authentication/api-key-ims-org.png)

Zusätzlich zu den oben genannten Anmeldedaten benötigen Sie auch die **[!UICONTROL Kundengeheimnis]** für einen zukünftigen Schritt. Auswählen **[!UICONTROL Kundengeheimnis abrufen]** , um den Wert anzuzeigen und ihn dann zur späteren Verwendung zu kopieren.

![](././images/api-authentication/client-secret.png)

## JSON-Web-Token (JWT) erstellen {#jwt}

Im nächsten Schritt erstellen Sie ein JSON Web Token (JWT) auf Basis Ihrer Kontoanmeldedaten. Dieser Wert wird verwendet, um Ihre `{ACCESS_TOKEN}` Anmeldedaten für die Verwendung in Platform API-Aufrufen, die alle 24 Stunden neu generiert werden müssen.

Auswählen **[!UICONTROL Dienstkonto (JWT)]** in der linken Navigation und wählen Sie dann **[!UICONTROL JWT erstellen]**.

![](././images/api-authentication/generate-jwt.png)

Im Textfeld unter **[!UICONTROL Benutzerdefiniertes JWT erstellen]**, fügen Sie den Inhalt des privaten Schlüssels ein, den Sie zuvor beim Hinzufügen der Plattform-API zu Ihrem Dienstkonto erstellt haben. Wählen Sie dann **[!UICONTROL Token generieren]**.

![](././images/api-authentication/paste-key.png)

Die Seite wird aktualisiert, um die generierte JWT sowie einen Beispielbefehl für cURL anzuzeigen, mit dem Sie ein Zugriffstoken generieren können. Für die Zwecke dieses Tutorials wählen Sie **[!UICONTROL Kopieren]** neben **[!UICONTROL Generierte JWT]** , um das Token in die Zwischenablage zu kopieren.

![](././images/api-authentication/copy-jwt.png)

## Zugriffstoken erstellen

Nachdem Sie eine JWT erstellt haben, können Sie sie in einem API-Aufruf verwenden, um Ihre `{ACCESS_TOKEN}`. Im Gegensatz zu den Werten für `{API_KEY}` und `{IMS_ORG}`muss alle 24 Stunden ein neues Token erstellt werden, um weiterhin Platform APIs verwenden zu können.

**Anfrage**

Die folgende Anforderung generiert eine neue `{ACCESS_TOKEN}` auf der Grundlage der in der Nutzlast angegebenen Anmeldeinformationen. Dieser Endpunkt akzeptiert nur Formulardaten als Nutzlast und muss daher `Content-Type` Kopfzeile von `multipart/form-data`.

```shell
curl -X POST https://ims-na1.adobelogin.com/ims/exchange/jwt \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `{API_KEY}` | Die `{API_KEY}` ([!UICONTROL Client-ID]), die Sie in einem [Vorheriger Schritt](#api-ims-secret). |
| `{SECRET}` | Das Kundengeheimnis, das Sie in einem [Vorheriger Schritt](#api-ims-secret). |
| `{JWT}` | Die JWT, die Sie in einem [Vorheriger Schritt](#jwt). |

>[!NOTE]
>
>Sie können denselben API-Schlüssel, dasselbe Clientgeheimnis und dasselbe JWT verwenden, um ein neues Zugriffstoken für jede Sitzung zu erstellen. Dadurch können Sie die Erstellung von Zugriffstoken in Ihren Anwendungen automatisieren.

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
| `access_token` | Die `{ACCESS_TOKEN}`. Dieser Wert, dem Wort vorangestellt `Bearer`, wird als `Authentication` -Header für alle Platform-API-Aufrufe. |
| `expires_in` | Die Anzahl der Millisekunden, die bis zum Ablauf des Zugriffstokens verbleiben. Wenn dieser Wert 0 erreicht, muss ein neues Zugriffstoken erstellt werden, um weiterhin Platform APIs verwenden zu können. |

## Zugriffsberechtigungen testen

Nachdem Sie alle drei erforderlichen Anmeldedaten gesammelt haben, können Sie versuchen, den folgenden API-Aufruf durchzuführen. Dieser Aufruf Liste alle Standardwerte [!DNL Experience Data Model] (XDM) Klassen für Ihr Unternehmen verfügbar.

**Anfrage**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```

**Antwort**

Wenn Ihre Antwort der unten angezeigten ähnlich ist, sind Ihre Anmeldedaten gültig und funktionieren. (Diese Antwort wurde aus Platzgründen abgeschnitten.)

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

[Postman](https://www.postman.com/) ist ein beliebtes Tool, mit dem Entwickler RESTful-APIs erkunden und testen können. Dieses [Mittlerer Beitrag](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) beschreibt, wie Sie Postman so einrichten können, dass es automatisch JWT-Authentifizierung ausführt und zum Verwenden von Plattform-APIs verwendet wird.

## Nächste Schritte

Durch Lesen dieses Dokuments haben Sie Ihre Zugriffsberechtigungen für Platform-APIs gesammelt und erfolgreich getestet. Sie können nun den Beispielaufrufen der API folgen, die im gesamten [Dokumentation](../landing/documentation/overview.md).

Zusätzlich zu den Authentifizierungswerten, die Sie in diesem Tutorial gesammelt haben, benötigen viele Plattform-APIs auch eine gültige `{SANDBOX_NAME}` als Kopfzeile bereitzustellen. Weiterführende Informationen dazu finden Sie unter [Sandbox-Übersicht](../sandboxes/home.md).