---
title: Datentyp der Datenerfassung für Advertising Pod-Details
description: Erfahren Sie mehr über den Datentyp Advertising Pod Details Collection Experience Data Model (XDM).
exl-id: 401c393f-aeda-4ecd-89f4-458833190ced
source-git-commit: 9350cfc299c20bd63a2a559c177b3af02739e5b9
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 8%

---

# [!UICONTROL Advertising Pod-], Sammlungsdatentyp

[!UICONTROL Advertising Pod-]: Die Sammlung ist ein standardmäßiger Datentyp des Experience-Datenmodells (XDM). Sie definiert eine Sequenz oder Gruppe von Anzeigen, die normalerweise nacheinander während der Inhaltspausen abgespielt werden. Verwenden Sie den Datentyp [!UICONTROL Advertising Pod Details]-Sammlung, um Details wie die Anzeigenunterbrechungs-ID, einen Anzeigenamen für die Anzeigenunterbrechung, den Index der Anzeigen innerhalb der Unterbrechung und den Versatz der Anzeigenunterbrechung innerhalb der Zeitleiste des Inhalts in Sekunden zu erfassen.

![Abbildung des Datentyps für die Datenerfassung von Advertising Pod-Details.](../images/data-types/advertising-pod-details-collection.png)

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|-----------------------------------------|-----------------|-----------|----------|---------------------------------------------------------|
| [!UICONTROL Anzeige in Position Pod] | `index` | integer | Ja | Der Index der Anzeige innerhalb des übergeordneten Anzeigenunterbrechungsstarts. |
| [!UICONTROL Anzeigename des Pod] | `friendlyName` | Zeichenfolge | Nein | Der leicht verständliche Name der Werbeunterbrechung. |
| [!UICONTROL Pod-Versatz] | `offset` | integer | Ja | Der Versatz der Werbeunterbrechung innerhalb des Inhalts in Sekunden. |

{style="table-layout:auto"}
