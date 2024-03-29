---
title: Audit Query API-Anleitung
description: Audit Query ist eine RESTful-API, mit der Entwickler sehen können, wer welche Aktionen in Adobe Experience Platform durchgeführt hat.
exl-id: 9ed291c6-ff8b-4d9b-9fed-d1e3fa8f92fb
source-git-commit: c2c5778e0a3fff7f488ad7a672123c813cca59f1
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 9%

---

# [!DNL Audit Query]-API-Handbuch

Die [!DNL Audit Query] API bietet Endpunkte, mit denen Sie Ereignisdaten programmgesteuert für verschiedene Adobe Experience Platform-Funktionen abrufen und überwachen können. Die Endpunkte sind unten dargestellt. Besuchen Sie die [Erste Schritte](./getting-started.md) für wichtige Informationen zu erforderlichen Kopfzeilen, zum Lesen von Beispiel-API-Aufrufen und mehr.

Um alle verfügbaren Endpunkte und CRUD-Vorgänge zu sehen, besuchen Sie den [[!DNL Audit Query] API-Swagger](https://www.adobe.io/experience-platform-apis/references/audit-query/).

## Ereignisse

Audit-Ereignisse bieten Einblicke in Benutzeraktionen in Platform, einschließlich Aktionstyp, Datum und Uhrzeit, E-Mail-ID des Benutzers, der die Aktion ausgeführt hat, und zusätzlichen Attributen, die für den Aktionstyp für verschiedene Funktionen in Adobe Experience Platform relevant sind. Informationen zum Abrufen von Metriken mithilfe der API finden Sie unter [Handbuch zum Ereignisendpunkt](./events.md).

## Exportieren

Mit dem Audit-Export können Sie Ereignisdaten abrufen, indem Sie die Ereignisse angeben, die Sie in der Payload abrufen möchten. Informationen zum Abrufen von Metriken mithilfe der API finden Sie unter [Export-Endpunkthandbuch](./export.md).
