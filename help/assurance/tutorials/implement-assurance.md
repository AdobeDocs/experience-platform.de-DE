---
title: Implementieren der Adobe Experience Platform Assurance-Erweiterung
description: In diesem Handbuch wird erläutert, wie Sie die Adobe Experience Platform Assurance-Erweiterung implementieren und installieren.
exl-id: b7bd1bb1-1606-4d00-97e0-c329c86d8ca4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 2%

---

# Implementieren der Adobe Experience Platform Assurance-Erweiterung

In diesem Tutorial erfahren Sie, wie Sie die Platform Assurance-Erweiterung im Mobile SDK installieren und implementieren. Anweisungen zum Hinzufügen der Assurance-Erweiterung zu Ihrer Anwendung finden Sie im Abschnitt [Übersicht über die Adobe Experience Platform Assurance-Erweiterung](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## Erste Schritte

Um die Assurance-Erweiterung zu installieren und zu implementieren, benötigen Sie Zugriff auf die folgenden Dienste:

- Die [Adobe Experience Platform-Datenerfassungs-Benutzeroberfläche](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

## Erstellen einer mobilen Eigenschaft

>[!NOTE]
>
>Wenn Sie bereits über eine Eigenschaft für Mobilgeräte verfügen, können Sie mit dem nächsten Schritt fortfahren.

Wählen Sie in der Datenerfassungs-Benutzeroberfläche die Option **[!UICONTROL Tags]**. Es wird eine Liste mit mobilen und Web-Eigenschaften mit Informationen zu den Eigenschaften angezeigt, die zu Ihrem Unternehmen gehören. Auswählen **[!UICONTROL Neue Eigenschaft]** , um eine neue Eigenschaft zu erstellen.

![Die Schaltfläche &quot;Neue Eigenschaft&quot;ist hervorgehoben und zeigt an, was Sie zum Erstellen einer neuen Eigenschaft auswählen](./images/implement-assurance/create-new-property.png)

Die **[!UICONTROL Eigenschaft erstellen]** angezeigt. Geben Sie den Namen für die neue Eigenschaft ein und wählen Sie **[!UICONTROL Mobile]** als Ihre Plattform. Nachdem Sie Ihre Details eingefügt haben, wählen Sie **[!UICONTROL Speichern]** , um die Eigenschaft für Mobilgeräte zu erstellen.

>[!NOTE]
>
>Die Eigenschaft für Mobilgeräte **[!UICONTROL Datenschutz]** Einstellung **not** sich auf die Datenerfassung von Assurance auswirken.

![Die Seite Eigenschaft erstellen wird angezeigt. Hier können Sie Informationen zu Ihrer mobilen Eigenschaft einfügen.](./images/implement-assurance/create-property.png)

## Installieren der Assurance-Erweiterung

Wählen Sie die mobile Eigenschaft aus, in der Sie die Assurance-Erweiterung installieren möchten.

![Die Seite Tag-Eigenschaften wird angezeigt, wobei die ausgewählte Eigenschaft für Mobilgeräte hervorgehoben ist.](./images/implement-assurance/select-mobile-property.png)

Die **Mobile-Eigenschaftendetails** angezeigt. Auswählen **[!UICONTROL Erweiterungen]** , um eine Liste der Erweiterungen anzuzeigen, die derzeit mit Ihrer mobilen Eigenschaft verknüpft sind.

![Die Detailseite für die mobile Eigenschaft wird angezeigt. Es werden Informationen zu den letzten Aktivitäten angezeigt. Die Registerkarte Erweiterungen wird hervorgehoben.](./images/implement-assurance/tag-properties.png)

Auswählen **[!UICONTROL Katalog]** , um eine Liste der Erweiterungen anzuzeigen, die Sie zur Eigenschaft für Mobilgeräte hinzufügen können. Suchen Sie mithilfe des Filters die **[!UICONTROL AEP Assurance]** Erweiterung und wählen Sie **[!UICONTROL Installieren]**.

![Der Erweiterungskatalog wird angezeigt. Die Erweiterung &quot;Assurance&quot;wird gefiltert und angezeigt, wobei die Schaltfläche &quot;Installieren&quot;hervorgehoben ist.](./images/implement-assurance/assurance-extension.png)

## Nächste Schritte

Nachdem Sie die Assurance-Erweiterung in Ihrer mobilen Eigenschaft installiert haben, können Sie mit der Verwendung von Assurance in Ihren Anwendungen beginnen. Informationen zum Hinzufügen der Assurance-Erweiterung zu Ihrer Anwendung finden Sie im Abschnitt [Übersicht über die Adobe Experience Platform Assurance-Erweiterung](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). Informationen zur Verwendung von Assurance finden Sie im Abschnitt [Verwenden des Assurance-Handbuchs](./using-assurance.md).
