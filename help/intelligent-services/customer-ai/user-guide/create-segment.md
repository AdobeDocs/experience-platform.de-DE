---
keywords: Experience Platform;insights; customer ai;popular topics
solution: Experience Platform
title: Kundensegmente mit prognostizierten Werten erstellen
topic: Create a segment
translation-type: tm+mt
source-git-commit: fba6ae701a38737812dccbf4f63e5a07f935ad8b
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 87%

---


# Kundensegmente mit prognostizierten Werten erstellen

Nach Abschluss einer Prognose werden die prognostizierten Tendenzwerte von Profilen automatisch übernommen. Ein Anreichern von Profilen mit Customer AI-Werten ermöglicht eine Erstellung von Kundensegmenten, die Zielgruppen basierend auf ihren Tendenzwerten finden. In diesem Abschnitt werden Schritte zum Erstellen von Segmenten mit Segment Builder beschrieben. Eine genauere Anleitung zum Erstellen von Segmenten finden Sie im [Segment Builder-Benutzerhandbuch](../../../segmentation/ui/overview.md).

>[!IMPORTANT]
>
>Um diese Methode verwenden zu können, muss das Echtzeit-Kundenprofil für den Datensatz aktiviert werden.

Klicken Sie in der Benutzeroberfläche von Platform im linken Navigationsbereich auf **[!UICONTROL Segmente]** und dann auf **[!UICONTROL Segment erstellen]**.

![](../images/user-guide/segments.png)

*Segment Builder* wird angezeigt. Klicken Sie in der linken Spalte *Felder* und auf der Registerkarte *Attribute* auf den Ordner **[!UICONTROL XDM Individual Profile]** und dann auf den Ordner mit dem Namespace Ihres Unternehmens. Der Ordner **[!UICONTROL Customer AI]** enthält die Ergebnisse von Prognoseausführungen und wird nach der Instanz benannt, zu der die Werte gehören. Klicken Sie auf einen Instanzordner, um auf die Ergebnisse der gewünschten Instanz zuzugreifen.

![](../images/user-guide/results.png)

Ziehen Sie das Attribut **[!UICONTROL Wert]**, das sich in der Mitte von Segment Builder befindet, in die *Arbeitsfläche zum Erstellen von Regeln*, um eine Regel zu definieren.

Geben Sie in der rechten Spalte *Segmenteigenschaften* einen Namen für das Segment ein.

![](../images/user-guide/properties.png)

Above the left-hand *Fields* column, click the **gear** icon and select a *Merge policy* from the drop-down. Klicken Sie auf **[!UICONTROL Speichern]**, um das Segment zu erstellen.

![](../images/user-guide/merge_policy.png)

## Nächste Schritte

In diesem Tutorial haben Sie mithilfe des Segmentaufbaus Audiencen anhand ihrer Tendenzwerte erfolgreich gefunden. Sie können nun Ihre Zielgruppen ansprechen, indem Sie diese für Ziele aktivieren. Weiterführende Informationen dazu finden Sie unter [Ziele – Übersicht](https://docs.adobe.com/content/help/de-DE/experience-platform/rtcdp/destinations/destinations-overview.html).