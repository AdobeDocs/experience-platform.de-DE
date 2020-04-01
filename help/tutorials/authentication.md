---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Authentifizierung und Zugriff auf Experience Platform-APIs
topic: tutorial
translation-type: tm+mt
source-git-commit: fca15ebf87559b08dd09e63b5df5655b57ef5977

---


# Authentifizierung und Zugriff auf Experience Platform APIs

Dieses Dokument bietet eine schrittweise Anleitung zum Zugriff auf ein Adobe Experience Platform-Entwicklerkonto, um Aufrufe an Experience Platform-APIs durchzuführen.

## Authentifizierung für API-Aufrufe

Um die Sicherheit Ihrer Anwendungen und Benutzer zu gewährleisten, müssen alle Anforderungen an Adobe I/O-APIs mit Standards wie OAuth und JSON Web Tokens (JWT) authentifiziert und autorisiert werden. Die JWT wird dann zusammen mit kundenspezifischen Informationen verwendet, um Ihr persönliches Zugriffstoken zu generieren.

Dieses Lernprogramm beschreibt die Authentifizierungsschritte durch die Erstellung eines Zugriffstokens, das im folgenden Flussdiagramm dargestellt wird:
![](images/authentication/authentication-flowchart.png)

## Voraussetzungen

Für die erfolgreiche Ausführung von Aufrufen an Experience Platform-APIs benötigen Sie Folgendes:

* Eine IMS-Organisation mit Zugriff auf die Adobe Experience Platform
* Ein registriertes Adobe ID-Konto
* Administrator der Admin-Konsole, um Sie als **Entwickler** und als **Benutzer** für ein Produkt hinzuzufügen.

In den folgenden Abschnitten werden die Schritte zum Erstellen einer Adobe-ID und zum Erstellen eines Entwicklers und Benutzers für ein Unternehmen erläutert.

### Erstellen einer Adobe ID

Wenn Sie keine Adobe-ID haben, können Sie eine wie folgt erstellen:

1. Zur [Adobe-E/A-Konsole wechseln](https://console.adobe.io)
2. Klicken Sie auf **Neues Konto erstellen**
3. Anmeldevorgang abschließen


### Werden Sie Entwickler und Benutzer von Experience Platform für eine Organisation

Vor der Erstellung von Integrationen auf Adobe I/O muss Ihr Konto über Entwicklerberechtigungen für ein Produkt in einer IMS-Organisation verfügen. Ausführliche Informationen zu Entwicklerkonten in der Admin-Konsole finden Sie im [Support-Dokument](https://helpx.adobe.com/enterprise/using/manage-developers.html) für die Verwaltung von Entwicklern.

**Entwicklerzugriff erlangen**

Wenden Sie sich an einen Administrator der Admin-Konsole in Ihrer Organisation, um Sie als Entwickler für eines der Produkte Ihrer Organisation mithilfe der [Admin-Konsole](https://adminconsole.adobe.com/)hinzuzufügen.

![](images/authentication/assign-developer.png)

Der Administrator muss Sie als Entwickler mindestens einem Produkt-Profil zuweisen, um fortfahren zu können.

![](images/authentication/add-developer.png)

Nachdem Sie als Entwickler zugewiesen wurden, haben Sie Zugriffsrechte, um Integrationen auf [Adobe I/O](https://console.adobe.io/)zu erstellen. Bei diesen Integrationen handelt es sich um eine Pipeline von externen Apps und Diensten zur Adobe API.

**Benutzerzugriff sichern**

Der Administrator der Admin-Konsole muss Sie auch als Benutzer zum Produkt hinzufügen.

![](images/authentication/assign-users.png)

Ähnlich wie beim Hinzufügen eines Entwicklers muss der Administrator Sie mindestens einem Profil zuweisen, um fortfahren zu können.

![](images/authentication/assign-user-details.png)


## Einmalige Einrichtung

Die folgenden Schritte müssen nur einmal durchgeführt werden:

* Anmelden bei Adobe I/O Console
* Integration erstellen
* Abwärts-Zugriffswerte kopieren

Sobald Sie über Ihre Integrations- und Zugriffswerte verfügen, können Sie diese in Zukunft zur Authentifizierung wiederverwenden. Jeder Schritt wird nachfolgend detailliert behandelt.

### Anmelden bei der Adobe I/O-Konsole

Wechseln Sie zur [Adobe-E/A-Konsole](https://console.adobe.io/) und melden Sie sich mit Ihrer Adobe-ID an.

Nachdem Sie angemeldet sind, klicken Sie oben im Bildschirm auf die Registerkarte **Integrationen** . Eine Integration ist ein Dienstkonto, das für die ausgewählte IMS-Organisation erstellt wird. Sie dürfen nur die IMS-Organisation aufrufen, in der die Integration erstellt wird.

>[!NOTE]
>Wenn Ihr Konto mit mehreren Organisationen verknüpft ist, können Sie über das Dropdown-Menü oben rechts im Bildschirm problemlos zwischen ihnen wechseln.

### Integration erstellen

Klicken Sie auf der Seite &quot; **Integrationen** &quot;auf **Neue Integration** , um den Prozess Beginn. Der Prozess umfasst drei Schritte:
* Integrationstyp auswählen
* Wählen Sie, welcher Adobe-Dienst in
* Details zur Hinzufügen, öffentlicher Schlüssel und Produkt-Profil

![](images/authentication/integrations.png)

#### Integrationstyp auswählen

Im nächsten Bildschirm wird gefragt, ob Sie auf eine API zugreifen oder Beinahe-Echtzeit-Ereignis empfangen möchten. Wählen Sie **Zugriff auf eine API** und dann **Fortfahren**.

![](images/authentication/create-new-integration.png)

#### Wählen Sie, welcher Adobe-Dienst in

Wenn Ihr Konto mit mehreren IMS-Organisationen verknüpft ist, können Sie über das Dropdown-Menü oben rechts zwischen ihnen wechseln. Wählen Sie **Workshop** und **Experience Platform API** unter **Adobe Experience Platform** , um auf die APIs zuzugreifen.

![](images/authentication/integration-select-service.png)

Klicken Sie auf **Weiter** , um zum nächsten Abschnitt zu wechseln.

#### Details zur Hinzufügen, öffentlicher Schlüssel und Produkt-Profil

Im nächsten Bildschirm werden Sie aufgefordert, Ihre Integrationsdetails auszufüllen, Ihr Zertifikat für den öffentlichen Schlüssel einzugeben und ein Profil auszuwählen.

![](images/authentication/integration-details.png)

Geben Sie zuerst Ihre Integrationsdetails ein. Wählen Sie anschließend ein Profil aus. Produktfunktionen gewähren granularen Zugriff auf eine Reihe von Profilen, die zu dem Dienst gehören, den Sie in den vorherigen Schritten ausgewählt haben.

Für den Zertifikatabschnitt müssen Sie ein Zertifikat generieren:

**Für MacOS- und Linux-Plattformen:**

Öffnen Sie die Befehlszeile und führen Sie den folgenden Befehl aus:

`openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`


**Für Windows-Plattformen:**

1. Laden Sie einen openssl-Client herunter, um öffentliche Zertifikate zu generieren (z. B. [OpenSSL-Windows-Client](https://bintray.com/vszakats/generic/download_file?file_path=openssl-1.1.1-win64-mingw.zip))

1. Extrahieren Sie den Ordner und kopieren Sie ihn in den Ordner C:/libs/.

1. Öffnen Sie die Befehlszeilenaufforderung und führen Sie die folgenden Befehle aus:

   `set OPENSSL_CONF=C:/libs/openssl-1.1.1-win64-mingw/openssl.cnf`

   `cd C:/libs/openssl-1.1.1-win64-mingw/`

   `openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout private.key -out certificate_pub.crt`

Sie erhalten eine Antwort wie die folgende, die Sie auffordert, einige Informationen über sich selbst einzugeben:

```
Generating a 2048 bit RSA private key
.................+++
.......................................+++
writing new private key to 'private.key'
-----
You are about to be asked to enter information that will be incorporated
into your certificate request.
What you are about to enter is what is called a Distinguished Name or a DN.
There are quite a few fields but you can leave some blank
For some fields there will be a default value,
If you enter '.', the field will be left blank.
-----
Country Name (2 letter code) []:
State or Province Name (full name) []:
Locality Name (eg, city) []:
Organization Name (eg, company) []:
Organizational Unit Name (eg, section) []:
Common Name (eg, fully qualified host name) []:
Email Address []:
```

Nach Eingabe der Informationen werden zwei Dateien generiert: `certificate_pub.crt` und `private.key`.

>[!NOTE]
>`certificate_pub.crt` läuft in 365 Tagen ab. Sie können den Zeitraum verlängern, indem Sie den Wert von `days` im obigen `openssl` Befehl ändern. Das regelmäßige Drehen der Anmeldeinformationen ist jedoch eine gute Sicherheitsmaßnahme.

Die `private.key` wird verwendet, um unsere JWT im späteren Abschnitt zu generieren.

Mit der `certificate_pub.crt` wird ein API-Schlüssel erstellt. Gehen Sie zurück zur Adobe I/O-Konsole und klicken Sie auf Datei **auswählen** , um Ihre `certificate_pub.crt` Datei hochzuladen.

Klicken Sie auf Integration **erstellen** , um den Prozess abzuschließen.

### Herunterladen von Zugriffswerten

Nachdem Sie die Integration erstellt haben, können Sie deren Details Ansicht vornehmen. Klicken Sie auf **Clientgeheimnis** abrufen, und Ihr Bildschirm sieht in etwa so aus:

![](images/authentication/access-values.png)

Kopieren Sie die Werte für `{API KEY}`, d. h. `{IMS ORG}` die Organisations-ID, `{CLIENT SECRET}` da diese im nächsten Schritt verwendet werden.

## Authentifizierung für jede Sitzung

Der letzte Schritt besteht darin, Ihre API-Aufrufe zu generieren, `{ACCESS_TOKEN}` die zur Authentifizierung verwendet werden. Das Zugriffstoken muss bei jedem API-Aufruf, den Sie an Adobe Experience Platform richten, im Autorisierungs-Header enthalten sein. Zugriffstoken laufen nach 24 Stunden ab. Danach müssen neue Token generiert werden, um weiterhin die APIs verwenden zu können.

### JWT erstellen

Navigieren Sie auf der Detailseite Ihrer Integration in der Adobe I/O-Konsole zur Registerkarte **JWT** :

![](images/authentication/generate-jwt.png)

Auf der Seite werden Sie aufgefordert, die im vorherigen Abschnitt `private.key` erstellte einzugeben. Öffnen Sie die Befehlszeile, um den Inhalt der `private.key` Datei Ansicht:

```shell
cat private.key
```

Ihre Ausgabe sieht ungefähr so aus:

```shell
-----BEGIN PRIVATE KEY-----
MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQCYjPj18NrVlmrc
H+YUTuwWrlHTiPfkBGM0P1HbIOdwrlSTCmPhmaNNG5+mEiULJLWlrhQpx/7uQVNW
......
xbWgBWatJ2hUhU5/K2iFlNJBVXyNy7rN0XzOagLRJ1uS2CM6Hn3vBOqLbHRG4Pen
J1LvEocGunT12UJekLdEaQR4AKodIyjv5opvewrzxUZhVvUIIgeU5vUpg9smCXai
wPW5MQjmygodzCh7+eGLrg==
-----END PRIVATE KEY-----
```

Kopieren Sie die gesamte Ausgabe und fügen Sie sie in das Textfeld ein. Klicken Sie dann auf JWT **generieren**. Kopieren Sie die generierte JWT für den nächsten Schritt nach unten.

![](images/authentication/generated-jwt.png)

### Zugriffstoken generieren

Sie können ein Zugriffstoken über einen cURL-Befehl generieren. Wenn Sie cURL nicht installiert haben, können Sie es mit `npm install curl`installieren. Weitere Informationen zu cURL [finden Sie hier](https://curl.haxx.se/)

Nach der Installation von cURL müssen Sie die Felder im folgenden Befehl durch Ihre eigenen Felder `{API_KEY}`, `{CLIENT_SECRET}`und `{JWT_TOKEN}`ersetzen:

```SHELL
curl -X POST "https://ims-na1.adobelogin.com/ims/exchange/jwt/" \
  -F "client_id={API_KEY}" \
  -F "client_secret={CLIENT_SECRET}" \
  -F "jwt_token={JWT_TOKEN}"
```

Bei erfolgreichem Abschluss sieht die Ausgabe wie folgt aus:

```JSON
{
  "token_type":"bearer",
  "access_token":"eyJ4NXUiOiJpbXNfbmExLXN0ZzEta2V5LT2VyIiwiYWxnIjoiUlMyNTYifQ.eyJpZCI6IjE1MjAzMDU0ODY5MDhfYzMwM2JkODMtMWE1My00YmRiLThhNjctMWDhhNDJiNTE1X3VlMSIsImNsaWVudF9pZCI6ImYwNjY2Y2M4ZGVhNzQ1MWNiYzQ2ZmI2MTVkMzY1YzU0IiwidXNlcl9pZCI6IjA0ODUzMkMwNUE5ODg2QUQwQTQ5NDEzOUB0ZWNoYWNjdC5hZG9iZS5jb20iLCJzdGF0ZSI6IntcInNlc3Npb25cIjpcImh0dHBzOi8vaW1zLW5hMS1zdGcxLmFkb2JlbG9naW4uY29tL2ltcy9zZXNzaW9uL3YxL05UZzJZemM1TVdFdFlXWTNaUzAwT1RWaUxUZ3lPVFl0WkdWbU5EUTVOelprT0dFeUxTMHdORGcxTXpKRPVGc0TmtGRU1FRTBPVFF4TXpsQWRHVmphR0ZqWTNRdVlXUnZZbVV1WTI5dFwifSIsInR5cGUiOiJhY2Nlc3NfdG9rZW4iLCJhcyI6Imltcy1uYTEtc3RnMSIsImZnIjoiU0hRUlJUQ0ZTWFJJTjdSQjVVQ09NQ0lBWVU9PT09PT0iLCJtb2kiOiJhNTYwOWQ5ZiIsImMiOiJMeksySTBuZ2F2M1BhWWIxV0J3d3FRPT0iLCJleHBpcmVzX2luIjoiODY0MDAwMDAiLCJzY29wZSI6Im9wZW5pZCxzZXNzaW9uLEFkb2JlSUQscmVhZF9vcmdhbml6YXRpb25zLGFkZGl0aW9uYWxfaW5mby5wcm9qZWN0ZWRQcm9kdWN0Q29udGV4dCIsImNyZWF0ZWRfYXQiOiIxNTIwMzA1NDg2OTA4In0.EBgpw0JyKVzbjIBmH6fHDZUvJpvNG8xf8HUHNCK2l-dnVJqXxdi0seOk_kjVodkIa3evC54V560N60vi_mzt7gef-g954VH6l3gFh6XQ7yqRJD2LMW7G1lhQGhga4hrQCnJlfSQoztvIp9hkar9Zcu-MYgyEB5UlwK3KtB3elu7vJGk35F3T9OnqVL4PFj0Ix6zcuN_4gikgQgmtoUjuXULinbtu9Bkmdf7so9FvhapUd5ZTUTTMrAfJ36gEOQPqsuzlu9oUQaYTAn8v4B9TgoS0Paslo6WIksc4f_rSVWsbO6_TSUqIOi0e_RyL6GkMBA1ELA-Dkgbs-jUdkw",
  "expires_in":86399947
}
```

Ihr Zugriffstoken ist der Wert unter dem `access_token` Schlüssel. Dieses Zugriffstoken `expires_in` 86399947 Millisekunden (24 Stunden). Danach müssen Sie ein neues Zugriffstoken erstellen, indem Sie die oben beschriebenen Schritte ausführen.

Sie können jetzt API-Anfragen in Adobe Experience Platform stellen!

### Zugriffscode testen

Um zu testen, ob Ihr Zugriffstoken gültig ist, können Sie den folgenden API-Aufruf durchführen. Dieser Aufruf Liste alle Klassen innerhalb des `global` Containers:

>[!NOTE]
>`{API_KEY}` und `{IMS_ORG}` beziehen Sie sich auf die oben generierten Werte.

**Anfrage**

```SHELL
curl -X GET https://platform.adobe.io/data/foundation/schemaregistry/global/classes \
  -H 'Accept: application/vnd.adobe.xed-id+json' \
  -H 'Authorization: Bearer {ACCESS_TOKEN}' \
  -H 'x-api-key: {API_KEY}' \
  -H 'x-gw-ims-org-id: {IMS_ORG}'
```


Wenn Ihre Antwort der unten aufgeführten ähnlich ist, dann `access_token` ist Ihre Gültigkeit gültig und funktioniert. (Diese Antwort wurde aus Platzgründen abgeschnitten.)

**Antwort**

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

## Verwenden von Postman für JWT-Authentifizierung und API-Aufrufe

[Postman](https://www.getpostman.com/) ist ein beliebtes Werkzeug, um mit RESTful APIs zu arbeiten. In diesem [Beitrag](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f) &quot;Mittel&quot;wird beschrieben, wie Sie Postman so einrichten können, dass eine JWT-Authentifizierung automatisch durchgeführt und Adobe Experience Platform-APIs verwendet werden.