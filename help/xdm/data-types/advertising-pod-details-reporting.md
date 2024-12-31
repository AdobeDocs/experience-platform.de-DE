---
title: Berichtdatentyp "Advertising Pod-Details“
description: Erfahren Sie mehr über den Datentyp Advertising Pod Details Reporting Experience Data Model (XDM).
exl-id: 5164520f-8c48-4eb0-a0b0-66dc10b68356
source-git-commit: 799a384556b43bc844782d8b67416c7eea77fbf0
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 6%

---

# [!UICONTROL Advertising Pod-]-Datentyp

Die Berichterstellung für [!UICONTROL Advertising Pod] ist ein standardmäßiger Datentyp des Experience-Datenmodells (XDM). Sie definiert eine Sequenz oder Gruppe von Anzeigen, die normalerweise nacheinander während der Inhaltspausen abgespielt werden. Verwenden Sie den Datentyp [!UICONTROL Advertising Pod Details Reporting], um Details wie die Anzeigenunterbrechungs-ID, einen Anzeigenamen für die Anzeigenunterbrechung, den Index der Anzeigen innerhalb der Unterbrechung und den Versatz der Anzeigenunterbrechung innerhalb der Zeitleiste des Inhalts in Sekunden zu erfassen.

![Abbildung des Reporting-Datentyps für Advertising-Pod-Details.](../images/data-types/advertising-pod-details-information.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|----------------------------|------------------------|-----------|-------------------------------------------------------|
| [!UICONTROL Werbeunterbrechungs-ID] | `ID` | Zeichenfolge | Die ID der Werbeunterbrechung. |
| [!UICONTROL Anzeigename des Pod] | `friendlyName` | Zeichenfolge | Der leicht verständliche Name der Werbeunterbrechung. |
| [!UICONTROL Anzeige in Position Pod] | `index` | integer | Der Index der Anzeige innerhalb des übergeordneten Anzeigenunterbrechungsstarts. |
| [!UICONTROL Pod-Versatz] | `offset` | integer | **Erforderlich** Der Versatz der Anzeigenunterbrechung im Inhalt in Sekunden. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie im [öffentlichen XDM-Repository](https://github.com/adobe/xdm/blob/master/components/datatypes/advertisingpoddetails.schema.json)
