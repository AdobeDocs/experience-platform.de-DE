---
description: Erfahren Sie, wie Sie die Zielgruppen-Metadateneinstellungen für Ziele konfigurieren, die mit Destination SDK erstellt wurden.
title: Konfiguration von Zielgruppen-Metadaten
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: ht
source-wordcount: '406'
ht-degree: 100%

---


# Konfiguration von Zielgruppen-Metadaten

Beim Exportieren von Daten aus der Experience Platform in Ihr Ziel benötigen Sie möglicherweise bestimmte Zielgruppen-Metadaten, wie Segmentnamen oder Segment-IDs, die für die Experience Platform und Ihr Ziel freigegeben werden.

Destination SDK bietet Tools, mit denen Sie Zielgruppen in Ihrer Zielplattform programmgesteuert erstellen, aktualisieren oder löschen können.

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm in der Dokumentation zu [Konfigurationsoptionen](../configuration-options.md) oder im Handbuch zum [Verwenden von Destination SDK zum Konfigurieren eines Streaming-Ziels](../../guides/configure-destination-instructions.md#create-destination-configuration).

Sie können die Vorlage für Zielgruppen-Metadaten über den Endpunkt `/authoring/audience-templates` konfigurieren. Nachdem Sie die Konfiguration der Zielgruppen-Metadaten erstellt haben, können Sie den Endpunkt `/authoring/destinations` zum Konfigurieren des Abschnitts `audienceMetadataConfig` verwenden. Dieser Abschnitt teilt Ihrem Ziel mit, welche Segmentmetadaten Ihrer Zielgruppenvorlage zugeordnet werden sollen.

Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Aktualisieren einer Zielkonfiguration](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [Erstellen einer Zielgruppenvorlage](../../metadata-api/create-audience-template.md)
* [Aktualisieren einer Zielgruppenvorlage](../../metadata-api/update-audience-template.md)

>[!IMPORTANT]
>
>Bei allen von Destination SDK unterstützten Parameternamen und Werten wird **nach Groß-/Kleinschreibung unterschieden**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Ja |
| Dateibasierte (Batch-)Integrationen | Ja |

## Unterstützte Parameter {#supported-parameters}

Bei der Erstellung Ihrer Zielgruppen-Metadatenkonfiguration können Sie die in der folgenden Tabelle beschriebenen Parameter verwenden, um die Einstellungen für die Segmentzuordnung zu konfigurieren.

```json
  "audienceMetadataConfig":{
   "mapExperiencePlatformSegmentName":false,
   "mapExperiencePlatformSegmentId":false,
   "mapUserInput":false,
   "audienceTemplateId":"YOUR_AUDIENCE_TEMPLATE_ID"
}
```

| Parameter | Typ | Beschreibung |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | Boolesch | Gibt an, ob der Wert der [[!UICONTROL Zuordnungs-ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) im Zielaktivierungs-Workflow der Segmentname aus Experience Platform sein sollte. |
| `mapExperiencePlatformSegmentId` | Boolesch | Gibt an, ob der Wert der [[!UICONTROL Zuordnungs-ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) im Zielaktivierungs-Workflow die Segment-ID aus Experience Platform sein sollte. |
| `mapUserInput` | Boolesch | Aktiviert oder deaktiviert die Benutzereingabe für den Wert der [[!UICONTROL Zuordnungs-ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) im Zielaktivierungs-Workflow. Wenn er auf `true`, gesetzt ist, kann `audienceTemplateId` nicht vorhanden sein. |
| `audienceTemplateId` | Boolesch | Die `instanceId` der [Zielgruppen-Metadatenvorlage](../../metadata-api/create-audience-template.md), die für Ihr Ziel verwendet wird. |

{style="table-layout:auto"}

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie ein besseres Verständnis davon haben, wie Sie Zielgruppen-Metadaten für Ihr Ziel konfigurieren können.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Konfiguration der Kundenauthentifizierung](customer-authentication.md)
* [OAuth 2-Authentifizierung](oauth2-authentication.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Benutzeroberflächenattribute](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration von Identity-Namespaces](identity-namespace-configuration.md)
* [Unterstützte Zuordnungskonfigurationen](supported-mapping-configurations.md)
* [Zielbereitstellung](destination-delivery.md)
* [Aggregationsrichtlinie](aggregation-policy.md)
* [Batch-Konfiguration](batch-configuration.md)
* [Historische Profilqualifikationen](historical-profile-qualifications.md)