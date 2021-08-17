---
keywords: Profilattribute aktivieren; Ziele aktivieren; Daten aktivieren; E-Mail-Marketing-Ziele aktivieren; Aktivieren von Cloud-Speicher-Zielen
title: Aktivieren von Zielgruppendaten für Streaming-Profil-Export-Ziele
type: Tutorial
seo-title: Aktivieren von Zielgruppendaten für Streaming-Profil-Export-Ziele
description: Erfahren Sie, wie Sie die in Adobe Experience Platform vorhandenen Zielgruppendaten aktivieren können, indem Sie Segmente an profilbasierte Ziele senden.
seo-description: Erfahren Sie, wie Sie die in Adobe Experience Platform vorhandenen Zielgruppendaten aktivieren können, indem Sie Segmente an profilbasierte Ziele senden.
source-git-commit: 02c22453470d55236d4235c479742997e8407ef3
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 14%

---


# Aktivieren von Zielgruppendaten für Streaming-Profil-Export-Ziele

## Übersicht {#overview}

In diesem Artikel wird der Workflow erläutert, der zum Aktivieren von Zielgruppendaten in profilbasierten Adobe Experience Platform-Zielen wie Amazon Kinesis erforderlich ist.

## Voraussetzungen {#prerequisites}

Um Daten für Ziele aktivieren zu können, müssen Sie über eine erfolgreiche [Verbindung zu einem Ziel](./connect-destination.md) verfügen. Wenn Sie dies noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

## Ziel auswählen {#select-destination}

1. Gehen Sie zu **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Durchsuchen]** aus.

   ![Registerkarte &quot;Ziel durchsuchen&quot;](../assets/ui/activate-streaming-profile-destinations/browse-tab.png)

1. Wählen Sie die Schaltfläche **[!UICONTROL Segmente hinzufügen]** aus, die dem Ziel entspricht, an dem Sie Ihre Segmente aktivieren möchten, wie in der Abbildung unten dargestellt.

   ![Schaltflächen aktivieren](../assets/ui/activate-streaming-profile-destinations/activate-buttons-browse.png)

1. Navigieren Sie zum nächsten Abschnitt [wählen Sie Ihre Segmente](#select-segments) aus.

## Segmente auswählen {#select-segments}

Verwenden Sie die Kontrollkästchen links neben den Segmentnamen, um die Segmente auszuwählen, die Sie für das Ziel aktivieren möchten, und wählen Sie dann **[!UICONTROL Weiter]** aus.

![Segmente auswählen](../assets/ui/activate-streaming-profile-destinations/select-segments.png)

## Profilattribute auswählen {#select-attributes}

Wählen Sie die Profilattribute aus, die Sie an das Ziel senden möchten.

>[!NOTE]
>
> Adobe Experience Platform füllt Ihre Auswahl mit vier empfohlenen, häufig verwendeten Attributen aus Ihrem Schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Dateiexporte variieren auf folgende Weise, je nachdem, ob `segmentMembership.status` ausgewählt ist:
* Wenn das Feld `segmentMembership.status` ausgewählt ist, enthalten exportierte Dateien **[!UICONTROL Aktive]** Mitglieder im ersten vollständigen Snapshot und **[!UICONTROL Aktive]** und **[!UICONTROL Abgelaufene]** Mitglieder in nachfolgenden inkrementellen Exporten.
* Wenn das Feld `segmentMembership.status` nicht ausgewählt ist, enthalten exportierte Dateien nur **[!UICONTROL aktive]**-Mitglieder im ersten vollständigen Snapshot und in nachfolgenden inkrementellen Exporten.

![empfohlene Attribute](../assets/ui/activate-streaming-profile-destinations/attributes-default.png)

1. Wählen Sie auf der Seite **[!UICONTROL Attribute]** auswählen **[!UICONTROL Neues Feld hinzufügen]** aus.

   ![Neues Mapping hinzufügen](../assets/ui/activate-streaming-profile-destinations/add-new-field.png)

1. Wählen Sie den Pfeil rechts neben dem Eintrag **[!UICONTROL Schema field]** aus.

   ![Quellfeld auswählen](../assets/ui/activate-streaming-profile-destinations/select-schema-field.png)

1. Wählen Sie auf der Seite **[!UICONTROL Feld]** auswählen die XDM-Attribute aus, die Sie an das Ziel senden möchten, und wählen Sie dann **[!UICONTROL Auswählen]**.

   ![Quellfeldseite auswählen](../assets/ui/activate-streaming-profile-destinations/target-field-page.png)


1. Um weitere Zuordnungen hinzuzufügen, wiederholen Sie die Schritte 1 bis 3 und wählen Sie dann **[!UICONTROL Weiter]** aus.

## Überprüfung {#review}

Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

>[!IMPORTANT]
>
>In diesem Schritt prüft Adobe Experience Platform, ob Verstöße gegen Datennutzungsrichtlinien vorliegen. Im Folgenden finden Sie ein Beispiel, bei dem eine Richtlinie verletzt wird. Sie können den Workflow zur Segmentaktivierung erst abschließen, nachdem Sie den Verstoß behoben haben. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Richtliniendurchsetzung](../../rtcdp/privacy/data-governance-overview.md#enforcement) im Abschnitt zur Data Governance-Dokumentation.

![Verletzung von Datenrichtlinien](../assets/common/data-policy-violation.png)

Wenn keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Beenden]** aus, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

![Überprüfung](../assets/ui/activate-streaming-profile-destinations/review.png)

## Segmentaktivierung überprüfen {#verify}


Für E-Mail-Marketing-Ziele und Cloud-Speicher-Ziele erstellt Adobe Experience Platform eine tabulatorgetrennte `.csv`-Datei am von Ihnen angegebenen Speicherort. An diesem Speicherort wird täglich eine neue Datei erstellt. Das standardmäßige Dateiformat lautet:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

Dateien, die Sie an drei aufeinander folgenden Tagen erhalten, könnten wie folgt aussehen:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

Das Vorhandensein dieser Dateien an Ihrem Speicherort bestätigt die erfolgreiche Aktivierung. Um zu verstehen, wie die exportierten Dateien strukturiert sind, können Sie [eine .csv-Beispieldatei](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv) herunterladen. Diese Beispieldatei enthält die Profilattribute `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear` und `personalEmail.address`.
