---
title: Advertising-Berichtdatentyp zu Details der Werbeunterbrechung
description: Erfahren Sie mehr über den Datentyp Advertising Pod Details Reporting Experience Data Model (XDM) .
exl-id: 5164520f-8c48-4eb0-a0b0-66dc10b68356
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 6%

---

# Datentyp [!UICONTROL Advertising Pod Details Reporting]

[!UICONTROL Advertising Pod Details Reporting] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp. Sie definiert eine Sequenz oder Gruppe von Anzeigen, die in der Regel während Inhaltsunterbrechungen nacheinander wiedergegeben werden. Verwenden Sie den Datentyp &quot;[!UICONTROL Advertising-Werbeunterbrechungs-Berichterstellung]&quot;, um Details wie die Werbeunterbrechungs-ID, einen Anzeigennamen für die Werbeunterbrechung, den Index der Anzeigen innerhalb der Werbeunterbrechung und den Versatz der Werbeunterbrechung innerhalb der Timeline des Inhalts in Sekunden zu erfassen.

![Ein Diagramm des Datentyps Advertising Pod Details Reporting.](../images/data-types/advertising-pod-details-information.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL Werbeunterbrechungs-ID] | `ID` | Zeichenfolge | Die ID der Werbeunterbrechung. |
| [!UICONTROL Pod Friendly Name] | `friendlyName` | Zeichenfolge | Der leicht verständliche Name der Werbeunterbrechung. |
| [!UICONTROL Anzeigenposition innerhalb der Werbeunterbrechung] | `index` | integer | Der Index der Anzeige innerhalb des Starts der übergeordneten Werbeunterbrechung. |
| [!UICONTROL Pod offset] | `offset` | integer | **Erforderlich** Der Versatz der Werbeunterbrechung innerhalb des Inhalts in Sekunden. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
