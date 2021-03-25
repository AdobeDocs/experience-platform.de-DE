---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Importieren und Verwenden externer Audiencen
description: In diesem Lernprogramm erfahren Sie, wie Sie externe Audiencen mit Adobe Experience Platform verwenden.
topic: Tutorial
translation-type: tm+mt
source-git-commit: 400e4d9007212ed2693d031ae912a4f1cca97c57
workflow-type: tm+mt
source-wordcount: '652'
ht-degree: 9%

---


# Importieren und Verwenden externer Audiencen

Adobe Experience Platform unterstützt die Möglichkeit, externe Audiencen zu importieren, die anschließend als Komponenten für eine neue Segmentdefinition verwendet werden können. In diesem Dokument finden Sie eine Anleitung zum Einrichten der Experience Platform zum Importieren und Verwenden externer Audiencen.

## Erste Schritte

- [Segmentation Service](../home.md): Ermöglicht Ihnen das Erstellen von Zielgruppensegmenten aus Echtzeit-Kundenprofildaten.
- [Echtzeit-Kundenprofil](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [Experience-Datenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert.
- [Datensätze](../../catalog/datasets/overview.md): Das Speicher- und Verwaltungskonstrukt für Datenpersistenz in Experience Platform.
- [Streaming-Erfassung](../../ingestion/streaming-ingestion/overview.md): So erfasst und speichert Experience Platform Daten von client- und serverseitigen Geräten in Echtzeit.

## Erstellen eines Identitäts-Namensraums für die externe Audience

Der erste Schritt zur Verwendung externer Audiencen ist das Erstellen eines Identitäts-Namensraums. Identitäts-Namensraum ermöglichen die Zuordnung von Segmenten, von denen ein Segment stammt.

Um einen Identitäts-Namensraum zu erstellen, befolgen Sie die Anweisungen im [Identitäts-Namensraum-Handbuch](../../identity-service/namespaces.md#manage-namespaces). Fügen Sie beim Erstellen Ihres Identitäts-Namensraums die Quelldetails zum Identitäts-Namensraum hinzu und markieren Sie dessen [!UICONTROL Typ] als **[!UICONTROL Kennung für Nicht-Personen]**.

![](../images/tutorials/external-audiences/identity-namespace-info.png)

## Schema für Segmentmetadaten erstellen

Nachdem Sie einen Identitäts-Namensraum erstellt haben, müssen Sie ein neues Schema für das Segment erstellen, das Sie erstellen möchten.

Um mit dem Erstellen eines Schemas zu beginnen, wählen Sie zunächst **[!UICONTROL Schema]** in der linken Navigationsleiste und dann **[!UICONTROL Schema erstellen]** oben rechts im Arbeitsbereich &quot;Schemas&quot;aus. Wählen Sie **[!UICONTROL Durchsuchen]** aus, um eine vollständige Auswahl der verfügbaren Schema-Typen anzuzeigen.

![](../images/tutorials/external-audiences/create-schema-browse.png)

Da Sie eine Segmentdefinition erstellen, die eine vordefinierte Klasse ist, wählen Sie **[!UICONTROL Vorhandene Klasse verwenden]**. Wählen Sie nun die Klasse **[!UICONTROL Segmentdefinition]**, gefolgt von **[!UICONTROL Klasse zuweisen]**.

![](../images/tutorials/external-audiences/assign-class.png)

Nachdem Ihr Schema erstellt wurde, müssen Sie angeben, welches Feld die Segment-ID enthalten soll. Dieses Feld sollte als primäre Identität markiert und den zuvor erstellten Namensräumen zugewiesen werden.

![](../images/tutorials/external-audiences/mark-primary-identifier.png)

Nachdem Sie das Feld `_id` als primäre Identität markiert haben, wählen Sie den Titel des Schemas aus, gefolgt von dem Umschalter **[!UICONTROL Profil]**. Wählen Sie **[!UICONTROL Aktivieren]**, um das Schema für [!DNL Real-time Customer Profile] zu aktivieren.

![](../images/tutorials/external-audiences/schema-profile.png)

Dieses Schema ist jetzt zum Profil aktiviert, wobei die primäre ID dem von Ihnen erstellten Identitäts-Namensraum zugewiesen ist, der keine Person ist. Dies bedeutet, dass Segmentmetadaten, die mithilfe dieses Schemas in die Plattform importiert wurden, in Profil eingebunden werden, ohne mit anderen personenbezogenen Profil-Daten zusammengeführt zu werden.

## Datensatz für das Schema erstellen

Nach der Konfiguration des Schemas müssen Sie einen Datensatz für die Segmentmetadaten erstellen.

Um einen Datensatz zu erstellen, befolgen Sie die Anweisungen im [Dataset-Benutzerhandbuch](../../catalog/datasets/user-guide.md#create). Sie möchten die Option **[!UICONTROL Datensatz aus Schema]** erstellen mit dem zuvor erstellten Schema verwenden.

![](../images/tutorials/external-audiences/select-schema.png)

Nachdem Sie den Datensatz erstellt haben, befolgen Sie die Anweisungen im [Dataset-Benutzerhandbuch](../../catalog/datasets/user-guide.md#enable-profile), um diesen Datensatz für Echtzeit-Kundendaten zu aktivieren.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Audiencen einrichten und importieren

Wenn der Datensatz aktiviert ist, können Daten jetzt entweder über die Benutzeroberfläche oder mithilfe der Experience Platform-APIs an die Plattform gesendet werden. Um diese Daten in Platform zu erfassen, müssen Sie eine Streaming-Verbindung erstellen.

Um eine Streaming-Verbindung zu erstellen, befolgen Sie die Anweisungen entweder im [API-Tutorial](../../sources/tutorials/api/create/streaming/http.md) oder im [UI-Tutorial](../../sources/tutorials/ui/create/streaming/http.md).

Nachdem Sie Ihre Streaming-Verbindung erstellt haben, haben Sie Zugriff auf Ihren eindeutigen Streaming-Endpunkt, an den Sie Ihre Daten senden können. Informationen zum Senden von Daten an diese Endpunkte finden Sie im [Tutorial zum Streaming von Datensatzdaten](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Erstellen von Segmenten mit importierten Audiencen

Nachdem die importierten Audiencen eingerichtet wurden, können sie als Teil des Segmentierungsprozesses verwendet werden. Um externe Audiencen zu suchen, gehen Sie zum Segmentaufbau und wählen Sie im Abschnitt **[!UICONTROL Audiencen]** die Registerkarte ****.

![](../images/tutorials/external-audiences/external-audiences.png)

## Nächste Schritte

Da Sie jetzt externe Audiencen in Ihren Segmenten verwenden können, können Sie mit dem Segmentaufbau Segmente erstellen. Informationen zum Erstellen von Segmenten finden Sie im [Lernprogramm zum Erstellen von Segmenten](./create-a-segment.md).