---
title: Berichtdatentyp für Details der Werbeunterbrechung
description: Erfahren Sie mehr über den Datentyp des Experience-Datenmodells (XDM) für Details der Werbeunterbrechung.
source-git-commit: b6b916c76d1b2babb673d419ab69ae414dd42f20
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 6%

---

# [!UICONTROL Reporting zu Details der Werbeunterbrechung] Datentyp

[!UICONTROL Reporting zu Details der Werbeunterbrechung] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp. Sie definiert eine Sequenz oder Gruppe von Anzeigen, die in der Regel während Inhaltsunterbrechungen nacheinander wiedergegeben werden. Verwenden Sie die [!UICONTROL Reporting zu Details der Werbeunterbrechung] Datentyp , um Details wie die ID der Werbeunterbrechung, einen Anzeigennamen für die Werbeunterbrechung, den Index der Anzeigen innerhalb der Werbeunterbrechung und den Offset der Werbeunterbrechung innerhalb der Timeline des Inhalts in Sekunden zu erfassen.

![Ein Diagramm des Datentyps Werbeunterbrechungsdetails Berichterstellung .](../images/data-types/advertising-pod-details-information.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL ID der Werbeunterbrechung] | `ID` | Zeichenfolge | Die ID der Werbeunterbrechung. |
| [!UICONTROL Anzeigename der Werbeunterbrechung] | `friendlyName` | Zeichenfolge | Der leicht verständliche Name der Werbeunterbrechung. |
| [!UICONTROL Anzeigenposition innerhalb der Werbeunterbrechung] | `index` | integer | Der Index der Anzeige innerhalb des Starts der übergeordneten Werbeunterbrechung. |
| [!UICONTROL Werbeunterbrechung] | `offset` | integer | **Erforderlich** Der Versatz der Werbeunterbrechung innerhalb des Inhalts in Sekunden. |

{style="table-layout:auto"}

Weiterführende Informationen zur Feldergruppe finden Sie im Abschnitt [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
