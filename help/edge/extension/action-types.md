---
title: Aktionstypen für Platform Web SDK
description: Adobe Experience Platform Web SDK Extension Action Types in Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 473cc1f7617f1d65cdb70ff0e758178ea0174f00
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 54%

---


# Aktionstypen

Nachdem Sie die [Adobe Experience Platform Web SDK Extension](web-sdk-extension.md) für [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html) konfiguriert haben, konfigurieren Sie die Aktionstypen.

Auf dieser Seite werden die verfügbaren Aktionstypen beschrieben.

## Ereignis senden

Sendet ein Ereignis an die Adobe [!DNL Experience Platform], damit Adobe Experience Platform die von Ihnen gesendeten Daten erfassen und darauf reagieren kann. Sie müssen eine Instanz auswählen (wenn mehrere Instanzen vorhanden sind). Wenn das Ereignis zu Beginn eines Seitenladevorgangs oder während einer Seitenänderung in einer Einzelseitenanwendung erfolgt, wählen Sie **[!UICONTROL Tritt am Beginn einer Ansicht]** ein.

Alle Daten, die Sie senden möchten, können im Feld **[!UICONTROL XDM Data]** gesendet werden. Dies sollte ein JSON-Objekt sein, das der Struktur Ihres XDM-Schemas entspricht. Dieses Objekt kann entweder auf Ihrer Seite oder über ein **[!UICONTROL Benutzerspezifischer Code]** **[!UICONTROL Datenelement]** erstellt werden.

## Festlegen des Einverständnisses

Nachdem Sie die Einwilligung Ihres Benutzers erhalten haben, muss diese an das Adobe Experience Platform Web SDK weitergeleitet werden. Dazu verwenden Sie den Aktionstyp „Einverständnis festlegen“. Derzeit werden zwei Arten von Standards unterstützt: „Adobe“ und „IAB TCF“. Bei Verwendung des Adobe-Standards können Sie das Einverständnis derzeit als „In“ oder „Out“ festlegen oder mithilfe eines Datenelements bereitstellen. Wenn Sie den IAB-TCF-Standard verwenden, geben Sie die Version und den Wert an, die Sie verwenden möchten, sowie zusätzliche Informationen zur DSGVO.

In dieser Aktion erhalten Sie auch ein optionales Feld, um eine Identitätskarte einzuschließen, damit Identitäten nach Erhalt des Einverständnisses synchronisiert werden können. Dies kann nützlich sein, wenn das Einverständnis als „Ausstehend“ konfiguriert ist, da der Einverständnisaufruf wahrscheinlich der erste ausgelöste Aufruf sein wird.

## Zurücksetzen der Zusammenführungs-ID des Ereignisses

Wenn Sie die Zusammenführungs-ID des Ereignisses auf Ihrer Seite zurücksetzen möchten, können Sie dies mit dieser Aktion tun. Um Ihre ID zurückzusetzen, müssen Sie die Zusammenführungs-ID auswählen, die Sie zurücksetzen möchten, und die Aktion nach Bedarf auslösen.

## Nächste Schritte

Nachdem Sie die Aktionstypen festgelegt haben, konfigurieren Sie [die Datenelementtypen](data-element-types.md).