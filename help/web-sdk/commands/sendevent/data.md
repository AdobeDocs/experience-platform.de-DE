---
title: data
description: Erfahren Sie, wie Sie Nicht-XDM-Daten über das Datenobjekt an Adobe senden.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: 8c652e96fa79b587c7387a4053719605df012908
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---


# `data`

Mit dem Objekt `data` können Sie eine Payload an Adobe senden, die nicht mit einem XDM-Schema übereinstimmt. Dies ist in Nicht-XDM-Szenarien nützlich, z. B. beim direkten Senden von Daten an Adobe Analytics, Adobe Target oder Adobe Audience Manager. Wenn Daten in den Datastream eingehen, können Sie [Datenvorbereitung-Zuordnung](/help/data-prep/ui/mapping.md) verwenden, um jedem Feld im `data` -Objekt XDM-Felder zuzuweisen.

>[!IMPORTANT]
>
>Die Daten in diesem Objekt müssen mindestens eine der folgenden Aktionen aufweisen:
>
>* Ein Dienst im Datastream muss so konfiguriert werden, dass Daten aus einer bestimmten Eigenschaft im `data` -Objekt abgerufen werden.
>* Die angegebene Eigenschaft muss mithilfe von data prep einem XDM-Feld zugeordnet werden.
>
>Wenn eine bestimmte Eigenschaft keinem XDM-Feld zugeordnet oder von einem konfigurierten Dienst verwendet wird, gehen diese Daten dauerhaft verloren.

## Verwenden des Objekts `data` über die Web SDK-Tag-Erweiterung {#tag-extension}

Geben Sie ein Datenelement im Feld **[!UICONTROL Daten]** innerhalb der Aktionen einer Tag-Regel an.

1. Melden Sie sich mit Ihren Adobe ID-Anmeldedaten bei [experience.adobe.com](https://experience.adobe.com) an.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen Sie unter [!UICONTROL Aktionen] eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Setzen Sie das Dropdown-Feld [!UICONTROL Erweiterung] auf **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie den Aktionstyp ] auf **[!UICONTROL Ereignis senden]** fest.[!UICONTROL 
1. Geben Sie das Datenelement mit dem gewünschten Objekt im Feld **[!UICONTROL Daten]** an.
1. Klicken Sie auf **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Verwenden des Objekts `data` über die Web SDK JavaScript-Bibliothek {#library}

Legen Sie das Objekt `data` als Teil des JSON-Objekts innerhalb des Parameters des Befehls `sendEvent` fest. Für Daten, die Sie im Datastream zuordnen möchten, können Sie dieses Objekt beliebig strukturieren. Stellen Sie bei Daten, die von bestimmten Diensten verwendet werden, sicher, dass die Objekthierarchie mit den Erwartungen des Dienstes übereinstimmt. Sie können sowohl das Objekt `data` als auch das Objekt [`xdm`](xdm.md) im selben Befehl `sendEvent` einbeziehen.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Verwenden des Objekts `data` mit Adobe Analytics {#analytics}

Sie können das `data` -Objekt mit Adobe Analytics verwenden, um Daten an eine Report Suite ohne XDM-Schema zu senden. Variablen sind so konfiguriert, dass sie dieselbe Syntax wie [!DNL AppMeasurement] -Variablen verwenden und so den Aktualisierungsprozess auf das Web SDK vereinfachen. Weitere Informationen finden Sie unter [Zuordnung von Datenobjektvariablen zu Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) im Implementierungshandbuch zu Adobe Analytics.
