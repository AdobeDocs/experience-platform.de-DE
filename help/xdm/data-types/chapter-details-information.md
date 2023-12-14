---
title: Datentyp "Kapiteldetails"
description: Erfahren Sie mehr über den Datentyp "Kapiteldetails-Informationen - Experience-Datenmodell (XDM)".
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '195'
ht-degree: 7%

---

# [!UICONTROL Kapiteldetails] Datentyp

[!UICONTROL Kapiteldetails] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der verschiedene Attribute beschreibt, die sich auf Kapitel oder Segmente in Medieninhalten beziehen. Verwenden Sie die [!UICONTROL Kapiteldetails] Datentyp , um Details wie Kapitelname, Dauer, Position, ID, Wiedergabestatus (gestartet/abgeschlossen) und die für jedes Kapitel verbrachte Zeit zu erfassen.

![Ein Diagramm des Datentyps Kapiteldetails .](../images/data-types/chapter-details-information.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|---------------------------|---------------|-----------|---------------------------------------------------|
| [!UICONTROL Kapitelname] | `friendlyName` | Zeichenfolge | Der Name des Kapitels und/oder Segments. |
| [!UICONTROL Kapitellänge oder -dauer] | `length` | integer | **Erforderlich** Die Länge des Kapitels in Sekunden. |
| [!UICONTROL Kapiteloffset] | `offset` | integer | **Erforderlich** Der Versatz des Kapitels innerhalb des Inhalts ab Beginn (in Sekunden). |
| [!UICONTROL Kapitelposition] | `index` | integer | **Erforderlich** Die Position (Index, Integer) des Kapitels im Inhalt. |
| [!UICONTROL Kapitel-ID] | `ID` | Zeichenfolge | Die automatisch generierte ID des Kapitels. |
| [!UICONTROL Kapitel gestartet] | `isStarted` | boolean | Gibt an, ob das Kapitel begonnen hat. |
| [!UICONTROL Kapitel abgeschlossen] | `isCompleted` | boolean | Gibt an, ob das Kapitel abgeschlossen ist. |
| [!UICONTROL Wiedergabe des Kapitels] | `timePlayed` | integer | Die mit dem Kapitel verbrachte Zeit in Sekunden. |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/chapterdetails.schema.json)
