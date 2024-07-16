---
title: Aktivieren von Zielgruppendaten für Streaming-Ziele
type: Tutorial
description: Erfahren Sie, wie Sie die in Adobe Experience Platform vorhandenen Zielgruppen aktivieren, indem Sie sie Streaming-Zielen zuordnen.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 19%

---


# Aktivieren von Zielgruppen für Streaming-Ziele

>[!IMPORTANT]
> 
> * Um Zielgruppen zu aktivieren und den Schritt [Zuordnen](#mapping) des Workflows zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [.](/help/access-control/home.md#permissions)
> * Um Zielgruppen zu aktivieren, ohne den Schritt [Zuordnen](#mapping) des Workflows zu durchlaufen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Segment ohne Zuordnung aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [.](/help/access-control/home.md#permissions)
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}
> 
> Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

## Übersicht {#overview}

In diesem Artikel wird der Workflow erläutert, der zum Aktivieren von Zielgruppen in Adobe Experience Platform-Streaming-Zielen erforderlich ist.

## Voraussetzungen {#prerequisites}

Um Zielgruppen für Ziele zu aktivieren, müssen Sie erfolgreich [mit einem Ziel verbunden sein](./connect-destination.md). Wenn Sie das noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

## Auswählen des Ziels {#select-destination}

1. Navigieren Sie zu **[!UICONTROL Verbindungen und Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]**.

   ![Registerkarte &quot;Zielkatalog&quot;mit verschiedenen Streaming-Zielen.](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Wählen Sie **[!UICONTROL Zielgruppen aktivieren]** auf der Karte aus, die dem Ziel entspricht, in dem Sie Ihre Zielgruppen aktivieren möchten, wie in der Abbildung unten dargestellt.

   ![Aktivieren Sie das Steuerelement, das im Zielkatalog hervorgehoben ist.](../assets/ui/activate-segment-streaming-destinations/activate-audiences-button.png)

1. Wählen Sie die Zielverbindung aus, die Sie zum Aktivieren Ihrer Zielgruppen verwenden möchten, und wählen Sie dann **[!UICONTROL Weiter]** aus.

   ![Eine im Schritt Ziel auswählen hervorgehobene Zielverbindung.](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Wechseln Sie zum nächsten Abschnitt mit [Auswählen Ihrer Zielgruppen](#select-audiences).

## Audiences auswählen {#select-audiences}

Um die Zielgruppen auszuwählen, die Sie für das Ziel aktivieren möchten, aktivieren Sie die Kontrollkästchen links neben den Zielgruppennamen und wählen Sie dann **[!UICONTROL Weiter]** aus.

Je nach Herkunft können Sie aus mehreren Zielgruppentypen auswählen:

* **[!UICONTROL Segmentation Service]**: Zielgruppen, die innerhalb von Experience Platform vom Segmentation Service generiert werden. Weitere Informationen finden Sie in der [Dokumentation zur Segmentierung](../../segmentation/ui/overview.md) .
* **[!UICONTROL Benutzerdefinierter Upload]**: Zielgruppen, die außerhalb von Experience Platform generiert und als CSV-Dateien in Platform hochgeladen wurden. Weitere Informationen zu externen Zielgruppen finden Sie in der Dokumentation zum [Importieren einer Zielgruppe](../../segmentation/ui/audience-portal.md#import-audience).
* Andere Zielgruppentypen, die von anderen Adobe-Lösungen wie [!DNL Audience Manager] stammen.

![Mehrere im Schritt Zielgruppenauswahl hervorgehobene Zielgruppen.](../assets/ui/activate-segment-streaming-destinations/select-audiences.png)

## Zuordnen von Attributen und Identitäten {#mapping}

>[!IMPORTANT]
>
>Dieser Schritt gilt nur für einige Zielgruppen-Streaming-Ziele. Wenn Ihr Ziel keinen Schritt **[!UICONTROL Zuordnung]** aufweist, können Sie zur [Zielgruppenplanung](#scheduling) überspringen.
>
>Beim Aktivieren von Zielgruppen für Streaming-Ziele müssen Sie zusätzlich zu den Zielprofilattributen auch mindestens einen Zielidentitäts-Namespace *zuordnen.* Andernfalls werden die Zielgruppen nicht für die Zielplattform aktiviert.
> ![Bild des Zuordnungsschritts, der eine obligatorische Namespace-Zuordnung für die Identität anzeigt.](../assets/ui/activate-segment-streaming-destinations/identity-mapping-mandatory.png) {zoomable="yes"}


Bei einigen Zielgruppen-Streaming-Zielen müssen Sie Quellattribute oder Identitäts-Namespaces auswählen, um sie als Zielidentitäten im Ziel zuzuordnen.

1. Wählen Sie auf der Seite **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus.

   ![Fügen Sie das neue Zuordnungssteuerelement hervorgehoben hinzu.](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Wählen Sie den Pfeil rechts neben dem Eintrag **[!UICONTROL Quellfeld]** aus.

   ![Wählen Sie das Steuerelement des Quellfelds als hervorgehoben aus.](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. Verwenden Sie auf der Seite **[!UICONTROL Quellfeld auswählen]** die Optionen **[!UICONTROL Attribute auswählen]** oder **[!UICONTROL Identitäts-Namespace auswählen]** , um zwischen den beiden Kategorien der verfügbaren Quellfelder zu wechseln. Wählen Sie aus den verfügbaren [!DNL XDM] -Profilattributen und Identitäts-Namespaces diejenigen aus, die Sie dem Ziel zuordnen möchten, und wählen Sie dann **[!UICONTROL Auswählen]**.

   Verwenden Sie den Umschalter **[!UICONTROL Nur Felder mit Daten anzeigen]** , um nur Schemafelder anzuzeigen, die mit Werten gefüllt sind. Standardmäßig werden nur ausgefüllte Schemafelder angezeigt.

   ![Wählen Sie die Quellfeldseite aus, die mehrere verfügbare Quellfelder anzeigt.](../assets/ui/activate-segment-streaming-destinations/select-source-field-modal.png)

1. Wählen Sie die Schaltfläche rechts neben dem Eintrag **[!UICONTROL Zielfeld]** aus.

   ![Wählen Sie das Zielfeld hervorgehoben aus.](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. Wählen Sie auf der Seite **[!UICONTROL Zielfeld auswählen]** den Zielidentitäts-Namespace aus, dem Sie das Quellfeld zuordnen möchten, und wählen Sie **[!UICONTROL Auswählen]**.

   ![Wählen Sie die Zielfeldseite aus, die verfügbare Optionen für Zielfeldzuordnungen anzeigt.](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Um weitere Zuordnungen hinzuzufügen, wiederholen Sie die Schritte 1 bis 5.

### Transformation anwenden {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Transformation anwenden"
>abstract="Aktivieren Sie diese Option, wenn Sie nicht gehashte Quellfelder verwenden, damit diese automatisch von Adobe Experience Platform bei der Aktivierung gehasht werden."

Wenn Sie ungehashte Quellattribute Zielattributen zuordnen, von denen das Ziel erwartet, dass sie gehasht werden (z. B.: `email_lc_sha256` oder `phone_sha256`), aktivieren Sie die Option **Umwandlung anwenden**, damit Adobe Experience Platform die Quellattribute bei Aktivierung automatisch hasst.

![Wenden Sie das im Schritt Identitätszuordnung hervorgehobene Transformationssteuerelement an.](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Planen eines Zielgruppenexports {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="Enddatum"
>abstract="Dem Zielgruppenzeitplan kann kein Enddatum hinzugefügt werden."

Standardmäßig zeigt die Seite **[!UICONTROL Zielgruppenplan]** nur die neu ausgewählten Zielgruppen an, die Sie im aktuellen Aktivierungsablauf ausgewählt haben.

Um alle für Ihr Ziel aktivierten Zielgruppen anzuzeigen, verwenden Sie die Filteroption und deaktivieren Sie den Filter **[!UICONTROL Nur neue Zielgruppen anzeigen]** .

![Alle Zielgruppen](../assets/ui/activate-segment-streaming-destinations/all-audiences.png)

1. Wählen Sie auf der Seite **[!UICONTROL Zielgruppenplan]** jede Zielgruppe aus und konfigurieren Sie dann mithilfe der Selektoren **[!UICONTROL Startdatum]** und **[!UICONTROL Enddatum]** das Zeitintervall für das Senden von Daten an Ihr Ziel.

   ![Der Zielgruppenzeitplanfilter wurde hervorgehoben.](../assets/ui/activate-segment-streaming-destinations/audience-schedule.png)

   * Für einige Ziele müssen Sie den **[!UICONTROL Ursprung der Zielgruppe]** für jede Zielgruppe über das Dropdown-Menü unter den Kalenderauswahl auswählen. Wenn Ihr Ziel diesen Selektor nicht enthält, überspringen Sie diesen Schritt.

     ![ Dropdown-Liste Zuordnungs-ID markiert.](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Bei einigen Zielen müssen Sie [!DNL Platform] -Zielgruppen manuell ihrem Gegenstück im Ziel zuordnen. Wählen Sie dazu jede Zielgruppe aus und geben Sie dann die entsprechende Zielgruppen-ID aus der Zielplattform in das Feld **[!UICONTROL Zuordnungs-ID]** ein. Wenn Ihr Ziel dieses Feld nicht enthält, überspringen Sie diesen Schritt.

     ![Herkunft des Zielgruppen-Dropdown-Menüs hervorgehoben.](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Bei einigen Zielen müssen Sie beim Aktivieren von [!DNL IDFA] - oder [!DNL GAID] -Zielgruppen eine **[!UICONTROL App-ID]** eingeben. Wenn Ihr Ziel dieses Feld nicht enthält, überspringen Sie diesen Schritt.

     ![App-ID-Dropdown hervorgehoben.](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Wählen Sie **[!UICONTROL Weiter]** aus, um zur Seite [!UICONTROL Überprüfen] zu wechseln.

## Überprüfung {#review}

Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

![Auswahlzusammenfassung im Überprüfungsschritt.](../assets/ui/activate-segment-streaming-destinations/review.png)

### Auswertung der Einverständnisrichtlinie {#consent-policy-evaluation}

Wenn Ihr Unternehmen **Adobe Healthcare Shield** oder **Adobe Privacy &amp; Security Shield** erworben hat, wählen Sie **[!UICONTROL Aktuelle Einverständnisrichtlinien anzeigen]** aus, um zu sehen, welche Einverständnisrichtlinien angewendet werden und wie viele Profile in der Aktivierung enthalten sind. Weitere Informationen finden Sie unter [Bewertung von Zustimmungsrichtlinien](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) .

### Prüfungen von Datennutzungsrichtlinien {#data-usage-policy-checks}

Im Schritt **[!UICONTROL Überprüfen]** überprüft Experience Platform auch auf Verstöße gegen Datennutzungsrichtlinien. Nachstehend ist ein Beispiel angegeben, bei dem eine Richtlinie verletzt wird. Sie können den Aktivierungs-Workflow für die Zielgruppe erst abschließen, nachdem Sie den Verstoß behoben haben. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Verstöße gegen Datennutzungsrichtlinien](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) im Abschnitt zur Data Governance-Dokumentation.

![Ein Beispiel für einen Verstoß gegen die Datenrichtlinie, der im Aktivierungs-Workflow angezeigt wird.](../assets/common/data-policy-violation.png)

### Filtern von Zielgruppen {#filter-audiences}

Außerdem können Sie in diesem Schritt die verfügbaren Filter auf der Seite verwenden, um nur die Zielgruppen anzuzeigen, deren Zeitplan oder Zuordnung im Rahmen dieses Workflows aktualisiert wurde. Sie können auch umschalten, welche Tabellenspalten angezeigt werden sollen.

![Bildschirmaufzeichnung mit den verfügbaren Zielgruppenfiltern im Überprüfungsschritt.](../assets/ui/activate-segment-streaming-destinations/filter-audiences-review-step.gif)

Wenn Sie mit Ihrer Auswahl zufrieden sind und keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Beenden]** aus, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

## Überprüfung der Zielgruppenaktivierung {#verify}

Detaillierte Informationen zur Überwachung des Datenflusses zu Ihren Zielen finden Sie in der Dokumentation zur [Zielüberwachung](../../dataflows/ui/monitor-destinations.md) .

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Audience membership in the audience would be added and removed as users are qualified or disqualified for the activated audiences.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical audience qualifications are sent to [!DNL Facebook] when you activate the audiences to the destination.
-->
