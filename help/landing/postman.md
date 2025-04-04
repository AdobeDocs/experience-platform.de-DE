---
keywords: Experience Platform;Startseite;beliebte Themen;Adobe Experience Platform;API-Handbuch;Platform-API-Handbuch;Einführung in Platform;Entwicklerhandbuch
solution: Experience Platform
title: Postman in Adobe Experience Platform
description: Dieses Dokument enthält Schritte zum Einrichten einer Postman-Umgebung, zum Importieren von Postman-Sammlungen und eine Liste der verfügbaren Sammlungen für jeden Experience Platform-Service.
role: Developer
feature: API
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '524'
ht-degree: 0%

---

# Postman in Adobe Experience Platform

Postman ist eine Kollaborationsplattform für die API-Entwicklung, mit der Sie Umgebungen mit voreingestellten Variablen einrichten, API-Sammlungen freigeben, CRUD-Anfragen optimieren und vieles mehr. Die meisten Experience Platform-API-Services verfügen über Postman-Sammlungen, die Sie bei API-Aufrufen unterstützen können.

## Einrichten einer Postman-Umgebung für Experience Platform

Im folgenden Video-Handbuch wird das Erstellen und Einrichten Ihrer Postman-Umgebung beschrieben. Eine Postman-Umgebung enthält alle erforderlichen Kopfzeilen, die Sie für API-Aufrufe an die verschiedenen unten bereitgestellten Sammlungen benötigen. Sobald eingerichtet, können Sie bei jedem Ablauf eines Werts (z. B. eines `ACCESS_TOKEN`) den aktuellen Wert in der Umgebung aktualisieren. Dieser neue Wert wird dann für alle Sammlungen verwendet.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Postman-Sammlungen {#collections}

Einen Ordner mit allen verfügbaren Postman-Sammlungen finden Sie, indem Sie das GitHub-Repository mit den [Experience Platform Postman-Beispielen besuchen](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Alternativ kann ein Sammlungs-Link für Postman in jeder einzelnen Swagger-Datei in der (API[Referenzdokumentation) ](https://www.adobe.com/go/platform-api-reference-en) Adobe I/O gefunden werden.

Um eine Postman-Sammlung herunterzuladen, wählen Sie auf der GitHub-Seite die Option **[!DNL Raw]** aus, um die rohe JSON-Datei in eine neue Registerkarte zu laden. Klicken Sie dann mit der rechten Maustaste und wählen Sie **[!DNL Save as]** , um die Datei an einem lokalen Ziel Ihrer Wahl zu speichern.

![Roh-JSON](./images/api-guide/raw-collection.PNG)

## Postman-Sammlung importieren {#import}

Um eine [Postman-Sammlung zu ](#collections), muss eine Umgebung eingerichtet sein. Nachdem Sie die Einrichtung der Umgebung abgeschlossen haben, wählen Sie oben rechts die **[!DNL Manage Environments]** aus.

![Umgebungsauswahl verwalten](./images/api-guide/environment-selector.png)

Ein Pop-up wird angezeigt, in dem alle Ihre aktuellen Umgebungen angezeigt werden. Um eine Sammlung zu importieren, wählen Sie **[!DNL import]** aus.

![Importschaltfläche](./images/api-guide/import-collection.png)

Sie werden aufgefordert, eine zu importierende Datei auszuwählen. Wählen Sie die Postman-Sammlungsdatei aus, die Sie importieren möchten. Nach der Auswahl wird die Sammlung in der linken Leiste auf der Registerkarte Sammlungen befüllt.

![Ausgefüllte Sammlung](./images/api-guide/imported-collection.png)

Jede Sammlung verfügt über verschiedene Schlüssel-Wert-Paare, die möglicherweise erforderlich sind, um einen erfolgreichen CRUD-Vorgang durchzuführen. Lesen Sie das API[Entwicklerhandbuch des Service, ](api-guide.md#api-guides) sich über die erforderlichen Werte und Tipps zu informieren und Beispiele anzuzeigen.

Weitere Informationen zur Postman-Benutzeroberfläche und ihren verfügbaren Funktionen finden Sie in der Dokumentation zu [Postman](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Erstellen eines Zugriffstokens mit Postman für produktionsfremde Zwecke

>[!WARNING]
>
>Wie in der Postman-Sammlung des Identity Management Service (IMS) erwähnt, sind die genannten Generierungsmethoden für **produktionsfremde Verwendung)**. Beim lokalen Signieren wird eine JavaScript-Bibliothek von einem Drittanbieterhost geladen, und beim Remote-Signieren wird der private Schlüssel an einen Webservice gesendet, der sich im Besitz von Adobe befindet und von diesem betrieben wird. Adobe speichert diesen privaten Schlüssel zwar nicht, aber die Produktionsschlüssel sollten niemals für andere freigegeben werden.

Im folgenden Video wird die Postman-Sammlung des [Identity Management-Services (IMS](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Identity%20Management%20Service.postman_collection.json) verwendet, die aus dem öffentlichen GitHub-Repository heruntergeladen werden kann.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Nächste Schritte

In diesem Dokument wurden Postman-Umgebungen, Sammlungen und das Importieren von Sammlungen vorgestellt. Nachdem Sie nun Postman bereit haben, finden Sie im Handbuch „Erste Schritte mit Experience Platform](api-guide.md) Informationen zu erforderlichen Kopfzeilen, Beispielen und einer Liste von [API-Handbüchern](api-guide.md#api-guides) die für jeden Experience Platform-Service verfügbar sind.[
