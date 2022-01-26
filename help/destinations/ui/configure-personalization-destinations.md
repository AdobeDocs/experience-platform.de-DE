---
keywords: Personalisierung; Zielgruppe; Bestimmungsort; Personalisierungsziele; Personalisierungsziele konfigurieren; dieselbe Seite; nächste Seite;
title: Personalisierungsziele für die Personalisierung von derselben Seite und nächsten Seiten konfigurieren
type: Tutorial
seo-title: Configure personalization destinations for same-page and next-page personalization.
description: Erfahren Sie, wie Sie Personalisierungsziele für die Personalisierung von derselben Seite und nächsten Seiten konfigurieren.
seo-description: Configure personalization destinations for same-page and next-page personalization.
source-git-commit: 24e8d088dd79304e0bf0335b7c3df2ef75baf81d
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 1%

---


# Configure personalization destinations for same-page and next-page personalization

## Übersicht {#overview}

Adobe Experience Platform verwendet [Kantensegmentierung](../../segmentation/ui/edge-segmentation.md) , damit Kunden Zielgruppensegmente in großem Maßstab in Echtzeit erstellen und ansprechen können.

Mit dieser Funktion können Sie Anwendungsfälle für die Personalisierung von derselben Seite und nächsten Seiten konfigurieren.

Dieser Artikel enthält eine schrittweise Anleitung zum Konfigurieren der Experience Platform und Ihrer Personalisierungsziele für diese Anwendungsfälle.

## Schritt 1: Experience Platform Web SDK-Datenspeicher konfigurieren {#configure-datastream}

Der erste Schritt bei der Konfiguration Ihres Personalisierungsanwendungsfalls besteht darin, eine [!DNL Web SDK datastream].

Follow the instructions described in the [datastream configuration](../../edge/fundamentals/datastreams.md) documentation.

## Schritt 2: Personalisierungsziel konfigurieren {#configure-destination}

After you have configured your datastream, you can start configuring your personalization destination.

Befolgen Sie die [Tutorial zur Erstellung von Zielverbindungen](../ui/connect-destination.md) für detaillierte Anweisungen zum Erstellen einer neuen Zielverbindung.

Abhängig vom konfigurierten Ziel finden Sie in den folgenden Artikeln Informationen zu zielspezifischen Voraussetzungen und zugehörigen Informationen:

* [Adobe Target connection](../catalog/personalization/adobe-target-connection.md)
* [Benutzerdefinierte Personalisierungsverbindung](../catalog/personalization/custom-personalization.md)

## Schritt 3: Erstellen Sie eine [!DNL Active-On-Edge] Zusammenführungsrichtlinie {#create-merge-policy}

Nachdem Sie Ihre Zielverbindung erstellt haben, müssen Sie eine [!DNL Active-On-Edge] Zusammenführungsrichtlinie.

Follow the instructions on [creating a merge policy](../../profile/merge-policies/ui-guide.md#create-a-merge-policy), and make sure to enable the **[!UICONTROL Active-On-Edge Merge Policy]** toggle.

## Schritt 4: Neues Segment in Platform erstellen {#create-segment}

Nachdem Sie die [!DNL Active-On-Edge] Zusammenführungsrichtlinie erstellen, müssen Sie ein neues Segment in Platform erstellen.

Befolgen Sie die [Segment Builder](../../segmentation/ui/segment-builder.md) Anleitung zum Erstellen Ihres neuen Segments und stellen Sie sicher, dass [zuweisen](../../segmentation/ui/segment-builder.md#merge-policies) die [!DNL Active-On-Edge] Zusammenführungsrichtlinie, die Sie in Schritt 3 erstellt haben.

## Step 5: Activate the segment to your destination

The last step of the configuration process is to activate the segment that you created at step 4 to the destination that you created at step 2.

Gehen Sie dazu wie folgt vor: [Aktivierungs-Tutorial](../ui/activate-profile-request-destinations.md).

## Überprüfen der Konfiguration {#validate-configuration}

After succesfully following the steps above, you should see your new segments in your personalization destination.