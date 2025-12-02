---
title: data
description: Erfahren Sie, wie Sie Nicht-XDM-Daten über das Datenobjekt an Adobe senden.
exl-id: 537fc34e-3cda-4aa7-ae0d-0d3ef4b89848
source-git-commit: f4a2778c71ad6a48621212f3ece1776d1b3ac643
workflow-type: tm+mt
source-wordcount: '311'
ht-degree: 0%

---

# `data`

Mit dem `data`-Objekt können Sie eine Payload an Adobe senden, die nicht mit einem XDM-Schema übereinstimmt. Dies ist in Nicht-XDM-Szenarien nützlich, z. B. wenn Daten direkt an Adobe Analytics, Adobe Target oder Adobe Audience Manager gesendet werden. Wenn Daten im Datenstrom eingehen, können Sie [Datenvorbereitung-Zuordnung](/help/data-prep/ui/mapping.md) verwenden, um jedem Feld im `data`-Objekt XDM-Felder zuzuweisen. Wenn ein Produkt bereits von Adobe konfiguriert wurde, um Felder innerhalb des `data` zu erkennen, können Sie diese Daten unverändert an einen Datenstrom senden.

>[!IMPORTANT]
>
>Daten in diesem Objekt müssen mindestens eine der folgenden Aktionen aufweisen:
>
>* Ein Service im Datenstrom muss so konfiguriert sein, dass Daten aus einer bestimmten Eigenschaft im `data`-Objekt abgerufen werden.
>* Die angegebene Eigenschaft muss mithilfe der Datenvorbereitung einem XDM-Feld zugeordnet werden.
>
>Wenn eine bestimmte Eigenschaft keinem XDM-Feld zugeordnet ist oder von einem konfigurierten Service verwendet wird, gehen diese Daten dauerhaft verloren.

Legen Sie das `data`-Objekt als Teil des JSON-Objekts innerhalb des -Parameters des `sendEvent`-Befehls fest. Für Daten, die Sie im Datenstrom zuordnen möchten, können Sie dieses Objekt beliebig strukturieren. Stellen Sie bei Daten, die von bestimmten Services verwendet werden, sicher, dass die Objekthierarchie mit dem übereinstimmt, was der Service erwartet. Sie können sowohl das `data`- als auch das [`xdm`](xdm.md)-Objekt in denselben `sendEvent`-Befehl aufnehmen.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Verwenden des `data`-Objekts mit Adobe Analytics {#analytics}

Sie können das `data`-Objekt mit Adobe Analytics verwenden, um Daten ohne XDM-Schema an eine Report Suite zu senden. Variablen sind so konfiguriert, dass sie dieselbe Syntax wie AppMeasurement-Variablen verwenden, was den Upgrade-Prozess auf die Web-SDK vereinfacht. Adobe Analytics Weitere Informationen finden [&#x200B; unter „Zuordnen von Datenobjektvariablen zu &#x200B;](https://experienceleague.adobe.com/de/docs/analytics/implementation/aep-edge/data-var-mapping)&quot; im Adobe Analytics-Implementierungshandbuch.

## Verwenden des `data`-Objekts mithilfe der Tag-Erweiterung „Web SDK&quot;

Das `data`-Objekt ist als [Variablendatenelement“ verfügbar](/help/tags/extensions/client/web-sdk/data-element-types.md#variable) wenn die Tag-Erweiterung „Web SDK&quot; verwendet wird.
