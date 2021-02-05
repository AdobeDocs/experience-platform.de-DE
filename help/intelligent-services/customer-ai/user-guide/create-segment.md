---
keywords: Experience Platform;Einblicke;Kundenwerbung;beliebte Themen;Kundendienstsegmente
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Erstellen von Kundensegmenten mit prognostizierten Ergebnissen
topic: Create a segment
description: Nach Abschluss einer Prognose werden die prognostizierten Tendenzwerte von Profilen automatisch übernommen. Ein Anreichern von Profilen mit Customer AI-Werten ermöglicht eine Erstellung von Kundensegmenten, die Zielgruppen basierend auf ihren Tendenzwerten finden. In diesem Abschnitt werden Schritte zum Erstellen von Segmenten mit Segment Builder beschrieben.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 83%

---


# Kundensegmente mit prognostizierten Werten erstellen

Nach Abschluss einer Prognose werden die prognostizierten Tendenzwerte von Profilen automatisch übernommen. Ein Anreichern von Profilen mit Customer AI-Werten ermöglicht eine Erstellung von Kundensegmenten, die Zielgruppen basierend auf ihren Tendenzwerten finden. In diesem Abschnitt werden Schritte zum Erstellen von Segmenten mit Segment Builder beschrieben. Eine genauere Anleitung zum Erstellen von Segmenten finden Sie im [Segment Builder-Benutzerhandbuch](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Um diese Methode verwenden zu können, muss das Echtzeit-Kundenprofil für den Datensatz aktiviert werden.

Klicken Sie in der Benutzeroberfläche von Platform im linken Navigationsbereich auf **[!UICONTROL Segmente]** und dann auf **[!UICONTROL Segment erstellen]**.

![](../images/user-guide/segments.png)

**Segment Builder** wird angezeigt. Klicken Sie in der linken Spalte **[!UICONTROL Felder]** und auf der Registerkarte **[!UICONTROL Attribute]** auf den Ordner **[!UICONTROL XDM Individual Profile]** und dann auf den Ordner mit dem Namespace Ihres Unternehmens. Der Ordner **[!UICONTROL Customer AI]** enthält die Ergebnisse von Prognoseausführungen und wird nach der Instanz benannt, zu der die Werte gehören. Klicken Sie auf einen Instanzordner, um auf die Ergebnisse der gewünschten Instanz zuzugreifen.

![](../images/user-guide/results.png)

Ziehen Sie das Attribut **[!UICONTROL Wert]**, das sich in der Mitte von Segment Builder befindet, in die *Arbeitsfläche zum Erstellen von Regeln*, um eine Regel zu definieren.

Geben Sie in der rechten Spalte *Segmenteigenschaften* einen Namen für das Segment ein.

![](../images/user-guide/properties.png)

Klicken Sie über der Spalte *Felder* auf das Symbol **Zahnrad** und wählen Sie aus der Dropdownliste eine *Richtlinie zusammenführen*. Klicken Sie auf **[!UICONTROL Speichern]**, um das Segment zu erstellen.

![](../images/user-guide/merge_policy.png)

## Nächste Schritte

In diesem Tutorial haben Sie mithilfe des Segmentaufbaus Audiencen anhand ihrer Tendenzwerte erfolgreich gefunden. Sie können nun Ihre Zielgruppen ansprechen, indem Sie diese für Ziele aktivieren. Weiterführende Informationen dazu finden Sie unter [Ziele – Übersicht](../../../destinations/home.md).