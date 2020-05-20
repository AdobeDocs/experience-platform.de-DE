---
keywords: Experience Platform;insights; customer ai;popular topics
solution: Experience Platform
title: Kundensegmente mit prognostizierten Werten erstellen
topic: Create a segment
translation-type: tm+mt
source-git-commit: 66ccea896846c1da4310c1077e2dc7066a258063
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 52%

---


# Kundensegmente mit prognostizierten Werten erstellen

Nach Abschluss einer Prognose werden die prognostizierten Tendenzwerte von Profilen automatisch übernommen. Die Anreicherung von Profilen mit Kundentreuewerten ermöglicht die Erstellung von Kundensegmenten, um Audiencen anhand ihrer Tendenzwerte zu finden. In diesem Abschnitt werden Schritte zum Erstellen von Segmenten mit Segment Builder beschrieben. Eine genauere Anleitung zum Erstellen von Segmenten finden Sie im [Segment Builder-Benutzerhandbuch](../../../segmentation/tutorials/create-a-segment.md).

>[!IMPORTANT] Um diese Methode verwenden zu können, muss Echtzeit-Kundendaten-Profil für den Datensatz aktiviert werden.

Klicken Sie in der Benutzeroberfläche von Platform im linken Navigationsbereich auf **[!UICONTROL Segmente]** und dann auf **[!UICONTROL Segment erstellen]**.

![](../images/user-guide/segments.png)

*Segment Builder* wird angezeigt. Klicken Sie in der linken Spalte *Felder* und auf der Registerkarte *Attribute* auf den Ordner **[!UICONTROL Individuelles XDM-Profil]** und dann auf den Ordner mit dem Namespace Ihres Unternehmens. Der Ordner **[!UICONTROL Customer AI]** enthält die Ergebnisse von Prognoseausführungen und wird nach der Instanz benannt, zu der die Werte gehören. Klicken Sie auf einen Instanzordner, um auf die Ergebnisse der gewünschten Instanz zuzugreifen.

![](../images/user-guide/results.png)

Ziehen Sie das Attribut **[!UICONTROL Wert]**, das sich in der Mitte von Segment Builder befindet, in die *Arbeitsfläche zum Erstellen von Regeln*, um eine Regel zu definieren.

Geben Sie in der rechten Spalte *Segmenteigenschaften* einen Namen für das Segment ein.

![](../images/user-guide/properties.png)

Klicken Sie über der Spalte &quot; *Felder* links&quot;auf das **Zahnradsymbol** und wählen Sie aus der Dropdownliste eine Richtlinie *für die* Zusammenführung aus. Click **[!UICONTROL Save]** to create the segment.

![](../images/user-guide/merge_policy.png)

## Nächste Schritte

In diesem Tutorial haben Sie mithilfe des Segmentaufbaus Audiencen anhand ihrer Tendenzwerte erfolgreich gefunden. Sie können Ihre Audiencen jetzt in Zielgruppen aktivieren, indem Sie sie an Zielorten aktivieren. See the [destinations overview](https://docs.adobe.com/content/help/en/experience-platform/rtcdp/destinations/destinations-overview.html) for more information.