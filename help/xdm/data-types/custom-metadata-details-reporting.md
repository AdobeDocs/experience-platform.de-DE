---
title: Berichtdatentyp Benutzerdefinierte Metadatendetails
description: Erfahren Sie mehr über den Datentyp "Custom Metadata Details Reporting Experience Data Model"(XDM).
exl-id: d82d42fb-c725-4a81-9b2a-f6434020ab49
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 10%

---

# [!UICONTROL Custom Metadata Details] Berichtdatentyp

[!UICONTROL Benutzerspezifische Metadatendetails] Die Berichterstellung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der eine Struktur zum Speichern benutzerdefinierter Metadaten definiert. Der Berichtdatentyp [!UICONTROL Benutzerdefinierte Metadatendetails] erfasst Details wie den Namen und den Wert benutzerdefinierter Metadaten, die mit Inhalten oder Interaktionen verknüpft sind. Medienberichtsfelder werden von Adobe-Diensten verwendet, um die von Benutzern gesendeten Mediensammlungsfelder zu analysieren. Diese Daten werden zusammen mit anderen spezifischen Benutzermetriken berechnet und in Berichten verwendet.

![Ein Diagramm des Datentyps &quot;Custom Metadata Details Reporting&quot;.](../images/data-types/the-custom-metadata-reporting.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Benutzerdefinierter Metadatenfeldname] | `name` | Zeichenfolge | Der Name des benutzerdefinierten Felds. |
| [!UICONTROL Benutzerdefinierter Metadatenfeldwert] | `value` | Zeichenfolge | Der -Wert des benutzerdefinierten Felds. |

{style="table-layout:auto"}
