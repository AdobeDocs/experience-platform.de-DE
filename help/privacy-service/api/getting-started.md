---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Handbuch zur Privacy Service-API
description: Die Privacy Service-API ermöglicht es Entwicklern, Kundenanfragen zu erstellen und zu verwalten, um in allen Experience Cloud-Anwendungen auf ihre personenbezogenen Daten zuzugreifen oder sie zu löschen. Dabei gelten die gesetzlichen Datenschutzbestimmungen. In diesem Handbuch erfahren Sie, wie Sie wichtige Vorgänge mit der API durchführen.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
translation-type: tm+mt
source-git-commit: e226990fc84926587308077b32b128bfe334e812
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 21%

---

# [!DNL Privacy Service] API-Handbuch

Adobe Experience Platform [!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie die personenbezogenen Daten Ihrer betroffenen Personen (Kunden) in Adobe Experience Cloud-Anwendungen verwalten (aufrufen und löschen) können. [!DNL Privacy Service] bietet außerdem einen zentralen Audit- und Protokollierungsmechanismus, mit dem Sie auf den Status und die Ergebnisse von Aufträgen zugreifen können, die  [!DNL Experience Cloud] Anwendungen betreffen.

In diesem Handbuch wird die Verwendung der [!DNL Privacy Service]-API behandelt. Weitere Informationen zur Verwendung der Benutzeroberfläche finden Sie in der [Übersicht über die Privacy Service-Benutzeroberfläche](../ui/overview.md). Eine umfassende Liste aller verfügbaren Endpunkte in der [!DNL Privacy Service]-API finden Sie unter [API-Referenz](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml).

## Erste Schritte {#getting-started}

Dieses Handbuch erfordert ein Verständnis der folgenden [!DNL Experience Platform]-Funktionen:

* [[!DNL Privacy Service]](../home.md): Bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie die Zugriffs- und Löschanfragen Ihrer Datensubjekte (Kunden) in allen Adobe Experience Cloud-Anwendungen verwalten können.

Die folgenden Abschnitte enthalten zusätzliche Informationen, die Sie benötigen, um die Privacy Service-API erfolgreich aufrufen zu können.

### Lesen von Beispiel-API-Aufrufen

In diesem Tutorial wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md) im Fehlerbehebungshandbuch für [!DNL Experience Platform]

## Sammeln von Werten für erforderliche Kopfzeilen

Um Aufrufe an die [!DNL Privacy Service]-API durchzuführen, müssen Sie zunächst Ihre Zugriffsberechtigungen erfassen, um in den erforderlichen Headern verwendet werden zu können:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Hierzu gehört das Abrufen von Entwicklerberechtigungen für [!DNL Experience Platform] in Adobe Admin Console und das Generieren der Anmeldeinformationen in Adobe Developer Console.

### Zugriff für Entwickler auf [!DNL Experience Platform]

Um Entwicklern Zugriff auf [!DNL Platform] zu gewähren, führen Sie die ersten Schritte im [Tutorial zur Experience Platform-Authentifizierung](https://www.adobe.com/go/platform-api-authentication-en) durch. Sobald Sie den Schritt &quot;Anmeldeinformationen für den Zugriff in der Adobe Developer Console erstellen&quot;erreicht haben, kehren Sie zu diesem Lernprogramm zurück, um die spezifischen Anmeldeinformationen für [!DNL Privacy Service] zu generieren.

### Zugriffsberechtigungen generieren

Mit der Adobe Developer Console müssen Sie die folgenden drei Zugriffsberechtigungen generieren:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Ihre `{IMS_ORG}` und `{API_KEY}` müssen nur einmal generiert werden und können in zukünftigen API-Aufrufen wiederverwendet werden. Ihr `{ACCESS_TOKEN}` ist jedoch temporär und muss alle 24 Stunden neu generiert werden.

Die Schritte zum Generieren dieser Werte werden nachfolgend detailliert beschrieben.

#### Einmalige Einrichtung

Wechseln Sie zu [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui_de) und melden Sie sich bei Ihrem Adobe ID an. Führen Sie anschließend die Schritte aus, die im Lernprogramm [Erstellen eines leeren Projekts](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) in der Adobe Developer Console-Dokumentation beschrieben werden.

Nachdem Sie ein neues Projekt erstellt haben, wählen Sie im Bildschirm **[!UICONTROL Projektübersicht]** die Option **[!UICONTROL Hinzufügen-API]**.

![](../images/api/getting-started/add-api-button.png)

Der Bildschirm **[!UICONTROL Hinzufügen eine API]** wird angezeigt. Wählen Sie **[!UICONTROL Privacy Service-API]** aus der Liste der verfügbaren APIs, bevor Sie **[!UICONTROL Weiter]** auswählen.

![](../images/api/getting-started/add-privacy-service-api.png)

Der Bildschirm **[!UICONTROL API konfigurieren]** wird angezeigt. Wählen Sie die Option **[!UICONTROL Generate a key pair]** und wählen Sie **[!UICONTROL Generate keypair]** in der unteren rechten Ecke.

![](../images/api/getting-started/generate-key-pair.png)

Das Schlüsselpaar wird automatisch generiert und eine ZIP-Datei mit einem privaten Schlüssel und einem öffentlichen Zertifikat wird auf Ihren lokalen Computer heruntergeladen (in einem späteren Schritt zu verwenden). Wählen Sie **[!UICONTROL Konfigurierte API speichern]**, um die Konfiguration abzuschließen.

![](../images/api/getting-started/key-pair-generated.png)

Nachdem die API zum Projekt hinzugefügt wurde, wird die Projektseite auf der Seite **Übersicht über die Privacy Service-API** erneut angezeigt. Blättern Sie von hier nach unten zum Abschnitt **[!UICONTROL Dienstkonto (JWT)]**, der die folgenden Zugriffsberechtigungen bereitstellt, die für alle Aufrufe der [!DNL Privacy Service]-API erforderlich sind:

* **[!UICONTROL CLIENT-ID]**: Die Client-ID ist die  `{API_KEY}` dafür erforderliche Client-ID, die im Header x-api-key angegeben werden muss.
* **[!UICONTROL Organisations-ID]**: Die Organisations-ID ist der  `{IMS_ORG}` Wert, der im Header x-gw-ims-org-id verwendet werden muss.

![](../images/api/getting-started/jwt-credentials.png)

#### Authentifizierung für jede Sitzung

Die letzte erforderliche Berechtigung, die Sie erfassen müssen, ist Ihr `{ACCESS_TOKEN}`, das im Autorisierungs-Header verwendet wird. Im Gegensatz zu den Werten für `{API_KEY}` und `{IMS_ORG}` muss alle 24 Stunden ein neues Token generiert werden, um weiterhin [!DNL Platform]-APIs verwenden zu können.

Um ein neues `{ACCESS_TOKEN}` zu erstellen, öffnen Sie den zuvor heruntergeladenen privaten Schlüssel und fügen Sie den Inhalt in das Textfeld neben **[!UICONTROL Zugriffstoken]** ein, bevor Sie **[!UICONTROL Token generieren]** auswählen.

![](../images/api/getting-started/paste-private-key.png)

Es wird ein neues Zugriffstoken generiert und eine Schaltfläche zum Kopieren des Tokens in die Zwischenablage bereitgestellt. Dieser Wert wird für den erforderlichen Autorisierungs-Header verwendet und muss im Format `Bearer {ACCESS_TOKEN}` angegeben werden.

![](../images/api/getting-started/generated-access-token.png)

## Nächste Schritte

Nachdem Sie wissen, welche Header verwendet werden sollen, können Sie mit dem Aufrufen der [!DNL Privacy Service]-API beginnen. Das Dokument zu [Datenschutzaufträgen](privacy-jobs.md) führt durch die verschiedenen API-Aufrufe, die Sie mit der [!DNL Privacy Service]-API durchführen können. Jeder Beispielaufruf enthält das allgemeine API-Format, eine Beispielanfrage mit den erforderlichen Kopfzeilen und eine Beispielantwort.
