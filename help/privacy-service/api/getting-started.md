---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Handbuch zur Privacy Service-API
description: Die Privacy Service-API ermöglicht es Entwicklern, Kundenanfragen für den Zugriff auf oder die Löschung ihrer personenbezogenen Daten in allen Experience Cloud-Applikationen gemäß den gesetzlichen Datenschutzbestimmungen zu erstellen und zu verwalten. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 33%

---

# [!DNL Privacy Service]-API-Handbuch

Adobe Experience Platform [!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie die personenbezogenen Daten Ihrer Datensubjekte (Kunden) in allen Adobe Experience Cloud-Anwendungen verwalten (aufrufen und löschen) können. [!DNL Privacy Service] bietet außerdem einen zentralen Prüfungs- und Protokollierungsmechanismus, mit dem Sie auf den Status und die Ergebnisse von Vorgängen zugreifen können, die  [!DNL Experience Cloud] Anwendungen betreffen.

In diesem Handbuch wird die Verwendung der API [!DNL Privacy Service] beschrieben. Weitere Informationen zur Verwendung der Benutzeroberfläche finden Sie in der [Übersicht über die Privacy Service-Benutzeroberfläche](../ui/overview.md). Eine umfassende Liste aller verfügbaren Endpunkte in der [!DNL Privacy Service]-API finden Sie in der [API-Referenz](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Erste Schritte {#getting-started}

Dieses Handbuch setzt ein Verständnis der folgenden [!DNL Experience Platform]-Funktionen voraus:

* [[!DNL Privacy Service]](../home.md): Bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie die Zugriffs- und Löschanfragen Ihrer Datensubjekte (Kunden) in allen Adobe Experience Cloud-Anwendungen verwalten können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Privacy Service-API erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md) im Handbuch zur Fehlerbehebung für [!DNL Experience Platform]

## Sammeln von Werten für erforderliche Kopfzeilen

Um die [!DNL Privacy Service]-API aufrufen zu können, müssen Sie zunächst Ihre Zugriffsberechtigungen erfassen, um in den erforderlichen Kopfzeilen verwendet zu werden:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Dazu gehört das Abrufen von Entwicklerberechtigungen für [!DNL Experience Platform] in der Adobe Admin Console und das anschließende Generieren der Anmeldeinformationen in der Adobe Developer Console.

### Entwicklerzugriff auf [!DNL Experience Platform]

Um Entwicklerzugriff auf [!DNL Platform] zu erhalten, führen Sie die ersten Schritte im [Tutorial zur Experience Platform-Authentifizierung](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de#platform-apis) aus. Sobald Sie den Schritt &quot;Anmeldeinformationen für den Zugriff in der Adobe Developer Console generieren&quot;erreicht haben, kehren Sie zu diesem Tutorial zurück, um die spezifischen Anmeldeinformationen für [!DNL Privacy Service] zu generieren.

### Generieren von Zugriffsberechtigungen

Mithilfe der Adobe-Entwicklerkonsole müssen Sie die folgenden drei Zugriffsberechtigungen generieren:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Ihre `{IMS_ORG}` und `{API_KEY}` müssen nur einmal generiert werden und können in zukünftigen API-Aufrufen wiederverwendet werden. Ihr `{ACCESS_TOKEN}` ist jedoch temporär und muss alle 24 Stunden neu generiert werden.

Die Schritte zum Generieren dieser Werte werden im Folgenden detailliert beschrieben.

#### Einmalige Einrichtung

Wechseln Sie zur [Adobe-Entwicklerkonsole](https://www.adobe.com/go/devs_console_ui) und melden Sie sich mit Ihrer Adobe ID an. Führen Sie anschließend die im Tutorial [Erstellen eines leeren Projekts](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) beschriebenen Schritte in der Dokumentation zur Adobe Developer Console aus.

Nachdem Sie ein neues Projekt erstellt haben, wählen Sie **[!UICONTROL API]** hinzufügen im Bildschirm **[!UICONTROL Project Overview]** aus.

![](../images/api/getting-started/add-api-button.png)

Der Bildschirm **[!UICONTROL API hinzufügen]** wird angezeigt. Wählen Sie **[!UICONTROL Privacy Service-API]** aus der Liste der verfügbaren APIs, bevor Sie **[!UICONTROL Weiter]** auswählen.

![](../images/api/getting-started/add-privacy-service-api.png)

Der Bildschirm **[!UICONTROL API]** konfigurieren wird angezeigt. Wählen Sie die Option **[!UICONTROL Generate a key pair]** und wählen Sie dann **[!UICONTROL Generate keypair]** in der rechten unteren Ecke aus.

![](../images/api/getting-started/generate-key-pair.png)

Das Schlüsselpaar wird automatisch generiert und eine ZIP-Datei mit einem privaten Schlüssel und einem öffentlichen Zertifikat wird auf Ihren lokalen Computer heruntergeladen (um in einem späteren Schritt verwendet zu werden). Wählen Sie **[!UICONTROL Konfigurierte API]** speichern aus, um die Konfiguration abzuschließen.

![](../images/api/getting-started/key-pair-generated.png)

Nachdem die API zum Projekt hinzugefügt wurde, wird die Projektseite erneut auf der Seite **Übersicht über die Privacy Service-API** angezeigt. Scrollen Sie von hier nach unten zum Abschnitt **[!UICONTROL Dienstkonto (JWT)]** , der die folgenden Zugriffsberechtigungen bereitstellt, die für alle Aufrufe der [!DNL Privacy Service]-API erforderlich sind:

* **[!UICONTROL CLIENT-ID]**: Die Client-ID ist die  `{API_KEY}` dafür erforderliche Client-ID, die in der x-api-key-Kopfzeile angegeben werden muss.
* **[!UICONTROL ORGANISATIONS-ID]**: Die Organisations-ID ist der  `{IMS_ORG}` Wert, der im Header x-gw-ims-org-id verwendet werden muss.

![](../images/api/getting-started/jwt-credentials.png)

#### Authentifizierung für jede Sitzung

Die letzte erforderliche Berechtigung, die Sie erfassen müssen, ist Ihr `{ACCESS_TOKEN}`, der in der Autorisierungskopfzeile verwendet wird. Im Gegensatz zu den Werten für `{API_KEY}` und `{IMS_ORG}` muss alle 24 Stunden ein neues Token generiert werden, um weiterhin [!DNL Platform]-APIs zu verwenden.

Um einen neuen `{ACCESS_TOKEN}` zu generieren, öffnen Sie den zuvor heruntergeladenen privaten Schlüssel und fügen Sie seinen Inhalt in das Textfeld neben **[!UICONTROL Zugriffstoken generieren]** ein, bevor Sie **[!UICONTROL Token generieren]** auswählen.

![](../images/api/getting-started/paste-private-key.png)

Es wird ein neues Zugriffs-Token generiert und eine Schaltfläche zum Kopieren des Tokens in die Zwischenablage bereitgestellt. Dieser Wert wird für die erforderliche Autorisierungskopfzeile verwendet und muss im Format `Bearer {ACCESS_TOKEN}` angegeben werden.

![](../images/api/getting-started/generated-access-token.png)

## Nächste Schritte

Nachdem Sie nun wissen, welche Header verwendet werden sollen, können Sie mit Aufrufen an die [!DNL Privacy Service]-API beginnen. Das Dokument zu [Datenschutzaufträgen](privacy-jobs.md) führt durch die verschiedenen API-Aufrufe, die Sie mit der [!DNL Privacy Service]-API ausführen können. Jeder Beispielaufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.
