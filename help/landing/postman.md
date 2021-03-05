---
keywords: Experience Platform;Home;beliebte Themen;Adobe Experience Platform;API-Handbuch;Plattform-API-Handbuch;Einführung in die Plattform;Entwicklerhandbuch
solution: Experience Platform
title: Postman in Adobe Experience Platform
topic: API-Handbuch
description: In diesem Dokument wird beschrieben, wie Sie eine Postman-Umgebung einrichten, Postman-Sammlungen importieren und eine Liste der verfügbaren Sammlungen für jeden Plattformdienst erstellen.
translation-type: tm+mt
source-git-commit: effc8fef666ffbf62c2e0874d048245f19c12111
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 0%

---


# Postman in Adobe Experience Platform

Postman ist eine Kooperationsplattform für die API-Entwicklung, mit der Sie Umgebung mit voreingestellten Variablen einrichten, API-Sammlungen freigeben, CRUD-Anforderungen optimieren und mehr. Die meisten Plattform-API-Dienste verfügen über Postman-Sammlungen, mit denen API-Aufrufe durchgeführt werden können.

## Einrichten einer Postman-Umgebung für Experience Platformen

Im folgenden Videoleitfaden wird das Erstellen und Einrichten Ihrer Postman-Umgebung beschrieben. Eine Postman-Umgebung enthält alle erforderlichen Kopfzeilen, die Sie zum Aufrufen der API für die verschiedenen Sammlungen unten angeben müssen. Nach der Einrichtung können Sie jederzeit, wenn ein Wert abläuft (z. B. ein `ACCESS_TOKEN`), den aktuellen Wert in der Umgebung aktualisieren. Dieser neue Wert wird in allen Sammlungen verwendet.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Postman-Sammlungen {#collections}

Ein Ordner, der alle verfügbaren Postman-Sammlungen enthält, finden Sie unter [Experience Platform Postman samples GitHub repository](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Alternativ kann in jeder einzelnen Swagger-Datei in der [API-Referenzdokumentation](http://www.adobe.com/go/platform-api-reference-en) auf der Adobe I/O ein Postman-Sammlungslink gefunden werden.

Um eine Postman-Sammlung herunterzuladen, wählen Sie **[!DNL Raw]** auf der GitHub-Seite, um die JSON-Rohdatei in eine neue Registerkarte zu laden. Klicken Sie dann mit der rechten Maustaste und wählen Sie **[!DNL Save as]**, um die Datei an einem lokalen Ziel Ihrer Wahl zu speichern.

![raw JSON](./images/api-guide/raw-collection.PNG)

## Importieren einer Postman-Sammlung {#import}

Um eine [Postman-Sammlung](#collections) verwenden zu können, müssen Sie eine Umgebung einrichten. Nachdem Sie die Umgebung eingerichtet haben, wählen Sie in der rechten oberen Ecke die Auswahl **[!DNL Manage Environments]** aus.

![Auswahl für Umgebung verwalten](./images/api-guide/environment-selector.png)

Es wird ein Popup angezeigt, in dem alle aktuellen Umgebung angezeigt werden. Um eine Sammlung zu importieren, wählen Sie **[!DNL import]** aus.

![Schaltfläche importieren](./images/api-guide/import-collection.png)

Sie werden aufgefordert, eine zu importierende Datei auszuwählen. Wählen Sie die Postman-Sammlungsdatei aus, die Sie importieren möchten. Nach der Auswahl wird die Sammlung in der linken Leiste unter der Registerkarte &quot;Sammlungen&quot;angezeigt.

![gefüllte Sammlung](./images/api-guide/imported-collection.png)

Jede Sammlung verfügt über verschiedene Schlüssel/Wert-Paare, die für einen erfolgreichen CRUD-Vorgang erforderlich sein können. Bitte lesen Sie das [API-Entwicklerhandbuch](api-guide.md#api-guides) des Dienstes, um mehr über erforderliche Werte, Tipps und Beispiele zu erfahren.

Weitere Informationen zur Postman-Benutzeroberfläche und ihren verfügbaren Funktionen finden Sie in der [Postman-Dokumentation](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Erstellen Sie ein Zugriffstoken mit Postman für die Verwendung ohne Produktionscharakter

>[!WARNING]
>
>Wie in der Postman-Sammlung zur Adobe I/O-Zugriffstoken-Generierung angegeben, sind die angegebenen Generierungsmethoden für **Nicht-Produktions-Verwendung** geeignet. Beim lokalen Signieren wird eine JavaScript-Bibliothek von einem Drittanbieter-Host geladen, und durch das Fernsignieren wird der private Schlüssel an einen Webdienst gesendet, der sich im Besitz der Adobe befindet und von dieser betrieben wird. Während Adobe diesen privaten Schlüssel nicht speichert, sollten Produktionsschlüssel niemals für andere freigegeben werden.

Das folgende Video verwendet die Generierungssammlung [Adobe I/O-Zugriffstoken](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Adobe%20IO%20Access%20Token%20Generation.postman_collection.json), die aus dem öffentlichen GitHub-Repository heruntergeladen werden kann.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Nächste Schritte

In diesem Dokument wurden Umgebung, Sammlungen und das Importieren von Sammlungen in Postman vorgestellt. Sobald Sie Postman bereit haben, finden Sie im Handbuch [Plattformstart](api-guide.md) Informationen zu erforderlichen Kopfzeilen, Beispielen und einer Liste der [API-Handbücher](api-guide.md#api-guides), die für jeden Plattformdienst verfügbar sind.