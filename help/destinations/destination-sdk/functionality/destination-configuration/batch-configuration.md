---
description: Erfahren Sie, wie Sie die Dateiexporteinstellungen für Ziele konfigurieren, die mit Destination SDK erstellt wurden.
title: Batch-Konfiguration
source-git-commit: 3f31a54c0cf329d374808dacce3fac597a72aa11
workflow-type: tm+mt
source-wordcount: '1073'
ht-degree: 81%

---


# Batch-Konfiguration {#batch-configuration}

Verwenden Sie die Batch-Konfigurationsoptionen in Destination SDK, um Benutzerinnen und Benutzern die Möglichkeit zu geben, die exportierten Dateinamen anzupassen und den Exportzeitplan nach ihren Wünschen zu konfigurieren.

Wenn Sie dateibasierte Ziele über Destination SDK erstellen, können Sie Standarddateinamen konfigurieren und Zeitpläne exportieren. Alternativ können Sie Benutzerinnen und Benutzern über die Platform-Benutzeroberfläche die Option zum Konfigurieren dieser Einstellungen geben. Sie können beispielsweise Verhaltensweisen wie die folgenden konfigurieren:

* Einschließen spezifischer Informationen in den Dateinamen, wie Zielgruppen-IDs, Ziel-IDs oder benutzerdefinierte Informationen.
* Benutzerinnen und Benutzer können die Dateibenennung über die Platform-Benutzeroberfläche anpassen.
* Konfigurieren von Dateiexporten für bestimmte Zeitintervalle.
* Definieren, welche Anpassungsoptionen für die Dateibenennung und den Export von Zeitplänen für Benutzerinnen und Benutzer in der Platform-Benutzeroberfläche angezeigt werden.

Batch-Konfigurationseinstellungen sind Teil der Zielkonfiguration für dateibasierte Ziele.

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm in der Dokumentation zu [Konfigurationsoptionen](../configuration-options.md) oder im Handbuch zur [Verwendung von Destination SDK zum Konfigurieren eines dateibasierten Ziels](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Sie können die Dateibenennungs- und Exportzeitplaneinstellungen über den Endpunkt `/authoring/destinations` konfigurieren. Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aktualisieren einer Zielkonfiguration](../../authoring-api/destination-configuration/update-destination-configuration.md)

In diesem Artikel werden alle unterstützten Batch-Konfigurationsoptionen beschrieben, die Sie für Ihr Ziel verwenden können, und es wird gezeigt, was Kundinnen und Kunden in der Platform-Benutzeroberfläche sehen werden.

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Nein |
| Dateibasierte (Batch-)Integrationen | Ja |

## Unterstützte Parameter {#supported-parameters}

Die Werte, die Sie hier einrichten, werden im [Zielgruppenexport planen](../../../ui/activate-batch-profile-destinations.md#scheduling) Schritt des dateibasierten Zielaktivierungs-Workflows.

```json
"batchConfig":{
   "allowMandatoryFieldSelection":true,
   "allowDedupeKeyFieldSelection":true,
   "defaultExportMode":"DAILY_FULL_EXPORT",
   "allowedExportMode":[
      "DAILY_FULL_EXPORT",
      "FIRST_FULL_THEN_INCREMENTAL"
   ],
   "allowedScheduleFrequency":[
      "DAILY",
      "EVERY_3_HOURS",
      "EVERY_6_HOURS",
      "EVERY_8_HOURS",
      "EVERY_12_HOURS",
      "ONCE"
   ],
   "defaultFrequency":"DAILY",
   "defaultStartTime":"00:00",
   "filenameConfig":{
         "allowedFilenameAppendOptions":[
            "SEGMENT_NAME",
            "DESTINATION_INSTANCE_ID",
            "DESTINATION_INSTANCE_NAME",
            "ORGANIZATION_NAME",
            "SANDBOX_NAME",
            "DATETIME",
            "CUSTOM_TEXT"
         ],
         "defaultFilenameAppendOptions":[
            "DATETIME"
         ],
         "defaultFilename":"%DESTINATION%_%SEGMENT_ID%"
      },
   "segmentGroupingEnabled": true
   }
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Boolesch | Wenn auf `true` eingestellt, können Kundinnen und Kunden festlegen, welche Profilattribute obligatorisch sind. Der Standardwert ist `false`. Weitere Informationen finden Sie unter [Obligatorische Attribute](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `allowDedupeKeyFieldSelection` | Boolesch | Wenn auf `true` eingestellt, können Kundinnen und Kunden Deduplizierungsschlüssel angeben. Der Standardwert ist `false`. Weitere Informationen finden Sie unter [Deduplizierungsschlüssel](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |
| `defaultExportMode` | Enum | Definiert den standardmäßigen Dateiexportmodus. Unterstützte Werte:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> Der Standardwert ist `DAILY_FULL_EXPORT`. Weitere Informationen zur Planung von Dateiexporten finden Sie in der [Dokumentation zur Batch-Aktivierung](../../../ui/activate-batch-profile-destinations.md#scheduling). |
| `allowedExportModes` | Liste | Definiert die für Kundinnen und Kunden verfügbaren Dateiexportmodi. Unterstützte Werte:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Liste | Definiert die für Kundinnen und Kunden verfügbare Dateiexportfrequenz. Unterstützte Werte:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enum | Definiert die standardmäßige Dateiexportfrequenz. Unterstützte Werte:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> Der Standardwert ist `DAILY`. |
| `defaultStartTime` | Zeichenfolge | Definiert die standardmäßige Startzeit für den Dateiexport. Verwendet das 24-Stunden-Dateiformat. Der Standardwert ist „00:00“. |
| `filenameConfig.allowedFilenameAppendOptions` | Zeichenfolge | *Erforderlich*. Liste der verfügbaren Dateinamenmakros, aus denen Benutzerinnen und Benutzer auswählen können. Dadurch wird bestimmt, welche Elemente an die exportierten Dateinamen angehängt werden (Zielgruppen-ID, Organisationsname, Datum und Uhrzeit des Exports usw.). Wenn Sie `defaultFilename`festlegen, sollten Sie darauf achten, dass Makros nicht dupliziert werden. <br><br>Unterstützte Werte: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Unabhängig von der Reihenfolge, in der Sie die Makros definieren, zeigt die Experience Platform-Benutzeroberfläche sie immer in der hier dargestellten Reihenfolge an. <br><br> Wenn `defaultFilename` leer ist, muss die Liste `allowedFilenameAppendOptions` mindestens ein Makro enthalten. |
| `filenameConfig.defaultFilenameAppendOptions` | Zeichenfolge | *Erforderlich*. Vorausgewählte Standardmakros für Dateinamen, die von Benutzerinnen und Benutzern deaktiviert werden können.<br><br> Die Makros in dieser Liste sind eine Teilmenge der in `allowedFilenameAppendOptions` definierten. |
| `filenameConfig.defaultFilename` | Zeichenfolge | *Optional*. Definiert die standardmäßigen Dateinamenmakros für die exportierten Dateien. Diese können von Benutzerinnen und Benutzern nicht überschrieben werden. <br><br>Jedes von `allowedFilenameAppendOptions` definierte Makro wird nach den `defaultFilename`-Makros angehängt. <br><br>Wenn `defaultFilename` leer ist, müssen Sie mindestens ein Makro in `allowedFilenameAppendOptions` definieren. |
| `segmentGroupingEnabled` | Boolesch | Definiert, ob die aktivierten Zielgruppen in einer oder mehreren Dateien je nach Zielgruppe exportiert werden sollen [Zusammenführungsrichtlinie](../../../../profile/merge-policies/overview.md). Unterstützte Werte: <ul><li>`true`: exportiert eine Datei pro Zusammenführungsrichtlinie.</li><li>`false`: exportiert eine Datei pro Zielgruppe, unabhängig von der Zusammenführungsrichtlinie. Dies ist das Standardverhalten. Sie können dasselbe Ergebnis erzielen, indem Sie diesen Parameter vollständig ausschließen.</li></ul> |

{style="table-layout:auto"}

## Dateinamenkonfiguration {#file-name-configuration}

Verwenden Sie Makros zur Dateinamenkonfiguration, um zu definieren, was die Namen der exportierten Dateien enthalten sollen. Die Makros in der folgenden Tabelle beschreiben Elemente, die in der Benutzeroberfläche des Bildschirms [Dateinamenkonfiguration](../../../ui/activate-batch-profile-destinations.md#file-names) angezeigt werden.

>[!TIP]
> 
>Als Best Practice sollten Sie immer das `SEGMENT_ID`-Makro in den Namen der exportierten Dateien aufnehmen. Segment-IDs sind eindeutig. Daher lässt sich am besten sicherstellen, dass Dateinamen auch eindeutig sind, indem Sie sie in den Dateinamen aufnehmen.

| Makro | UI-Bezeichnung | Beschreibung | Beispiel |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Ziel] | Zielname in der Benutzeroberfläche. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL Segment-ID] | Eindeutige, Platform-generierte Zielgruppen-ID | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Segmentname] | Benutzerdefinierter Zielgruppenname | VIP |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL Ziel-ID] | Eindeutige, von Platform generierte ID der Zielinstanz | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Zielname] | Benutzerdefinierter Name der Zielinstanz. | Mein Werbeziel 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Organisationsname] | Name der Kundenorganisation in Adobe Experience Platform. | Mein Organisationsname |
| `SANDBOX_NAME` | [!UICONTROL Sandbox-Name] | Name der von der Kundinnen oder dem Kunden verwendeten Sandbox. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Datum und Uhrzeit] | `DATETIME` und `TIMESTAMP` definieren beide den Zeitpunkt der Erstellung der Datei, jedoch in verschiedenen Formaten. <br><br><ul><li>`DATETIME` verwendet das folgende Format: JJJJMMTT_HHMMSS.</li><li>`TIMESTAMP` verwendet das 10-stellige Unix-Format. </li></ul> `DATETIME` und `TIMESTAMP` schließen sich gegenseitig aus und können nicht gleichzeitig verwendet werden. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Benutzerdefinierter Text] | Benutzerdefinierter Text, der in den Dateinamen eingefügt werden soll. Kann nicht in `defaultFilename` verwendet werden. | Mein_Benutzerdefinierter_Text |
| `TIMESTAMP` | [!UICONTROL Datum und Uhrzeit] | 10-stelliger Zeitstempel der Zeit, zu der die Datei generiert wurde, im Unix-Format. | 1652131584 |
| `MERGE_POLICY_ID` | [!UICONTROL Zusammenführungsrichtlinien-ID] | Die ID der [Zusammenführungsrichtlinie](../../../../profile/merge-policies/overview.md) wird zum Generieren der exportierten Audience verwendet. Verwenden Sie dieses Makro, wenn Sie exportierte Zielgruppen basierend auf einer Zusammenführungsrichtlinie in Dateien gruppieren. Verwenden Sie dieses Makro zusammen mit `segmentGroupingEnabled:true`. | e8591fdb-2873-4b12-b63e-15275b1c1439 |
| `MERGE_POLICY_NAME` | [!UICONTROL Name der Zusammenführungsrichtlinie] | Der Name der [Zusammenführungsrichtlinie](../../../../profile/merge-policies/overview.md) wird zum Generieren der exportierten Audience verwendet. Verwenden Sie dieses Makro, wenn Sie exportierte Zielgruppen basierend auf einer Zusammenführungsrichtlinie in Dateien gruppieren. Verwenden Sie dieses Makro zusammen mit `segmentGroupingEnabled:true`. | Meine benutzerspezifische Zusammenführungsrichtlinie |

{style="table-layout:auto"}

### Beispiel für eine Dateinamenkonfiguration

Das folgende Konfigurationsbeispiel zeigt die Korrespondenz zwischen der im API-Aufruf verwendeten Konfiguration und den in der Benutzeroberfläche angezeigten Optionen.

```json
"filenameConfig":{
   "allowedFilenameAppendOptions":[
      "CUSTOM_TEXT",
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilenameAppendOptions":[
      "SEGMENT_ID",
      "DATETIME"
   ],
   "defaultFilename": "%DESTINATION%"
}
```

![UI-Bild mit dem Konfigurationsbildschirm für Dateinamen mit vorab ausgewählten Makros](../../assets/functionality/destination-configuration/file-name-configuration.png)

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie besser verstehen, wie Sie die Dateibenennung und Exportzeitpläne für Ihre dateibasierten Ziele konfigurieren können.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Konfiguration der Kundenauthentifizierung](customer-authentication.md)
* [OAuth 2-Authentifizierung](oauth2-authentication.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Benutzeroberflächenattribute](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration von Identity-Namespaces](identity-namespace-configuration.md)
* [Unterstützte Zuordnungskonfigurationen](supported-mapping-configurations.md)
* [Zielbereitstellung](destination-delivery.md)
* [Konfiguration von Zielgruppen-Metadaten](audience-metadata-configuration.md)
* [Aggregationsrichtlinie](aggregation-policy.md)
* [Historische Profilqualifikationen](historical-profile-qualifications.md)