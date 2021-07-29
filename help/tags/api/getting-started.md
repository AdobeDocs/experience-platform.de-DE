---
title: Erste Schritte mit der Reactor-API
description: Erfahren Sie, wie Sie mit der Reactor-API beginnen, einschließlich der Schritte zum Generieren erforderlicher Zugriffsberechtigungen.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1064'
ht-degree: 2%

---

# Erste Schritte mit der Reactor-API

Um die [Reactor-API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/reactor.yaml) verwenden zu können, muss jede Anfrage die folgenden Authentifizierungskopfzeilen enthalten:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

In diesem Handbuch wird beschrieben, wie Sie die Adobe Developer Console verwenden, um die Werte für die einzelnen Header zu erfassen, damit Sie Aufrufe an die Reactor-API durchführen können.

## Entwicklerzugriff auf Adobe Experience Platform erhalten

Bevor Sie Authentifizierungswerte für die Reactor-API generieren können, müssen Sie über Entwicklerzugriff auf Experience Platform verfügen. Um Entwicklerzugriff zu erhalten, führen Sie die ersten Schritte im [Tutorial zur Experience Platform-Authentifizierung](http://www.adobe.com/go/platform-api-authentication-en) aus. Sobald Sie den Schritt &quot;Anmeldeinformationen für den Zugriff in der Adobe Developer Console generieren&quot;erreicht haben, kehren Sie zu diesem Tutorial zurück, um die spezifischen Anmeldeinformationen für die Reactor-API zu generieren.

## Zugriffsberechtigungen generieren

Mithilfe der Adobe Developer Console müssen Sie die folgenden drei Zugriffsberechtigungen generieren:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Die ID (`{IMS_ORG}`) Ihrer IMS-Organisation und der API-Schlüssel (`{API_KEY}`) können nach der anfänglichen Erstellung in zukünftigen API-Aufrufen wiederverwendet werden. Ihr Zugriffstoken (`{ACCESS_TOKEN}`) ist jedoch temporär und muss alle 24 Stunden neu generiert werden.

Die Schritte zum Generieren dieser Werte werden im Folgenden detailliert beschrieben.

### Einmalige Einrichtung

Wechseln Sie zu [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) und melden Sie sich mit Ihrer Adobe ID an. Führen Sie anschließend die im Tutorial [Erstellen eines leeren Projekts](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) beschriebenen Schritte in der Dokumentation zur Developer Console aus.

Nachdem Sie ein Projekt erstellt haben, wählen Sie **API** hinzufügen im Bildschirm **Project Overview** aus.

![](../images/api/getting-started/add-api-button.png)

Der Bildschirm **API** hinzufügen wird angezeigt. Wählen Sie **Experience Platform Reactor-API** aus der Liste der verfügbaren APIs, bevor Sie **Weiter** auswählen.

![](../images/api/getting-started/add-launch-api.png)

Im nächsten Bildschirm werden Sie aufgefordert, eine JSON Web Token (JWT)-Berechtigung zu erstellen, die entweder ein neues Keypair generiert oder Ihren eigenen öffentlichen Schlüssel hochlädt. Wählen Sie für dieses Tutorial die Option **Generate a key pair** und dann **Generate keypair** in der rechten unteren Ecke.

![](../images/api/getting-started/create-jwt.png)

Im nächsten Bildschirm wird bestätigt, dass das Keypair erfolgreich generiert wurde und ein komprimierter Ordner mit einem öffentlichen Zertifikat und einem privaten Schlüssel automatisch auf Ihren Computer heruntergeladen wird. Dieser private Schlüssel ist in einem späteren Schritt erforderlich, um ein Zugriffstoken zu generieren.

Wählen Sie **Next** aus, um fortzufahren.

![](../images/api/getting-started/keypair-generated.png)

Im nächsten Bildschirm werden Sie aufgefordert, ein oder mehrere Produktprofile auszuwählen, die mit der API-Integration verknüpft werden sollen.

>[!NOTE]
>
>Produktprofile werden von Ihrem Unternehmen über die Adobe Admin Console verwaltet und enthalten bestimmte Berechtigungssätze für granulare Funktionen. Produktprofile und ihre Berechtigungen können nur von Benutzern mit Administratorrechten innerhalb Ihres Unternehmens verwaltet werden. Wenn Sie sich nicht sicher sind, welche Produktprofile für die API ausgewählt werden sollen, wenden Sie sich an Ihren Administrator.

Wählen Sie die gewünschten Produktprofile aus der Liste aus und klicken Sie dann auf **Konfigurierte API speichern** , um die API-Registrierung abzuschließen.

![](../images/api/getting-started/select-product-profile.png)

Nachdem die API zum Projekt hinzugefügt wurde, wird die Projektseite erneut auf der Experience Platform Reactor-API-Seite angezeigt. Scrollen Sie von hier nach unten zum Abschnitt **Dienstkonto (JWT)** , der die folgenden Zugriffsberechtigungen bereitstellt, die für alle Aufrufe der Reactor-API erforderlich sind:

* **CLIENT-ID**: Die Client-ID ist die erforderliche,  `{API_KEY}` die in der  `x-api-key` Kopfzeile angegeben werden muss.
* **ORGANISATIONS-ID**: Die Organisations-ID ist der  `{IMS_ORG}` Wert, der in der  `x-gw-ims-org-id` Kopfzeile verwendet werden muss.

![](../images/api/getting-started/access-creds.png)

### Authentifizierung für jede Sitzung

Nachdem Sie nun über die Werte `{API_KEY}` und `{IMS_ORG}` verfügen, generiert der letzte Schritt einen `{ACCESS_TOKEN}` -Wert.

>[!NOTE]
>
>Diese Token laufen nach 24 Stunden ab. Wenn Sie diese Integration für eine Anwendung verwenden, empfiehlt es sich, Ihr Trägertoken programmgesteuert aus Ihrer Anwendung abzurufen.

Je nach Anwendungsfall haben Sie zwei Möglichkeiten, Ihre Zugriffstoken zu generieren:

* [Manuelles Generieren von Token](#manual)
* [Token programmgesteuert generieren](#program)

#### Zugriffstoken manuell generieren {#manual}

Öffnen Sie den zuvor heruntergeladenen privaten Schlüssel in einem Texteditor oder Browser und kopieren Sie den Inhalt. Navigieren Sie dann zurück zur Developer Console und fügen Sie den privaten Schlüssel in den Abschnitt **Zugriffstoken generieren** auf der Reactor-API-Seite für Ihr Projekt ein, bevor Sie **Token generieren** auswählen.

![](../images/api/getting-started/paste-private-key.png)

Es wird ein neues Zugriffstoken generiert und eine Schaltfläche zum Kopieren des Tokens in die Zwischenablage bereitgestellt. Dieser Wert wird für die erforderliche `Authorization`-Kopfzeile verwendet und muss im Format `Bearer {ACCESS_TOKEN}` angegeben werden.

![](../images/api/getting-started/token-generated.png)

#### Zugriffstoken programmgesteuert generieren {#program}

Wenn Sie Ihre Integration für eine Anwendung verwenden, können Sie über API-Anfragen programmgesteuert Zugriffstoken generieren. Um dies zu erreichen, müssen Sie die folgenden Werte abrufen:

* Client-ID (`{API_KEY}`)
* Client-Geheimnis (`{SECRET}`)
* Ein JSON-Web-Token (`{JWT}`)

Ihre Client-ID und Ihr Client-Geheimnis können Sie von der Hauptseite für Ihr Projekt erhalten, wie im [vorherigen Schritt](#one-time-setup) dargestellt.

![](../images/api/getting-started/auto-access-creds.png)

Um Ihre JWT-Berechtigung zu erhalten, navigieren Sie im linken Navigationsbereich zu **Service Account (JWT)** und wählen Sie dann die Registerkarte **JWT generieren** aus. Fügen Sie auf dieser Seite unter **Benutzerdefiniertes JWT** erstellen den Inhalt Ihres privaten Schlüssels in das bereitgestellte Textfeld ein und wählen Sie dann **Token generieren** aus.

![](../images/api/getting-started/generate-jwt.png)

Das generierte JWT wird unten angezeigt, sobald die Verarbeitung abgeschlossen ist, zusammen mit einem Beispielbefehl cURL , mit dem Sie das Token bei Bedarf testen können. Verwenden Sie die Schaltfläche **Kopieren** , um das Token in die Zwischenablage zu kopieren.

![](../images/api/getting-started/jwt-generated.png)

Nachdem Sie Ihre Anmeldedaten gesammelt haben, können Sie den unten stehenden API-Aufruf in Ihre Anwendung integrieren, um Zugriffstoken programmgesteuert zu generieren.

**Anfrage**

Die Anfrage muss eine `multipart/form-data`-Payload senden und Ihre Authentifizierungsberechtigungen angeben, wie unten dargestellt:

```shell
curl -X POST \
  https://ims-na1.adobelogin.com/ims/exchange/jwt/ \
  -H 'Content-Type: multipart/form-data' \
  -F 'client_id={API_KEY}' \
  -F 'client_secret={SECRET}' \
  -F 'jwt_token={JWT}'
```

**Antwort**

Eine erfolgreiche Antwort gibt ein neues Zugriffstoken sowie die Anzahl der Sekunden zurück, die bis zu seinem Ablauf verbleiben.

```json
{
  "token_type": "bearer",
  "access_token": "{ACCESS_TOKEN}",
  "expires_in": 86399999
}
```

| Eigenschaft | Beschreibung |
| :-- | :-- |
| `access_token` | Der neu generierte Zugriffstoken-Wert. Dieser Wert wird für die erforderliche `Authorization`-Kopfzeile verwendet und muss im Format `Bearer {ACCESS_TOKEN}` angegeben werden. |
| `expires_in` | Die verbleibende Zeit bis zum Ablauf des Tokens in Millisekunden. Sobald ein Token abläuft, muss ein neuer generiert werden. |

{style=&quot;table-layout:auto&quot;}

## Nächste Schritte

Durch Befolgen der Schritte in diesem Tutorial sollten Sie über gültige Werte für `{IMS_ORG}`, `{API_KEY}` und `{ACCESS_TOKEN}` verfügen. Sie können diese Werte jetzt testen, indem Sie sie in einer einfachen cURL-Anfrage an die Reactor-API verwenden.

Beginnen Sie mit dem Versuch, einen API-Aufruf an [aufzuführen, um alle Unternehmen](./endpoints/companies.md#list) aufzulisten.

>[!NOTE]
>
>Möglicherweise haben Sie in Ihrem Unternehmen keine Unternehmen. In diesem Fall lautet die Antwort HTTP-Status 404 (Nicht gefunden). Solange kein 403-Fehler (Verboten) ausgegeben wird, sind Ihre Zugangsdaten gültig und funktionieren.

Sobald Sie sich vergewissert haben, dass Ihre Zugriffsberechtigungen funktionieren, lesen Sie die andere API-Referenzdokumentation, um mehr über die vielen Funktionen der API zu erfahren.

## Zusätzliche Ressourcen

JWT-Bibliotheken und SDKs: [https://jwt.io/](https://jwt.io/)

Postman-API-Entwicklung: [https://www.postman.com/](https://www.postman.com/)
