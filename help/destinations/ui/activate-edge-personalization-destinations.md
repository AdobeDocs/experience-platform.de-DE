---
title: Aktivieren von Zielgruppen für Edge-Personalisierungsziele
description: Erfahren Sie, wie Sie Zielgruppen aus Adobe Experience Platform für Personalisierungs-Anwendungsfälle der gleichen Seite und der nächsten Seite für Edge-Ziele aktivieren.
type: Tutorial
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1885'
ht-degree: 8%

---


# Aktivieren von Zielgruppen für Edge-Personalisierungsziele

## Überblick {#overview}

Adobe Experience Platform verwendet [Edge-](../../segmentation/methods/edge-segmentation.md)) zusammen mit [Edge-Zielen](/help/destinations/destination-types.md#edge-personalization-destinations), damit Kundinnen und Kunden Zielgruppen in großem Umfang in Echtzeit erstellen und ansprechen können. Mit dieser Funktion können Sie Anwendungsfälle für die Personalisierung von derselben Seite und von der nächsten Seite konfigurieren.

Beispiele für Edge-Ziele sind die [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md)- und [Custom Personalization](../../destinations/catalog/personalization/custom-personalization.md)-Verbindungen.

>[!NOTE]
>
>Beim [Konfigurieren der Adobe Target](../catalog/personalization/adobe-target-connection.md)Verbindung *ohne* mithilfe einer Datenstrom-ID werden die in diesem Artikel beschriebenen Anwendungsfälle nicht unterstützt. Es werden nur Anwendungsfälle für die Personalisierung der nächsten Sitzung unterstützt, wenn kein Datenstrom vorhanden ist.

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren und den [Zuordnungsschritt](#mapping) des Workflows zu aktivieren, benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions).
>* Um Daten zu aktivieren, ohne den [Zuordnungsschritt](#mapping) des Workflows zu durchlaufen, benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Segment without Mapping]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions).
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[&#x200B; &#x200B;](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}
> 
> Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

In diesem Artikel wird der Workflow erläutert, der zum Aktivieren von Zielgruppen für Adobe Experience Platform Edge-Ziele erforderlich ist. Bei Verwendung zusammen mit [Edge-](../../segmentation/methods/edge-segmentation.md)) und der optionalen [Profilattributzuordnung](#mapping) ermöglichen diese Ziele Anwendungsfälle für die Personalisierung der gleichen Seite und der nächsten Seite in Ihren Web- und Mobile-Eigenschaften.

Einen kurzen Überblick über die Konfiguration der Adobe Target-Verbindung für die Edge-Personalisierung erhalten Sie im folgenden Video.

>[!NOTE]
>
>Die Benutzeroberfläche von Experience Platform wird häufig aktualisiert und kann sich seit der Aufzeichnung dieses Videos geändert haben. Die aktuellsten Informationen finden Sie in den Konfigurationsschritten, die in den folgenden Abschnitten beschrieben werden.

>[!VIDEO](https://video.tv.adobe.com/v/3449802/?captions=ger&quality=12&learn=on)

Einen kurzen Überblick darüber, wie Sie Audiences und Profilattribute für Adobe Target und benutzerdefinierte Personalisierungsziele freigeben können, erhalten Sie im folgenden Video.

>[!VIDEO](https://video.tv.adobe.com/v/3447364/?captions=ger&quality=12&learn=on)

## Anwendungsfälle {#use-cases}

Verwenden Sie Personalisierungslösungen von Adobe wie Adobe Target oder Ihre eigenen Personalisierungspartnerplattformen (z. B. [!DNL Optimizely], [!DNL Pega]) sowie proprietäre Systeme (z. B. hauseigene CMS), um über das Ziel [Benutzerdefinierte Personalization](../catalog/personalization/custom-personalization.md) ein tieferes Personalisierungserlebnis zu ermöglichen. All dies unter Verwendung der Datenerfassungs- und Segmentierungsfunktionen von Experience Platform Edge Network.

Die unten beschriebenen Anwendungsfälle umfassen sowohl die Personalisierung der Site als auch zielgerichtete Werbung auf der Site.

Um diese Anwendungsfälle zu ermöglichen, benötigen Kundinnen und Kunden eine schnelle, optimierte Möglichkeit, sowohl Zielgruppen- als auch Profilattributinformationen von Experience Platform abzurufen und diese Informationen entweder an die [Adobe Target](../catalog/personalization/adobe-target-connection.md)- oder die [Custom Personalization](../catalog/personalization/custom-personalization.md)-Verbindungen in der Experience Platform-Benutzeroberfläche zu senden.

### Personalisierung derselben Seite {#same-page}

Ein Benutzer besucht eine Seite Ihrer Website. Sie können die aktuellen Seitenbesuchsinformationen (z. B. verweisende URL, Browser-Sprache, eingebettete Produktinformationen) verwenden, um die nächste Aktion oder Entscheidung (z. B. Personalisierung) auszuwählen, indem Sie die Verbindung [Benutzerdefinierte Personalisierung](../catalog/personalization/custom-personalization.md) für Nicht-Adobe-Plattformen verwenden (z. B. [!DNL Pega], [!DNL Optimizely] oder andere).

### Personalisierung der nächsten Seite {#next-page}

Ein Benutzer besucht Seite A auf Ihrer Website. Basierend auf dieser Interaktion hat sich der Benutzer für eine Reihe von Zielgruppen qualifiziert. Der Benutzer klickt dann auf einen Link, der ihn von Seite A zu Seite B führt. Die Zielgruppen, für die sich der Benutzer während der vorherigen Interaktion auf Seite A qualifiziert hatte, werden zusammen mit den durch den aktuellen Website-Besuch bestimmten Profilaktualisierungen zur Unterstützung der nächsten Aktion oder Entscheidung verwendet (z. B. welches Werbebanner dem Besucher angezeigt werden soll oder, im Fall von A/B-Tests, welche Version der Seite angezeigt werden soll).

### Personalisierung der nächsten Sitzung {#next-session}

Ein Benutzer besucht mehrere Seiten Ihrer Website. Basierend auf diesen Interaktionen hat sich der Benutzer für eine Reihe von Zielgruppen qualifiziert. Der Benutzer beendet dann die aktuelle Browsersitzung.

Am folgenden Tag kehrt der Benutzer zur gleichen Kunden-Website zurück. Die Zielgruppen, für die sie sich während der vorherigen Interaktion mit allen besuchten Webseiten qualifiziert hatten, werden zusammen mit den durch den aktuellen Website-Besuch bestimmten Profilaktualisierungen zur Auswahl der nächsten Aktion/Entscheidung verwendet (z. B. welches Werbebanner dem Besucher angezeigt werden soll oder, im Fall von A/B-Tests, welche Version der Seite angezeigt werden soll).

### Personalisieren eines Homepage-Banners {#home-page-banner}

Ein Unternehmen, das Häuser vermietet und verkauft, möchte seine Startseite mit einem Banner personalisieren, das auf den Zielgruppen-Qualifikationen in Adobe Experience Platform basiert. Das Unternehmen kann auswählen, welche Zielgruppen ein personalisiertes Erlebnis erhalten sollen, und diese Zielgruppen als Targeting-Kriterien für sein Target-Angebot an Adobe Target senden.

## Voraussetzungen {#prerequisites}

### Konfigurieren eines Datenstroms in der Datenerfassungs-Benutzeroberfläche {#configure-datastream}

Der erste Schritt bei der Einrichtung Ihres Personalisierungsziels besteht darin, einen Datenstrom für das Experience Platform Web SDK zu konfigurieren. Dies erfolgt in der Benutzeroberfläche für die Datenerfassung.

Stellen Sie beim Konfigurieren des Datenstroms unter **[!UICONTROL Adobe Experience Platform]** sicher, dass sowohl **[!UICONTROL Edge Segmentation]** als auch **[!UICONTROL Personalization Destinations]** ausgewählt sind.

>[!TIP]
>
>Ab der Version April 2024 müssen Sie beim Konfigurieren der Verbindung zu Adobe Target das Kontrollkästchen [Edge-Segmentierung“ nicht &#x200B;](/help/destinations/catalog/personalization/adobe-target-connection.md). In diesem Fall ist [Personalisierung der nächsten Sitzung](#next-session) der einzige verfügbare Anwendungsfall für die Personalisierung.

![Datenstromkonfiguration mit hervorgehobener Edge-Segmentierung und hervorgehobenen Personalization-Zielen!](../assets/ui/activate-edge-personalization-destinations/datastream-config.png)

Weitere Informationen zum Einrichten eines Datenstroms finden Sie in den Anweisungen in der [Dokumentation zu Experience Platform Web SDK](../../datastreams/configure.md#aep).

### Erstellen einer [!DNL Active-On-Edge] Zusammenführungsrichtlinie {#create-merge-policy}

Nachdem Sie Ihre Zielverbindung erstellt haben, müssen Sie eine [!DNL Active-On-Edge] Zusammenführungsrichtlinie erstellen. Die [!DNL Active-On-Edge] Zusammenführungsrichtlinie stellt sicher, dass Zielgruppen ständig [on the Edge](../../segmentation/methods/edge-segmentation.md) ausgewertet werden und für Anwendungsfälle der Personalisierung in Echtzeit und auf der nächsten Seite verfügbar sind.

>[!IMPORTANT]
>
>Derzeit unterstützen Edge-Ziele nur die Aktivierung von Zielgruppen, die die [Active-On-Edge-Zusammenführungsrichtlinie](../../segmentation/ui/segment-builder.md#merge-policies) als Standard festlegen. Wenn Sie Zielgruppen, die eine andere Zusammenführungsrichtlinie verwenden, Edge-Zielen zuordnen, werden diese Zielgruppen nicht ausgewertet.

Befolgen Sie die Anweisungen unter [Erstellen einer Zusammenführungsrichtlinie](../../profile/merge-policies/ui-guide.md#create-a-merge-policy) und stellen Sie sicher, dass Sie den Umschalter **[!UICONTROL Active-On-Edge Merge Policy]** aktivieren.

### Erstellen einer neuen Zielgruppe in Experience Platform {#create-audience}

Nachdem Sie die [!DNL Active-On-Edge] Zusammenführungsrichtlinie erstellt haben, müssen Sie eine neue Zielgruppe in Experience Platform erstellen.

Befolgen Sie die [Audience Builder](../../segmentation/ui/segment-builder.md)-Anleitung zum Erstellen Ihrer neuen Zielgruppe und stellen Sie sicher, [&#x200B; Sie &#x200B;](../../segmentation/ui/segment-builder.md#merge-policies) im vorherigen Schritt erstellte [!DNL Active-On-Edge]-Zusammenführungsrichtlinie „zuweisen“.

### Erstellen einer Zielverbindung {#connect-destination}

Nachdem Sie Ihren Datenstrom konfiguriert haben, können Sie mit der Konfiguration Ihres Personalisierungsziels beginnen.

Im [Tutorial zur Erstellung von Zielverbindungen](../ui/connect-destination.md) finden Sie detaillierte Anweisungen zum Erstellen einer neuen Zielverbindung.

Je nach Ziel, das Sie konfigurieren, finden Sie in den folgenden Artikeln zielspezifische Voraussetzungen und zugehörige Informationen:

* [Adobe Target-Verbindung](../catalog/personalization/adobe-target-connection.md#parameters)
* [Benutzerdefinierte Personalisierungsverbindung](../catalog/personalization/custom-personalization.md#parameters)

## Auswählen des Ziels {#select-destination}

Nachdem Sie die Voraussetzungen erfüllt haben, können Sie jetzt das Edge-Personalisierungsziel auswählen, das für die Personalisierung der gleichen Seite und der nächsten Seite verwendet werden soll.

1. Wechseln Sie zu **[!UICONTROL Connections > Destinations]** und wählen Sie die Registerkarte **[!UICONTROL Catalog]** aus.

   ![Registerkarte „Zielkatalog“ in der Experience Platform-Benutzeroberfläche hervorgehoben.](../assets/ui/activate-edge-personalization-destinations/catalog-tab.png)

1. Wählen Sie **[!UICONTROL Activate audiences]** auf der Karte, die dem Personalisierungsziel entspricht, für das Sie Ihre Zielgruppen aktivieren möchten, wie in der Abbildung unten dargestellt.

   ![Zielgruppen-Steuerelement aktivieren, das auf einer Zielkarte im Katalog hervorgehoben ist.](../assets/ui/activate-edge-personalization-destinations/activate-audiences-button.png)

1. Wählen Sie die Zielverbindung aus, die Sie zum Aktivieren Ihrer Zielgruppen verwenden möchten, und klicken Sie dann auf **[!UICONTROL Next]**.

   ![Zielschritt im Aktivierungs-Workflow auswählen.](../assets/ui/activate-edge-personalization-destinations/select-destination.png)

1. Gehen Sie zum nächsten Abschnitt, um [Ihre Zielgruppen auswählen](#select-audiences).

## Audiences auswählen {#select-audiences}

Aktivieren Sie die Kontrollkästchen links neben den Zielgruppennamen, um die Zielgruppen auszuwählen, die Sie für das Ziel aktivieren möchten, und klicken Sie dann auf **[!UICONTROL Next]**.

Um die Zielgruppen auszuwählen, die Sie für das Ziel aktivieren möchten, aktivieren Sie die Kontrollkästchen links neben den Zielgruppennamen und klicken Sie dann auf **[!UICONTROL Next]**.

Je nach Herkunft können Sie aus verschiedenen Arten von Zielgruppen auswählen:

* **[!UICONTROL Segmentation Service]**: Zielgruppen, die in Experience Platform vom Segmentierungs-Service generiert werden. Weitere Informationen finden Sie [Segmentierungsdokumentation](../../segmentation/ui/overview.md) .
* **[!UICONTROL Custom upload]**: Zielgruppen, die außerhalb von Experience Platform generiert und als CSV-Dateien in Experience Platform hochgeladen wurden. Weitere Informationen zu externen Zielgruppen finden Sie in der Dokumentation unter [Importieren einer Zielgruppe](../../segmentation/ui/audience-portal.md#import-audience).
* Andere Arten von Zielgruppen, die aus anderen Adobe-Lösungen wie [!DNL Audience Manager] stammen.

![Schritt „Zielgruppen auswählen“ des Aktivierungs-Workflows mit mehreren hervorgehobenen Zielgruppen.](../assets/ui/activate-edge-personalization-destinations/select-audiences.png)

## Attribute zuordnen {#mapping}

>[!IMPORTANT]
>
>Profilattribute können vertrauliche Daten enthalten. Um diese Daten zu schützen, erfordert das **[!UICONTROL Custom Personalization]**-Ziel, dass Sie beim Konfigurieren des Ziels für [&#x200B; Attribut-basierte Personalisierung die &#x200B;](https://developer.adobe.com/data-collection-apis/docs/)Edge Network-API verwenden. Alle Edge Network-API-Aufrufe müssen in einem [authentifizierten Kontext](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication/) erfolgen.
>
><br>Wenn Sie bereits Web SDK oder Mobile SDK für Ihre Integration verwenden, können Sie Attribute über die Edge Network-API abrufen, indem Sie eine serverseitige Integration hinzufügen.
>
><br>Wenn Sie die oben genannten Anforderungen nicht erfüllen, basiert die Personalisierung nur auf der Zugehörigkeit zur Zielgruppe.

Wählen Sie die Attribute aus, auf deren Grundlage Sie Anwendungsfälle für die Personalisierung für Ihre Benutzerinnen und Benutzer aktivieren möchten. Wenn sich der Wert eines Attributs ändert oder einem Profil ein Attribut hinzugefügt wird, wird dieses Profil Mitglied der Zielgruppe und wird für das Personalisierungsziel aktiviert.

Das Hinzufügen von Attributen ist optional, und Sie können trotzdem mit dem nächsten Schritt fortfahren und die Personalisierung der gleichen Seite und der nächsten Seite aktivieren, ohne Attribute auszuwählen. Wenn Sie in diesem Schritt keine Attribute hinzufügen, erfolgt die Personalisierung weiterhin auf der Grundlage der Zielgruppenzugehörigkeit und der Identitätszuordnungsqualifikationen für Profile.

![Bild, das den Zuordnungsschritt mit einem ausgewählten Attribut zeigt.](../assets/ui/activate-edge-personalization-destinations/mapping-step.png)

### Quellattribute auswählen {#select-source-attributes}

Um Quellattribute hinzuzufügen, wählen Sie die **[!UICONTROL Add new field]** in der Spalte **[!UICONTROL Source field]** aus und suchen oder navigieren Sie zum gewünschten XDM-Attributfeld, wie unten dargestellt.

![Bildschirmaufzeichnung, die zeigt, wie ein Zielattribut im Zuordnungsschritt ausgewählt wird.](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-attribute.gif)

### Auswählen der Zielattribute {#select-target-attributes}

Um Zielattribute hinzuzufügen, wählen Sie das **[!UICONTROL Add new field]** in der Spalte **[!UICONTROL Target field]** aus und geben Sie den benutzerdefinierten Attributnamen ein, dem Sie das Quellattribut zuordnen möchten.

>[!NOTE]
>
>Die Auswahl von Zielattributen gilt nur für den Aktivierungs[Workflow „Benutzerdefinierte Personalization](../catalog/personalization/custom-personalization.md), um die Zuordnung von Feldern mit benutzerfreundlichen Namen in der Zielplattform zu unterstützen.

![Bildschirmaufzeichnung, die zeigt, wie ein XDM-Attribut im Zuordnungsschritt ausgewählt wird](../assets/ui/activate-edge-personalization-destinations/mapping-step-select-target-attribute.gif)

## Planen eines Zielgruppenexports {#scheduling}

Standardmäßig werden auf der Seite [!UICONTROL Audience schedule] nur die neu ausgewählten Zielgruppen angezeigt, die Sie im aktuellen Aktivierungsfluss ausgewählt haben.

Um alle für Ihr Ziel aktivierten Zielgruppen anzuzeigen, verwenden Sie die Filteroption und deaktivieren Sie den **[!UICONTROL Show new audiences only]**.

![Filter „Alle Zielgruppen“ hervorgehoben.](../assets/ui/activate-edge-personalization-destinations/all-audiences.png)

Wählen Sie auf der Seite **[!UICONTROL Audience schedule]** jede Zielgruppe aus und konfigurieren Sie dann mit den Selektoren **[!UICONTROL Start date]** und **[!UICONTROL End date]** das Zeitintervall für das Senden von Daten an Ihr Ziel.

![Audience-Zeitplanschritt des Aktivierungs-Workflows mit hervorgehobenem Start- und Enddatum.](../assets/ui/activate-edge-personalization-destinations/audience-schedule.png)

Wählen Sie **[!UICONTROL Next]** aus, um zur Seite [!UICONTROL Review] zu wechseln.

## Überprüfung {#review}

Auf der Seite **[!UICONTROL Review]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Cancel]** aus, um den Fluss zu unterbrechen, **[!UICONTROL Back]**, Ihre Einstellungen zu ändern, oder **[!UICONTROL Finish]** , um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

![Zusammenfassung der Auswahl im Überprüfungsschritt.](../assets/ui/activate-edge-personalization-destinations/review.png)

### Auswertung der Einverständnisrichtlinie {#consent-policy-evaluation}

Wenn Ihr Unternehmen **Adobe Healthcare Shield** oder **Adobe Privacy &amp; Security Shield** erworben hat, wählen Sie **[!UICONTROL View applicable consent policies]** aus, um zu sehen, welche Einverständnisrichtlinien angewendet werden und wie viele Profile in der Aktivierung enthalten sind. Weitere Informationen finden [&#x200B; unter &#x200B;](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) der Einverständnisrichtlinie .

### Prüfung der Datennutzungsrichtlinien {#data-usage-policy-checks}

Im **[!UICONTROL Review]** Schritt prüft Experience Platform auch, ob Verstöße gegen Datennutzungsrichtlinien vorliegen. Nachstehend ist ein Beispiel angegeben, bei dem eine Richtlinie verletzt wird. Sie können den Zielgruppenaktivierungs-Workflow erst abschließen, nachdem Sie den Verstoß behoben haben. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Verstöße gegen Datennutzungsrichtlinien](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) im Dokumentationsabschnitt zur Data Governance.

![Beispiel für eine Datenrichtlinienverletzung.](../assets/common/data-policy-violation.png)

### Audiences filtern {#filter-audiences}

In diesem Schritt können Sie die auf der Seite verfügbaren Filter verwenden, um nur die Zielgruppen anzuzeigen, deren Zeitplan oder Zuordnung im Rahmen dieses Workflows aktualisiert wurde. Sie können auch umschalten, welche Tabellenspalten angezeigt werden sollen.

![Bildschirmaufzeichnung mit den verfügbaren Zielgruppenfiltern im Überprüfungsschritt.](../assets/ui/activate-edge-personalization-destinations/filter-audiences-review-step.gif)

Wenn Sie mit Ihrer Auswahl zufrieden sind und keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Finish]** aus, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify audience activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->
