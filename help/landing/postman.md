---
keywords: Experience Platform; Startseite; beliebte Themen; Adobe Experience Platform; API-Handbuch; Plattform-API-Handbuch; Einführung in die Plattform; Entwicklerhandbuch
solution: Experience Platform
title: Postman in Adobe Experience Platform
description: In diesem Dokument wird beschrieben, wie Sie eine Postman-Umgebung einrichten, Postman-Sammlungen importieren und für jeden Platform-Dienst eine Liste der verfügbaren Sammlungen anzeigen.
role: Developer
feature: API
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 0%

---

# Postman in Adobe Experience Platform

Postman ist eine Kooperationsplattform für die API-Entwicklung, mit der Sie Umgebungen mit vordefinierten Variablen einrichten, API-Sammlungen freigeben, CRUD-Anforderungen optimieren und vieles mehr. Die meisten Platform-API-Dienste verfügen über Postman-Sammlungen, die beim Ausführen von API-Aufrufen verwendet werden können.

## Einrichten einer Postman-Umgebung für Experience Platform

Im folgenden Videohandbuch wird die Erstellung und Einrichtung Ihrer Postman-Umgebung beschrieben. Eine Postman-Umgebung enthält alle erforderlichen Kopfzeilen, die Sie zum Ausführen von API-Aufrufen für die verschiedenen Kollektionen benötigen, die unten bereitgestellt werden. Nach der Einrichtung können Sie bei jedem Ablauf eines Werts (z. B. &quot;`ACCESS_TOKEN`&quot;) den aktuellen Wert in der Umgebung aktualisieren. Dieser neue Wert wird für alle Sammlungen verwendet.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Postman-Sammlungen {#collections}

Einen Ordner mit allen verfügbaren Postman-Sammlungen finden Sie unter dem GitHub-Repository ](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform) mit den Beispielen für die Experience Platform Postman. [ Alternativ kann in jeder einzelnen Swagger-Datei in der [API-Referenzdokumentation](https://www.adobe.com/go/platform-api-reference-en) auf Adobe I/O ein Postman-Sammlungslink gefunden werden.

Um eine Postman-Sammlung herunterzuladen, wählen Sie auf der GitHub-Seite die Option &quot;**[!DNL Raw]**&quot;, um die JSON-Rohdatei in eine neue Registerkarte zu laden. Klicken Sie dann mit der rechten Maustaste und wählen Sie **[!DNL Save as]** aus, um die Datei an einem lokalen Ziel Ihrer Wahl zu speichern.

![raw JSON](./images/api-guide/raw-collection.PNG)

## Importieren einer Postman-Sammlung {#import}

Um eine [Postman-Sammlung](#collections) verwenden zu können, muss eine Umgebung eingerichtet sein. Nachdem Sie die Umgebungseinrichtung abgeschlossen haben, wählen Sie oben rechts den Selektor **[!DNL Manage Environments]** aus.

![Verwalten des Umgebungs-Selektors](./images/api-guide/environment-selector.png)

Ein Popup-Fenster wird angezeigt und zeigt alle Ihre aktuellen Umgebungen an. Um eine Sammlung zu importieren, wählen Sie **[!DNL import]** aus.

![Importschaltfläche](./images/api-guide/import-collection.png)

Sie werden aufgefordert, eine zu importierende Datei auszuwählen. Wählen Sie die zu importierende Postman-Erfassungsdatei aus. Nach der Auswahl wird die Sammlung in der linken Leiste auf der Registerkarte Sammlungen angezeigt.

![befüllte Sammlung](./images/api-guide/imported-collection.png)

Jede Sammlung verfügt über verschiedene Schlüssel-Wert-Paare, die für die Durchführung eines erfolgreichen CRUD-Vorgangs erforderlich sein können. Weitere Informationen zu erforderlichen Werten, Tipps und Beispiele finden Sie im [API-Entwicklerhandbuch des Dienstes](api-guide.md#api-guides) .

Weitere Informationen zur Postman-Benutzeroberfläche und den verfügbaren Funktionen finden Sie in der [Postman-Dokumentation](https://learning.postman.com/docs/getting-started/navigating-postman/) .

### Zugriffstoken mit Postman für Nicht-Produktionsumgebungen generieren

>[!WARNING]
>
>Wie in der Postman-Sammlung von Identity Management Service (IMS) angegeben, sind die angegebenen Generierungsmethoden für die Verwendung von **Nicht-Produktionsumgebungen** geeignet. Beim lokalen Signieren wird eine JavaScript-Bibliothek von einem Drittanbieter-Host geladen. Beim Remote-Signieren wird der private Schlüssel an einen Webdienst gesendet, der im Besitz von Adobe ist und von diesem betrieben wird. Während Adobe diesen privaten Schlüssel nicht speichert, sollten Produktionsschlüssel niemals für andere freigegeben werden.

Im folgenden Video wird die Postman-Sammlung [Identity Management-Dienst (IMS)](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) verwendet, die aus dem öffentlichen GitHub-Repository heruntergeladen werden kann.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Nächste Schritte

In diesem Dokument wurden Postman-Umgebungen, Sammlungen und das Importieren von Sammlungen vorgestellt. Nachdem Sie Postman fertig sind, finden Sie im Leitfaden [Erste Schritte für die Plattform](api-guide.md) Informationen zu erforderlichen Kopfzeilen und Beispielen sowie eine Liste mit [API-Handbüchern](api-guide.md#api-guides), die für jeden Platform-Dienst verfügbar sind.
