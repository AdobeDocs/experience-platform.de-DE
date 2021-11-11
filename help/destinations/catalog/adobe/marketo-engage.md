---
title: Marketo Engage-Ziel
description: Marketo Engage ist die einzige End-to-End-Lösung für Customer Experience Management (CXM) für Marketing, Werbung, Analyse und Handel. Damit können Sie Aktivitäten von der CRM-Lead-Verwaltung über die Kundeninteraktion bis hin zur kontobasierten Marketing- und Umsatzzuordnung automatisieren und verwalten.
exl-id: 5ae5f114-47ba-4ff6-8e42-f8f43eb079f7
source-git-commit: 3e2382cf4b02ea4fd40e3638b52b4719938a2ea2
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 1%

---

# Marketo Engage-Ziel {#beta-marketo-engage-destination}

## Übersicht {#overview}

Marketo Engage ist die einzige End-to-End-Lösung für Customer Experience Management (CXM) für Marketing, Werbung, Analyse und Handel. Damit können Sie Aktivitäten von der CRM-Lead-Verwaltung über die Kundeninteraktion bis hin zur kontobasierten Marketing- und Umsatzzuordnung automatisieren und verwalten.

Mit dem Ziel können Marketingexperten in Adobe Experience Platform erstellte Segmente an Marketo senden, wo sie als statische Listen angezeigt werden.

## Unterstützte Identitäten {#supported-identities}

| Zielgruppenidentität | Beschreibung |
|---|---|
| ECID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Alias referenziert werden: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Siehe folgendes Dokument unter [ECID](/help/identity-service/ecid.md) für weitere Informationen. |
| E-Mail  | Ein Namespace, der eine E-Mail-Adresse darstellt. Dieser Namespace ist häufig mit einer einzelnen Person verknüpft und kann daher zur kanalübergreifenden Identifizierung dieser Person verwendet werden. |

## Exporttyp {#export-type}

Segmentexport: Sie exportieren alle Segmentmitglieder (Zielgruppe) mit den IDs (E-Mail, ECID), die im Marketo Engage-Ziel verwendet werden.

## Einrichten des Ziels und Aktivieren von Segmenten {#set-up}

Detaillierte Anweisungen zum Einrichten des Ziels und Aktivieren von Segmenten finden Sie unter [Adobe Experience Platform-Segment in eine statische Marketo-Liste pushen](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en) in der Marketo-Dokumentation.

<!--

## Connect to the destination {#connect}

To connect to this destination, follow the steps described in the [destination configuration tutorial](../../ui/connect-destination.md).

-->

## Datennutzung und -verwaltung {#data-usage-governance}

Alle [!DNL Adobe Experience Platform] Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen zur [!DNL Adobe Experience Platform] erzwingt Data Governance, siehe [Data Governance - Übersicht](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).

<!--

## Activate segments to this destination {#activate}

See [Activate audience data to streaming segment export destinations](../../ui/activate-segment-streaming-destinations.md) for instructions on activating audience segments to this destination.

-->