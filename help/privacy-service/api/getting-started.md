---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Entwicklerhandbuch für Privacy Service
description: Verwenden Sie die RESTful-API, um die personenbezogenen Daten Ihrer Datensubjekte in allen Adobe Experience Cloud-Anwendungen zu verwalten.
topic: developer guide
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 25%

---


# [!DNL Privacy Service] Entwicklerhandbuch

Adobe Experience Platform [!DNL Privacy Service] provides a RESTful API and user interface that allow you to manage (access and delete) the personal data of your data subjects (customers) across Adobe Experience Cloud applications. [!DNL Privacy Service] bietet außerdem einen zentralen Audit- und Protokollierungsmechanismus, mit dem Sie auf den Status und die Ergebnisse von Aufträgen zugreifen können, an denen [!DNL Experience Cloud] Anwendungen beteiligt sind.

This guide covers how to use the [!DNL Privacy Service] API. Weitere Informationen zur Verwendung der Benutzeroberfläche finden Sie in der [Übersicht über die Privacy Service-Benutzeroberfläche](../ui/overview.md). For a comprehensive list of all available endpoints in the [!DNL Privacy Service] API, please see the [API reference](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html).

## Erste Schritte {#getting-started}

This guide requires a working understanding the following [!DNL Experience Platform] features:

* [!DNL Privacy Service](../home.md): Bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie die Zugriffs- und Löschanfragen Ihrer Datensubjekte (Kunden) in allen Adobe Experience Cloud-Anwendungen verwalten können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Schema Privacy Service-API erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dabei wird auf Pfade ebenso eingegangen wie auf die erforderlichen Kopfzeilen und die für Anfrage-Payloads zu verwendende Formatierung. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Die in der Dokumentation zu Beispielen für API-Aufrufe verwendeten Konventionen werden im Handbuch zur Fehlerbehebung für unter [Lesehilfe für Beispiel-API-Aufrufe](../../landing/troubleshooting.md) erläutert.[!DNL Experience Platform]

## Werte der zu verwendenden Kopfzeilen

Um die [!DNL Privacy Service] API aufrufen zu können, müssen Sie zunächst Ihre Zugriffsberechtigungen erfassen, um in den erforderlichen Kopfzeilen verwendet werden zu können:

* Authorization: Bearer `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Hierzu gehört das Abrufen von Entwicklerberechtigungen für [!DNL Experience Platform] die Adobe-Admin Console und das Generieren der Anmeldeinformationen in Adobe Developer Console.

### Entwicklerzugriff erhalten [!DNL Experience Platform]

Um Entwicklern Zugriff auf [!DNL Platform]zu erhalten, führen Sie die ersten Schritte im Tutorial zur [Experience Platform-Authentifizierung durch](../../tutorials/authentication.md). Sobald Sie den Schritt &quot;Anmeldeinformationen für den Zugriff in der Adobe Developer Console erstellen&quot;erreicht haben, kehren Sie zu diesem Lernprogramm zurück, um die spezifischen Anmeldeinformationen für [!DNL Privacy Service]dieses Lernprogramm zu generieren.

### Zugriffsberechtigungen generieren

Mit Adobe Developer Console müssen Sie die folgenden drei Zugriffsberechtigungen generieren:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Ihre `{IMS_ORG}` und `{API_KEY}` nur einmal generiert werden müssen und können in zukünftigen API-Aufrufen wiederverwendet werden. Ihre `{ACCESS_TOKEN}` Daten sind jedoch nur vorübergehend und müssen alle 24 Stunden neu generiert werden.

Die Schritte zum Generieren dieser Werte werden nachfolgend detailliert beschrieben.

#### Einmalige Einrichtung

Go to [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) and sign in with your Adobe ID. Führen Sie anschließend die Schritte aus, die im Lernprogramm zum [Erstellen eines leeren Projekts](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in der Dokumentation zur Adobe Developer Console beschrieben sind.

Nachdem Sie ein neues Projekt erstellt haben, klicken Sie im Bildschirm &quot; **[!UICONTROL Projektübersicht]** &quot;auf _[!UICONTROL Hinzufügen API]_.

![](../images/api/getting-started/add-api-button.png)

Der _[!UICONTROL Hinzufügen eines API]_-Bildschirms wird angezeigt. Wählen Sie**[!UICONTROL  Privacy Service-API ]**aus der Liste der verfügbaren APIs, bevor Sie auf**[!UICONTROL  Weiter ]**klicken.

![](../images/api/getting-started/add-privacy-service-api.png)

Der Bildschirm _[!UICONTROL API]_konfigurieren wird angezeigt. Wählen Sie die Option zum**[!UICONTROL  Generieren eines Schlüsselpaars ]**aus und klicken Sie dann unten rechts auf**[!UICONTROL  Generate keypair ]**.

![](../images/api/getting-started/generate-key-pair.png)

Das Schlüsselpaar wird automatisch generiert und eine ZIP-Datei mit einem privaten Schlüssel und einem öffentlichen Zertifikat wird auf Ihren lokalen Computer heruntergeladen (in einem späteren Schritt zu verwenden). Wählen Sie Konfigurierte API **[!UICONTROL speichern]** , um die Konfiguration abzuschließen.

![](../images/api/getting-started/key-pair-generated.png)

Nachdem die API zum Projekt hinzugefügt wurde, wird die Projektseite auf der Übersichtsseite zur _Privacy Service-API_ erneut angezeigt. Blättern Sie von hier nach unten zum Abschnitt _[!UICONTROL Dienstkonto (JWT)]_, der die folgenden Zugriffsberechtigungen bereitstellt, die für alle Aufrufe der[!DNL Privacy Service]API erforderlich sind:

* **[!UICONTROL CLIENT-ID]**: Die Client-ID ist die erforderliche `{API_KEY}` für die Bereitstellung im X-API-Schlüssel-Header.
* **[!UICONTROL Organisations-ID]**: Die Organisations-ID ist der `{IMS_ORG}` Wert, der im Header x-gw-ims-org-id verwendet werden muss.

![](../images/api/getting-started/jwt-credentials.png)

#### Authentifizierung für jede Sitzung

Die letzte erforderliche Berechtigung, die Sie erfassen müssen, ist Ihre `{ACCESS_TOKEN}`, die im Autorisierungs-Header verwendet wird. Im Gegensatz zu den Werten für `{API_KEY}` und `{IMS_ORG}`muss alle 24 Stunden ein neues Token generiert werden, um weiterhin mit [!DNL Platform] APIs arbeiten zu können.

Um einen neuen zu generieren, öffnen Sie `{ACCESS_TOKEN}`den zuvor heruntergeladenen privaten Schlüssel und fügen Sie den Inhalt in das Textfeld neben _[!UICONTROL Zugriffstoken]_erstellen ein, bevor Sie auf Token**[!UICONTROL  generieren ]**klicken.

![](../images/api/getting-started/paste-private-key.png)

Es wird ein neues Zugriffstoken generiert und eine Schaltfläche zum Kopieren des Tokens in die Zwischenablage bereitgestellt. Dieser Wert wird für den erforderlichen Autorisierungs-Header verwendet und muss im Format angegeben werden `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Nächste Schritte

Now that you understand what headers to use, you are ready to begin making calls to the [!DNL Privacy Service] API. The document on [privacy jobs](privacy-jobs.md) walks through the various API calls you can make using the [!DNL Privacy Service] API. Jeder Beispielaufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.
