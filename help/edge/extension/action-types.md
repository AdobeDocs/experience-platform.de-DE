---
title: Aktionstypen in der Adobe Experience Platform Web SDK-Erweiterung
description: Erfahren Sie mehr über die verschiedenen Aktionstypen, die von der Adobe Experience Platform Web SDK-Tag-Erweiterung bereitgestellt werden.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 5218e6cf82b74efbbbcf30495395a4fe2ad9fe14
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 4%

---

# Aktionstypen

Nachdem Sie die Tag-Erweiterung [Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md) konfiguriert haben, konfigurieren Sie Ihre Aktionstypen.

Auf dieser Seite werden die verfügbaren Aktionstypen beschrieben.


## Ereignis senden

Sendet ein Ereignis an die Adobe [!DNL Experience Platform], damit Adobe Experience Platform die gesendeten Daten erfassen und darauf reagieren kann. Wählen Sie eine Instanz aus (wenn mehrere Instanzen vorhanden sind). Alle Daten, die Sie senden möchten, können im Feld **[!UICONTROL XDM Data]** gesendet werden. Verwenden Sie ein JSON-Objekt, das der Struktur Ihres XDM-Schemas entspricht. Dieses Objekt kann entweder auf Ihrer Seite oder über ein **[!UICONTROL benutzerdefinierter Code]** **[!UICONTROL Datenelement]** erstellt werden.

Es gibt einige weitere Felder im Aktionstyp Ereignis senden , die je nach Implementierung ebenfalls nützlich sein können. Bitte beachten Sie, dass alle diese Felder optional sind.

- **Typ:** Mit diesem Feld können Sie einen Ereignistyp angeben, der in Ihrem XDM-Schema aufgezeichnet wird. Weitere Informationen zu den standardmäßigen Ereignistypen finden Sie in der [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) .
- **Daten:** Daten, die nicht mit einem XDM-Schema übereinstimmen, können mit diesem Feld gesendet werden. Dieses Feld ist nützlich, wenn Sie versuchen, ein Adobe Target-Profil zu aktualisieren oder Target Recommendations-Attribute zu senden. Beispiele finden Sie in der [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en).
<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **Datensatz-ID:** Wenn Sie Daten an einen Datensatz senden müssen, der nicht von Ihnen im Datensatz angegeben wurde, können Sie diese Datensatz-ID hier angeben.
- **Dokument wird entladen:** Wenn Sie sicherstellen möchten, dass die Ereignisse den Server erreichen, auch wenn der Benutzer von der Seite weg navigiert, aktivieren Sie das Kontrollkästchen  **[!UICONTROL Dokument wird]** entladen . Dadurch können Ereignisse den Server erreichen, Antworten werden jedoch ignoriert.
- **Entscheidungen zur visuellen Personalisierung rendern:** Wenn Sie personalisierte Inhalte auf Ihrer Seite rendern möchten, aktivieren Sie das Kontrollkästchen  **[!UICONTROL visuelle Personalisierungsentscheidung]** rendern . Sie können bei Bedarf auch Entscheidungsbereiche festlegen. Weitere Informationen zum Rendern personalisierter Inhalte finden Sie in der [Personalisierungsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#automatically-rendering-content) .

## Festlegen des Einverständnisses

Nachdem Sie die Einwilligung Ihres Benutzers erhalten haben, muss diese Einwilligung mithilfe des Aktionstyps &quot;Einverständnis festlegen&quot;an das Adobe Experience Platform Web SDK übermittelt werden. Derzeit werden zwei Arten von Standards unterstützt: „Adobe“ und „IAB TCF“. Siehe [Unterstützende Voreinstellungen für die Kundeneinwilligung](../consent/supporting-consent.md). Bei Verwendung von Adobe Version 2.0 wird nur ein Datenelementwert unterstützt. Sie müssen ein Datenelement erstellen, das in das Objekt für die Zustimmung aufgelöst wird.

Bei dieser Aktion erhalten Sie auch ein optionales Feld, um eine Identity Map einzuschließen, damit Identitäten synchronisiert werden können, sobald die Zustimmung eingeht. Die Synchronisierung ist nützlich, wenn die Zustimmung als &quot;Ausstehend&quot;oder &quot;Out&quot;konfiguriert ist, da der Zustimmungsaufruf wahrscheinlich der erste ausgelöste Aufruf ist.

## Zurücksetzen der Zusammenführungs-ID des Ereignisses

Wenn Sie Ihre Ereigniszusammenführungs-ID auf Ihrer Seite zurücksetzen möchten, können Sie dies mit dieser Aktion tun. Um Ihre ID zurückzusetzen, wählen Sie die Zusammenführungs-ID aus, die Sie zurücksetzen möchten, und lösen Sie die Aktion nach Bedarf aus.

## Wie geht es weiter

Nachdem Sie Ihre Aktionen festgelegt haben, konfigurieren Sie [Ihre Datenelementtypen](data-element-types.md).
