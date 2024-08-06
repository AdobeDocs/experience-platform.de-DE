---
title: Aktionstypen in der Adobe Experience Platform Web SDK-Erweiterung
description: Erfahren Sie mehr über die verschiedenen Aktionstypen, die von der Adobe Experience Platform Web SDK-Tag-Erweiterung bereitgestellt werden.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: c3b05dfd57b3335230e9abb40de6f2e1ee5ee6fa
workflow-type: tm+mt
source-wordcount: '2114'
ht-degree: 2%

---


# Aktionstypen

Nachdem Sie die Tag-Erweiterung [Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md) konfiguriert haben, müssen Sie Ihre Aktionstypen konfigurieren.

Auf dieser Seite werden die von der Tag-Erweiterung [Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md) unterstützten Aktionstypen beschrieben.

## Vorschläge anwenden {#apply-propositions}

Mit dem Aktionstyp **[!UICONTROL Vorschläge anwenden]** können Sie Vorschläge in Einzelseitenanwendungen rendern, ohne die Metriken zu erhöhen.

Dieser Aktionstyp ist beim Arbeiten mit Einzelseitenanwendungen nützlich, bei denen Teile der Seite erneut gerendert werden, wodurch möglicherweise bereits auf die Seite angewendete Personalisierungen überschrieben werden.

Sie können diesen Aktionstyp für verschiedene Anwendungsfälle verwenden, z. B.:

1. **Render mbox HTML offer**. Vorschläge, die explizit über einen Bereich oder eine Oberfläche von einer Aktion vom Typ **[!UICONTROL Ereignis senden]** angefordert werden, werden nicht automatisch gerendert. Sie können den Aktionstyp **[!UICONTROL Vorschläge anwenden]** verwenden, um dem Web SDK mitzuteilen, wo diese zu rendern sind, indem Sie die Metadaten für Vorschläge angeben.
2. **Rendern Sie die Angebote für eine Ansicht in einer Einzelseitenanwendung**. Wenn beim Rendern eines Ansichtsänderungsereignisses die Analysedaten noch nicht bereit sind, können Sie die Aktion **[!UICONTROL Vorschläge anwenden]** verwenden, um die Ansichtsvorschläge oben auf der Seite zu rendern. Weitere Informationen finden Sie unter [Anfang und Ende der Seitenereignisse (zweite Seitenansicht - Option 2)](../../../../web-sdk/use-cases/top-bottom-page-events.md) . Geben Sie dazu einen **[!UICONTROL Anzeigenamen]** in das Formular ein.
3. **Vorschläge erneut rendern**. Wenn Ihre Site zum erneuten Rendern von Inhalten ein Framework wie React verwendet, müssen Sie möglicherweise die Personalisierung erneut anwenden. In solchen Fällen können Sie hierzu den Aktionstyp **[!UICONTROL Vorschläge anwenden]** verwenden.

Dieser Aktionstyp sendet kein Anzeigeereignis für gerenderte Vorschläge. Sie verfolgt die gerenderten Vorschläge, damit sie in nachfolgende **[!UICONTROL Ereignis-Senden-Aufrufe]** einbezogen werden können.


![Platform-Tags-Benutzeroberfläche, die den Aktionstyp &quot;Vorschläge anwenden&quot;anzeigt.](assets/apply-propositions.png)

Dieser Aktionstyp unterstützt die folgenden Felder:

* **[!UICONTROL Vorschläge]**: Ein Array von Vorschlagsobjekten, die Sie erneut rendern möchten.
* **[!UICONTROL Name der Ansicht]**: Der Name der Ansicht, die gerendert werden soll.
* **[!UICONTROL Vorschlagsmetadaten]**: Ein Objekt, das bestimmt, wie HTML-Angebote angewendet werden können. Sie können diese Informationen entweder über das Formular oder über ein Datenelement bereitstellen. Sie enthält die folgenden Eigenschaften:
   * **[!UICONTROL Perimeter]**
   * **[!UICONTROL Selektor]**
   * **[!UICONTROL Aktionstyp]**

## Antwort anwenden {#apply-response}

Verwenden Sie den Aktionstyp **[!UICONTROL Antwort anwenden]** , wenn Sie basierend auf einer Antwort des Edge Networks verschiedene Aktionen durchführen möchten. Dieser Aktionstyp wird normalerweise in Hybridbereitstellungen verwendet, bei denen der Server einen ersten Aufruf an das Edge Network durchführt. Anschließend nimmt dieser Aktionstyp die Antwort aus diesem Aufruf und initialisiert das Web SDK im Browser.

Die Verwendung dieses Aktionstyps kann die Client-Ladezeiten für hybride Personalisierungsfälle verkürzen.

![Bild der Experience Platform-Benutzeroberfläche mit dem Aktionstyp &quot;Antwort anwenden&quot;.](assets/apply-response.png)

Dieser Aktionstyp unterstützt die folgenden Konfigurationsoptionen:

* **[!UICONTROL Instanz]**: Wählen Sie die verwendete Web SDK-Instanz aus.
* **[!UICONTROL Antwortheader]**: Wählen Sie das Datenelement aus, das ein Objekt zurückgibt, das die Header-Schlüssel und die vom Edge Network-Server-Aufruf zurückgegebenen Werte enthält.
* **[!UICONTROL Antworttext]**: Wählen Sie das Datenelement aus, das das Objekt zurückgibt, das die von der Edge Network-Antwort bereitgestellte JSON-Payload enthält.
* **[!UICONTROL visuelle Personalisierungsentscheidungen rendern]**: Aktivieren Sie diese Option, um den vom Edge Network bereitgestellten Personalisierungsinhalt automatisch wiederzugeben und den Inhalt vorab auszublenden, um Flackern zu vermeiden.

## Bewerten von Regelsätzen {#evaluate-rulesets}

Dieser Aktionstyp Trigger manuell die Regelsatzauswertung. Regelsätze werden von Adobe Journey Optimizer zurückgegeben, um Funktionen wie In-Browser-Nachrichten zu unterstützen.

![Bild der Experience Platform-Benutzeroberfläche, das den Aktionstyp Regelsätze auswerten anzeigt.](assets/evaluate-rulesets.png)

Dieser Aktionstyp unterstützt die folgenden Optionen:

* **[!UICONTROL visuelle Personalisierungsentscheidungen rendern]**: Aktivieren Sie diese Option, um visuelle Personalisierungsentscheidungen für die Regelsatzelemente zu rendern, die übereinstimmen.
* **[!UICONTROL Entscheidungskontext]**: Dies ist eine Schlüssel-Wert-Zuordnung, die beim Auswerten von Adobe Journey Optimizer-Regelsätzen für geräteübergreifende Entscheidungen verwendet wird. Sie können den Entscheidungskontext manuell oder über ein Datenelement bereitstellen.

## Media Analytics-Tracker abrufen {#get-media-analytics-tracker}

Mit dieser Aktion wird die veraltete Media Analytics-API abgerufen. Wenn die Aktion konfiguriert und ein Objektname angegeben wird, wird die veraltete Media Analytics-API in dieses Fensterobjekt exportiert. Wenn keines angegeben ist, wird es wie die aktuelle Medien-JS-Bibliothek nach `window.Media` exportiert.

![Bild der Platform-Benutzeroberfläche, das den Aktionstyp &quot;Get Media Analytics Tracker&quot;anzeigt.](assets/get-media-analytics-tracker.png)

## Umleiten mit Identität {#redirect-with-identity}

Verwenden Sie diesen Aktionstyp, um Identitäten von der aktuellen Seite für andere Domänen freizugeben. Diese Aktion ist für die Verwendung mit dem Ereignistyp **[!UICONTROL click]** und einer Wertvergleichsbedingung konzipiert. Weitere Informationen zur Verwendung dieses Aktionstyps finden Sie unter [Anhängen der Identität an URL mithilfe der Web SDK-Erweiterung](../../../../web-sdk/commands/appendidentitytourl.md#extension) .

## Ereignis senden {#send-event}

Sendet ein Ereignis an die Experience Platform, damit Platform die von Ihnen gesendeten Daten erfassen und darauf reagieren kann. Alle Daten, die Sie senden möchten, können im Feld **[!UICONTROL XDM-Daten]** gesendet werden. Verwenden Sie ein [!DNL JSON] -Objekt, das der Struktur Ihres [!DNL XDM]-Schemas entspricht. Dieses Objekt kann entweder auf Ihrer Seite oder über ein **[!UICONTROL benutzerdefinierter Code]** **[!UICONTROL Datenelement]** erstellt werden.

Der Aktionstyp **[!UICONTROL Ereignis senden]** unterstützt die unten beschriebenen Felder und Einstellungen. Diese Felder sind alle optional.

### Instanzeneinstellungen {#instance}

Verwenden Sie den Selektor **[!UICONTROL Instanz]** , um Ihre Web SDK-Instanz auszuwählen, die Sie konfigurieren möchten. Wenn Sie nur eine Instanz haben, wird sie vorausgewählt.

![UI-Bild für Platform-Tags mit den Instanzeinstellungen für den Aktionstyp &quot;Ereignis senden&quot;](assets/instance-settings.png)

* **[!UICONTROL Instanz]**: Wählen Sie die Web SDK-Instanz aus, die Sie konfigurieren möchten. Wenn Sie nur eine Instanz haben, wird sie vorausgewählt.
* **[!UICONTROL Geführte Ereignisse verwenden]**: Aktivieren Sie diese Option, um bestimmte Felder automatisch auszufüllen oder auszublenden, um einen bestimmten Anwendungsfall zu aktivieren. Durch Aktivierung dieser Option wird die Anzeige der folgenden Einstellungen Trigger.

  >[!NOTE]
  >
  >Die unten aufgeführten geführten Ereignisse beziehen sich auf [die Ereignisse oben und unten auf der Seite](../../../../web-sdk/use-cases/top-bottom-page-events.md).
   * **[!UICONTROL Personalisierung anfordern]**: Dieses Ereignis soll oben auf der Seite aufgerufen werden. Wenn diese Option aktiviert ist, werden durch dieses Ereignis die folgenden Felder festgelegt:
      * **[!UICONTROL Typ]**: **[!UICONTROL Abrufen des Entscheidungsvorschlags]**
      * **[!UICONTROL Ereignis &quot;Anzeige automatisch senden&quot;]**: **[!UICONTROL false]**
      * Um in diesem Fall die Personalisierung automatisch zu rendern, aktivieren Sie die Option **[!UICONTROL Entscheidungen zur visuellen Personalisierung rendern]** .
   * **[!UICONTROL Analyse erfassen]**: Dieses Ereignis soll am Ende der Seite aufgerufen werden. Wenn diese Option aktiviert ist, werden durch dieses Ereignis die folgenden Felder festgelegt:
      * **[!UICONTROL Wiedergegebene Vorschläge einschließen]**: **[!UICONTROL true]**
      * Die Einstellungen für **[!UICONTROL Personalization]** sind ausgeblendet


### Daten {#data}

![UI-Bild für Platform-Tags mit den Datenelementeinstellungen für den Aktionstyp &quot;Ereignis senden&quot;](assets/data.png)

* **[!UICONTROL Typ]**: Mit diesem Feld können Sie einen Ereignistyp angeben, der in Ihrem XDM-Schema aufgezeichnet wird. Weitere Informationen finden Sie unter [`type`](/help/web-sdk/commands/sendevent/type.md) im Befehl `sendEvent` .
* **[!UICONTROL XDM]**:
* **[!UICONTROL Daten]**: Verwenden Sie dieses Feld, um Daten zu senden, die nicht mit einem XDM-Schema übereinstimmen. Dieses Feld ist nützlich, wenn Sie versuchen, ein Adobe Target-Profil zu aktualisieren oder Target Recommendations-Attribute zu senden. Weitere Informationen finden Sie unter [`data`](/help/web-sdk/commands/sendevent/data.md) im Befehl `sendEvent` .
* **[!UICONTROL Wiedergegebene Vorschläge einschließen]**: Aktivieren Sie diese Option, um alle Vorschläge einzuschließen, die gerendert wurden, aber kein Anzeigeereignis gesendet wurde. Verwenden Sie dies gemeinsam mit deaktiviertem **[!UICONTROL Anzeigenereignis automatisch senden]** . Diese Einstellung aktualisiert das XDM-Feld `_experience.decisioning` mit Informationen zu den gerenderten Vorschlägen.
* **[!UICONTROL Dokument wird entladen]**: Aktivieren Sie diese Option, um sicherzustellen, dass die Ereignisse den Server erreichen, selbst wenn der Benutzer von der Seite weg navigiert. Dadurch können Ereignisse den Server erreichen, Antworten werden jedoch ignoriert.
* **[!UICONTROL Zusammenführungs-ID]**: **Dieses Feld ist veraltet**. Dadurch wird das XDM-Feld `eventMergeId` gefüllt.

### Personalisierung {#personalization}

![Benutzeroberflächenbild für Platform Tags mit den Personalization-Einstellungen für den Aktionstyp &quot;Ereignis senden&quot;](assets/personalization-settings.png)

* **[!UICONTROL Perimeter]**: Wählen Sie die Perimeter (Adobe Target [!DNL mboxes]) aus, die explizit aus der Personalisierung angefordert werden sollen. Sie können die Bereiche manuell eingeben oder ein Datenelement angeben.
* **[!UICONTROL Oberflächen]**: Legen Sie die Weboberflächen fest, die auf der Seite zur Personalisierung verfügbar sind. Weitere Informationen finden Sie in der [Adobe Journey Optimizer-Dokumentation](https://experienceleague.adobe.com/docs/journey-optimizer/using/web/create-web.html) .
* **visuelle Personalisierungsentscheidungen rendern:** Wenn Sie personalisierte Inhalte auf Ihrer Seite rendern möchten, aktivieren Sie das Kontrollkästchen **[!UICONTROL visuelle Personalisierungsentscheidungen rendern]** . Sie können bei Bedarf auch Entscheidungsbereiche und/oder Oberflächen angeben. Weitere Informationen zum Rendern personalisierter Inhalte finden Sie in der [Personalisierungsdokumentation](/help/web-sdk/personalization/rendering-personalization-content.md#automatically-rendering-content) .
* **[!UICONTROL Standardpersonalisierung anfordern]**: Mit diesem Abschnitt können Sie steuern, ob der seitenweite Umfang (globale Mbox) und die Standardoberfläche (Weboberfläche basierend auf der aktuellen URL) angefordert werden. Standardmäßig wird dies beim ersten `sendEvent` -Aufruf des Seitenladevorgangs automatisch angefordert. Sie können aus den folgenden Optionen auswählen:
   * **[!UICONTROL Automatisch]**: Dies ist das Standardverhalten. Fordern Sie nur die Standardpersonalisierung an, wenn diese noch nicht angefordert wurde. Dies entspricht `requestDefaultPersonalization` nicht im Web SDK-Befehl festgelegt.
   * **[!UICONTROL Aktiviert]**: Fordern Sie explizit den Seitenbereich und die Standardoberfläche an. Dadurch wird der SPA-Ansichts-Cache aktualisiert. Dies entspricht `requestDefaultPersonalization` , der auf `true` gesetzt ist.
   * **[!UICONTROL Deaktiviert]**: Unterdrückt explizit die Anforderung für den Seitenbereich und die Standardoberfläche. Dies entspricht `requestDefaultPersonalization` , der auf `false` gesetzt ist.
* **[!UICONTROL Entscheidungskontext]**: Dies ist eine Schlüssel-Wert-Zuordnung, die beim Auswerten von Adobe Journey Optimizer-Regelsätzen für geräteübergreifende Entscheidungen verwendet wird. Sie können den Entscheidungskontext manuell oder über ein Datenelement bereitstellen.

### Überschreibungen der Datastream-Konfiguration {#datastream-overrides}

Mit Datenstromüberschreibungen können Sie zusätzliche Konfigurationen für Ihre Datenströme definieren, die über das Web SDK an das Edge-Netzwerk übergeben werden.

Dies hilft Ihnen beim Trigger verschiedener Datenspeicherverhaltensweisen als der Standardeinstellungen, ohne einen neuen Datenspeicher zu erstellen oder Ihre vorhandenen Einstellungen zu ändern. Weitere Informationen finden Sie in der Dokumentation zu [Konfigurieren von Datastream-Überschreibungen](web-sdk-extension-configuration.md#datastream-overrides) .

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

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie ein besseres Verständnis davon haben, wie Sie Ihre Aktionen konfigurieren. Lesen Sie als Nächstes, wie Sie [Ihre Datenelementtypen konfigurieren](data-element-types.md).
