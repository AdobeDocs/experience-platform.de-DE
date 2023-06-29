---
title: Aktionstypen in der Adobe Experience Platform Web SDK-Erweiterung
description: Erfahren Sie mehr über die verschiedenen Aktionstypen, die von der Adobe Experience Platform Web SDK-Tag-Erweiterung bereitgestellt werden.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 528b13aa20da62c32456e02cb2293fdded156421
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 4%

---


# Aktionstypen

Nachdem Sie die [Adobe Experience Platform Web SDK-Tag-Erweiterung](web-sdk-extension-configuration.md)müssen Sie Ihre Aktionstypen konfigurieren.

Auf dieser Seite werden die von der Variablen [Adobe Experience Platform Web SDK-Tag-Erweiterung](web-sdk-extension-configuration.md).

## Ereignis senden {#send-event}

Sendet ein Ereignis an Adobe [!DNL Experience Platform] damit Adobe Experience Platform die von Ihnen gesendeten Daten erfassen und entsprechend handeln kann. Wählen Sie eine Instanz aus (wenn mehrere Instanzen vorhanden sind). Alle Daten, die Sie senden möchten, können im **[!UICONTROL XDM-Daten]** -Feld. Verwenden Sie ein JSON-Objekt, das der Struktur Ihres XDM-Schemas entspricht. Dieses Objekt kann entweder auf Ihrer Seite oder über eine **[!UICONTROL Benutzerspezifischer Code]** **[!UICONTROL Datenelement]**.

Es gibt einige weitere Felder im Aktionstyp Ereignis senden , die je nach Implementierung ebenfalls nützlich sein können. Bitte beachten Sie, dass alle diese Felder optional sind.

- **Typ:** In diesem Feld können Sie einen Ereignistyp angeben, der in Ihrem XDM-Schema aufgezeichnet wird. Siehe [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=de#using-the-sendbeacon-api) für weitere Informationen zu den standardmäßigen Ereignistypen.
- **Daten:** Daten, die nicht mit einem XDM-Schema übereinstimmen, können mit diesem Feld gesendet werden. Dieses Feld ist nützlich, wenn Sie versuchen, ein Adobe Target-Profil zu aktualisieren oder Target Recommendations-Attribute zu senden. Beispiele: Sehen Sie sich unsere [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=de).<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **Datensatz-ID:** Wenn Sie Daten an einen Datensatz senden müssen, der nicht in Ihrem Datensatz angegeben wurde, können Sie diese Datensatz-ID hier angeben.
- **Dokument wird entladen:** Wenn Sie sicherstellen möchten, dass die Ereignisse den Server erreichen, auch wenn der Benutzer von der Seite weg navigiert, überprüfen Sie die **[!UICONTROL Dokument wird entladen]** aktivieren. Dadurch können Ereignisse den Server erreichen, Antworten werden jedoch ignoriert.
- **Entscheidungen zur visuellen Personalisierung rendern:** Wenn Sie personalisierte Inhalte auf Ihrer Seite rendern möchten, überprüfen Sie die **[!UICONTROL visuelle Personalisierungsentscheidungen rendern]** aktivieren. Sie können bei Bedarf auch Entscheidungsbereiche und/oder Oberflächen angeben. Siehe [Personalisierungsdokumentation](../../../../edge/personalization/rendering-personalization-content.md#automatically-rendering-content) für weitere Informationen zum Rendern personalisierter Inhalte.

## Einverständnis festlegen {#set-consent}

Nachdem Sie die Einwilligung Ihres Benutzers erhalten haben, muss diese Einwilligung mithilfe des Aktionstyps &quot;Einverständnis festlegen&quot;an das Adobe Experience Platform Web SDK übermittelt werden. Derzeit werden zwei Arten von Standards unterstützt: „Adobe“ und „IAB TCF“. Siehe [Unterstützende Voreinstellungen für die Kundeneinwilligung](../../../../edge/consent/supporting-consent.md). Bei Verwendung von Adobe Version 2.0 wird nur ein Datenelementwert unterstützt. Sie müssen ein Datenelement erstellen, das in das Objekt für die Zustimmung aufgelöst wird.

Bei dieser Aktion erhalten Sie auch ein optionales Feld, um eine Identity Map einzuschließen, damit Identitäten synchronisiert werden können, sobald die Zustimmung eingeht. Die Synchronisierung ist nützlich, wenn die Zustimmung als &quot;Ausstehend&quot;oder &quot;Out&quot;konfiguriert ist, da der Zustimmungsaufruf wahrscheinlich der erste ausgelöste Aufruf ist.

## Variable aktualisieren {#update-variable}

Verwenden Sie diese Aktion, um ein XDM-Objekt als Ergebnis eines Ereignisses zu ändern. Mit dieser Aktion soll ein Objekt erstellt werden, das später über eine **[!UICONTROL Ereignis senden]** -Aktion, um das Ereignis-XDM-Objekt aufzuzeichnen.

Um diesen Aktionstyp verwenden zu können, müssen Sie eine [Variable](data-element-types.md#variable) Datenelement. Sobald Sie ein zu änderndes Variablendatenelement ausgewählt haben, wird ein Editor ähnlich dem Editor für [XDM-Objekt](data-element-types.md#xdm-object) Datenelement.

![](assets/update-variable.png)

Das für den Editor verwendete XDM-Schema ist das Schema, das auf der [!UICONTROL Variable] Datenelement. Sie können eine oder mehrere Eigenschaften des Objekts festlegen, indem Sie auf eine der Eigenschaften im Baum auf der linken Seite klicken und dann den Wert auf der rechten Seite ändern. Im folgenden Screenshot wird beispielsweise die Eigenschaft &quot;productionBy&quot;auf das Datenelement &quot;Produced by data element&quot;gesetzt.

![](assets/update-variable-set-property.png)

Es gibt einige Unterschiede zwischen dem Editor in der Aktion &quot;Variable aktualisieren&quot;und dem Editor im XDM-Objektdatenelement. Zunächst enthält die Aktion für die Variable &quot;update&quot;ein Element auf der Stammebene mit der Bezeichnung &quot;xdm&quot;. Wenn Sie auf dieses Element klicken, können Sie ein Datenelement angeben, das zum Festlegen des gesamten Objekts verwendet werden soll. Zweitens verfügt die Aktion für die Variable &quot;update&quot;über Kontrollkästchen, um die Daten aus dem xdm-Objekt zu löschen. Klicken Sie links auf eine der Eigenschaften und aktivieren Sie dann das Kontrollkästchen rechts, um den Wert zu löschen. Dadurch wird der aktuelle Wert gelöscht, bevor Werte für die Variable festgelegt werden.

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie ein besseres Verständnis davon haben, wie Sie Ihre Aktionen konfigurieren. Lesen Sie als Nächstes, wie Sie [Datenelementtypen konfigurieren](data-element-types.md).
