---
keywords: Experience Platform; Modell für maschinelles Lernen; Data Science Workspace; Echtzeit-Kundenprofil; beliebte Themen; Einblicke in maschinelles Lernen
solution: Experience Platform
title: Anreicherung des Echtzeit-Kundenprofils mit Einblicken aus maschinellem Lernen
type: Tutorial
description: Dieses Dokument bietet eine Anleitung zur Anreicherung des Echtzeit-Kundenprofils mit Einblicken aus maschinellem Lernen.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 13%

---

# Anreicherung von [!DNL Real-Time Customer Profile] mit Einblicken aus maschinellem Lernen

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Adobe Experience Platform [!DNL Data Science Workspace] bietet die Tools und Ressourcen zum Erstellen, Auswerten und Verwenden maschineller Lernmodelle, um Datenprognosen und Einblicke zu generieren. Wenn Einblicke aus maschinellem Lernen in einen [!DNL Profile]-aktivierten Datensatz aufgenommen werden, werden dieselben Daten auch als [!DNL Profile]-Datensätze erfasst, die dann mit [!DNL Adobe Experience Platform Segmentation Service] segmentiert werden können.

Der Segmentierungsprozess hängt von der Auswertungsmethode für die Zielgruppe ab. Wenn eine Zielgruppe als **Streaming** konfiguriert ist, werden alle neuen vom Modell in das Profil geschriebenen Aktualisierungen in Echtzeit verarbeitet. Wenn jedoch eine Zielgruppe für die Auswertung von **Batch** konfiguriert ist, werden die neuen Werte im nächsten Batch ausgewertet.

Dieses Dokument enthält Links zu Tutorials, mit denen Sie [!DNL Real-Time Customer Profile] mit Ihren Einblicken aus maschinellem Lernen anreichern können.

## Erste Schritte

Um die unten stehenden Tutorials abzuschließen, benötigen Sie ein Verständnis für die Aufnahme von [!DNL Profile] -Daten und die Erstellung von Zielgruppen. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet eine vollständige, einheitliche Darstellung jedes einzelnen Kunden auf der Grundlage aggregierter Daten aus mehreren Quellen.
- [[!DNL Identity Service]](../../identity-service/home.md): Aktiviert [!DNL Real-Time Customer Profile] durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, die in Platform erfasst werden.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.

Neben den oben genannten Dokumenten sollten Sie auch folgende Leitfäden zu Schemata und dem Schema-Editor lesen:

- [Grundlagen der Schemakomposition](../../xdm/schema/composition.md): Beschreibt XDM-Schemas, Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in [!DNL Experience Platform] verwendet werden sollen.
- [Tutorial zum Schema-Editor](../../xdm/tutorials/create-schema-ui.md): Enthält ausführliche Anweisungen zum Erstellen von Schemas mit dem Schema-Editor in [!DNL Experience Platform].

## Ausgabeschema und -datensatz erstellen und konfigurieren {#create-an-output-schema-and-dataset}

Der erste Schritt zur Anreicherung von [!DNL Real-Time Customer Profile] mit Scoring-Einblicken besteht darin zu wissen, welches reale Objekt (z. B. eine Person) Ihre Daten definieren. Wenn Sie Ihre Daten verstehen, können Sie eine Struktur beschreiben und entwerfen, um Bedeutung hinzuzufügen, ähnlich wie beim Entwerfen einer relationalen Datenbank.

Das Erstellen eines Schemas beginnt mit dem Zuweisen einer Klasse. Klassen definieren die Verhaltensaspekte der Daten, die das Schema enthalten soll (Datensatz oder Zeitreihen). Um Ihre eigenen Schemas zu erstellen, führen Sie die Schritte im Tutorial zum Erstellen eines Schemas mit dem Schema-Editor ](../../xdm/tutorials/create-schema-ui.md) aus. [ Bevor Sie einen Datensatz für [!DNL Profile] aktivieren können, müssen Sie das Schema des Datensatzes so konfigurieren, dass es ein primäres Identitätsfeld enthält, und dann das Schema für [!DNL Profile] aktivieren. Wenn Daten in einen [!DNL Profile]-aktivierten Datensatz aufgenommen werden, werden dieselben Daten auch als [!DNL Profile]-Datensätze erfasst.

Wenn Sie lieber ein Schema mit der [!DNL Schema Registry]-API erstellen möchten, lesen Sie zunächst das [[!DNL Schema Registry] Entwicklerhandbuch](../../xdm/api/getting-started.md), bevor Sie im Rahmen des Tutorials versuchen, [ein Schema mithilfe der API zu erstellen](../../xdm/tutorials/create-schema-api.md).

Sobald Ihr Schema und Ihr Datensatz vorbereitet sind, können Sie Scoring-Daten generieren und in den Datensatz aufnehmen, indem Sie Scoring-Läufe mit einem geeigneten Modell durchführen.

## Erstellen von Zielgruppen mit dem [!DNL Segment Builder] {#create-audiences-using-the-segment-builder}

Nachdem Sie Ihre Auswertungsdateneinblicke generiert und in Ihren [!DNL Profile]-aktivierten Datensatz aufgenommen haben, können Sie dynamische Zielgruppen mit dem [!DNL Segment Builder] erstellen.

Der [!DNL Segment Builder] bietet einen umfassenden Arbeitsbereich, in dem Sie mit [!DNL Profile] -Datenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag &amp; Drop-Kacheln, die zur Darstellung von Dateneigenschaften verwendet werden. Folgen Sie dem [[!DNL Segment Builder] Benutzerhandbuch](../../segmentation/ui/segment-builder.md) , um mehr über Folgendes zu erfahren:

- Erstellen von Segmentdefinitionen mithilfe einer Kombination aus Attributen, Ereignissen und vorhandenen Zielgruppen als Bausteinen.
- Verwenden der Arbeitsfläche und Container des Regel-Builders, um die Reihenfolge zu steuern, in der Zielgruppenregeln ausgeführt werden.
- Anzeigen von Schätzungen Ihrer potenziellen Zielgruppe, sodass Sie Ihre Segmentdefinitionen nach Bedarf anpassen können.
- Aktivieren aller Segmentdefinitionen für die geplante Segmentierung.
- Aktivierung bestimmter Segmentdefinitionen für Streaming-Segmentierung.

## Nächste Schritte {#next-steps}

Weitere Informationen zu Zielgruppen und dem [!DNL Segment Builder] finden Sie in der Übersicht über den [Segmentation Service](../../segmentation/home.md) .

Weitere Informationen zu [!DNL Real-Time Customer Profile] finden Sie in der [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md) .
