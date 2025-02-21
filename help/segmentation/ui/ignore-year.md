---
solution: Experience Platform
title: Update der Jahreszeitbeschränkung ignorieren
description: Erfahren Sie, wie Sie ein Problem mit der Zeitbeschränkung „Jahr ignorieren“ beheben.
hidefromtoc: true
exl-id: 44bb8817-e32d-4806-ad4e-b1840313e768
source-git-commit: c7d71113ddcef6aca8b2637814b46e589a6b7fdf
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 8%

---

# Aktualisierung der Jahreszeitbegrenzung ignorieren {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="Jahresaktualisierung ignorieren"
>abstract="Das Ignorieren der Aktualisierung der Jahreszeitbegrenzung wurde aktualisiert. Speichern Sie Ihre Zielgruppe erneut."

>[!IMPORTANT]
>
>Sie können die Zeitbeschränkung „Jahr ignorieren“ nur in einer Segmentdefinition verwenden, die mithilfe der **Batch-Segmentierung“ ausgewertet**. Wenn Sie Ihrer Segmentdefinition die Zeitbeschränkung „Jahr ignorieren“ hinzufügen, wird die resultierende Zielgruppe **nicht** Streaming oder Edge-Segmentierung geeignet.

In der Version vom Februar 2024 für Adobe Experience Platform wurden Änderungen am Adobe Experience Platform Segmentation Service eingeführt, die ein Problem mit der Option „Jahr ignorieren“ bei der Erstellung und Auswertung von Zielgruppen beheben.

Die Option „Jahr ignorieren“ soll bei der Durchführung von Zielgruppenbewertungen die Jahreskomponente eines Datums ignorieren. Sie können diese Option in Situationen verwenden, in denen die zeitliche Beziehung zwischen verschiedenen Ereignissen wichtig ist, das bestimmte Jahr jedoch unwichtig ist, z. B. in einem Feld Geburtsdatum .

In Schaltjahren wie 2024 konnte das zugrunde liegende System diese Option jedoch nicht ordnungsgemäß verarbeiten, was zu ungenauen Zielgruppenbewertungen führte. Wenn in einem Schaltjahr „Jahr ignorieren“ aktiviert ist, würde die Zielgruppenbewertung einen Tag verpassen.

Wenn Sie eine Zielgruppe erstellt haben, bevor diese Fehlerbehebung veröffentlicht wurde, müssen Sie nur die Zielgruppe im Segment Builder erneut speichern, um die Fehlerbehebung anzuwenden. Wenn Sie sich nicht sicher sind, ob Ihre Zielgruppe von dieser Auflösung betroffen ist, fordert Sie Segment Builder auf, anzugeben, ob die vorhandene Zielgruppe von diesem Problem betroffen ist.
