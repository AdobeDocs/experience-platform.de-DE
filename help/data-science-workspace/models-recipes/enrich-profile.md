---
keywords: Experience Platform; Modell für maschinelles Lernen; Data Science Workspace; Echtzeit-Kundenprofil; beliebte Themen; Einblicke in maschinelles Lernen
solution: Experience Platform
title: Echtzeit-Kundenprofil mit Einblicken aus maschinellem Lernen anreichern
topic-legacy: tutorial
type: Tutorial
description: Dieses Dokument bietet eine Anleitung zur Anreicherung von Echtzeit-Kundenprofil mit Einblicken aus maschinellem Lernen.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 24%

---

# Anreicherung von [!DNL Real-time Customer Profile] mit Einblicken aus maschinellem Lernen

Adobe Experience Platform [!DNL Data Science Workspace] bietet die Tools und Ressourcen zum Erstellen, Auswerten und Verwenden maschineller Lernmodelle, um Datenprognosen und Einblicke zu generieren. Wenn Einblicke aus maschinellem Lernen in einen [!DNL Profile]-aktivierten Datensatz aufgenommen werden, werden dieselben Daten auch als [!DNL Profile] Datensätze erfasst, die dann mit [!DNL Adobe Experience Platform Segmentation Service] segmentiert werden können. Bevor aufgenommene Profil- und Zeitreihendaten mit bestehenden Daten zusammengeführt werden und die Vereinigungsansicht aktualisiert wird, bestimmt das Echtzeit-Kundenprofil anhand der sogenannten Streaming-Segmentierung durchgehend automatisch, ob die neuen Daten in den Segmenten eingeschlossen oder von ihnen ausgeschlossen werden. Das Ergebnis: Berechnungen und Entscheidungen dazu, wie Sie Ihren Kunden herausragende, individuell auf sie abgestimmte Erlebnisse liefern, lassen sich direkt während ihrer Interaktion mit Ihrer Marke anstellen bzw. treffen.

Dieses Dokument enthält Links zu Tutorials, mit denen Sie [!DNL Real-time Customer Profile] mit Ihren Einblicken aus maschinellem Lernen anreichern können.

## Erste Schritte

Um die unten stehenden Tutorials abzuschließen, benötigen Sie ein Verständnis für die Aufnahme von [!DNL Profile]-Daten und die Erstellung von Segmenten. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet eine vollständige, einheitliche Darstellung der einzelnen Kunden auf der Grundlage aggregierter Daten aus verschiedenen Quellen.
- [[!DNL Identity Service]](../../identity-service/home.md): Ermöglicht  [!DNL Real-time Customer Profile] die Überbrückung von Identitäten aus unterschiedlichen Datenquellen, die in Platform erfasst werden.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.

Neben den oben genannten Dokumenten sollten Sie auch folgende Leitfäden zu Schemas und dem Schema-Editor lesen:

- [Grundlagen der Schemakomposition](../../xdm/schema/composition.md): Beschreibt XDM-Schemas, Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in verwendet werden  [!DNL Experience Platform]sollen.
- [Anleitung für den Schema-Editor](../../xdm/tutorials/create-schema-ui.md): Enthält ausführliche Anweisungen zum Erstellen von Schemas mit dem Schema-Editor in [!DNL Experience Platform].

## Ausgabeschema und -datensatz erstellen und konfigurieren {#create-an-output-schema-and-dataset}

Der erste Schritt zur Anreicherung von [!DNL Real-time Customer Profile] mit Scoring-Einblicken besteht darin zu wissen, welches reale Objekt (z. B. eine Person) Ihre Daten definieren. Wenn Sie Ihre Daten verstehen, können Sie eine Struktur beschreiben und entwerfen, um Bedeutung hinzuzufügen, ähnlich wie beim Entwerfen einer relationalen Datenbank.

Das Erstellen eines Schemas beginnt mit dem Zuweisen einer Klasse. Klassen definieren die Verhaltensaspekte der Daten, die das Schema enthalten soll (Datensatz oder Zeitreihen). Um Ihre eigenen Schemas zu erstellen, führen Sie die Schritte im Tutorial zum Erstellen eines Schemas mit dem Schema-Editor](../../xdm/tutorials/create-schema-ui.md) aus. [ Beachten Sie, dass Sie, bevor Sie einen Datensatz für [!DNL Profile] aktivieren können, das Schema des Datensatzes so konfigurieren müssen, dass es ein primäres Identitätsfeld enthält, und das Schema für [!DNL Profile] aktivieren müssen. Wenn Daten in einen [!DNL Profile]-aktivierten Datensatz aufgenommen werden, werden dieselben Daten auch als [!DNL Profile]-Datensätze erfasst.

Wenn Sie stattdessen ein Schema mit der [!DNL Schema Registry]-API erstellen möchten, lesen Sie zunächst das [[!DNL Schema Registry] Entwicklerhandbuch](../../xdm/api/getting-started.md) , bevor Sie das Tutorial zum Erstellen eines Schemas mit der API](../../xdm/tutorials/create-schema-api.md) durchführen.[

Sobald Ihr Schema und Ihr Datensatz vorbereitet sind, können Sie Scoring-Daten generieren und in den Datensatz aufnehmen, indem Sie Scoring-Läufe mit einem geeigneten Modell durchführen.

## Erstellen von Segmenten mit [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Nachdem Sie Ihre Auswertungsdateneinblicke generiert und in Ihren [!DNL Profile]-aktivierten Datensatz aufgenommen haben, können Sie mit [!DNL Segment Builder] dynamische Segmente erstellen.

Der [!DNL Segment Builder] bietet einen Rich-Workspace, mit dem Sie mit [!DNL Profile] Datenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag-and-Drop-Kacheln, die zur Darstellung von Dateneigenschaften dienen. Folgen Sie dem [[!DNL Segment Builder] Benutzerhandbuch](../../segmentation/ui/segment-builder.md), um mehr über Folgendes zu erfahren:

- Erstellen von Segmentdefinitionen mithilfe einer Kombination aus Attributen, Ereignissen und vorhandenen Zielgruppen als Bausteinen.
- Verwenden der Arbeitsfläche und Container des Regel-Builders, um die Reihenfolge zu steuern, in der Segmentregeln ausgeführt werden.
- Anzeigen von Schätzungen Ihrer potenziellen Zielgruppe, sodass Sie Ihre Segmentdefinitionen nach Bedarf anpassen können.
- Aktivieren aller Segmentdefinitionen für die geplante Segmentierung.
- Aktivierung bestimmter Segmentdefinitionen für Streaming-Segmentierung.

## Nächste Schritte {#next-steps}

Weitere Informationen zu Segmenten und dem [!DNL Segment Builder] finden Sie unter [Übersicht über den Segmentation Service](../../segmentation/home.md).

Weitere Informationen zu [!DNL Real-time Customer Profile] finden Sie unter [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md) .
