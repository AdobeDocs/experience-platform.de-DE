---
title: Datenerfassungstyp für benutzerdefinierte Metadatendetails
description: Erfahren Sie mehr über den Datentyp "Custom Metadata Details Collection Experience Data Model (XDM)".
source-git-commit: e9107092b60361216744e154752f48546b5bad73
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 15%

---

# [!UICONTROL Benutzerdefinierte Metadatendetails] Sammlungsdatentyp

[!UICONTROL Benutzerdefinierte Metadatendetails] Die Sammlung ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der eine Struktur zum Speichern benutzerdefinierter Metadaten definiert. Verwenden Sie die [!UICONTROL Benutzerdefinierte Metadatendetails] Sammlungsdatentyp zum Erfassen von Details wie dem Namen und Wert von benutzerdefinierten Metadaten, die mit Inhalten oder Interaktionen verknüpft sind.

![Ein Diagramm des Datentyps für die Sammlung benutzerspezifischer Metadatendetails.](../images/data-types/the-custom-metadata-collection.png)

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|--------------------------------------------|------------------|-----------|----------|-------------------------------|
| [!UICONTROL Benutzerdefinierter Metadatenfeldname] | `name` | Zeichenfolge | Nein | Der Name des benutzerdefinierten Felds. |
| [!UICONTROL Benutzerdefinierter Metadatenfeldwert] | `value` | Zeichenfolge | Nein | Der -Wert des benutzerdefinierten Felds. |

{style="table-layout:auto"}
