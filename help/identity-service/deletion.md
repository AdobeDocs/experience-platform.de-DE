---
title: Löschungen im Identity Service
description: Dieses Dokument bietet einen Überblick über die verschiedenen Mechanismen, mit denen Sie Ihre Identitätsdaten in Experience Platform löschen und Klarheit darüber schaffen können, wie sich Identitätsdiagramme auf diese Weise auswirken können.
source-git-commit: da1ce4560d28d43db47318883f9656cebb2eb487
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 13%

---

# Löschungen im Identity Service

Adobe Experience Platform Identity Service generiert Identitätsdiagramme, indem Identitäten für eine Person über Geräte und Systeme hinweg deterministisch miteinander verknüpft werden. Identitätsdiagramm-Verknüpfungen werden eingerichtet, wenn innerhalb derselben Datenzeile zwei oder mehr markierte Identitäten empfangen werden.

Identitätsdiagramme werden vom Echtzeit-Kundenprofil genutzt, um eine umfassende und einzigartige Ansicht Ihrer Kundenattribute und Verhaltensweisen zu erstellen, sodass Sie effektive, persönliche digitale Erlebnisse in Echtzeit für Personen und nicht für Geräte bereitstellen können.

Dieses Dokument bietet einen Überblick über die verschiedenen Mechanismen, mit denen Sie Ihre Identitätsdaten in Experience Platform löschen und Klarheit darüber schaffen können, wie sich Identitätsdiagramme auf diese Weise auswirken können.

## Erste Schritte

Das folgende Dokument verweist auf die folgenden Funktionen von Experience Platform:

* [Identity Service](home.md): Verschaffen Sie sich einen besseren Überblick über einzelne Kunden und deren Verhalten, indem Sie Identitäten geräte- und systemübergreifend verknüpfen.
   * [Identitätsdiagramm](./ui/identity-graph-viewer.md): Ein Identitätsdiagramm ist eine Zusammenstellung der Beziehungen zwischen verschiedenen Identitäten für einen bestimmten Kunden und bietet Ihnen eine visuelle Darstellung, wie Ihr Kunde über verschiedene Kanäle hinweg mit Ihrer Marke interagiert.
   * [Identitäts-Namespaces](namespaces.md): Identitäts-Namespaces sind eine Komponente des Identity Service , die als Indikatoren für den Kontext dient, auf den sich eine Identität bezieht. Sie unterscheiden beispielsweise den Wert von „name<span>@email.com“ als E-Mail-Adresse oder „443522“ als numerische CRM-ID.
* [Catalog Service](../catalog/home.md): Erkunden Sie die Datenherkunft, Metadaten, Dateibeschreibungen, Verzeichnisse und Datensätze im Data Lake.
* [Datenhygiene](../hygiene/home.md): Verwalten Sie Ihre gespeicherten Verbraucherdaten, indem Sie automatisierte Datensatzabläufe planen oder einzelne Datensätze aus einem Datensatz oder allen Datensätzen löschen.
* [Adobe Experience Platform Privacy Service](../privacy-service/home.md): Verwalten Sie Kundenanfragen für den Zugriff auf, die Abmeldung vom Verkauf oder das Löschen ihrer personenbezogenen Daten in allen Adobe Experience Cloud-Anwendungen.
* [Echtzeit-Kundenprofil](../profile/home.md): Bietet ein einheitliches Kundenprofil in Echtzeit, das auf aggregierten Daten aus mehreren Quellen basiert.

## Löschen einzelner Identitäten

Einzelne Identitätslöschanfragen ermöglichen das Löschen einer Identität innerhalb eines Diagramms, sodass Links entfernt werden, die mit einer einzelnen Benutzeridentität verknüpft sind, die mit einem Identitäts-Namespace verknüpft ist. Sie können Mechanismen verwenden, die von [Privacy Service](../privacy-service/home.md) für Anwendungsfälle wie Kundenanfragen zum Löschen von Daten und Einhaltung von Datenschutzbestimmungen wie der Datenschutz-Grundverordnung (DSGVO).

Die folgenden Abschnitte beschreiben die Mechanismen, die Sie für einzelne Identitätslöschanfragen in Experience Platform verwenden können.

### Löschen einer einzelnen Identität in Privacy Service

Der Privacy Service verarbeitet Anfragen von Kunden hinsichtlich Zugriff auf, Opt-out vom Verkauf oder Löschen ihrer personenbezogenen Daten, wie in Datenschutzvorschriften wie der Datenschutz-Grundverordnung (DSGVO) und dem California Consumer Privacy Act (CCPA) definiert. Mit Privacy Service können Sie Auftragsanfragen über die API oder die Benutzeroberfläche senden. Wenn Experience Platform von Privacy Service eine Löschanfrage erhält, sendet Platform eine Bestätigung an Privacy Service, dass die Anfrage empfangen wurde und die betroffenen Daten zum Löschen markiert wurden. Das Löschen einer einzelnen Identität basiert auf dem angegebenen Namespace- und/oder ID-Wert. Darüber hinaus erfolgt der Löschvorgang für alle Sandboxes, die mit einer bestimmten Organisation verbunden sind. Weitere Informationen finden Sie im Handbuch unter [Verarbeitung von Datenschutzanfragen in Identity Service](privacy.md).

Die nachstehende Tabelle enthält eine Aufschlüsselung des einzelnen Identitätslöschens in Privacy Service :

| Löschen einer einzelnen Identität | Privacy Service |
| --- | --- |
| Angenommene Anwendungsfälle | Nur Datenschutzanfragen (DSGVO, CCPA). |
| Geschätzte Latenz | Tage bis Wochen |
| Betroffene Dienste | Durch das Löschen einer einzelnen Identität in Privacy Service können Sie festlegen, ob Daten aus Identity Service, Echtzeit-Kundenprofil oder Data Lake gelöscht werden sollen. |
| Löschmuster | Löschen Sie eine Identität aus Identity Service. |

{style=&quot;table-layout:auto&quot;}

## Löschen von Datensätzen

Die folgenden Abschnitte beschreiben die Mechanismen, die zum Löschen von Datensätzen und zugehörigen Identitätsverknüpfungen in Experience Platform verwendet werden können.

### Löschen von Datensätzen in Catalog Service

Sie können den Catalog Service verwenden, um Anforderungen zum Löschen von Datensätzen zu senden. Weitere Informationen zum Löschen von Datensätzen mit Catalog Service finden Sie im Handbuch unter [Löschen von Objekten mithilfe der Catalog Service-API](../catalog/api/delete-object.md). Alternativ können Sie die Platform-Benutzeroberfläche verwenden, um Anforderungen zum Löschen von Datensätzen zu senden. Weitere Informationen finden Sie im Abschnitt [Benutzerhandbuch zu Datensätzen](../catalog/datasets/user-guide.md#delete-a-dataset).

### Datensatzabläufe in der Datenhygiene

Der Arbeitsbereich [[!UICONTROL Datenhygiene]](../hygiene/ui/overview.md) in der Adobe Experience Platform-Benutzeroberfläche bietet Ihnen die Möglichkeit, die Gültigkeitsdauer für Datensätze festzulegen. Wenn ein Datensatz sein Ablaufdatum erreicht, beginnen der Data Lake, der Identity Service und das Echtzeit-Kundenprofil separate Prozesse, um den Inhalt des Datensatzes aus den entsprechenden Diensten zu entfernen. Weitere Informationen finden Sie im Handbuch unter [Verwalten der Datensatzabläufe mithilfe der Variablen [!UICONTROL Datenhygiene] Arbeitsbereich](../hygiene/ui/dataset-expiration.md).

Die folgende Tabelle enthält eine Aufschlüsselung der Unterschiede zwischen dem Löschen von Datensätzen in Catalog Service und der Datenhygiene:

| Löschen von Datensätzen | Katalog-Service | Datenhygiene |
| --- | --- | --- |
| Angenommene Anwendungsfälle | Löschen Sie vollständige Datensätze und die zugehörigen Identitätsdaten in Platform. | Verwaltung der in Experience Platform gespeicherten Daten. |
| Geschätzte Latenz | Days | Days |
| Betroffene Dienste | Beim Löschen von Datensätzen durch den Katalogdienst werden Daten aus Identity Service, Echtzeit-Kundenprofil und Data Lake gelöscht. | Durch das Löschen von Datensätzen durch Datenhygiene werden Daten aus Identity Service, Echtzeit-Kundenprofil und Data Lake gelöscht. |
| Löschmuster | Löschen Sie verknüpfte Identitäten aus Identity Service, der von einem bestimmten Datensatz erstellt wurde. | Löschen Sie verknüpfte Identitäten aus Identity Service, der von einem bestimmten Datensatz basierend auf dem Ablaufzeitplan eingerichtet wurde. |

{style=&quot;table-layout:auto&quot;}

## Verschiedene Status von Identitätsdiagrammen nach dem Löschen

Alle Löschungen von Identitätsdiagrammen führen dazu, dass Verknüpfungen zwischen zwei oder mehr Identitäten entfernt werden, wie in der Löschanfrage angegeben. Bei Anforderungen zum Löschen von Datensätzen werden alle vom angegebenen Datensatz festgelegten Identitätsverknüpfungen entfernt und können Identitäten aus Diagrammen entfernen. Bei einzelnen Identitätslöschanfragen werden Identitätsverknüpfungen für die angegebene Identität entfernt, sodass der Identitätswert selbst aus allen Identitätsdiagrammen entfernt wird. Identitäten ohne einzelne Verknüpfung mit einer anderen Identität werden nicht im Identity Service gespeichert.

Nachstehend finden Sie einen Überblick über die möglichen Auswirkungen von Löschungen auf den Status von Identitätsdiagrammen.

| Identitätsdiagramm-Status | Beschreibung |
| --- | --- |
| Teilweise aktualisiert | Ein Diagramm wird teilweise aktualisiert, wenn mindestens zwei Identitäten innerhalb eines Diagramms verknüpft bleiben, nachdem eine Löschanfrage erfolgreich verarbeitet wurde. Nach dem Löschen können die verbleibenden Identitätslinks miteinander verbunden bleiben oder je nach gelöschten Identitäten in zwei oder mehr separate Diagramme unterteilt werden. |
| Vollständige Entfernung | Ein Diagramm muss mindestens zwei verknüpfte Identitäten aufweisen, damit es existieren kann. Wenn daher eine Löschanfrage dazu führt, dass alle vorhandenen Links in einem Diagramm entfernt werden, wird das Diagramm vollständig entfernt. |
| Keine Änderung | Ein Diagramm wird nicht beeinflusst, wenn eine bestimmte Löschanfrage eine Identität oder einen Datensatz enthält, die mit keinem Mitglied des Diagramms verknüpft sind. Außerdem wird ein Diagramm nicht aktualisiert, auch wenn mit der Löschanfrage eine Verknüpfung zwischen einem Datensatz oder einer Kombination aus Identitäts-Datensatz entfernt wird, da die Verknüpfung durch eine andere, nicht gelöschte Verknüpfung hergestellt wurde. Wenn also eine Verknüpfung in zwei verschiedenen Datensätzen vorhanden ist, wird das Diagramm nicht aktualisiert, da nur einer der Datensätze entfernt wird. |

{style=&quot;table-layout:auto&quot;}

## Nächste Schritte

In diesem Dokument wurden die verschiedenen Mechanismen behandelt, mit denen Sie Identitäten und Datensätze in Experience Platform löschen können. In diesem Dokument wurde auch erläutert, wie sich das Löschen von Identitäts- und Datensätzen auf Identitätsdiagramme auswirken kann. Weitere Informationen zu Identity Service finden Sie im Abschnitt [Identity Service - Übersicht](home.md).

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