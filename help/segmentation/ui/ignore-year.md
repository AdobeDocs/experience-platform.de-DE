---
solution: Experience Platform
title: Aktualisierung der Zeitbegrenzung für das Jahr ignorieren
description: Erfahren Sie, wie Sie ein Problem mit der Zeitbegrenzung für das Jahr ignorieren können.
source-git-commit: d0bd7990f0d77cd5f8d30da735b89c188e13c780
workflow-type: tm+mt
source-wordcount: '208'
ht-degree: 0%

---


# Aktualisierung der Jahreszeitbegrenzung ignorieren {#ignore-year}

>[!CONTEXTUALHELP]
>id="platform_audiences_segmentBuilder_ignoreYear"
>title="Jahresaktualisierung ignorieren"
>abstract="Die Zeitbeschränkung für das ignorierte Jahr wurde aktualisiert. Speichern Sie Ihre Audience erneut."

In der Version vom Februar 2024 für Adobe Experience Platform wurden Änderungen am Adobe Experience Platform-Segmentierungsdienst eingeführt, die ein Problem mit der Option &quot;Jahr ignorieren&quot;bei der Erstellung und Auswertung von Zielgruppen beheben.

Die Option &quot;Jahr ignorieren&quot;ist so konzipiert, dass die Jahreskomponente eines Datums bei der Durchführung von Zielgruppenbewertungen ignoriert wird. Sie können diese Option in Situationen verwenden, in denen die zeitliche Beziehung zwischen verschiedenen Ereignissen wichtig ist, das spezifische Jahr jedoch unwichtig ist, z. B. ein Geburtsdatumsfeld.

In Schaltjahren wie 2024 konnte das zugrunde liegende System diese Option jedoch nicht ordnungsgemäß handhaben, was zu ungenauen Zielgruppenbewertungen führte. Wenn also &quot;Jahr ignorieren&quot;in einem Schaltjahr aktiviert ist, würde die Zielgruppenbewertung einen Tag verpassen.

Wenn Sie eine Zielgruppe erstellt haben, bevor diese Korrektur veröffentlicht wurde, müssen Sie die Zielgruppe nur im Segment Builder erneut speichern, um die Korrektur anwenden zu können. Wenn Sie sich nicht sicher sind, ob Ihre Zielgruppe von dieser Lösung betroffen ist, werden Sie vom Segment Builder aufgefordert, den Benutzer aufzufordern, wenn dieses Problem die bestehende Zielgruppe betrifft.
