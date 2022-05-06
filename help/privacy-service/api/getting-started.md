---
title: Erste Schritte mit der Privacy Service-API
description: Erfahren Sie, wie Sie sich bei der Privacy Service-API authentifizieren und wie Sie Beispiel-API-Aufrufe in der Dokumentation interpretieren.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 47a94b00e141b24203b01dc93834aee13aa6113c
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 31%

---

# Erste Schritte mit der Privacy Service-API

Dieses Handbuch bietet eine Einführung in die wichtigsten Konzepte, die Sie kennen müssen, bevor Sie Aufrufe an die Privacy Service-API durchführen.

## Voraussetzungen

Dieses Handbuch setzt ein Verständnis der folgenden Funktionen voraus:

* [Adobe Experience Platform Privacy Service](../home.md): Bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie Zugriffs- und Löschanfragen Ihrer Datensubjekte (Kunden) in allen Adobe Experience Cloud-Anwendungen verwalten können.

## Sammeln von Werten für erforderliche Kopfzeilen

Um die Privacy Service-API aufrufen zu können, müssen Sie zunächst Ihre Zugriffsberechtigungen erfassen, damit sie in den erforderlichen Kopfzeilen verwendet werden können:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Dazu gehört das Abrufen von Entwicklerberechtigungen für Adobe Experience Platform in Adobe Admin Console und das anschließende Generieren der Anmeldeinformationen in der Adobe Developer Console.

### Erhalten von Entwicklerzugriff auf Experience Platform

So erhalten Sie Entwicklerzugriff auf [!DNL Platform]Führen Sie die ersten Schritte im Abschnitt [Tutorial zur Experience Platform-Authentifizierung](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de). Sobald Sie den Schritt &quot;Zugangsdaten in der Adobe Developer Console generieren&quot;erreicht haben, kehren Sie zu diesem Tutorial zurück, um die spezifischen Anmeldeinformationen für Privacy Service zu generieren.

### Generieren von Zugriffsberechtigungen

Mithilfe der Adobe-Entwicklerkonsole müssen Sie die folgenden drei Zugriffsberechtigungen generieren:

* `{ORG_ID}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Ihre `{ORG_ID}` und `{API_KEY}` muss nur einmal generiert werden und kann in zukünftigen API-Aufrufen wiederverwendet werden. Allerdings muss Ihre `{ACCESS_TOKEN}` ist temporär und muss alle 24 Stunden neu generiert werden.

Die Schritte zum Generieren dieser Werte werden im Folgenden detailliert beschrieben.

#### Einmalige Einrichtung

Wechseln Sie zur [Adobe-Entwicklerkonsole](https://www.adobe.com/go/devs_console_ui) und melden Sie sich mit Ihrer Adobe ID an. Führen Sie anschließend die Schritte aus, die im Tutorial [Erstellen eines leeren Projekts](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in der Dokumentation zu Adobe Developer Console beschrieben werden.

Nachdem Sie ein neues Projekt erstellt haben, wählen Sie **[!UICONTROL API hinzufügen]** auf **[!UICONTROL Projektübersicht]** angezeigt.

![](../images/api/getting-started/add-api-button.png)

Der Bildschirm **[!UICONTROL API hinzufügen]** wird angezeigt. Auswählen **[!UICONTROL Privacy Service-API]** aus der Liste der verfügbaren APIs, bevor Sie **[!UICONTROL Nächste]**.

![](../images/api/getting-started/add-privacy-service-api.png)

Die **[!UICONTROL API konfigurieren]** angezeigt. Wählen Sie die zu **[!UICONTROL Generieren eines Schlüsselpaars]**, wählen Sie **[!UICONTROL Generieren von keypair]** unten rechts.

![](../images/api/getting-started/generate-key-pair.png)

Das Schlüsselpaar wird automatisch generiert und eine ZIP-Datei mit einem privaten Schlüssel und einem öffentlichen Zertifikat wird auf Ihren lokalen Computer heruntergeladen (um in einem späteren Schritt verwendet zu werden). Auswählen **[!UICONTROL Konfigurierte API speichern]** , um die Konfiguration abzuschließen.

![](../images/api/getting-started/key-pair-generated.png)

Nachdem die API zum Projekt hinzugefügt wurde, wird die Projektseite erneut auf der **Übersicht über die Privacy Service-API** Seite. Scrollen Sie von hier nach unten zum **[!UICONTROL Dienstkonto (JWT)]** -Abschnitt, der die folgenden Zugriffsberechtigungen bereitstellt, die für alle Aufrufe der Privacy Service-API erforderlich sind:

* **[!UICONTROL CLIENT-ID]**: Die Client-ID ist die erforderliche `{API_KEY}` für muss in der x-api-key -Kopfzeile angegeben werden.
* **[!UICONTROL ORGANISATIONS-ID]**: Die Organisations-ID ist die `{ORG_ID}` -Wert, der im Header x-gw-ims-org-id verwendet werden muss.

![](../images/api/getting-started/jwt-credentials.png)

#### Authentifizierung für jede Sitzung

Die letzte erforderliche Berechtigung, die Sie erfassen müssen, ist Ihre `{ACCESS_TOKEN}`, der in der Autorisierungskopfzeile verwendet wird. Im Gegensatz zu den Werten für `{API_KEY}` und `{ORG_ID}`muss ein neues Token alle 24 Stunden generiert werden, damit Sie weiterhin [!DNL Platform] APIs.

So generieren Sie eine neue `{ACCESS_TOKEN}`, öffnen Sie den zuvor heruntergeladenen privaten Schlüssel und fügen Sie seinen Inhalt in das Textfeld neben **[!UICONTROL Zugriffstoken generieren]** vor der Auswahl **[!UICONTROL Generate Token]**.

![](../images/api/getting-started/paste-private-key.png)

Es wird ein neues Zugriffs-Token generiert und eine Schaltfläche zum Kopieren des Tokens in die Zwischenablage bereitgestellt. Dieser Wert wird für die erforderliche Autorisierungskopfzeile verwendet und muss im Format angegeben werden `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/api-guide.md#sample-api) in den Ersten Schritten für Platform-APIs.

## Nächste Schritte

Nachdem Sie nun wissen, welche Kopfzeilen zu verwenden sind, können Sie erste Aufrufe an die Privacy Service-API stellen. Wählen Sie eine der Endpunktleitfäden für die ersten Schritte aus:

* [Datenschutzaufträge](./privacy-jobs.md)
* [Einverständnis](./consent.md)
