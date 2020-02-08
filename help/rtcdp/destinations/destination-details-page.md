---
title: Zieldetailseite
seo-title: Zieldetailseite
description: 'Die Detailseite für ein einzelnes Ziel bietet einen Überblick über die Zieldetails, wie den Zielnamen, die ID, die dem Ziel zugeordneten Segmente und die Steuerelemente zum Bearbeiten der Aktivierung und zum Aktivieren und Deaktivieren des Datenflusses. '
seo-description: 'Die Detailseite für ein einzelnes Ziel bietet einen Überblick über die Zieldetails, wie den Zielnamen, die ID, die dem Ziel zugeordneten Segmente und die Steuerelemente zum Bearbeiten der Aktivierung und zum Aktivieren und Deaktivieren des Datenflusses. '
translation-type: tm+mt
source-git-commit: b784b67092ea8d30ad00cda9a40779b3890862fd

---


# Zieldetailseite {#destinations-details-page}

Die Detailseite für ein einzelnes Ziel bietet einen Überblick über die Zieldetails, wie den Zielnamen, die ID, die dem Ziel zugeordneten Segmente und die Steuerelemente zum Bearbeiten der Aktivierung und zum Aktivieren und Deaktivieren des Datenflusses. Um diese Details anzuzeigen, gehen Sie zu **Ziele** > **Durchsuchen** und klicken Sie auf den Namen des Ziels, mit dem Sie arbeiten möchten.

Hauptkomponenten eines einzelnen Ziels sind:

* 1 - Zielname und ID
* 2 - Am Ziel aktivierte Segmente
* 3 - Informationen zur rechten Schiene
* 4 - Steuerelemente zum Bearbeiten der Aktivierung und Aktivieren/Deaktivieren des Datenflusses

![Nummerierte Zielseite](/help/rtcdp/destinations/assets/destination-page-numbered.png)

Navigieren Sie zu einer einzelnen Zielseite, um einen Überblick über die Zieldetails zu erhalten, z. B.:

## 1. Zielname und ID

Sie können den Zielnamen in der Seitenüberschrift und die Ziel-ID in der Seiten-URL sehen.

## 2. Am Ziel aktivierte Segmente

Dieser Abschnitt zeigt, welche Segmente derzeit dem Ziel zugeordnet sind, sowie weitere Informationen zu diesen Segmenten. Weitere Informationen finden Sie in der nachstehenden Tabelle:

| Element | Beschreibung |
---------|----------|
| Segmentname | Der Name Ihres Segments. |
| Segmentbeschreibung | Die Beschreibung Ihres Segments. |
| Startdatum | Das Datum, ab dem diese Segmente zum Ziel aktiviert werden. |
| Enddatum | Das Datum, an dem diese Segmente nicht mehr am Ziel aktiviert werden. |
| Mapping-ID | *Nicht verfügbar für E-Mail-Marketing-Ziele*. Gibt die ID an, mit der das Segment in der Zielplattform bekannt ist. |

## 3. Informationen zur rechten Schiene

Die rechte Leiste enthält Informationen über Ihr Ziel. Weitere Informationen finden Sie in der unten stehenden Tabelle:

| Element | Beschreibung |
---------|----------|
| Plattform | Stellt die Zielplattform dar, an die Zielgruppen gesendet werden. Weitere Informationen finden Sie unter [Zielkatalog](/help/rtcdp/destinations/destinations-catalog.md) . |
| Beschreibung | Sie können die Beschreibung Ihres Zielflusses bearbeiten. |
| Kategorie | Gibt den Zieltyp an. Weitere Informationen finden Sie unter [Zielkatalog](/help/rtcdp/destinations/destinations-catalog.md) . |
| Verbindungstyp | Gibt an, in welcher Form Ihre Zielgruppen an das Ziel gesendet werden. Kann **Cookie** oder **profilbasiert** sein. |
| Häufigkeit | Gibt an, wie oft die Zielgruppen an das Ziel gesendet werden. Kann **Streaming** oder **Batch** sein. |
| Identität | Stellt den vom Ziel akzeptierten Identitäts-Namespace dar. Das Identitätsfeld kann beispielsweise GAID, IDFA, E-Mail lauten. Informationen zu allen akzeptierten Identitätsnamen finden Sie unter Standardnamensräume in der Übersicht über den [Identitäts-Namespace](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md). |
| Erstellt von | Gibt den Benutzer an, der diesen Zielfluss erstellt hat. |
| Erstellt | Gibt das UTC-Datum und die Uhrzeit an, zu der dieser Zielfluss erstellt wurde. |

## 4. Steuerelemente zum Bearbeiten der Aktivierung und Aktivieren/Deaktivieren des Datenflusses

Mit dem Aktivierungssteuerelement Bearbeiten können Sie bearbeiten, welche Segmente dem Ziel zugeordnet werden. Klicken Sie auf Aktivierung bearbeiten, um den Arbeitsablauf für die [Segmentaktivierung](/help/rtcdp/destinations/activate-destinations.md)zu öffnen.

Mit dem Umschalter &quot; **Aktivieren/Deaktivieren** &quot;können Sie den Datenexport an ein Ziel starten und anhalten.