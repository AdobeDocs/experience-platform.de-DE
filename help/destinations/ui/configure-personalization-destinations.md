---
keywords: Personalisierung;Zielgruppe;Ziel;Personalisierungsziele;Personalisierungsziele konfigurieren;dieselbe Seite;nächste Seite;
title: Konfigurieren von Personalisierungszielen für die Personalisierung auf derselben Seite und auf der nächsten Seite
type: Tutorial
description: Erfahren Sie, wie Sie Personalisierungsziele für die Personalisierung auf derselben Seite und der nächsten Seiten konfigurieren.
exl-id: 7d7b6869-bd59-4766-a044-f449396f6524
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 95%

---

# Konfigurieren von Personalisierungszielen für die Personalisierung auf derselben Seite und auf der nächsten Seite

## Übersicht {#overview}

>[!NOTE]
>
>Wann [Konfigurieren der Adobe Target-Verbindung](../catalog/personalization/adobe-target-connection.md) ohne Verwendung einer Datastream-ID werden die in diesem Artikel beschriebenen Anwendungsfälle nicht unterstützt.

Adobe Experience Platform verwendet [Edge-Segmentierung](../../segmentation/ui/edge-segmentation.md), damit Kunden Zielgruppensegmente im gewünschten Umfang in Echtzeit erstellen und ansprechen können.

Mit dieser Funktion können Sie Anwendungsfälle für die Personalisierung von derselben Seite und von der nächsten Seite konfigurieren.

Dieser Artikel enthält eine schrittweise Anleitung zum Konfigurieren von Experience Platform und Ihrer Personalisierungsziele für diese Anwendungsfälle.

Sehen Sie sich außerdem das folgende Video an, um einen Überblick über den End-to-End-Konfigurationsprozess zu erhalten.

>[!VIDEO](https://video.tv.adobe.com/v/340091/)

>[!NOTE]
>
>Die Benutzeroberfläche von Experience Platform wird häufig aktualisiert und kann sich seit der Aufzeichnung dieses Videos geändert haben. Die aktuellsten Informationen finden Sie in den Konfigurationsschritten, die in den folgenden Abschnitten beschrieben werden.

## Schritt 1: Konfigurieren eines Datenstroms in der Benutzeroberfläche für die Datenerfassung {#configure-datastream}

Der erste Schritt bei der Einrichtung Ihres Personalisierungsziels besteht darin, einen Datenstrom für das Experience Platform Web SDK zu konfigurieren. Dies erfolgt in der Benutzeroberfläche für die Datenerfassung.

Stellen Sie beim Konfigurieren des Datenstroms unter **[!UICONTROL Adobe Experience Platform]** sicher, dass sowohl **[!UICONTROL Edge-Segmentierung]** als auch **[!UICONTROL Personalisierungsziele]** ausgewählt sind.

![Datenstromkonfiguration](../assets/ui/configure-personalization-destinations/datastream-config.png)

Weitere Informationen zum Einrichten eines Datenstroms finden Sie in den Anweisungen in der [Dokumentation zum Platform Web SDK](../../edge/datastreams/overview.md).

## Schritt 2: Konfigurieren Ihres Personalisierungsziels {#configure-destination}

Nachdem Sie Ihren Datenstrom konfiguriert haben, können Sie mit der Konfiguration Ihres Personalisierungsziels beginnen.

Im [Tutorial zur Erstellung von Zielverbindungen](../ui/connect-destination.md) finden Sie detaillierte Anweisungen zum Erstellen einer neuen Zielverbindung.

Je nach dem Ziel, das Sie konfigurieren, finden Sie in den folgenden Artikeln zielspezifische Voraussetzungen und zugehörige Informationen:

* [Adobe Target-Verbindung](../catalog/personalization/adobe-target-connection.md)
* [Benutzerdefinierte Personalisierungsverbindung](../catalog/personalization/custom-personalization.md)

## Schritt 3: Erstellen einer [!DNL Active-On-Edge]-Zusammenführungsrichtlinie {#create-merge-policy}

Nachdem Sie Ihre Zielverbindung erstellt haben, müssen Sie eine [!DNL Active-On-Edge]-Zusammenführungsrichtlinie erstellen.

Befolgen Sie die Anweisungen zum [Erstellen einer Zusammenführungsrichtlinie](../../profile/merge-policies/ui-guide.md#create-a-merge-policy) und stellen Sie sicher, dass Sie die **[!UICONTROL Active-On-Edge-Zusammenführungsrichtlinie]** aktivieren.

## Schritt 4: Erstellen eines neuen Segments in Platform {#create-segment}

Nachdem Sie die [!DNL Active-On-Edge]-Zusammenführungsrichtlinie erstellt haben, müssen Sie ein neues Segment in Platform erstellen.

Befolgen Sie die Anweisungen im Handbuch zu [Segment Builder](../../segmentation/ui/segment-builder.md), um Ihr neues Segment zu erstellen, und stellen Sie sicher, dass Sie ihm die [!DNL Active-On-Edge] Zusammenführungsrichtlinie [zuweisen](../../segmentation/ui/segment-builder.md#merge-policies), die Sie in Schritt 3 erstellt haben.

## Schritt 5: Aktivieren des Segments für Ihr Ziel

Der letzte Schritt des Konfigurationsprozesses besteht darin, das in Schritt 4 erstellte Segment für das in Schritt 2 erstellte Ziel zu aktivieren.

Gehen Sie dazu vor, wie in diesem [Aktivierungs-Tutorial](../ui/activate-profile-request-destinations.md) erläutert.

## Überprüfen der Konfiguration {#validate-configuration}

Nachdem Sie die oben genannten Schritte erfolgreich ausgeführt haben, sollten Ihre neuen Segmente in Ihrem Personalisierungsziel angezeigt werden.
