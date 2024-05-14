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

Die `data` -Objekt können Sie eine Payload an Adobe senden, die nicht mit einem XDM-Schema übereinstimmt. Dies ist in Nicht-XDM-Szenarien nützlich, z. B. beim direkten Senden von Daten an Adobe Analytics, Adobe Target oder Adobe Audience Manager. Wenn Daten in den Datastream eingehen, können Sie [Datenvorbereitung](/help/data-prep/ui/mapping.md) , um jedem Feld im `data` -Objekt.

>[!IMPORTANT]
>
>Die Daten in diesem Objekt müssen mindestens eine der folgenden Aktionen aufweisen:
>
>* Ein Dienst im Datastream muss konfiguriert werden, um Daten aus einer bestimmten Eigenschaft in der `data` -Objekt.
>* Die angegebene Eigenschaft muss mithilfe von data prep einem XDM-Feld zugeordnet werden.
>
>Wenn eine bestimmte Eigenschaft keinem XDM-Feld zugeordnet oder von einem konfigurierten Dienst verwendet wird, gehen diese Daten dauerhaft verloren.

## Verwenden Sie die `data` -Objekt über die Web SDK-Tag-Erweiterung {#tag-extension}

Stellen Sie ein Datenelement im **[!UICONTROL Daten]** in den Aktionen einer Tag-Regel.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. under [!UICONTROL Aktionen], wählen Sie eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie die [!UICONTROL Erweiterung] Dropdown-Feld zu **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie die [!UICONTROL Aktionstyp] nach **[!UICONTROL Ereignis senden]**.
1. Stellen Sie das Datenelement bereit, das das gewünschte Objekt im **[!UICONTROL Daten]** -Feld.
1. Klicks **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Verwenden Sie die `data` -Objekt über die JavaScript-Bibliothek des Web SDK {#library}

Legen Sie die `data` -Objekt als Teil des JSON-Objekts innerhalb des -Parameters der `sendEvent` Befehl. Für Daten, die Sie im Datastream zuordnen möchten, können Sie dieses Objekt beliebig strukturieren. Stellen Sie bei Daten, die von bestimmten Diensten verwendet werden, sicher, dass die Objekthierarchie mit den Erwartungen des Dienstes übereinstimmt. Sie können beide `data` und dem [`xdm`](xdm.md) -Objekt im selben `sendEvent` Befehl.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```

## Verwenden Sie die `data` Objekt mit Adobe Analytics {#analytics}

Sie können die `data` -Objekt mit Adobe Analytics verwenden, um Daten an eine Report Suite ohne XDM-Schema zu senden. Variablen sind so konfiguriert, dass sie dieselbe Syntax wie [!DNL AppMeasurement] Variablen, wodurch der Aktualisierungsprozess auf das Web SDK vereinfacht wird. Siehe [Zuordnung von Datenobjektvariablen zu Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics/implementation/aep-edge/data-var-mapping) Weitere Informationen finden Sie im Adobe Analytics-Implementierungshandbuch.
