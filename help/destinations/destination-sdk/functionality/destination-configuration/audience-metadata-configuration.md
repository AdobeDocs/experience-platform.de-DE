---
description: Erfahren Sie, wie Sie die Zielgruppen-Metadateneinstellungen für Ziele konfigurieren, die mit Destination SDK erstellt wurden.
title: Konfiguration von Zielgruppen-Metadaten
exl-id: ae71df4f-b753-4084-835f-03559b4986cb
source-git-commit: 20cb2dbfbfc8e73c765073818c8e7e561d4e6629
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 90%

---

# Konfiguration von Zielgruppen-Metadaten

Beim Exportieren von Daten aus Experience Platform in Ihr Ziel benötigen Sie möglicherweise bestimmte Zielgruppen-Metadaten, wie Zielgruppennamen oder Zielgruppen-IDs, die für Experience Platform und Ihr Ziel freigegeben werden.

Destination SDK bietet Tools, mit denen Sie Zielgruppen in Ihrer Zielplattform programmgesteuert erstellen, aktualisieren oder löschen können.

Informationen dazu, wo diese Komponente in eine mit Destination SDK erstellte Integration passt, finden Sie im Diagramm in der Dokumentation zu [Konfigurationsoptionen](../configuration-options.md) oder im Handbuch dazu, wie Sie mit der Destination SDK [ein Streaming-Ziel konfigurieren](../../guides/configure-destination-instructions.md#create-destination-configuration).

Sie können die Vorlage für Zielgruppen-Metadaten über den Endpunkt `/authoring/audience-templates` konfigurieren. Nachdem Sie die Konfiguration der Zielgruppen-Metadaten erstellt haben, können Sie den Endpunkt `/authoring/destinations` zum Konfigurieren des Abschnitts `audienceMetadataConfig` verwenden. Dieser Abschnitt teilt Ihrem Ziel mit, welche Zielgruppenmetadaten Ihrer Zielgruppenvorlage zugeordnet werden sollen.

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

Beim Erstellen der Konfiguration für Ihre Zielgruppenmetadaten können Sie die in der folgenden Tabelle beschriebenen Parameter verwenden, um die Einstellungen für die Zielgruppenzuordnung zu konfigurieren.

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
| `mapExperiencePlatformSegmentName` | Boolesch | Gibt an, ob der Wert der [[!UICONTROL Zuordnungs-ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) im Zielaktivierungs-Workflow der Zielgruppenname aus Experience Platform sein soll. |
| `mapExperiencePlatformSegmentId` | Boolesch | Gibt an, ob der Wert der [[!UICONTROL Zuordnungs-ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) im Zielaktivierungs-Workflow die Zielgruppen-ID aus Experience Platform sein soll. |
| `mapUserInput` | Boolesch | Aktiviert oder deaktiviert die Benutzereingabe für den Wert der [[!UICONTROL Zuordnungs-ID]](../../../ui/activate-segment-streaming-destinations.md#scheduling) im Zielaktivierungs-Workflow. Wenn er auf `true`, gesetzt ist, kann `audienceTemplateId` nicht vorhanden sein. |
| `audienceTemplateId` | Zeichenfolge | Die `instanceId` der [Zielgruppen-Metadatenvorlage](../../metadata-api/create-audience-template.md), die für Ihr Ziel verwendet wird. |

{style="table-layout:auto"}

## Nächste Schritte {#next-steps}

Nach dem Lesen dieses Artikels sollten Sie ein besseres Verständnis davon haben, wie Sie Zielgruppen-Metadaten für Ihr Ziel konfigurieren können.

Weitere Informationen zu den anderen Zielkomponenten finden Sie in den folgenden Artikeln:

* [Konfiguration der Kundenauthentifizierung](customer-authentication.md)
* [OAuth2-Autorisierung](oauth2-authorization.md)
* [Benutzerdefinierte Datenfelder](customer-data-fields.md)
* [Benutzeroberflächenattribute](ui-attributes.md)
* [Schemakonfiguration](schema-configuration.md)
* [Konfiguration von Identity-Namespaces](identity-namespace-configuration.md)
* [Unterstützte Zuordnungskonfigurationen](supported-mapping-configurations.md)
* [Zielbereitstellung](destination-delivery.md)
* [Aggregationsrichtlinie](aggregation-policy.md)
* [Batch-Konfiguration](batch-configuration.md)
* [Historische Profilqualifikationen](historical-profile-qualifications.md)
