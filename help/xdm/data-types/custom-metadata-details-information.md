---
title: Datentyp "Benutzerdefinierte Metadatendetails"
description: Erfahren Sie mehr über den Datentyp "Custom Metadata Details Experience Data Model"(XDM).
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '122'
ht-degree: 11%

---

# [!UICONTROL Informationen zu benutzerspezifischen Metadaten] Datentyp

[!UICONTROL Informationen zu benutzerspezifischen Metadaten] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der eine Struktur zum Speichern benutzerdefinierter Metadaten definiert. Verwenden Sie die [!UICONTROL Informationen zu benutzerspezifischen Metadaten] Datentyp zum Erfassen von Details wie dem Namen und Wert von benutzerdefinierten Metadaten, die mit Inhalten oder Interaktionen verknüpft sind.

![Ein Diagramm des Datentyps Benutzerdefinierte Metadatendetails .](../images/data-types/custom-metadata-details-information.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|--------------------------------------------|------------------|-----------|-----------------------------------------|
| [!UICONTROL Benutzerdefinierter Metadatenfeldname] | `name` | Zeichenfolge | Der Name des benutzerdefinierten Felds. |
| [!UICONTROL Benutzerdefinierter Metadatenfeldwert] | `value` | Zeichenfolge | Der -Wert des benutzerdefinierten Felds. |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/custommetadatadetails.schema.json)
