---
solution: Experience Platform
title: Rohdaten mit Experience Platform-Dashboards durchsuchen und verarbeiten
type: Documentation
description: Erfahren Sie, wie Sie mit Query Service Rohdatensätze untersuchen und verarbeiten können, die Profil-, Segment- und Ziel-Dashboards in Experience Platform unterstützen.
source-git-commit: 1facf7079213918c2ef966b704319827eaa4a53d
workflow-type: ht
source-wordcount: '614'
ht-degree: 100%

---


# Dashboard-Datensätze mithilfe von Query Service durchsuchen, überprüfen und verarbeiten

Adobe Experience Platform bietet wichtige Informationen zu den Profil-, Segment- und Zieldaten Ihres Unternehmens über Dashboards, die in der Experience Platform-Benutzeroberfläche verfügbar sind. Anschließend können Sie den Adobe Experience Platform-Abfragedienst verwenden, um die Rohdatensätze zu untersuchen, zu überprüfen und zu verarbeiten, über die diese Dashboards im Data Lake bereitgestellt werden.

## Erste Schritte mit Query Service

Adobe Experience Platform Query Service unterstützt Marketingexperten dabei, Einblicke aus ihren Daten zu gewinnen, indem es die Verwendung von Standard-SQL zur Abfrage von Daten im Data Lake ermöglicht. Query Service bietet eine Benutzeroberfläche und eine API, die verwendet werden können, um einen beliebigen Datensatz im Data Lake zu verbinden und die Abfrageergebnisse als neue Datensätze zu erfassen, die für die Berichterstellung, das maschinelle Lernen oder die Aufnahme in das Echtzeit-Kundenprofil verwendet werden können.

Um mehr über Query Service und seine Rolle in Experience Platform zu erfahren, lesen Sie zunächst den Abschnitt [Query Service - Übersicht](../query-service/home.md).

## Verfügbare Datensätze

Sie können Query Service verwenden, um Raw-Datensätze für Profil-, Segment- und Ziel-Dashboards abzufragen. In den folgenden Abschnitten werden die Rohdatensätze beschrieben, die Sie im Data Lake finden können.

### Profilattributdatensätze

Für jede aktive Zusammenführungsrichtlinie im Echtzeit-Kundenprofil steht im Data Lake ein Datensatz mit Profilattributen zur Verfügung.

Die Namenskonvention für diese Datensätze lautet **Profilattribut**, gefolgt von einem alphanumerischen Wert. Beispiel: `Profile Attribute 14adf268-2a20-4dee-bee6-a6b0e34616a9`

Um das vollständige Schema jedes Datensatzes zu verstehen, können Sie die Datensätze mit dem Datensatz-Viewer in der Experience Platform-Benutzeroberfläche in der Vorschau anzeigen und untersuchen.

### Datensatz für Segmentmetadaten

Im Data Lake ist ein Segment-Metadaten-Datensatz verfügbar, der Metadaten für die einzelnen Segmente Ihres Unternehmens enthält.

Die Namenskonvention für diesen Datensatz lautet **Profilsegmentdefinition**, gefolgt von einem alphanumerischen Wert. Beispiel: `Profile Segment Definition 6591ba8f-1422-499d-822a-543b2f7613a3`

Um das vollständige Schema des Datensatzes zu verstehen, können Sie das Schema mit dem Datensatz-Viewer in der Experience Platform-Benutzeroberfläche in der Vorschau anzeigen und untersuchen.

![](images/query/segment-metadata.png)

### Ziel-Metadaten-Datensatz

Die Metadaten für alle aktivierten Ziele Ihres Unternehmens sind als Rohdatensatz im Data Lake verfügbar.

Die Namenskonvention dieses Datensatzes lautet **DIM_Destination**.

Um das vollständige Schema des Datensatzes zu verstehen, können Sie das Schema mit dem Datensatz-Viewer in der Experience Platform-Benutzeroberfläche in der Vorschau anzeigen und untersuchen.

![](images/query/destinations-metadata.png)

## Beispielabfragen

Die folgenden Beispielabfragen enthalten Beispiel-SQL, das in Query Service verwendet werden kann, um die Rohdatensätze zu untersuchen, zu überprüfen und zu verarbeiten, die Ihre Dashboards unterstützen.

### Anzahl der Profile nach Identität

Dieser Profileinblick bietet eine Aufschlüsselung der Identitäten über alle zusammengeführten Profile im Datensatz hinweg. Die Gesamtzahl der Profile nach Identität (d. h. das Addieren der für jeden Namespace angezeigten Werte) kann höher sein als die Gesamtzahl der zusammengeführten Profile, da einem Profil mehrere Namespaces zugeordnet sein können. Wenn beispielsweise ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Namespaces zugeordnet.

**Abfrage**

```sql
Select
        Key namespace,
        count(1) count_of_profiles
     from
        (
           Select
               explode(identitymap)
           from
              profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
        )
     group by
        namespace;
```

### Anzahl der Profile nach Segment

Dieser Zielgruppeneinblick liefert die Gesamtanzahl der zusammengeführten Profile innerhalb jedes Segments im Datensatz. Diese Zahl ist das Ergebnis der Anwendung der Segmentzusammenführungsrichtlinie auf Ihre Profildaten, um Profilfragmente zu einem einzigen Profil für jede Person im Segment zusammenzuführen.

```sql
Select          
        concat_ws('-', key, source_namespace) segment_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Segmentmembership)
                  from
                    profile_attribute_14adf268-2a20-4dee-bee6-a6b0e34616a9
              )
        )
      group by
      segment_id
```

## Nächste Schritte

Durch Lesen dieses Handbuchs können Sie jetzt Query Service verwenden, um mehrere Abfragen durchzuführen, um die Rohdatensätze zu untersuchen und zu verarbeiten, die Ihre Profil-, Segment- und Ziel-Dashboards unterstützen.

Um mehr über diese Dashboards und die darin verfügbaren Metriken zu erfahren, treffen Sie bitte eine entsprechende Auswahl aus der Liste der verfügbaren Dashboards in der Dokumentationsnavigation.
