---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Importieren und Verwenden externer Audiencen
description: Folgen Sie diesem Tutorial, um zu erfahren, wie Sie externe Audiencen mit Adobe Experience Platform verwenden können.
topic-legacy: tutorial
exl-id: 56fc8bd3-3e62-4a09-bb9c-6caf0523f3fe
source-git-commit: 8325ae6fd7d0013979e80d56eccd05b6ed6f5108
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 9%

---

# Importieren und Verwenden externer Audiencen

Adobe Experience Platform unterstützt die Möglichkeit, externe Audience zu importieren, die dann als Komponenten für eine neue Segmentdefinition verwendet werden kann. Dieses Dokument enthält ein Tutorial zum Einrichten der Experience Platform zum Importieren und Verwenden externer Audiencen.

## Erste Schritte

Dieses Tutorial erfordert ein Verständnis der verschiedenen [!DNL Adobe Experience Platform] Dienste, die mit der Erstellung von Audiencen-Segmenten verbunden sind. Bevor Sie mit diesem Tutorial beginnen, lesen Sie bitte die Dokumentation für die folgenden Dienste:

- [Segmentation Service](../home.md): Ermöglicht Ihnen das Erstellen von Zielgruppensegmenten aus Echtzeit-Kundenprofildaten.
- [Echtzeit-Kundenprofil](../../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [Experience-Datenmodell (XDM)](../../xdm/home.md): Das standardisierte Framework, mit dem Platform Kundenerlebnisdaten organisiert. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profil und Ereignis gemäß der [Best Practices für die Datenmodellierung](../../xdm/schema/best-practices.md).
- [Datensätze](../../catalog/datasets/overview.md): Das Speicher- und Verwaltungskonstrukt für Datenpersistenz in Experience Platform.
- [Streaming-Erfassung](../../ingestion/streaming-ingestion/overview.md): So integriert und speichert die Experience Platform Daten von Client- und Server-Geräten in Echtzeit.

### Segmentdaten und Segmentmetadaten

Bevor Sie Beginn mit dem Importieren und Verwenden externer Audiencen haben, müssen Sie den Unterschied zwischen Segmentdaten und Segmentmetadaten verstehen.

Segmentdaten beziehen sich auf die Profil, die die Segmentqualifizierungskriterien erfüllen und daher Teil der Audience sind.

Segmentmetadaten sind Informationen über das Segment selbst, die den Namen, die Beschreibung, den Ausdruck (falls zutreffend), das Erstellungsdatum, das letzte Änderungsdatum und eine ID enthalten. Die ID verknüpft die Segmentmetadaten mit den einzelnen Profilen, die die Segmentqualifikation erfüllen und Teil der resultierenden Audience sind.

| Segmentdaten | Segmentmetadaten |
| ------------ | ---------------- |
| Profil, die die Segmentqualifikation erfüllen | Informationen zum Segment selbst |

## Identitäts-Namensraum für externe Audience erstellen

Der erste Schritt zur Verwendung externer Audiencen ist das Erstellen eines Identitäts-Namensraums. Identity-Namensraum ermöglichen die Zuordnung von Segmenten, von denen ein Segment stammt.

Um einen Identitäts-Namensraum zu erstellen, befolgen Sie die Anweisungen in [Identitäts-Namensraum-Handbuch](../../identity-service/namespaces.md#manage-namespaces). Fügen Sie beim Erstellen Ihres Identitäts-Namensraums die Quelldetails zum Identitäts-Namensraum hinzu und markieren Sie dessen  [!UICONTROL Typ] als **[!UICONTROL Personenidentifikator]**.

![](../images/tutorials/external-audiences/identity-namespace-info.png)

## Schema für Segmentmetadaten erstellen

Nach dem Erstellen eines Identitäts-Namensraums müssen Sie ein neues Schema für das Segment erstellen, das Sie erstellen werden.

Um mit der Erstellung eines Schemas zu beginnen, wählen Sie zuerst **[!UICONTROL Schemas]** auf der linken Navigationsleiste, gefolgt von **[!UICONTROL Schema erstellen]** in der oberen rechten Ecke des Schemas-Arbeitsbereichs. Wählen Sie von hier aus **[!UICONTROL Durchsuchen]** um eine vollständige Auswahl der verfügbaren Schema zu erhalten.

![](../images/tutorials/external-audiences/create-schema-browse.png)

Da Sie eine Segmentdefinition erstellen, die eine vordefinierte Klasse ist, wählen Sie **[!UICONTROL Vorhandene Klasse verwenden]**. Wählen Sie nun die **[!UICONTROL Segmentdefinition]** Klasse, gefolgt von **[!UICONTROL Klasse zuweisen]**.

![](../images/tutorials/external-audiences/assign-class.png)

Nachdem Ihr Schema erstellt wurde, müssen Sie angeben, welches Feld die Segment-ID enthalten soll. Dieses Feld sollte als Primäridentität markiert und den zuvor erstellten Namensräumen zugewiesen werden.

![](../images/tutorials/external-audiences/mark-primary-identifier.png)

Nach dem Markieren `_id` als Primäridentität ein, wählen Sie den Titel des Schemas aus, gefolgt von dem mit der Bezeichnung **[!UICONTROL Profil]**. Auswählen **[!UICONTROL Aktivieren]** um das Schema zu aktivieren für [!DNL Real-time Customer Profile].

![](../images/tutorials/external-audiences/schema-profile.png)

Dieses Schema ist nun zum Profil aktiviert, wobei die primäre Identifikation dem von Ihnen erstellten Identitäts-Namensraum zugewiesen ist. Dies bedeutet, dass Segmentmetadaten, die mit diesem Schema in die Plattform importiert werden, in Profil integriert werden, ohne mit anderen personenbezogenen Profil-Daten zusammengeführt zu werden.

## Dataset für das Schema erstellen

Nach der Konfiguration des Schemas müssen Sie ein Dataset für die Segmentmetadaten erstellen.

Um ein Dataset zu erstellen, befolgen Sie die Anweisungen in [DataSet-Benutzerhandbuch](../../catalog/datasets/user-guide.md#create). Sie werden dem **[!UICONTROL Datensatz aus Schema erstellen]** -Option, wobei das zuvor erstellte Schema verwendet wird.

![](../images/tutorials/external-audiences/select-schema.png)

Fahren Sie nach dem Erstellen des Datasets mit den Anweisungen im [DataSet-Benutzerhandbuch](../../catalog/datasets/user-guide.md#enable-profile) , um dieses Dataset für Echtzeit-Kundendaten zu aktivieren.

![](../images/tutorials/external-audiences/dataset-profile.png)

## Audience einrichten und importieren

Wenn das Dataset aktiviert ist, können Daten über die Benutzeroberfläche oder über die Experience Platform-APIs an die Plattform gesendet werden. Um diese Daten in Platform zu erfassen, müssen Sie eine Streaming-Verbindung erstellen.

Um eine Streaming-Verbindung zu erstellen, folgen Sie den Anweisungen in [API-Führung](../../sources/tutorials/api/create/streaming/http.md) oder [UI-Tutorial](../../sources/tutorials/ui/create/streaming/http.md).

Sobald Sie Ihre Streaming-Verbindung erstellt haben, haben Sie Zugriff auf Ihren eindeutigen Streaming-Endpunkt, an den Sie Ihre Daten senden können. Informationen zum Senden von Daten an diese Endpunkte finden Sie im [Tutorial zu Streaming-Datensatzdaten](../../ingestion/tutorials/streaming-record-data.md#ingest-data).

![](../images/tutorials/external-audiences/get-streaming-endpoint.png)

## Segmente mit importierten Audiencen erstellen

Sobald die importierten Audiencen eingerichtet sind, können sie als Teil des Segmentierungsprozesses verwendet werden. Um externe Audiencen zu suchen, navigieren Sie zum Segmentaufbau und wählen Sie die Option **[!UICONTROL Audiencen]** im **[!UICONTROL Felder]** Abschnitt.

![](../images/tutorials/external-audiences/external-audiences.png)

## Nächste Schritte

Da Sie jetzt externe Audiencen in Ihren Segmenten verwenden können, können Sie den Segmentaufbau verwenden, um Segmente zu erstellen. Informationen zum Erstellen von Segmenten finden Sie im [Tutorial zum Erstellen von Segmenten](./create-a-segment.md).
