---
title: Anfragen zum Löschen von Datensätzen (UI-Workflow)
description: Erfahren Sie, wie Sie Datensätze in der Adobe Experience Platform-Benutzeroberfläche löschen.
exl-id: 5303905a-9005-483e-9980-f23b3b11b1d9
source-git-commit: 56ae47f511a7392286c4f85173dba30e93fc07d0
workflow-type: tm+mt
source-wordcount: '2520'
ht-degree: 10%

---

# Anfragen zum Löschen von Datensätzen (UI-Workflow) {#record-delete}

Verwenden Sie den [[!UICONTROL Data Lifecycle] Arbeitsbereich](./overview.md) um Datensätze in Adobe Experience Platform basierend auf ihren primären Identitäten zu löschen. Diese Datensätze können mit einzelnen Verbrauchern oder jeder anderen Entität verknüpft werden, die im Identitätsdiagramm enthalten ist.

>[!IMPORTANT]
>
>Löschvorgänge von Datensätzen dienen zur Datenbereinigung, zum Entfernen anonymer Daten oder zur Datenminimierung. Sie dürfen **nicht** für Anfragen zu den Rechten der betroffenen Personen (Compliance) verwendet werden, da sie sich auf Datenschutzbestimmungen wie die Datenschutz-Grundverordnung (DSGVO) beziehen. Verwenden Sie stattdessen [Adobe Experience Platform Privacy Service](../../privacy-service/home.md) für alle Compliance-Anwendungsfälle.

## Voraussetzungen {#prerequisites}

Das Löschen von Datensätzen setzt ein Verständnis der Funktionsweise von Identitätsfeldern in Experience Platform voraus. Insbesondere müssen Sie den primären Identity-Namespace und die Werte für die Entitäten kennen, deren Datensätze Sie löschen möchten. Diese Werte hängen vom Datensatz (oder den Datensätzen) ab, aus dem/denen Sie sie löschen möchten.

Weitere Informationen zu Identitäten in Experience Platform finden Sie in der folgenden Dokumentation:

* [Adobe Experience Platform Identity Service](../../identity-service/home.md): Führt Identitäten zwischen Geräten und Systemen zusammen und verknüpft Datensätze anhand der Identitätsfelder, die von den entsprechenden XDM-Schemata definiert werden.
* [Identity-Namespaces](../../identity-service/features/namespaces.md): In Identity-Namespaces werden die verschiedenen Arten von Identitätsinformationen definiert, die sich auf eine einzelne Person beziehen können. Sie sind eine erforderliche Komponente für jedes Identitätsfeld.
* [Echtzeit-Kundenprofil](../../profile/home.md): Verwendet Identitätsdiagramme, um vereinheitlichte Verbraucherprofile auf der Grundlage aggregierter Daten aus mehreren Quellen bereitzustellen, die nahezu in Echtzeit aktualisiert werden.
* [Experience-Datenmodell (XDM)](../../xdm/home.md): Stellt Standarddefinitionen und -strukturen für Experience Platform-Daten durch die Verwendung von Schemata bereit. Alle Experience Platform-Datensätze entsprechen einem bestimmten XDM-Schema und das Schema definiert, welche Felder Identitäten sind.
* [Identitätsfelder](../../xdm/ui/fields/identity.md): Erfahren Sie, wie ein Identitätsfeld in einem XDM-Schema definiert wird.

>[!IMPORTANT]
>
>Löschvorgänge von Datensätzen beziehen sich ausschließlich auf **Feld &quot;** Identität“, das im Schema des Datensatzes definiert ist. Die folgenden Einschränkungen gelten:
>
>* **Sekundäre Identitäten werden nicht überprüft.** Wenn ein Datensatz mehrere Identitätsfelder enthält, wird nur die primäre Identität für die Zuordnung verwendet. Datensätze können nicht basierend auf nicht primären Identitäten ausgewählt oder gelöscht werden.
>* **Datensätze ohne ausgefüllte primäre Identität werden übersprungen.** Wenn für einen Datensatz keine primären Identitätsmetadaten ausgefüllt sind, kann er nicht gelöscht werden.
>* **Daten, die vor der Identitätskonfiguration aufgenommen wurden, sind nicht zulässig.** Wenn das primäre Identitätsfeld einem Schema nach der Datenaufnahme hinzugefügt wurde, können zuvor aufgenommene Datensätze über diesen Workflow nicht gelöscht werden.

## Erstellen einer Anfrage {#create-request}

Wählen Sie zunächst im linken Navigationsbereich der Benutzeroberfläche von Experience Platform die Option **[!UICONTROL Data Lifecycle]** aus. Der [!UICONTROL Data lifecycle requests] Arbeitsbereich wird angezeigt. Wählen Sie als Nächstes **[!UICONTROL Create request]** auf der Hauptseite im Arbeitsbereich aus.

![Der [!UICONTROL Data lifecycle requests] Arbeitsbereich mit [!UICONTROL Create request] ausgewählten.](../images/ui/record-delete/create-request-button.png)

Der Workflow zur Anfrageerstellung wird angezeigt. Standardmäßig ist die Option **[!UICONTROL Delete record]** im Abschnitt **[!UICONTROL Requested Action]** ausgewählt. Lassen Sie diese Option aktiviert.

>[!IMPORTANT]
> 
>Um die Effizienz zu verbessern und den Datensatzbetrieb kostengünstiger zu gestalten, können Unternehmen, die in das Delta-Format verschoben wurden, Daten aus dem Identity Service, dem Echtzeit-Kundenprofil und dem Data Lake löschen. Dieser Benutzertyp wird als „delta-migriert“ bezeichnet. Benutzer von Organisationen, die in den Delta-Bereich migriert wurden, können Datensätze aus einem oder allen Datensätzen löschen. Benutzer von Organisationen, die keine Delta-Migration durchgeführt haben, können keine Datensätze selektiv aus einem einzelnen Datensatz oder allen Datensätzen löschen, wie in der Abbildung unten dargestellt. Fahren Sie in diesem Fall mit dem Abschnitt [Bereitstellen von ](#provide-identities)&quot; des Handbuchs fort.

![Der Workflow für die Anfrageerstellung mit ausgewählter und hervorgehobener Option &quot;[!UICONTROL Delete record]&quot;.](../images/ui/record-delete/delete-record.png)

## Auswählen von Datensätzen {#select-dataset}

Der nächste Schritt besteht darin festzustellen, ob Sie Datensätze aus einem einzelnen Datensatz oder allen Datensätzen löschen möchten. Abhängig von der Konfiguration Ihres Unternehmens ist die Option zur Datensatzauswahl möglicherweise nicht verfügbar. Wenn diese Option nicht angezeigt wird, fahren Sie mit dem Abschnitt [Identitäten angeben](#provide-identities) des Handbuchs fort.

Wählen Sie im Abschnitt **[!UICONTROL Record Details]** eine Optionsschaltfläche aus, um entweder einen bestimmten Datensatz oder alle Datensätze auszuwählen.

Um aus einem bestimmten Datensatz zu löschen, klicken Sie auf **[!UICONTROL Select dataset]** und wählen dann das Datenbanksymbol (![Datenbanksymbol](/help/images/icons/database.png)). Wählen Sie im angezeigten Dialogfeld einen Datensatz aus und klicken Sie zur Bestätigung auf **[!UICONTROL Done]** .

![Das Dialogfeld &quot;[!UICONTROL Select dataset]&quot; mit ausgewähltem Datensatz und hervorgehobener [!UICONTROL Done].](../images/ui/record-delete/select-dataset.png)

Um aus allen Datensätzen zu löschen, wählen Sie **[!UICONTROL All datasets]** aus. Diese Option vergrößert den Umfang des Vorgangs und erfordert, dass Sie für jeden Datensatz, den Sie ansprechen möchten, den primären Identitätstyp angeben.

![Das Dialogfeld &quot;[!UICONTROL Select dataset]&quot; mit ausgewählter Option &quot;[!UICONTROL All datasets]&quot;.](../images/ui/record-delete/all-datasets.png)

>[!WARNING]
>
>Durch die Auswahl von **[!UICONTROL All datasets]** wird der Vorgang auf alle Datensätze in Ihrer Organisation erweitert. Jeder Datensatz kann einen anderen primären Identitätstyp verwenden. Sie müssen **den primären Identitätstyp für jeden Datensatz) angeben** um eine genaue Übereinstimmung sicherzustellen.
>
>Wenn ein Identitätstyp fehlt, werden beim Löschen möglicherweise einige Datensätze übersprungen. Dies kann die Verarbeitung verlangsamen und zu (**Ergebnissen)**.

Jeder Datensatz in Experience Platform unterstützt nur einen primären Identitätstyp.

* Beim Löschen aus einem **einzelnen Datensatz** müssen alle Identitäten in Ihrer Anfrage den **gleichen Typ** verwenden.
* Beim Löschen aus **allen Datensätzen** können Sie **mehrere Identitätstypen** einbeziehen, da verschiedene Datensätze möglicherweise auf verschiedenen primären Identitäten basieren.“

## Angeben von Identitäten {#provide-identities}

>[!CONTEXTUALHELP]
>id="platform_hygiene_primaryidentity"
>title="Primärer Identity-Namespace"
>abstract="Der primäre Identity-Namespace ist das Attribut, das einen Datensatz eindeutig mit dem Profil eines Verbrauchers in Experience Platform verknüpft. Das Feld für die primäre Identität für einen Datensatz wird durch das Schema definiert, auf dem der Datensatz basiert. In dieser Spalte müssen Sie den primären Identity-Namespace (z. B. `email` für E-Mail-Adressen oder `ecid` für Experience Cloud-IDs) angeben, der dem Schema des Datensatzes entspricht. Weitere Informationen finden Sie im Handbuch zur Datenlebenszyklus-Benutzeroberfläche."

>[!CONTEXTUALHELP]
>id="platform_hygiene_identityvalue"
>title="Primärer Identitätswert"
>abstract="In dieser Spalte müssen Sie den Wert für den Identity-Namespace des Eintrags angeben, der dem in der linken Spalte angegebenen Identitätstyp entsprechen muss. Wenn der Typ des Identity-Namespace `email` ist, sollte der Wert die E-Mail-Adresse des Eintrags sein. Weitere Informationen finden Sie im Handbuch zur Datenlebenszyklus-Benutzeroberfläche."

Beim Löschen von Datensätzen müssen Sie Identitätsinformationen angeben, damit das System bestimmen kann, welche Datensätze gelöscht werden sollen. Für jeden Datensatz in Experience Platform werden Datensätze basierend auf dem Feld **primäre Identität** gelöscht, das durch das Schema des Datensatzes definiert wird.

>[!NOTE]
>
>Obwohl Sie in der Benutzeroberfläche einen Identity-Namespace auswählen können, wird zur Ausführungszeit nur **im Schema** Datensatzes konfigurierte (primäre Identität) verwendet. Stellen Sie sicher, dass die von Ihnen angegebenen Identitätswerte mit dem primären Identitätsfeld des Datensatzes übereinstimmen.

Wie alle Identitätsfelder in Experience Platform besteht eine primäre Identität aus zwei Elementen: einem **type** (dem Identity-Namespace) und einem **value**. Der Identitätstyp liefert den Kontext dazu, wie das Feld einen Datensatz identifiziert (z. B. über eine E-Mail-Adresse). Der Wert stellt die spezifische Identität eines Datensatzes für diesen Typ dar (z. B. `jdoe@example.com` für den `email` Identitätstyp). Zu den gebräuchlichen Feldern, die als primäre Identitäten verwendet werden, gehören Kontoinformationen, Geräte-IDs und Cookie-IDs.

>[!TIP]
>
>Wenn Sie den Identity-Namespace für einen bestimmten Datensatz nicht kennen, können Sie ihn in der Experience Platform-Benutzeroberfläche finden. Wählen Sie dazu im Arbeitsbereich **[!UICONTROL Datasets]** den betreffenden Datensatz aus der Liste aus. Bewegen Sie auf der Detailseite für den Datensatz den Mauszeiger in der rechten Leiste über den Namen des Datensatzschemas. Der Identity-Namespace wird zusammen mit dem Schemanamen und der Beschreibung angezeigt.
>
>![Das Dashboard „Datensätze“, in dem ein Datensatz ausgewählt und ein Schemadialogfeld im Bedienfeld „Datensatzdetails“ geöffnet wurde. Die primäre ID des Datensatzes ist hervorgehoben.](../images/ui/record-delete/dataset-primary-identity.png)

Es gibt zwei Möglichkeiten, beim Löschen von Datensätzen Identitäten bereitzustellen:

* [Hochladen einer JSON-Datei](#upload-json)
* [Manuelle Eingabe primärer Identitätswerte](#manual-identity)

### Hochladen einer JSON-Datei {#upload-json}

Um eine JSON-Datei hochzuladen, können Sie die Datei per Drag-and-Drop in den entsprechenden Bereich ziehen oder **[!UICONTROL Choose files]** auswählen, um die Datei in Ihrem lokalen Verzeichnis zu suchen und auszuwählen.

![Der Workflow für die Anfrageerstellung mit der hervorgehobenen Option „Dateien auswählen“ und der hervorgehobenen Drag-and-Drop-Oberfläche für das Hochladen von JSON-Dateien.](../images/ui/record-delete/upload-json.png)

Die JSON-Datei muss als Array von Objekten formatiert sein, wobei jedes Objekt einen primären Identitätswert für den Zieldatensatz darstellt.

```json
[
  {
    "namespaceCode": "email",
    "value": "jdoe@example.com"
  },
  {
    "namespaceCode": "email",
    "value": "san.gray@example.com"
  }
]
```

| Eigenschaft | Beschreibung |
| --- | --- |
| `namespaceCode` | Der primäre Identity-Namespace für den Zieldatensatz. |
| `value` | Der primäre Identitätswert, wie durch den Typ gekennzeichnet. |

Nach dem Hochladen der Datei können Sie mit dem [Senden der Anfrage](#submit) fortfahren.

### Manuelles Eingeben von Identitäten {#manual-identity}

Um Identitäten manuell einzugeben, wählen Sie **[!UICONTROL Add identity]** aus.

![Der Workflow für die Anfrageerstellung mit hervorgehobener Option &quot;[!UICONTROL Add identity]&quot;.](../images/ui/record-delete/add-identity.png)

Es werden Steuerelemente angezeigt, mit denen Sie Identitäten einzeln eingeben können. Wählen Sie unter **[!UICONTROL identity namespace]** im Dropdown-Menü den Identitätstyp aus. Geben Sie unter **[!UICONTROL Primary Identity Value]** den Identity-Namespace-Wert für den Datensatz an.

![Der Workflow zur Anfrageerstellung mit einem Identitätsfeld wurde manuell hinzugefügt.](../images/ui/record-delete/identity-added.png)

Um weitere Identitäten hinzuzufügen, wählen Sie das Pluszeichen (![ Pluszeichen ) aus.](/help/images/icons/tree-expand-all.png)) neben einer der Zeilen oder wählen Sie **[!UICONTROL Add identity]** aus.

![Der Workflow für die Anfrageerstellung mit dem Pluszeichen und dem hervorgehobenen Symbol „Identität hinzufügen“.](../images/ui/record-delete/more-identities.png)

## Kontingente und Verarbeitungszeitpläne {#quotas}

Anfragen zum Löschen von Datensätzen unterliegen täglichen und monatlichen Obergrenzen für die Übermittlung von Identifikatoren, die durch die Lizenzberechtigung Ihres Unternehmens bestimmt werden. Diese Einschränkungen gelten sowohl für benutzeroberflächen- als auch für API-basierte Löschanfragen.

>[!NOTE]
>
>Sie können bis zu **1.000.000 Kennungen pro Tag**, jedoch nur, wenn Ihr restliches monatliches Kontingent dies zulässt. Wenn Ihre monatliche Obergrenze weniger als 1 Million beträgt, können Ihre täglichen Einreichungen diese Obergrenze nicht überschreiten.

### Berechtigung zur monatlichen Übermittlung nach Produkt {#quota-limits}

In der folgenden Tabelle sind die Beschränkungen für die Übermittlung von Kennungen nach Produkt und Berechtigungsebene aufgeführt. Für jedes Produkt ist die monatliche Obergrenze der niedrigere von zwei Werten: eine feste Kennungsobergrenze oder ein prozentualer Schwellenwert, der an Ihr lizenziertes Datenvolumen gebunden ist.

| Produkt | Beschreibung der Berechtigung | Monatliche Obergrenze (je nachdem, welcher Wert niedriger ist) |
|----------|-------------------------|---------------------------------|
| Real-Time CDP oder Adobe Journey Optimizer | Ohne Privacy and Security Shield oder Healthcare Shield-Add-on | 2.000.000 Kennungen oder 5 % der adressierbaren Zielgruppe |
| Real-Time CDP oder Adobe Journey Optimizer | Mit dem Add-on Privacy and Security Shield oder Healthcare Shield | 15.000.000 Kennungen oder 10 % der adressierbaren Zielgruppe |
| Customer Journey Analytics | Ohne Privacy and Security Shield oder Healthcare Shield-Add-on | 2.000.000 Kennungen oder 100 Kennungen pro Million CJA-Berechtigungszeilen |
| Customer Journey Analytics | Mit dem Add-on Privacy and Security Shield oder Healthcare Shield | 15.000.000 Kennungen oder 200 Kennungen pro Million CJA-Berechtigungszeilen |

>[!NOTE]
>
> Die meisten Unternehmen verfügen über niedrigere monatliche Limits, die auf ihren tatsächlichen adressierbaren Zielgruppen- oder CJA-Zeilenberechtigungen basieren.

Die Kontingente werden am ersten Tag jedes Kalendermonats zurückgesetzt. Nicht verwendetes Kontingent wird **nicht** übertragen.

>[!NOTE]
>
>Kontingente basieren auf der lizenzierten monatlichen Berechtigung Ihres Unternehmens für **übermittelte Kennungen**. Diese werden von den Systemschutzmechanismen nicht durchgesetzt, können jedoch überwacht und überprüft werden.
>
>Löschen eines Datensatzes ist ein **freigegebener Dienst**. Die monatliche Obergrenze spiegelt die höchsten Berechtigungen für Real-Time CDP, Adobe Journey Optimizer, Customer Journey Analytics und alle anwendbaren Shield-Add-ons wider.

### Zeitleisten für die Übermittlung von Identifikatoren {#sla-processing-timelines}

Nach der Übermittlung werden Anfragen zum Löschen von Datensätzen basierend auf Ihrer Berechtigungsstufe in die Warteschlange gestellt und verarbeitet.

| Produkt- und Berechtigungsbeschreibung | Warteschlangendauer | Maximale Verarbeitungszeit (SLA) |
|------------------------------------------------------------------------------------|---------------------|-------------------------------|
| Ohne Privacy and Security Shield oder Healthcare Shield-Add-on | Bis zu 15 Tage | 30 Tage |
| Mit dem Add-on Privacy and Security Shield oder Healthcare Shield | In der Regel 24 Stunden | 15 Tage |

Wenn für Ihr Unternehmen höhere Limits erforderlich sind, wenden Sie sich zur Überprüfung der Berechtigungen an den Adobe-Support.

>[!TIP]
>
>Informationen zur aktuellen Kontingentnutzung oder Berechtigungsstufe finden Sie im [Kontingentreferenzhandbuch](../api/quota.md).

## Senden der Anfrage {#submit}

Nachdem Sie unter **[!UICONTROL Request settings]** die Identitäten zur Anfrage hinzugefügt haben, geben Sie einen Namen und eine optionale Beschreibung für die Anfrage ein, bevor Sie **[!UICONTROL Submit]** auswählen.

>[!TIP]
>
>Sie können über die Benutzeroberfläche bis zu 10.000 Identitäten pro Anfrage senden. Verwenden Sie zum Übermitteln größerer Volumes (bis zu 100.000 IDs pro Anfrage) die [API-Methode](../api/workorder.md#create).

![Die [!UICONTROL Name]- und [!UICONTROL Description]-Felder der Anfrageeinstellung mit hervorgehobener [!UICONTROL Submit].](../images/ui/record-delete/submit.png)

Es erscheint ein [!UICONTROL Confirm request] Dialogfeld, das anzeigt, dass die Identitäten nach dem Löschen nicht wiederhergestellt werden können. Wählen Sie **[!UICONTROL Submit]** aus, um die Liste der Identitäten zu bestätigen, deren Daten Sie löschen möchten.

![Der [!UICONTROL Confirm request]-Dialog.](../images/ui/record-delete/confirm-request.png)

Nachdem die Anfrage gesendet wurde, wird ein Arbeitsauftrag erstellt und auf der Registerkarte [!UICONTROL Record] des Arbeitsbereichs [!UICONTROL Data Lifecycle] angezeigt. Hier können Sie den Fortschritt des Arbeitsauftrags überwachen.

>[!NOTE]
>
>Im Abschnitt „Übersicht“ unter [Timelines und Transparenz](../home.md#record-delete-transparency) finden Sie Einzelheiten darüber, wie Löschvorgänge von Datensätzen verarbeitet werden, sobald sie ausgeführt werden.

![Die Registerkarte &quot;[!UICONTROL Record]&quot; des Arbeitsbereichs &quot;[!UICONTROL Data Lifecycle]&quot; mit hervorgehobener neuer Anfrage.](../images/ui/record-delete/request-log.png)

## Löschen von Datensätzen aus Datensätzen basierend auf relationalen Schemata {#relational-record-delete}

Wenn der Datensatz, aus dem Sie löschen möchten, auf einem relationalen Schema basiert, sollten Sie die folgenden Überlegungen überprüfen, um sicherzustellen, dass Datensätze korrekt entfernt und aufgrund von Diskrepanzen zwischen Experience Platform und Ihrem Quellsystem nicht erneut aufgenommen werden.

### Verhalten beim Löschen von Datensätzen

In der folgenden Tabelle wird beschrieben, wie sich das Löschen von Datensätzen je nach Aufnahmemethode und geänderter Datenerfassungskonfiguration über Experience Platform- und Quellsysteme hinweg verhält.

| Aspekt | Verhalten |
|---------------------|--------------------------------------------------------------------------|
| Platform-Löschung | Datensätze werden aus dem Experience Platform-Datensatz und dem Data Lake entfernt. |
| Aufbewahrung in Source | Datensätze verbleiben im Quellsystem, es sei denn, sie werden dort explizit gelöscht. |
| Auswirkung auf vollständige Aktualisierung | Bei Verwendung der vollständigen Aktualisierung können gelöschte Datensätze erneut aufgenommen werden, es sei denn, sie werden entfernt oder aus der Quelle ausgeschlossen. |
| Verhalten bei der Datenerfassung ändern | Datensätze, die mit `_change_request_type = 'd'` gekennzeichnet sind, werden während der Aufnahme gelöscht. Nicht gekennzeichnete Datensätze können erneut aufgenommen werden. |

Um eine erneute Aufnahme zu verhindern, wenden Sie denselben Löschansatz sowohl auf Ihr Quellsystem als auch auf Experience Platform an, indem Sie entweder Datensätze aus beiden Systemen entfernen oder `_change_request_type = 'd'` für Datensätze einschließen, die Sie löschen möchten.

### Ändern von Datenerfassungs- und Kontrollspalten

Relationale Schemata, die Quellen mit Änderungsdatenerfassung verwenden, können die `_change_request_type` Kontrollspalte verwenden, wenn zwischen Löschvorgängen und Upserts unterschieden wird. Während der Aufnahme werden Datensätze, die mit `d` gekennzeichnet sind, aus dem Datensatz gelöscht, während Datensätze, die mit `u` oder ohne Spalte gekennzeichnet sind, als Upserts behandelt werden. Die `_change_request_type` Spalte wird nur zur Aufnahmezeit gelesen und nicht im Zielschema gespeichert oder XDM-Feldern zugeordnet.

>[!NOTE]
>
>Das Löschen von Datensätzen über die Data Lifecycle-Benutzeroberfläche hat keine Auswirkungen auf das Quellsystem. Um Daten aus beiden Speicherorten zu entfernen, löschen Sie sie sowohl in Experience Platform als auch in der Quelle.

### Zusätzliche Löschmethoden für relationale Schemata

Über den standardmäßigen Löscharbeitsablauf für Datensätze hinaus unterstützen relationale Schemata zusätzliche Methoden für bestimmte Anwendungsfälle:

* **Ansatz mit sicherer Kopie des Datensatzes**: Duplizieren Sie den Produktionsdatensatz und wenden Sie Löschvorgänge auf die Kopie an, um sie kontrollierten Tests oder einer Abstimmung zu unterziehen, bevor Sie Änderungen auf die Produktionsdaten anwenden.
* **Nur-Löschen-Batch-Upload**: Laden Sie eine Datei hoch, die nur Löschvorgänge für eine gezielte Hygiene enthält, wenn Sie bestimmte Datensätze entfernen müssen, ohne andere Daten zu beeinflussen.

### Deskriptorunterstützung für Hygienevorgänge {#descriptor-support}

Relationale Schemadeskriptoren stellen wichtige Metadaten für präzise Hygienevorgänge bereit:

* **Primärer Schlüsseldeskriptor**: Identifiziert Datensätze eindeutig für zielgerichtete Aktualisierungen oder Löschungen, um sicherzustellen, dass die richtigen Datensätze betroffen sind.
* **Versionsdeskriptor**: Stellt sicher, dass Löschvorgänge und Aktualisierungen in der richtigen chronologischen Reihenfolge durchgeführt werden, um Vorgänge außerhalb der Sequenz zu verhindern.
* **Zeitstempeldeskriptor (Zeitreihenschemata)**: Richtet Löschvorgänge an den Ereigniszeiten und nicht an den Aufnahmezeiten aus.

>[!NOTE]
>
>Hygieneprozesse werden auf Datensatzebene ausgeführt. Bei profilaktivierten Datensätzen sind möglicherweise zusätzliche Profil-Workflows erforderlich, um die Konsistenz über das Echtzeit-Kundenprofil hinweg zu wahren.

### Geplante Aufbewahrung für relationale Schemata

Informationen zur automatisierten Hygiene basierend auf dem Datenalter und nicht auf bestimmten Identitäten finden Sie unter [Verwalten der Experience Event-Datensatzaufbewahrung (TTL)](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) für die geplante Aufbewahrung auf Zeilenebene im Data Lake.

>[!NOTE]
>
>Die Gültigkeit auf Zeilenebene wird nur für Datensätze unterstützt, die Zeitreihenverhalten verwenden.

### Best Practices für das Löschen von relationalen Datensätzen

Befolgen Sie die folgenden Best Practices, um eine unbeabsichtigte erneute Aufnahme von Daten zu vermeiden und die Konsistenz der Daten systemübergreifend zu gewährleisten:

* **Löschungen koordinieren**: Richten Sie das Löschen von Datensätzen an Ihrer geänderten Datenerfassungskonfiguration und Ihrer Strategie zur Verwaltung von Quelldaten aus.
* **Ändern von Datenerfassungsflüssen**: Nachdem Sie Datensätze in Platform gelöscht haben, überwachen Sie Datenflüsse und bestätigen Sie, dass das Quellsystem dieselben Datensätze entfernt oder in `_change_request_type = 'd'` einbezieht.
* **Quelle bereinigen**: Löschen Sie bei Quellen, die eine vollständige Aktualisierungsaufnahme verwenden, oder Quellen, die Löschvorgänge über die Änderungsdatenerfassung nicht unterstützen, Datensätze direkt aus dem Quellsystem, um eine erneute Aufnahme zu vermeiden.

Weitere Informationen zu Schemaanforderungen finden Sie unter [Anforderungen an relationale ](../../xdm/schema/relational.md#relational-schemas).

Informationen zur Funktionsweise der Änderungsdatenerfassung mit Quellen finden Sie unter [Aktivieren der Änderungsdatenerfassung in Quellen](../../sources/tutorials/api/change-data-capture.md#using-change-data-capture-with-relational-schemas).

## Nächste Schritte

In diesem Dokument wurde beschrieben, wie Datensätze in der Experience Platform-Benutzeroberfläche gelöscht werden. Weitere Informationen zur Durchführung anderer Datenlebenszyklus-Management-Aufgaben in der Benutzeroberfläche finden Sie im Abschnitt [Übersicht über die Datenlebenszyklus-Benutzeroberfläche](./overview.md).

Informationen zum Löschen von Datensätzen mithilfe der Datenhygiene-API finden Sie im [Handbuch zum Arbeitsauftrags-Endpunkt](../api/workorder.md).
