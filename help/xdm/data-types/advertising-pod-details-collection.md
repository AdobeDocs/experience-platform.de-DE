---
title: Datenerfassungstyp für Advertising-Pod-Details
description: Erfahren Sie mehr über den Datentyp Advertising Pod Details Collection Experience Data Model (XDM) .
exl-id: 401c393f-aeda-4ecd-89f4-458833190ced
source-git-commit: 9350cfc299c20bd63a2a559c177b3af02739e5b9
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 8%

---

# [!UICONTROL Advertising Pod Details] Sammlungsdatentyp

[!UICONTROL Advertising Pod Details] Collection ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp. Sie definiert eine Sequenz oder Gruppe von Anzeigen, die in der Regel während Inhaltsunterbrechungen nacheinander wiedergegeben werden. Verwenden Sie den Datentyp [!UICONTROL Advertising-Werbeunterbrechungsdetails], um Details wie die Werbeunterbrechungs-ID, einen Anzeigennamen für die Werbeunterbrechung, den Index der Anzeigen innerhalb der Werbeunterbrechung und den Versatz der Werbeunterbrechung innerhalb der Timeline des Inhalts in Sekunden zu erfassen.

![Ein Diagramm des Datentyps &quot;Advertising Pod Details Collection Information Collection&quot;.](../images/data-types/advertising-pod-details-collection.png)

| Anzeigename | Eigenschaft | Datentyp | Erforderlich | Beschreibung |
|-----------------------------------------|-----------------|-----------|----------|---------------------------------------------------------|
| [!UICONTROL Anzeigenposition innerhalb der Werbeunterbrechung] | `index` | integer | Ja | Der Index der Anzeige innerhalb des Starts der übergeordneten Werbeunterbrechung. |
| [!UICONTROL Pod Friendly Name] | `friendlyName` | Zeichenfolge | Nein | Der leicht verständliche Name der Werbeunterbrechung. |
| [!UICONTROL Pod offset] | `offset` | integer | Ja | Der Versatz der Werbeunterbrechung innerhalb des Inhalts in Sekunden. |

{style="table-layout:auto"}
