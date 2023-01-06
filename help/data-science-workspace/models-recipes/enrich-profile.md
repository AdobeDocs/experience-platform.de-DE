---
keywords: Experience Platform; Modell für maschinelles Lernen; Data Science Workspace; Echtzeit-Kundenprofil; beliebte Themen; Einblicke in maschinelles Lernen
solution: Experience Platform
title: Anreicherung des Echtzeit-Kundenprofils mit Einblicken aus maschinellem Lernen
type: Tutorial
description: Dieses Dokument bietet eine Anleitung zur Anreicherung des Echtzeit-Kundenprofils mit Einblicken aus maschinellem Lernen.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 18%

---

# Anreichern [!DNL Real-Time Customer Profile] mit Einblicken aus maschinellem Lernen

Adobe Experience Platform [!DNL Data Science Workspace] bietet die Tools und Ressourcen zum Erstellen, Auswerten und Verwenden maschineller Lernmodelle, um Datenprognosen und -einblicke zu generieren. Wenn Einblicke aus maschinellem Lernen in eine [!DNL Profile]-aktivierter Datensatz, der dieselben Daten auch als [!DNL Profile] Datensätze, die dann mithilfe von [!DNL Adobe Experience Platform Segmentation Service].

Dieses Dokument enthält Links zu Tutorials, die Ihnen die Anreicherung ermöglichen [!DNL Real-Time Customer Profile] mit Ihren Einblicken aus maschinellem Lernen.

## Erste Schritte

Um die unten stehenden Tutorials abschließen zu können, benötigen Sie ein grundlegendes Verständnis der Erfassung [!DNL Profile] Daten und der Erstellung von Segmenten. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Services:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): Bietet eine vollständige, einheitliche Darstellung der einzelnen Kunden auf der Grundlage aggregierter Daten aus verschiedenen Quellen.
- [[!DNL Identity Service]](../../identity-service/home.md): Aktiviert [!DNL Real-Time Customer Profile] durch Überbrückung von Identitäten aus unterschiedlichen Datenquellen, die in Platform erfasst werden.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten ordnet.

Neben den oben genannten Dokumenten sollten Sie auch folgende Leitfäden zu Schemas und dem Schema-Editor lesen:

- [Grundlagen der Schemakomposition](../../xdm/schema/composition.md): Beschreibt XDM-Schemas, Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in verwendet werden sollen [!DNL Experience Platform].
- [Anleitung für den Schema-Editor](../../xdm/tutorials/create-schema-ui.md): Enthält ausführliche Anweisungen zum Erstellen von Schemas mit dem Schema-Editor in [!DNL Experience Platform].

## Ausgabeschema und -datensatz erstellen und konfigurieren {#create-an-output-schema-and-dataset}

Der erste Schritt zur Anreicherung [!DNL Real-Time Customer Profile] mit Scoring-Einblicken weiß, welches reale Objekt (wie eine Person) Ihre Daten definieren. Wenn Sie Ihre Daten verstehen, können Sie eine Struktur beschreiben und entwerfen, um Bedeutung hinzuzufügen, ähnlich wie beim Entwerfen einer relationalen Datenbank.

Das Erstellen eines Schemas beginnt mit dem Zuweisen einer Klasse. Klassen definieren die Verhaltensaspekte der Daten, die das Schema enthalten soll (Datensatz oder Zeitreihen). Um eigene Schemata zu erstellen, führen Sie die Schritte im Tutorial zu [Erstellen eines Schemas mit dem Schema Editor](../../xdm/tutorials/create-schema-ui.md). Beachten Sie, dass Sie, bevor Sie einen Datensatz für [!DNL Profile], müssen Sie das Schema des Datensatzes so konfigurieren, dass es ein primäres Identitätsfeld enthält, und dann das Schema für [!DNL Profile]. Wenn Daten in eine [!DNL Profile]-aktivierter Datensatz, der dieselben Daten auch als [!DNL Profile] Datensätze.

Wenn Sie lieber ein Schema mit der [!DNL Schema Registry] API stattdessen verwenden, indem Sie die [[!DNL Schema Registry] Entwicklerhandbuch](../../xdm/api/getting-started.md) vor dem Versuch des Tutorials auf [Erstellen eines Schemas mithilfe der API](../../xdm/tutorials/create-schema-api.md).

Sobald Ihr Schema und Ihr Datensatz vorbereitet sind, können Sie Scoring-Daten generieren und in den Datensatz aufnehmen, indem Sie Scoring-Läufe mit einem geeigneten Modell durchführen.

## Erstellen Sie Segmente mithilfe der [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Nachdem Sie Ihre Scoring-Dateneinblicke generiert und in Ihre [!DNL Profile]-aktivierter Datensatz, können Sie dynamische Segmente mithilfe der [!DNL Segment Builder].

Die [!DNL Segment Builder] bietet einen umfassenden Arbeitsbereich, in dem Sie mit [!DNL Profile] Datenelemente. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag-and-Drop-Kacheln, die zur Darstellung von Dateneigenschaften dienen. Befolgen Sie die [[!DNL Segment Builder] Benutzerhandbuch](../../segmentation/ui/segment-builder.md) Weitere Informationen:

- Erstellen von Segmentdefinitionen mithilfe einer Kombination aus Attributen, Ereignissen und vorhandenen Zielgruppen als Bausteinen.
- Verwenden der Arbeitsfläche und Container des Regel-Builders, um die Reihenfolge zu steuern, in der Segmentregeln ausgeführt werden.
- Anzeigen von Schätzungen Ihrer potenziellen Zielgruppe, sodass Sie Ihre Segmentdefinitionen nach Bedarf anpassen können.
- Aktivieren aller Segmentdefinitionen für die geplante Segmentierung.
- Aktivierung bestimmter Segmentdefinitionen für Streaming-Segmentierung.

## Nächste Schritte {#next-steps}

Weitere Informationen zu Segmenten und dem [!DNL Segment Builder], lesen Sie die [Übersicht über den Segmentierungsdienst](../../segmentation/home.md).

Weitere Informationen finden Sie unter [!DNL Real-Time Customer Profile], lesen Sie die [Übersicht über das Echtzeit-Kundenprofil](../../profile/home.md)
