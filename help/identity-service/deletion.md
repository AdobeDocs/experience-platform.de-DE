---
title: Löschungen in Identity Service
description: Dieses Dokument bietet einen Überblick über die verschiedenen Mechanismen, mit denen Sie Ihre Identitätsdaten in Experience Platform löschen und Klarheit darüber schaffen können, wie sich dies auf Identitätsdiagramme auswirken kann.
source-git-commit: da1ce4560d28d43db47318883f9656cebb2eb487
workflow-type: ht
source-wordcount: '1207'
ht-degree: 100%

---

# Löschungen in Identity Service

Adobe Experience Platform Identity Service generiert Identitätsdiagramme, indem Identitäten für eine Person über Geräte und Systeme hinweg deterministisch miteinander verknüpft werden. Identitätsdiagramm-Verknüpfungen werden eingerichtet, wenn innerhalb derselben Datenzeile zwei oder mehr markierte Identitäten empfangen werden.

Identitätsdiagramme werden vom Echtzeit-Kundenprofil genutzt, um eine umfassende und einzigartige Sicht auf Kundenattribute und -verhalten zu erhalten, sodass Sie eindrucksvolle, persönliche digitale Erlebnisse in Echtzeit für Personen und nicht für Geräte bereitstellen können.

Dieses Dokument bietet einen Überblick über die verschiedenen Mechanismen, mit denen Sie Ihre Identitätsdaten in Experience Platform löschen und Klarheit darüber schaffen können, wie sich dies auf Identitätsdiagramme auswirken kann.

## Erste Schritte

Das nachstehende Dokument verweist auf die folgenden Funktionen von Experience Platform:

* [Identity Service](home.md): Verschaffen Sie sich einen besseren Überblick über einzelne Kundinnen und Kunden und deren Verhalten, indem Sie Identitäten geräte- und systemübergreifend verknüpfen.
   * [Identitätsdiagramm](./ui/identity-graph-viewer.md): In einem Identitätsdiagramm werden die Beziehungen zwischen den verschiedenen Identitäten einer Kundin oder eines Kunden zusammengefasst. Dort wird visuell veranschaulicht, wie die Kundin oder der Kunde auf unterschiedlichen Kanälen mit Ihrer Marke interagiert.
   * [Identity-Namespaces](namespaces.md): Identity-Namespaces sind eine Komponente von Identity Service, die als Indikatoren für den Kontext dienen, auf den sich eine Identität bezieht. Sie unterscheiden beispielsweise den Wert von „name<span>@email.com“ als E-Mail-Adresse oder „443522“ als numerische CRM-ID.
* [Katalog-Service](../catalog/home.md): Informieren Sie sich über Datenherkunft, Metadaten, Dateibeschreibungen, Verzeichnisse und Datensätze im Data Lake.
* [Datenhygiene](../hygiene/home.md): Verwalten Sie Ihre gespeicherten Verbraucherdaten, indem Sie einen automatisierten Ablauf von Datensätzen planen oder einzelne Datensätze aus einem Datensatz oder allen Datensätzen löschen.
* [Adobe Experience Platform Privacy Service](../privacy-service/home.md): Verwalten Sie Kundenanfragen für den Zugriff, den Opt-out vom Verkauf oder das Löschen ihrer personenbezogenen Daten in allen Adobe Experience Cloud-Anwendungen.
* [Echtzeit-Kundenprofil](../profile/home.md): Das Echtzeit-Kundenprofli bietet ein einheitliches, kundenspezifisches Profil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.

## Löschen einzelner Identitäten

Anfragen zum Löschen einzelner Identitäten ermöglichen das Löschen einer Identität innerhalb eines Diagramms, sodass Links entfernt werden, die mit einer einzelnen mit einem Identity-Namespace verknüpften Benutzeridentität verbunden sind. Sie können Mechanismen verwenden, die von [Privacy Service](../privacy-service/home.md) für Anwendungsfälle wie Kundenanfragen zum Löschen von Daten und die Einhaltung von Datenschutzbestimmungen, etwa der Datenschutz-Grundverordnung (DSGVO), bereitgestellt werden.

Die folgenden Abschnitte beschreiben die Mechanismen, die Sie für Anfragen zum Löschen einzelner Identitäten in Experience Platform verwenden können.

### Löschen einzelner Identitäten in Privacy Service

Der Privacy Service verarbeitet Anfragen von Kunden hinsichtlich Zugriff auf, Opt-out vom Verkauf oder Löschen ihrer personenbezogenen Daten, wie in Datenschutzvorschriften wie der Datenschutz-Grundverordnung (DSGVO) und dem California Consumer Privacy Act (CCPA) definiert. Mit Privacy Service können Sie Auftragsanfragen über die API oder die Benutzeroberfläche senden. Wenn Experience Platform von Privacy Service eine Löschanfrage erhält, sendet Platform eine Bestätigung an Privacy Service, dass die Anfrage empfangen wurde und die betroffenen Daten zum Löschen markiert wurden. Das Löschen einer einzelnen Identität basiert auf dem angegebenen Namespace- und/oder ID-Wert. Darüber hinaus erfolgt der Löschvorgang für alle mit einer bestimmten Organisation verbundenen Sandboxes. Weiterführende Informationen finden Sie im Handbuch zum [Verarbeiten von Datenschutzanfragen in Identity Service](privacy.md).

Die nachstehende Tabelle enthält eine Aufschlüsselung der Löschvorgänge für einzelne Identitäten in Privacy Service:

| Löschen einer einzelnen Identität | Privacy Service |
| --- | --- |
| Akzeptierte Anwendungsfälle | Nur Datenschutzanfragen (DSGVO, CCPA). |
| Geschätzte Latenz | Tage bis Wochen. |
| Betroffene Services | Durch das Löschen einer einzelnen Identität in Privacy Service können Sie festlegen, ob Daten aus Identity Service, dem Echtzeit-Kundenprofil oder dem Data Lake gelöscht werden sollen. |
| Löschmuster | Löschen einer Identität aus Identity Service. |

{style=&quot;table-layout:auto&quot;}

## Löschen von Datensätzen

Die folgenden Abschnitte beschreiben die Mechanismen, die zum Löschen von Datensätzen und zugehörigen Identitätsverknüpfungen in Experience Platform verwendet werden können.

### Löschen von Datensätzen im Katalog-Service

Sie können den Katalog-Service verwenden, um Anfragen zum Löschen von Datensätzen zu senden. Weiterführende Informationen zum Löschen von Datensätzen mit dem Katalog-Service finden Sie im Handbuch zum [Löschen von Objekten mithilfe der Katalog-Service-API](../catalog/api/delete-object.md). Sie können auch die Platform-Benutzeroberfläche verwenden, um Anfragen zum Löschen von Datensätzen zu senden. Weiterführende Informationen finden Sie im [Benutzerhandbuch zu Datensätzen](../catalog/datasets/user-guide.md#delete-a-dataset).

### Datensatzablauf im Rahmen der Datenhygiene

Der Arbeitsbereich [[!UICONTROL Datenhygiene]](../hygiene/ui/overview.md) in der Adobe Experience Platform-Benutzeroberfläche bietet Ihnen die Möglichkeit, die Gültigkeitsdauer für Datensätze festzulegen. Wenn ein Datensatz sein Ablaufdatum erreicht, starten der Data Lake, der Identity Service und das Echtzeit-Kundenprofil separate Prozesse, um den Inhalt des Datensatzes aus den entsprechenden Services zu entfernen. Weiterführende Informationen finden Sie im Handbuch zum [Verwalten des Datensatzablaufs mithilfe des Arbeitsbereichs für die [!UICONTROL Datenhygiene]](../hygiene/ui/dataset-expiration.md).

Die folgende Tabelle enthält eine Aufschlüsselung der Unterschiede zwischen dem Löschen von Datensätzen im Katalog-Service und im Rahmen der Datenhygiene:

| Löschen von Datensätzen | Katalog-Service | Datenhygiene |
| --- | --- | --- |
| Akzeptierte Anwendungsfälle | Löschen vollständiger Datensätze und ihrer zugehörigen Identitätsdaten in Platform. | Verwaltung der in Experience Platform gespeicherten Daten. |
| Geschätzte Latenz | Tage | Tage |
| Betroffene Services | Beim Löschen von Datensätzen durch den Katalog-Service werden Daten aus dem Identity Service, dem Echtzeit-Kundenprofil und dem Data Lake gelöscht. | Durch das Löschen von Datensätzen im Rahmen der Datenhygiene werden Daten aus dem Identity Service, dem Echtzeit-Kundenprofil und dem Data Lake gelöscht. |
| Löschmuster | Löschen verknüpfter Identitäten aus dem Identity Service, festgelegt von einem bestimmten Datensatz. | Löschen verknüpfter Identitäten aus dem Identity Service, festgelegt von einem bestimmten Datensatz basierend auf dem Ablaufzeitplan. |

{style=&quot;table-layout:auto&quot;}

## Verschiedene Status von Identitätsdiagrammen nach dem Löschen

Alle Löschvorgänge von Identitätsdiagrammen führen dazu, dass Verknüpfungen zwischen zwei oder mehr Identitäten entfernt werden, wie in der Löschanfrage angegeben. Bei Anfragen zum Löschen von Datensätzen werden alle vom angegebenen Datensatz festgelegten Identitätsverknüpfungen entfernt und es können Identitäten aus Diagrammen entfernt werden. Bei Anfragen zum Löschen einzelner Identitäten werden Identitätsverknüpfungen für die angegebene Identität entfernt, sodass der Identitätswert selbst aus allen Identitätsdiagrammen entfernt wird. Identitäten ohne einzelne Verknüpfung mit einer anderen Identität werden nicht in Identity Service gespeichert.

Nachstehend finden Sie einen Überblick über die möglichen Auswirkungen von Löschungen auf den Status von Identitätsdiagrammen.

| Identitätsdiagramm-Status | Beschreibung |
| --- | --- |
| Teilweise Aktualisierung | Ein Diagramm wird teilweise aktualisiert, wenn mindestens zwei Identitäten innerhalb eines Diagramms verknüpft bleiben, nachdem eine Löschanfrage erfolgreich verarbeitet wurde. Nach dem Löschen können die verbleibenden Identitätsverknüpfungen miteinander verbunden bleiben oder je nach gelöschten Identitäten in zwei oder mehr separate Diagramme unterteilt werden. |
| Vollständige Entfernung | Ein Diagramm muss mindestens zwei verknüpfte Identitäten aufweisen, damit es existieren kann. Wenn eine Löschanfrage dazu führt, dass alle vorhandenen Verknüpfungen in einem Diagramm entfernt werden, wird das Diagramm daher vollständig entfernt. |
| Keine Änderung | Ein Diagramm wird nicht beeinflusst, wenn eine bestimmte Löschanfrage Identitäten oder Datensätze enthält, die mit keinem Mitglied des Diagramms verknüpft sind. Außerdem wird ein Diagramm nicht aktualisiert, auch wenn mit der Löschanfrage eine Verknüpfung zwischen einem Datensatz oder einer Identitäts-Datensatz-Kombination entfernt wird, da die Verknüpfung durch eine andere, nicht gelöschte Verknüpfung hergestellt wurde. Wenn also eine Verknüpfung in zwei verschiedenen Datensätzen vorhanden ist, wird das Diagramm nicht aktualisiert, da nur einer der Datensätze entfernt wird. |

{style=&quot;table-layout:auto&quot;}

## Nächste Schritte

In diesem Dokument wurden die verschiedenen Mechanismen behandelt, mit denen Sie Identitäten und Datensätze in Experience Platform löschen können. In diesem Dokument wurde auch erläutert, wie sich das Löschen von Identitäten und Datensätzen auf Identitätsdiagramme auswirken kann. Weiterführende Informationen zu Identity Service finden Sie in der [Übersicht zu Identity Service](home.md).

<!--

You can use [Data hygiene](../hygiene/home.md) for data cleansing, removing anonymous data, or data minimization for the data that you have collected.

### Single identity deletion in the [!UICONTROL Data Hygiene] workspace

The [[!UICONTROL Data Hygiene] workspace](../hygiene/ui/overview.md) in the Platform UI allows you to delete consumer records that are participating in Identity Service and Real-Time Customer Profile. For a comprehensive guide on using the [!UICONTROL Data Hygiene] workspace, see the tutorial on [deleting consumer records](../hygiene/ui/record-delete.md).

The table below provides a breakdown of differences between single identity deletion in Privacy Service and Data hygiene:

| Single identity deletion | Privacy Service | Data hygiene |
| --- | --- | --- |
| Accepted use cases | Data privacy requests (GDPR, CCPA) only. | Management of data stored in Experience Platform. |
| Estimated latency | Days to weeks | Days |
| Services impacted | Single identity deletion in Privacy Service allows you to select whether data will be deleted from Identity Service, Real-Time Customer Profile, or data lake. | Single identity deletion in Data hygiene deletes the selected data across Identity Service, Real-Time Customer Profile, and data lake. |
| Deletion patterns | Delete an identity from Identity Service. | Delete an identity from Identity Service. |

-->