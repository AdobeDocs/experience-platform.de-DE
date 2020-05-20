---
title: Zieldetailseite
seo-title: Zieldetailseite
description: 'Die Detailseite für ein einzelnes Ziel bietet einen Überblick über die Zieldetails, wie den Zielnamen, die Kennung, die dem Ziel zugeordneten Segmente und die Steuerelemente zum Bearbeiten der Aktivierung sowie zum Aktivieren und Deaktivieren des Datenflusses. '
seo-description: 'Die Detailseite für ein einzelnes Ziel bietet einen Überblick über die Zieldetails, wie den Zielnamen, die Kennung, die dem Ziel zugeordneten Segmente und die Steuerelemente zum Bearbeiten der Aktivierung sowie zum Aktivieren und Deaktivieren des Datenflusses. '
translation-type: tm+mt
source-git-commit: e21cf6794e6c9ee522482cd9ccb95d66b06d330a
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 100%

---


# Zieldetailseite {#destinations-details-page}

Die Detailseite für ein einzelnes Ziel bietet einen Überblick über die Zieldetails, wie den Zielnamen, die Kennung, die dem Ziel zugeordneten Segmente und die Steuerelemente zum Bearbeiten der Aktivierung sowie zum Aktivieren und Deaktivieren des Datenflusses. Um diese Details anzuzeigen, navigieren Sie zu **Ziele** > **Durchsuchen** und klicken Sie auf den Namen des Ziels, mit dem Sie arbeiten möchten.

Hauptkomponenten eines Ziels sind:

* 1 – Zielname und Kennung
* 2 – Für das Ziel aktivierte Segmente
* 3 – Informationen in rechter Leiste
* 4 – Steuerelemente zum Bearbeiten der Aktivierung und Aktivieren/Deaktivieren des Datenflusses

![Nummerierte Zielseite](/help/rtcdp/destinations/assets/destination-page-numbered.png)

Navigieren Sie zur Seite eines Ziels, um einen Überblick über die Zieldetails zu erhalten, z. B.:

## 1. Zielname und Kennung

Sie können den Zielnamen in der Seitenüberschrift und die Zielkennung in der Seiten-URL sehen.

## 2. Für das Ziel aktivierte Segmente

Dieser Abschnitt zeigt, welche Segmente dem Ziel derzeit zugeordnet sind, und enthält weitere Informationen zu diesen Segmenten. Weitere Informationen finden Sie in der folgenden Tabelle:

| Element | Beschreibung |
---------|----------|
| Segmentname | Der Name Ihres Segments. |
| Segmentbeschreibung | Die Beschreibung Ihres Segments. |
| Anfangsdatum | Das Datum, ab dem diese Segmente für das Ziel aktiviert werden. |
| Enddatum | Das Datum, an dem diese Segmente für das Ziel deaktiviert werden. |
| Mapping-ID | *Nicht verfügbar bei E-Mail-Marketing-Zielen*. Gibt die Kennung an, anhand der das Segment in der Zielplattform bekannt ist. |

## 3. Informationen in rechter Leiste

Die rechte Leiste enthält Informationen über Ihr Ziel. Weiterführende Informationen finden Sie in der folgenden Tabelle:

| Element | Beschreibung |
---------|----------|
| Plattform | Die Zielplattform, an die Zielgruppen gesendet werden. Weiterführende Informationen finden Sie unter [Zielkatalog](/help/rtcdp/destinations/destinations-catalog.md). |
| Beschreibung | Sie können die Beschreibung Ihres Zielflusses bearbeiten. |
| Kategorie | Gibt den Zieltyp an. Weiterführende Informationen finden Sie unter [Zielkatalog](/help/rtcdp/destinations/destinations-catalog.md). |
| Verbindungstyp | Gibt an, in welcher Form Ihre Zielgruppen an das Ziel gesendet werden. Kann **Cookie**- oder **profilbasiert** sein. |
| Häufigkeit | Gibt an, wie oft die Zielgruppen an das Ziel gesendet werden. Kann **Streaming** oder **Batch** sein. |
| Identität | Stellt den vom Ziel akzeptierten Identitäts-Namespace dar. Das Identitätsfeld kann beispielsweise „GAID“, „IDFA“ oder „E-Mail“ lauten. Für Informationen zu allen akzeptierten Identitäts-Namespaces konsultieren Sie die standardmäßigen Namespaces unter [Identitäts-Namespaces – Übersicht](../../identity-service/namespaces.md). |
| Erstellt von | Gibt den Anwender an, der diesen Zielfluss erstellt hat. |
| Erstellt | Gibt Datum und Uhrzeit (UTC) an, zu dem/der dieser Zielfluss erstellt wurde. |

## 4. Steuerelemente zum Bearbeiten der Aktivierung und Aktivieren/Deaktivieren des Datenflusses

Mit dem Steuerelement „Aktivierung bearbeiten“ können Sie bearbeiten, welche Segmente dem Ziel zugeordnet werden. Klicken Sie auf „Aktivierung bearbeiten“, um den [Workflow für die Segmentaktivierung](/help/rtcdp/destinations/activate-destinations.md) zu öffnen.

Mit dem Umschalter **Aktivieren/Deaktivieren** können Sie den Datenexport an ein Ziel starten und anhalten.