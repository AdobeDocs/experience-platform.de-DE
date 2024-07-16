---
solution: Experience Platform
title: Importieren und Verwenden externer Zielgruppen
description: In diesem Tutorial erfahren Sie, wie Sie externe Zielgruppen mit Adobe Experience Platform verwenden.
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
hide: true
hidefromtoc: true
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 4%

---

# Importieren und Verwenden externer Zielgruppen

>[!IMPORTANT]
>
>Diese Dokumentation enthält Informationen aus einer früheren Version der Dokumentation zu Zielgruppen und ist daher veraltet.

Adobe Experience Platform unterstützt die Möglichkeit, externe Zielgruppen zu importieren, die anschließend als Komponenten für eine neue Zielgruppe verwendet werden können. Dieses Dokument enthält ein Tutorial zum Einrichten von Experience Platform zum Importieren und Verwenden externer Zielgruppen.

## Erste Schritte

Dieses Tutorial setzt ein Verständnis der verschiedenen [!DNL Adobe Experience Platform]-Dienste voraus, die am Erstellen von Zielgruppen beteiligt sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Services:

- [Segmentation Service](../home.md): Ermöglicht Ihnen das Erstellen von Zielgruppen aus Echtzeit-Kundenprofildaten.
- [Echtzeit-Kundenprofil](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [Experience-Datenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profile und Ereignisse gemäß den [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md) aufgenommen werden.
- [Datensätze](../../catalog/datasets/overview.md): Das Speicher- und Verwaltungskonstrukt für Datenpersistenz in Experience Platform.
- [Streaming-Erfassung](../../ingestion/streaming-ingestion/overview.md): So erfasst und speichert Experience Platform Daten von Client- und Server-seitigen Geräten in Echtzeit.

### Zielgruppen vs. Segmentdefinitionen

Bevor Sie mit dem Import und der Verwendung externer Zielgruppen beginnen, müssen Sie sich mit dem Unterschied zwischen Zielgruppen und Segmentdefinitionen vertraut machen.

Zielgruppen beziehen sich auf die Gruppe von Profilen, nach denen Sie filtern möchten. Bei Verwendung von Segmentdefinitionen können Sie eine Zielgruppe erstellen, indem Sie eine Segmentdefinition erstellen, die Ihre Profile in die Teilmenge filtert, die die Segmentqualifikationskriterien erfüllt.

Segmentdefinitionen umfassen Informationen wie den Namen, die Beschreibung, den Ausdruck (falls zutreffend), das Erstellungsdatum, das Datum der letzten Änderung und eine ID. Die ID verknüpft die Segmentmetadaten mit den einzelnen Profilen, die die Segmentqualifikation erfüllen und Teil der resultierenden Zielgruppe sind.

| Zielgruppen | Segmentdefinition |
| --------- | ---------------- |
| Die Gruppe von Profilen, die Sie suchen. Bei der Verwendung von Segmentdefinitionen bedeutet dies, dass die Gruppe von Profilen die Segmentqualifizierung erfüllt. | Die Gruppe von Regeln, die zum Segmentieren der gesuchten Zielgruppe verwendet werden. |

## Erstellen eines Identitäts-Namespace für die externe Zielgruppe

Der erste Schritt zur Verwendung externer Zielgruppen besteht in der Erstellung eines Identitäts-Namespace. Identitäts-Namespaces ermöglichen es Platform, zu verknüpfen, woher eine Zielgruppe stammt.

Um einen Identitäts-Namespace zu erstellen, befolgen Sie die Anweisungen im Handbuch [Identitäts-Namespace](../../identity-service/features/namespaces.md#manage-namespaces). Fügen Sie beim Erstellen Ihres Identitäts-Namespace die Quelldetails zum Identitäts-Namespace hinzu und markieren Sie dessen [!UICONTROL Typ] als **[!UICONTROL Kennung für Personen ohne diese]**.

![Die Kennung ohne Person wird im Modal Identitäts-Namespace erstellen hervorgehoben.](../images/tutorials/external-audiences/identity-namespace-info.png)

## Erstellen eines Schemas für die Segmentmetadaten

Nachdem Sie einen Identitäts-Namespace erstellt haben, müssen Sie ein neues Schema für das Segment erstellen, das Sie erstellen werden.

Um mit dem Erstellen eines Schemas zu beginnen, wählen Sie zunächst **[!UICONTROL Schemas]** in der linken Navigationsleiste und dann das Schema erstellen **[!UICONTROL Schema erstellen]** in der oberen rechten Ecke des Arbeitsbereichs &quot;Schemas&quot;. Wählen Sie hier **[!UICONTROL Durchsuchen]** aus, um eine vollständige Auswahl der verfügbaren Schematypen anzuzeigen.

![Schema erstellen und Durchsuchen werden hervorgehoben.](../images/tutorials/external-audiences/create-schema-browse.png)

Da Sie eine Segmentdefinition erstellen, bei der es sich um eine vordefinierte Klasse handelt, wählen Sie **[!UICONTROL Vorhandene Klasse verwenden]**. Wählen Sie nun die Klasse **[!UICONTROL Segmentdefinition]** und danach **[!UICONTROL Klasse zuweisen]** aus.

![Die Segmentdefinitionsklasse wird hervorgehoben.](../images/tutorials/external-audiences/assign-class.png)

Nachdem Ihr Schema erstellt wurde, müssen Sie angeben, welches Feld die Segment-ID enthalten soll. Dieses Feld sollte als primäre Identität markiert und den zuvor von Ihnen erstellten Namespaces zugewiesen werden.

![Die Kontrollkästchen, mit denen das ausgewählte Feld als primäre Identität markiert werden soll, werden im Schema Editor hervorgehoben.](../images/tutorials/external-audiences/mark-primary-identifier.png)

Nachdem Sie das Feld `_id` als primäre Identität markiert haben, wählen Sie den Titel des Schemas aus, gefolgt von dem Umschalter mit der Bezeichnung **[!UICONTROL Profil]**. Wählen Sie **[!UICONTROL Aktivieren]** aus, um das Schema für [!DNL Real-Time Customer Profile] zu aktivieren.

![Der Umschalter zum Aktivieren des Schemas für Profil wird im Schema-Editor hervorgehoben.](../images/tutorials/external-audiences/schema-profile.png)

Jetzt ist dieses Schema für Profil aktiviert, wobei die primäre Identifizierung dem von Ihnen erstellten Identitäts-Namespace ohne Person zugewiesen ist. Das bedeutet, dass Segmentmetadaten, die mithilfe dieses Schemas in Platform importiert wurden, in das Profil aufgenommen werden, ohne mit anderen personenbezogenen Profildaten zusammengeführt zu werden.

## Datensatz für das Schema erstellen

Nach dem Konfigurieren des Schemas müssen Sie einen Datensatz für die Segmentmetadaten erstellen.

Um einen Datensatz zu erstellen, befolgen Sie die Anweisungen im [Benutzerhandbuch zum Datensatz](../../catalog/datasets/user-guide.md#create). Sie sollten die Option **[!UICONTROL Datensatz aus Schema erstellen]** mit dem zuvor erstellten Schema verwenden.

![Das Schema, auf dem der Datensatz basieren soll, ist hervorgehoben.](../images/tutorials/external-audiences/select-schema.png)

Nachdem Sie den Datensatz erstellt haben, befolgen Sie die Anweisungen im [Benutzerhandbuch zum Datensatz](../../catalog/datasets/user-guide.md#enable-profile) , um diesen Datensatz für das Echtzeit-Kundenprofil zu aktivieren.

![Der Umschalter zum Aktivieren des Schemas für Profil wird auf der Seite Datensatzaktivität hervorgehoben.](../images/tutorials/external-audiences/dataset-profile.png)

## Einrichten und Importieren von Zielgruppendaten

Wenn der Datensatz aktiviert ist, können Daten jetzt entweder über die Benutzeroberfläche oder mithilfe der Experience Platform-APIs an Platform gesendet werden. Sie können diese Daten entweder über eine Batch- oder Streaming-Verbindung erfassen.

### Daten mithilfe einer Batch-Verbindung erfassen

Um eine Batch-Verbindung zu erstellen, befolgen Sie die Anweisungen im allgemeinen Benutzerhandbuch für den [lokalen Datei-Upload](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Eine vollständige Liste der verfügbaren Quellen, mit denen Sie Daten erfassen können, finden Sie in der [Quellenübersicht](../../sources/home.md).

### Daten mithilfe einer Streaming-Verbindung erfassen

Um eine Streaming-Verbindung zu erstellen, folgen Sie den Anweisungen im Tutorial [API-Tutorial](../../sources/tutorials/api/create/streaming/http.md) oder im Tutorial [UI-Tutorial](../../sources/tutorials/ui/create/streaming/http.md).

Nachdem Sie Ihre Streaming-Verbindung erstellt haben, haben Sie Zugriff auf Ihren eindeutigen Streaming-Endpunkt, an den Sie Ihre Daten senden können. Informationen zum Senden von Daten an diese Endpunkte finden Sie im [Tutorial zum Streaming von Datensatzdaten](../../ingestion/tutorials/streaming-record-data.md#ingest-data) .

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
| `schemaRef` | Das Schema &quot;**must**&quot; bezieht sich auf das zuvor erstellte Schema für die Segmentmetadaten. |
| `datasetId` | Die Datensatz-ID **muss** auf den zuvor erstellten Datensatz für das soeben erstellte Schema verweisen. |
| `xdmEntity._id` | Die Kennung **muss** auf dieselbe Segment-ID verweisen, die Sie als Ihre externe Zielgruppe verwenden. |
| `xdmEntity.identityMap` | Dieser Abschnitt **muss** die Identitätsbezeichnung enthalten, die beim Erstellen des zuvor erstellten Namespace verwendet wird. |
| `{IDENTITY_NAMESPACE}` | Dies ist die Bezeichnung des zuvor erstellten Identitäts-Namespace. Wenn Sie beispielsweise Ihren Identitäts-Namespace &quot;externalAudience&quot;nennen, würden Sie ihn als Schlüssel des Arrays verwenden. |
| `segmentName` | Der Name des Segments, nach dem die externe Zielgruppe segmentiert werden soll. |

## Erstellen von Segmenten mit importierten Zielgruppen

Nachdem die importierten Zielgruppen eingerichtet wurden, können sie im Rahmen des Segmentierungsprozesses verwendet werden. Um externe Zielgruppen zu finden, gehen Sie zum Segment Builder und wählen Sie im Abschnitt **[!UICONTROL Felder]** die Registerkarte **[!UICONTROL Zielgruppen]** aus.

![Der externe Zielgruppenselektor im Segment Builder ist hervorgehoben.](../images/tutorials/external-audiences/external-audiences.png)

## Nächste Schritte

Nachdem Sie jetzt externe Zielgruppen in Ihren Segmenten verwenden können, können Sie mit Segment Builder Segmente erstellen. Informationen zum Erstellen von Segmenten finden Sie im Tutorial [ zum Erstellen von Segmenten](./create-a-segment.md).

## Anhang

Zusätzlich zur Verwendung importierter Metadaten aus externen Zielgruppen und deren Verwendung zum Erstellen von Segmenten können Sie auch externe Segmentmitgliedschaften in Platform importieren.

### Einrichten eines Zielschemas für die Mitgliedschaft in einem externen Segment

Um mit dem Erstellen eines Schemas zu beginnen, wählen Sie zunächst **[!UICONTROL Schemas]** in der linken Navigationsleiste und dann das Schema erstellen **[!UICONTROL Schema erstellen]** in der oberen rechten Ecke des Arbeitsbereichs &quot;Schemas&quot;. Wählen Sie hier **[!UICONTROL XDM Individual Profile]** aus.

![Der Bereich &quot;XDM Individual Profile&quot;ist hervorgehoben.](../images/tutorials/external-audiences/create-schema-profile.png)

Nachdem das Schema erstellt wurde, müssen Sie die Feldergruppe Segmentmitgliedschaft als Teil des Schemas hinzufügen. Wählen Sie dazu [!UICONTROL Details der Segmentmitgliedschaft] und danach [!UICONTROL Feldergruppen hinzufügen] aus.

![Die Feldergruppe Segmentzugehörigkeitsdetails wird hervorgehoben.](../images/tutorials/external-audiences/segment-membership-details.png)

Stellen Sie außerdem sicher, dass das Schema für **[!UICONTROL Profil]** markiert ist. Dazu müssen Sie ein Feld als primäre Identität markieren.

![Der Umschalter zum Aktivieren des Schemas für Profil wird im Schema-Editor hervorgehoben.](../images/tutorials/external-audiences/external-segment-profile.png)

### Datensatz einrichten

Nachdem Sie Ihr Schema erstellt haben, müssen Sie einen Datensatz erstellen.

Um einen Datensatz zu erstellen, befolgen Sie die Anweisungen im [Benutzerhandbuch zum Datensatz](../../catalog/datasets/user-guide.md#create). Sie sollten die Option **[!UICONTROL Datensatz aus Schema erstellen]** mit dem zuvor erstellten Schema verwenden.

![Das Schema, das Sie zum Erstellen der Datenbank verwenden, wird hervorgehoben.](../images/tutorials/external-audiences/select-schema.png)

Nachdem Sie den Datensatz erstellt haben, befolgen Sie die Anweisungen im [Benutzerhandbuch zum Datensatz](../../catalog/datasets/user-guide.md#enable-profile) , um diesen Datensatz für das Echtzeit-Kundenprofil zu aktivieren.

![Der Umschalter zum Aktivieren des Schemas für Profil wird im Workflow zum Erstellen von Datensätzen hervorgehoben.](../images/tutorials/external-audiences/dataset-profile.png)

## Einrichten und Importieren externer Daten zur Zielgruppenmitgliedschaft

Wenn der Datensatz aktiviert ist, können Daten jetzt entweder über die Benutzeroberfläche oder mithilfe der Experience Platform-APIs an Platform gesendet werden. Sie können diese Daten entweder über eine Batch- oder Streaming-Verbindung erfassen.

### Daten mithilfe einer Batch-Verbindung erfassen

Um eine Batch-Verbindung zu erstellen, befolgen Sie die Anweisungen im allgemeinen Benutzerhandbuch für den [lokalen Datei-Upload](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Eine vollständige Liste der verfügbaren Quellen, mit denen Sie Daten erfassen können, finden Sie in der [Quellenübersicht](../../sources/home.md).

### Daten mithilfe einer Streaming-Verbindung erfassen

Um eine Streaming-Verbindung zu erstellen, folgen Sie den Anweisungen im Tutorial [API-Tutorial](../../sources/tutorials/api/create/streaming/http.md) oder im Tutorial [UI-Tutorial](../../sources/tutorials/ui/create/streaming/http.md).

Nachdem Sie Ihre Streaming-Verbindung erstellt haben, haben Sie Zugriff auf Ihren eindeutigen Streaming-Endpunkt, an den Sie Ihre Daten senden können. Informationen zum Senden von Daten an diese Endpunkte finden Sie im [Tutorial zum Streaming von Datensatzdaten](../../ingestion/tutorials/streaming-record-data.md#ingest-data) .

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
| `schemaRef` | Das Schema &quot;**must**&quot; bezieht sich auf das zuvor erstellte Schema für die Segmentmitgliedsdaten. |
| `datasetId` | Die Datensatz-ID **muss** auf den zuvor erstellten Datensatz für das soeben erstellte Mitgliedschaftsschema verweisen. |
| `xdmEntity._id` | Eine geeignete ID, die verwendet wird, um den Datensatz im Datensatz eindeutig zu identifizieren. |
| `{TENANT_NAME}.identities` | Dieser Abschnitt wird verwendet, um die Feldergruppe der benutzerdefinierten Identitäten mit den zuvor importierten Benutzern zu verbinden. |
| `segmentMembership.{IDENTITY_NAMESPACE}` | Dies ist die Bezeichnung des zuvor erstellten benutzerdefinierten Identitäts-Namespace. Wenn Sie beispielsweise Ihren Identitäts-Namespace &quot;externalAudience&quot;nennen, würden Sie ihn als Schlüssel des Arrays verwenden. |

>[!NOTE]
>
>Standardmäßig werden externe Zielgruppenmitgliedschaften nach 30 Tagen gelöscht. Um zu verhindern, dass Daten gelöscht und länger als 30 Tage aufbewahrt werden, verwenden Sie beim Erfassen Ihrer Zielgruppendaten das Feld `validUntil` . Weiterführende Informationen zu diesem Feld finden Sie im Handbuch zu den Schemakategorien für die Segmentzugehörigkeitsdetails ](../../xdm/field-groups/profile/segmentation.md).[
