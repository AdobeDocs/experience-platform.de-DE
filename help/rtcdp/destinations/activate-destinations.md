---
title: Profile und Segmente für ein Ziel aktivieren
seo-title: Profile und Segmente für ein Ziel aktivieren
description: Aktivieren Sie die Daten, die in der Echtzeit-Kundendatenplattform von Adobe vorhanden sind, indem Sie Segmente Zielen zuordnen. Gehen Sie dazu wie folgt vor.
seo-description: Aktivieren Sie die Daten, die in der Echtzeit-Kundendatenplattform von Adobe vorhanden sind, indem Sie Segmente Zielen zuordnen. Gehen Sie dazu wie folgt vor.
translation-type: tm+mt
source-git-commit: 7dafdf0dd1ad3af2defab3bf6b784fd37e777062
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 77%

---


# Profile und Segmente für ein Ziel aktivieren

Aktivieren Sie die Daten, die in der Echtzeit-Kundendatenplattform von Adobe vorhanden sind, indem Sie Segmente Zielen zuordnen. Gehen Sie dazu wie folgt vor.

## Voraussetzungen {#prerequisites}

Um Daten für Ziele aktivieren zu können, müssen Sie eine erfolgreiche [Verbindung zu einem Ziel](/help/rtcdp/destinations/assets/connect-destination.png) hergestellt haben. Wenn Sie das noch nicht getan haben, navigieren Sie zum [Zielkatalog](/help/rtcdp/destinations/destinations-catalog.md), durchsuchen Sie die unterstützten Ziele und richten Sie ein oder mehrere Ziele ein.

## Daten aktivieren {#activate-data}

1. Wählen Sie unter **[!UICONTROL Ziele > Durchsuchen]** das Ziel aus, an dem Sie Ihre Segmente aktivieren möchten.
2. Klicken Sie auf den Namen des Ziels. So gelangen Sie zum Aktivierungsfluss.
   ![Aktivierungsfluss](/help/rtcdp/destinations/assets/activate-flow.png)
Beachten Sie, dass sich, wenn für ein Ziel bereits ein Aktivierungsfluss vorhanden ist, die Segmente anzeigen lassen, die derzeit an das Ziel gesendet werden. Wählen Sie in der rechten Leiste die Option **[!UICONTROL Aktivierung bearbeiten]** und führen Sie die unten beschriebenen Schritte aus, um die Aktivierungsdetails zu ändern.
3. Wählen Sie **[!UICONTROL Aktivieren]**.
4. In the **[!UICONTROL Activate destination]** workflow, on the **[!UICONTROL Select Segments]** page, select which segments to send to the destination.
   ![Segment an Ziel](/help/rtcdp/destinations/assets/select-segments.png)
5. *Bedingt*. Dieser Schritt gilt nur für Segmente, die Cloud-Datenspeicherung-Zielen und E-Mail-Marketingzielen zugeordnet sind. <br> Wählen Sie auf der Seite **[!UICONTROL Zielattribute]** die Option **[!UICONTROL Neues Feld hinzufügen]** und wählen Sie die Attribute aus, die Sie an das Ziel senden möchten.
Wir empfehlen, eines der Attribute aus Ihrem Vereinigungsschema als [eindeutige Kennung](/help/rtcdp/destinations/email-marketing-destinations.md#identity) zu verwenden. Weiterführende Informationen zu obligatorischen Attributen finden Sie unter „Identität“ im Artikel [E-Mail-Marketing-Ziele](/help/rtcdp/destinations/email-marketing-destinations.md#identity).
   ![Zielattribute](/help/rtcdp/destinations/assets/destination-attributes.png)
6. On the **[!UICONTROL Segment schedule]** page, you can see the start date for sending data to the destination, as well as the frequency of sending data to the destination.

   >[!IMPORTANT]
   >
   >Bei Social-Zielen müssen Sie in diesem Schritt die Herkunft Ihrer Audience auswählen. Sie können mit dem nächsten Schritt nur fortfahren, nachdem Sie eine der Optionen in der Abbildung unten ausgewählt haben.

   ![Herkunft wählen](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

![Auswahl bestätigen](/help/rtcdp/destinations/assets/confirm-selection.png)

## Aktivierung bearbeiten {#edit-activation}

Gehen Sie wie folgt vor, um vorhandene Aktivierungsflüsse in der Echtzeit-Kundendatenplattform zu bearbeiten:

1. Wählen Sie in der linken Navigationsleiste **[!UICONTROL Ziele]**, klicken Sie dann auf die Registerkarte **[!UICONTROL Durchsuchen]** und klicken Sie auf den Zielnamen.
2. Wählen Sie in der rechten Leiste **[!UICONTROL Aktivierung bearbeiten]**, um zu ändern, welche Segmente an das Ziel gesendet werden.

## Überprüfen, ob die Segmentaktivierung erfolgreich war {#verify-activation}

### E-Mail-Marketing- und Cloud-Speicher-Ziele

Bei E-Mail-Marketing- und Cloud-Speicher-Zielen erstellt die Adobe-Echtzeit-CDP eine tabulatorgetrennte `.txt`- oder `.csv`-Datei am von Ihnen angegebenen Speicherort. An diesem Speicherort wird täglich eine neue Datei erstellt. Das Dateiformat lautet:
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

Dateien, die Sie an drei aufeinander folgenden Tagen erhalten, könnten wie folgt aussehen:

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

Das Vorhandensein dieser Dateien an Ihrem Speicherort bestätigt die erfolgreiche Aktivierung.

### Werbeziele

Markieren Sie das entsprechende Werbeziel, für das Sie Ihre Daten aktivieren. Wenn die Aktivierung erfolgreich war, werden in Ihrer Werbeplattform Zielgruppen ausgefüllt.

### Social-Netzwerkziele

Bei Facebook bedeutet eine erfolgreiche Aktivierung, dass eine benutzerdefinierte Facebook-Audience programmgesteuert im [Facebook Ads Manager](https://www.facebook.com/adsmanager/manage/)erstellt wird. Die Segmentmitgliedschaft in der Audience wird hinzugefügt und entfernt, da Benutzer für die aktivierten Segmente qualifiziert oder disqualifiziert sind.

## Aktivierung deaktivieren {#disable-activation}

Gehen Sie wie folgt vor, um einen vorhandenen Aktivierungsfluss zu deaktivieren:

1. Wählen Sie in der linken Navigationsleiste **[!UICONTROL Ziele]**, klicken Sie dann auf die Registerkarte **[!UICONTROL Durchsuchen]** und klicken Sie auf den Zielnamen.
2. Klicken Sie in der rechten Leiste auf das Steuerelement **[!UICONTROL Aktiviert]**, um den Status des Aktivierungsflusses zu ändern.
3. Wählen Sie im Fenster **Datenflussstatus aktualisieren** die Option **Bestätigen**, um den Aktivierungsfluss zu deaktivieren.

