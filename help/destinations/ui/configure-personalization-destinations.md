---
keywords: Personalisierung; Zielgruppe; Bestimmungsort; Personalisierungsziele; Personalisierungsziele konfigurieren; dieselbe Seite; nächste Seite;
title: Personalisierungsziele für die Personalisierung von derselben Seite und nächsten Seiten konfigurieren
type: Tutorial
seo-title: Configure personalization destinations for same-page and next-page personalization.
description: Erfahren Sie, wie Sie Personalisierungsziele für die Personalisierung von derselben Seite und nächsten Seiten konfigurieren.
seo-description: Configure personalization destinations for same-page and next-page personalization.
exl-id: 7d7b6869-bd59-4766-a044-f449396f6524
source-git-commit: 69db8dbc315f97a0133bcc761ebf850d587dd7d1
workflow-type: tm+mt
source-wordcount: '380'
ht-degree: 0%

---

# Personalisierungsziele für die Personalisierung von derselben Seite und nächsten Seiten konfigurieren

Adobe Experience Platform verwendet [Kantensegmentierung](../../segmentation/ui/edge-segmentation.md) , damit Kunden Zielgruppensegmente in großem Maßstab in Echtzeit erstellen und ansprechen können.

Mit dieser Funktion können Sie Anwendungsfälle für die Personalisierung von derselben Seite und nächsten Seiten konfigurieren.

Dieser Artikel enthält eine schrittweise Anleitung zum Konfigurieren der Experience Platform und Ihrer Personalisierungsziele für diese Anwendungsfälle.

Sehen Sie sich außerdem das folgende Video an, um einen Überblick über den End-to-End-Konfigurationsprozess zu erhalten.

>[!VIDEO](https://video.tv.adobe.com/v/340091/)

## Schritt 1: Konfigurieren eines Datenspeichers in der Benutzeroberfläche für die Datenerfassung {#configure-datastream}

Der erste Schritt bei der Einrichtung Ihres Personalisierungsziels besteht darin, einen Datastream für das Experience Platform Web SDK zu konfigurieren. Dies erfolgt in der Benutzeroberfläche für die Datenerfassung.

Beim Konfigurieren des Datastreams unter **[!UICONTROL Adobe Experience Platform]** Stellen Sie sicher, dass beide **[!UICONTROL Edge-Segmentierung]** und **[!UICONTROL Personalisierungsziele]** ausgewählt sind.

![Datenspeicherkonfiguration](../assets/ui/configure-personalization-destinations/datastream-config.png)

Weitere Informationen zum Einrichten eines Datastreams finden Sie in den Anweisungen unter [Dokumentation zum Platform Web SDK](../../edge/fundamentals/datastreams.md).

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

Der letzte Schritt des Konfigurationsprozesses besteht darin, das in Schritt 4 erstellte Segment für das in Schritt 2 erstellte Ziel zu aktivieren.

Gehen Sie dazu wie folgt vor: [Aktivierungs-Tutorial](../ui/activate-profile-request-destinations.md).

## Überprüfen der Konfiguration {#validate-configuration}

Nachdem Sie die oben genannten Schritte erfolgreich ausgeführt haben, sollten Ihre neuen Segmente in Ihrem Personalisierungsziel angezeigt werden.
