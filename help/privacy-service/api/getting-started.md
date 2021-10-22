---
title: Erste Schritte mit der Privacy Service-API
description: Erfahren Sie, wie Sie sich bei der Privacy Service-API authentifizieren und wie Sie Beispiel-API-Aufrufe in der Dokumentation interpretieren.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 6dcbf2df46ba35104abd9c4e6412799e77c9c49f
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 26%

---

# Erste Schritte mit der Privacy Service-API

Dieses Handbuch enthält eine Einführung in die Kernkonzepte, die Sie kennen müssen, bevor Sie Aufrufe der Privacy Service-API durchführen können.

## Voraussetzungen

Dieses Handbuch erfordert ein Verständnis der folgenden Funktionen:

* [Adobe Experience Platform Privacy Service](../home.md): Bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie Zugriff auf und Löschen von Anforderungen von Ihren Datensubjekten (Kunden) in allen Adobe Experience Cloud-Anwendungen verwalten können.

## Sammeln von Werten für erforderliche Kopfzeilen

Um Aufrufe der Privacy Service-API zu tätigen, müssen Sie zunächst Ihre Zugriffsberechtigungen erfassen, damit sie in den erforderlichen Kopfzeilen verwendet werden können:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Dazu gehört das Erlangen von Entwicklerberechtigungen für Adobe Experience Platform in Adobe Admin Console und das anschließende Generieren der Anmeldedaten in der Adobe Developer Console.

### Erhalten von Entwicklerzugriff auf Experience Platform

So erhalten Entwickler Zugriff auf [!DNL Platform]folgen Sie den ersten Schritten in [Tutorial zur Experience Platform-Authentifizierung](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis). Sobald Sie im Schritt &quot;Zugangsdaten in der Adobe Developer Console generieren&quot; ankommen, kehren Sie zu diesem Tutorial zurück, um die spezifischen Anmeldedaten für Privacy Service zu generieren.

### Generieren von Zugriffsberechtigungen

Mithilfe der Adobe-Entwicklerkonsole müssen Sie die folgenden drei Zugriffsberechtigungen generieren:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Ihre `{IMS_ORG}` und `{API_KEY}` nur einmal generiert werden und in zukünftigen API-Aufrufen wiederverwendet werden können. Allerdings `{ACCESS_TOKEN}` ist vorübergehend und muss alle 24 Stunden regeneriert werden.

Die Schritte zum Generieren dieser Werte werden im Folgenden detailliert beschrieben.

#### Einmalige Einrichtung

Wechseln Sie zur [Adobe-Entwicklerkonsole](https://www.adobe.com/go/devs_console_ui) und melden Sie sich mit Ihrer Adobe ID an. Führen Sie anschließend die Schritte aus, die im Tutorial [Erstellen eines leeren Projekts](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in der Dokumentation zu Adobe Developer Console beschrieben werden.

Sobald Sie ein neues Projekt erstellt haben, wählen Sie **[!UICONTROL hinzufügen-API]** zu **[!UICONTROL Projektübersicht]** Bildschirm.

![](../images/api/getting-started/add-api-button.png)

Der Bildschirm **[!UICONTROL API hinzufügen]** wird angezeigt. Auswählen **[!UICONTROL Privacy Service-API]** aus der Liste der verfügbaren APIs, bevor Sie **[!UICONTROL Weiter]**.

![](../images/api/getting-started/add-privacy-service-api.png)

Die **[!UICONTROL API konfigurieren]** angezeigt. Option auswählen, um **[!UICONTROL Schlüsselpaar erstellen]**, wählen Sie **[!UICONTROL Schlüsselbild generieren]** in der rechten unteren Ecke.

![](../images/api/getting-started/generate-key-pair.png)

Das Schlüsselpaar wird automatisch erstellt und eine ZIP-Datei mit einem privaten Schlüssel und einem öffentlichen Zertifikat wird auf Ihren lokalen Computer heruntergeladen (um in einem späteren Schritt verwendet zu werden). Auswählen **[!UICONTROL Konfigurierte API speichern]** , um die Konfiguration abzuschließen.

![](../images/api/getting-started/key-pair-generated.png)

Sobald die API dem Projekt hinzugefügt wurde, wird die Projektseite auf der **Übersicht über die Privacy Service-API** Seite. Von hier aus scrollen Sie nach unten zum **[!UICONTROL Dienstkonto (JWT)]** -Abschnitt, der die folgenden Zugriffsberechtigungen bereitstellt, die bei allen Aufrufen der Privacy Service-API erforderlich sind:

* **[!UICONTROL CLIENT-ID]**: Die Client-ID ist erforderlich. `{API_KEY}` dafür muss im x-api-key-Header angegeben werden.
* **[!UICONTROL ORGANISATIONS-ID]**: Die Organisations-ID ist die `{IMS_ORG}` Wert, der im x-gw-ims-org-id-Header verwendet werden muss.

![](../images/api/getting-started/jwt-credentials.png)

#### Authentifizierung für jede Sitzung

Die letzte erforderliche Berechtigung, die Sie sammeln müssen, ist Ihre `{ACCESS_TOKEN}`, das im Autorisierungskopfabschnitt verwendet wird. Im Gegensatz zu den Werten für `{API_KEY}` und `{IMS_ORG}`muss alle 24 Stunden ein neues Token erstellt werden, um weiterhin verwendet werden zu können [!DNL Platform] APIs.

So erstellen Sie ein neues `{ACCESS_TOKEN}`, öffnen Sie den zuvor heruntergeladenen privaten Schlüssel und fügen Sie den Inhalt in das Textfeld neben **[!UICONTROL Zugriffstoken erstellen]** vor Auswahl **[!UICONTROL Token generieren]**.

![](../images/api/getting-started/paste-private-key.png)

Es wird ein neues Zugriffs-Token generiert und eine Schaltfläche zum Kopieren des Tokens in die Zwischenablage bereitgestellt. Dieser Wert wird für den erforderlichen Autorisierungs-Header verwendet und muss im Format angegeben werden `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zu [Lesen von Beispiel-API-Aufrufen](../../landing/api-guide.md#sample-api) im Handbuch &quot;Erste Schritte&quot;für Plattform-APIs.

## Nächste Schritte

Nachdem Sie nun wissen, welche Kopfzeilen zu verwenden sind, können Sie erste Aufrufe an die Privacy Service-API stellen. Wählen Sie eine der Endpunkt-Hilfslinien, um zu beginnen:

* [Datenschutzaufträge](./privacy-jobs.md)
* [Einverständnis](./consent.md)
