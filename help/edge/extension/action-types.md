---
title: Aktionstypen in der Adobe Experience Platform Web SDK-Erweiterung
description: Erfahren Sie mehr über die verschiedenen Aktionstypen, die von der Adobe Experience Platform Web SDK-Tag-Erweiterung bereitgestellt werden.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 1b0f1e2e1625f6994a6e09bd086e4b63a3e8d4ab
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 4%

---

# Aktionstypen

Nachdem Sie die [Adobe Experience Platform Web SDK-Tag-Erweiterung](web-sdk-extension-configuration.md), konfigurieren Sie Ihre Aktionstypen.

Auf dieser Seite werden die verfügbaren Aktionstypen beschrieben.


## Ereignis senden

Sendet ein Ereignis an Adobe [!DNL Experience Platform] damit Adobe Experience Platform die von Ihnen gesendeten Daten erfassen und entsprechend handeln kann. Wählen Sie eine Instanz aus (wenn mehrere Instanzen vorhanden sind). Alle Daten, die Sie senden möchten, können im **[!UICONTROL XDM-Daten]** -Feld. Verwenden Sie ein JSON-Objekt, das der Struktur Ihres XDM-Schemas entspricht. Dieses Objekt kann entweder auf Ihrer Seite oder über eine **[!UICONTROL Benutzerspezifischer Code]** **[!UICONTROL Datenelement]**.

Es gibt einige weitere Felder im Aktionstyp Ereignis senden , die je nach Implementierung ebenfalls nützlich sein können. Bitte beachten Sie, dass alle diese Felder optional sind.

- **Typ:** In diesem Feld können Sie einen Ereignistyp angeben, der in Ihrem XDM-Schema aufgezeichnet wird. Siehe [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) für weitere Informationen zu den standardmäßigen Ereignistypen.
- **Daten:** Daten, die nicht mit einem XDM-Schema übereinstimmen, können mit diesem Feld gesendet werden. Dieses Feld ist nützlich, wenn Sie versuchen, ein Adobe Target-Profil zu aktualisieren oder Target Recommendations-Attribute zu senden. Beispiele: Sehen Sie sich unsere [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en).<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **Datensatz-ID:** Wenn Sie Daten an einen Datensatz senden müssen, der nicht in Ihrem Datensatz angegeben wurde, können Sie diese Datensatz-ID hier angeben.
- **Dokument wird entladen:** Wenn Sie sicherstellen möchten, dass die Ereignisse den Server erreichen, auch wenn der Benutzer von der Seite weg navigiert, überprüfen Sie die **[!UICONTROL Dokument wird entladen]** aktivieren. Dadurch können Ereignisse den Server erreichen, Antworten werden jedoch ignoriert.
- **visuelle Personalisierungsentscheidungen rendern:** Wenn Sie personalisierte Inhalte auf Ihrer Seite rendern möchten, überprüfen Sie die **[!UICONTROL visuelle Personalisierungsentscheidungen rendern]** aktivieren. Sie können bei Bedarf auch Entscheidungsbereiche und/oder Oberflächen angeben. Siehe [Personalisierungsdokumentation](../personalization/rendering-personalization-content.md#automatically-rendering-content) für weitere Informationen zum Rendern personalisierter Inhalte.

## Festlegen des Einverständnisses

Nachdem Sie die Einwilligung Ihres Benutzers erhalten haben, muss diese Einwilligung mithilfe des Aktionstyps &quot;Einverständnis festlegen&quot;an das Adobe Experience Platform Web SDK übermittelt werden. Derzeit werden zwei Arten von Standards unterstützt: „Adobe“ und „IAB TCF“. Siehe [Unterstützende Voreinstellungen für die Kundeneinwilligung](../consent/supporting-consent.md). Bei Verwendung von Adobe Version 2.0 wird nur ein Datenelementwert unterstützt. Sie müssen ein Datenelement erstellen, das in das Objekt für die Zustimmung aufgelöst wird.

Bei dieser Aktion erhalten Sie auch ein optionales Feld, um eine Identity Map einzuschließen, damit Identitäten synchronisiert werden können, sobald die Zustimmung eingeht. Die Synchronisierung ist nützlich, wenn die Zustimmung als &quot;Ausstehend&quot;oder &quot;Out&quot;konfiguriert ist, da der Zustimmungsaufruf wahrscheinlich der erste ausgelöste Aufruf ist.

## Zurücksetzen der Zusammenführungs-ID des Ereignisses

Wenn Sie Ihre Ereigniszusammenführungs-ID auf Ihrer Seite zurücksetzen möchten, können Sie dies mit dieser Aktion tun. Um Ihre ID zurückzusetzen, wählen Sie die Zusammenführungs-ID aus, die Sie zurücksetzen möchten, und lösen Sie die Aktion nach Bedarf aus.

## Wie geht es weiter

Nachdem Sie die Aktionen festgelegt haben, [Datenelementtypen konfigurieren](data-element-types.md).
