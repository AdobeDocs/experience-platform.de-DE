---
title: Aktionstypen in der Adobe Experience Platform Web SDK-Erweiterung
description: Erfahren Sie mehr über die verschiedenen Aktionstypen, die von der Adobe Experience Platform Web SDK-Tag-Erweiterung bereitgestellt werden.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: fb9f7757d77b221c733bbed5124fa576a6b02ed2
workflow-type: tm+mt
source-wordcount: '1264'
ht-degree: 1%

---


# Aktionstypen

Nachdem Sie die Tag-Erweiterung [Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md) konfiguriert haben, müssen Sie Ihre Aktionstypen konfigurieren.

Auf dieser Seite werden die von der Tag-Erweiterung [Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md) unterstützten Aktionstypen beschrieben.


## Antwort anwenden {#apply-response}

Verwenden Sie den Aktionstyp **[!UICONTROL Antwort anwenden]** , wenn Sie basierend auf einer Antwort des Edge Networks verschiedene Aktionen durchführen möchten. Dieser Aktionstyp wird normalerweise in Hybridbereitstellungen verwendet, bei denen der Server einen ersten Aufruf an das Edge Network durchführt. Anschließend nimmt dieser Aktionstyp die Antwort aus diesem Aufruf und initialisiert das Web SDK im Browser.

Die Verwendung dieses Aktionstyps kann die Client-Ladezeiten für hybride Personalisierungsfälle verkürzen.

![Bild der Experience Platform-Benutzeroberfläche mit dem Aktionstyp &quot;Antwort anwenden&quot;.](assets/apply-response.png)

Dieser Aktionstyp unterstützt die folgenden Konfigurationsoptionen:

* **[!UICONTROL Instanz]**: Wählen Sie die verwendete Web SDK-Instanz aus.
* **[!UICONTROL Antwortheader]**: Wählen Sie das Datenelement aus, das ein Objekt zurückgibt, das die Header-Schlüssel und die vom Edge Network-Server-Aufruf zurückgegebenen Werte enthält.
* **[!UICONTROL Antworttext]**: Wählen Sie das Datenelement aus, das das Objekt zurückgibt, das die von der Edge Network-Antwort bereitgestellte JSON-Payload enthält.
* **[!UICONTROL visuelle Personalisierungsentscheidungen rendern]**: Aktivieren Sie diese Option, um den vom Edge Network bereitgestellten Personalisierungsinhalt automatisch wiederzugeben und den Inhalt vorab auszublenden, um Flackern zu vermeiden.

## Ereignis senden {#send-event}

Sendet ein Ereignis an Adobe [!DNL Experience Platform] , damit Adobe Experience Platform die gesendeten Daten erfassen und darauf reagieren kann. Wählen Sie eine Instanz aus (wenn mehrere Instanzen vorhanden sind). Alle Daten, die Sie senden möchten, können im Feld **[!UICONTROL XDM-Daten]** gesendet werden. Verwenden Sie ein JSON-Objekt, das der Struktur Ihres XDM-Schemas entspricht. Dieses Objekt kann entweder auf Ihrer Seite oder über ein **[!UICONTROL benutzerdefinierter Code]** **[!UICONTROL Datenelement]** erstellt werden.

Es gibt einige weitere Felder im Aktionstyp Ereignis senden , die je nach Implementierung ebenfalls nützlich sein können. Bitte beachten Sie, dass alle diese Felder optional sind.

* **Typ:** Mit diesem Feld können Sie einen Ereignistyp angeben, der in Ihrem XDM-Schema aufgezeichnet wird. Weitere Informationen finden Sie unter [`type`](/help/web-sdk/commands/sendevent/type.md) im Befehl `sendEvent` .
* **Daten:** Daten, die nicht mit einem XDM-Schema übereinstimmen, können mit diesem Feld gesendet werden. Dieses Feld ist nützlich, wenn Sie versuchen, ein Adobe Target-Profil zu aktualisieren oder Target Recommendations-Attribute zu senden. Weitere Informationen finden Sie unter [`data`](/help/web-sdk/commands/sendevent/data.md) im Befehl `sendEvent` .<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
* **Datensatz-ID:** Wenn Sie Daten an einen Datensatz senden müssen, der nicht in Ihrem Datensatz enthalten ist, können Sie diese Datensatz-ID hier angeben.
* **Dokument wird entladen:** Wenn Sie sicherstellen möchten, dass die Ereignisse den Server erreichen, auch wenn der Benutzer von der Seite weg navigiert, aktivieren Sie das Kontrollkästchen **[!UICONTROL Dokument wird entladen]** . Dadurch können Ereignisse den Server erreichen, Antworten werden jedoch ignoriert.
* **visuelle Personalisierungsentscheidungen rendern:** Wenn Sie personalisierte Inhalte auf Ihrer Seite rendern möchten, aktivieren Sie das Kontrollkästchen **[!UICONTROL visuelle Personalisierungsentscheidungen rendern]** . Sie können bei Bedarf auch Entscheidungsbereiche und/oder Oberflächen angeben. Weitere Informationen zum Rendern personalisierter Inhalte finden Sie in der [Personalisierungsdokumentation](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content) .

## Einverständnis festlegen {#set-consent}

Nachdem Sie die Einwilligung Ihres Benutzers erhalten haben, muss diese Einwilligung mithilfe des Aktionstyps &quot;Einverständnis festlegen&quot;an das Adobe Experience Platform Web SDK übermittelt werden. Derzeit werden zwei Arten von Standards unterstützt: „Adobe“ und „IAB TCF“. Siehe [Unterstützende Voreinstellungen für die Kundeneinwilligung](../../../../web-sdk/commands/setconsent.md). Bei Verwendung von Adobe Version 2.0 wird nur ein Datenelementwert unterstützt. Sie müssen ein Datenelement erstellen, das in das Objekt für die Zustimmung aufgelöst wird.

Bei dieser Aktion erhalten Sie auch ein optionales Feld, um eine Identity Map einzuschließen, damit Identitäten synchronisiert werden können, sobald die Zustimmung eingeht. Die Synchronisierung ist nützlich, wenn die Zustimmung als &quot;Ausstehend&quot;oder &quot;Out&quot;konfiguriert ist, da der Zustimmungsaufruf wahrscheinlich der erste ausgelöste Aufruf ist.

## Variable aktualisieren {#update-variable}

Verwenden Sie diese Aktion, um ein XDM-Objekt als Ergebnis eines Ereignisses zu ändern. Mit dieser Aktion soll ein Objekt erstellt werden, auf das später über eine Aktion vom Typ **[!UICONTROL Ereignis senden]** verwiesen werden kann, um das Ereignis-XDM-Objekt aufzuzeichnen.

Um diesen Aktionstyp verwenden zu können, müssen Sie ein [variable](data-element-types.md#variable) -Datenelement definiert haben. Sobald Sie ein zu änderndes Variablendatenelement auswählen, wird ein Editor ähnlich dem Editor für das Datenelement [XDM-Objekt](data-element-types.md#xdm-object) angezeigt.

![](assets/update-variable.png)

Das für den Editor verwendete XDM-Schema ist das Schema, das im Datenelement [!UICONTROL variable] ausgewählt ist. Sie können eine oder mehrere Eigenschaften des Objekts festlegen, indem Sie auf eine der Eigenschaften im Baum auf der linken Seite klicken und dann den Wert auf der rechten Seite ändern. Im folgenden Screenshot wird beispielsweise die Eigenschaft &quot;productionBy&quot;auf das Datenelement &quot;Produced by data element&quot;gesetzt.

![](assets/update-variable-set-property.png)

Es gibt einige Unterschiede zwischen dem Editor in der Aktion &quot;Variable aktualisieren&quot;und dem Editor im XDM-Objektdatenelement. Zunächst enthält die Aktion für die Variable &quot;update&quot;ein Element auf der Stammebene mit der Bezeichnung &quot;xdm&quot;. Wenn Sie auf dieses Element klicken, können Sie ein Datenelement angeben, das zum Festlegen des gesamten Objekts verwendet werden soll. Zweitens verfügt die Aktion für die Variable &quot;update&quot;über Kontrollkästchen, um die Daten aus dem xdm-Objekt zu löschen. Klicken Sie links auf eine der Eigenschaften und aktivieren Sie dann das Kontrollkästchen rechts, um den Wert zu löschen. Dadurch wird der aktuelle Wert gelöscht, bevor Werte für die Variable festgelegt werden.

## Medienereignis senden {#send-media-event}

Sendet ein Medienereignis an Adobe Experience Platform und/oder Adobe Analytics. Diese Aktion ist nützlich, wenn Sie Medienereignisse auf Ihrer Website verfolgen. Wählen Sie eine Instanz aus (wenn mehrere Instanzen vorhanden sind). Für die Aktion ist ein `playerId` erforderlich, der eine eindeutige Kennung für eine verfolgte Mediensitzung darstellt. Außerdem sind beim Starten einer Mediensitzung ein Datenelement vom Typ **[!UICONTROL Erlebnisqualität]** und ein Datenelement vom Typ `playhead` erforderlich.

![Bild der Platform-Benutzeroberfläche, das den Bildschirm für das Ereignis &quot;Medien senden&quot;anzeigt.](assets/send-media-event.png)

Der Aktionstyp **[!UICONTROL Medien-Ereignis senden]** unterstützt die folgenden Eigenschaften:

* **[!UICONTROL Instanz]**: Die verwendete Web SDK-Instanz.
* **[!UICONTROL Medien-Ereignistyp]**: Der Typ des zu verfolgenden Medienereignisses.
* **[!UICONTROL Player-ID]**: Die eindeutige Kennung der Mediensitzung.
* **[!UICONTROL Abspielleiste]**: Die aktuelle Position der Medienwiedergabe in Sekunden.
* **[!UICONTROL Details der Mediensitzung]**: Beim Senden eines Medienstartereignisses sollten die erforderlichen Details zur Mediensitzung angegeben werden.
* **[!UICONTROL Kapiteldetails]**: In diesem Abschnitt können Sie die Kapiteldetails beim Senden eines Kapitelstart-Medienereignisses angeben.
* **[!UICONTROL Advertising-Details]**: Beim Senden eines `AdBreakStart` -Ereignisses müssen Sie die erforderlichen Werbedetails angeben.
* **[!UICONTROL Advertising-Werbeunterbrechungsdetails]**: Details zum Anzeigen-Pod beim Senden eines `AdStart` -Ereignisses.
* **[!UICONTROL Fehlerdetails]**: Details zum Wiedergabefehler, der verfolgt wird.
* **[!UICONTROL Statusaktualisierungsdetails]**: Der Player-Status, der aktualisiert wird.
* **[!UICONTROL Benutzerdefinierte Metadaten]**: Die benutzerspezifischen Metadaten zum verfolgten Medienereignis.
* **[!UICONTROL Erlebnisqualität]**: Die Medienqualität der getrackten Erlebnisdaten.

## Media Analytics-Tracker abrufen {#get-media-analytics-tracker}

Mit dieser Aktion wird die veraltete Media Analytics-API abgerufen. Wenn die Aktion konfiguriert und ein Objektname angegeben wird, wird die veraltete Media Analytics-API in dieses Fensterobjekt exportiert. Wenn keines angegeben ist, wird es wie die aktuelle Medien-JS-Bibliothek nach `window.Media` exportiert.

![Bild der Platform-Benutzeroberfläche, das den Aktionstyp &quot;Get Media Analytics Tracker&quot;anzeigt.](assets/get-media-analytics-tracker.png)

## Umleiten mit Identität {#redirect-with-identity}

Verwenden Sie diesen Aktionstyp, um Identitäten von der aktuellen Seite für andere Domänen freizugeben. Diese Aktion ist für die Verwendung mit dem Ereignistyp **[!UICONTROL click]** und einer Wertvergleichsbedingung konzipiert. Weitere Informationen zur Verwendung dieses Aktionstyps finden Sie unter [Anhängen der Identität an URL mithilfe der Web SDK-Erweiterung](../../../../web-sdk/commands/appendidentitytourl.md#extension) .

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie ein besseres Verständnis davon haben, wie Sie Ihre Aktionen konfigurieren. Lesen Sie als Nächstes, wie Sie [Ihre Datenelementtypen konfigurieren](data-element-types.md).
