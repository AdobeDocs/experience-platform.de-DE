---
title: Anwendungsfälle für die Segmentierung der Echtzeit-Kundendatenplattform B2B Edition
description: Ein Überblick über die verschiedenen Anwendungsfälle der Echtzeit-CDP B2B Edition.
exl-id: 2a99b85e-71b3-4781-baf7-a4d5436339d3
source-git-commit: 9bd7434f2b224d76decac1e04d8491a6b3149a3a
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 1%

---

# Anwendungsfälle für die Segmentierung für Real-time Customer Data Platform B2B Edition

Dieses Dokument enthält Beispiele für Segmentdefinitionen in der Echtzeit-Kundendatenplattform B2B Edition und wie verschiedene Attributtypen für gängige B2B-Anwendungsfälle kombiniert werden können. Informationen dazu, wie Ziele in Ihren B2B-Workflow integriert werden können, finden Sie im Abschnitt [End-to-End-Tutorial](../b2b-tutorial.md#create-a-segment-to-evaluate-your-data).

>[!NOTE]
>
>Die für diese Anwendungsfälle der Segmentierung erforderlichen Attribute stehen nur Kunden von Real-time Customer Data Platform B2B Edition zur Verfügung. Wenn Sie Real-time Customer Data Platform B2B Edition nicht verwenden, lesen Sie den Abschnitt [Segmentierungsübersicht](./segmentation-overview.md) anstatt.

## Voraussetzungen

Bevor Sie die Segmentierungsattribute für B2B-Klassen verwenden können, müssen Sie die folgenden Schritte ausführen:

1. Erstellen Sie Schemas, die die B2B-Klassen verwenden. Die B2B Edition-Klassen umfassen Konto, Kampagne, Chancen, Marketingliste und mehr. Informationen über [Einrichten von Schemata zur Verwendung mit B2B-Klassen](../schemas/b2b.md) finden Sie in der Schemadokumentation.
1. Erstellen Sie Beziehungen zwischen Ihren Experience-Datenmodell (XDM) B2B-Schemas. Segmente, die auf B2B Edition-Attributen basieren, erfordern Beziehungen zwischen den Klassen, um die erweiterte Funktion zur B2B-Segmentierung vollständig zu nutzen. Weitere Informationen finden Sie in der Dokumentation unter [wie eine Beziehung zwischen zwei B2B-Schemas definiert wird](../../xdm/tutorials/relationship-b2b.md) für weitere Informationen.
1. Erfassen Sie Daten mithilfe von Datensätzen basierend auf Ihren B2B-Schemas. Weitere Informationen finden Sie in der Quelldokumentation für [Informationen zur Datenerfassung](../../sources/connectors/adobe-applications/marketo/marketo.md).
1. Lesen Sie die [Segment Builder-Benutzerhandbuch](../../segmentation/ui/segment-builder.md) für eine detailliertere Anleitung zum Erstellen von Segmenten.

Sobald diese Anforderungen erfüllt sind, können Sie diese Attribute für gängige B2B-Anwendungsfälle kombinieren.

## Erste Schritte

Sobald die Vereinigungsschemas für die B2B-Klassen Beziehungen hergestellt haben und zum Erfassen von Daten verwendet wurden, werden ihre Attribute in der linken Leiste des Segment Builder verfügbar gemacht.

B2B-Klassen und ihre Attribute werden mit einem `B2B` im Arbeitsbereich &quot;Segmentierung&quot;, um sie von den in Real-time Customer Data Platform standardmäßig verfügbaren zu unterscheiden.

Um Segmente für B2B-Anwendungsfälle effektiv erstellen zu können, ist es wichtig, über eine genaue Kenntnis des Schemas zu verfügen und zu verstehen, wie das Datenmodell aussieht. Beachten Sie auch den Pfad, den die Daten von einem Datenobjekt zum anderen führen.

Die folgende Abbildung zeigt die Beziehungen zwischen den B2B-Klassen, die in der Echtzeit-Kundendatenplattform B2B Edition verfügbar sind.

![B2B-Klasse ERD](../assets/segmentation/b2b-classes.png)

Da Ihr Datenmodell kompliziert sein kann, können Sie über die Platform-Benutzeroberfläche eine detailliertere visuelle Darstellung Ihres Datenmodells anzeigen, um die relevanten Attribute für Ihren Anwendungsfall zu finden. Beginnen Sie mit der Platform-Benutzeroberfläche und wählen Sie im linken Navigationsbereich Schemas aus.

Wählen Sie das entsprechende Schema aus der verfügbaren Liste aus und wählen Sie die entsprechende Beziehung aus der [!UICONTROL Komposition] Seitenleiste. Im folgenden Beispiel zeigt die Auswahl der Beziehung &quot;Person&quot;an, welches Attribut im aktuellen Schema auf das zugehörige Schema &quot;Person&quot;verweist (wenn es das Quellschema in der Beziehung ist) oder durch das Schema &quot;Person&quot;referenziert wird (wenn es das Zielschema in der Beziehung ist).

![Quellschlüsselbeispiel mithilfe der Personenbeziehung im Arbeitsbereich &quot;Schema&quot;](../assets/segmentation/source-key-schema-relationship-example.png)

Diese Beziehung wird im Segment Builder durch die Verwendung von `Key` Ordner wie in der Abbildung unten dargestellt.

![Quellschlüsselbeispiel zur Verwendung des Segment-Builders im Segmentierungsarbeitsbereich](../assets/segmentation/source-key-segmentation-example.png)

Weitere Informationen finden Sie unter [Schemata in der Dokumentation zu Real-time Customer Data Platform B2B Edition](../schemas/b2b.md) für weitere Informationen zu den verfügbaren B2B-Klassen.

Die folgenden Anwendungsfälle liefern Informationen darüber, welche Klassen verwendet werden, um Beziehungen zwischen den verschiedenen Schemas herzustellen, um diese Ergebnisse zu erzielen. Diese Beispiele helfen Ihnen beim Erstellen eigener Segmente.

## Beispiele für unterschiedliche Anwendungsfälle

Die folgenden Anwendungsfälle stehen für die Segmentierung mit der B2B Edition zur Verfügung. Jedes Beispiel enthält eine Beschreibung der Funktion des Segments und eine Beschreibung der Klassen, die zum Erstellen verwendet wurden. Die bereitgestellten Bilder markieren den Dateipfad im [!UICONTROL Attribute] Seitenleiste, die die Struktur des Schemas widerspiegelt. Die [!UICONTROL Segmenteigenschaften] rechts neben der Anzeige eine schriftliche Aufschlüsselung der Attribute des Segments.

### Beispiel 1

Finden Sie alle Menschen, die der &quot;Entscheidungsträger&quot;jeder Gelegenheit sind. Dieses Segment erfordert eine Verknüpfung zwischen dem [!UICONTROL XDM Individual Profile] und [!UICONTROL XDM Business Opportunity-Personenbeziehung] -Klasse.

![Benutzeroberfläche mit Beispiel 1-Einstellungen](../assets/segmentation/example-1.png)

### Beispiel 2

Finden Sie alle Personen, die direkt mit allen Möglichkeiten verbunden sind, deren Opportunitätsbetrag größer ist als der angegebene Betrag ($1 Million). Dieses Segment erfordert eine Verknüpfung zwischen dem [!UICONTROL XDM Individual Profile] Klasse, [!UICONTROL XDM Business Opportunity-Personenbeziehung] -Klasse und [!UICONTROL XDM-Geschäftschancen] -Klasse.

![Benutzeroberfläche mit Beispiel 2-Einstellungen](../assets/segmentation/example-2.png)

### Beispiel 3

Finden Sie alle Personen, die allen Möglichkeiten direkt zugewiesen sind, in denen sich das Konto an einem bestimmten Ort (Kanada) befindet. Dieses Segment erfordert eine Verknüpfung zwischen dem [!UICONTROL XDM Individual Profile] Klasse, [!UICONTROL XDM Business Opportunity-Personenbeziehung] Klasse, [!UICONTROL XDM-Geschäftschancen] -Klasse und [!UICONTROL XDM-Geschäftskonto] -Klasse.

![Benutzeroberfläche mit Beispiel 3-Einstellungen](../assets/segmentation/example-3.png)

### Beispiel 4

Finden Sie alle Personen, die ein &quot;Entscheidungsträger&quot;sind, von jeder Gelegenheit, wo sich das Konto in der &quot;Finance&quot;-Branche befindet, und besuchten Sie die Preisseite in den letzten drei Tagen. Dieses Segment erfordert eine Verknüpfung zwischen dem [!UICONTROL XDM Individual Profile] Klasse, [!UICONTROL XDM Business Opportunity-Personenbeziehung] Klasse, [!UICONTROL XDM-Geschäftschancen] -Klasse und [!UICONTROL XDM-Geschäftskonto] -Klasse und [!UICONTROL XDM ExperienceEvent] -Klasse.

![Benutzeroberfläche mit Beispiel 4-Einstellungen](../assets/segmentation/example-4.png)

### Beispiel 5

Finden Sie alle Personen, die in einer Personalabteilung (HR) arbeiten und mit jedem Konto verbunden sind, das mindestens eine offene Chance im Wert des angegebenen Betrags (1 Million Dollar) oder mehr hat. Dieses Segment erfordert eine Verknüpfung zwischen dem [!UICONTROL XDM Individual Profile] Klasse, [!UICONTROL XDM-Geschäftskonto] -Klasse und [!UICONTROL XDM-Geschäftschancen] -Klasse.

![Benutzeroberfläche mit Beispiel-5-Einstellungen](../assets/segmentation/example-5.png)

### Beispiel 6

Finden Sie alle Personen, deren Berufsbezeichnung Vizepräsident ist und die mit einem beliebigen Konto verbunden sind, dessen Jahresumsatz den angegebenen Betrag (100 Millionen Dollar) oder mehr beträgt, und haben die Preisseite im letzten Monat mindestens dreimal besucht. Dieses Segment erfordert eine Verknüpfung zwischen dem [!UICONTROL XDM Individual Profile] Klasse, [!UICONTROL XDM-Geschäftskonto] -Klasse und [!UICONTROL XDM ExperienceEvent] -Klasse.

![Benutzeroberfläche mit Beispiel 6-Einstellungen](../assets/segmentation/example-6.png)

### Beispiel 7

Finden Sie alle Personen, die ein &quot;Entscheidungsträger&quot;jeder verlorenen Gelegenheit sind und die Preisseite in der letzten Woche besucht haben. Dieses Segment erfordert eine Verknüpfung zwischen dem [!UICONTROL XDM Individual Profile] Klasse, [!UICONTROL XDM Business Opportunity-Personenbeziehung] Klasse, [!UICONTROL XDM-Geschäftschancen] -Klasse und [!UICONTROL XDM ExperienceEvent] -Klasse.

![Benutzeroberfläche mit Beispiel 7-Einstellungen](../assets/segmentation/example-7.png)

## Nächste Schritte

Nach dem Lesen dieser Übersicht haben Sie jetzt ein Verständnis der Segmentierungsmöglichkeiten, die mit der Echtzeit-Kundendatenplattform (B2B Edition) verfügbar sind. Weitere Informationen zum Segmentierungsdienst finden Sie in der [Dokumentation zur Segmentierung](../../segmentation/home.md).
