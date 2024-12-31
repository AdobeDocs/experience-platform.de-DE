---
title: Implementieren der Adobe Experience Platform Assurance-Erweiterung
description: In diesem Handbuch wird beschrieben, wie Sie die Adobe Experience Platform Assurance-Erweiterung implementieren und installieren.
exl-id: b7bd1bb1-1606-4d00-97e0-c329c86d8ca4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 1%

---

# Implementieren der Adobe Experience Platform Assurance-Erweiterung

In diesem Tutorial wird erläutert, wie Sie die Platform Assurance-Erweiterung in Mobile SDK installieren und implementieren. Anweisungen zum Hinzufügen der Assurance-Erweiterung zu Ihrem Programm finden Sie in der [Übersicht über die Adobe Experience Platform Assurance-Erweiterung](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## Erste Schritte

Um die Assurance-Erweiterung zu installieren und zu implementieren, benötigen Sie Zugriff auf die folgenden Services:

- Die Datenerfassungs-Benutzeroberfläche von [Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

## Erstellen einer Mobile-Eigenschaft

>[!NOTE]
>
>Wenn Sie bereits über eine Mobile-Eigenschaft verfügen, können Sie mit dem nächsten Schritt fortfahren.

Wählen Sie in der Datenerfassungs-UI **[!UICONTROL Tags]** aus. Eine Liste der Mobile- und Web-Eigenschaften wird mit Informationen zu den Eigenschaften angezeigt, die zu Ihrer Organisation gehören. Wählen Sie **[!UICONTROL Neue Eigenschaft]** aus, um eine neue Eigenschaft zu erstellen.

![Die Schaltfläche „Neue Eigenschaft“ ist hervorgehoben und zeigt an, was Sie zum Erstellen einer neuen Eigenschaft ausgewählt haben](./images/implement-assurance/create-new-property.png)

Die **[!UICONTROL Eigenschaft erstellen]** wird angezeigt. Geben Sie den Namen für Ihre neue Eigenschaft ein und wählen Sie **[!UICONTROL Mobile]** als Plattform aus. Klicken Sie nach dem Einfügen Ihrer Details auf **[!UICONTROL Speichern]**, um die Mobile-Eigenschaft zu erstellen.

>[!NOTE]
>
>Die Einstellung **[!UICONTROL Datenschutz]** der Mobile-Eigenschaft hat **keine** Auswirkungen auf die Datenerfassung von Assurance.

![Die Seite Eigenschaft erstellen wird angezeigt. Hier können Sie Informationen zu Ihrer mobilen Eigenschaft einfügen.](./images/implement-assurance/create-property.png)

## Installieren der Assurance-Erweiterung

Wählen Sie die Mobile-Eigenschaft aus, in der Sie die Assurance-Erweiterung installieren möchten.

![Die Seite mit den Tag-Eigenschaften wird angezeigt, wobei die ausgewählte Mobile-Eigenschaft hervorgehoben ist.](./images/implement-assurance/select-mobile-property.png)

Die **Mobile-Eigenschaftsdetails** wird angezeigt. Wählen Sie **[!UICONTROL Erweiterungen]** aus, um eine Liste der Erweiterungen aufzurufen, die derzeit mit Ihrer Mobile-Eigenschaft verknüpft sind.

![Die Seite mit den Details zu den Mobile-Eigenschaften wird angezeigt. Es werden Informationen zu den letzten Aktivitäten angezeigt. Die Registerkarte „Erweiterungen“ ist hervorgehoben.](./images/implement-assurance/tag-properties.png)

Wählen Sie **[!UICONTROL Katalog]** aus, um eine Liste der Erweiterungen anzuzeigen, die Sie der Mobile-Eigenschaft hinzufügen können. Suchen Sie mithilfe des Filters nach der **[!UICONTROL AEP Assurance]** und wählen Sie **[!UICONTROL Installieren]** aus.

![Der Erweiterungskatalog wird angezeigt. Die Assurance-Erweiterung wird nach gefiltert und angezeigt. Die Schaltfläche „Installieren“ ist hervorgehoben.](./images/implement-assurance/assurance-extension.png)

## Nächste Schritte

Nachdem Sie die Assurance-Erweiterung in Ihrer mobilen Eigenschaft installiert haben, können Sie Assurance in Ihren Anwendungen verwenden. Informationen zum Hinzufügen der Assurance-Erweiterung zu Ihrem Programm finden Sie in der [Übersicht über die Adobe Experience Platform Assurance-Erweiterung](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). Um zu erfahren, wie Sie Assurance verwenden, lesen Sie bitte das [Handbuch zur Verwendung von Assurance](./using-assurance.md).
