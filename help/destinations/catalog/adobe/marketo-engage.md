---
title: Marketo Engage-Ziel
description: Marketo Engage ist die einzige End-to-End-Lösung für Customer Experience Management (CXM) für Marketing, Werbung, Analyse und Handel. Damit können Sie Aktivitäten von der CRM-Lead-Verwaltung über die Kundeninteraktion bis hin zur kontobasierten Marketing- und Umsatzzuordnung automatisieren und verwalten.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 0006c498cd33d9deb66f1d052b4771ec7504457d
workflow-type: tm+mt
source-wordcount: '491'
ht-degree: 16%

---

# Marketo Engage-Ziel {#beta-marketo-engage-destination}

## Übersicht {#overview}

Marketo Engage is the only end-to-end customer experience management (CXM) solution for marketing, advertising, analytics, and commerce. It lets you automate and manage activities from CRM lead management and customer engagement to account-based marketing and revenue attribution.

Das Marketo-Ziel ermöglicht es Marketing-Experten, in Adobe Experience Platform erstellte Segmente per Push an zu übertragen, wo sie als statische Listen angezeigt werden.

## Unterstützte Identitäten {#supported-identities}

| Zielgruppenidentität | Beschreibung |
|---|---|
| ECID | A namespace that represents ECID. This namespace can also be referred to by the following aliases: “Adobe Marketing Cloud ID”, “Adobe Experience Cloud ID”, “Adobe Experience Platform ID”. See the following document on [ECID](/help/identity-service/ecid.md) for more information. |
| E-Mail | A namespace that represents an email address. Dieser Namespace ist häufig mit einer einzelnen Person verknüpft und kann daher zur kanalübergreifenden Identifizierung dieser Person verwendet werden. |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Im [Zuordnungsschritt](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping) des Workflows Ziel aktivieren *mandatory* Zuordnen von Identitäten und *optional* , um Attribute zuzuordnen. Die Zuordnung von E-Mail und/oder ECID auf der Registerkarte Identity-Namespace ist die wichtigste Maßnahme, um sicherzustellen, dass die Person in Marketo übereinstimmt. Mapping Email ensures the highest match rate.

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Segmentmitglieder (Zielgruppe) mit den IDs (E-Mail, ECID), die im Marketo Engage-Ziel verwendet werden. |
| Exporthäufigkeit | **[!UICONTROL Streaming]** | Streaming destinations are &quot;always on&quot; API-based connections. As soon as a profile is updated in Experience Platform based on segment evaluation, the connector sends the update downstream to the destination platform. Read more about [streaming destinations](/help/destinations/destination-types.md#streaming-destinations). |

{style=&quot;table-layout:auto&quot;}

## Einrichten des Ziels und Aktivieren von Segmenten {#set-up}

>[!IMPORTANT]
> 
>* Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions).
>* To activate data, you need the **[!UICONTROL Manage Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]**, and **[!UICONTROL View Segments]** [access control permissions](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.


For detailed instructions on how to set up the destination and activate segments, read [Push an Adobe Experience Platform Segment to a Marketo Static List](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) in the Marketo documentation.

Das folgende Video zeigt auch die Schritte zum Konfigurieren eines Marketo-Ziels und zum Aktivieren von Segmenten.

>[!NOTE]
>
>Die Benutzeroberfläche von Experience Platform wird häufig aktualisiert und kann sich seit der Aufzeichnung dieses Videos geändert haben. For the most up-to-date information, please refer to the guide linked above.

>[!VIDEO](https://video.tv.adobe.com/v/338248?quality=12)

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. For detailed information on how [!DNL Adobe Experience Platform] enforces data governance, see the [data governance overview](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html?lang=de).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->
