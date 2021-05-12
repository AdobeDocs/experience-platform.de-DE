---
title: Aktionstypen in der Adobe Experience Platform Web SDK Extension
description: Erfahren Sie mehr über die verschiedenen Aktionstypen, die die Adobe Experience Platform Web SDK Extension in Adobe Experience Platform Launch bereitstellt.
solution: Experience Platform
feature: Web SDK
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 7e87f5b29d388b34681217e392c3f1ae8f2b67ee
workflow-type: tm+mt
source-wordcount: '547'
ht-degree: 4%

---

# Aktionstypen

Nachdem Sie die [Adobe Experience Platform Web SDK Extension](web-sdk-extension.md) für [Adobe Experience Platform Launch](https://experienceleague.adobe.com/docs/launch.html) konfiguriert haben, konfigurieren Sie die Aktionstypen.

Auf dieser Seite werden die verfügbaren Aktionstypen beschrieben.

## Ereignis senden

Sendet ein Ereignis an die Adobe [!DNL Experience Platform], damit Adobe Experience Platform die von Ihnen gesendeten Daten erfassen und darauf reagieren kann. Wählen Sie eine Instanz aus (wenn mehrere Instanzen vorhanden sind). Alle Daten, die Sie senden möchten, können im Feld **[!UICONTROL XDM Data]** gesendet werden. Verwenden Sie ein JSON-Objekt, das der Struktur Ihres XDM-Schemas entspricht. Dieses Objekt kann entweder auf Ihrer Seite oder über ein **[!UICONTROL Benutzerspezifischer Code]** **[!UICONTROL Datenelement]** erstellt werden.

Es gibt einige weitere Felder im Aktionstyp Ereignis senden, die je nach Implementierung ebenfalls nützlich sein können. Bitte beachten Sie, dass diese Felder alle optional sind.

- **Typ:** Dieses Feld ermöglicht Ihnen, einen Ereignistyp anzugeben, der in Ihrem XDM-Schema aufgezeichnet wird. Weitere Informationen zu den Standard-Ereignistypen finden Sie in der [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api).
- **Zusammenführungs-ID:** Wenn Sie eine  [Zusammenführungs-](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/merging-event-data.html?lang=en#fundamentals) ID für Ihr Ereignis angeben möchten, können Sie dies in diesem Feld tun. Bitte beachten Sie, dass die nachgeschalteten Ereignisse derzeit nicht in der Lage sind, Ihre Daten zusammenzuführen.
- **Dataset-ID:** Wenn Sie Daten an einen anderen Datensatz als den im Datastream angegebenen senden müssen, können Sie diese Dataset-ID hier angeben.
- **Dokument wird entladen:** Wenn Sie sicherstellen möchten, dass die Ereignis auch dann auf den Server gelangen, wenn der Benutzer von der Seite weg navigiert, aktivieren Sie das Kontrollkästchen  **[!UICONTROL Dokument wird]** entladen. Dadurch können Ereignis den Server erreichen, Antworten werden jedoch ignoriert.
- **Entscheidungen zur visuellen Personalisierung rendern:** Wenn Sie personalisierte Inhalte auf Ihrer Seite wiedergeben möchten, aktivieren Sie das Kontrollkästchen  **[!UICONTROL Visuelle Personalisierung]** rendernfür die Deaktivierung. Sie können bei Bedarf auch Entscheidungsbereiche angeben. Weitere Informationen zum Rendern personalisierter Inhalte finden Sie in der [Personalisierungsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#automatically-rendering-content).

## Festlegen des Einverständnisses

Nachdem Sie die Einwilligung Ihres Benutzers erhalten haben, muss diese Einwilligung mit dem Aktionstyp &quot;Einwilligung festlegen&quot;an das Adobe Experience Platform Web SDK übermittelt werden. Derzeit werden zwei Arten von Standards unterstützt: „Adobe“ und „IAB TCF“. Siehe [Voreinstellungen für unterstützende Kunden-Zustimmung](../consent/supporting-consent.md). Bei Verwendung der Adobe 2.0 wird nur ein Datenelementwert unterstützt. Sie müssen ein Datenelement erstellen, das zum Objekt für die Zustimmung aufgelöst wird.

In dieser Aktion wird Ihnen auch ein optionales Feld zur Aufnahme einer Identitätskarte bereitgestellt, damit Identitäten synchronisiert werden können, sobald die Zustimmung eingegangen ist. Die Synchronisierung ist nützlich, wenn die Zustimmung als &quot;Ausstehend&quot;oder &quot;Ausstehend&quot;konfiguriert ist, da der Genehmigungsaufruf wahrscheinlich der erste ausgelöste Aufruf ist.

## Zurücksetzen der Zusammenführungs-ID des Ereignisses

Wenn Sie Ihre Ereignis Merge-ID auf Ihrer Seite zurücksetzen möchten, können Sie dies mit dieser Aktion tun. Um Ihre ID zurückzusetzen, wählen Sie die Zusammenfüge-ID aus, die Sie zurücksetzen möchten, und starten Sie die Aktion nach Bedarf.

## Wie geht es weiter

Nachdem Sie die Aktionen festgelegt haben, konfigurieren Sie [die Datenelementtypen](data-element-types.md).
