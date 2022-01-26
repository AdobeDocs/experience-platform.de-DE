---
keywords: Personalisierung; Zielgruppe; Bestimmungsort; Personalisierungsziele; Personalisierungsziele konfigurieren; dieselbe Seite; nächste Seite;
title: Personalisierungsziele für die Personalisierung von derselben Seite und nächsten Seiten konfigurieren
type: Tutorial
seo-title: Configure personalization destinations for same-page and next-page personalization
description: Erfahren Sie, wie Sie Personalisierungsziele für die Personalisierung der gleichen Seite und der nächsten Seite konfigurieren.
seo-description: Configure personalization destinations for same-page and next-page personalization
source-git-commit: 628e7a993a3566322e0249a5a9864cf6b3fe4493
workflow-type: tm+mt
source-wordcount: '320'
ht-degree: 1%

---


# Personalisierungsziele für die Personalisierung von derselben Seite und nächsten Seiten konfigurieren

## Übersicht {#overview}

Adobe Experience Platform verwendet [Kantensegmentierung](../../segmentation/ui/edge-segmentation.md) , damit Kunden Zielgruppensegmente in großem Maßstab in Echtzeit erstellen und ansprechen können.

Mit dieser Funktion können Sie Anwendungsfälle für die Personalisierung von derselben Seite und nächsten Seiten konfigurieren.

Dieser Artikel enthält eine schrittweise Anleitung zum Konfigurieren der Experience Platform und Ihrer Personalisierungsziele für diese Anwendungsfälle.

## Schritt 1: Experience Platform Web SDK-Datenspeicher konfigurieren {#configure-datastream}

Der erste Schritt bei der Konfiguration Ihres Personalisierungsanwendungsfalls besteht darin, eine [!DNL Web SDK datastream].

Befolgen Sie die Anweisungen im Abschnitt [Datenspeicherkonfiguration](../../edge/fundamentals/datastreams.md) Dokumentation.

## Schritt 2: Personalisierungsziel konfigurieren {#configure-destination}

Nachdem Sie Ihren Datastream konfiguriert haben, können Sie mit der Konfiguration Ihres Personalisierungsziels beginnen.

Befolgen Sie die [Tutorial zur Erstellung von Zielverbindungen](../ui/connect-destination.md) für detaillierte Anweisungen zum Erstellen einer neuen Zielverbindung.

Abhängig vom konfigurierten Ziel finden Sie in den folgenden Artikeln Informationen zu zielspezifischen Voraussetzungen und zugehörigen Informationen:

* [Adobe Target-Verbindung](../catalog/personalization/adobe-target-connection.md)
* [Benutzerdefinierte Personalisierungsverbindung](../catalog/personalization/custom-personalization.md)

## Schritt 3: Erstellen Sie eine [!DNL Active-On-Edge] Zusammenführungsrichtlinie {#create-merge-policy}

Nachdem Sie Ihre Zielverbindung erstellt haben, müssen Sie eine [!DNL Active-On-Edge] Zusammenführungsrichtlinie.

Befolgen Sie die Anweisungen unter [Erstellen einer Zusammenführungsrichtlinie](../../profile/merge-policies/ui-guide.md#create-a-merge-policy)und stellen Sie sicher, dass Sie die **[!UICONTROL Richtlinie zur aktiven Zusammenführung auf Edge]** umschalten.

## Schritt 4: Neues Segment in Platform erstellen {#create-segment}

Nachdem Sie die [!DNL Active-On-Edge] Zusammenführungsrichtlinie erstellen, müssen Sie ein neues Segment in Platform erstellen.

Befolgen Sie die [Segment Builder](../../segmentation/ui/segment-builder.md) Anleitung zum Erstellen Ihres neuen Segments und stellen Sie sicher, dass [zuweisen](../../segmentation/ui/segment-builder.md#merge-policies) die [!DNL Active-On-Edge] Zusammenführungsrichtlinie, die Sie in Schritt 3 erstellt haben.

## Schritt 5: Aktivieren des Segments für Ihr Ziel

Der letzte Schritt des Konfigurationsprozesses besteht darin, das Segment, das Sie in Schritt 4 erstellt haben, für das Ziel zu aktivieren, das Sie in Schritt 2 erstellt haben.

Gehen Sie dazu wie folgt vor: [Aktivierungs-Tutorial](../ui/activate-profile-request-destinations.md).

## Überprüfen der Konfiguration {#validate-configuration}

Nachdem Sie die oben genannten Schritte erfolgreich ausgeführt haben, sollten Ihre neuen Segmente in Ihrem Personalisierungsziel angezeigt werden.