---
keywords: Experience Platform;Startseite;beliebte Themen;Connector für Kundenattribute
solution: Experience Platform
title: Übersicht über den Source-Connector für Kundenattribute
description: Erfahren Sie, wie Sie Kundenattribute mithilfe von APIs oder der Benutzeroberfläche mit Adobe Experience Platform verbinden
exl-id: 63765ecd-ddb5-4992-a3de-d53f054bfb28
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 12%

---

# Connector für Kundenattribute

Adobe Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Programme, Cloud-basierte Datenspeicher und Datenbanken.

Mit der [[!DNL Customer Attributes]](https://experienceleague.adobe.com/docs/core-services/interface/services/customer-attributes/attributes.html?lang=de) in Experience Cloud können Sie Ihre erfassten Unternehmensdaten aus einer CRM-Datenbank (Customer Relationship Management) hochladen. Sie können die Daten in eine Datenquelle für Kundenattribute in Experience Cloud hochladen und dann die Daten in Adobe Analytics und Adobe Target verwenden.

Experience Platform unterstützt die Aufnahme [!DNL Customer Attributes] Profildaten in Adobe Experience Platform.

## Datensätze und Schemata

Die [!DNL Customer Attributes] erstellt automatisch den Datensatz, in den die Daten aufgenommen werden sollen. Dieser automatisch erstellte Datensatz wurde korrigiert und kann nicht manuell ausgewählt werden. Die -Quelle erstellt außerdem automatisch das Schema für den Datensatz basierend auf der Eingabedatenquelle. Dieser Prozess umfasst auch die automatische Erstellung der erforderlichen Zuordnungen zwischen dem Schema und den Quelldaten.

## Identitäten

Die primäre Identität eines Datensatzes ist in der ersten Spalte der CSV-Datei der Quelldaten enthalten. Die [!DNL Customer Attributes]-Quelle geht davon aus, dass die Identität immer dem [`CORE`-Namespace zugeordnet &#x200B;](../../../identity-service/features/namespaces.md), einem systemgenerierten Namespace, der von [[!DNL Identity Service]](../../../identity-service/home.md) unterstützt wird.

Bei Verwendung [!DNL Customer Attributes] Quelle können Sie keinen vorhandenen Namespace für die Identität auswählen, da [!DNL Customer Attributes] davon ausgeht, dass sich die primäre Identität für das Schema immer in der Identitätszuordnung befindet. [!DNL Customer Attributes] erstellt dann automatisch die Zuordnung der Quell-ID zur Identitätszuordnungs-UUID.

Damit [!DNL Customer Attributes] Daten mit anderen [!DNL Profile]-Datensätzen verknüpft werden können, müssen ihre Daten und Identitäten mit einer Experience Cloud ID abgeglichen werden können.

Sie können den `CORE`-Namespace einrichten, indem Sie die Experience Cloud-ID für den Besucher mithilfe von [Web SDK](/help/web-sdk/identity/overview.md), [Mobile SDK](https://developer.adobe.com/client-sdks/documentation/mobile-core/identity/) oder der [Experience Cloud ID Service-API &#x200B;](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=de).

Die [!DNL Customer Attributes]-Datei füllt keine anderen Identitätsbeziehungen weiter. Wenn beispielsweise ein [!DNL Customer Attributes] Quelldatensatz ein **E-Mail**- und ein **Treueprogramm-ID**-Feld enthält, müssen diese Felder als Identitätsfelder im Schema gekennzeichnet werden, damit sie in [!DNL Identity Service] verarbeitet werden können.

Weitere Informationen finden Sie im Tutorial [Erstellen  [!DNL Customer Attributes]  Quellverbindung in &#x200B;](../../tutorials/ui/create/adobe-applications/customer-attributes.md) Benutzeroberfläche“.
