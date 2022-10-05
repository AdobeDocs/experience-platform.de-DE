---
title: Marketo Engage-Ziel
description: Marketo Engage ist die einzige End-to-End-Lösung für Customer Experience Management (CXM) für Marketing, Werbung, Analyse und Handel. Damit können Sie Aktivitäten von der CRM-Lead-Verwaltung über die Kundeninteraktion bis hin zur kontobasierten Marketing- und Umsatzzuordnung automatisieren und verwalten.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 9f305ee7824bd8790dec57ccbd2d9462ccfa8b49
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 20%

---

# Marketo Engage-Ziel {#beta-marketo-engage-destination}

## Ziel-Änderungsprotokoll {#changelog}

>[!IMPORTANT]
>
>Mit der Veröffentlichung der [Verbesserter Zielanschluss für Marketo V2](/help/release-notes/2022/july-2022.md#destinations)angezeigt, werden nun zwei Marketo-Karten im Zielkatalog angezeigt.
>* Wenn Sie bereits Daten für die **[!UICONTROL Marketo V1]** Ziel: Erstellen Sie neue Datenflüsse an die **[!UICONTROL Marketo V2]** Ziel und Löschen vorhandener Datenflüsse an die **[!UICONTROL Marketo V1]** Ziel bis Februar 2023. Ab diesem Datum wird die **[!UICONTROL Marketo V1]** Die Zielkarte wird entfernt.
>* Wenn Sie noch keinen Datenfluss zum **[!UICONTROL Marketo V1]** Ziel, verwenden Sie bitte die neue **[!UICONTROL Marketo V2]** -Karte, um eine Verbindung mit Marketo herzustellen und Daten nach zu exportieren.


![Bild der beiden Marketo-Zielkarten in einer Seitenansicht.](/help/destinations/assets/catalog/adobe/marketo-side-by-side-view.png)

Zu den Verbesserungen am Marketo V2-Ziel gehören:

* In Marketo V1 mussten Sie im Schritt **[!UICONTROL Segment planen]** des Aktivierungs-Workflows manuell eine **Zuordnungs-ID** hinzufügen, um Daten erfolgreich in Marketo zu exportieren. Dieser manuelle Schritt ist in Marketo V2 nicht mehr erforderlich.
* Im Schritt **[!UICONTROL Zuordnung]** des Aktivierungs-Workflows konnten Sie XDM-Felder in Marketo V1 nur drei Zielfeldern in Marketo zuordnen: `firstName`, `lastName` und `companyName`. Mit der Version Marketo V2 können Sie jetzt XDM-Felder vielen weiteren Feldern in Marketo zuordnen. Weitere Informationen finden Sie im Abschnitt [unterstützte Attribute](#supported-attributes) weiter unten.

## Übersicht {#overview}

[!DNL Marketo Engage] ist die einzige End-to-End-Lösung für Customer Experience Management (CXM) für Marketing, Werbung, Analyse und Handel. Damit können Sie Aktivitäten von der CRM-Lead-Verwaltung über die Kundeninteraktion bis hin zur kontobasierten Marketing- und Umsatzzuordnung automatisieren und verwalten.

Das Marketo-Ziel ermöglicht es Marketing-Experten, in Adobe Experience Platform erstellte Segmente per Push an zu übertragen, wo sie als statische Listen angezeigt werden.

## Unterstützte Identitäten und Attribute {#supported-identities-attributes}

>[!NOTE]
>
>Im [Zuordnungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) des Workflows Ziel aktivieren *mandatory* Zuordnen von Identitäten und *optional* , um Attribute zuzuordnen. Die Zuordnung von E-Mail und/oder ECID auf der Registerkarte Identity-Namespace ist die wichtigste Maßnahme, um sicherzustellen, dass die Person in Marketo übereinstimmt. Die Zuordnung von E-Mail stellt die höchste Übereinstimmungsrate sicher.

### Unterstützte Identitäten {#supported-identities}

| Zielgruppenidentität | Beschreibung |
|---|---|
| ECID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Alias referenziert werden: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Siehe folgendes Dokument unter [ECID](/help/identity-service/ecid.md) für weitere Informationen. |
| E-Mail | Ein Namespace, der eine E-Mail-Adresse darstellt. Dieser Namespace ist häufig mit einer einzelnen Person verknüpft und kann daher zur kanalübergreifenden Identifizierung dieser Person verwendet werden. |

{style=&quot;table-layout:auto&quot;}

### Unterstützte Attribute {#supported-attributes}

Sie können Attribute von Experience Platform zu allen Attributen zuordnen, auf die Ihr Unternehmen in Marketo Zugriff hat. In Marketo können Sie die [API-Anfrage beschreiben](https://developers.marketo.com/rest-api/lead-database/leads/#describe) , um die Attributfelder abzurufen, auf die Ihr Unternehmen Zugriff hat.

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den in der Variablen [!DNL Marketo Engage] Ziel. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming-Ziele sind &quot;immer auf&quot;-API-basierte Verbindungen. Sobald ein Profil in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert wird, sendet der Connector das Update nachgelagert an die Zielplattform. Mehr dazu [Streaming-Ziele](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Einrichten des Ziels und Aktivieren von Segmenten {#set-up}

>[!IMPORTANT]
> 
>* Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions).
>* Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.


Detaillierte Anweisungen zum Einrichten des Ziels und Aktivieren von Segmenten finden Sie unter [Adobe Experience Platform-Segment in eine statische Marketo-Liste pushen](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) in der Marketo-Dokumentation.

Das folgende Video zeigt auch die Schritte zum Konfigurieren eines Marketo-Ziels und zum Aktivieren von Segmenten.

>[!IMPORTANT]
>
>Das Video spiegelt die aktuelle Funktion nicht vollständig wider. Die aktuellsten Informationen finden Sie im oben stehenden Handbuch. Die folgenden Teile des Videos sind veraltet:
> 
>* Die Zielkarte, die Sie in der Experience Platform-Benutzeroberfläche verwenden sollten, lautet **[!UICONTROL Marketo V2]**.
>* Das Video zeigt das neue **[!UICONTROL Personenerstellung]** Selektorfeld im Workflow Verbindung mit Ziel herstellen.
>* Die beiden im Video genannten Einschränkungen gelten nicht mehr. Sie können jetzt neben den Segmentzugehörigkeitsinformationen, die zum Zeitpunkt der Videoverfolgung unterstützt wurden, viele weitere Profilattributfelder zuordnen. Sie können auch Segmentmitglieder nach Marketo exportieren, die noch nicht in Ihren statischen Marketo-Listen vorhanden sind. Diese werden dann zu den Listen hinzugefügt.
>* In Marketo V1 mussten Sie im Schritt **** Segment planen des Aktivierungs-Workflows manuell eine **[!UICONTROL Zuordnungs-ID]** hinzufügen, um Daten erfolgreich in Marketo zu exportieren. Dieser manuelle Schritt ist in Marketo V2 nicht mehr erforderlich.


>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
