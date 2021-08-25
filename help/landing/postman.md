---
keywords: Experience Platform; Startseite; beliebte Themen; Adobe Experience Platform; API-Handbuch; Plattform-API-Handbuch; Einführung in die Plattform; Entwicklerhandbuch
solution: Experience Platform
title: Postman in Adobe Experience Platform
topic-legacy: api guide
description: Dieses Dokument enthält Schritte zum Einrichten einer Postman-Umgebung, zum Importieren von Postman-Sammlungen und eine Liste der verfügbaren Sammlungen für jeden Platform-Dienst.
exl-id: a09b3875-97f5-47f1-a562-52decbce67b1
source-git-commit: a0f4e49192a54075ce7c48620c9729e61ecdfdac
workflow-type: tm+mt
source-wordcount: '550'
ht-degree: 1%

---

# Postman in Adobe Experience Platform

Postman ist eine Kooperationsplattform für die API-Entwicklung, mit der Sie Umgebungen mit vordefinierten Variablen einrichten, API-Sammlungen freigeben, CRUD-Anforderungen optimieren und vieles mehr. Die meisten Platform-API-Dienste verfügen über Postman-Sammlungen, die beim Ausführen von API-Aufrufen verwendet werden können.

## Einrichten einer Postman-Umgebung für die Experience Platform

Im folgenden Video-Handbuch wird das Erstellen und Einrichten Ihrer Postman-Umgebung beschrieben. Eine Postman-Umgebung enthält alle erforderlichen Kopfzeilen, die Sie zum Ausführen von API-Aufrufen für die verschiedenen Sammlungen im Folgenden angeben müssen. Nach der Einrichtung können Sie bei jedem Ablauf eines Werts (z. B. `ACCESS_TOKEN`) den aktuellen Wert in der Umgebung aktualisieren. Dieser neue Wert wird für alle Sammlungen verwendet.

>[!VIDEO](https://video.tv.adobe.com/v/28832)

## Postman-Sammlungen {#collections}

Einen Ordner mit allen verfügbaren Postman-Sammlungen finden Sie unter [Experience Platform Postman samples GitHub-Repository](https://github.com/adobe/experience-platform-postman-samples/tree/master/apis/experience-platform). Alternativ kann in jeder einzelnen Swagger-Datei in der [API-Referenzdokumentation](https://www.adobe.com/go/platform-api-reference-en) auf der Adobe I/O ein Postman-Sammlungslink gefunden werden.

Um eine Postman-Sammlung herunterzuladen, wählen Sie **[!DNL Raw]** auf der GitHub-Seite aus, um die JSON-Rohdatei in eine neue Registerkarte zu laden. Klicken Sie dann mit der rechten Maustaste und wählen Sie **[!DNL Save as]** aus, um die Datei an einem lokalen Ziel Ihrer Wahl zu speichern.

![Raw-JSON](./images/api-guide/raw-collection.PNG)

## Importieren einer Postman-Sammlung {#import}

Um eine [Postman-Sammlung](#collections) verwenden zu können, müssen Sie eine Umgebung einrichten. Nachdem Sie die Umgebungseinrichtung abgeschlossen haben, wählen Sie den Selektor **[!DNL Manage Environments]** in der oberen rechten Ecke aus.

![Umgebungsauswahl verwalten](./images/api-guide/environment-selector.png)

Ein Popup-Fenster wird angezeigt und zeigt alle Ihre aktuellen Umgebungen an. Um eine Sammlung zu importieren, wählen Sie **[!DNL import]** aus.

![Importschaltfläche](./images/api-guide/import-collection.png)

Sie werden aufgefordert, eine zu importierende Datei auszuwählen. Wählen Sie die Postman-Kollektionsdatei aus, die Sie importieren möchten. Nach der Auswahl wird die Sammlung in der linken Leiste auf der Registerkarte Sammlungen angezeigt.

![befüllte Sammlung](./images/api-guide/imported-collection.png)

Jede Sammlung verfügt über verschiedene Schlüssel-Wert-Paare, die für die Durchführung eines erfolgreichen CRUD-Vorgangs erforderlich sein können. Lesen Sie das [API-Entwicklerhandbuch](api-guide.md#api-guides) des Diensts, um mehr über erforderliche Werte, Tipps und Beispiele zu erfahren.

Weitere Informationen zur Postman-Benutzeroberfläche und den verfügbaren Funktionen finden Sie in der [Postman-Dokumentation](https://learning.postman.com/docs/getting-started/navigating-postman/).

### Generieren eines Zugriffstokens mit Postman zur Nicht-Produktions-Verwendung

>[!WARNING]
>
>Wie in der Postman-Sammlung der Adobe I/O-Zugriffstoken-Generierung angegeben, sind die angegebenen Generierungsmethoden für **Nicht-Produktions-Verwendung** geeignet. Beim lokalen Signieren wird eine JavaScript-Bibliothek von einem Drittanbieter-Host geladen. Beim Remote-Signieren wird der private Schlüssel an einen Webdienst gesendet, der sich im Besitz von Adobe befindet und von diesem betrieben wird. Während Adobe diesen privaten Schlüssel nicht speichert, sollten Produktionsschlüssel nie für andere freigegeben werden.

Im folgenden Video wird die [Erfassung des Zugriffstokens für Adoben I/O](https://github.com/adobe/experience-platform-postman-samples/blob/master/apis/ims/Adobe%20IO%20Access%20Token%20Generation.postman_collection.json) verwendet, die vom öffentlichen GitHub-Repository heruntergeladen werden kann.

>[!VIDEO](https://video.tv.adobe.com/v/29698/?quality=12&learn=on)

## Nächste Schritte

In diesem Dokument wurden Postman-Umgebungen, Sammlungen und das Importieren von Sammlungen vorgestellt. Nachdem Sie Postman fertig sind, finden Sie im Leitfaden [Erste Schritte für die Plattform](api-guide.md) Informationen zu erforderlichen Kopfzeilen, Beispielen und einer Liste der [API-Handbücher](api-guide.md#api-guides), die für jeden Platform-Dienst verfügbar sind.
