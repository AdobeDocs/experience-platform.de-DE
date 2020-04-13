---
title: Profile und Segmente für ein Ziel aktivieren
seo-title: Profile und Segmente für ein Ziel aktivieren
description: Aktivieren Sie die Daten, die in der Echtzeit-Kundendatenplattform von Adobe vorhanden sind, indem Sie Segmente Zielen zuordnen. Gehen Sie dazu wie folgt vor.
seo-description: Aktivieren Sie die Daten, die in der Echtzeit-Kundendatenplattform von Adobe vorhanden sind, indem Sie Segmente Zielen zuordnen. Gehen Sie dazu wie folgt vor.
translation-type: tm+mt
source-git-commit: 2eddd5bb7b62dcc414ad906647b05ce10c766ac6

---


# Profile und Segmente für ein Ziel aktivieren

Aktivieren Sie die Daten, die in der Echtzeit-Kundendatenplattform von Adobe vorhanden sind, indem Sie Segmente Zielen zuordnen. Gehen Sie dazu wie folgt vor.

## Voraussetzungen {#prerequisites}

Um Daten für Ziele aktivieren zu können, müssen Sie eine erfolgreiche [Verbindung zu einem Ziel](/help/rtcdp/destinations/assets/connect-destination.png) hergestellt haben. Wenn Sie das noch nicht getan haben, navigieren Sie zum [Zielkatalog](/help/rtcdp/destinations/destinations-catalog.md), durchsuchen Sie die unterstützten Ziele und richten Sie ein oder mehrere Ziele ein.

## Daten aktivieren {#activate-data}

1. In **[!UICONTROL Destinations > Browse]**, select the destination where you want to activate your segments.
2. Klicken Sie auf den Namen des Ziels. So gelangen Sie zum Aktivierungsfluss.
   ![Aktivierungsfluss](/help/rtcdp/destinations/assets/activate-flow.png)
Beachten Sie, dass sich, wenn für ein Ziel bereits ein Aktivierungsfluss vorhanden ist, die Segmente anzeigen lassen, die derzeit an das Ziel gesendet werden. Select **[!UICONTROL Edit activation]** in the right rail and follow the steps below to modify the activation details.
3. Select **[!UICONTROL Activate]**;
4. Wählen Sie im **[!UICONTROL Activate destination]** Workflow auf der **[!UICONTROL Select Segments]** Seite die Segmente aus, die an das Ziel gesendet werden sollen.
   ![Segment an Ziel](/help/rtcdp/destinations/assets/select-segments.png)
5. *Bedingt*. Dieser Schritt gilt nur für Segmente, die E-Mail-Marketing-Zielen zugeordnet sind. <br> Wählen Sie auf der **[!UICONTROL Destination Attributes]** Seite die Attribute aus, die Sie an das Ziel senden möchten, **[!UICONTROL Add new field]** und wählen Sie sie aus.
Wir empfehlen, eines der Attribute aus Ihrem Vereinigungsschema als [eindeutige Kennung](/help/rtcdp/destinations/email-marketing-destinations.md#identity) zu verwenden. Weiterführende Informationen zu obligatorischen Attributen finden Sie unter „Identität“ im Artikel [E-Mail-Marketing-Ziele](/help/rtcdp/destinations/email-marketing-destinations.md#identity).
   ![Zielattribute](/help/rtcdp/destinations/assets/destination-attributes.png)
6. On the **[!UICONTROL Segment schedule]** page, you can see the start date for sending data to the destination, as well as the frequency of sending data to the destination.

   >[!IMPORTANT]
   >
   >Bei Social-Zielen müssen Sie in diesem Schritt die Herkunft Ihrer Audience auswählen. Sie können mit dem nächsten Schritt nur fortfahren, nachdem Sie eine der Optionen in der Abbildung unten ausgewählt haben.

   ![Herkunft wählen](/help/rtcdp/destinations/assets/choose-data-origin.png)

7. On the **[!UICONTROL Review]** page, you can see a summary of your selection. Select **[!UICONTROL Cancel]** to break up the flow, **[!UICONTROL Back]** to modify your settings, or **[!UICONTROL Finish]** to confirm your selection and start sending data to the destination.

![Auswahl bestätigen](/help/rtcdp/destinations/assets/confirm-selection.png)

## Aktivierung bearbeiten {#edit-activation}

Gehen Sie wie folgt vor, um vorhandene Aktivierungsflüsse in der Echtzeit-Kundendatenplattform zu bearbeiten:

1. Select **[!UICONTROL Destinations]** in the left navigation bar, then click the **[!UICONTROL Browse]** tab, and click the destination name.
2. Select **[!UICONTROL Edit activation]** in the right rail to change which segments to send to the destination.

## Überprüfen, ob die Segmentaktivierung erfolgreich war {#verify-activation}

### E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele

For email marketing destinations and cloud storage destinations, Adobe Real-time CDP creates a tab-delimited `.txt` or `.csv` file in the storage location that you provided. An diesem Speicherort wird täglich eine neue Datei erstellt. Das Dateiformat lautet:
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

1. Select **[!UICONTROL Destinations]** in the left navigation bar, then click the **[!UICONTROL Browse]** tab, and click the destination name.
2. Click the **[!UICONTROL Enabled]** control in the right rail to change the activation flow state.
3. Wählen Sie im Fenster **Datenflussstatus aktualisieren** die Option **Bestätigen**, um den Aktivierungsfluss zu deaktivieren.

