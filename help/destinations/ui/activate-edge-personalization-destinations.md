---
title: Aktivieren von Zielgruppen für Edge-Personalisierungsziele
description: Erfahren Sie, wie Sie Zielgruppen von Adobe Experience Platform aus für Edge-Personalisierungsziele aktivieren können, um Anwendungsfälle für die Personalisierung von derselben Seite und nächsten Seiten zu nutzen.
type: Tutorial
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: 14dccb993b38ca352c6de3ed851bafe7c44ca631
workflow-type: tm+mt
source-wordcount: '1957'
ht-degree: 15%

---


# Aktivieren von Zielgruppen für Edge-Personalisierungsziele

## Übersicht {#overview}

Adobe Experience Platform verwendet [Edge-Segmentierung](../../segmentation/ui/edge-segmentation.md) zusammen mit [Edge-Zielen](/help/destinations/destination-types.md#edge-personalization-destinations), um Kunden die Erstellung und das Targeting von Zielgruppen in großem Maßstab in Echtzeit zu ermöglichen. Mit dieser Funktion können Sie Anwendungsfälle für die Personalisierung von derselben Seite und von der nächsten Seite konfigurieren.

Beispiele für Edge-Ziele sind die Verbindungen [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) und [Benutzerdefinierte Personalisierung](../../destinations/catalog/personalization/custom-personalization.md) .

>[!NOTE]
>
>Beim [ Konfigurieren der Adobe Target-Verbindung ](../catalog/personalization/adobe-target-connection.md) *ohne* mithilfe einer Datastraam-ID werden die in diesem Artikel beschriebenen Anwendungsfälle nicht unterstützt. Es werden nur Anwendungsfälle für die Personalisierung der nächsten Sitzung unterstützt, wenn kein Datastream vorhanden ist.

>[!IMPORTANT]
> 
> * Um Daten zu aktivieren und den Schritt [Zuordnen](#mapping) des Workflows zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [.](/help/access-control/home.md#permissions)
> * Um Daten zu aktivieren, ohne den Schritt [Zuordnen](#mapping) des Workflows zu durchlaufen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Segment ohne Zuordnung aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [.](/help/access-control/home.md#permissions)
>* Um *identities* zu exportieren, benötigen Sie die Zugriffssteuerungsberechtigung **[!UICONTROL Identitätsdiagramm anzeigen]** [ ](/help/access-control/home.md#permissions). <br> ![Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie den im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}
> 
> Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

In diesem Artikel wird der Workflow erläutert, der zum Aktivieren von Zielgruppen für Adobe Experience Platform Edge-Ziele erforderlich ist. Wenn diese Ziele zusammen mit [Kantensegmentierung](../../segmentation/ui/edge-segmentation.md) und der optionalen Zuordnung der Profilattribute](#mapping) verwendet werden, ermöglichen sie die Anwendungsfälle für die Personalisierung von derselben Seite und nächsten Seiten in Ihren Web- und mobilen Eigenschaften.[

Eine kurze Übersicht über die Konfiguration der Adobe Target-Verbindung für die Edge-Personalisierung finden Sie im folgenden Video.

>[!NOTE]
>
>Die Benutzeroberfläche von Experience Platform wird häufig aktualisiert und kann sich seit der Aufzeichnung dieses Videos geändert haben. Die aktuellsten Informationen finden Sie in den Konfigurationsschritten, die in den folgenden Abschnitten beschrieben werden.

>[!VIDEO](https://video.tv.adobe.com/v/3418799/?quality=12&learn=on)

Eine kurze Übersicht darüber, wie Sie Zielgruppen und Profilattribute für Adobe Target und benutzerdefinierte Personalisierungsziele freigeben können, finden Sie im folgenden Video.

>[!VIDEO](https://video.tv.adobe.com/v/3419036/?quality=12&learn=on)

## Anwendungsfälle {#use-cases}

Verwenden Sie Adobe-Personalisierungslösungen wie Adobe Target oder Ihre eigenen Personalisierungspartner-Plattformen (z. B. [!DNL Optimizely], [!DNL Pega]) sowie proprietäre Systeme (z. B. das interne CMS), um ein tieferes Kundenpersonalisierungs-Erlebnis über das Ziel [Benutzerspezifische Personalization](../catalog/personalization/custom-personalization.md) zu erzielen. Dies alles nutzt gleichzeitig auch Experience Platform Edge Network-Datenerfassungs- und Segmentierungsfunktionen.

Die unten beschriebenen Anwendungsfälle umfassen sowohl die Personalisierung der Site als auch zielgruppengerechte On-site-Werbung.

Um diese Anwendungsfälle zu aktivieren, benötigen Kunden eine schnelle, optimierte Methode, um sowohl Zielgruppen- als auch Profilattributinformationen von Experience Platform abzurufen und diese Informationen entweder an die [Adobe Target](../catalog/personalization/adobe-target-connection.md) - oder die [Custom Personalization](../catalog/personalization/custom-personalization.md) -Verbindungen in der Experience Platform-Benutzeroberfläche zu senden.

### Personalisierung auf derselben Seite {#same-page}

Ein Benutzer besucht eine Seite Ihrer Website. Sie können die aktuelle Seitenbesuchsinformationen (z. B. verweisende URL, Browsersprache, eingebettete Produktinformationen) verwenden, um die nächste Aktion oder Entscheidung (z. B. Personalisierung) auszuwählen, indem Sie die [Benutzerdefinierte Personalisierung](../catalog/personalization/custom-personalization.md)-Verbindung für Nicht-Adobe-Plattformen (z. B. [!DNL Pega], [!DNL Optimizely] oder andere Plattformen verwenden.)

### Personalisierung der nächsten Seite {#next-page}

Ein Benutzer besucht Seite A auf Ihrer Website. Auf der Grundlage dieser Interaktion hat sich der Benutzer für eine Reihe von Zielgruppen qualifiziert. Der Benutzer klickt dann auf einen Link, der ihn von Seite A zu Seite B bringt. Die Zielgruppen, für die sich der Benutzer während der vorherigen Interaktion auf Seite A qualifiziert hat, werden zusammen mit den durch den aktuellen Website-Besuch festgelegten Profilaktualisierungen verwendet, um die nächste Aktion oder Entscheidung zu ermöglichen (z. B. welches Werbebanner dem Besucher angezeigt werden soll oder im Fall von A/B-Tests, welche Version der Seite angezeigt werden soll).

### Personalisierung der nächsten Sitzung {#next-session}

Ein Benutzer besucht mehrere Seiten auf Ihrer Website. Auf der Grundlage dieser Interaktionen hat sich der Benutzer für eine Reihe von Zielgruppen qualifiziert. Der Benutzer beendet dann die aktuelle Browser-Sitzung.

Am folgenden Tag kehrt der Benutzer zur gleichen Kundenwebsite zurück. Die Zielgruppen, für die sie sich während der vorherigen Interaktion mit allen besuchten Webseiten qualifiziert hatten, sowie die durch den aktuellen Website-Besuch bestimmten Profilaktualisierungen werden verwendet, um die nächste Aktion/Entscheidung auszuwählen (z. B. welches Werbebanner dem Besucher angezeigt werden soll oder, im Fall von A/B-Tests, welche Version der Seite angezeigt werden soll).

### Personalisieren eines Homepage-Banners {#home-page-banner}

Ein häusliches Verleih- und Vertriebsunternehmen möchte seine Homepage mit einem Banner personalisieren, das auf den Zielgruppenqualifikationen in Adobe Experience Platform basiert. Das Unternehmen kann auswählen, welche Zielgruppen ein personalisiertes Erlebnis erhalten sollen, und diese Zielgruppen als Targeting-Kriterien für sein Target-Angebot an Adobe Target senden.

## Voraussetzungen {#prerequisites}

### Konfigurieren eines Datenspeichers in der Benutzeroberfläche für die Datenerfassung {#configure-datastream}

Der erste Schritt bei der Einrichtung Ihres Personalisierungsziels besteht darin, einen Datenstrom für das Experience Platform Web SDK zu konfigurieren. Dies erfolgt in der Benutzeroberfläche für die Datenerfassung.

Stellen Sie beim Konfigurieren des Datenstroms unter **[!UICONTROL Adobe Experience Platform]** sicher, dass sowohl **[!UICONTROL Edge-Segmentierung]** als auch **[!UICONTROL Personalisierungsziele]** ausgewählt sind.

>[!TIP]
>
>Ab der Version vom April 2024 müssen Sie bei der Konfiguration der Verbindung zu Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) nicht mehr das Kontrollkästchen Edge-Segmentierung aktivieren. [ In diesem Fall ist [Personalisierung der nächsten Sitzung](#next-session) der einzige verfügbare Anwendungsfall für die Personalisierung.

![Datenspeicherkonfiguration mit Edge-Segmentierung und Personalization-Zielen hervorgehoben!](../assets/ui/activate-edge-personalization-destinations/datastream-config.png)

Weitere Informationen zum Einrichten eines Datenstroms finden Sie in den Anweisungen in der [Dokumentation zum Platform Web SDK](../../datastreams/configure.md#aep).

### Erstellen einer [!DNL Active-On-Edge] -Zusammenführungsrichtlinie {#create-merge-policy}

Nachdem Sie Ihre Zielverbindung erstellt haben, müssen Sie eine [!DNL Active-On-Edge] -Zusammenführungsrichtlinie erstellen. Die [!DNL Active-On-Edge]-Zusammenführungsrichtlinie stellt sicher, dass Zielgruppen ständig [am Rand](../../segmentation/ui/edge-segmentation.md) ausgewertet werden und für den Anwendungsfall der Personalisierung in Echtzeit und auf der nächsten Seite verfügbar sind.

>[!IMPORTANT]
>
>Derzeit unterstützen Edge-Ziele nur die Aktivierung von Zielgruppen, die die als Standard festgelegte [Active-on-Edge-Zusammenführungsrichtlinie](../../segmentation/ui/segment-builder.md#merge-policies) verwenden. Wenn Sie Zielgruppen, die eine andere Zusammenführungsrichtlinie verwenden, Edge-Zielen zuordnen, werden diese Zielgruppen nicht ausgewertet.

Befolgen Sie die Anweisungen zum [Erstellen einer Zusammenführungsrichtlinie](../../profile/merge-policies/ui-guide.md#create-a-merge-policy) und stellen Sie sicher, dass Sie die **[!UICONTROL Active-On-Edge-Zusammenführungsrichtlinie]** aktivieren.

### Erstellen einer neuen Zielgruppe in Platform {#create-audience}

Nachdem Sie die Zusammenführungsrichtlinie [!DNL Active-On-Edge] erstellt haben, müssen Sie in Platform eine neue Zielgruppe erstellen.

Befolgen Sie das Handbuch [Audience Builder](../../segmentation/ui/segment-builder.md) , um Ihre neue Audience zu erstellen, und stellen Sie sicher, dass Sie [ihr ](../../segmentation/ui/segment-builder.md#merge-policies) die [!DNL Active-On-Edge] Zusammenführungsrichtlinie zuweisen, die Sie im vorherigen Schritt erstellt haben.

### Erstellen einer Zielverbindung {#connect-destination}

Nachdem Sie Ihren Datenstrom konfiguriert haben, können Sie mit der Konfiguration Ihres Personalisierungsziels beginnen.

Im [Tutorial zur Erstellung von Zielverbindungen](../ui/connect-destination.md) finden Sie detaillierte Anweisungen zum Erstellen einer neuen Zielverbindung.

Abhängig vom konfigurierten Ziel finden Sie in den folgenden Artikeln Informationen zu zielspezifischen Voraussetzungen und zugehörigen Informationen:

* [Adobe Target-Verbindung](../catalog/personalization/adobe-target-connection.md#parameters)
* [Benutzerdefinierte Personalisierungsverbindung](../catalog/personalization/custom-personalization.md#parameters)

## Auswählen des Ziels {#select-destination}

Nachdem Sie die Voraussetzungen erfüllt haben, können Sie jetzt das Edge-Personalisierungsziel auswählen, das für die Personalisierung der gleichen Seite und der nächsten Seite verwendet werden soll.

1. Navigieren Sie zu **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]**.

   ![Die Registerkarte &quot;Zielkatalog&quot;wurde in der Experience Platform-Benutzeroberfläche hervorgehoben.](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. Wählen Sie **[!UICONTROL Zielgruppen aktivieren]** auf der Karte aus, die dem Personalisierungsziel entspricht, in dem Sie Ihre Zielgruppen aktivieren möchten, wie in der Abbildung unten dargestellt.

   ![Aktivieren Sie die Zielgruppenkontrolle, die auf einer Zielkarte im Katalog hervorgehoben ist.](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. Wählen Sie die Zielverbindung aus, die Sie zum Aktivieren Ihrer Zielgruppen verwenden möchten, und wählen Sie dann **[!UICONTROL Weiter]** aus.

   ![Wählen Sie den Zielschritt im Aktivierungs-Workflow aus.](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. Wechseln Sie zum nächsten Abschnitt mit [Auswählen Ihrer Zielgruppen](#select-audiences).

## Audiences auswählen {#select-audiences}

Verwenden Sie die Kontrollkästchen links neben den Zielgruppennamen, um die Zielgruppen auszuwählen, die Sie für das Ziel aktivieren möchten, und wählen Sie dann **[!UICONTROL Weiter]** aus.

Um die Zielgruppen auszuwählen, die Sie für das Ziel aktivieren möchten, aktivieren Sie die Kontrollkästchen links neben den Zielgruppennamen und wählen Sie dann **[!UICONTROL Weiter]** aus.

Je nach Herkunft können Sie aus mehreren Zielgruppentypen auswählen:

* **[!UICONTROL Segmentation Service]**: Zielgruppen, die innerhalb von Experience Platform vom Segmentation Service generiert werden. Weitere Informationen finden Sie in der [Dokumentation zur Segmentierung](../../segmentation/ui/overview.md) .
* **[!UICONTROL Benutzerdefinierter Upload]**: Zielgruppen, die außerhalb von Experience Platform generiert und als CSV-Dateien in Platform hochgeladen wurden. Weitere Informationen zu externen Zielgruppen finden Sie in der Dokumentation zum [Importieren einer Zielgruppe](../../segmentation/ui/audience-portal.md#import-audience).
* Andere Zielgruppentypen, die von anderen Adobe-Lösungen wie [!DNL Audience Manager] stammen.

![Wählen Sie den Schritt Zielgruppen des Aktivierungs-Workflows aus, wobei mehrere Zielgruppen hervorgehoben sind.](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

## Zuordnungsattribute {#mapping}

>[!IMPORTANT]
>
>Profilattribute können vertrauliche Daten enthalten. Zum Schutz dieser Daten müssen Sie beim Konfigurieren des Ziels für eine attributbasierte Personalisierung die [Edge Network-Server-API](../../server-api/overview.md) verwenden, wenn Sie das Ziel für eine benutzerdefinierte Personalization ]**-Zielgruppe konfigurieren.**[!UICONTROL  Alle Server-API-Aufrufe müssen in einem [authentifizierten Kontext](../../server-api/authentication.md) durchgeführt werden.
>
><br>Wenn Sie bereits Web SDK oder Mobile SDK für Ihre Integration verwenden, können Sie Attribute über die Server-API abrufen, indem Sie eine serverseitige Integration hinzufügen.
>
><br>Wenn Sie die obigen Anforderungen nicht erfüllen, basiert die Personalisierung nur auf der Zielgruppenzugehörigkeit.

Wählen Sie die Attribute aus, auf deren Grundlage Sie die Anwendungsfälle der Personalisierung für Ihre Benutzer aktivieren möchten. Wenn sich also der Wert eines Attributs ändert oder einem Profil ein Attribut hinzugefügt wird, wird dieses Profil Mitglied der Zielgruppe und für das Personalisierungsziel aktiviert.

Das Hinzufügen von Attributen ist optional. Sie können weiterhin mit dem nächsten Schritt fortfahren und die Personalisierung der gleichen Seite und der nächsten Seite aktivieren, ohne Attribute auszuwählen. Wenn Sie in diesem Schritt keine Attribute hinzufügen, erfolgt die Personalisierung weiterhin basierend auf der Zielgruppenzugehörigkeit und den Qualifikationen der Identitätszuordnung für Profile.

![Bild, das den Zuordnungsschritt mit einem ausgewählten Attribut anzeigt.](../assets/ui/activate-edge-personalization-destinations/mapping-step.png)

### Quellattribute auswählen {#select-source-attributes}

Um Quellattribute hinzuzufügen, wählen Sie das Steuerelement **[!UICONTROL Neues Feld hinzufügen]** in der Spalte **[!UICONTROL Source-Feld]** aus und suchen oder navigieren Sie zum gewünschten XDM-Attributfeld, wie unten dargestellt.

![Bildschirmaufzeichnung, die zeigt, wie ein Zielattribut im Zuordnungsschritt ausgewählt wird.](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

### Zielattribute auswählen {#select-target-attributes}

Um Zielattribute hinzuzufügen, wählen Sie das Steuerelement **[!UICONTROL Neues Feld hinzufügen]** in der Spalte **[!UICONTROL Zielfeld]** aus und geben Sie den benutzerdefinierten Attributnamen ein, dem Sie das Quellattribut zuordnen möchten.

>[!NOTE]
>
>Die Auswahl der Zielattribute gilt nur für den Aktivierungs-Workflow [Benutzerdefinierter Personalization](../catalog/personalization/custom-personalization.md) , um die Zuordnung von Anzeigenamenfeldern in der Zielplattform zu unterstützen.

![Bildschirmaufzeichnung, die zeigt, wie ein XDM-Attribut im Zuordnungsschritt ausgewählt wird](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)

## Planen eines Zielgruppenexports {#scheduling}

Standardmäßig zeigt die Seite [!UICONTROL Zielgruppenplan] nur die neu ausgewählten Zielgruppen an, die Sie im aktuellen Aktivierungsablauf ausgewählt haben.

Um alle für Ihr Ziel aktivierten Zielgruppen anzuzeigen, verwenden Sie die Filteroption und deaktivieren Sie den Filter **[!UICONTROL Nur neue Zielgruppen anzeigen]** .

![Der Filter &quot;Alle Zielgruppen&quot;wurde hervorgehoben.](../assets/ui/activate-edge-personalization-destinations/all-audiences.png)

Wählen Sie auf der Seite **[!UICONTROL Zielgruppenplan]** jede Zielgruppe aus und konfigurieren Sie dann mithilfe der Selektoren **[!UICONTROL Startdatum]** und **[!UICONTROL Enddatum]** das Zeitintervall für das Senden von Daten an Ihr Ziel.

![Schritt Zielgruppenplanung des Aktivierungs-Workflows mit hervorgehobenem Start- und Enddatum.](../assets/ui/activate-edge-personalization-destinations/audience-schedule.png)

Wählen Sie **[!UICONTROL Weiter]** aus, um zur Seite [!UICONTROL Überprüfen] zu wechseln.

## Überprüfung {#review}

Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

![Auswahlzusammenfassung im Überprüfungsschritt.](../assets/ui/activate-edge-personalization-destinations/review.png)

### Auswertung der Einverständnisrichtlinie {#consent-policy-evaluation}

Wenn Ihr Unternehmen **Adobe Healthcare Shield** oder **Adobe Privacy &amp; Security Shield** erworben hat, wählen Sie **[!UICONTROL Aktuelle Einverständnisrichtlinien anzeigen]** aus, um zu sehen, welche Einverständnisrichtlinien angewendet werden und wie viele Profile in der Aktivierung enthalten sind. Weitere Informationen finden Sie unter [Bewertung von Zustimmungsrichtlinien](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) .

### Prüfungen von Datennutzungsrichtlinien {#data-usage-policy-checks}

Im Schritt **[!UICONTROL Überprüfen]** überprüft Experience Platform auch auf Verstöße gegen Datennutzungsrichtlinien. Nachstehend ist ein Beispiel angegeben, bei dem eine Richtlinie verletzt wird. Sie können den Aktivierungs-Workflow für die Zielgruppe erst abschließen, nachdem Sie den Verstoß behoben haben. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Verstöße gegen Datennutzungsrichtlinien](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) im Abschnitt zur Data Governance-Dokumentation.

![Ein Beispiel für eine Verletzung einer Datenrichtlinie.](../assets/common/data-policy-violation.png)

### Filtern von Zielgruppen {#filter-audiences}

In diesem Schritt können Sie die verfügbaren Filter auf der Seite verwenden, um nur die Zielgruppen anzuzeigen, deren Zeitplan oder Zuordnung im Rahmen dieses Workflows aktualisiert wurde. Sie können auch umschalten, welche Tabellenspalten angezeigt werden sollen.

![Bildschirmaufzeichnung mit den verfügbaren Zielgruppenfiltern im Überprüfungsschritt.](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)

Wenn Sie mit Ihrer Auswahl zufrieden sind und keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Beenden]** aus, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify audience activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->
