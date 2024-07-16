---
keywords: Experience Platform;home;popular topics;Customer Attributes Connector
solution: Experience Platform
title: Übersicht über Kundenattribute in Source Connector
description: Erfahren Sie, wie Sie mithilfe von APIs oder der Benutzeroberfläche Kundenattribute mit Adobe Experience Platform verbinden.
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 19%

---

# Kundenattribut-Connector

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Mit [[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html) in Experience Cloud können Sie Ihre erfassten Unternehmensdaten aus einer CRM-Datenbank (Customer Relationship Management) hochladen. Sie können die Daten in eine Datenquelle für Kundenattribute in Experience Cloud hochladen und dann die Daten in Adobe Analytics und Adobe Target verwenden.

Experience Platform unterstützt die Aufnahme von [!DNL Customer Attributes] -Profildaten in Adobe Experience Platform.

## Datensätze und Schemata

Die Quelle [!DNL Customer Attributes] erstellt automatisch den Datensatz, in den Daten landen sollen. Dieser automatisch erstellte Datensatz ist fest und kann nicht manuell ausgewählt werden. Die Quelle erstellt außerdem automatisch das Schema für den Datensatz basierend auf der Eingabedatenquelle. Dieser Prozess umfasst auch die automatische Erstellung der erforderlichen Zuordnungen zwischen dem Schema und den Quelldaten.

## Identitäten

Die primäre Identität eines Datensatzes ist in der ersten Spalte der CSV-Datei der Quelldaten enthalten. Die Quelle [!DNL Customer Attributes] setzt voraus, dass die Identität immer dem Namespace [`CORE`](../../../identity-service/features/namespaces.md) zugeordnet ist, einem vom System generierten Namespace, der von [[!DNL Identity Service]](../../../identity-service/home.md) unterstützt wird.

Bei Verwendung der Quelle [!DNL Customer Attributes] können Sie keinen vorhandenen Namespace für die Identität auswählen, da [!DNL Customer Attributes] davon ausgeht, dass sich die primäre Identität für das Schema immer in der Identitätszuordnung befindet. [!DNL Customer Attributes] erstellt dann die automatisierte Zuordnung der Quell-ID zur Identitätszuordnungs-UUID.

Damit [!DNL Customer Attributes] -Daten mit anderen [!DNL Profile] -Datensätzen verknüpft werden, müssen ihre Daten und Identitäten mit einer Experience Cloud-ID abgeglichen werden können.

Sie können den Namespace `CORE` einrichten, indem Sie die Experience Cloud-ID für den Besucher mithilfe von [Web SDK](/help/web-sdk/identity/overview.md), [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/) oder der [Experience Cloud ID Service API](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de) festlegen.

Die Datei [!DNL Customer Attributes] füllt keine anderen Identitätsbeziehungen mehr. Wenn beispielsweise ein [!DNL Customer Attributes]-Quelldatensatz ein Feld **E-Mail** und ein Feld **Loyalitäts-ID** enthält, müssen diese Felder im Schema als Identitätsfelder gekennzeichnet werden, damit sie in [!DNL Identity Service] verarbeitet werden können.

Weitere Informationen finden Sie im Tutorial zum Erstellen einer  [!DNL Customer Attributes] Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/adobe-applications/customer-attributes.md) .[
