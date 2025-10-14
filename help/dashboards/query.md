---
solution: Experience Platform
title: Dashboard-Datensätze mithilfe von Query Service durchsuchen, überprüfen und verarbeiten
type: Documentation
description: Erfahren Sie, wie Sie mit Query Service Rohdatensätze untersuchen und verarbeiten können, die Profil-, Audience- und Ziel-Dashboards im Experience Platform unterstützen.
exl-id: 0087dcab-d5fe-4a24-85f6-587e9ae74fb8
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 37%

---

# Dashboard-Datensätze mithilfe von [!DNL Query Service] durchsuchen, überprüfen und verarbeiten

Adobe Experience Platform stellt über Dashboards, die in der Experience Platform-Benutzeroberfläche verfügbar sind, wichtige Informationen zu den Profil-, Zielgruppen- und Zieldaten Ihres Unternehmens bereit. Anschließend können Sie Adobe Experience Platform [!DNL Query Service] verwenden, um die Rohdatensätze zu untersuchen, zu überprüfen und zu verarbeiten, über die diese Dashboards im Data Lake bereitgestellt werden.

## Erste Schritte mit [!DNL Query Service]

Adobe Experience Platform [!DNL Query Service] unterstützt Marketing-Fachleute dabei, Einblicke aus ihren Daten zu gewinnen, indem es die Verwendung von Standard-SQL zur Abfrage von Daten im Data Lake ermöglicht. [!DNL Query Service] bietet eine Benutzeroberfläche und eine API, die verwendet werden können, um einen beliebigen Datensatz im Data Lake zu verbinden und die Abfrageergebnisse als neue Datensätze zu erfassen, die für die Berichterstellung, das maschinelle Lernen oder die Aufnahme in das Echtzeit-Kundenprofil verwendet werden können.

Um mehr über [!DNL Query Service] und seine Rolle in Experience Platform zu erfahren, lesen Sie zunächst den [[!DNL Query Service] Überblick](../query-service/home.md).

## Zugreifen auf verfügbare Datensätze

Sie können [!DNL Query Service] verwenden, um Rohdatensätze nach Profil-, Zielgruppen- und Ziel-Dashboards abzufragen. Um Ihre verfügbaren Datensätze anzuzeigen, wählen Sie in der Experience Platform-Benutzeroberfläche **Datensätze** im linken Navigationsbereich aus, um das Dashboard „Datensätze“ zu öffnen. Das Dashboard listet alle verfügbaren Datensätze für Ihre Organisation auf. Details werden für jeden aufgelisteten Datensatz angezeigt, einschließlich seines Namens, des Schemas, dem der Datensatz entspricht, und des Status des letzten Aufnahmedurchgangs.

![Das Dashboard zum Durchsuchen von Datensätzen mit hervorgehobener Registerkarte „Datensätze“ in der linken Navigation.](./images/query/browse-datasets.png)

### Systemgenerierte Datensätze {#system-generated-datasets}

>[!IMPORTANT]
>
>Systemgenerierte Datensätze sind standardmäßig ausgeblendet. Standardmäßig zeigt die Registerkarte [!UICONTROL Durchsuchen] nur Datensätze an, in die Sie Daten aufgenommen haben.

Um systemgenerierte Datensätze anzuzeigen, klicken Sie auf das Filtersymbol (![Filtersymbol](/help/images/icons/filter.png)) links von der Suchleiste.

![Die Registerkarte zum Durchsuchen von Datensätzen mit hervorgehobenem Filtersymbol.](./images/query/filter-datasets.png)

Eine Seitenleiste wird angezeigt, die zwei Umschalter [!UICONTROL In Profil enthalten] und [!UICONTROL Systemdatensätze anzeigen] enthält. Wählen Sie den Umschalter für [!UICONTROL Systemdatensätze anzeigen] aus, um systemgenerierte Datensätze in die durchsuchbare Liste der Datensätze aufzunehmen.

![Die Registerkarte zum Durchsuchen von Datensätzen mit dem hervorgehobenen Umschalter „Systemdatensätze anzeigen“.](./images/query/show-system-datasets.png)

### Profilattributdatensätze {#profile-attribute-datasets}

Profil-Dashboard-Einblicke sind mit Zusammenführungsrichtlinien verknüpft, die von Ihrer Organisation definiert wurden. Für jede aktive Zusammenführungsrichtlinie steht im Data Lake ein Datensatz mit Profilattributen zur Verfügung.

Die Namenskonvention für diese Datensätze lautet **Profil-Schnappschuss-Export**, gefolgt von einem systemgenerierten zufälligen alphanumerischen Wert. Beispiel: `Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f`.

Um das vollständige Schema jedes Profilschnappschuss-Exportdatensatzes zu verstehen, können Sie eine Vorschau anzeigen und die Datensätze [unter Verwendung des Datensatz-Viewers](../catalog/datasets/user-guide.md) in der Experience Platform-Benutzeroberfläche erkunden.

![Eine Vorschau des Profilschnappschuss-Export-Datensatzes.](images/query/profile-attribute.png)

#### Zuordnen von Profilattribut-Datensätzen zu Zusammenführungsrichtlinien-IDs

Der jedem systemgenerierten Profilattribut-Datensatz zugewiesene alphanumerische Wert ist eine zufällige Zeichenfolge, die einer Zusammenführungsrichtlinien-ID einer der von Ihrer Organisation erstellten Zusammenführungsrichtlinien zugeordnet ist. Die Zuordnung jeder Zusammenführungsrichtlinien-ID zu der zugehörigen Datensatz-Zeichenfolge des Profilattributs wird im Datensatz `adwh_dim_merge_policies` beibehalten.

Der Datensatz `adwh_dim_merge_policies` enthält die folgenden Felder:

* `merge_policy_name`
* `merge_policy_id`
* `merge_policy`
* `dataset_id`

Dieser Datensatz kann mithilfe der Benutzeroberfläche des Abfrage-Editors in Experience Platform untersucht werden. Weitere Informationen zur Verwendung des Abfrage-Editors finden Sie im [Handbuch zur Benutzeroberfläche des Abfrage-Editors](../query-service/ui/user-guide.md).

### Zielgruppen-Metadaten-Datensatz

Im Data Lake ist ein Zielgruppen-Metadaten-Datensatz verfügbar, der Metadaten für die einzelnen Zielgruppen Ihres Unternehmens enthält.

Die Namenskonvention für diesen Datensatz lautet **Segmentdefinition-Schnappschuss-Export**, gefolgt von einem alphanumerischen Wert. Beispiel: `Segmentdefinition-Snapshot-Export-acf28952-2b6c-47ed-8f7f-016ac3c6b4e7`

Um das vollständige Schema jedes Segmentdefinitions-Schnappschuss-Exportdatensatzes zu verstehen, können Sie eine Vorschau anzeigen und die Datensätze [unter Verwendung des Datensatz-Viewers](../catalog/datasets/user-guide.md) in der Experience Platform-Benutzeroberfläche erkunden.

### Ziel-Metadaten-Datensatz

Die Metadaten für alle aktivierten Ziele Ihres Unternehmens sind als Rohdatensatz im Data Lake verfügbar.

Die Namenskonvention dieses Datensatzes lautet **DIM_Destination**.

Um das vollständige Schema des DIM-Zieldatensatzes zu verstehen, können Sie eine Vorschau anzeigen und den Datensatz [unter Verwendung des Datensatz-Viewers](../catalog/datasets/user-guide.md) in der Experience Platform-Benutzeroberfläche erkunden.

![Eine Vorschau des DIM_Destination-Datensatzes.](images/query/destinations-metadata.png)

## Insights-Berichte in Customer Data Platform (CDP)

Die Funktion CDP-Insights-Datenmodelle stellt den SQL-Code zur Verfügung, der die Insights für verschiedene Profil-, Ziel- und Segmentierungs-Widgets steuert. Sie können diese SQL-Abfragevorlagen anpassen, um CDP-Berichte für Ihre Marketing- und KPI-Anwendungsfälle zu erstellen.

Die CDP-Berichterstellung bietet Einblicke in Ihre Profildaten und deren Beziehung zu Audiences und Zielen. Siehe die Dokumentation zum CDP-Insights-Datenmodell für detaillierte Informationen zur [&#x200B; (Anwendung der CDP-Insights-Datenmodelle auf Ihre speziellen KPI-Anwendungsfälle](./data-models/cdp-insights-data-model-b2c.md).

## Beispielabfragen

Die folgenden Beispielabfragen enthalten Beispiel-SQL, das in [!DNL Query Service] verwendet werden kann, um die Rohdatensätze zu untersuchen, zu überprüfen und zu verarbeiten, die Ihre Dashboards unterstützen.

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

### Anzahl der Profile nach Zielgruppe

Dieser Zielgruppeneinblick liefert die Gesamtzahl der zusammengeführten Profile innerhalb jeder Zielgruppe im Datensatz. Diese Zahl ist das Ergebnis der Anwendung der Zielgruppen-Zusammenführungsrichtlinie auf Ihre Profildaten, um Profilfragmente zu einem einzigen Profil für jede Person in der Zielgruppe zusammenzuführen.

```sql
Select          
        concat_ws('-', key, source_namespace) audience_id,
        count(1) count_of_profiles
      from
        (
            Select
              Upper(key) as source_namespace,
              explode(value)
            from
              (
                  Select
                    explode(Audiencemembership)
                  from
                    Profile-Snapshot-Export-abbc7093-80f4-4b49-b96e-e743397d763f
              )
        )
      group by
      audience_id
```

## Nächste Schritte

Durch Lesen dieses Handbuchs können Sie jetzt [!DNL Query Service] verwenden, um mehrere Abfragen durchzuführen, um die Rohdatensätze zu untersuchen und zu verarbeiten, die Ihre Profil-, Zielgruppen- und Ziel-Dashboards unterstützen.

Um mehr über diese Dashboards und die darin verfügbaren Metriken zu erfahren, treffen Sie bitte eine entsprechende Auswahl aus der Liste der verfügbaren Dashboards in der Dokumentationsnavigation.
