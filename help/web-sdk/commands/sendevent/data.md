---
title: data
description: Erfahren Sie, wie Sie Nicht-XDM-Daten an Adobe senden.
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 1%

---

# data

Die `data` -Eigenschaft können Sie Daten an Adobe senden, die nicht mit einem XDM-Schema übereinstimmen. Dies ist in Nicht-XDM-Szenarien nützlich, z. B. beim Aktualisieren einer [Adobe Target-Profil](/help/web-sdk/personalization/adobe-target/target-overview.md). Wenn Daten bei Adobe eingehen, können Sie mit dem Datastream-Mapping-Tool XDM-Felder jedem Feld im `data` -Eigenschaft.

>[!IMPORTANT]
>
>Daten innerhalb dieser Eigenschaft müssen mindestens eine der folgenden Aktionen aufweisen:
>
>* Ein Dienst im Datastream muss konfiguriert werden, um Daten aus einer bestimmten Eigenschaft in der `data` Objekt
>* Jede Eigenschaft muss einem XDM-Feld zugeordnet sein.
>
>Wenn ein bestimmtes Feld nicht einem XDM-Feld zugeordnet oder von einem konfigurierten Dienst verwendet wird, gehen diese Daten dauerhaft verloren.

## Verwenden der Dateneigenschaft mithilfe der Web SDK-Tag-Erweiterung

Stellen Sie ein Datenelement im **[!UICONTROL Daten]** in den Aktionen einer Tag-Regel.

1. Anmelden bei [experience.adobe.com](https://experience.adobe.com) mit Ihren Adobe ID-Anmeldedaten.
1. Navigieren Sie zu **[!UICONTROL Datenerfassung]** > **[!UICONTROL Tags]**.
1. Wählen Sie die gewünschte Tag-Eigenschaft aus.
1. Navigieren Sie zu **[!UICONTROL Regeln]** und wählen Sie dann die gewünschte Regel aus.
1. under [!UICONTROL Aktionen], wählen Sie eine vorhandene Aktion aus oder erstellen Sie eine Aktion.
1. Legen Sie die [!UICONTROL Erweiterung] Dropdown-Feld zu **[!UICONTROL Adobe Experience Platform Web SDK]** und legen Sie die [!UICONTROL Aktionstyp] nach **[!UICONTROL Ereignis senden]**.
1. Stellen Sie das Datenelement bereit, das das gewünschte Objekt im **[!UICONTROL Daten]** -Feld.
1. Klicks **[!UICONTROL Änderungen beibehalten]** und führen Sie dann Ihren Veröffentlichungs-Workflow aus.

## Verwenden der Dateneigenschaft mit der JavaScript-Bibliothek des Web SDK

Legen Sie die `data` -Eigenschaft als Teil des JSON-Objekts innerhalb des -Parameters der `sendEvent` Befehl. Für Daten, die Sie im Datastream zuordnen möchten, können Sie diese Eigenschaft beliebig strukturieren. Stellen Sie bei Daten, die von bestimmten Diensten verwendet werden, sicher, dass die Objekthierarchie mit den Erwartungen des Dienstes übereinstimmt. Sie können beide `data` und dem [`xdm`](xdm.md) -Objekt im selben `sendEvent` Befehl.

```javascript
alloy("sendEvent", {
  "data": dataObject
});
```
