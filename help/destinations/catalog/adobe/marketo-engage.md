---
title: Marketo Engage-Ziel
description: Marketo Engage ist die einzige End-to-End-Lösung für Customer Experience Management (CXM) für Marketing, Werbung, Analyse und Handel. Damit können Sie Aktivitäten von der CRM-Lead-Verwaltung über die Kundeninteraktion bis hin zur kontobasierten Marketing- und Umsatzzuordnung automatisieren und verwalten.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: c35b43654d31f0f112258e577a1bb95e72f0a971
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 26%

---

# Marketo Engage-Ziel {#beta-marketo-engage-destination}

## Ziel-Änderungsprotokoll {#changelog}

>[!IMPORTANT]
>
>Mit der Veröffentlichung des [verbesserten Marketo V2-Zielsteckers](/help/release-notes/2022/july-2022.md#destinations) werden jetzt zwei Marketo-Karten im Zielkatalog angezeigt.
>* Wenn Sie bereits Daten für das Ziel &quot;**[!UICONTROL Marketo V1]**&quot;aktivieren: Erstellen Sie neue Datenflüsse zum Ziel &quot;**[!UICONTROL Marketo V2]**&quot;und löschen Sie bis Februar 2023 vorhandene Datenflüsse zum Ziel &quot;**[!UICONTROL Marketo V1]**&quot;. Ab diesem Datum wird die Zielkarte **[!UICONTROL Marketo V1]** entfernt.
>* Wenn Sie noch keinen Datenfluss zum Ziel **[!UICONTROL Marketo V1]** erstellt haben, verwenden Sie die neue Karte **[!UICONTROL Marketo V2]** , um eine Verbindung mit Marketo herzustellen und Daten nach zu exportieren.

![Bild der beiden Marketo-Zielkarten in einer Seitenansicht.](../..//assets/catalog/adobe/marketo-side-by-side-view.png)

Zu den Verbesserungen am Marketo V2-Ziel gehören:

* In Marketo V1 mussten Sie im Schritt **[!UICONTROL Segment planen]** des Aktivierungs-Workflows manuell eine **Zuordnungs-ID** hinzufügen, um Daten erfolgreich in Marketo zu exportieren. Dieser manuelle Schritt ist in Marketo V2 nicht mehr erforderlich.
* Im Schritt **[!UICONTROL Zuordnung]** des Aktivierungs-Workflows konnten Sie XDM-Felder in Marketo V1 nur drei Zielfeldern in Marketo zuordnen: `firstName`, `lastName` und `companyName`. Mit der Version Marketo V2 können Sie jetzt XDM-Felder vielen weiteren Feldern in Marketo zuordnen. Weitere Informationen finden Sie weiter unten im Abschnitt [unterstützte Attribute](#supported-attributes) .

## Übersicht {#overview}

[!DNL Marketo Engage] ist die einzige End-to-End Customer Experience Management (CXM)-Lösung für Marketing, Werbung, Analyse und Handel. Damit können Sie Aktivitäten von der CRM-Lead-Verwaltung über die Kundeninteraktion bis hin zur kontobasierten Marketing- und Umsatzzuordnung automatisieren und verwalten.

Mit dem Ziel können Marketingexperten in Adobe Experience Platform erstellte Zielgruppen an Marketo senden, wo sie als statische Listen angezeigt werden.

## Unterstützte Identitäten und Attribute {#supported-identities-attributes}

>[!NOTE]
>
>Im Schritt [Zuordnen](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) des Ziel-Workflows aktivieren ist es *obligatorisch*, Identitäten zuzuordnen, und *optional*, Attribute zuzuordnen. Die Zuordnung von E-Mail und/oder ECID auf der Registerkarte Identity-Namespace ist die wichtigste Maßnahme, um sicherzustellen, dass die Person in Marketo übereinstimmt. Die Zuordnung von E-Mail stellt die höchste Übereinstimmungsrate sicher.

### Unterstützte Identitäten {#supported-identities}

| Ziel-Identität | Beschreibung |
|---|---|
| ECID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Aliase referenziert werden: „Adobe Marketing Cloud ID“, „Adobe Experience Cloud ID“, „Adobe Experience Platform ID“. Weitere Informationen finden Sie im folgenden Dokument zu [ECID](/help/identity-service/features/ecid.md) . |
| E-Mail | Ein Namespace, der eine E-Mail-Adresse darstellt. Dieser Namespace ist häufig mit einer einzelnen Person verknüpft und kann daher zur kanalübergreifenden Identifizierung dieser Person verwendet werden. |

{style="table-layout:auto"}

### Unterstützte Attribute {#supported-attributes}

Sie können Attribute von Experience Platform zu jedem der Attribute zuordnen, auf die Ihr Unternehmen in Marketo Zugriff hat. In Marketo können Sie mit der [API-Anfrage beschreiben](https://developers.marketo.com/rest-api/lead-database/leads/#describe) die Attributfelder abrufen, auf die Ihr Unternehmen Zugriff hat.

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die durch den Experience Platform [Segmentierungsdienst](../../../segmentation/home.md) generiert wurden. |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (E-Mail, ECID), die im Ziel [!DNL Marketo Engage] verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind „immer verfügbare“ API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Zielgruppenauswertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Lesen Sie mehr über [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style="table-layout:auto"}

## Einrichten des Ziels und Aktivieren von Zielgruppen {#set-up}

>[!IMPORTANT]
> 
>* Um eine Verbindung zum Ziel herzustellen, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Ziele verwalten]** [.](/help/access-control/home.md#permissions)
>* Um Daten zu aktivieren, benötigen Sie die Zugriffssteuerungsberechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [. ](/help/access-control/home.md#permissions) Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.

Detaillierte Anweisungen zum Einrichten des Ziels und Aktivieren von Zielgruppen finden Sie unter [Push an eine Adobe Experience Platform-Zielgruppe in eine statische Marketo-Liste](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=de) in der Marketo-Dokumentation.

Das folgende Video zeigt auch die Schritte zum Konfigurieren eines Marketo-Ziels und zum Aktivieren von Zielgruppen.

>[!IMPORTANT]
>
>Das Video spiegelt die aktuelle Funktion nicht vollständig wider. Die aktuellsten Informationen finden Sie im oben stehenden Handbuch. Die folgenden Teile des Videos sind veraltet:
> 
>* Die Zielkarte, die Sie in der Experience Platform-Benutzeroberfläche verwenden sollten, ist **[!UICONTROL Marketo V2]**.
>* Im Video wird das neue Auswahlfeld **[!UICONTROL Personenerstellung]** im Workflow Verbindung mit Ziel nicht angezeigt.
>* Die beiden im Video genannten Einschränkungen gelten nicht mehr. Sie können jetzt neben den zum Zeitpunkt der Aufzeichnung des Videos unterstützten Informationen zur Zielgruppenmitgliedschaft viele weitere Profilattributfelder zuordnen. Sie können Zielgruppenmitglieder auch nach Marketo exportieren, die noch nicht in Ihren statischen Marketo-Listen vorhanden sind. Diese werden dann zu den Listen hinzugefügt.
>* Im Schritt **[!UICONTROL Zielgruppe planen]** des Aktivierungs-Workflows mussten Sie in Marketo V1 manuell eine **[!UICONTROL Zuordnungs-ID]** hinzufügen, um Daten erfolgreich nach Marketo zu exportieren. Dieser manuelle Schritt ist in Marketo V2 nicht mehr erforderlich.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen dazu, wie [!DNL Adobe Experience Platform] Data Governance durchsetzt, finden Sie unter [Data Governance - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).

<!--

## Activate audiences to this destination {#activate}

See [Activate audience data to streaming audience export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audiences to this destination.

-->
