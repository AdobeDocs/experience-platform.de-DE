---
keywords: Experience Platform;Startseite;beliebte Themen;CJA;Journey Analytics;Customer Journey Analytics;Kampagnenorchestrierung;Orchestrierung;Customer Journey;Journey;Journey Orchestration;Möglichkeiten;Region
title: Beispiel für einen End-to-End-Workflow von Adobe Experience Platform
description: Lernen Sie den grundlegenden End-to-End-Workflow für Adobe Experience Platform auf einer allgemeinen Ebene kennen.
exl-id: 0a4d3b68-05a5-43ef-bf0d-5738a148aa77
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1859'
ht-degree: 11%

---

# Beispiel für einen End-to-End-Workflow von Adobe Experience Platform

Adobe Experience Platform ist eines der leistungsfähigsten, flexibelsten und offensten auf dem Markt verfügbaren Systeme für die Einrichtung und Verwaltung umfassender Lösungen zur Umsetzung starker Kundenerlebnisse. Mit Adobe Experience Platform können Unternehmen Kundendaten und Content aus beliebigen Systemen zentral zusammenführen und standardisieren sowie mithilfe von Datenwissenschaft und maschinellem Lernen die Gestaltung und Bereitstellung umfassender, personalisierter Erlebnisse erheblich verbessern.

Experience Platform stellt Entwicklern auf der Grundlage von RESTful-APIs die volle Funktionalität des Systems zur Verfügung und erleichtert so die Integration von Unternehmenslösungen mit bekannten Tools. Mit Experience Platform können Sie eine ganzheitliche Sicht auf Ihre Kundinnen und Kunden ableiten, indem Sie Ihre Kundendaten erfassen, Ihre Daten auf die Zielgruppen segmentieren, die Sie ansprechen möchten, und diese Zielgruppen für ein externes Ziel aktivieren. Das folgende Tutorial zeigt einen End-to-End-Workflow, der alle Schritte von der Aufnahme über Quellen bis zur Zielgruppenaktivierung über Ziele zeigt.

End-to-End-Workflow von ![Experience Platform](./images/end-to-end-tutorial/platform-end-2-end-workflow.png)

## Erste Schritte

Dieser End-to-End-Workflow nutzt mehrere Adobe Experience Platform-Services. Im Folgenden finden Sie eine Liste der in diesem Workflow verwendeten Services mit Links zu ihren Übersichten:

- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): Das standardisierte Framework, mit dem Kundenerlebnisdaten durch [!DNL Experience Platform] organisiert werden. Um die Segmentierung optimal zu nutzen, stellen Sie sicher, dass Ihre Daten als Profile und Ereignisse gemäß den [Best Practices für die Datenmodellierung](../xdm/schema/best-practices.md) aufgenommen werden.
- [[!DNL Identity Service]](../identity-service/home.md): Bietet Ihnen einen umfassenden Überblick über Ihre Kunden und deren Verhalten, indem Identitäten geräte- und systemübergreifend zusammengeführt werden.
- [Quellen](../sources/home.md): [!DNL Experience Platform] ermöglicht die Aufnahme von Daten aus verschiedenen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern.
- [[!DNL Segmentation Service]](../segmentation/home.md): [!DNL Segmentation Service] ermöglicht die Aufteilung der in [!DNL Experience Platform] gespeicherten Daten, die sich auf Einzelanwender (wie Kunden, Interessenten, Benutzer oder Organisationen) beziehen, in kleinere Gruppen.
- [[!DNL Real-Time Customer Profile]](../profile/home.md): Bietet ein einheitliches Echtzeit-Kundenprofil, das auf aggregierten Daten aus verschiedenen Quellen basiert.
- [Datensätze](../catalog/datasets/overview.md): Das Speicher- und Verwaltungskonstrukt für die Datenpersistenz in [!DNL Experience Platform].
- [Ziele](../destinations/home.md): Ziele sind vorgefertigte Integrationen mit häufig verwendeten Programmen, die die nahtlose Aktivierung von Daten aus Experience Platform für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle ermöglichen.

## Erstellen eines XDM-Schemas

Bevor Sie Daten in Experience Platform aufnehmen, müssen Sie zunächst ein XDM-Schema erstellen, um die Struktur dieser Daten zu beschreiben. Wenn Sie Ihre Daten im nächsten Schritt aufnehmen, werden Sie Ihre eingehenden Daten diesem Schema zuordnen. Um zu erfahren, wie Sie ein Beispiel-XDM-Schema erstellen, lesen Sie das Tutorial [Erstellen eines Schemas mithilfe des Schema-Editors](../xdm/tutorials/create-schema-ui.md).

Das obige Tutorial zeigt, wie Sie Identitätsfelder für Ihre Schemata festlegen. Ein Identitätsfeld stellt ein Feld dar, das verwendet werden kann, um eine einzelne Person im Zusammenhang mit einem Datensatz- oder Zeitreihenereignis zu identifizieren. Identitätsfelder sind eine wichtige Komponente bei der Erstellung von Kundenidentitätsdiagrammen in Experience Platform, was sich letztendlich darauf auswirkt, wie das Echtzeit-Kundenprofil unterschiedliche Datenfragmente zusammenführt, um einen vollständigen Überblick über den Kunden zu erhalten. Weitere Informationen zum Anzeigen von Identitätsdiagrammen in Experience Platform finden Sie im Tutorial [Verwenden des Identitätsdiagramm-Viewers](../identity-service/features/identity-graph-viewer.md).

Sie müssen Ihr Schema für die Verwendung im Echtzeit-Kundenprofil aktivieren, damit Kundenprofile anhand der Daten basierend auf Ihrem Schema erstellt werden können. Weitere Informationen finden Sie im Abschnitt [Aktivieren eines Schemas für ](../xdm/ui/resources/schemas.md#profile)) im Handbuch zur Benutzeroberfläche von Schemas .

## Aufnehmen von Daten in Experience Platform

Nachdem Sie ein XDM-Schema erstellt haben, können Sie mit dem Einbringen Ihrer Daten in das System beginnen.

Alle in Experience Platform importierten Daten werden bei der Aufnahme in einzelne Datensätze gespeichert. Ein Datensatz ist eine Sammlung von Datensätzen, die einem bestimmten XDM-Schema zugeordnet sind. Bevor Ihre Daten von [!DNL Real-Time Customer Profile] verwendet werden können, muss der betreffende Datensatz speziell konfiguriert werden. Vollständige Anweisungen zum Aktivieren eines Datensatzes für Profil finden Sie im [Handbuch zur Datensatzbenutzeroberfläche](../catalog/datasets/user-guide.md#enable-profile) und im [Tutorial zur Datensatzkonfigurations-API](../profile/tutorials/dataset-configuration.md). Nachdem der Datensatz konfiguriert wurde, können Sie mit der Aufnahme von Daten in ihn beginnen.

Experience Platform ermöglicht die Aufnahme von Daten aus externen Quellen und bietet Ihnen die Möglichkeit, die eingehenden Daten mithilfe von Experience Platform-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedensten Quellen aufgenommen werden, darunter etwa Adobe-Anwendungen, Cloud-basierte Datenspeicher und Datenbanken. Beispielsweise können Sie Ihre Daten mit [Amazon S3&rbrace; ](../sources/tutorials/api/create/cloud-storage/s3.md). Eine vollständige Liste der verfügbaren Quellen finden Sie in der [Übersicht über Quell-Connectoren](../sources/home.md).

Wenn Sie Amazon S3 als Quell-Connector verwenden, können Sie den Anweisungen im API-Tutorial zum [Erstellen eines Amazon S3-Connectors](../sources/tutorials/api/create/cloud-storage/s3.md) oder im Benutzeroberflächen-Tutorial zum [Erstellen eines Amazon S3-Connectors](../sources/tutorials/ui/create/cloud-storage/s3.md) folgen, um zu erfahren, wie Sie Daten im Connector erstellen, mit ihm verbinden und aufnehmen.

Ausführlichere Anweisungen zu Quell-Connectoren finden Sie in der [Übersicht zu Quell-Connectoren](../sources/home.md). Weitere Informationen zum Flow Service, der API, auf der die Quellen basieren, finden Sie in der [Flow Service-API-Referenz](https://www.adobe.io/experience-platform-apis/references/flow-service/).

Nachdem Ihre Daten über den Quell-Connector in Experience Platform importiert und in Ihrem profilaktivierten Datensatz gespeichert wurden, werden Kundenprofile automatisch auf der Grundlage der Identitätsdaten erstellt, die Sie in Ihrem XDM-Schema konfiguriert haben.

Beim erstmaligen Hochladen von Daten in einen neuen Datensatz oder beim Einrichten eines neuen ETL-Prozesses oder einer neuen Datenquelle wird empfohlen, die Daten sorgfältig zu überprüfen, um sicherzustellen, dass sie korrekt hochgeladen wurden und die generierten Profile die erwarteten Daten enthalten. Weitere Informationen zum Zugriff auf Kundenprofile in der Experience Platform-Benutzeroberfläche finden Sie [ Handbuch zur Benutzeroberfläche des Echtzeit-Kundenprofils](../profile/ui/user-guide.md). Weitere Informationen zum Zugriff auf Profile mithilfe der Echtzeit-Kundenprofil-API finden Sie im Handbuch unter [Verwenden des Entitäten-Endpunkts](../profile/api/entities.md).

## Daten auswerten

Nachdem Sie aus Ihren aufgenommenen Daten erfolgreich Profile generiert haben, können Sie Ihre Daten mithilfe der Segmentierung auswerten. Bei der Segmentierung handelt es sich um den Prozess der Definition spezifischer Attribute oder Verhaltensweisen, die von einer Untergruppe von Personen aus Ihrem Profilspeicher gemeinsam genutzt werden, um eine vermarktbare Personengruppe aus Ihrem Kundenstamm zu unterscheiden. Weitere Informationen zur Segmentierung finden Sie unter [Segmentierungs-Service - Übersicht](../segmentation/home.md).

### Erstellen einer Segmentdefinition

Zunächst müssen Sie eine Segmentdefinition erstellen, um Ihre Kunden zu einem Cluster zusammenzufassen und Ihre Zielgruppe zu erstellen. Eine Segmentdefinition ist eine Sammlung von Regeln, mit denen Sie die Audience definieren können, die Sie ansprechen möchten. Um eine Segmentdefinition zu erstellen, folgen Sie den Anweisungen im Handbuch zur Benutzeroberfläche unter Verwendung des [Segment Builders](../segmentation/ui/segment-builder.md) oder im API-Tutorial [Erstellen eines Segments](../segmentation/tutorials/create-a-segment.md).

Nachdem Sie eine Segmentdefinition erstellt haben, stellen Sie sicher, dass Sie die Segmentdefinitions-ID notieren.

### Auswerten der Segmentdefinition

Nachdem Sie Ihre Segmentdefinition erstellt haben, können Sie entweder einen Segmentauftrag erstellen, um das Segment als einmalige Instanz zu bewerten, oder einen Zeitplan erstellen, um das Segment laufend zu bewerten.

Um eine Segmentdefinition bei Bedarf auszuwerten, können Sie einen Segmentauftrag erstellen. Ein Segmentauftrag ist ein asynchroner Prozess, der ein neues Zielgruppensegment basierend auf der referenzierten Segmentdefinition und den Zusammenführungsrichtlinien erstellt. Eine Zusammenführungsrichtlinie ist ein Regelsatz, mit dem Experience Platform bestimmt, welche Daten zum Erstellen von Kundenprofilen verwendet werden und welche Daten bei Diskrepanzen zwischen Quellen priorisiert werden. Informationen zum Arbeiten mit Zusammenführungsrichtlinien finden Sie im [UI-Handbuch für Zusammenführungsrichtlinien](../profile/merge-policies/ui-guide.md).

Nachdem der Segmentauftrag erstellt und ausgewertet wurde, können Sie Informationen über das Segment abrufen, z. B. die Größe Ihrer Audience oder Fehler, die während der Verarbeitung aufgetreten sein können. Informationen zum Erstellen eines Segmentvorgangs, einschließlich aller Details, die Sie angeben müssen, finden Sie im [Entwicklerhandbuch für Segmentvorgänge](../segmentation/api/segment-jobs.md).

Um eine Segmentdefinition laufend auszuwerten, können Sie einen Zeitplan erstellen und aktivieren. Ein Zeitplan ist ein Tool, mit dem ein Segmentauftrag einmal täglich zu einer bestimmten Zeit automatisch ausgeführt werden kann. Informationen zum Erstellen und Aktivieren eines Zeitplans finden Sie in den Anweisungen im API-Handbuch [ Endpunkt „Zeitpläne](../segmentation/api/schedules.md).

## Exportieren der ausgewerteten Daten

Nach der Erstellung Ihres einmaligen Segmentauftrags oder Ihres fortlaufenden Zeitplans können Sie entweder einen Segmentexportauftrag erstellen, um die Ergebnisse in einen Datensatz zu exportieren, oder die Ergebnisse an ein Ziel exportieren. Die folgenden Abschnitte enthalten Anleitungen zu diesen beiden Optionen.

### Exportieren der ausgewerteten Daten in einen Datensatz

Nach der Erstellung Ihres einmaligen Segmentauftrags oder Ihres fortlaufenden Zeitplans können Sie die Ergebnisse exportieren, indem Sie einen Segmentexportauftrag erstellen. Ein Segmentexportvorgang ist eine asynchrone Aufgabe, die Informationen zur ausgewerteten Zielgruppe an einen Datensatz sendet.

Bevor Sie einen Exportvorgang erstellen können, müssen Sie zunächst einen Datensatz erstellen, in den die Daten exportiert werden sollen. Um zu erfahren, wie Sie einen Datensatz erstellen, lesen Sie bitte den Abschnitt zum [ eines Zieldatensatzes ](../segmentation/tutorials/evaluate-a-segment.md#create-dataset) Tutorial zum Auswerten eines Segments, um sicherzustellen, dass Sie die Datensatz-ID nach der Erstellung notieren. Nachdem Sie einen Datensatz erstellt haben, können Sie einen Exportvorgang erstellen. Um zu erfahren, wie Sie einen Exportvorgang erstellen, folgen Sie den Anweisungen im API-Handbuch für den Endpunkt [Exportvorgänge](../segmentation/api/export-jobs.md).

### Exportieren der ausgewerteten Daten in ein Ziel

Alternativ können Sie nach der Erstellung Ihres einmaligen Segmentauftrags oder Ihres fortlaufenden Zeitplans die Ergebnisse in ein Ziel exportieren. Ein Ziel ist ein Endpunkt, z. B. eine Adobe-Anwendung auf einem externen Service, über den eine Zielgruppe aktiviert und bereitgestellt werden kann. Eine vollständige Liste der verfügbaren Ziele finden Sie im [Zielkatalog](../destinations/catalog/overview.md).

Anweisungen zum Aktivieren von Daten für Batch- oder E-Mail-Marketing-Ziele finden Sie im Tutorial [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele mithilfe der Experience Platform-Benutzeroberfläche](../destinations/ui/activate-batch-profile-destinations.md) und im [Handbuch zum Verbinden mit Batch-Zielen und Aktivieren von Daten mithilfe der Flow Service-API](../destinations/api/connect-activate-batch-destinations.md).

## Überwachen von Experience Platform-Datenaktivitäten

Mit Experience Platform können Sie verfolgen, wie Daten mithilfe von Datenflüssen verarbeitet werden. Dabei handelt es sich um Aufträge, mit denen Daten über die verschiedenen Komponenten von Experience Platform hinweg verschoben werden. Diese Datenflüsse werden über verschiedene Services konfiguriert und unterstützen Sie dabei, Daten von den Quell-Connectoren in Zieldatensätze zu verschieben, wo sie dann von [!DNL Identity Service] und [!DNL Real-Time Customer Profile] verwendet werden, bevor sie schließlich für Ziele aktiviert werden. Das Monitoring-Dashboard bietet eine visuelle Darstellung der Journey eines Datenflusses. Informationen zum Überwachen von Datenflüssen in der Experience Platform-Benutzeroberfläche finden Sie in den Tutorials [Überwachen von Datenflüssen für ](../dataflows/ui/monitor-sources.md) und [Überwachen von Datenflüssen für Ziele](../dataflows/ui/monitor-destinations.md).

Sie können Experience Platform-Aktivitäten auch mithilfe von statistischen Metriken und Ereignisbenachrichtigungen überwachen, indem Sie [!DNL Observability Insights] verwenden. Sie können Warnhinweise über die Experience Platform-Benutzeroberfläche abonnieren oder an einen konfigurierten Webhook senden. Weitere Informationen zum Anzeigen, Aktivieren, Deaktivieren und Abonnieren verfügbarer Warnhinweise über die Experience Platform-Benutzeroberfläche finden Sie im Handbuch [[!UICONTROL Warnhinweise]-Benutzeroberfläche](../observability/alerts/ui.md). Weitere Informationen zum Empfang von Warnhinweisen über Webhooks finden Sie im Handbuch [Abonnieren von Adobe I/O-Ereignisbenachrichtigungen](../observability/alerts/subscribe.md).

## Nächste Schritte

Durch das Lesen dieses Tutorials erhielten Sie eine grundlegende Einführung in einen einfachen End-to-End-Ablauf für Experience Platform. Weitere Informationen zu Adobe Experience Platform finden Sie in der [Übersicht über Experience Platform](./home.md). Weitere Informationen zur Verwendung der Experience Platform-Benutzeroberfläche und der Experience Platform-API finden Sie im [Handbuch zur Experience Platform-Benutzeroberfläche](./ui-guide.md) bzw. im [Handbuch zur Experience Platform](./api-guide.md)API.
