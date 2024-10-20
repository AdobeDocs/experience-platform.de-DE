---
title: Authentifizieren von und Zugreifen auf die Reactor-API
description: Hier erfahren Sie, wie Sie mit der Reactor-API beginnen, einschließlich der Schritte zum Generieren erforderlicher Zugriffsberechtigungen.
exl-id: fc1acc1d-6cfb-43c1-9ba9-00b2730cad5a
source-git-commit: 2c8ac35e9bf72c91743714da1591c3414db5c5e9
workflow-type: tm+mt
source-wordcount: '908'
ht-degree: 51%

---

# Authentifizieren von und Zugreifen auf die Reactor-API

Damit die [Reactor-API](https://developer.adobe.com/experience-platform-apis/references/reactor/) zum Erstellen und Verwalten von Tags-Erweiterungen verwendet werden kann, muss jede Anfrage die folgenden Authentifizierungskopfzeilen enthalten:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

In diesem Handbuch wird beschrieben, wie Sie die Adobe-Entwicklerkonsole verwenden, um die Werte für die einzelnen Header zu erfassen, damit Sie Aufrufe an die Reactor-API durchführen können.

## Erhalten von Entwicklerzugriff auf Adobe Experience Platform {#gain-developer-access}

Bevor Sie Authentifizierungswerte für die Reactor-API generieren können, müssen Sie über Entwicklerzugriff auf Experience Platform verfügen. Um Entwicklerzugriff zu erhalten, führen Sie die ersten Schritte im [Authentifizierungs-Tutorial für Experience Platform](/help/landing/api-authentication.md) aus. Kehren Sie nach Abschluss des Schritts [Benutzerzugriff erlangen](/help/landing/api-authentication.md#gain-user-access) zu diesem Tutorial zurück, um die spezifischen Anmeldeinformationen für die Reactor-API zu generieren.

## Generieren von Zugriffsberechtigungen {#generate-access-credentials}

Mithilfe der Adobe-Entwicklerkonsole müssen Sie die folgenden drei Zugriffsberechtigungen generieren:

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Die ID (`{ORG_ID}`) und der API-Schlüssel (`{API_KEY}`) Ihres Unternehmens können in zukünftigen API-Aufrufen wiederverwendet werden, nachdem sie ursprünglich generiert wurden. Ihr Zugriffs-Token (`{ACCESS_TOKEN}`) ist jedoch temporär und muss alle 24 Stunden neu generiert werden.

Die Schritte zum Generieren dieser Werte werden im Folgenden detailliert beschrieben.

### Einmalige Einrichtung {#one-time-setup}

Wechseln Sie zur [Adobe-Entwicklerkonsole](https://www.adobe.com/go/devs_console_ui) und melden Sie sich mit Ihrer Adobe ID an. Führen Sie anschließend die im Tutorial [Erstellen eines leeren Projekts](https://developer.adobe.com/developer-console/docs/guides/projects/projects-empty/) in der Dokumentation zur Entwicklerkonsole beschriebenen Schritte aus.

Nachdem Sie ein Projekt erstellt haben, wählen Sie **API hinzufügen** im Bildschirm **Projektübersicht** aus.

![](../images/api/getting-started/add-api-button.png)

Der Bildschirm **API hinzufügen** wird angezeigt. Wählen Sie **Experience Platform Launch API** aus der Liste der verfügbaren APIs, bevor Sie **Weiter** auswählen.

![](../images/api/getting-started/add-launch-api.png)

Wählen Sie anschließend den Authentifizierungstyp aus, um Zugriffstoken zu generieren und auf die Experience Platform-API zuzugreifen.

>[!IMPORTANT]
>
>Wählen Sie die Methode **[!UICONTROL OAuth Server-zu-Server]** aus, da dies künftig die einzige unterstützte Methode sein wird. Die Methode **[!UICONTROL Dienstkonto (JWT)]** wird nicht mehr unterstützt. Während Integrationen, die die JWT-Authentifizierungsmethode verwenden, bis zum 1. Januar 2025 weiterhin funktionieren, empfiehlt Adobe dringend, vorhandene Integrationen vor diesem Datum auf die neue OAuth Server-zu-Server-Methode zu migrieren. Weitere Informationen finden Sie im Abschnitt [!BADGE Veraltet] .{type=negative}[Generieren Sie ein JSON-Web-Token (JWT)](/help/landing/api-authentication.md#jwt) im Tutorial zur Platform-API-Authentifizierung.

Klicken Sie auf **Weiter**, um fortzufahren.

![Wählen Sie die OAuth Server-zu-Server-Authentifizierungsmethode.](/help/tags/images/api/getting-started/oauth-authentication-method.png)

Im nächsten Bildschirm werden Sie aufgefordert, ein oder mehrere Produktprofile auszuwählen, die mit der API-Integration verknüpft werden sollen.

>[!NOTE]
>
Produktprofile werden von Ihrem Unternehmen über die Adobe Admin Console verwaltet und enthalten bestimmte Berechtigungssätze für granulare Funktionen. Produktprofile und ihre Berechtigungen können nur von Benutzern mit Administratorrechten innerhalb Ihres Unternehmens verwaltet werden. Wenn Sie sich nicht sicher sind, welche Produktprofile für die API ausgewählt werden sollen, wenden Sie sich an Ihren Administrator.

Wählen Sie die gewünschten Produktprofile aus der Liste aus und klicken Sie dann auf **Konfigurierte API speichern**, um die API-Registrierung abzuschließen.

![](../images/api/getting-started/select-product-profile.png)

### Sammeln von Anmeldeinformationen {#gather-credentials}

Nachdem die API zum Projekt hinzugefügt wurde, zeigt die Seite **[!UICONTROL Experience Platform-API]** für das Projekt die folgenden Anmeldeinformationen an, die für alle Aufrufe an Experience Platform-APIs erforderlich sind:

* `{API_KEY}` ([!UICONTROL Client-ID])
* `{ORG_ID}` ([!UICONTROL Organisations-ID])

![Integrationsinformationen nach dem Hinzufügen einer API in Developer Console.](/help/tags/images/api/getting-started/api-integration-information.png)

### Zugriffstoken generieren {#generate-access-token}

Der nächste Schritt besteht darin, eine `{ACCESS_TOKEN}` -Berechtigung für die Verwendung in Platform-API-Aufrufen zu generieren. Im Gegensatz zu den Werten für `{API_KEY}` und `{ORG_ID}` muss alle 24 Stunden ein neues Token generiert werden, um weiterhin Platform-APIs verwenden zu können.

>[!TIP]
>
Diese Token laufen nach 24 Stunden ab. Wenn Sie diese Integration für ein Programm verwenden, empfiehlt es sich, Ihr Träger-Token programmgesteuert aus Ihrem Programm abzurufen.

Je nach Anwendungsfall haben Sie zwei Möglichkeiten, Ihre Zugriffs-Token zu generieren:

* [Manuelles Generieren von Token](#manual)
* [Token-Generierung automatisieren](#auto-token)

#### Manuelles Generieren von Zugriffs-Token {#manual}

Um manuell einen neuen `{ACCESS_TOKEN}` zu generieren, navigieren Sie zu **[!UICONTROL Anmeldeinformationen]** > **[!UICONTROL OAuth Server-to-Server]** und wählen Sie **[!UICONTROL Zugriffstoken generieren]**, wie unten dargestellt.

![Bildschirmaufzeichnung, wie und wie das Zugriffstoken in der Developer Console-Benutzeroberfläche generiert wird.](/help/tags/images/api/getting-started/generate-access-token.gif)

Es wird ein neues Zugriffs-Token generiert und eine Schaltfläche zum Kopieren des Tokens in die Zwischenablage bereitgestellt. Dieser Wert wird für die erforderliche Autorisierungskopfzeile verwendet und muss im Format `Bearer {ACCESS_TOKEN}` angegeben werden.

#### Token-Generierung automatisieren {#auto-token}

Sie können auch eine Postman-Umgebung und -Sammlung verwenden, um Zugriffstoken zu generieren. Weitere Informationen finden Sie im Abschnitt über die Verwendung von Postman zum Authentifizieren und Testen von API-Aufrufen](/help/landing/api-authentication.md#use-postman) im Experience Platform API-Authentifizierungshandbuch.[

## API-Anmeldeinformationen testen {#test-api-credentials}

Durch Befolgen der Schritte in diesem Tutorial sollten Sie über gültige Werte für `{ORG_ID}`, `{API_KEY}` und `{ACCESS_TOKEN}` verfügen. Sie können diese Werte jetzt testen, indem Sie sie in einer einfachen cURL-Anfrage an die Reactor-API verwenden.

Beginnen Sie mit dem Versuch, einen API-Aufruf durchzuführen, um [alle Unternehmen aufzulisten](./endpoints/companies.md#list).

>[!NOTE]
>
Möglicherweise haben Sie in Ihrer Organisation keine Unternehmen. In diesem Fall lautet die Antwort HTTP-Status 404 (Nicht gefunden). Solange kein 403-Fehler (Verboten) ausgegeben wird, sind Ihre Zugangsdaten gültig und funktionieren.

Sobald Sie sich vergewissert haben, dass Ihre Zugriffsberechtigungen funktionieren, lesen Sie die weitere API-Referenzdokumentation, um mehr über die vielen Funktionen der API zu erfahren.

## Lesen von Beispiel-API-Aufrufen {#read-sample-api-calls}

Jedes Endpunkthandbuch enthält Beispiel-API-Aufrufe, die zeigen, wie Sie Ihre Anfragen formatieren. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zu [Lesen von Beispiel-API-Aufrufen](../../landing/api-guide.md#sample-api) im Erste-Schritte-Handbuch für Platform-APIs.

## Nächste Schritte {#next-steps}

Nachdem Sie nun wissen, welche Header verwendet werden sollen, können Sie mit Aufrufen an die Reactor-API beginnen. Wählen Sie eine der Endpunktleitfäden für die ersten Schritte aus:

* [Referenzdokumentation für Reactor-API](https://developer.adobe.com/experience-platform-apis/references/reactor/)
* [Übersicht über die Reactor-API](/help/tags/api/overview.md)
