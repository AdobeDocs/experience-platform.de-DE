---
title: Datentyp für Berichterstellung zu benutzerdefinierten Metadatendetails
description: Erfahren Sie mehr über den Datentyp „Custom Metadata Details Reporting Experience Data Model“ (XDM).
exl-id: d82d42fb-c725-4a81-9b2a-f6434020ab49
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 10%

---

# [!UICONTROL Benutzerdefinierte Metadatendetails] Reporting-Datentyp

[!UICONTROL Benutzerdefinierte Metadatendetails] Die Berichterstellung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der eine Struktur zum Speichern benutzerdefinierter Metadaten definiert. Der [!UICONTROL Datentyp „Benutzerdefinierte Metadatendetails] erfasst Details wie den Namen und den Wert von benutzerdefinierten Metadaten, die mit Inhalten oder Interaktionen verknüpft sind. Medien-Reporting-Felder werden von Adobe-Services verwendet, um die von Benutzenden gesendeten Mediensammlungsfelder zu analysieren. Diese Daten werden zusammen mit anderen spezifischen Benutzermetriken berechnet und in Berichten erfasst.

![Diagramm zum Datentyp Berichterstellung für benutzerdefinierte Metadatendetails.](../images/data-types/the-custom-metadata-reporting.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Benutzerdefinierter Metadatenfeldname] | `name` | Zeichenfolge | Der Name des benutzerdefinierten Felds. |
| [!UICONTROL Wert des benutzerdefinierten Metadatenfelds] | `value` | Zeichenfolge | Der Wert des benutzerdefinierten Felds. |

{style="table-layout:auto"}
