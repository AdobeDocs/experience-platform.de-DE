---
solution: Experience Platform
title: Rohdaten mit Platform-Dashboards durchsuchen und verarbeiten
type: Documentation
description: Erfahren Sie, wie Sie mit Query Service Rohdatensätze untersuchen und verarbeiten können, die Profil-, Segment- und Ziel-Dashboards in Experience Platform unterstützen.
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: b9dd7584acc43b5946f8c0669d7a81001e44e702
workflow-type: tm+mt
source-wordcount: '738'
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

Profil-Dashboard-Einblicke sind mit Zusammenführungsrichtlinien verknüpft, die von Ihrer Organisation definiert wurden. Für jede aktive Zusammenführungsrichtlinie steht im Data Lake ein Datensatz mit Profilattributen zur Verfügung.

Die Namenskonvention für diese Datensätze lautet **Profil-Schnappschuss-Export**, gefolgt von einem systemgenerierten zufälligen alphanumerischen Wert. Beispiel: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Um das vollständige Schema jedes Profilschnappschuss-Exportdatensatzes zu verstehen, können Sie eine Vorschau anzeigen und die Datensätze [unter Verwendung des Datensatz-Viewers](../catalog/datasets/user-guide.md) in der Experience Platform-Benutzeroberfläche erkunden.

![](images/query/profile-attribute.png)

#### Zuordnen von Profilattribut-Datensätzen zu Zusammenführungsrichtlinien-IDs

Jeder Profilattribut-Datensatz erhält die Bezeichnung **Profil-Schnappschuss-Export**, gefolgt von einem systemgenerierten zufälligen alphanumerischen Wert. Beispiel: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Dieser alphanumerische Wert ist eine systemgenerierte zufällige Zeichenfolge, die einer Zusammenführungsrichtlinien-ID einer der von Ihrer Organisation erstellten Zusammenführungsrichtlinien zugeordnet ist. Die Zuordnung jeder Zusammenführungsrichtlinien-ID zu der zugehörigen Datensatz-Zeichenfolge des Profilattributs wird im Datensatz `adwh_dim_merge_policies` beibehalten.

Der Datensatz `adwh_dim_merge_policies` enthält die folgenden Felder:

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

Dieser Datensatz kann mithilfe der Benutzeroberfläche des Abfrage-Editors in Experience Platform untersucht werden. Weitere Informationen zur Verwendung des Abfrage-Editors finden Sie im [Handbuch zur Benutzeroberfläche des Abfrage-Editors](../query-service/ui/user-guide.md).

### Datensatz für Segmentmetadaten

Im Data Lake ist ein Segment-Metadaten-Datensatz verfügbar, der Metadaten für die einzelnen Segmente Ihres Unternehmens enthält.

Die Namenskonvention für diesen Datensatz lautet **Segmentdefinition-Schnappschuss-Export**, gefolgt von einem alphanumerischen Wert. Beispiel: `Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

Um das vollständige Schema jedes Segmentdefinitions-Schnappschuss-Exportdatensatzes zu verstehen, können Sie eine Vorschau anzeigen und die Datensätze [unter Verwendung des Datensatz-Viewers](../catalog/datasets/user-guide.md) in der Experience Platform-Benutzeroberfläche erkunden.

![](images/query/segment-metadata.png)

### Ziel-Metadaten-Datensatz

Die Metadaten für alle aktivierten Ziele Ihres Unternehmens sind als Rohdatensatz im Data Lake verfügbar.

Die Namenskonvention dieses Datensatzes lautet **DIM_Destination**.

Um das vollständige Schema des DIM-Zieldatensatzes zu verstehen, können Sie eine Vorschau anzeigen und den Datensatz [unter Verwendung des Datensatz-Viewers](../catalog/datasets/user-guide.md) in der Experience Platform-Benutzeroberfläche erkunden.

![](images/query/destinations-metadata.png)

## Beispielabfragen

Die folgenden Beispielabfragen enthalten Beispiel-SQL, das in Query Service verwendet werden kann, um die Rohdatensätze zu untersuchen, zu überprüfen und zu verarbeiten, die Ihre Dashboards unterstützen.

### Anzahl der Profile nach Identität

Dieser Profileinblick bietet eine Aufschlüsselung der Identitäten über alle zusammengeführten Profile im Datensatz hinweg.

>[!NOTE]
>
>Die Gesamtzahl der Profile nach Identität (d. h. das Addieren der für jeden Namespace angezeigten Werte) kann höher sein als die Gesamtzahl der zusammengeführten Profile, da einem Profil mehrere Namespaces zugeordnet sein können. Wenn beispielsweise ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Namespaces zugeordnet.

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
              Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
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
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      segment_id
```

## Nächste Schritte

Durch Lesen dieses Handbuchs können Sie jetzt Query Service verwenden, um mehrere Abfragen durchzuführen, um die Rohdatensätze zu untersuchen und zu verarbeiten, die Ihre Profil-, Segment- und Ziel-Dashboards unterstützen.

Um mehr über diese Dashboards und die darin verfügbaren Metriken zu erfahren, treffen Sie bitte eine entsprechende Auswahl aus der Liste der verfügbaren Dashboards in der Dokumentationsnavigation.
