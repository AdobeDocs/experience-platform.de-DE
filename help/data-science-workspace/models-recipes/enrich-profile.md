---
keywords: Experience Platform;Modell für maschinelles Lernen;Data Science Workspace;Echtzeit-Kundenprofil;beliebte Themen;Einblicke aus maschinellem Lernen
solution: Experience Platform
title: Echtzeit-Kundenprofil mit Einblicken aus maschinellem Lernen anreichern
type: Tutorial
description: Dieses Dokument enthält eine Anleitung zum Anreichern des Echtzeit-Kundenprofils mit Einblicken aus maschinellem Lernen.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '655'
ht-degree: 15%

---

# [!DNL Real-Time Customer Profile] mit Einblicken aus maschinellem Lernen anreichern

>[!NOTE]
>
>Data Science Workspace ist nicht mehr erhältlich.
>
>Diese Dokumentation richtet sich an Bestandskunden mit vorherigen Berechtigungen für Data Science Workspace.

Adobe Experience Platform [!DNL Data Science Workspace] bietet die Tools und Ressourcen zum Erstellen, Auswerten und Verwenden von Modellen für maschinelles Lernen, um Datenvorhersagen und Erkenntnisse zu generieren. Wenn Einblicke aus maschinellem Lernen in einen [!DNL Profile]-aktivierten Datensatz aufgenommen werden, werden dieselben Daten auch als [!DNL Profile] aufgenommen, die dann mithilfe von [!DNL Adobe Experience Platform Segmentation Service] segmentiert werden können.

Der Segmentierungsprozess hängt von der Auswertungsmethode für die Zielgruppe ab. Wenn eine Zielgruppe als **Streaming** konfiguriert ist, verarbeitet sie alle neuen Aktualisierungen, die vom Modell in Echtzeit in das Profil geschrieben wurden. Wenn eine Zielgruppe jedoch für die **Batch**-Auswertung konfiguriert ist, werden die neuen Werte im nächsten Batch ausgewertet.

Dieses Dokument enthält Links zu Tutorials, mit denen Sie [!DNL Real-Time Customer Profile] mit Einblicken aus maschinellem Lernen anreichern können.

## Erste Schritte

Um die unten stehenden Tutorials abzuschließen, benötigen Sie ein grundlegendes Verständnis von der Aufnahme [!DNL Profile] Daten und der Erstellung von Audiences. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet eine vollständige, einheitliche Darstellung jedes einzelnen Kunden auf der Grundlage aggregierter Daten aus verschiedenen Quellen.
- [[!DNL Identity Service]](../../identity-service/home.md): Aktiviert die [!DNL Real-Time Customer Profile] durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, die in Experience Platform aufgenommen werden.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten ordnet.

Neben den oben genannten Dokumenten sollten Sie auch folgende Leitfäden zu Schemata und dem Schema-Editor lesen:

- [Grundlagen der Schemakomposition](../../xdm/schema/composition.md): Beschreibt XDM-Schemata, Bausteine, Prinzipien und Best Practices zum Erstellen von Schemata, die in [!DNL Experience Platform] verwendet werden können.
- [Tutorial zum Schema](../../xdm/tutorials/create-schema-ui.md)Editor: Enthält detaillierte Anweisungen zum Erstellen von Schemata mithilfe des Schema-Editors in [!DNL Experience Platform].

## Erstellen und Konfigurieren eines Ausgabeschemas und Datensatzes {#create-an-output-schema-and-dataset}

Der erste Schritt zur Anreicherung von [!DNL Real-Time Customer Profile] mit Scoring-Einblicken besteht darin zu wissen, welches reale Objekt (z. B. eine Person) Ihre Daten definieren. Wenn Sie Ihre Daten verstehen, können Sie eine Struktur beschreiben und entwerfen, um eine Bedeutung hinzuzufügen, ähnlich wie beim Entwerfen einer relationalen Datenbank.

Das Erstellen eines Schemas beginnt mit dem Zuweisen einer Klasse. Klassen definieren die Verhaltensaspekte der Daten, die das Schema enthalten soll (Datensatz oder Zeitreihen). Um Ihre eigenen Schemata zu erstellen, führen Sie die Schritte im Tutorial [Erstellen eines Schemas mithilfe des Schema-Editors“ &#x200B;](../../xdm/tutorials/create-schema-ui.md). Beachten Sie, dass Sie, bevor Sie einen Datensatz für die [!DNL Profile] aktivieren können, das Schema des Datensatzes so konfigurieren müssen, dass es ein primäres Identitätsfeld hat, und dann das Schema für die [!DNL Profile] aktivieren müssen. Wenn Daten in einen [!DNL Profile] Datensatz aufgenommen werden, werden dieselben Daten auch als [!DNL Profile] aufgenommen.

Wenn Sie lieber ein Schema mit der [!DNL Schema Registry]-API erstellen möchten, lesen Sie zunächst das [[!DNL Schema Registry] Entwicklerhandbuch](../../xdm/api/getting-started.md), bevor Sie im Rahmen des Tutorials versuchen, [ein Schema mithilfe der API zu erstellen](../../xdm/tutorials/create-schema-api.md).

Nach der Vorbereitung Ihres Schemas und Datensatzes können Sie Bewertungsdaten generieren und in den Datensatz aufnehmen, indem Sie Bewertungsdurchgänge mit einem entsprechenden Modell durchführen.

## Erstellen von Audiences mit dem [!DNL Segment Builder] {#create-audiences-using-the-segment-builder}

Nachdem Sie Ihre Bewertungsdaten-Insights in Ihrem [!DNL Profile]-aktivierten Datensatz generiert und aufgenommen haben, können Sie mit dem [!DNL Segment Builder] dynamische Zielgruppen erstellen.

Die [!DNL Segment Builder] bietet einen umfangreichen Arbeitsbereich, in dem Sie mit [!DNL Profile] Datenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag-and-Drop-Kacheln zur Darstellung von Dateneigenschaften. Folgen Sie [[!DNL Segment Builder] Benutzerhandbuch](../../segmentation/ui/segment-builder.md) um mehr über Folgendes zu erfahren:

- Erstellen von Segmentdefinitionen mithilfe einer Kombination von Attributen, Ereignissen und vorhandenen Zielgruppen als Bausteine.
- Verwenden der Arbeitsfläche und der Container des Regel-Builders zur Steuerung der Reihenfolge, in der Zielgruppenregeln ausgeführt werden.
- Anzeigen von Schätzungen Ihrer potenziellen Zielgruppe, sodass Sie Ihre Segmentdefinitionen nach Bedarf anpassen können.
- Aktivieren aller Segmentdefinitionen für die geplante Segmentierung.
- Aktivieren der angegebenen Segmentdefinitionen für die Streaming-Segmentierung.

## Nächste Schritte {#next-steps}

Weitere Informationen zu Zielgruppen und den [!DNL Segment Builder] finden Sie in der [Segmentierungs-Service - Übersicht](../../segmentation/home.md).

Weitere Informationen zu [!DNL Real-Time Customer Profile] finden Sie in der [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md)
