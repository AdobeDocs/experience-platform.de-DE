---
title: Datentyp mit Details zur Werbeunterbrechung
description: Erfahren Sie mehr über den Datentyp "Experience-Datenmodell (XDM)"für Details der Werbeunterbrechung.
source-git-commit: 65f3dcf1cacfbc4e8a598244810d238bd88f64bd
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 6%

---

# [!UICONTROL Details der Werbeunterbrechung] Datentyp

[!UICONTROL Details der Werbeunterbrechung] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp. Sie definiert eine Sequenz oder Gruppe von Anzeigen, die in der Regel während Inhaltsunterbrechungen nacheinander wiedergegeben werden. Verwenden Sie die [!UICONTROL Details der Werbeunterbrechung] Datentyp , um Details wie die ID der Werbeunterbrechung, einen Anzeigennamen für die Werbeunterbrechung, den Index der Anzeigen innerhalb der Werbeunterbrechung und den Offset der Werbeunterbrechung innerhalb der Timeline des Inhalts in Sekunden zu erfassen.

![Ein Diagramm des Datentyps Details der Werbeunterbrechung .](../images/data-types/advertising-pod-details-information.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID der Werbeunterbrechung] | `ID` | Zeichenfolge | Die ID der Werbeunterbrechung. |
| [!UICONTROL Anzeigename der Werbeunterbrechung] | `friendlyName` | Zeichenfolge | Der leicht verständliche Name der Werbeunterbrechung. |
| [!UICONTROL Anzeigenposition innerhalb der Werbeunterbrechung] | `index` | integer | Der Index der Anzeige innerhalb des Starts der übergeordneten Werbeunterbrechung. |
| [!UICONTROL Werbeunterbrechung] | `offset` | integer | **Erforderlich** Der Versatz der Werbeunterbrechung innerhalb des Inhalts in Sekunden. |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
