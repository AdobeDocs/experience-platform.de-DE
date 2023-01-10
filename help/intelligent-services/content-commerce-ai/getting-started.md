---
keywords: Experience Platform; Erste Schritte; Content-Hilfe; Commerce-API; Inhalts- und Commerce-API
solution: Experience Platform
title: Erste Schritte mit Content and Commerce AI
description: Die Inhalts- und Commerce-KI verwendet Adobe I/O-APIs. Um Adobe I/O-APIs und die I/O-Konsolenintegration aufzurufen, müssen Sie zunächst das Authentifizierungs-Tutorial abschließen.
exl-id: e7b0e9bb-a1f1-479c-9e9b-46991f2942e2
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 14%

---

# Erste Schritte mit Content and Commerce AI

>[!NOTE]
>
>Die KI für Inhalte und Commerce befindet sich in der Beta-Phase. Die Dokumentation kann sich ändern.

[!DNL Content and Commerce AI] verwendet Adobe I/O-APIs. Um Adobe I/O-APIs und die I/O-Konsolenintegration aufzurufen, müssen Sie zunächst die [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de).

Wenn Sie jedoch zum **API hinzufügen** -Schritt, befindet sich die API unter Experience Cloud anstelle von Adobe Experience Platform, wie im folgenden Screenshot gezeigt:

![Hinzufügen von Inhalts- und Commerce-KI](./images/add-api.png)

Durch Abschluss des Authentifizierungs-Tutorials werden die Werte für die einzelnen erforderlichen Kopfzeilen in allen Adobe I/O API-Aufrufen bereitgestellt, wie unten dargestellt:

- `Authorization: Bearer {ACCESS_TOKEN}`
- `x-api-key: {API_KEY}`
- `x-gw-ims-org-id: {ORG_ID}`

## Erstellen einer Postman-Umgebung (optional)

Nachdem Sie Ihr Projekt und Ihre API in der Adobe Developer Console eingerichtet haben, können Sie eine Umgebungsdatei für Postman herunterladen. under **[!UICONTROL APIs]** Wählen Sie in der linken Leiste Ihres Projekts die Option **[!UICONTROL Inhalts- und Commerce-KI]**. Eine neue Registerkarte wird geöffnet, die eine Karte mit der Bezeichnung &quot;[!DNL Try it out]&quot;. Auswählen **Herunterladen für Postman** um eine JSON-Datei herunterzuladen, die zur Konfiguration Ihrer Postman-Umgebung verwendet wird.

![Download für Postman](./images/add-to-postman.png)

Nachdem Sie die Datei heruntergeladen haben, öffnen Sie Postman und wählen Sie die **Zahnradsymbol** oben rechts, um die **Umgebungen** angezeigt.

![Zahnradsymbol](./images/select-gear-icon.png)

Wählen Sie als Nächstes **Import** innerhalb von **Umgebungen verwalten** angezeigt.

![importieren](./images/import.png)

Sie werden umgeleitet und aufgefordert, eine Umgebungsdatei von Ihrem Computer auszuwählen. Wählen Sie die zuvor heruntergeladene JSON-Datei aus und klicken Sie auf **Öffnen** , um die Umgebung zu laden.

![](./images/choose-your-file.png)

![](./images/click-open.png)

Sie werden zurück zum *Umgebungen verwalten* mit einem neuen Umgebungsnamen. Wählen Sie den Umgebungsnamen aus, um die in Postman verfügbaren Variablen anzuzeigen und zu bearbeiten. Sie müssen die `JWT_TOKEN` und `ACCESS_TOKEN`. Diese Werte sollten beim Abschließen der [Authentifizierungs-Tutorial](https://experienceleague.adobe.com/docs/experience-platform/landing/platform-apis/api-authentication.html?lang=de).

![](./images/re-direct.png)

Nach dem Abschluss sollten Ihre Variablen ungefähr wie im Screenshot unten dargestellt aussehen. Auswählen **Aktualisieren** , um die Einrichtung Ihrer Umgebung abzuschließen.

![](./images/final-environment.png)

Jetzt können Sie Ihre Umgebung aus dem Dropdown-Menü oben rechts auswählen und alle gespeicherten Werte automatisch ausfüllen. Bearbeiten Sie die Werte einfach jederzeit neu, um alle Ihre API-Aufrufe zu aktualisieren.

![Beispiel](./images/select-environment.png)

Weitere Informationen zum Arbeiten mit Adobe I/O-APIs mit Postman finden Sie im Beitrag Medium unter [Verwenden von Postman für die JWT-Authentifizierung bei Adobe I/O](https://medium.com/adobetech/using-postman-for-jwt-authentication-on-adobe-i-o-7573428ffe7f).

## Lesen von Beispiel-API-Aufrufen

In diesem Handbuch wird anhand von Beispielen für API-Aufrufe die korrekte Formatierung von Anfragen aufgezeigt. Dazu gehören Pfade, erforderliche Kopfzeilen und ordnungsgemäß formatierte Anfrage-Payloads. Außerdem wird ein Beispiel für eine von der API im JSON-Format zurückgegebene Antwort bereitgestellt. Informationen zu den Konventionen, die in der Dokumentation für Beispiel-API-Aufrufe verwendet werden, finden Sie im Abschnitt zum [Lesen von Beispiel-API-Aufrufen](../../landing/troubleshooting.md) im Handbuch zur Fehlerbehebung für Experience Platform.

## Nächste Schritte {#next-steps}

Sobald Sie alle Ihre Anmeldedaten haben, können Sie einen benutzerdefinierten Worker für [!DNL Content and Commerce AI]. Die folgenden Dokumente helfen Ihnen beim Verständnis des Erweiterungs-Frameworks und der Umgebungseinrichtung.

Um mehr über das Erweiterungs-Framework zu erfahren, lesen Sie zunächst das [Einführung in die Erweiterbarkeit](https://experienceleague.adobe.com/docs/asset-compute/using/extend/understand-extensibility.html?lang=de) Dokument. In diesem Dokument werden die Voraussetzungen und Bereitstellungsanforderungen beschrieben.

Weitere Informationen zum Einrichten einer Umgebung für [!DNL Content and Commerce AI], lesen Sie zunächst das Handbuch für [Einrichten einer Entwicklungsumgebung](https://experienceleague.adobe.com/docs/asset-compute/using/extend/setup-environment.html). Dieses Dokument enthält Einrichtungsanweisungen, die die Entwicklung für den Asset compute-Service ermöglichen.
