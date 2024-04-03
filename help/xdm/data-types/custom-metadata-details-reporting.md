---
title: Berichtdatentyp Benutzerdefinierte Metadatendetails
description: Erfahren Sie mehr über den Datentyp "Custom Metadata Details Reporting Experience Data Model"(XDM).
source-git-commit: a604dc8b541784ace8aedef42030e5bd8b646c28
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 10%

---

# [!UICONTROL Benutzerdefinierte Metadatendetails] Berichtdatentyp

[!UICONTROL Benutzerdefinierte Metadatendetails] Die Berichterstellung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der eine Struktur zum Speichern benutzerdefinierter Metadaten definiert. Die [!UICONTROL Benutzerdefinierte Metadatendetails] Der Berichtdatentyp erfasst Details wie den Namen und den Wert von benutzerdefinierten Metadaten, die mit Inhalten oder Interaktionen verknüpft sind. Medienberichtsfelder werden von Adobe-Diensten verwendet, um die von Benutzern gesendeten Mediensammlungsfelder zu analysieren. Diese Daten werden zusammen mit anderen spezifischen Benutzermetriken berechnet und in Berichten verwendet.

![Ein Diagramm des Datentyps &quot;Custom Metadata Details Reporting&quot;.](../images/data-types/the-custom-metadata-reporting.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Benutzerdefinierter Metadatenfeldname] | `name` | Zeichenfolge | Der Name des benutzerdefinierten Felds. |
| [!UICONTROL Benutzerdefinierter Metadatenfeldwert] | `value` | Zeichenfolge | Der -Wert des benutzerdefinierten Felds. |

{style="table-layout:auto"}
