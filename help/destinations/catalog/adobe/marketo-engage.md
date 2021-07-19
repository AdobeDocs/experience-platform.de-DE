---
title: Marketo Engage-Ziel
description: Marketo Engage ist die einzige End-to-End-Lösung für Customer Experience Management (CXM) für Marketing, Werbung, Analyse und Handel. Damit können Sie Aktivitäten von der CRM-Lead-Verwaltung über die Kundeninteraktion bis hin zur kontobasierten Marketing- und Umsatzzuordnung automatisieren und verwalten.
source-git-commit: 9b1c805f0717d0ed2c5759420d20abf5dcdeaabc
workflow-type: tm+mt
source-wordcount: '286'
ht-degree: 4%

---


# (Beta) Marketo Engage-Ziel {#beta-marketo-engage-destination}

>[!IMPORTANT]
>
>Das Marketo Engage-Ziel in Adobe Experience Platform ist derzeit als Betaversion verfügbar. Dokumentation und Funktionalität können sich ändern.

## Übersicht {#overview}

Marketo Engage ist die einzige End-to-End-Lösung für Customer Experience Management (CXM) für Marketing, Werbung, Analyse und Handel. Damit können Sie Aktivitäten von der CRM-Lead-Verwaltung über die Kundeninteraktion bis hin zur kontobasierten Marketing- und Umsatzzuordnung automatisieren und verwalten.

Mit dem Segmentanschluss können Marketingexperten in Adobe Experience Platform erstellte Segmente an Marketo senden, wo sie als statische Listen angezeigt werden.

## Unterstützte Identitäten {#supported-identities}

| Zielgruppenidentität | Beschreibung |
|---|---|
| ECID | Ein Namespace, der die ECID darstellt. Dieser Namespace kann auch durch die folgenden Alias referenziert werden: &quot;Adobe Marketing Cloud ID&quot;, &quot;Adobe Experience Cloud ID&quot;, &quot;Adobe Experience Platform ID&quot;. Weitere Informationen finden Sie im folgenden Dokument zu [ECID](/help/identity-service/ecid.md). |
| E-Mail | Ein Namespace, der eine E-Mail-Adresse darstellt. Dieser Namespace ist häufig mit einer einzelnen Person verknüpft und kann daher zur kanalübergreifenden Identifizierung dieser Person verwendet werden. |

## Exporttyp {#export-type}

Segmentexport: Sie exportieren alle Segmentmitglieder (Zielgruppe) mit den IDs (Marketo Engage, Telefonnummer usw.), die im Zielsegment verwendet werden.

## Einrichten {#set-up}

Anweisungen zum Einrichten des Ziels [finden Sie hier](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html?lang=en).

## Datennutzung und -verwaltung {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Detaillierte Informationen dazu, wie [!DNL Adobe Experience Platform] Data Governance durchsetzt, finden Sie unter [Übersicht über Data Governance](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
