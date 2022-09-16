---
keywords: Experience Platform; Startseite; beliebte Themen; Kundenattribut-Connector
solution: Experience Platform
title: Übersicht über den Quell-Connector für Kundenattribute
topic-legacy: overview
description: Erfahren Sie, wie Sie mithilfe von APIs oder der Benutzeroberfläche Kundenattribute mit Adobe Experience Platform verbinden.
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: 541cc87f218a6ef3dcca37573f6d0f9cf560edfb
workflow-type: tm+mt
source-wordcount: '411'
ht-degree: 19%

---

# Kundenattribut-Connector

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet spezielle Services, mittels derer Sie eingehende Daten strukturieren, beschriften und erweitern können. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

[[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=en) in Experience Cloud können Sie Ihre erfassten Unternehmensdaten aus einer CRM-Datenbank (Customer Relationship Management) hochladen. Sie können die Daten in eine Datenquelle für Kundenattribute in Experience Cloud hochladen und dann die Daten in Adobe Analytics und Adobe Target verwenden.

Experience Platform unterstützt die Aufnahme von [!DNL Customer Attributes] Profildaten in Adobe Experience Platform.

## Datensätze und Schemata

Die [!DNL Customer Attributes] -Quelle erstellt automatisch den Datensatz, in den Daten landen sollen. Dieser automatisch erstellte Datensatz ist fest und kann nicht manuell ausgewählt werden. Die Quelle erstellt außerdem automatisch das Schema für den Datensatz basierend auf der Eingabedatenquelle. Dieser Prozess umfasst auch die automatische Erstellung der erforderlichen Zuordnungen zwischen dem Schema und den Quelldaten.

## Identitäten

Die primäre Identität eines Datensatzes ist in der ersten Spalte der CSV-Datei der Quelldaten enthalten. Die [!DNL Customer Attributes] -Quelle geht davon aus, dass die Identität immer der [`CORE` namespace](../../../identity-service/namespaces.md), ein systemgenerierter Namespace, der von [[!DNL Identity Service]](../../../identity-service/home.md).

Bei Verwendung von [!DNL Customer Attributes] -Quelle [!DNL Customer Attributes] geht davon aus, dass sich die primäre Identität für das Schema immer in der Identitätszuordnung befindet. [!DNL Customer Attributes] erstellt dann die automatisierte Zuordnung der Quell-ID zur Identitätszuordnungs-UUID.

Für [!DNL Customer Attributes] Daten, die mit anderen verknüpft werden sollen [!DNL Profile] -Datensätze, ihre Daten und Identitäten müssen mit einer Experience Cloud-ID abgeglichen werden können.

Sie können die `CORE` -Namespace durch Festlegen der Experience Cloud-ID für den Besucher mit [Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en), [Mobile SDK](https://aep-sdks.gitbook.io/docs/foundation-extensions/mobile-core/identity)oder [Experience Cloud-ID-Dienst-API](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de).

Die [!DNL Customer Attributes] -Datei füllt keine anderen Identitätsbeziehungen weiter. Wenn beispielsweise eine [!DNL Customer Attributes] Quelldatensatz enthält einen **Email** und **Treueprogramm-ID** eingeben, müssen diese Felder im Schema als Identitätsfelder gekennzeichnet werden, damit sie verarbeitet werden können [!DNL Identity Service].

Siehe Tutorial zu [Erstellen einer [!DNL Customer Attributes] Quellverbindung in der Benutzeroberfläche](../../tutorials/ui/create/adobe-applications/customer-attributes.md) für weitere Informationen.
