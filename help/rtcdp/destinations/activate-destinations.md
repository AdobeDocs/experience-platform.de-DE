---
title: Profile und Segmente für ein Ziel aktivieren
seo-title: Profile und Segmente für ein Ziel aktivieren
description: Aktivieren Sie die Daten, die in der Echtzeit-Kundendatenplattform von Adobe vorhanden sind, indem Sie Segmente Zielen zuordnen. Gehen Sie dazu wie folgt vor.
seo-description: Aktivieren Sie die Daten, die in der Echtzeit-Kundendatenplattform von Adobe vorhanden sind, indem Sie Segmente Zielen zuordnen. Gehen Sie dazu wie folgt vor.
translation-type: tm+mt
source-git-commit: 237ca5fc950b46ae4718850ab1360cdf52b8b112
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 53%

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
5. *Bedingt*. Dieser Schritt unterscheidet sich je nach Zieltyp, in dem Sie Ihre Segmente aktivieren. <br> Wählen Sie für *E-Mail-Marketing-Ziele* und *Cloud-Datenspeicherung-Ziele* auf der Seite &quot;Attribute **[!UICONTROL auswählen]** &quot; **[!UICONTROL Hinzufügen neues Feld]** und wählen Sie die Attribute aus, die Sie an das Ziel senden möchten.
Wir empfehlen, eines der Attribute aus Ihrem Vereinigungsschema als [eindeutige Kennung](/help/rtcdp/destinations/email-marketing-destinations.md#identity) zu verwenden. Weiterführende Informationen zu obligatorischen Attributen finden Sie unter „Identität“ im Artikel [E-Mail-Marketing-Ziele](/help/rtcdp/destinations/email-marketing-destinations.md#identity).
   ![Zielattribute](/help/rtcdp/destinations/assets/select-attributes-step.png)

   <br> 

   Bei *Social-Zielen* können Sie im Schritt zur **[!UICONTROL Identitätszuordnung]** Quellattribute auswählen, die als Zielgruppen-Identitäten im Ziel zugeordnet werden sollen. Dieser Schritt ist entweder optional oder obligatorisch, je nachdem, welche primäre Identität Sie im Schema verwenden. <br> 

   *E-Mail-Adresse als primäre Identität*: Wenn Sie die E-Mail-Adresse als primäre Identität in Ihrem Schema verwenden, können Sie den Schritt für die Identitätszuordnung überspringen, wie nachfolgend gezeigt:

   ![E-Mail-Adresse als Identität](/help/rtcdp/destinations/assets/email-as-identity.gif)

   <br> 

   *Eine weitere ID als primäre Identität*: Wenn Sie eine andere ID wie *Belohnungs-ID* oder *Loyalität-ID* als primäre Identität in Ihrem Schema verwenden, müssen Sie die E-Mail-Adresse aus Ihrem Identitäts-Schema manuell als Zielgruppen-ID im Social-Ziel zuordnen, wie nachfolgend gezeigt:

   ![Loyalität-ID als Identität](/help/rtcdp/destinations/assets/rewardsid-as-identity.gif)


   Wählen Sie `Email_LC_SHA256` als Zielgruppen-ID aus, wenn Sie bei der Datenerfassung auf der Adobe Experience Platform entsprechend den Anforderungen [für das](/help/rtcdp/destinations/facebook-destination.md#email-hashing-requirements)E-Mail-Hashing in Facebook Kundenadressen mit Hashing versehen haben. <br> Wählen Sie `Email` als Zielgruppen-ID aus, wenn die von Ihnen verwendeten E-Mail-Adressen nicht mit Hashing versehen werden. Adobe CDP in Echtzeit hash die E-Mail-Adressen, um die Facebook-Anforderungen zu erfüllen.

   ![Identitätszuordnung nach dem Ausfüllen von Feldern](/help/rtcdp/destinations/assets/identity-mapping.png)

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

>[!TIP]
>
>Die Integration von Adobe Echtzeit-CDP und Facebook unterstützt historische Audiencen-Backups. Alle historischen Segmentqualifikationen werden an Facebook gesendet, wenn Sie die Segmente an das Ziel aktivieren.

## Aktivierung deaktivieren {#disable-activation}

Gehen Sie wie folgt vor, um einen vorhandenen Aktivierungsfluss zu deaktivieren:

1. Wählen Sie in der linken Navigationsleiste **[!UICONTROL Ziele]**, klicken Sie dann auf die Registerkarte **[!UICONTROL Durchsuchen]** und klicken Sie auf den Zielnamen.
2. Klicken Sie in der rechten Leiste auf das Steuerelement **[!UICONTROL Aktiviert]**, um den Status des Aktivierungsflusses zu ändern.
3. Wählen Sie im Fenster **Datenflussstatus aktualisieren** die Option **Bestätigen**, um den Aktivierungsfluss zu deaktivieren.

Generieren Sie in AWS Kinesis einen Zugriffsschlüssel - ein Schlüssel-Paar für den geheimen Zugriff, um Adobe Echtzeit-CDP Zugriff auf Ihr AWS-Kinesis-Konto zu gewähren. Weitere Informationen finden Sie in der [AWS-Kinesis-Dokumentation](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html).