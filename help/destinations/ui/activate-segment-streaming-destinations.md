---
title: Aktivieren von Zielgruppendaten für Streaming-Ziele
type: Tutorial
description: Erfahren Sie, wie Sie Ihre Zielgruppen in Adobe Experience Platform aktivieren, indem Sie sie Streaming-Zielen zuordnen.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 19%

---


# Aktivieren von Zielgruppen für Streaming-Ziele

>[!IMPORTANT]
> 
> * Zum Aktivieren von Zielgruppen und Aktivieren [Zuordnungsschritts](#mapping) des Workflows sind die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **&#x200B;**&#x200B;Segmente anzeigen[ erforderlich](/help/access-control/home.md#permissions).
> * Um Zielgruppen zu aktivieren, ohne den [Zuordnungsschritt](#mapping) des Workflows zu durchlaufen, benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Segment ohne Zuordnung aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions).
>* Zum Exportieren *Identitäten* benötigen Sie die Berechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffssteuerung](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}
> 
> Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

## Übersicht {#overview}

In diesem Artikel wird der Workflow erläutert, der zum Aktivieren von Zielgruppen in Adobe Experience Platform-Streaming-Zielen erforderlich ist.

## Voraussetzungen {#prerequisites}

Um Zielgruppen für Ziele aktivieren zu können, müssen Sie erfolgreich [mit einem Ziel verbunden](./connect-destination.md). Wenn Sie das noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

## Auswählen des Ziels {#select-destination}

1. Navigieren Sie zu **[!UICONTROL Verbindungen und Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]**.

   ![Registerkarte Zielkatalog mit verschiedenen Streaming-Zielen.](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Wählen Sie **[!UICONTROL Zielgruppen aktivieren]** auf der Karte, die dem Zielort entspricht, an dem Sie Ihre Zielgruppen aktivieren möchten, wie in der Abbildung unten dargestellt.

   ![Im Zielkatalog hervorgehobenes Steuerelement „Aktivieren“.](../assets/ui/activate-segment-streaming-destinations/activate-audiences-button.png)

1. Wählen Sie die Zielverbindung aus, die Sie zum Aktivieren Ihrer Zielgruppen verwenden möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**.

   ![Eine Zielverbindung, die im Schritt „Ziel auswählen“ hervorgehoben ist.](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Gehen Sie zum nächsten Abschnitt, um [Ihre Zielgruppen auswählen](#select-audiences).

## Audiences auswählen {#select-audiences}

Um die Zielgruppen auszuwählen, die Sie für das Ziel aktivieren möchten, aktivieren Sie die Kontrollkästchen links neben den Zielgruppennamen und klicken Sie dann auf **[!UICONTROL Weiter]**.

Je nach Herkunft können Sie aus verschiedenen Arten von Zielgruppen auswählen:

* **[!UICONTROL Segmentierungs-Service]**: Zielgruppen, die in Experience Platform vom Segmentierungs-Service generiert werden. Weitere Informationen finden Sie [Segmentierungsdokumentation](../../segmentation/ui/overview.md) .
* **[!UICONTROL Benutzerdefinierter Upload]**: Zielgruppen, die außerhalb von Experience Platform generiert und als CSV-Dateien in Experience Platform hochgeladen werden. Weitere Informationen zu externen Zielgruppen finden Sie in der Dokumentation unter [Importieren einer Zielgruppe](../../segmentation/ui/audience-portal.md#import-audience).
* Andere Arten von Zielgruppen, die aus anderen Adobe-Lösungen wie [!DNL Audience Manager] stammen.

![Mehrere Zielgruppen, die im Schritt „Zielgruppen auswählen“ hervorgehoben sind.](../assets/ui/activate-segment-streaming-destinations/select-audiences.png)

## Zuordnen von Attributen und Identitäten {#mapping}

>[!IMPORTANT]
>
>Dieser Schritt gilt nur für einige Zielgruppen-Streaming-Ziele. Wenn Ihr Ziel nicht über einen Schritt **[!UICONTROL Zuordnung]** verfügt, fahren Sie mit [Zielgruppen-Planung](#scheduling) fort.
>
>Beim Aktivieren von Zielgruppen für Streaming-Ziele müssen Sie zusätzlich zu *Zielprofilattributen auch mindestens* Zielidentitäts-Namespace zuordnen. Andernfalls werden die Zielgruppen nicht für die Zielplattform aktiviert.
> ![Abbildung des Zuordnungsschritts, der eine obligatorische Identitäts-Namespace-Zuordnung anzeigt.](../assets/ui/activate-segment-streaming-destinations/identity-mapping-mandatory.png) {zoomable="yes"}


Bei einigen Zielgruppen-Streaming-Zielen müssen Sie Quellattribute oder Identity-Namespaces auswählen, die als Zielidentitäten im Ziel zugeordnet werden sollen.

1. Wählen Sie auf **[!UICONTROL Seite]** Zuordnung“ **[!UICONTROL Neue Zuordnung hinzufügen]** aus.

   ![Neues Zuordnungssteuerelement hinzufügen hervorgehoben.](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Wählen Sie den Pfeil rechts neben dem Eintrag **[!UICONTROL Quellfeld]** aus.

   ![Hervorgehobene Steuerung zur Auswahl des Quellfelds.](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. Verwenden Sie auf der **[!UICONTROL Quellfeld auswählen]** die Optionen **[!UICONTROL Attribute auswählen]** oder **[!UICONTROL Identity-Namespace auswählen]**, um zwischen den beiden Kategorien verfügbarer Quellfelder zu wechseln. Wählen Sie aus den verfügbaren [!DNL XDM] Profilattributen und Identity-Namespaces die Namen aus, die Sie dem Ziel zuordnen möchten, und wählen Sie dann **[!UICONTROL Auswählen]**.

   Verwenden Sie den Umschalter **[!UICONTROL Nur Felder mit Daten anzeigen]**, um nur Schemafelder anzuzeigen, die mit Werten gefüllt sind. Standardmäßig werden nur ausgefüllte Schemafelder angezeigt.

   ![Seite „Quellfeld auswählen“ mit mehreren verfügbaren Quellfeldern.](../assets/ui/activate-segment-streaming-destinations/select-source-field-modal.png)

1. Wählen Sie die Schaltfläche rechts neben dem Eintrag **[!UICONTROL Zielfeld]** aus.

   ![Zielfeld auswählen hervorgehoben.](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. Wählen **[!UICONTROL auf der Seite]** Zielfeld auswählen“ den Zielidentitäts-Namespace aus, dem Sie das Quellfeld zuordnen möchten, und wählen Sie **[!UICONTROL Auswählen]**.

   ![Seite „Zielfeld auswählen“ mit verfügbaren Optionen für Zielfeldzuordnungen.](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Um weitere Zuordnungen hinzuzufügen, wiederholen Sie die Schritte 1 bis 5.

### Transformation anwenden {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Transformation anwenden"
>abstract="Aktivieren Sie diese Option, wenn Sie nicht gehashte Quellfelder verwenden, damit diese automatisch von Adobe Experience Platform bei der Aktivierung gehasht werden."

Wenn Sie ungehashte Quellattribute Zielattributen zuordnen, von denen das Ziel erwartet, dass sie gehasht werden (z. B.: `email_lc_sha256` oder `phone_sha256`), aktivieren Sie die Option **Umwandlung anwenden**, damit Adobe Experience Platform die Quellattribute bei Aktivierung automatisch hasst.

![hervorgehobenes Steuerelement „Umwandlung anwenden“ im Schritt „Identitätszuordnung“.](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Planen eines Zielgruppenexports {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="Enddatum"
>abstract="Dem Zielgruppenzeitplan kann kein Enddatum hinzugefügt werden."

Standardmäßig werden auf der **[!UICONTROL Zielgruppen-Zeitplan]** nur die neu ausgewählten Zielgruppen angezeigt, die Sie im aktuellen Aktivierungsfluss ausgewählt haben.

Um alle für Ihr Ziel aktivierten Zielgruppen anzuzeigen, verwenden Sie die Filteroption und deaktivieren Sie den Filter **[!UICONTROL Nur neue Zielgruppen anzeigen]**.

![Alle Zielgruppen](../assets/ui/activate-segment-streaming-destinations/all-audiences.png)

1. Wählen Sie auf **[!UICONTROL Seite Zielgruppen]** jede Zielgruppe aus und verwenden Sie dann die Selektoren **[!UICONTROL Startdatum]** und **[!UICONTROL Enddatum]** zum Konfigurieren des Zeitintervalls für den Versand von Daten an Ihr Ziel.

   ![Filter für Zielgruppen-Zeitplan hervorgehoben.](../assets/ui/activate-segment-streaming-destinations/audience-schedule.png)

   * Für einige Ziele müssen Sie den **[!UICONTROL Ursprung der Zielgruppe]** für jede Zielgruppe mithilfe des Dropdown-Menüs unter den Kalenderselektoren auswählen. Wenn Ihr Ziel diesen Selektor nicht enthält, überspringen Sie diesen Schritt.

     ![Dropdown-Liste „Zuordnungs-ID“ hervorgehoben.](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Bei einigen Zielen müssen Sie [!DNL Experience Platform] Zielgruppen manuell ihrem Gegenstück im Ziel zuordnen. Wählen Sie dazu jede Zielgruppe aus und geben Sie dann die entsprechende Zielgruppen-ID aus der Zielplattform im Feld **[!UICONTROL Zuordnungs-ID]** ein. Wenn Ihr Ziel dieses Feld nicht enthält, überspringen Sie diesen Schritt.

     ![Herkunft des Zielgruppen-Dropdown hervorgehoben.](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Für einige Ziele müssen Sie beim Aktivieren von [!DNL IDFA] oder [!DNL GAID] Zielgruppen eine **[!UICONTROL App]** ID“ eingeben. Wenn Ihr Ziel dieses Feld nicht enthält, überspringen Sie diesen Schritt.

     ![Dropdown-Liste „App-ID“ hervorgehoben.](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Wählen Sie **[!UICONTROL Weiter]** aus, um zur Seite [!UICONTROL Überprüfen] zu wechseln.

## Überprüfung {#review}

Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

![Zusammenfassung der Auswahl im Überprüfungsschritt.](../assets/ui/activate-segment-streaming-destinations/review.png)

### Auswertung der Einverständnisrichtlinie {#consent-policy-evaluation}

Wenn Ihr Unternehmen **Adobe Healthcare Shield** oder **Adobe Privacy &amp; Security Shield** erworben hat, wählen Sie **[!UICONTROL Aktuelle Einverständnisrichtlinien anzeigen]** aus, um zu sehen, welche Einverständnisrichtlinien angewendet werden und wie viele Profile in der Aktivierung enthalten sind. Weitere Informationen finden [ unter ](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) der Einverständnisrichtlinie .

### Prüfung der Datennutzungsrichtlinien {#data-usage-policy-checks}

Im Schritt **[!UICONTROL Überprüfen]** prüft Experience Platform auch, ob Verstöße gegen Datennutzungsrichtlinien vorliegen. Nachstehend ist ein Beispiel angegeben, bei dem eine Richtlinie verletzt wird. Sie können den Zielgruppenaktivierungs-Workflow erst abschließen, nachdem Sie den Verstoß behoben haben. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Verstöße gegen Datennutzungsrichtlinien](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) im Dokumentationsabschnitt zur Data Governance.

![Ein Beispiel für eine Datenrichtlinienverletzung, das im Aktivierungs-Workflow angezeigt wird.](../assets/common/data-policy-violation.png)

### Audiences filtern {#filter-audiences}

In diesem Schritt können Sie auch die auf der Seite verfügbaren Filter verwenden, um nur die Zielgruppen anzuzeigen, deren Zeitplan oder Zuordnung im Rahmen dieses Workflows aktualisiert wurde. Sie können auch umschalten, welche Tabellenspalten angezeigt werden sollen.

![Bildschirmaufzeichnung mit den verfügbaren Zielgruppenfiltern im Überprüfungsschritt.](../assets/ui/activate-segment-streaming-destinations/filter-audiences-review-step.gif)

Wenn Sie mit Ihrer Auswahl zufrieden sind und keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Beenden]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

## Zielgruppenaktivierung überprüfen {#verify}

In der [Dokumentation zur Zielüberwachung](../../dataflows/ui/monitor-destinations.md) finden Sie detaillierte Informationen darüber, wie Sie den Datenfluss zu Ihren Zielen überwachen.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Audience membership in the audience would be added and removed as users are qualified or disqualified for the activated audiences.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical audience qualifications are sent to [!DNL Facebook] when you activate the audiences to the destination.
-->
