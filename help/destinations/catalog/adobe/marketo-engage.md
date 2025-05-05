---
title: Marketo Engage-Ziel
description: Marketo Engage ist die einzige End-to-End-Lösung für Customer Experience Management (CXM) für Marketing, Werbung, Analysen und Commerce. Damit können Sie Aktivitäten automatisieren und verwalten, von der CRM-Lead-Verwaltung und Kundeninteraktion bis hin zu Account-basiertem Marketing und Umsatzzuordnung.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: c57a519b5a230dc62699808cf5c020d48cc79083
workflow-type: tm+mt
source-wordcount: '967'
ht-degree: 24%

---

# Marketo Engage-Ziel {#beta-marketo-engage-destination}

## Ziel-Änderungsprotokoll {#changelog}

>[!IMPORTANT]
>
>Mit der Veröffentlichung des [erweiterten Marketo V2-Ziel](/help/release-notes/2022/july-2022.md#destinations)Connectors werden jetzt zwei Marketo-Karten im Zielkatalog angezeigt.
>* Wenn Sie bereits Daten für das Ziel **[!UICONTROL Marketo V1]** aktivieren: Erstellen Sie neue Datenflüsse für das Ziel **[!UICONTROL Marketo V2]** und löschen Sie bestehende Datenflüsse für das Ziel **[!UICONTROL Marketo V1]** bis Februar 2023. Ab diesem Datum wird die Zielkarte **[!UICONTROL Marketo]** 1&rbrace; entfernt.
>* Wenn Sie noch keine Datenflüsse zum Ziel **[!UICONTROL Marketo V1]** erstellt haben, verwenden Sie die neue Karte **[!UICONTROL Marketo V2]**, um eine Verbindung mit Marketo herzustellen und Daten dorthin zu exportieren.

![Abbildung der beiden Marketo-Zielkarten, die diese nebeneinander in einer Ansicht zeigt.](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

Zu den Verbesserungen am Marketo V2-Ziel gehören:

* In Marketo V1 mussten Sie im Schritt **[!UICONTROL Segment planen]** des Aktivierungs-Workflows manuell eine **Zuordnungs-ID** hinzufügen, um Daten erfolgreich in Marketo zu exportieren. Dieser manuelle Schritt ist in Marketo V2 nicht mehr erforderlich.
* Im Schritt **[!UICONTROL Zuordnung]** des Aktivierungs-Workflows konnten Sie XDM-Felder in Marketo V1 nur drei Zielfeldern in Marketo zuordnen: `firstName`, `lastName` und `companyName`. Mit der Version Marketo V2 können Sie jetzt XDM-Felder vielen weiteren Feldern in Marketo zuordnen. Weitere Informationen finden Sie im Abschnitt [Unterstützte Attribute](#supported-attributes) weiter unten.

## Übersicht {#overview}

[!DNL Marketo Engage] ist die einzige End-to-End-Lösung für Customer Experience Management (CXM) für Marketing, Werbung, Analysen und Commerce. Damit können Sie Aktivitäten automatisieren und verwalten, von der CRM-Lead-Verwaltung und Kundeninteraktion bis hin zu Account-basiertem Marketing und Umsatzzuordnung.

Das Ziel ermöglicht es Marketing-Experten, in Adobe Experience Platform erstellte Zielgruppen an Marketo zu übertragen, wo sie als statische Listen angezeigt werden.

## Unterstützte Identitäten und Attribute {#supported-identities-attributes}

>[!NOTE]
>
>Im [Zuordnungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) des Zielaktivierungs-Workflows ist es *obligatorisch* Identitäten zuzuordnen und *optional* Attribute zuzuordnen. Das Zuordnen von E-Mail und/oder ECID auf der Registerkarte Identity-Namespace ist das Wichtigste, um sicherzustellen, dass die Person in Marketo abgeglichen wird. Die E-Mail-Zuordnung sorgt für die höchste Übereinstimmungsrate.

### Unterstützte Identitäten {#supported-identities}

| Ziel-Identität | Beschreibung |
|---|---|
| ECID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Weitere Informationen finden Sie im folgenden Dokument [ECID](/help/identity-service/features/ecid.md) . |
| E-Mail | Ein Namespace, der eine E-Mail-Adresse darstellt. Dieser Namespace ist häufig mit einer einzelnen Person verknüpft und kann daher verwendet werden, um diese Person über verschiedene Kanäle hinweg zu identifizieren. |

{style="table-layout:auto"}

### Unterstützte Attribute {#supported-attributes}

Sie können Attribute aus Experience Platform jedem der Attribute zuordnen, auf die Ihr Unternehmen in Marketo Zugriff hat. In Marketo können Sie die [API-Anfrage beschreiben](https://developers.marketo.com/rest-api/lead-database/leads/#describe) verwenden, um die Attributfelder abzurufen, auf die Ihr Unternehmen Zugriff hat.

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[ (Segmentierungs-Service) generiert ](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (E-Mail, ECID), die im [!DNL Marketo Engage]-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Einrichten des Ziels und Aktivieren von Zielgruppen {#set-up}

>[!IMPORTANT]
> 
>* Um eine Verbindung mit dem Ziel herzustellen, benötigen Sie **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions).
>* Zum Aktivieren von Daten benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**&#x200B;[Zugriffssteuerung](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Detaillierte Anweisungen zum Einrichten des Ziels und Aktivieren von Zielgruppen finden Sie unter [Pushen einer Adobe Experience Platform-Zielgruppe in eine statische Marketo-Liste](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=de) in der Dokumentation zu Marketo.

Das folgende Video zeigt auch die Schritte zum Konfigurieren eines Marketo-Ziels und zum Aktivieren von Zielgruppen.

>[!IMPORTANT]
>
>Das Video spiegelt die aktuelle Funktion nicht vollständig wider. Die aktuellsten Informationen finden Sie in dem oben verlinkten Handbuch. Die folgenden Teile des Videos sind veraltet:
> 
>* Die Zielkarte, die Sie in der Experience Platform-Benutzeroberfläche verwenden sollten, ist **[!UICONTROL Marketo V2]**.
>* Das Video zeigt nicht das neue Auswahlfeld **[!UICONTROL Personenerstellung]** im Workflow Mit Ziel verbinden . Um dieses Feld zu verwenden, müssen Sie während des Schritts zur Attributzuordnung sowohl den Vor- als auch den Nachnamen zuordnen.
>* Die beiden im Video genannten Einschränkungen gelten nicht mehr. Zusätzlich zu den Informationen zur Zielgruppenzugehörigkeit, die zum Zeitpunkt der Videoaufzeichnung unterstützt wurden, können Sie jetzt viele weitere Profilattributfelder zuordnen. Sie können auch Zielgruppenmitglieder, die noch nicht in Ihren statischen Marketo-Listen vorhanden sind, nach Marketo exportieren. Diese werden dann den Listen hinzugefügt.
>* Im Schritt **[!UICONTROL Zielgruppe planen]** des Aktivierungs-Workflows mussten Sie in Marketo V1 manuell eine **[!UICONTROL Zuordnungs-ID“ hinzufügen]** um Daten erfolgreich in Marketo zu exportieren. Dieser manuelle Schritt ist in Marketo V2 nicht mehr erforderlich.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

## Ziel überwachen {#monitor-destination}

Nachdem Sie eine Verbindung zum Ziel hergestellt und einen Ziel-Datenfluss eingerichtet haben, können Sie die [Überwachungsfunktion](/help/dataflows/ui/monitor-destinations.md) in Real-Time CDP verwenden, um ausführliche Informationen über die Profildatensätze zu erhalten, die in jeder Datenflussausführung für Ihr Ziel aktiviert wurden.

Die Überwachungsinformationen für die [!DNL Marketo Engage]-Verbindung enthalten Informationen auf Zielgruppenebene, die sich auf aktivierte, ausgeschlossene und fehlgeschlagene Identitäten in jedem Datenfluss und jeder Datenflussausführung beziehen. [Weitere Informationen](/help/dataflows/ui/monitor-destinations.md#segment-level-view) über die Funktion.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).

