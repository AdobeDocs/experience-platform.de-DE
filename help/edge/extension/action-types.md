---
title: Aktionstypen in der Adobe Experience Platform Web SDK Extension
description: Erfahren Sie mehr über die verschiedenen Aktionstypen, die die Adobe Experience Platform Web SDK Extension in Adobe Experience Platform Launch bereitstellt.
translation-type: tm+mt
source-git-commit: 2a0ae9541a8bb2bb985d43a402d0842e73b23c81
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 18%

---


# Aktionstypen

Nachdem Sie die [Adobe Experience Platform Web SDK Extension](web-sdk-extension.md) für [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html) konfiguriert haben, konfigurieren Sie die Aktionstypen.

Auf dieser Seite werden die verfügbaren Aktionstypen beschrieben.

## Ereignis senden

Sendet ein Ereignis an die Adobe [!DNL Experience Platform], damit Adobe Experience Platform die von Ihnen gesendeten Daten erfassen und darauf reagieren kann. Wählen Sie eine Instanz aus (wenn mehrere Instanzen vorhanden sind). Wenn das Ereignis zu Beginn eines Seitenladevorgangs oder während einer Seitenänderung in einer Einzelseitenanwendung erfolgt, wählen Sie **[!UICONTROL Tritt am Beginn einer Ansicht]** ein.

Alle Daten, die Sie senden möchten, können im Feld **[!UICONTROL XDM Data]** gesendet werden. Verwenden Sie ein JSON-Objekt, das der Struktur Ihres XDM-Schemas entspricht. Dieses Objekt kann entweder auf Ihrer Seite oder über ein **[!UICONTROL Benutzerspezifischer Code]** **[!UICONTROL Datenelement]** erstellt werden.

## Festlegen des Einverständnisses

Nachdem Sie die Einwilligung Ihres Benutzers erhalten haben, muss diese Einwilligung mit dem Aktionstyp &quot;Einwilligung festlegen&quot;an das Adobe Experience Platform Web SDK übermittelt werden. Derzeit werden zwei Arten von Standards unterstützt: „Adobe“ und „IAB TCF“. Bei Verwendung des Adobe-Standards können Sie das Einverständnis derzeit als „In“ oder „Out“ festlegen oder mithilfe eines Datenelements bereitstellen. Wenn Sie den IAB-TCF-Standard verwenden, geben Sie die Version und den Wert an, die Sie verwenden möchten, sowie zusätzliche Informationen zur DSGVO.

In dieser Aktion wird Ihnen auch ein optionales Feld zur Aufnahme einer Identitätskarte bereitgestellt, damit Identitäten synchronisiert werden können, sobald die Zustimmung eingegangen ist. Die Synchronisierung ist nützlich, wenn die Zustimmung als &quot;Ausstehend&quot;konfiguriert ist, da der Einwilligungsaufruf wahrscheinlich der erste ausgelöste Aufruf ist.

## Zurücksetzen der Zusammenführungs-ID des Ereignisses

Wenn Sie Ihre Ereignis Merge-ID auf Ihrer Seite zurücksetzen möchten, können Sie dies mit dieser Aktion tun. Um Ihre ID zurückzusetzen, wählen Sie die Zusammenfüge-ID aus, die Sie zurücksetzen möchten, und starten Sie die Aktion nach Bedarf.

## Nächste Schritte

Nachdem Sie die Aktionstypen festgelegt haben, konfigurieren Sie [die Datenelementtypen](data-element-types.md).