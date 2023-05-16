---
description: Erfahren Sie, wie Sie die Dateiexporteinstellungen für Ziele konfigurieren, die mit Destination SDK erstellt wurden.
title: Batch-Konfiguration
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 18%

---


# Batch-Konfiguration {#batch-configuration}

Verwenden Sie die Batch-Konfigurationsoptionen in Destination SDK, um Benutzern die Möglichkeit zu geben, die exportierten Dateinamen anzupassen und den Exportzeitplan entsprechend ihrer Voreinstellung zu konfigurieren.

Wenn Sie dateibasierte Ziele über Destination SDK erstellen, können Sie Standarddateinamen konfigurieren und Zeitpläne exportieren. Alternativ können Sie Benutzern über die Platform-Benutzeroberfläche die Option zum Konfigurieren dieser Einstellungen geben. Sie können beispielsweise Verhaltensweisen wie die folgenden konfigurieren:

* Einschließen spezifischer Informationen in den Dateinamen, z. B. Segment-IDs, Ziel-IDs oder benutzerdefinierte Informationen.
* Benutzer können die Dateibenennung über die Platform-Benutzeroberfläche anpassen.
* Konfigurieren Sie Dateiexporte für bestimmte Zeitintervalle.
* Definieren Sie, welche Anpassungsoptionen für die Dateibenennung und den Export von Zeitplänen für Benutzer in der Platform-Benutzeroberfläche angezeigt werden.

Batch-Konfigurationseinstellungen sind Teil der Zielkonfiguration für dateibasierte Ziele.

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm im [Konfigurationsoptionen](../configuration-options.md) Dokumentation oder lesen Sie das Handbuch zu [Destination SDK zum Konfigurieren eines dateibasierten Ziels verwenden](../../guides/configure-file-based-destination-instructions.md#create-server-file-configuration).

Sie können die Dateibenennungs- und Exportzeitplaneinstellungen über die `/authoring/destinations` -Endpunkt. Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Zielkonfiguration aktualisieren](../../authoring-api/destination-configuration/update-destination-configuration.md)

In diesem Artikel werden alle unterstützten Batch-Konfigurationsoptionen beschrieben, die Sie für Ihr Ziel verwenden können, und es wird gezeigt, was Kunden in der Platform-Benutzeroberfläche sehen werden.

>[!IMPORTANT]
>
>Alle von Destination SDK unterstützten Parameternamen und Werte sind **Groß-/Kleinschreibung**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Nein |
| Dateibasierte (Batch-)Integrationen | Ja |

## Unterstützte Parameter {#supported-parameters}

Die Werte, die Sie hier einrichten, werden im [Segmentexport planen](../../../ui/activate-batch-profile-destinations.md#scheduling) Schritt des dateibasierten Zielaktivierungs-Workflows.

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
   }
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `allowMandatoryFieldSelection` | Boolesch | Wenn auf `true` eingestellt, können Kunden festlegen, welche Profilattribute obligatorisch sind. Der Standardwert ist `false`. Weitere Informationen finden Sie unter [Obligatorische Attribute](../../../ui/activate-batch-profile-destinations.md#mandatory-attributes). |
| `allowDedupeKeyFieldSelection` | Boolesch | Mit der Einstellung auf `true` können Kunden Deduplizierungsschlüssel angeben. Der Standardwert ist `false`. Weitere Informationen finden Sie unter [Deduplizierungsschlüssel](../../../ui/activate-batch-profile-destinations.md#deduplication-keys). |
| `defaultExportMode` | Enum | Definiert den standardmäßigen Dateiexportmodus. Unterstützte Werte:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> Der Standardwert ist `DAILY_FULL_EXPORT`. Weitere Informationen zur Planung von Dateiexporten finden Sie in der [Dokumentation zur Batch-Aktivierung](../../../ui/activate-batch-profile-destinations.md#scheduling). |
| `allowedExportModes` | Liste | Definiert die für Kunden verfügbaren Dateiexportmodi. Unterstützte Werte:<ul><li>`DAILY_FULL_EXPORT`</li><li>`FIRST_FULL_THEN_INCREMENTAL`</li></ul> |
| `allowedScheduleFrequency` | Liste | Definiert die für Kunden verfügbare Dateiexportfrequenz. Unterstützte Werte:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> |
| `defaultFrequency` | Enum | Definiert die standardmäßige Dateiexportfrequenz. Unterstützte Werte:<ul><li>`ONCE`</li><li>`EVERY_3_HOURS`</li><li>`EVERY_6_HOURS`</li><li>`EVERY_8_HOURS`</li><li>`EVERY_12_HOURS`</li><li>`DAILY`</li></ul> Der Standardwert ist `DAILY`. |
| `defaultStartTime` | Zeichenfolge | Definiert die standardmäßige Startzeit für den Dateiexport. Verwendet das 24-Stunden-Dateiformat. Der Standardwert ist „00:00“. |
| `filenameConfig.allowedFilenameAppendOptions` | Zeichenfolge | *Erforderlich*. Liste der verfügbaren Dateinamenmakros, aus denen Benutzer auswählen können. Dadurch wird bestimmt, welche Elemente an exportierte Dateinamen angehängt werden (Segment-ID, Organisationsname, Datum und Uhrzeit des Exports usw.). Wenn `defaultFilename`sollten Sie darauf achten, dass Makros nicht dupliziert werden. <br><br>Unterstützte Werte: <ul><li>`DESTINATION`</li><li>`SEGMENT_ID`</li><li>`SEGMENT_NAME`</li><li>`DESTINATION_INSTANCE_ID`</li><li>`DESTINATION_INSTANCE_NAME`</li><li>`ORGANIZATION_NAME`</li><li>`SANDBOX_NAME`</li><li>`DATETIME`</li><li>`CUSTOM_TEXT`</li></ul>Unabhängig von der Reihenfolge, in der Sie die Makros definieren, zeigt die Experience Platform-Benutzeroberfläche sie immer in der hier dargestellten Reihenfolge an. <br><br> Wenn `defaultFilename` leer ist, ist die `allowedFilenameAppendOptions` -Liste muss mindestens ein Makro enthalten. |
| `filenameConfig.defaultFilenameAppendOptions` | Zeichenfolge | *Erforderlich*. Vorausgewählte Standardmakros für Dateinamen, die von Benutzern deaktiviert werden können.<br><br> Die Makros in dieser Liste sind eine Teilmenge der in `allowedFilenameAppendOptions`. |
| `filenameConfig.defaultFilename` | Zeichenfolge | *Optional*. Definiert die standardmäßigen Dateinamenmakros für die exportierten Dateien. Diese können von Benutzern nicht überschrieben werden. <br><br>Jedes von `allowedFilenameAppendOptions` wird angehängt, nachdem die `defaultFilename` Makros. <br><br>Wenn `defaultFilename` leer ist, müssen Sie mindestens ein Makro in `allowedFilenameAppendOptions`. |

{style="table-layout:auto"}

## Dateinamenkonfiguration {#file-name-configuration}

Verwenden Sie Dateinamenkonfigurationsmakros, um zu definieren, welche Namen der exportierten Datei enthalten sollen. Die Makros in der folgenden Tabelle beschreiben Elemente in der Benutzeroberfläche in der [Dateinamenkonfiguration](../../../ui/activate-batch-profile-destinations.md#file-names) angezeigt.

>[!TIP]
> 
>Als Best Practice sollten Sie immer die `SEGMENT_ID` Makro in den Namen der exportierten Dateien. Segment-IDs sind eindeutig. Daher lässt sich am besten sicherstellen, dass Dateinamen auch eindeutig sind, wenn Sie sie in den Dateinamen aufnehmen.

| Makro | UI-Bezeichnung | Beschreibung | Beispiel |
|---|---|---|---|
| `DESTINATION` | [!UICONTROL Ziel] | Zielname in der Benutzeroberfläche. | Amazon S3 |
| `SEGMENT_ID` | [!UICONTROL Segment-ID] | Eindeutige, Platform-generierte Segment-ID | ce5c5482-2813-4a80-99bc-57113f6acde2 |
| `SEGMENT_NAME` | [!UICONTROL Segmentname] | Benutzerdefinierter Segmentname | VIP |
| `DESTINATION_INSTANCE_ID` | [!UICONTROL Ziel-ID] | Eindeutige, Platform-generierte ID der Zielinstanz | 7b891e5f-025a-4f0d-9e73-1919e71da3b0 |
| `DESTINATION_INSTANCE_NAME` | [!UICONTROL Zielname] | Benutzerdefinierter Name der Zielinstanz. | Mein Werbeziel 2022 |
| `ORGANIZATION_NAME` | [!UICONTROL Organisationsname] | Name der Kundenorganisation in Adobe Experience Platform. | Mein Organisationsname |
| `SANDBOX_NAME` | [!UICONTROL Sandbox-Name] | Name der vom Kunden verwendeten Sandbox. | prod |
| `DATETIME` / `TIMESTAMP` | [!UICONTROL Datum und Uhrzeit] | `DATETIME` und `TIMESTAMP` beide definieren den Zeitpunkt der Erstellung der Datei, jedoch in verschiedenen Formaten. <br><br><ul><li>`DATETIME` verwendet das folgende Format: JJJJMMTT_HMMSS.</li><li>`TIMESTAMP` verwendet das 10-stellige Unix-Format. </li></ul> `DATETIME` und `TIMESTAMP` sich gegenseitig ausschließen und nicht gleichzeitig verwendet werden können. | <ul><li>`DATETIME`: 20220509_210543</li><li>`TIMESTAMP`: 1652131584</li></ul> |
| `CUSTOM_TEXT` | [!UICONTROL Benutzerdefinierter Text] | Benutzerdefinierter benutzerdefinierter Text, der in den Dateinamen eingefügt werden soll. Kann nicht in verwendet werden `defaultFilename`. | My_custom_text |
| `TIMESTAMP` | [!UICONTROL Datum und Uhrzeit] | 10-stelliger Zeitstempel der Zeit, zu der die Datei generiert wurde, im Unix-Format. | 1652131584 |

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

![Benutzeroberflächenbild mit dem Konfigurationsbildschirm für Dateinamen mit vorab ausgewählten Makros](../../assets/functionality/destination-configuration/file-name-configuration.png)

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie besser verstehen, wie Sie die Dateibenennung und Exportzeitpläne für Ihre dateibasierten Ziele konfigurieren können.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Konfiguration der Kundenauthentifizierung](customer-authentication.md)
* [OAuth 2-Authentifizierung](oauth2-authentication.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Benutzeroberflächenattribute](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Identitäts-Namespace-Konfiguration](identity-namespace-configuration.md)
* [Unterstützte Zuordnungskonfigurationen](supported-mapping-configurations.md)
* [Zielbereitstellung](destination-delivery.md)
* [Konfiguration von Zielgruppen-Metadaten](audience-metadata-configuration.md)
* [Aggregationsrichtlinie](aggregation-policy.md)
* [Historische Profilqualifikationen](historical-profile-qualifications.md)