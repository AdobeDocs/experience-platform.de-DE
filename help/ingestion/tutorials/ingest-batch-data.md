---
keywords: Experience Platform; Startseite; beliebte Themen; Erfassung; Erfassen von Batch-Daten; Tutorial; Batch-Erfassung; Tutorial; UI-Handbuch
solution: Experience Platform
title: Daten in Experience Platform erfassen
type: Tutorial
description: Mit Adobe Experience Platform können Sie Daten einfach als Batch-Dateien in Form von Parquet-Dateien oder Daten importieren, die einem bekannten Experience-Datenmodell (XDM)-Schema entsprechen.
exl-id: a4a7358d-b117-4d81-8cb0-3dbbfeccdcbd
source-git-commit: 8351f6907a0dc4a4bba01c7f6e9dec7c376c8575
workflow-type: tm+mt
source-wordcount: '1321'
ht-degree: 51%

---

# Daten in Adobe Experience Platform erfassen

Mit Adobe Experience Platform können Sie Daten einfach als Batch-Dateien in [!DNL Platform] importieren. Beispiele für zu erfassende Daten sind Profildaten aus einer reduzierten Datei in einem CRM-System (z. B. eine Parquet-Datei) oder Daten, die einem bekannten XDM-Schema (0) in der Schema Registry entsprechen.[!DNL Experience Data Model]

## Erste Schritte

Um dieses Tutorial abzuschließen, müssen Sie Zugriff auf [!DNL Experience Platform] haben. Wenn Sie keinen Zugriff auf eine Organisation in [!DNL Experience Platform] haben, wenden Sie sich an Ihren Systemadministrator, bevor Sie fortfahren.

Wenn Sie Daten lieber mit Data Ingestion-APIs erfassen möchten, lesen Sie zunächst das [Entwicklerhandbuch zur Batch-Erfassung](../batch-ingestion/api-overview.md).

## Arbeitsbereich „Datensätze“

Im Arbeitsbereich &quot;Datensätze&quot;von [!DNL Experience Platform] können Sie alle Datensätze, die Ihr Unternehmen erstellt hat, anzeigen und verwalten sowie neue Datensätze erstellen.

Zeigen Sie den Arbeitsbereich „Datensätze“ an, indem Sie im Navigationsbereich auf der linken Seite auf **[!UICONTROL Datensätze]** klicken. Der Arbeitsbereich &quot;Datensätze&quot;enthält eine Liste von Datensätzen, einschließlich der Spalten mit dem Namen, der erstellten Erstellung (Datum und Uhrzeit), der Quelle, dem Schema und dem Status des letzten Batches sowie dem Datum und der Uhrzeit der letzten Aktualisierung des Datensatzes.

>[!NOTE]
>
>Klicken Sie auf das Filtersymbol neben der Suchleiste, um Filterfunktionen zu verwenden und nur die für [!DNL Profile] aktivierten Datensätze anzuzeigen.

![Alle Datensätze anzeigen](../images/tutorials/ingest-batch-data/datasets-overview.png)

## Erstellen eines Datensatzes

Um einen Datensatz zu erstellen, klicken Sie in der oberen rechten Ecke des Arbeitsbereichs „Datensätze“ auf **[!UICONTROL Datensatz erstellen]**.

![](../images/tutorials/ingest-batch-data/click-create-datasets.png)

Wählen Sie im Bildschirm &quot;**[!UICONTROL Datensatz erstellen]**&quot;aus, ob Sie &quot;[!UICONTROL Datensatz aus Schema erstellen]&quot;oder &quot;[!UICONTROL Datensatz aus CSV-Datei erstellen]&quot;verwenden möchten.

In dieser Anleitung verwenden wir zum Erstellen des Datensatzes ein Schema. Klicken Sie auf **[!UICONTROL Datensatz aus Schema erstellen]**, um fortzufahren.

![Datenquelle auswählen](../images/tutorials/ingest-batch-data/create-dataset.png)

## Datensatzschema auswählen

Wählen Sie im Bildschirm **[!UICONTROL Schema auswählen]** ein Schema aus, indem Sie auf das Optionsfeld neben dem Schema klicken, das Sie nutzen möchten. In dieser Anleitung wird der Datensatz mithilfe des Schemas „Mitglieder des Treueprogramms“ erstellt. Die Verwendung der Suchleiste zum Filtern von Schemata ist eine hilfreich, um genau das Schema zu finden, nach dem Sie suchen.

Nachdem Sie das Optionsfeld neben dem Schema ausgewählt haben, das Sie verwenden möchten, klicken Sie auf **[!UICONTROL Weiter]**.

![Schema auswählen](../images/tutorials/ingest-batch-data/select-schema.png)

## Datensatz konfigurieren

Im Bildschirm **[!UICONTROL Datensatz konfigurieren]** müssen Sie Ihrem Datensatz einen Namen geben und möglicherweise auch eine Beschreibung des Datensatzes angeben.

**Hinweise zu Datensatznamen:**

- Datensatznamen sollten kurz und beschreibend sein, damit sich der Datensatz in der Bibliothek später leicht finden lässt.
- Datensatznamen müssen eindeutig sein, d. h. sie müssen spezifisch genug sein, damit sie in Zukunft nicht wiederverwendet werden.
- Es empfiehlt sich, mithilfe des Beschreibungsfelds zusätzliche Informationen zum Datensatz anzugeben, um anderen Benutzern in Zukunft dabei zu helfen, zwischen Datensätzen zu unterscheiden.

Sobald der Datensatz einen Namen und eine Beschreibung aufweist, klicken Sie auf **[!UICONTROL Fertig stellen]**.

![Datensatz konfigurieren](../images/tutorials/ingest-batch-data/configure-dataset.png)

## Datensatzaktivität

Es wurde nun ein leerer Datensatz erstellt und Sie befinden sich wieder auf der Registerkarte **[!UICONTROL Datensatzaktivität]** im Arbeitsbereich „Datensätze“. Sie sollten oben links im Arbeitsbereich den Namen des Datensatzes sowie eine Benachrichtigung sehen, die Ihnen mitteilt, dass keine Batches hinzugefügt wurden. Das ist zu erwarten, da Sie dem Datensatz noch keine Batches hinzugefügt haben.

Auf der rechten Seite des Arbeitsbereichs &quot;Datensätze&quot;wird die Registerkarte &quot;**[!UICONTROL Info]**&quot;mit Informationen zu Ihrem neuen Datensatz angezeigt, z. B. Datensatz-ID, Name, Beschreibung, Tabellenname, Schema, Streaming und Quelle. Die Registerkarte &quot;Info&quot;enthält auch Informationen zum Zeitpunkt der Erstellung des Datensatzes und zum Datum der letzten Änderung.

Auf der Registerkarte &quot;Info&quot;befindet sich außerdem ein Umschalter **[!UICONTROL Profil]** , mit dem Sie Ihren Datensatz zur Verwendung mit [!DNL Real-Time Customer Profile] aktivieren können. Die Verwendung dieses Umschalters und [!DNL Real-Time Customer Profile] wird im folgenden Abschnitt ausführlicher erläutert.

![Datensatzaktivität](../images/tutorials/ingest-batch-data/sample-dataset.png)

## Datensatz für [!DNL Real-Time Customer Profile] aktivieren

Datensätze werden für die Aufnahme von Daten in [!DNL Experience Platform] verwendet, und diese Daten werden letztendlich verwendet, um Einzelpersonen zu identifizieren und Informationen aus mehreren Quellen zusammenzuführen. Diese zusammengeführten Informationen werden als [!DNL Real-Time Customer Profile] bezeichnet. Damit [!DNL Platform] weiß, welche Informationen in [!DNL Real-Time Profile] enthalten sein sollen, können Datensätze mit dem Umschalter **[!UICONTROL Profil]** zur Aufnahme markiert werden.

Standardmäßig ist der Umschalter deaktiviert. Wenn Sie [!DNL Profile] aktivieren, werden alle im Datensatz erfassten Daten verwendet, um eine Person zu identifizieren und ihre [!DNL Real-Time Profile] zuzuordnen.

Weitere Informationen zu [!DNL Real-Time Customer Profile] und zum Arbeiten mit Identitäten finden Sie in der Dokumentation zum [Identitätsdienst](../../identity-service/home.md) .

Um den Datensatz für [!DNL Real-Time Customer Profile] zu aktivieren, klicken Sie auf den Umschalter **[!UICONTROL Profil]** auf der Registerkarte **[!UICONTROL Info]** .

![Profil-Umschalter](../images/tutorials/ingest-batch-data/dataset-profile-toggle.png)

Es wird ein Dialogfeld angezeigt, in dem Sie aufgefordert werden zu bestätigen, dass Sie den Datensatz für [!DNL Real-Time Customer Profile] aktivieren möchten.

![Dialog „Profil aktivieren“](../images/tutorials/ingest-batch-data/enable-dataset-for-profile.png)

Klicken Sie auf **[!UICONTROL Aktivieren]**; daraufhin wird der Umschalter blau und zeigt an, dass das Profil aktiviert ist.

![Für Profil aktiviert](../images/tutorials/ingest-batch-data/profile-enabled-dataset.png)

## Daten in Datensatz hinzufügen

Daten können auf verschiedene Weise in einen Datensatz eingefügt werden. Sie können [!DNL Data Ingestion] APIs oder einen ETL-Partner wie [!DNL Unifi] oder [!DNL Informatica] verwenden. In dieser Anleitung werden dem Datensatz Daten in der Benutzeroberfläche über die Registerkarte **[!UICONTROL Daten hinzufügen]** hinzugefügt.

Um Daten zum Datensatz hinzuzufügen, klicken Sie auf die Registerkarte **[!UICONTROL Daten hinzufügen]**. Jetzt können Sie Dateien per Drag-and-Drop verschieben oder auf Ihrem Computer nach Dateien suchen, die Sie hinzufügen möchten.

>[!NOTE]
>
>Platform unterstützt zwei Dateitypen für die Datenerfassung: Parquet oder JSON. Sie können bis zu fünf Dateien gleichzeitig hinzufügen, wobei die maximale Dateigröße 1 GB pro Datei beträgt.

![Registerkarte „Daten hinzufügen“](../images/tutorials/ingest-batch-data/drag-and-drop.png)

## Datei hochladen {#upload-file}

Nachdem Sie eine Parquet- oder JSON-Datei, die Sie hochladen möchten, per Drag-and-Drop (oder durch Durchsuchen und Auswählen) abgelegt haben, beginnt [!DNL Platform] sofort mit der Verarbeitung der Datei, und auf der Registerkarte **[!UICONTROL Daten hinzufügen]** wird ein Dialogfeld **[!UICONTROL Hochladen]** angezeigt, in dem der Fortschritt des Datei-Uploads angezeigt wird.

![Dialog „Upload läuft“](../images/tutorials/ingest-batch-data/uploading-file.png)

## Datensatzmetriken

Nach dem Hochladen der Datei steht auf der Registerkarte **[!UICONTROL Datensatzaktivität]** nicht mehr, dass keine Batches hinzugefügt wurden. Stattdessen werden auf der Registerkarte **[!UICONTROL Datensatzaktivität]** jetzt Datensatzmetriken angezeigt. Bei allen Metriken wird zu diesem Zeitpunkt „0“ angezeigt, da der Batch noch nicht geladen wurde.

Am unteren Rand der Registerkarte befindet sich eine Liste, in der die **[!UICONTROL Batch-Kennung]** der Daten angezeigt wird, die gerade mit dem Prozess [Daten zu Datensatz hinzufügen](#add-data-to-dataset) erfasst wurden. Dazu gehören auch Informationen zum Batch, einschließlich des erfassten Datums, der Anzahl der aufgenommenen Datensätze und des aktuellen Batch-Status.

![Datensatzmetriken](../images/tutorials/ingest-batch-data/batch-id.png)

## Batch-Details

Klicken Sie auf die **[!UICONTROL Batch-Kennung]**, um eine **[!UICONTROL Batch-Übersicht]** mit weiteren Details zum Batch anzuzeigen. Sobald der Batch geladen wurde, werden die Informationen zum Batch aktualisiert, um die Anzahl der aufgenommenen Datensätze und die Dateigröße anzuzeigen. Der Status ändert sich auch in &quot;Erfolg&quot;oder &quot;Fehlgeschlagen&quot;. Wenn der Batch fehlschlägt, enthält der Abschnitt **[!UICONTROL Fehler-Code]** Details zu Fehlern, die bei der Erfassung aufgetreten sind.

Weiterführende Informationen und häufig gestellte Fragen zur Batch-Erfassung finden Sie im [Handbuch zur Fehlerbehebung bei der Batch-Erfassung](../batch-ingestion/troubleshooting.md).

Um zum Bildschirm **[!UICONTROL Datensatzaktivität]** zurückzukehren, klicken Sie im Breadcrumb auf den Namen des Datensatzes (**[!UICONTROL Details zum Treueprogramm]**).

![Batch-Übersicht](../images/tutorials/ingest-batch-data/batch-details.png)

## Vorschau von Datensatz anzeigen

Sobald der Datensatz bereit ist, wird oben auf der Registerkarte **[!UICONTROL Datensatzaktivität]** eine Option zur **[!UICONTROL Vorschau des Datensatzes]** angezeigt.

Klicken Sie auf **[!UICONTROL Vorschau von Datensatz anzeigen]**, um einen Dialog mit Beispieldaten aus dem Datensatz zu öffnen. Wenn der Datensatz mit einem Schema erstellt wurde, werden auf der linken Seite der Vorschau Details zum Datensatzschema angezeigt. Sie können das Schema mithilfe der Pfeile erweitern, um die Schemastruktur anzuzeigen. Jede Spaltenüberschrift in den Vorschaudaten repräsentiert ein Feld im Datensatz.

![Datensatzdetails](../images/tutorials/ingest-batch-data/dataset-preview.png)

## Nächste Schritte und zusätzliche Ressourcen

Nachdem Sie einen Datensatz erstellt und erfolgreich Daten in [!DNL Experience Platform] erfasst haben, können Sie diese Schritte wiederholen, um einen neuen Datensatz zu erstellen oder mehr Daten in den vorhandenen Datensatz aufzunehmen.

Weiterführende Informationen zur Batch-Erfassung finden Sie in der [Batch-Erfassung - Übersicht](../batch-ingestion/overview.md) . Ergänzend dazu erhalten Sie Informationen, indem Sie sich das folgende Video ansehen.

>[!WARNING]
>
>Die im folgenden Video angezeigte [!DNL Platform]-Benutzeroberfläche ist veraltet. Die neuesten Screenshots und Funktionen der Benutzeroberfläche finden Sie in der obigen Dokumentation.

>[!VIDEO](https://video.tv.adobe.com/v/27269?quality=12&learn=on)
