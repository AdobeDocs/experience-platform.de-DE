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

Mit dem `data`-Objekt können Sie eine Payload an Adobe senden, die nicht mit einem XDM-Schema übereinstimmt. Dies ist in Nicht-XDM-Szenarien nützlich, z. B. wenn Daten direkt an Adobe Analytics, Adobe Target oder Adobe Audience Manager gesendet werden. Wenn Daten im Datenstrom eingehen, können Sie [Datenvorbereitung-Zuordnung](/help/data-prep/ui/mapping.md) verwenden, um jedem Feld im `data`-Objekt XDM-Felder zuzuweisen.

>[!IMPORTANT]
>
>Daten in diesem Objekt müssen mindestens eine der folgenden Aktionen aufweisen:
>
>* Ein Service im Datenstrom muss so konfiguriert sein, dass Daten aus einer bestimmten Eigenschaft im `data`-Objekt abgerufen werden.
>* Die angegebene Eigenschaft muss mithilfe der Datenvorbereitung einem XDM-Feld zugeordnet werden.
>
>Wenn eine bestimmte Eigenschaft keinem XDM-Feld zugeordnet ist oder von einem konfigurierten Service verwendet wird, gehen diese Daten dauerhaft verloren.

## Verwenden des `data`-Objekts über die Web-SDK-Tag-Erweiterung {#tag-extension}

Geben Sie ein Datenelement im Feld **[!UICONTROL Daten]** innerhalb der Aktionen einer Tag-Regel an.

1. Melden Sie sich mit Ihren Adobe ID[Anmeldeinformationen bei ](https://experience.adobe.com)experience.adobe.com) an.
1. Navigieren Sie **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. Wählen [!UICONTROL &#x200B; unter &quot;]&quot; eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie das [!UICONTROL Erweiterung] Dropdown-Feld auf **[!UICONTROL Adobe Experience Platform Web SDK]** fest und legen Sie den [!UICONTROL Aktionstyp] auf **[!UICONTROL Ereignis senden]**.
1. Geben Sie das Datenelement an, das das gewünschte Objekt im Feld **[!UICONTROL Daten]** enthält.
1. Klicken Sie **[!UICONTROL Änderungen beibehalten]** und führen Sie dann den Veröffentlichungs-Workflow aus.

## Verwenden des `data`-Objekts über die Web SDK JavaScript-Bibliothek {#library}

Legen Sie das `data`-Objekt als Teil des JSON-Objekts innerhalb des -Parameters des `sendEvent`-Befehls fest. Für Daten, die Sie im Datenstrom zuordnen möchten, können Sie dieses Objekt beliebig strukturieren. Stellen Sie bei Daten, die von bestimmten Services verwendet werden, sicher, dass die Objekthierarchie mit dem übereinstimmt, was der Service erwartet. Sie können sowohl das `data`- als auch das [`xdm`](xdm.md)-Objekt in denselben `sendEvent`-Befehl aufnehmen.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Verwenden des `data`-Objekts mit Adobe Analytics {#analytics}

Sie können das `data`-Objekt mit Adobe Analytics verwenden, um Daten ohne XDM-Schema an eine Report Suite zu senden. Variablen sind so konfiguriert, dass sie dieselbe Syntax wie [!DNL AppMeasurement] verwenden, was den Upgrade-Prozess auf die Web-SDK vereinfacht. Adobe Analytics Weitere Informationen finden [ unter „Zuordnen von Datenobjektvariablen zu ](https://experienceleague.adobe.com/de/docs/analytics/implementation/aep-edge/data-var-mapping)&quot; im Adobe Analytics-Implementierungshandbuch.
