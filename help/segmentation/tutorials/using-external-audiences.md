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
>Diese Dokumentation enthält Informationen aus einer früheren Version der Zielgruppen-Dokumentation und ist daher veraltet.

Adobe Experience Platform unterstützt den Import externer Zielgruppen, die anschließend als Komponenten für eine neue Zielgruppe verwendet werden können. Dieses Dokument enthält eine Anleitung zum Einrichten von Experience Platform für den Import und die Verwendung externer Zielgruppen.

## Erste Schritte

Dieses Tutorial setzt ein Grundverständnis der verschiedenen [!DNL Adobe Experience Platform]-Services voraus, die bei der Erstellung von Zielgruppen zum Einsatz kommen. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Services:

- [Segmentierungs-](../home.md): Ermöglicht das Erstellen von Zielgruppen aus Echtzeit-Kundenprofildaten.
- [Echtzeit-Kundenprofil](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [Experience-Datenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profile und Ereignisse gemäß den [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md) aufgenommen werden.
- [Datensätze](../../catalog/datasets/overview.md): Das Speicher- und Verwaltungskonstrukt für Datenpersistenz in Experience Platform.
- [Streaming-Aufnahme](../../ingestion/streaming-ingestion/overview.md): Wie Experience Platform Daten von Client- und Server-seitigen Geräten in Echtzeit aufnimmt und speichert.

### Zielgruppen vs. Segmentdefinitionen

Bevor Sie mit dem Import und der Verwendung externer Zielgruppen beginnen, müssen Sie den Unterschied zwischen Zielgruppen und Segmentdefinitionen verstehen.

Zielgruppen beziehen sich auf die Gruppe von Profilen, nach denen Sie filtern möchten. Bei Verwendung von Segmentdefinitionen können Sie eine Zielgruppe erstellen, indem Sie eine Segmentdefinition erstellen, die Ihre Profile nach der Teilmenge filtert, die den Segmentqualifikationskriterien entspricht.

Segmentdefinitionen enthalten Informationen wie den Namen, die Beschreibung, den Ausdruck (falls zutreffend), das Erstellungsdatum, das Datum der letzten Änderung und eine ID. Die ID verknüpft die Segmentmetadaten mit den einzelnen Profilen, die die Segmentqualifikation erfüllen und Teil der resultierenden Audience sind.

| Zielgruppen | Segmentdefinition |
| --------- | ---------------- |
| Die Gruppe von Profilen, die Sie suchen. Bei Verwendung von Segmentdefinitionen bedeutet dies, dass es sich um die Gruppe von Profilen handelt, die die Segmentqualifikation erfüllen. | Die Gruppe von Regeln, die zum Segmentieren der gesuchten Zielgruppe verwendet werden. |

## Erstellen eines Identity-Namespace für die externe Zielgruppe

Der erste Schritt zur Verwendung externer Zielgruppen besteht darin, einen Identity-Namespace zu erstellen. Mit Identity-Namespaces kann Platform verknüpfen, woher eine Zielgruppe stammt.

Um einen Identity-Namespace zu erstellen, befolgen Sie die Anweisungen im [Handbuch zum Identity-Namespace](../../identity-service/features/namespaces.md#manage-namespaces). Fügen Sie beim Erstellen Ihres Identity-Namespace die Quelldetails zum Identity-Namespace hinzu und markieren Sie dessen [!UICONTROL Typ] als **[!UICONTROL Nicht-Personen-Kennung]**.

![Die Nicht-Personen-Kennung wird im Modal „Identity-Namespace erstellen“ hervorgehoben.](../images/tutorials/external-audiences/identity-namespace-info.png)

## Erstellen eines Schemas für die Segmentmetadaten

Nachdem Sie einen Identity-Namespace erstellt haben, müssen Sie ein neues Schema für das Segment erstellen, das Sie erstellen möchten.

Um mit dem Erstellen eines Schemas zu beginnen **[!UICONTROL wählen Sie zunächst]** Schemata“ in der linken Navigationsleiste und dann **[!UICONTROL Schema erstellen]** in der oberen rechten Ecke des Arbeitsbereichs Schemata aus. Wählen Sie hier **[!UICONTROL Durchsuchen]**, um eine vollständige Auswahl der verfügbaren Schematypen anzuzeigen.

![Sowohl Schema erstellen als auch Durchsuchen sind hervorgehoben.](../images/tutorials/external-audiences/create-schema-browse.png)

Da Sie eine Segmentdefinition erstellen, bei der es sich um eine vordefinierte Klasse handelt, wählen Sie **[!UICONTROL Vorhandene Klasse verwenden]** aus. Wählen Sie jetzt die Klasse **[!UICONTROL Segmentdefinition]** und dann **[!UICONTROL Klasse zuweisen]** aus.

![Die Segmentdefinitionsklasse ist hervorgehoben.](../images/tutorials/external-audiences/assign-class.png)

Nachdem Ihr Schema erstellt wurde, müssen Sie angeben, welches Feld die Segment-ID enthalten wird. Dieses Feld sollte als primäre Identität markiert und den zuvor erstellten Namespaces zugewiesen werden.

![Die Kontrollkästchen zum Markieren des ausgewählten Felds als primäre Identität werden im Schema-Editor hervorgehoben.](../images/tutorials/external-audiences/mark-primary-identifier.png)

Nachdem Sie das Feld `_id` als primäre Identität markiert haben, wählen Sie den Titel des Schemas aus, gefolgt vom Umschalter mit der Bezeichnung **[!UICONTROL Profil]**. Wählen Sie **[!UICONTROL Aktivieren]** aus, um das Schema für die [!DNL Real-Time Customer Profile] zu aktivieren.

![Der Umschalter zum Aktivieren des Schemas für das Profil ist im Schema-Editor hervorgehoben.](../images/tutorials/external-audiences/schema-profile.png)

Jetzt ist dieses Schema für das Profil aktiviert, wobei die primäre Kennung dem von Ihnen erstellten Nicht-Personen-Identity-Namespace zugewiesen ist. Dies bedeutet, dass Segmentmetadaten, die mit diesem Schema in Platform importiert wurden, in Profile aufgenommen werden, ohne mit anderen personenbezogenen Profildaten zusammengeführt zu werden.

## Erstellen eines Datensatzes für das Schema

Nach dem Konfigurieren des Schemas müssen Sie einen Datensatz für die Segmentmetadaten erstellen.

Um einen Datensatz zu erstellen, befolgen Sie die Anweisungen im [Benutzerhandbuch für Datensätze](../../catalog/datasets/user-guide.md#create). Sie sollten der Option **[!UICONTROL Datensatz aus Schema erstellen]** unter Verwendung des zuvor erstellten Schemas folgen.

![Das Schema, auf dem Ihr Datensatz basieren soll, ist hervorgehoben.](../images/tutorials/external-audiences/select-schema.png)

Nachdem Sie den Datensatz erstellt haben, befolgen Sie die Anweisungen im [Benutzerhandbuch zum Datensatz](../../catalog/datasets/user-guide.md#enable-profile), um diesen Datensatz für das Echtzeit-Kundenprofil zu aktivieren.

![Der Umschalter zum Aktivieren des Schemas für das Profil ist auf der Seite Datensatzaktivität hervorgehoben.](../images/tutorials/external-audiences/dataset-profile.png)

## Zielgruppendaten einrichten und importieren

Wenn der Datensatz aktiviert ist, können Daten jetzt entweder über die Benutzeroberfläche oder mithilfe der Experience Platform-APIs an Platform gesendet werden. Sie können diese Daten entweder über eine Batch- oder Streaming-Verbindung aufnehmen.

### Aufnehmen von Daten über eine Batch-Verbindung

Um eine Batch-Verbindung zu erstellen, folgen Sie den Anweisungen im generischen [Handbuch zur Benutzeroberfläche für den Upload lokaler Dateien](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Eine vollständige Liste der verfügbaren Quellen, mit denen Sie Daten aufnehmen können, finden Sie unter [Quellen - Übersicht](../../sources/home.md).

### Aufnehmen von Daten über eine Streaming-Verbindung

Um eine Streaming-Verbindung zu erstellen, folgen Sie den Anweisungen entweder im [API-Tutorial](../../sources/tutorials/api/create/streaming/http.md) oder im [UI-Tutorial](../../sources/tutorials/ui/create/streaming/http.md).

Nachdem Sie Ihre Streaming-Verbindung erstellt haben, haben Sie Zugriff auf Ihren eindeutigen Streaming-Endpunkt, an den Sie Ihre Daten senden können. Informationen zum Senden von Daten an diese Endpunkte finden Sie im [Tutorial zum Streaming von Datensatzdaten](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![Der Streaming-Endpunkt für die Streaming-Verbindung wird auf der Seite mit den Quelldetails hervorgehoben.](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Zielgruppen-Metadatenstruktur

Nachdem Sie eine Verbindung erstellt haben, können Sie Ihre Daten jetzt in Platform aufnehmen.

Nachfolgend finden Sie ein Beispiel für die Metadaten der Payload der externen Zielgruppe:

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
| `schemaRef` | Das Schema **muss** für die Segmentmetadaten auf das zuvor erstellte Schema verweisen. |
| `datasetId` | Die Datensatz-ID **muss** verweist für das soeben erstellte Schema auf den zuvor erstellten Datensatz. |
| `xdmEntity._id` | Die ID **muss** auf dieselbe Segment-ID verweisen, die Sie als externe Zielgruppe verwenden. |
| `xdmEntity.identityMap` | Dieser Abschnitt **muss** die Identitätsbeschriftung enthalten, die beim Erstellen des zuvor erstellten Namespace verwendet wurde. |
| `{IDENTITY_NAMESPACE}` | Dies ist die Bezeichnung des zuvor erstellten Identity-Namespace. Wenn Sie beispielsweise Ihren Identity-Namespace „externalAudience“ aufrufen, verwenden Sie diesen als Schlüssel des Arrays. |
| `segmentName` | Der Name des Segments, nach dem die externe Zielgruppe segmentiert werden soll. |

## Erstellen von Segmenten mit importierten Audiences

Nachdem die importierten Zielgruppen eingerichtet wurden, können sie im Rahmen des Segmentierungsprozesses verwendet werden. Um externe Zielgruppen zu finden, wechseln Sie zum Segment Builder und wählen Sie **[!UICONTROL Zielgruppen]** im Abschnitt **[!UICONTROL Felder]** aus.

![Der Selektor für externe Zielgruppen in Segment Builder ist hervorgehoben.](../images/tutorials/external-audiences/external-audiences.png)

## Nächste Schritte

Da Sie nun externe Zielgruppen in Ihren Segmenten verwenden können, können Sie mit Segment Builder Segmente erstellen. Informationen zum Erstellen von Segmenten finden Sie im [Tutorial zum Erstellen von Segmenten](./create-a-segment.md).

## Anhang

Zusätzlich zur Verwendung importierter externer Zielgruppen-Metadaten und deren Verwendung zum Erstellen von Segmenten können Sie auch externe Segmentzugehörigkeiten in Platform importieren.

### Einrichten eines externen Zielschemas für die Segmentzugehörigkeit

Um mit dem Erstellen eines Schemas zu beginnen **[!UICONTROL wählen Sie zunächst]** Schemata“ in der linken Navigationsleiste und dann **[!UICONTROL Schema erstellen]** in der oberen rechten Ecke des Arbeitsbereichs Schemata aus. Wählen Sie von hier aus **[!UICONTROL Individuelles XDM-Profil]**.

![Der Bereich „Individuelles XDM-Profil“ ist hervorgehoben.](../images/tutorials/external-audiences/create-schema-profile.png)

Nachdem das Schema erstellt wurde, müssen Sie die Feldergruppe für die Segmentzugehörigkeit als Teil des Schemas hinzufügen. Wählen Sie dazu [!UICONTROL Details zur Segmentzugehörigkeit] und dann [!UICONTROL Feldergruppen hinzufügen] aus.

![Die Feldergruppe „Details der Segmentzugehörigkeit“ ist hervorgehoben.](../images/tutorials/external-audiences/segment-membership-details.png)

Stellen Sie außerdem sicher, dass das Schema für (**[!UICONTROL )]** ist. Dazu müssen Sie ein Feld als primäre Identität markieren.

![Der Umschalter zum Aktivieren des Schemas für das Profil ist im Schema-Editor hervorgehoben.](../images/tutorials/external-audiences/external-segment-profile.png)

### Einrichten des Datensatzes

Nachdem Sie Ihr Schema erstellt haben, müssen Sie einen Datensatz erstellen.

Um einen Datensatz zu erstellen, befolgen Sie die Anweisungen im [Benutzerhandbuch für Datensätze](../../catalog/datasets/user-guide.md#create). Sie sollten der Option **[!UICONTROL Datensatz aus Schema erstellen]** unter Verwendung des zuvor erstellten Schemas folgen.

![Das Schema, das Sie zum Erstellen der Datenbank verwenden, ist hervorgehoben.](../images/tutorials/external-audiences/select-schema.png)

Nachdem Sie den Datensatz erstellt haben, befolgen Sie die Anweisungen im [Benutzerhandbuch zum Datensatz](../../catalog/datasets/user-guide.md#enable-profile), um diesen Datensatz für das Echtzeit-Kundenprofil zu aktivieren.

![Der Umschalter zum Aktivieren des Schemas für das Profil ist im Workflow zum Erstellen von Datensätzen hervorgehoben.](../images/tutorials/external-audiences/dataset-profile.png)

## Einrichten und Importieren von Daten zur externen Zielgruppenzugehörigkeit

Wenn der Datensatz aktiviert ist, können Daten jetzt entweder über die Benutzeroberfläche oder mithilfe der Experience Platform-APIs an Platform gesendet werden. Sie können diese Daten entweder über eine Batch- oder Streaming-Verbindung aufnehmen.

### Aufnehmen von Daten über eine Batch-Verbindung

Um eine Batch-Verbindung zu erstellen, folgen Sie den Anweisungen im generischen [Handbuch zur Benutzeroberfläche für den Upload lokaler Dateien](../../sources/tutorials/ui/create/local-system/local-file-upload.md). Eine vollständige Liste der verfügbaren Quellen, mit denen Sie Daten aufnehmen können, finden Sie unter [Quellen - Übersicht](../../sources/home.md).

### Aufnehmen von Daten über eine Streaming-Verbindung

Um eine Streaming-Verbindung zu erstellen, folgen Sie den Anweisungen entweder im [API-Tutorial](../../sources/tutorials/api/create/streaming/http.md) oder im [UI-Tutorial](../../sources/tutorials/ui/create/streaming/http.md).

Nachdem Sie Ihre Streaming-Verbindung erstellt haben, haben Sie Zugriff auf Ihren eindeutigen Streaming-Endpunkt, an den Sie Ihre Daten senden können. Informationen zum Senden von Daten an diese Endpunkte finden Sie im [Tutorial zum Streaming von Datensatzdaten](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![Der Streaming-Endpunkt für die Streaming-Verbindung wird auf der Seite mit den Quelldetails hervorgehoben.](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Struktur der Segmentzugehörigkeit

Nachdem Sie eine Verbindung erstellt haben, können Sie Ihre Daten jetzt in Platform aufnehmen.

Nachfolgend finden Sie ein Beispiel für die Payload der externen Zielgruppenzugehörigkeit:

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
| `schemaRef` | Das Schema **muss** für die Segmentzugehörigkeitsdaten auf das zuvor erstellte Schema verweisen. |
| `datasetId` | Die Datensatz-ID **muss** verweist für das soeben erstellte Mitgliedschaftsschema auf den zuvor erstellten Datensatz. |
| `xdmEntity._id` | Eine geeignete ID, mit der der Datensatz im Datensatz eindeutig identifiziert wird. |
| `{TENANT_NAME}.identities` | Dieser Abschnitt wird verwendet, um die Feldergruppe der benutzerdefinierten Identitäten mit den zuvor importierten Benutzern zu verbinden. |
| `segmentMembership.{IDENTITY_NAMESPACE}` | Dies ist die Bezeichnung des zuvor erstellten benutzerdefinierten Identity-Namespace. Wenn Sie beispielsweise Ihren Identity-Namespace „externalAudience“ aufrufen, verwenden Sie diesen als Schlüssel des Arrays. |

>[!NOTE]
>
>Standardmäßig werden externe Zielgruppenzugehörigkeiten nach 30 Tagen gelöscht. Um das Löschen zu verhindern und sie länger als 30 Tage aufzubewahren, verwenden Sie bitte das Feld `validUntil` bei der Aufnahme Ihrer Zielgruppendaten. Weiterführende Informationen zu diesem Feld finden Sie im Handbuch zu den Schemafeldgruppen [Details zur Segmentzugehörigkeit](../../xdm/field-groups/profile/segmentation.md).
