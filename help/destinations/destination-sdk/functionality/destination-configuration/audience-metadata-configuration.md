---
description: Erfahren Sie, wie Sie die Metadateneinstellungen der Zielgruppe für Ziele konfigurieren, die mit Destination SDK erstellt wurden.
title: Konfiguration von Zielgruppen-Metadaten
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 6%

---


# Konfiguration von Zielgruppen-Metadaten

Beim Exportieren von Daten aus der Experience Platform in Ihr Ziel benötigen Sie möglicherweise bestimmte Zielgruppen-Metadaten, wie Segmentnamen oder Segment-IDs, die für die Experience Platform und Ihr Ziel freigegeben werden.

Destination SDK bietet Tools, mit denen Sie Zielgruppen in Ihrer Zielplattform programmgesteuert erstellen, aktualisieren oder löschen können.

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm im [Konfigurationsoptionen](../configuration-options.md) Dokumentation oder lesen Sie das Handbuch zu [Verwenden von Destination SDK zum Konfigurieren eines Streaming-Ziels](../../guides/configure-destination-instructions.md#create-destination-configuration).

Sie können die Vorlage für Zielgruppen-Metadaten über die `/authoring/audience-templates` -Endpunkt. Nachdem Sie die Konfiguration der Zielgruppen-Metadaten erstellt haben, können Sie die `/authoring/destinations` Endpunkt zum Konfigurieren des `audienceMetadataConfig` Abschnitt. Dieser Abschnitt teilt Ihrem Ziel mit, welche Segmentmetadaten Ihrer Zielgruppenvorlage zugeordnet werden sollen.

Detaillierte Beispiele für API-Aufrufe, in denen Sie die auf dieser Seite angezeigten Komponenten konfigurieren können, finden Sie auf den folgenden API-Referenzseiten.

* [Erstellen einer Zielkonfiguration](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Zielkonfiguration aktualisieren](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [Erstellen einer Zielgruppenvorlage](../../metadata-api/create-audience-template.md)
* [Aktualisieren einer Zielgruppenvorlage](../../metadata-api/update-audience-template.md)

>[!IMPORTANT]
>
>Alle von Destination SDK unterstützten Parameternamen und Werte sind **Groß-/Kleinschreibung**. Um Fehler bei der Groß-/Kleinschreibung zu vermeiden, verwenden Sie bitte die Parameternamen und -werte genau wie in der Dokumentation dargestellt.

## Unterstützte Integrationstypen {#supported-integration-types}

Die nachstehende Tabelle beschreibt ausführlich, welche Integrationstypen die auf dieser Seite beschriebenen Funktionen unterstützen.

| Integrationstyp | Unterstützt Funktionen |
|---|---|
| Echtzeit-Integrationen (Streaming) | Ja |
| Dateibasierte (Batch-)Integrationen | Ja |

## Unterstützte Parameter {#supported-parameters}

Bei der Erstellung Ihrer Audience-Metadatenkonfiguration können Sie die in der folgenden Tabelle beschriebenen Parameter verwenden, um die Einstellungen für die Segmentzuordnung zu konfigurieren.

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
| `mapExperiencePlatformSegmentName` | Boolesch | Gibt an, ob die Variable [[!UICONTROL Zuordnungs-ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) -Wert im Zielaktivierungs-Workflow sollte der Segmentname der Experience Platform sein. |
| `mapExperiencePlatformSegmentId` | Boolesch | Gibt an, ob die Variable [[!UICONTROL Zuordnungs-ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) -Wert im Zielaktivierungs-Workflow sollte die Experience Platform-Segment-ID sein. |
| `mapUserInput` | Boolesch | Aktiviert oder deaktiviert die Benutzereingabe für die [[!UICONTROL Zuordnungs-ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) -Wert im Zielaktivierungs-Workflow. Wenn auf `true`, `audienceTemplateId` nicht vorhanden sein. |
| `audienceTemplateId` | Boolesch | Die `instanceId` des [Zielgruppen-Metadatenvorlage](../../metadata-api/create-audience-template.md) verwendet für Ihr Ziel. |

{style="table-layout:auto"}

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie ein besseres Verständnis davon haben, wie Sie Zielgruppen-Metadaten für Ihr Ziel konfigurieren können.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Konfiguration der Kundenauthentifizierung](customer-authentication.md)
* [OAuth 2-Authentifizierung](oauth2-authentication.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Benutzeroberflächenattribute](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Identitäts-Namespace-Konfiguration](identity-namespace-configuration.md)
* [Unterstützte Zuordnungskonfigurationen](supported-mapping-configurations.md)
* [Zielbereitstellung](destination-delivery.md)
* [Aggregationsrichtlinie](aggregation-policy.md)
* [Batch-Konfiguration](batch-configuration.md)
* [Historische Profilqualifikationen](historical-profile-qualifications.md)