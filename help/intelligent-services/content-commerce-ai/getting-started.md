---
keywords: Experience Platform;getting started;content ai;commerce ai;content and commerce ai
solution: Experience Platform
title: Erste Schritte mit der Content and Commerce-API
topic: Getting started
description: Content and Commerce AI verwendet Adobe I/O APIs. Um Aufrufe an Adobe I/O-APIs und die I/O-Konsolenintegration durchzuführen, müssen Sie zunächst das Authentifizierungslehrgang abschließen.
translation-type: tm+mt
source-git-commit: 2be04547b96e1a6c293cc63e782fe1b3259619ba
workflow-type: tm+mt
source-wordcount: '576'
ht-degree: 12%

---


# Erste Schritte mit Content- und Commerce-API

>[!NOTE]
>
>Die AI für Inhalte und Commerce befindet sich in der Betaphase. Die Dokumentation kann geändert werden.

[!DNL Content and Commerce AI] verwendet Adobe I/O-APIs. Um Aufrufe an Adobe I/O-APIs und die I/O-Konsolenintegration durchzuführen, müssen Sie zunächst das [Authentifizierungslehrgang](../../tutorials/authentication.md)abschließen.

Wenn Sie jedoch zum Schritt **Hinzufügen API** gelangen, befindet sich die API unter Experience Cloud anstelle von Adobe Experience Platform, wie im folgenden Screenshot gezeigt:

![Hinzufügen von Content- und Commerce-API](./images/add-api.png)

Wenn Sie das Authentifizierungstraining abschließen, werden die Werte für die einzelnen erforderlichen Header in allen Adobe I/O API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {IMS_ORG}`

## Erstellen einer Postman-Umgebung (optional)

Nachdem Sie Ihr Projekt und Ihre API in der Adobe Developer Console eingerichtet haben, können Sie eine Umgebung für Postman herunterladen. Wählen Sie in der linken Leiste Ihres Projekts unter **[!UICONTROL APIs]** die Option **[!UICONTROL Content and Commerce AI]**. Eine neue Registerkarte mit einer Karte mit der Bezeichnung &quot;[!DNL Try it out]&quot;wird geöffnet. Wählen Sie &quot; **Download für Postman** &quot;, um eine JSON-Datei herunterzuladen, die zur Konfiguration Ihrer Postman-Umgebung verwendet wird.

![download for postman](./images/add-to-postman.png)

Nachdem Sie die Datei heruntergeladen haben, öffnen Sie Postman und wählen Sie das **Zahnradsymbol** oben rechts, um das Dialogfeld &quot;Umgebung **verwalten** &quot;zu öffnen.

![Zahnradsymbol](./images/select-gear-icon.png)

Wählen Sie anschließend im Dialogfeld &quot;Umgebung **verwalten&quot;die Option &quot;** Importieren **&quot;** .

![import](./images/import.png)

Sie werden umgeleitet und aufgefordert, eine Umgebung auf Ihrem Computer auszuwählen. Wählen Sie die zuvor heruntergeladene JSON-Datei aus und klicken Sie dann auf **Öffnen** , um die Umgebung zu laden.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Sie werden zurück zur Registerkarte &quot;Umgebung ** verwalten&quot;mit einem neuen Umgebung-Namen geleitet. Wählen Sie den Namen der zu Ansicht Umgebung aus und bearbeiten Sie die in Postman verfügbaren Variablen. Sie müssen weiterhin manuell die Felder `JWT_TOKEN` und `ACCESS_TOKEN`ausfüllen. Diese Werte sollten beim Abschluss des [Authentifizierungslehrgangs](../../tutorials/authentication.md)abgerufen werden.

![](./images/re-direct.png)

Nach Abschluss sollten Ihre Variablen etwa wie im folgenden Screenshot aussehen. Wählen Sie **Aktualisieren** , um die Einrichtung der Umgebung abzuschließen.

![](./images/final-environment.png)

Sie können Ihre Umgebung jetzt im Dropdown-Menü oben rechts auswählen und alle gespeicherten Werte automatisch ausfüllen. Bearbeiten Sie die Werte einfach jederzeit neu, um alle Ihre API-Aufrufe zu aktualisieren.

![example](./images/select-environment.png)

Weitere Informationen zum Arbeiten mit Adobe I/O-APIs mit Postman finden Sie im Beitrag &quot;Mittel&quot;zur [Verwendung von Postman für die JWT-Authentifizierung unter Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md) im Handbuch zur Fehlerbehebung für Experience Platform.

## Nächste Schritte {#next-steps}

Sobald Sie alle Ihre Anmeldeinformationen haben, können Sie einen benutzerdefinierten Worker für [!DNL Content and Commerce AI]die Die folgenden Dokumente helfen Ihnen beim Verständnis des Erweiterungs-Frameworks und der Umgebung-Einrichtung.

Um mehr über das Erweiterungs-Framework zu erfahren, lesen Sie den Beginn in der [Einführung zum Dokument Erweiterbarkeit](https://docs.adobe.com/content/help/en/asset-compute/using/extend/understand-extensibility.html) . In diesem Dokument werden die Voraussetzungen und Bereitstellungsanforderungen erläutert.

Weitere Informationen zum Einrichten einer Umgebung für [!DNL Content and Commerce AI]finden Sie im Beginn im Handbuch zum [Einrichten einer Entwickler-Umgebung](https://docs.adobe.com/content/help/en/asset-compute/using/extend/setup-environment.html). Dieses Dokument enthält Setupanweisungen, die Ihnen die Entwicklung für den Asset compute-Dienst ermöglichen.