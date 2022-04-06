---
keywords: Experience Platform; Startseite; beliebte Themen; Adobe Experience Platform; API-Handbuch; Plattform-API-Handbuch; Einführung in die Plattform; Entwicklerhandbuch
solution: Experience Platform
title: Postman in Adobe Experience Platform
topic-legacy: api guide
description: In diesem Dokument wird beschrieben, wie Sie eine Postman-Umgebung einrichten, Postman-Sammlungen importieren und für jeden Platform-Dienst eine Liste der verfügbaren Sammlungen anzeigen.
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: 9f00bff31f9e7d2da1294d3d1f24cba7870a4614
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 1%

---

# Postman in Adobe Experience Platform

Postman ist eine Kooperationsplattform für die API-Entwicklung, mit der Sie Umgebungen mit vordefinierten Variablen einrichten, API-Sammlungen freigeben, CRUD-Anforderungen optimieren und vieles mehr. Die meisten Platform-API-Dienste verfügen über Postman-Sammlungen, die beim Ausführen von API-Aufrufen verwendet werden können.

## Einrichten einer Postman-Umgebung für die Experience Platform

Im folgenden Videohandbuch wird die Erstellung und Einrichtung Ihrer Postman-Umgebung beschrieben. Eine Postman-Umgebung enthält alle erforderlichen Kopfzeilen, die Sie zum Ausführen von API-Aufrufen für die verschiedenen Kollektionen benötigen, die unten bereitgestellt werden. Sobald ein Wert eingerichtet ist, läuft er immer ab (z. B. `ACCESS_TOKEN`) können Sie den aktuellen Wert in der Umgebung aktualisieren. Dieser neue Wert wird für alle Ihre Sammlungen verwendet.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Postman-Sammlungen {#collections}

Einen Ordner mit allen verfügbaren Postman-Sammlungen finden Sie unter [Experience Platform Postman-Beispiele für GitHub-Repository](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Alternativ kann in jeder einzelnen Swagger-Datei im Abschnitt [API-Referenzdokumentation](https://www.adobe.com/go/platform-api-reference-en) auf Adobe I/O.

Um eine Postman-Sammlung herunterzuladen, wählen Sie **[!DNL Raw]** von der GitHub-Seite aus, um die JSON-Rohdatei in eine neue Registerkarte zu laden. Klicken Sie dann mit der rechten Maustaste und wählen Sie **[!DNL Save as]** , um die Datei an einem lokalen Ziel Ihrer Wahl zu speichern.

![Raw-JSON](./images/api-guide/raw-collection.PNG)

## Importieren einer Postman-Sammlung {#import}

Um eine [Postman-Sammlung](#collections)müssen Sie eine Umgebung einrichten. Nachdem Sie die Einrichtung der Umgebung abgeschlossen haben, wählen Sie die **[!DNL Manage Environments]** in der oberen rechten Ecke.

![Umgebungsauswahl verwalten](./images/api-guide/environment-selector.png)

Ein Popup-Fenster wird angezeigt und zeigt alle Ihre aktuellen Umgebungen an. Um eine Sammlung zu importieren, wählen Sie **[!DNL import]** .

![Importschaltfläche](./images/api-guide/import-collection.png)

Sie werden aufgefordert, eine zu importierende Datei auszuwählen. Wählen Sie die zu importierende Postman-Erfassungsdatei aus. Nach der Auswahl wird die Sammlung in der linken Leiste auf der Registerkarte Sammlungen angezeigt.

![befüllte Sammlung](./images/api-guide/imported-collection.png)

Jede Sammlung verfügt über verschiedene Schlüssel-Wert-Paare, die für die Durchführung eines erfolgreichen CRUD-Vorgangs erforderlich sein können. Bitte lesen Sie die [API-Entwicklerhandbuch](api-guide.md#api-guides) , um mehr über erforderliche Werte, Tipps und Beispiele zu erfahren.

Weitere Informationen zur Benutzeroberfläche von Postman und den verfügbaren Funktionen finden Sie unter [Postman-Dokumentation](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Zugriffstoken mit Postman für Nicht-Produktionsumgebungen generieren

>[!WARNING]
>
>Wie in der Postman-Sammlung zur Generierung von Adobe I/O-Zugriffstoken erwähnt, eignen sich die angegebenen Generierungsmethoden für **Verwendung ohne Produktion**. Beim lokalen Signieren wird eine JavaScript-Bibliothek von einem Drittanbieter-Host geladen. Beim Remote-Signieren wird der private Schlüssel an einen Webdienst gesendet, der sich im Besitz von Adobe befindet und von diesem betrieben wird. Während Adobe diesen privaten Schlüssel nicht speichert, sollten Produktionsschlüssel nie für andere freigegeben werden.

Das folgende Video verwendet die [Erfassung von Adobe I/O-Zugriffstoken](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Adobe%20IO%20Access%20Token%20Generation.postman_collection.json) die vom öffentlichen GitHub-Repository heruntergeladen werden können.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Nächste Schritte

In diesem Dokument wurden Postman-Umgebungen, Sammlungen und das Importieren von Sammlungen vorgestellt. Nachdem Sie Postman fertig sind, besuchen Sie die [Erste Schritte mit Platform](api-guide.md) für Informationen zu erforderlichen Kopfzeilen, Beispielen und einer Liste von [API-Handbücher](api-guide.md#api-guides) für jeden Platform-Dienst verfügbar sind.
