---
title: Aktivieren von Zielgruppendaten für Streaming-Ziele
type: Tutorial
description: Erfahren Sie, wie Sie die in Adobe Experience Platform vorhandenen Zielgruppen aktivieren, indem Sie sie Streaming-Zielen zuordnen.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: 34ae6f0f791a40584c2d476ed715bb7c5b733c42
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 20%

---


# Aktivieren von Zielgruppen für Streaming-Ziele

>[!IMPORTANT]
> 
> * So aktivieren Sie Zielgruppen und aktivieren die [Zuordnungsschritt](#mapping) des Workflows benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions).
> * So aktivieren Sie Zielgruppen, ohne die [Zuordnungsschritt](#mapping) des Workflows benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Segment ohne Zuordnung aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions).
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}
> 
> Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

## Übersicht {#overview}

In diesem Artikel wird der Workflow erläutert, der zum Aktivieren von Zielgruppen in Adobe Experience Platform-Streaming-Zielen erforderlich ist.

## Voraussetzungen {#prerequisites}

Um Zielgruppen für Ziele aktivieren zu können, müssen Sie erfolgreich [mit Ziel verbunden](./connect-destination.md). Wenn Sie das noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

## Auswählen des Ziels {#select-destination}

1. Navigieren Sie zu **[!UICONTROL Verbindungen und Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]**.

   ![Registerkarte Zielkatalog mit verschiedenen Streaming-Zielen.](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Auswählen **[!UICONTROL Aktivieren von Zielgruppen]** auf der Karte, die dem Ziel entspricht, in dem Sie Ihre Zielgruppen aktivieren möchten, wie in der Abbildung unten dargestellt.

   ![Aktivieren Sie die Kontrolle, die im Zielkatalog hervorgehoben ist.](../assets/ui/activate-segment-streaming-destinations/activate-audiences-button.png)

1. Wählen Sie die Zielverbindung aus, die Sie zum Aktivieren Ihrer Zielgruppen verwenden möchten, und wählen Sie dann **[!UICONTROL Nächste]**.

   ![Eine Zielverbindung, die im Schritt Ziel auswählen hervorgehoben ist.](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Zum nächsten Abschnitt wechseln, um [Zielgruppen auswählen](#select-audiences).

## Audiences auswählen {#select-audiences}

Um die Zielgruppen auszuwählen, die Sie für das Ziel aktivieren möchten, aktivieren Sie die Kontrollkästchen links neben den Zielgruppennamen und wählen Sie **[!UICONTROL Nächste]**.

Je nach Herkunft können Sie aus mehreren Zielgruppentypen auswählen:

* **[!UICONTROL Segmentierungsdienst]**: Vom Segmentation-Dienst innerhalb von Experience Platform generierte Zielgruppen. Siehe [Segmentierungsdokumentation](../../segmentation/ui/overview.md) für weitere Details.
* **[!UICONTROL Benutzerdefinierter Upload]**: Zielgruppen, die außerhalb von Experience Platform generiert und als CSV-Dateien in Platform hochgeladen wurden. Weitere Informationen zu externen Zielgruppen finden Sie in der Dokumentation unter [Audience importieren](../../segmentation/ui/overview.md#import-audience).
* Andere Zielgruppentypen, die von anderen Adobe-Lösungen stammen, z. B. [!DNL Audience Manager].

![Mehrere im Schritt Zielgruppen auswählen hervorgehobene Zielgruppen.](../assets/ui/activate-segment-streaming-destinations/select-audiences.png)

## Zuordnen von Attributen und Identitäten {#mapping}

>[!IMPORTANT]
>
>Dieser Schritt gilt nur für einige Zielgruppen-Streaming-Ziele. Wenn Ihr Ziel keine **[!UICONTROL Zuordnung]** Schritt, zum [Zielgruppenplanung](#scheduling).

Bei einigen Zielgruppen-Streaming-Zielen müssen Sie Quellattribute oder Identitäts-Namespaces auswählen, um sie als Zielidentitäten im Ziel zuzuordnen.

1. Im **[!UICONTROL Zuordnung]** Seite, auswählen **[!UICONTROL Neues Mapping hinzufügen]**.

   ![Fügen Sie ein neues Zuordnungssteuerelement hinzu, das hervorgehoben ist.](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Wählen Sie den Pfeil rechts neben dem Eintrag **[!UICONTROL Quellfeld]** aus.

   ![Wählen Sie Quellfeldsteuerung hervorgehoben aus.](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. Im **[!UICONTROL Quellfeld auswählen]** Seite, verwenden Sie die **[!UICONTROL Attribute auswählen]** oder **[!UICONTROL Identitäts-Namespace auswählen]** Optionen, um zwischen den beiden Kategorien der verfügbaren Quellfelder zu wechseln. In der [!DNL XDM] Profilattribute und Identitäts-Namespaces, die Sie dem Ziel zuordnen möchten, auswählen und dann **[!UICONTROL Auswählen]**.

   ![Wählen Sie die Quellfeldseite aus, die mehrere verfügbare Quellfelder anzeigt.](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. Wählen Sie die Schaltfläche rechts neben dem **[!UICONTROL Zielfeld]** eingeben.

   ![Wählen Sie Zielfeld hervorgehoben aus.](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. Im **[!UICONTROL Zielgruppenfeld auswählen]** Seite, wählen Sie den Zielidentitäts-Namespace aus, dem Sie das Quellfeld zuordnen möchten, und wählen Sie **[!UICONTROL Auswählen]**.

   ![Wählen Sie die Zielfeldseite aus, auf der die verfügbaren Optionen für Zielfeldzuordnungen angezeigt werden.](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Um weitere Zuordnungen hinzuzufügen, wiederholen Sie die Schritte 1 bis 5.

### Transformation anwenden {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Transformation anwenden"
>abstract="Aktivieren Sie diese Option, wenn Sie nicht gehashte Quellfelder verwenden, damit diese automatisch von Adobe Experience Platform bei der Aktivierung gehasht werden."

Wenn Sie ungehashte Quellattribute Zielattributen zuordnen, von denen das Ziel erwartet, dass sie gehasht werden (z. B.: `email_lc_sha256` oder `phone_sha256`), aktivieren Sie die Option **Umwandlung anwenden**, damit Adobe Experience Platform die Quellattribute bei Aktivierung automatisch hasst.

![Wenden Sie die Transformationssteuerung an, die im Schritt Identitätszuordnung hervorgehoben ist.](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Planen eines Zielgruppenexports {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="Enddatum"
>abstract="Dem Zielgruppenzeitplan kann kein Enddatum hinzugefügt werden."

Standardmäßig wird die Variable **[!UICONTROL Zielgruppenplanung]** zeigt nur die neu ausgewählten Zielgruppen an, die Sie im aktuellen Aktivierungsablauf ausgewählt haben.

Um alle für Ihr Ziel aktivierten Zielgruppen anzuzeigen, verwenden Sie die Filteroption und deaktivieren Sie die **[!UICONTROL Nur neue Zielgruppen anzeigen]** Filter.

![Alle Zielgruppen](../assets/ui/activate-segment-streaming-destinations/all-audiences.png)

1. Im **[!UICONTROL Zielgruppenplanung]** Seite, wählen Sie jede Zielgruppe aus und verwenden Sie dann die **[!UICONTROL Startdatum]** und **[!UICONTROL Enddatum]** Selektoren zum Konfigurieren des Zeitintervalls für das Senden von Daten an Ihr Ziel.

   ![Filter für Zielgruppenzeitpläne hervorgehoben.](../assets/ui/activate-segment-streaming-destinations/audience-schedule.png)

   * Bei einigen Zielen müssen Sie die **[!UICONTROL Ursprung der Zielgruppe]** für jede Zielgruppe mithilfe des Dropdown-Menüs unter den Kalenderselektoren. Wenn Ihr Ziel diesen Selektor nicht enthält, überspringen Sie diesen Schritt.

     ![Dropdown-Liste Zuordnungs-ID hervorgehoben.](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Für einige Ziele müssen Sie die Zuordnung manuell vornehmen [!DNL Platform] Zielgruppen zu ihrem Gegenstück im Ziel. Wählen Sie dazu die einzelnen Zielgruppen aus und geben Sie dann die entsprechende Zielgruppen-ID aus der Zielplattform im **[!UICONTROL Zuordnungs-ID]** -Feld. Wenn Ihr Ziel dieses Feld nicht enthält, überspringen Sie diesen Schritt.

     ![Herkunft des Zielgruppen-Dropdown hervorgehoben.](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Für einige Ziele müssen Sie eine **[!UICONTROL App-ID]** beim Aktivieren [!DNL IDFA] oder [!DNL GAID] Zielgruppen. Wenn Ihr Ziel dieses Feld nicht enthält, überspringen Sie diesen Schritt.

     ![Dropdown-Liste App-ID hervorgehoben.](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Auswählen **[!UICONTROL Nächste]** , um zu [!UICONTROL Überprüfen] Seite.

## Überprüfung {#review}

Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

![Auswahlzusammenfassung im Überprüfungsschritt.](../assets/ui/activate-segment-streaming-destinations/review.png)

### Auswertung der Einverständnisrichtlinie {#consent-policy-evaluation}

Wenn Ihr Unternehmen **Adobe Healthcare Shield** oder **Adobe Privacy &amp; Security Shield** erworben hat, wählen Sie **[!UICONTROL Aktuelle Einverständnisrichtlinien anzeigen]** aus, um zu sehen, welche Einverständnisrichtlinien angewendet werden und wie viele Profile in der Aktivierung enthalten sind. Informationen [Bewertung der Einwilligungsrichtlinie](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) für weitere Informationen.

### Prüfungen von Datennutzungsrichtlinien {#data-usage-policy-checks}

Im **[!UICONTROL Überprüfen]** -Schritt, überprüft Experience Platform auch auf Verstöße gegen Datennutzungsrichtlinien. Nachstehend ist ein Beispiel angegeben, bei dem eine Richtlinie verletzt wird. Sie können den Aktivierungs-Workflow für die Zielgruppe erst abschließen, nachdem Sie den Verstoß behoben haben. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Verstöße gegen Datennutzungsrichtlinien](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) im Abschnitt Data Governance-Dokumentation .

![Ein Beispiel für einen Verstoß gegen die Datenrichtlinie, der im Aktivierungs-Workflow angezeigt wird.](../assets/common/data-policy-violation.png)

### Filtern von Zielgruppen {#filter-audiences}

Außerdem können Sie in diesem Schritt die verfügbaren Filter auf der Seite verwenden, um nur die Zielgruppen anzuzeigen, deren Zeitplan oder Zuordnung im Rahmen dieses Workflows aktualisiert wurde. Sie können auch umschalten, welche Tabellenspalten angezeigt werden sollen.

![Bildschirmaufzeichnung mit den verfügbaren Zielgruppenfiltern im Überprüfungsschritt.](../assets/ui/activate-segment-streaming-destinations/filter-audiences-review-step.gif)

Wenn Sie mit Ihrer Auswahl zufrieden sind und keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Beenden]** , um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

## Überprüfung der Zielgruppenaktivierung {#verify}

Überprüfen Sie die [Zielüberwachungsdokumentation](../../dataflows/ui/monitor-destinations.md) für detaillierte Informationen zur Überwachung des Datenflusses zu Ihren Zielen.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Audience membership in the audience would be added and removed as users are qualified or disqualified for the activated audiences.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical audience qualifications are sent to [!DNL Facebook] when you activate the audiences to the destination.
-->
