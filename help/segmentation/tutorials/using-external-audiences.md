---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Importieren und Verwenden externer Zielgruppen
description: In diesem Tutorial erfahren Sie, wie Sie externe Zielgruppen mit Adobe Experience Platform verwenden.
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
source-git-commit: 57586104f1119f5cda926faf286c1663fbb0b240
workflow-type: tm+mt
source-wordcount: '1664'
ht-degree: 6%

---

# Importieren und Verwenden externer Zielgruppen

Adobe Experience Platform unterstützt die Möglichkeit, externe Zielgruppen zu importieren, die anschließend als Komponenten für eine neue Segmentdefinition verwendet werden können. Dieses Dokument enthält ein Tutorial zum Einrichten der Experience Platform zum Importieren und Verwenden externer Zielgruppen.

## Erste Schritte

Dieses Tutorial setzt ein Verständnis der verschiedenen [!DNL Adobe Experience Platform] Dienste, die an der Erstellung von Zielgruppensegmenten beteiligt sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Services:

- [Segmentierungsdienst](../home.md): Ermöglicht das Erstellen von Zielgruppensegmenten aus Echtzeit-Kundenprofildaten.
- [Echtzeit-Kundenprofil](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [Experience-Datenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profile und Ereignisse gemäß den [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md) aufgenommen werden.
- [Datensätze](../../catalog/datasets/overview.md): Das Speicher- und Verwaltungskonstrukt für Datenpersistenz in Experience Platform.
- [Streaming-Erfassung](../../ingestion/streaming-ingestion/overview.md): So erfasst und speichert Experience Platform Daten von Client- und Server-seitigen Geräten in Echtzeit.

### Segmentdaten vs. Segmentmetadaten

Bevor Sie mit dem Importieren und Verwenden externer Zielgruppen beginnen, müssen Sie den Unterschied zwischen Segmentdaten und Segmentmetadaten verstehen.

Segmentdaten beziehen sich auf die Profile, die die Segmentqualifikationskriterien erfüllen und daher Teil der Zielgruppe sind.

Segmentmetadaten sind Informationen zum Segment selbst, einschließlich Name, Beschreibung, Ausdruck (falls zutreffend), Erstellungsdatum, Datum der letzten Änderung und Kennung. Die ID verknüpft die Segmentmetadaten mit den einzelnen Profilen, die die Segmentqualifikation erfüllen und Teil der resultierenden Zielgruppe sind.

| Segmentieren von Daten | Segmentmetadaten |
| ------------ | ---------------- |
| Profile, die die Segmentqualifikation erfüllen | Informationen zum Segment selbst |

## Erstellen eines Identitäts-Namespace für die externe Zielgruppe

Der erste Schritt zur Verwendung externer Zielgruppen besteht in der Erstellung eines Identitäts-Namespace. Identitäts-Namespaces ermöglichen es Platform, zu verknüpfen, woher ein Segment stammt.

Um einen Identitäts-Namespace zu erstellen, befolgen Sie die Anweisungen im Abschnitt [Identitäts-Namespace-Handbuch](../../identity-service/namespaces.md#manage-namespaces). Fügen Sie beim Erstellen Ihres Identitäts-Namespace die Quelldetails zum Identitäts-Namespace hinzu und markieren Sie dessen [!UICONTROL Typ] as a **[!UICONTROL Personenidentifizierung]**.

![Die Kennung ohne Person wird im Modal Identitäts-Namespace erstellen hervorgehoben.](../images/tutorials/external-audiences/identity-namespace-info.png)

## Erstellen eines Schemas für die Segmentmetadaten

Nachdem Sie einen Identitäts-Namespace erstellt haben, müssen Sie ein neues Schema für das Segment erstellen, das Sie erstellen werden.

Um mit der Erstellung eines Schemas zu beginnen, wählen Sie zunächst **[!UICONTROL Schemas]** in der linken Navigationsleiste, gefolgt von der **[!UICONTROL Schema erstellen]** in der oberen rechten Ecke des Arbeitsbereichs &quot;Schemas&quot;. Wählen Sie von hier aus **[!UICONTROL Durchsuchen]** um eine vollständige Auswahl der verfügbaren Schematypen anzuzeigen.

![Sowohl Schema erstellen als auch Durchsuchen sind hervorgehoben.](../images/tutorials/external-audiences/create-schema-browse.png)

Da Sie eine Segmentdefinition erstellen, bei der es sich um eine vordefinierte Klasse handelt, wählen Sie **[!UICONTROL Vorhandene Klasse verwenden]**. Wählen Sie nun die **[!UICONTROL Segmentdefinition]** -Klasse, gefolgt von **[!UICONTROL Klasse zuweisen]**.

![Die Segmentdefinitionsklasse wird hervorgehoben.](../images/tutorials/external-audiences/assign-class.png)

Nachdem Ihr Schema erstellt wurde, müssen Sie angeben, welches Feld die Segment-ID enthalten soll. Dieses Feld sollte als primäre Identität markiert und den zuvor von Ihnen erstellten Namespaces zugewiesen werden.

![Die Kontrollkästchen, mit denen das ausgewählte Feld als primäre Identität markiert werden soll, werden im Schema Editor hervorgehoben.](../images/tutorials/external-audiences/mark-primary-identifier.png)

Nachdem Sie die `_id` als primäre Identität festlegen, wählen Sie den Titel des Schemas aus, gefolgt von dem Umschalter mit der Bezeichnung **[!UICONTROL Profil]**. Auswählen **[!UICONTROL Aktivieren]** , um das Schema für [!DNL Real-Time Customer Profile].

![Der Umschalter zum Aktivieren des Schemas für Profil wird im Schema-Editor hervorgehoben.](../images/tutorials/external-audiences/schema-profile.png)

Jetzt ist dieses Schema für Profil aktiviert, wobei die primäre Identifizierung dem von Ihnen erstellten Identitäts-Namespace ohne Person zugewiesen ist. Das bedeutet, dass Segmentmetadaten, die mithilfe dieses Schemas in Platform importiert wurden, in das Profil aufgenommen werden, ohne mit anderen personenbezogenen Profildaten zusammengeführt zu werden.

## Datensatz für das Schema erstellen

Nach dem Konfigurieren des Schemas müssen Sie einen Datensatz für die Segmentmetadaten erstellen.

Um einen Datensatz zu erstellen, befolgen Sie die Anweisungen im Abschnitt [Benutzerhandbuch zu Datensätzen](../../catalog/datasets/user-guide.md#create). Sie sollten die **[!UICONTROL Datensatz aus Schema erstellen]** -Option unter Verwendung des zuvor erstellten Schemas.

![Das Schema, auf dem Ihr Datensatz basieren soll, ist hervorgehoben.](../images/tutorials/external-audiences/select-schema.png)

Nachdem Sie den Datensatz erstellt haben, folgen Sie den Anweisungen im Abschnitt [Benutzerhandbuch zu Datensätzen](../../catalog/datasets/user-guide.md#enable-profile) , um diesen Datensatz für das Echtzeit-Kundenprofil zu aktivieren.

![Der Umschalter zum Aktivieren des Schemas für Profil wird auf der Seite Datensatzaktivität hervorgehoben.](../images/tutorials/external-audiences/dataset-profile.png)

## Einrichten und Importieren von Zielgruppendaten

Wenn der Datensatz aktiviert ist, können Daten jetzt entweder über die Benutzeroberfläche oder über die Experience Platform-APIs an Platform gesendet werden. Sie können diese Daten entweder über eine Batch- oder Streaming-Verbindung erfassen.

### Daten mithilfe einer Batch-Verbindung erfassen

Um eine Batch-Verbindung zu erstellen, folgen Sie den Anweisungen im Abschnitt [Handbuch zur Benutzeroberfläche für den lokalen Datei-Upload](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Eine vollständige Liste der verfügbaren Quellen, mit denen Sie Daten erfassen können, finden Sie in der [Quellen - Übersicht](../../sources/home.md).

### Daten mithilfe einer Streaming-Verbindung erfassen

Um eine Streaming-Verbindung zu erstellen, folgen Sie den Anweisungen in [API-Tutorial](../../sources/tutorials/api/create/streaming/http.md) oder [UI-Tutorial](../../sources/tutorials/ui/create/streaming/http.md).

Nachdem Sie Ihre Streaming-Verbindung erstellt haben, haben Sie Zugriff auf Ihren eindeutigen Streaming-Endpunkt, an den Sie Ihre Daten senden können. Informationen zum Senden von Daten an diese Endpunkte finden Sie in der [Tutorial zum Streaming von Datensatzdaten](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![Der Streaming-Endpunkt für die Streaming-Verbindung wird auf der Seite mit den Quelldetails hervorgehoben.](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Struktur von Zielgruppen-Metadaten

Nach dem Erstellen einer Verbindung können Sie Ihre Daten jetzt in Platform erfassen.

Nachfolgend finden Sie ein Beispiel der Metadaten der externen Zielgruppen-Payload:

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{SEGMENT_ID}",
            "description": "Sample description",
            "identityMap": {
                "{IDENTITY_NAMESPACE}": [{
                    "id": "{}"
                }]
            },
            "segmentName" : "{SEGMENT_NAME}",
            "segmentStatus": "ACTIVE",
            "version": "1.0"
        }
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `schemaRef` | Das Schema **must** beziehen sich auf das zuvor erstellte Schema für die Segmentmetadaten. |
| `datasetId` | Die Datensatz-ID **must** bezieht sich auf den zuvor erstellten Datensatz für das soeben erstellte Schema. |
| `xdmEntity._id` | Die ID **must** bezieht sich auf dieselbe Segment-ID, die Sie als externe Zielgruppe verwenden. |
| `xdmEntity.identityMap` | Dieser Abschnitt **must** enthalten die Identitätsbezeichnung, die beim Erstellen des zuvor erstellten Namespace verwendet wird. |
| `{IDENTITY_NAMESPACE}` | Dies ist die Bezeichnung des zuvor erstellten Identitäts-Namespace. Wenn Sie beispielsweise Ihren Identitäts-Namespace &quot;externalAudience&quot;nennen, würden Sie ihn als Schlüssel des Arrays verwenden. |
| `segmentName` | Der Name des Segments, nach dem die externe Zielgruppe segmentiert werden soll. |

## Erstellen von Segmenten mit importierten Zielgruppen

Nachdem die importierten Zielgruppen eingerichtet wurden, können sie im Rahmen des Segmentierungsprozesses verwendet werden. Um externe Zielgruppen zu finden, navigieren Sie zum Segment Builder und wählen Sie **[!UICONTROL Zielgruppen]** im **[!UICONTROL Felder]** Abschnitt.

![Die Auswahl der externen Zielgruppen im Segment Builder wird hervorgehoben.](../images/tutorials/external-audiences/external-audiences.png)

## Nächste Schritte

Nachdem Sie jetzt externe Zielgruppen in Ihren Segmenten verwenden können, können Sie mit Segment Builder Segmente erstellen. Informationen zum Erstellen von Segmenten finden Sie im Abschnitt [Tutorial zum Erstellen von Segmenten](./create-a-segment.md).

## Anhang

Zusätzlich zur Verwendung importierter Metadaten aus externen Zielgruppen und deren Verwendung zum Erstellen von Segmenten können Sie auch externe Segmentmitgliedschaften in Platform importieren.

### Einrichten eines Zielschemas für die Mitgliedschaft in einem externen Segment

Um mit der Erstellung eines Schemas zu beginnen, wählen Sie zunächst **[!UICONTROL Schemas]** in der linken Navigationsleiste, gefolgt von der **[!UICONTROL Schema erstellen]** in der oberen rechten Ecke des Arbeitsbereichs &quot;Schemas&quot;. Wählen Sie von hier aus **[!UICONTROL XDM Individual Profile]**.

![Der Bereich &quot;XDM Individual Profile&quot;wird hervorgehoben.](../images/tutorials/external-audiences/create-schema-profile.png)

Nachdem das Schema erstellt wurde, müssen Sie die Feldergruppe Segmentmitgliedschaft als Teil des Schemas hinzufügen. Wählen Sie dazu [!UICONTROL Details zur Segmentzugehörigkeit], gefolgt von [!UICONTROL Feldergruppen hinzufügen].

![Die Feldergruppe Segmentzugehörigkeitsdetails wird hervorgehoben.](../images/tutorials/external-audiences/segment-membership-details.png)

Stellen Sie außerdem sicher, dass das Schema für **[!UICONTROL Profil]**. Dazu müssen Sie ein Feld als primäre Identität markieren.

![Der Umschalter zum Aktivieren des Schemas für Profil wird im Schema-Editor hervorgehoben.](../images/tutorials/external-audiences/external-segment-profile.png)

### Datensatz einrichten

Nachdem Sie Ihr Schema erstellt haben, müssen Sie einen Datensatz erstellen.

Um einen Datensatz zu erstellen, befolgen Sie die Anweisungen im Abschnitt [Benutzerhandbuch zu Datensätzen](../../catalog/datasets/user-guide.md#create). Sie sollten die **[!UICONTROL Datensatz aus Schema erstellen]** -Option unter Verwendung des zuvor erstellten Schemas.

![Das Schema, das Sie zum Erstellen der Datenbank verwenden, wird hervorgehoben.](../images/tutorials/external-audiences/select-schema.png)

Nachdem Sie den Datensatz erstellt haben, folgen Sie den Anweisungen im Abschnitt [Benutzerhandbuch zu Datensätzen](../../catalog/datasets/user-guide.md#enable-profile) , um diesen Datensatz für das Echtzeit-Kundenprofil zu aktivieren.

![Der Umschalter zum Aktivieren des Schemas für Profil wird im Arbeitsablauf zum Erstellen von Datensätzen hervorgehoben.](../images/tutorials/external-audiences/dataset-profile.png)

## Einrichten und Importieren externer Daten zur Zielgruppenmitgliedschaft

Wenn der Datensatz aktiviert ist, können Daten jetzt entweder über die Benutzeroberfläche oder über die Experience Platform-APIs an Platform gesendet werden. Sie können diese Daten entweder über eine Batch- oder Streaming-Verbindung erfassen.

### Daten mithilfe einer Batch-Verbindung erfassen

Um eine Batch-Verbindung zu erstellen, folgen Sie den Anweisungen im Abschnitt [Handbuch zur Benutzeroberfläche für den lokalen Datei-Upload](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Eine vollständige Liste der verfügbaren Quellen, mit denen Sie Daten erfassen können, finden Sie in der [Quellen - Übersicht](../../sources/home.md).

### Daten mithilfe einer Streaming-Verbindung erfassen

Um eine Streaming-Verbindung zu erstellen, folgen Sie den Anweisungen in [API-Tutorial](../../sources/tutorials/api/create/streaming/http.md) oder [UI-Tutorial](../../sources/tutorials/ui/create/streaming/http.md).

Nachdem Sie Ihre Streaming-Verbindung erstellt haben, haben Sie Zugriff auf Ihren eindeutigen Streaming-Endpunkt, an den Sie Ihre Daten senden können. Informationen zum Senden von Daten an diese Endpunkte finden Sie in der [Tutorial zum Streaming von Datensatzdaten](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![Der Streaming-Endpunkt für die Streaming-Verbindung wird auf der Seite mit den Quelldetails hervorgehoben.](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Struktur der Segmentmitgliedschaft

Nach dem Erstellen einer Verbindung können Sie Ihre Daten jetzt in Platform erfassen.

Nachfolgend finden Sie ein Beispiel der Payload der externen Zielgruppenmitgliedschaft:

```json
{
    "header": {
        "schemaRef": {
            "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
            "contentType": "application/vnd.adobe.xed-full+json;version=1"
        },
        "imsOrgId": "{ORG_ID}",
        "datasetId": "{DATASET_ID}",
        "source": {
            "name": "Sample External Audience Membership"
        }
    },
    "body": {
        "xdmMeta": {
            "schemaRef": {
                "id": "https://ns.adobe.com/{TENANT_ID}/schemas/{SCHEMA_ID}",
                "contentType": "application/vnd.adobe.xed-full+json;version=1"
            }
        },
        "xdmEntity": {
            "_id": "{UNIQUE_ID}",
            "description": "Sample description",
            "{TENANT_NAME}": {
                "identities": {
                    "{SCHEMA_IDENTITY}": "sample-id"
                }
            },
            "personId" : "sample-name",
            "segmentMembership": {
                "{IDENTITY_NAMESPACE}": {
                    "{EXTERNAL_IDENTITY}": {
                        "status": "realized",
                        "lastQualificationTime": "2022-03-14T:00:00:00Z"
                    }
                }
            }
        }
    }
}
```

| Eigenschaft | Beschreibung |
| -------- | ----------- |
| `schemaRef` | Das Schema **must** bezieht sich auf das zuvor erstellte Schema für die Daten zur Segmentmitgliedschaft. |
| `datasetId` | Die Datensatz-ID **must** bezieht sich auf den zuvor erstellten Datensatz für das soeben erstellte Mitgliedschaftsschema. |
| `xdmEntity._id` | Eine geeignete ID, die verwendet wird, um den Datensatz im Datensatz eindeutig zu identifizieren. |
| `{TENANT_NAME}.identities` | Dieser Abschnitt wird verwendet, um die Feldergruppe der benutzerdefinierten Identitäten mit den zuvor importierten Benutzern zu verbinden. |
| `segmentMembership.{IDENTITY_NAMESPACE}` | Dies ist die Bezeichnung des zuvor erstellten benutzerdefinierten Identitäts-Namespace. Wenn Sie beispielsweise Ihren Identitäts-Namespace &quot;externalAudience&quot;nennen, würden Sie ihn als Schlüssel des Arrays verwenden. |

>[!NOTE]
>
>Standardmäßig werden externe Zielgruppenmitgliedschaften nur 30 Tage lang aufbewahrt. Um sie länger als 30 Tage aufzubewahren, verwenden Sie bitte die `validUntil` beim Erfassen Ihrer Zielgruppendaten. Weitere Informationen zu diesem Feld finden Sie im Handbuch unter [Feldgruppen des Schemas Segmentzugehörigkeitsdetails](../../xdm/field-groups/profile/segmentation.md).