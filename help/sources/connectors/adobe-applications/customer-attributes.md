---
keywords: Experience Platform;home;popular topics;Customer Attributes Connector
solution: Experience Platform
title: Übersicht über den Quell-Connector für Kundenattribute
description: Erfahren Sie, wie Sie mithilfe von APIs oder der Benutzeroberfläche Kundenattribute mit Adobe Experience Platform verbinden.
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 19%

---

# Kundenattribut-Connector

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=de) in Experience Cloud ermöglicht Ihnen das Hochladen Ihrer erfassten Unternehmensdaten aus einer CRM-Datenbank (Customer Relationship Management). Sie können die Daten in eine Datenquelle für Kundenattribute in Experience Cloud hochladen und dann die Daten in Adobe Analytics und Adobe Target verwenden.

Experience Platform unterstützt die Aufnahme [!DNL Customer Attributes] Profildaten in Adobe Experience Platform.

## Datensätze und Schemata

Die [!DNL Customer Attributes] -Quelle erstellt automatisch den Datensatz, in den Daten landen sollen. Dieser automatisch erstellte Datensatz ist fest und kann nicht manuell ausgewählt werden. Die Quelle erstellt außerdem automatisch das Schema für den Datensatz basierend auf der Eingabedatenquelle. Dieser Prozess umfasst auch die automatische Erstellung der erforderlichen Zuordnungen zwischen dem Schema und den Quelldaten.

## Identitäten

Die primäre Identität eines Datensatzes ist in der ersten Spalte der CSV-Datei der Quelldaten enthalten. Die [!DNL Customer Attributes] -Quelle geht davon aus, dass die Identität immer der [`CORE` namespace](../../../identity-service/features/namespaces.md), ein systemgenerierter Namespace, der von [[!DNL Identity Service]](../../../identity-service/home.md).

Bei Verwendung von [!DNL Customer Attributes] -Quelle [!DNL Customer Attributes] geht davon aus, dass sich die primäre Identität für das Schema immer in der Identitätszuordnung befindet. [!DNL Customer Attributes] erstellt dann die automatisierte Zuordnung der Quell-ID zur Identitätszuordnungs-UUID.

Für [!DNL Customer Attributes] Daten, die mit anderen verknüpft werden [!DNL Profile] -Datensätze, ihre Daten und Identitäten müssen mit einer Experience Cloud-ID abgeglichen werden können.

Sie können `CORE` Namespace durch Festlegen der Experience Cloud-ID für den Besucher mithilfe von [Web SDK](/help/web-sdk/identity/overview.md), [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/)oder die [Experience Cloud ID-Dienst-API](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de).

Die [!DNL Customer Attributes] -Datei füllt keine anderen Identitätsbeziehungen weiter. Beispiel: Wenn ein [!DNL Customer Attributes] Quelldatensatz enthält einen **Email** und **Treueprogramm-ID** eingeben, müssen diese Felder im Schema als Identitätsfelder gekennzeichnet werden, damit sie in [!DNL Identity Service].

Siehe Tutorial zu [Erstellen einer [!DNL Customer Attributes] Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/adobe-applications/customer-attributes.md) für weitere Informationen.
