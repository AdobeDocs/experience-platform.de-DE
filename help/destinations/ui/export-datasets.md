---
title: Exportieren von Datensätzen zu Cloud-Speicher-Zielen
type: Tutorial
description: Erfahren Sie, wie Sie Datensätze aus Adobe Experience Platform in Ihren bevorzugten Cloud-Speicher exportieren.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: 5624dab337bcd27e28b4153459bb4e85fab22d6f
workflow-type: tm+mt
source-wordcount: '2594'
ht-degree: 36%

---

# Exportieren von Datensätzen zu Cloud-Speicher-Zielen

>[!AVAILABILITY]
>
>* Diese Funktion steht Kunden zur Verfügung, die das Real-Time CDP Prime- oder Ultimate-Paket, Adobe Journey Optimizer oder Customer Journey Analytics erworben haben. Weitere Informationen erhalten Sie von Ihrem Adobe-Support-Mitarbeiter.

In diesem Artikel wird der Workflow erläutert, der zum Exportieren [Datensätze](/help/catalog/datasets/overview.md) von Adobe Experience Platform an Ihren bevorzugten Cloud-Speicherort, z. B. [!DNL Amazon S3], SFTP-Speicherorte oder [!DNL Google Cloud Storage], mithilfe der Experience Platform-Benutzeroberfläche erforderlich ist.

Sie können auch die Experience Platform-APIs zum Exportieren von Datensätzen verwenden. Weitere Informationen finden [ im Tutorial ](/help/destinations/api/export-datasets.md) Exportieren von Datensätzen .

## Datensätze, die exportiert werden können {#datasets-to-export}

Die Datensätze, die Sie exportieren können, variieren je nach Experience Platform-Anwendung (Real-Time CDP, Adobe Journey Optimizer), Ebene (Prime oder Ultimate) und Add-ons, die Sie erworben haben (z. B. Data Distiller).

In der folgenden Tabelle erfahren Sie, welche Datensatztypen Sie je nach Programm, Produktstufe und erworbenen Add-ons exportieren können:

<table>
<thead>
  <tr>
    <th>Anwendung/Add-on</th>
    <th>Stufe</th>
    <th>Für den Export verfügbare Datensätze</th>
  </tr>
</thead>
<tbody>
  <tr>
    <td rowspan="2">Real-Time CDP</td>
    <td>Prime</td>
    <td>Profil- und Erlebnisereignis-Datensätze, die in der Experience Platform-Benutzeroberfläche nach der Aufnahme oder Erfassung von Daten über Quellen, Web SDK, Mobile SDK, Analytics Data Connector und Audience Manager erstellt wurden.</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td><ul><li>Profil- und Erlebnisereignis-Datensätze, die in der Experience Platform-Benutzeroberfläche nach der Aufnahme oder Erfassung von Daten über Quellen, Web SDK, Mobile SDK, Analytics Data Connector und Audience Manager erstellt wurden.</li><li> <a href="https://experienceleague.adobe.com/docs/experience-platform/dashboards/query.html#profile-attribute-datasets">Systemgenerierter Profil-Snapshot-Datensatz</a>.</li></td>
  </tr>
  <tr>
    <td rowspan="2">Adobe Journey Optimizer</td>
    <td>Prime</td>
    <td>Weitere Informationen finden Sie in der <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Dokumentation </a> Adobe Journey Optimizer.</td>
  </tr>
  <tr>
    <td>Ultimate</td>
    <td>Weitere Informationen finden Sie in der <a href="https://experienceleague.adobe.com/docs/journey-optimizer/using/data-management/datasets/export-datasets.html#datasets"> Dokumentation </a> Adobe Journey Optimizer.</td>
  </tr>
  <tr>
    <td>Customer Journey Analytics</td>
    <td>Alle</td>
    <td> Profil- und Erlebnisereignis-Datensätze, die in der Experience Platform-Benutzeroberfläche nach der Aufnahme oder Erfassung von Daten über Quellen, Web SDK, Mobile SDK, Analytics Data Connector und Audience Manager erstellt wurden.</td>
  </tr>
  <tr>
    <td>Data Distiller</td>
    <td>Data Distiller (Add-on)</td>
    <td>Abgeleitete Datensätze, die über den Abfrage-Service erstellt wurden.</td>
  </tr>
</tbody>
</table>

## Video-Tutorial {#video-tutorial}

Sehen Sie sich das folgende Video an, um eine End-to-End-Erklärung des auf dieser Seite beschriebenen Workflows, die Vorteile der Verwendung der Funktion „Datensatz exportieren“ und einige vorgeschlagene Anwendungsfälle zu erhalten.

>[!VIDEO](https://video.tv.adobe.com/v/3424392/)

## Unterstützte Ziele {#supported-destinations}

Derzeit können Sie Datensätze in die Cloud-Speicher-Ziele exportieren, die im Screenshot hervorgehoben und unten aufgeführt sind.

![Zielkatalogseite, die zeigt, welche Ziele Datensatzexporte unterstützen.](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Wann Zielgruppen aktiviert oder Datensätze exportiert werden sollten {#when-to-activate-audiences-or-activate-datasets}

Einige dateibasierte Ziele im Experience Platform-Katalog unterstützen sowohl die Zielgruppenaktivierung als auch den Datensatzexport.

* Erwägen Sie die Aktivierung von Zielgruppen, wenn Ihre Daten in Profilen gruppiert nach Zielgruppeninteressen oder Qualifikationen strukturiert sein sollen.
* Alternativ können Sie Datensatzexporte in Betracht ziehen, wenn Sie Rohdatensätze exportieren möchten, die nicht nach Zielgruppeninteressen oder Qualifikationen gruppiert oder strukturiert sind. Sie können diese Daten für Berichte, Datenwissenschafts-Workflows und viele andere Anwendungsfälle verwenden. Als Administrator, Datentechniker oder Analyst können Sie beispielsweise Daten von Experience Platform exportieren, um sie mit Ihrem Data Warehouse zu synchronisieren, in BI-Analyse-Tools oder externen Cloud-ML-Tools verwenden oder in Ihrem System für langfristige Speicheranforderungen speichern.

Dieses Dokument enthält alle Informationen, die zum Exportieren von Datensätzen erforderlich sind. Wenn Sie „Zielgruppen *für Cloud* Speicher- oder E-Mail-Marketing-Ziele aktivieren möchten, lesen Sie [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](/help/destinations/ui/activate-batch-profile-destinations.md).

## Voraussetzungen {#prerequisites}

Um Datensätze in Cloud-Speicher-Ziele zu exportieren, müssen Sie erfolgreich [eine Verbindung mit einem Ziel hergestellt haben](./connect-destination.md). Wenn Sie es noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

### Erforderliche Berechtigungen {#permissions}

Zum Exportieren von Datensätzen benötigen Sie die Berechtigungen **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Datensätze anzeigen]** und **[!UICONTROL Datensatzziele verwalten und aktivieren]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um sicherzustellen, dass Sie über die erforderlichen Berechtigungen zum Exportieren von Datensätzen verfügen und dass das Ziel den Export von Datensätzen unterstützt, durchsuchen Sie den Zielkatalog. Wenn ein Ziel über die Steuerung **[!UICONTROL Aktivieren]** oder **[!UICONTROL Datensätze exportieren]** verfügt, dann haben Sie die entsprechenden Berechtigungen.

## Auswählen des Ziels {#select-destination}

Befolgen Sie die Anweisungen zum Auswählen eines Ziels, an das Sie Ihre Datensätze exportieren können:

1. Navigieren Sie zu **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]**.

   ![Registerkarte „Zielkatalog“ mit hervorgehobenem Katalog-Steuerelement.](/help/destinations/assets/ui/export-datasets/catalog-tab.png)

1. Wählen Sie **[!UICONTROL Aktivieren]** oder **[!UICONTROL Datensätze exportieren]** auf der Karte aus, die dem Ziel entspricht, an das Sie Datensätze exportieren möchten.

   ![Registerkarte „Zielkatalog“ mit hervorgehobenem Steuerelement „Aktivieren“.](/help/destinations/assets/ui/export-datasets/activate-button.png)

1. Wählen Sie **[!UICONTROL Datentypdatensätze]** und dann die Zielverbindung aus, in die Sie Datensätze exportieren möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**.

>[!TIP]
> 
>Wenn Sie ein neues Ziel zum Exportieren von Datensätzen einrichten möchten, wählen Sie **[!UICONTROL Neues Ziel konfigurieren]** aus, um den Workflow [Mit Ziel verbinden](/help/destinations/ui/connect-destination.md) auszulösen.

![Zielaktivierungs-Workflow mit hervorgehobenem Steuerelement „Datensätze“.](/help/destinations/assets/ui/export-datasets/select-datatype-datasets.png)

1. Die Ansicht **[!UICONTROL Datensätze auswählen]** wird angezeigt. Fahren Sie mit dem nächsten Abschnitt fort, um die [Datensätze auszuwählen](#select-datasets), die exportiert werden sollen.

## Auswählen Ihrer Datensätze {#select-datasets}

Aktivieren Sie die Kontrollkästchen links neben den Datensatznamen, um die Datensätze auszuwählen, die Sie für das Ziel aktivieren möchten, und klicken Sie dann auf **[!UICONTROL Weiter]**.

![Workflow für den Datensatzexport, der den Schritt „Datensätze auswählen“ zeigt, in dem Sie auswählen können, welche Datensätze exportiert werden sollen.](/help/destinations/assets/ui/export-datasets/select-datasets.png)

## Planen des Datensatzexports {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_datasets_exportoptions"
>title="Dateiexportoptionen für Datensätze"
>abstract="Wählen Sie **Inkrementelle Dateien exportieren** aus, um nur die Daten zu exportieren, die dem Datensatz seit dem letzten Export hinzugefügt wurden. <br> Der erste inkrementelle Dateiexport umfasst alle Daten im Datensatz, sodass eine Aufstockung durchgeführt wird. Weitere inkrementelle Dateien enthalten nur die Daten, die dem Datensatz seit dem ersten Export hinzugefügt wurden. <br> Wählen Sie **Vollständige Dateien exportieren** aus, um bei jedem Export die vollständige Zugehörigkeit jedes Datensatzes zu exportieren. "

>[!CONTEXTUALHELP]
>id="dataset_dataflow_needs_schedule_end_date_header"
>title="Aktualisieren des Enddatums für diesen Datenfluss"
>abstract="Aktualisieren des Enddatums für diesen Datenfluss"

>[!CONTEXTUALHELP]
>id="dataset_dataflow_needs_schedule_end_date_body"
>title="Aktualisieren des Enddatums für diesen Datenflusshauptteil"
>abstract="Aufgrund aktueller Aktualisierungen an diesem Ziel benötigt der Datenfluss jetzt ein Enddatum. Adobe hat als standardmäßiges Enddatum den 1. März 2025 festgelegt. Bitte aktualisieren Sie auf das gewünschte Enddatum. Andernfalls werden die Datenexporte am Standarddatum gestoppt."

Verwenden Sie den **[!UICONTROL Zeitplan]**-Schritt, um:

* Legen Sie ein Start- und Enddatum sowie eine Exportkadenz für Ihre Datensatzexporte fest.
* Konfigurieren Sie, ob die exportierten Datensatzdateien die vollständige Mitgliedschaft des Datensatzes exportieren sollen oder nur inkrementelle Änderungen an der Mitgliedschaft bei jedem Exportereignis.
* Passen Sie den Ordnerpfad an Ihrem Speicherort an, an den Datensätze exportiert werden sollen. Weitere Informationen zum [ (Bearbeiten des Exportordnerpfads](#edit-folder-path).

Verwenden Sie das Steuerelement **[!UICONTROL Zeitplan bearbeiten]** auf der Seite, um die Exportkadenz von Exporten zu bearbeiten und auszuwählen, ob vollständige oder inkrementelle Dateien exportiert werden sollen.

![Steuerung „Zeitplan bearbeiten“ im Schritt „Planung“ hervorgehoben.](/help/destinations/assets/ui/export-datasets/edit-schedule-control-highlight.png)

Die Option **[!UICONTROL Inkrementelle Dateien exportieren]** ist standardmäßig ausgewählt. Dies führt zu einem Trigger einer oder mehrerer Dateien, die einen vollständigen Schnappschuss des Datensatzes darstellen. Nachfolgende Dateien sind inkrementelle Ergänzungen zum Datensatz seit dem vorherigen Export. Sie können auch **[!UICONTROL Vollständige Dateien exportieren]** auswählen. Wählen Sie in diesem Fall die Häufigkeit **[!UICONTROL Einmal]** für einen einmaligen vollständigen Export des Datensatzes aus.

>[!IMPORTANT]
>
>Der erste inkrementelle Dateiexport umfasst alle vorhandenen Daten im Datensatz, sodass eine Aufstockung durchgeführt wird. Der Export kann eine oder mehrere Dateien enthalten.

![Workflow für den Datensatzexport, der den Planungsschritt zeigt.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Verwenden Sie den **[!UICONTROL Häufigkeitsselektor]** zur Auswahl der Exportfrequenz:

   * **[!UICONTROL Täglich]**: Planung von inkrementellen Dateiexporten einmal täglich, jeden Tag, zum von Ihnen festgelegten Zeitpunkt.
   * **[!UICONTROL Stündlich]**: Planung von inkrementellen Dateiexporten alle 3, 6, 8 oder 12 Stunden.

2. Verwenden Sie den **[!UICONTROL Zeitselektor]** zur Auswahl der Tageszeit im Format [!DNL UTC], zu der der Export erfolgen soll.

3. Verwenden Sie den **[!UICONTROL Datum]**-Selektor, um das Intervall auszuwählen, in dem der Export stattfinden soll.

4. Wählen Sie **[!UICONTROL Speichern]** aus, um den Zeitplan zu speichern, und fahren Sie mit dem Schritt **[!UICONTROL Überprüfen]** fort.

>[!NOTE]
> 
>Bei Datensatzexporten haben die Dateinamen ein vordefiniertes Standardformat, das nicht geändert werden kann. Siehe Abschnitt [Überprüfen eines erfolgreichen Datensatzexports](#verify), um weitere Informationen und Beispiele für exportierte Dateien zu erhalten.

## Ordnerpfad bearbeiten {#edit-folder-path}

>[!CONTEXTUALHELP]
>id="destinations_folder_name_template"
>title="Ordnerpfad bearbeiten"
>abstract="Verwenden Sie mehrere bereitgestellte Makros, um den Ordnerpfad anzupassen, in den Datensätze exportiert werden."

>[!CONTEXTUALHELP]
>id="destinations_folder_name_template_preview"
>title="Vorschau des Datensatzordnerpfads"
>abstract="Sehen Sie sich eine Vorschau der Ordnerstruktur an, die basierend auf den in diesem Fenster hinzugefügten Makros am Speicherort erstellt wird."

Wählen Sie **[!UICONTROL Ordnerpfad bearbeiten]**, um die Ordnerstruktur in Ihrem Speicherort, in dem exportierte Datensätze abgelegt werden, anzupassen.

![Das Steuerelement „Ordnerpfad bearbeiten“ ist im Planungsschritt hervorgehoben.](/help/destinations/assets/ui/export-datasets/edit-folder-path.png)

Sie können mehrere verfügbare Makros verwenden, um einen gewünschten Ordnernamen anzupassen. Doppelklicken Sie auf ein Makro, um es zum Ordnerpfad hinzuzufügen, und trennen Sie die Ordner mithilfe von `/` zwischen den Makros.

![Makroauswahl im modalen Fenster des benutzerdefinierten Ordners hervorgehoben.](/help/destinations/assets/ui/export-datasets/custom-folder-path-macros.png)

Nach Auswahl der gewünschten Makros können Sie eine Vorschau der Ordnerstruktur anzeigen, die an Ihrem Speicherort erstellt wird. Die erste Ebene in der Ordnerstruktur stellt den **[!UICONTROL Ordnerpfad“ dar]** den Sie angegeben haben, als Sie [mit dem Ziel verbunden) ](/help/destinations/ui/connect-destination.md##set-up-connection-parameters) Datensätze exportieren.

![Vorschau des Ordnerpfads im modalen Fenster des benutzerdefinierten Ordners hervorgehoben.](/help/destinations/assets/ui/export-datasets/custom-folder-path-preview.png)

## Überprüfung {#review}

Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]** aus, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertigstellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Datensätzen an das Ziel zu beginnen.

![Arbeitsablauf für den Datensatzexport, der den Überprüfungsschritt anzeigt.](/help/destinations/assets/ui/export-datasets/review.png)

## Überprüfen eines erfolgreichen Datensatzexports {#verify}

Beim Exportieren von Datensätzen erstellt Experience Platform eine oder mehrere `.json` oder `.parquet` Dateien an dem von Ihnen angegebenen Speicherort. Es ist damit zu rechnen, dass neue Dateien entsprechend dem von Ihnen angegebenen Exportzeitplan an Ihrem Speicherort abgelegt werden.

Experience Platform erstellt eine Ordnerstruktur am angegebenen Speicherort, in der die exportierten Datensatzdateien abgelegt werden. Das standardmäßige Exportmuster für Ordner wird unten gezeigt, Sie können jedoch [die Ordnerstruktur mit Ihren bevorzugten Makros anpassen](#edit-folder-path).

>[!TIP]
> 
>Die erste Ebene in dieser Ordnerstruktur - `folder-name-you-provided` - stellt den **[!UICONTROL Ordnerpfad]** dar, den Sie angegeben haben, als Sie [mit dem Ziel verbunden](/help/destinations/ui/connect-destination.md##set-up-connection-parameters) Datensätze exportieren.

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

Der standardmäßige Dateiname wird nach dem Zufallsprinzip generiert, was sicherstellt, dass die Namen von exportierten Dateien eindeutig sind.

### Beispiele für Datensatzdateien {#sample-files}

Das Vorhandensein dieser Dateien an Ihrem Speicherort bestätigt einen erfolgreichen Export. Um zu verstehen, wie die exportierten Dateien strukturiert sind, können Sie eine [Parquet](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet)- oder [JSON](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json)-Beispieldatei herunterladen.

#### Komprimierte Datensatzdateien {#compressed-dataset-files}

Im Workflow [Mit Ziel verbinden](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options) können Sie die exportierten Datensatzdateien auswählen, die komprimiert werden sollen, wie unten dargestellt:

![Dateityp- und Komprimierungsauswahl beim Herstellen einer Verbindung zu einem Ziel zum Exportieren von Datensätzen.](/help/destinations/assets/ui/export-datasets/compression-format-datasets.gif)

Beachten Sie den Unterschied im Dateiformat zwischen den beiden Dateitypen, wenn sie komprimiert werden:

* Beim Exportieren komprimierter JSON-Dateien wird das exportierte Dateiformat `json.gz`. Das Format des exportierten JSON ist NDJSON, das standardmäßige Austauschformat im Big-Data-Ökosystem. Adobe empfiehlt die Verwendung eines NDJSON-kompatiblen Clients zum Lesen der exportierten Dateien.
* Beim Exportieren von komprimierten Parquet-Dateien wird das exportierte Dateiformat `gz.parquet`

Exporte in JSON-Dateien werden unterstützt *nur im komprimierten Modus*. Exporte in Parquet-Dateien werden im komprimierten und unkomprimierten Modus unterstützt.

## Entfernen von Datensätzen aus Zielen {#remove-dataset}

Gehen Sie wie folgt vor, um Datensätze aus einem vorhandenen Datenfluss zu entfernen:

1. Melden Sie sich bei der [Experience Platform-Benutzeroberfläche](https://experience.adobe.com/platform/) an und wählen Sie **[!UICONTROL Ziele]** über die linke Navigationsleiste aus. Wählen Sie **[!UICONTROL Durchsuchen]** in der oberen Kopfzeile aus, um Ihre vorhandenen Ziel-Datenflüsse anzuzeigen.

   ![Die Ansicht „Ziel durchsuchen“, wobei eine Zielverbindung angezeigt wird und der Rest unscharf gemacht wurde.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Wählen Sie das Symbol ![Filter](/help/images/icons/filter.png) oben links, um das Sortier-Bedienfeld zu öffnen. Das Sortier-Bedienfeld bietet eine Liste aller Ihrer Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl von Datenflüssen anzuzeigen, die mit dem ausgewählten Ziel verknüpft sind.

2. Wählen Sie in der Spalte **[!UICONTROL Aktivierungsdaten]** das Steuerelement für Datensätze aus, um alle Datensätze anzuzeigen, die diesem Exportdatenfluss zugeordnet sind.

   ![Die verfügbare Navigationsoption für Datensätze, die in der Spalte „Aktivieriungsdaten“ hervorgehoben ist.](../assets/ui/export-datasets/go-to-datasets-data.png)

3. Die Seite **[!UICONTROL Aktivierungsdaten]** für dieses Ziel wird angezeigt. Aktivieren Sie die Kontrollkästchen links in der Datensatzliste, um die Datensätze auszuwählen, die Sie entfernen möchten, und wählen Sie dann **[!UICONTROL Datensätze entfernen]** in der rechten Leiste aus, um den Trigger zum Entfernen des Datensatzbestätigungsdialogfelds anzuzeigen.

   ![Der Dialog „Datensatz entfernen“, der die Steuerung „Datensatz entfernen“ in der rechten Leiste anzeigt.](../assets/ui/export-datasets/bulk-remove-datasets.png)

4. Wählen Sie im Bestätigungsdialog die Option **[!UICONTROL Entfernen]** aus, um den Datensatz sofort aus den Exporten in das Ziel zu entfernen.

   ![Dialogfeld mit der Option „Löschen des Datensatzes aus dem Datenfluss bestätigen“.](../assets/ui/export-datasets/remove-dataset-confirm.png)

## Berechtigungen für den Datensatzexport {#licensing-entitlement}

Informationen dazu, wie viele Daten Sie pro Experience Platform-Anwendung und Jahr exportieren dürfen, finden Sie in den Produktbeschreibungsdokumenten. Sie können beispielsweise die Real-Time CDP-Produktbeschreibung ([) ](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html).

Beachten Sie, dass die Berechtigungen für den Datenexport für verschiedene Programme nicht additiv sind. Wenn Sie beispielsweise Real-Time CDP Ultimate und Adobe Journey Optimizer Ultimate erwerben, ist die Berechtigung für den Profilexport gemäß den Produktbeschreibungen höher als die beiden Berechtigungen. Die Berechnung Ihrer Volumenberechtigungen erfolgt anhand der Gesamtzahl der lizenzierten Profile und der Multiplikation mit 500 KB für Real-Time CDP Prime bzw. 700 KB für Real-Time CDP Ultimate, um zu bestimmen, wie viel Datenvolumen Ihnen zusteht.

Wenn Sie dagegen Add-ons wie Data Distiller erworben haben, stellt das Datenexportlimit, zu dem Sie berechtigt sind, die Summe aus der Produktebene und dem Add-on dar.

Sie können Ihre Profilexporte anhand Ihrer vertraglichen Beschränkungen im Dashboard [Lizenznutzung“ anzeigen und ](/help/landing/license-usage-and-guardrails/license-usage-dashboard.md).

## Bekannte Einschränkungen {#known-limitations}

Beachten Sie die folgenden Einschränkungen für die allgemeine Verfügbarkeit von Releases von Datensatzexporten:

* Experience Platform exportiert möglicherweise mehrere Dateien, selbst für kleine Datensätze. Der Datensatzexport ist für die Integration von System zu System ausgelegt und für Leistung optimiert, sodass die Anzahl der exportierten Dateien nicht angepasst werden kann.
* Die Namen exportierter Dateien können derzeit nicht angepasst werden.
* Über API erstellte Datensätze sind derzeit nicht für den Export verfügbar.
* Die Benutzeroberfläche hindert Sie derzeit nicht daran, einen Datensatz zu löschen, während er an ein Ziel exportiert wird. Löschen Sie keine Datensätze, während sie an Ziele exportiert werden. [Entfernen Sie den Datensatz](#remove-dataset) aus einem Ziel-Datenfluss, bevor Sie ihn löschen.
* Überwachungsmetriken für Datensatzexporte werden derzeit mit Zahlen für Profilexporte gemischt, sodass sie nicht die tatsächlichen Exportzahlen widerspiegeln.
* Daten mit einem Zeitstempel, der älter als 365 Tage ist, werden aus Datensatzexporten ausgeschlossen. Weitere Informationen finden Sie in der [Leitplanken für geplante Datensatzexporte](/help/destinations/guardrails.md#guardrails-for-scheduled-dataset-exports)

## Häufig gestellte Fragen {#faq}

**Können wir eine Datei ohne Ordner erzeugen, wenn wir nur unter `/` als Ordnerpfad speichern? Wenn wir keinen Ordnerpfad benötigen, wie werden dann Dateien mit doppelten Namen in einem Ordner oder Speicherort generiert?**

+++Antwort
Ab der Version vom September 2024 ist es möglich, den Ordnernamen anzupassen und sogar `/` zum Exportieren von Dateien für alle Datensätze im selben Ordner zu verwenden. Adobe empfiehlt dies nicht für Ziele, die mehrere Datensätze exportieren, da systemgenerierte Dateinamen, die zu verschiedenen Datensätzen gehören, im selben Ordner gemischt werden.
+++

**Können Sie die Manifestdatei zu einem Ordner und die Datendateien zu einem anderen Ordner weiterleiten?**

+++Antwort
Nein, es gibt keine Möglichkeit, die Manifestdatei an einen anderen Speicherort zu kopieren.
+++

**Können wir die Reihenfolge oder den Zeitpunkt der Dateibereitstellung steuern?**

+++Antwort
Es gibt Optionen für die Planung des Exports. Es gibt keine Möglichkeiten, das Kopieren der Dateien zu verzögern oder zu sequenzieren. Sie werden an Ihren Speicherort kopiert, sobald sie generiert werden.
+++

**Welche Formate sind für die Manifestdatei verfügbar?**

+++Antwort
Die Manifestdatei liegt im JSON-Format vor.
+++

**Gibt es API-Verfügbarkeit für die Manifestdatei?**

+++Antwort
Für die Manifestdatei ist keine API verfügbar, sie enthält jedoch eine Liste der Dateien, die den Export umfassen.
+++

**Können wir der Manifestdatei zusätzliche Details hinzufügen (d. h. die Anzahl der Einträge)? Wenn ja, wie?**

+++Antwort
Es ist nicht möglich, der Manifestdatei zusätzliche Informationen hinzuzufügen. Die Anzahl der Einträge ist über die `flowRun`-Entität verfügbar (abfragbar über API). Weitere Informationen finden Sie unter Überwachung von Zielen.
+++

**Wie werden Datendateien aufgeteilt? Wie viele Datensätze pro Datei?**

+++Antwort
Datendateien werden gemäß der Standardpartitionierung im Data Lake von Experience Platform aufgeteilt. Größere Datensätze haben eine höhere Anzahl von Partitionen. Die Standardpartitionierung kann vom Benutzer nicht konfiguriert werden, da sie für das Lesen optimiert ist.
+++

**Können wir einen Schwellenwert (Anzahl der Datensätze pro Datei) festlegen?**

+++Antwort
Nein, das ist nicht möglich.
+++

**Wie senden wir einen Datensatz erneut, wenn der erste Versand fehlerhaft ist?**

+++Antwort
Für die meisten Arten von Systemfehlern werden automatisch weitere Zustellversuche unternommen.
+++