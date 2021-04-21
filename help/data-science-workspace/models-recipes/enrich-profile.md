---
keywords: Experience Platform;Modell für maschinelles Lernen;Arbeitsbereich für Datenwissenschaften;Echtzeit-Profil für Kunden;beliebte Themen;Einblicke in maschinelles Lernen
solution: Experience Platform
title: Verbessern Sie Ihr Echtzeit-Profil durch maschinelles Lernen - Insights
topic-legacy: tutorial
type: Tutorial
description: Dieses Dokument bietet einen Leitfaden, wie Sie Echtzeit-Kundeneinblicke durch maschinelles Lernen bereichern können.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 24%

---

# Bereichern Sie [!DNL Real-time Customer Profile] durch Einblicke in maschinelles Lernen.

Adobe Experience Platform [!DNL Data Science Workspace] bietet die Werkzeuge und Ressourcen zum Erstellen, Auswerten und Verwenden von maschinellen Lernmodellen, um Datenprognosen und -einblicke zu generieren. Wenn Einblicke in das maschinelle Lernen in einen [!DNL Profile]-aktivierten Datensatz aufgenommen werden, werden dieselben Daten auch als [!DNL Profile]-Datensätze erfasst, die dann mit [!DNL Adobe Experience Platform Segmentation Service] segmentiert werden können. Bevor aufgenommene Profil- und Zeitreihendaten mit bestehenden Daten zusammengeführt werden und die Vereinigungsansicht aktualisiert wird, bestimmt das Echtzeit-Kundenprofil anhand der sogenannten Streaming-Segmentierung durchgehend automatisch, ob die neuen Daten in den Segmenten eingeschlossen oder von ihnen ausgeschlossen werden. Das Ergebnis: Berechnungen und Entscheidungen dazu, wie Sie Ihren Kunden herausragende, individuell auf sie abgestimmte Erlebnisse liefern, lassen sich direkt während ihrer Interaktion mit Ihrer Marke anstellen bzw. treffen.

Dieses Dokument enthält Links zu Tutorials, mit denen Sie [!DNL Real-time Customer Profile] mit Ihren Erkenntnissen aus dem maschinellen Lernen bereichern können.

## Erste Schritte

Um die unten stehenden Lernprogramme abzuschließen, benötigen Sie ein funktionierendes Verständnis der Erfassung von [!DNL Profile]-Daten und der Erstellung von Segmenten. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Bietet eine vollständige, einheitliche Darstellung der einzelnen Kunden auf der Grundlage aggregierter Daten aus mehreren Quellen.
- [[!DNL Identity Service]](../../identity-service/home.md): Ermöglicht  [!DNL Real-time Customer Profile] die Überbrückung von Identitäten aus unterschiedlichen Datenquellen, die in Plattform erfasst werden.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): Das standardisierte Framework, mit dem Plattform Kundenerlebnisdaten organisiert.

Neben den oben genannten Dokumenten sollten Sie auch folgende Leitfäden zu Schemas und dem Schema-Editor lesen:

- [Grundlagen der Zusammensetzung](../../xdm/schema/composition.md) des Schemas: Beschreibt XDM-Schema, Bausteine, Grundsätze und Best Practices zum Erstellen von Schemas, die in  [!DNL Experience Platform]verwendet werden sollen.
- [Anleitung für den Schema-Editor](../../xdm/tutorials/create-schema-ui.md): Enthält ausführliche Anweisungen zum Erstellen von Schemas mit dem Schema-Editor in [!DNL Experience Platform].

## Output-Schema und -Datensatz {#create-an-output-schema-and-dataset} erstellen und konfigurieren

Der erste Schritt zur Bereicherung von [!DNL Real-time Customer Profile] mit bewertenden Einblicken ist das Wissen, welches real-world Objekt (wie eine Person) Ihre Daten definieren. Wenn Sie sich mit Ihren Daten auskennen, können Sie eine Struktur beschreiben und entwerfen, die Bedeutung hinzufügt, ähnlich wie beim Entwerfen einer relationalen Datenbank.

Das Erstellen eines Schemas beginnt mit dem Zuweisen einer Klasse. Klassen definieren die Verhaltensaspekte der Daten, die das Schema enthalten soll (Datensatz oder Zeitreihen). Gehen Sie wie im Lernprogramm [Erstellen eines Schemas mit dem Schema-Editor](../../xdm/tutorials/create-schema-ui.md) beschrieben vor, um Beginn zu erstellen, die eigene Schemas erstellen. Beachten Sie, dass Sie, bevor Sie einen Datensatz für [!DNL Profile] aktivieren können, das Schema des Datensatzes so konfigurieren müssen, dass es ein primäres Identitätsfeld enthält, und dann das Schema für [!DNL Profile] aktivieren müssen. Wenn Daten in einen [!DNL Profile]-aktivierten Datensatz aufgenommen werden, werden dieselben Daten auch als [!DNL Profile]-Datensätze erfasst.

Wenn Sie stattdessen lieber ein Schema mit der API zusammenstellen möchten, lesen Sie den Beginn [[!DNL Schema Registry] Entwicklerhandbuch](../../xdm/api/getting-started.md), bevor Sie das Lernprogramm [zum Erstellen eines Schemas mit der API](../../xdm/tutorials/create-schema-api.md) durchführen.[!DNL Schema Registry]

Nachdem Ihr Schema und Ihr Datensatz vorbereitet wurden, können Sie Bewertungsdaten für den Datensatz generieren und erfassen, indem Sie mit einem entsprechenden Modell Bewertungsausläufe durchführen.

## Erstellen Sie Segmente mit [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Nachdem Sie die Einblicke in die Bewertungsdaten in Ihren [!DNL Profile]-aktivierten Datensatz generiert und eingezogen haben, können Sie dynamische Segmente mit dem [!DNL Segment Builder] erstellen.

Das [!DNL Segment Builder] bietet eine Rich-Workspace-Funktion, mit der Sie mit [!DNL Profile]-Datenelementen interagieren können. Der Arbeitsbereich bietet intuitive Steuerelemente zum Erstellen und Bearbeiten von Regeln, z. B. Drag-and-Drop-Kacheln, die zur Darstellung von Dateneigenschaften dienen. Folgen Sie dem [[!DNL Segment Builder] Benutzerhandbuch](../../segmentation/ui/segment-builder.md), um mehr über Folgendes zu erfahren:

- Segmentdefinitionen mit einer Kombination aus Attributen, Ereignissen und vorhandenen Audiencen als Bausteine erstellen
- Verwenden der Regelaufbau-Arbeitsfläche und der Container zur Steuerung der Reihenfolge, in der Segmentregeln ausgeführt werden.
- Ansicht von Schätzungen Ihrer voraussichtlichen Audience, sodass Sie Ihre Segmentdefinitionen nach Bedarf anpassen können.
- Aktivieren aller Segmentdefinitionen für die geplante Segmentierung.
- Aktivieren spezifizierter Segmentdefinitionen für Streaming-Segmentierung.

## Nächste Schritte {#next-steps}

Weitere Informationen zu Segmenten und dem [!DNL Segment Builder] finden Sie im Abschnitt [Übersicht über den Segmentdienst](../../segmentation/home.md).

Weitere Informationen zu [!DNL Real-time Customer Profile] finden Sie im Abschnitt zum [Kundenüberblick in Echtzeit](../../profile/home.md).
