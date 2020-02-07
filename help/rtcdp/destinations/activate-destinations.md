---
title: Profile und Segmente zu einem Ziel aktivieren
seo-title: Profile und Segmente zu einem Ziel aktivieren
description: Aktivieren Sie die Daten, die Sie in der Adobe Echtzeit-Kundendatenplattform haben, indem Sie Segmente Zielen zuordnen. Gehen Sie wie folgt vor, um dies zu erreichen.
seo-description: Aktivieren Sie die Daten, die Sie in der Adobe Echtzeit-Kundendatenplattform haben, indem Sie Segmente Zielen zuordnen. Gehen Sie wie folgt vor, um dies zu erreichen.
translation-type: tm+mt
source-git-commit: 3b9584cca8943c52bb3d8e4512d327d3dbeb9e04

---


# Profile und Segmente zu einem Ziel aktivieren

Aktivieren Sie die Daten, die Sie in der Adobe Echtzeit-Kundendatenplattform haben, indem Sie Segmente Zielen zuordnen. Gehen Sie wie folgt vor, um dies zu erreichen.

## Voraussetzungen  {#prerequisites}

Um Daten an Ziele zu aktivieren, müssen Sie erfolgreich eine [Verbindung zu einem Ziel](/help/rtcdp/destinations/assets/connect-destination.png)hergestellt haben. Wenn Sie dies noch nicht getan haben, gehen Sie zum [Zielkatalog](/help/rtcdp/destinations/destinations-catalog.md), suchen Sie die unterstützten Ziele und richten Sie ein oder mehrere Ziele ein.

## Daten aktivieren {#activate-data}

1. Wählen Sie unter **Ziele > Durchsuchen** das Ziel aus, an dem Sie Ihre Segmente aktivieren möchten.
2. Klicken Sie auf den Namen des Ziels. Dadurch gelangen Sie zum Fluss Aktivieren.
   ![activate-flow](/help/rtcdp/destinations/assets/activate-flow.png)Beachten Sie, dass, wenn für ein Ziel bereits ein Aktivierungsablauf vorhanden ist, die Segmente angezeigt werden, die derzeit an das Ziel gesendet werden. Wählen Sie in der rechten Leiste die Option Aktivierung **bearbeiten** und befolgen Sie die unten stehenden Schritte, um die Aktivierungsdetails zu ändern.
3. Wählen Sie **Aktivieren**.
4. Wählen Sie im Assistenten **zum Aktivieren des Ziels** auf der Seite &quot;Segmente **auswählen** &quot;aus, welche Segmente an das Ziel gesendet werden sollen.
   ![segment-to-destination](/help/rtcdp/destinations/assets/select-segments.png)
5. *Bedingt*. Dieser Schritt gilt nur für Segmente, die E-Mail-Marketingzielen zugeordnet sind. <br> Wählen Sie auf der Seite **Zielattribute** die Option Neues Feld ****hinzufügen und wählen Sie die Attribute aus, die Sie an das Ziel senden möchten.
Es wird empfohlen, eines der Attribute als [eindeutige Kennung](/help/rtcdp/destinations/email-marketing-destinations.md#identity) aus Ihrem gewerkschaftlichen Schema zu verwenden. Weitere Informationen zu obligatorischen Attributen finden Sie unter Identität im Artikel [E-Mail-Marketing-Ziele](/help/rtcdp/destinations/email-marketing-destinations.md#identity) .
   ![destination-attributes](/help/rtcdp/destinations/assets/destination-attributes.png)
6. Auf der Seite &quot; **Plan** &quot;können Sie das Startdatum für das Senden der Daten an das Ziel sowie die Häufigkeit des Sendens der Daten an das Ziel sehen.
7. Auf der Seite &quot; **Überprüfen** &quot;wird eine Zusammenfassung Ihrer Auswahl angezeigt. Wählen Sie &quot; **Abbrechen** &quot;, um den Fluss zu unterbrechen, &quot; **Zurück** &quot;, um die Einstellungen zu ändern, oder &quot; **Fertig stellen** &quot;, um Ihre Auswahl zu bestätigen und Daten an das Ziel zu senden.

![verify-selection](/help/rtcdp/destinations/assets/confirm-selection.png)

## Aktivierung bearbeiten {#edit-activation}

Gehen Sie wie folgt vor, um vorhandene Aktivierungsabläufe in Echtzeit-CDP zu bearbeiten:

1. Wählen Sie **Ziele** in der linken Navigationsleiste aus, klicken Sie dann auf die Registerkarte &quot; **Durchsuchen** &quot;und klicken Sie auf den Zielnamen.
2. Wählen Sie in der rechten Leiste Aktivierung **** bearbeiten, um zu ändern, welche Segmente an das Ziel gesendet werden sollen.

## Überprüfen Sie, ob die Segmentaktivierung erfolgreich war. {#verify-activation}

### E-Mail-Marketingziele

Für E-Mail-Marketing-Ziele erstellt Adobe Echtzeit-CDP eine tabulatorgetrennte Datei `.txt` oder `.csv` Datei im von Ihnen angegebenen Speicherort. Sie erwarten, dass täglich eine neue Datei an Ihrem Speicherort erstellt wird. The file format is:
`<destination name>id<destination id><timestamp-yyyymmddhhmmss>`

Die Dateien, die Sie an drei aufeinander folgenden Tagen erhalten würden, könnten wie folgt aussehen:

```
Salesforce_id3544_20191120110000.csv
Salesforce_id3544_20191121123000.csv
Salesforce_id3544_20191122124530.csv
```

Das Vorhandensein dieser Dateien in Ihrem Speicherort ist eine Bestätigung für eine erfolgreiche Aktivierung.

### Werbeziele

Überprüfen Sie das entsprechende Werbeziel, an dem Sie Ihre Daten aktivieren. Wenn die Aktivierung erfolgreich war, werden Zielgruppen in Ihrer Werbeplattform aufgefüllt.

## Aktivierung deaktivieren {#disable-activation}

Gehen Sie wie folgt vor, um einen vorhandenen Aktivierungsablauf zu deaktivieren:

1. Wählen Sie **Ziele** in der linken Navigationsleiste aus, klicken Sie dann auf die Registerkarte &quot; **Durchsuchen** &quot;und klicken Sie auf den Zielnamen.
2. Klicken Sie in der rechten Leiste auf das Steuerelement **[!UICONTROL Aktiviert]** , um den Aktivierungsfluss zu ändern.
3. Wählen Sie im Fenster Datenflussstatus **aktualisieren** die Option **Bestätigen** , um den Aktivierungsablauf zu deaktivieren.

