---
keywords: Experience Platform;Insights;Kunden-KI;beliebte Themen;Kunden-KI-Segmente
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Erstellen von Kundensegmenten mit prognostizierten Scores
description: Nach Abschluss einer Prognose werden die prognostizierten Tendenzwerte von Profilen automatisch übernommen. Ein Anreichern von Profilen mit Customer AI-Werten ermöglicht eine Erstellung von Kundensegmenten, die Zielgruppen basierend auf ihren Tendenzwerten finden. In diesem Abschnitt finden Sie Schritte zum Erstellen von Segmenten mit Segment Builder.
exl-id: ac81f798-f599-4a8d-af25-c00c92e74b4e
source-git-commit: 73dea391f8fcb1d2d491c814b453afb4e538459d
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 66%

---

# Kundensegmente mit prognostizierten Werten erstellen

Nach Abschluss einer Prognose werden die prognostizierten Tendenzwerte von Profilen automatisch übernommen. Ein Anreichern von Profilen mit Customer AI-Werten ermöglicht eine Erstellung von Kundensegmenten, die Zielgruppen basierend auf ihren Tendenzwerten finden. In diesem Abschnitt werden Schritte zum Erstellen von Segmenten mit Segment Builder beschrieben. Eine genauere Anleitung zum Erstellen von Segmenten finden Sie im [Segment Builder-Benutzerhandbuch](../../../segmentation/ui/segment-builder.md).

>[!IMPORTANT]
>
>Um diese Methode verwenden zu können, muss das Echtzeit-Kundenprofil für den Datensatz aktiviert sein.

Klicken Sie in der Benutzeroberfläche von Experience Platform **[!UICONTROL Segmente]** im linken Navigationsbereich und klicken Sie dann auf **[!UICONTROL Segment erstellen]**.

![Screenshot der Seite „Segmente“ in der Experience Platform-Benutzeroberfläche mit der Option zum Erstellen eines neuen Segments.](../images/user-guide/segments_new.png)

**Segment Builder** wird angezeigt. Klicken Sie in der linken Spalte **[!UICONTROL Felder]** und auf der Registerkarte **[!UICONTROL Attribute]** auf den Ordner **[!UICONTROL XDM Individual Profile]** und dann auf den Ordner mit dem Namespace Ihres Unternehmens. Der Ordner **[!UICONTROL Customer AI]** enthält die Ergebnisse von Prognoseausführungen und wird nach der Instanz benannt, zu der die Werte gehören. Klicken Sie auf einen Instanzordner, um auf die Ergebnisse der gewünschten Instanz zuzugreifen.

![](../images/user-guide/results_new.png)

Ziehen Sie das Attribut **[!UICONTROL Wert]**, das sich in der Mitte von Segment Builder befindet, in die *Arbeitsfläche zum Erstellen von Regeln*, um eine Regel zu definieren.

Geben Sie in der rechten Spalte *Segmenteigenschaften* einen Namen für das Segment ein.

![](../images/user-guide/properties_new.png)

Klicken Sie über der linken Spalte *Felder* auf das Symbol **Zahnrad** und wählen Sie *Zusammenführungsrichtlinie* aus der Dropdown-Liste. Klicken Sie auf **[!UICONTROL Speichern]**, um das Segment zu erstellen.

![](../images/user-guide/merge_policy_new.png)

## Nächste Schritte

In diesem Tutorial haben Sie mithilfe von Segment Builder erfolgreich Zielgruppen gefunden, die auf ihren Neigungs-Scores basieren. Sie können nun Ihre Zielgruppen ansprechen, indem Sie diese für Ziele aktivieren. Weiterführende Informationen dazu finden Sie unter [Ziele – Übersicht](../../../destinations/home.md).
