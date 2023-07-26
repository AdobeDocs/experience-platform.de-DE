---
title: (Beta) Exportieren von Datensätzen an Cloud-Speicher-Ziele
type: Tutorial
description: Erfahren Sie, wie Sie Datensätze aus Adobe Experience Platform in Ihren bevorzugten Cloud-Speicher exportieren.
exl-id: e89652d2-a003-49fc-b2a5-5004d149b2f4
source-git-commit: fadc1f5f3842c9c2e39b6204dd455621ec84ad68
workflow-type: tm+mt
source-wordcount: '1421'
ht-degree: 82%

---

# (Beta) Exportieren von Datensätzen an Cloud-Speicher-Ziele

>[!IMPORTANT]
>
>* Die Funktion zum Export von Datensätzen befindet sich derzeit in der Beta-Phase und steht nicht allen Nutzern zur Verfügung. Dokumentation und Funktionalitäten können sich ändern.
>* Diese Beta-Funktion unterstützt den Export von Daten der ersten Generation, wie er in der [Produktbeschreibung](https://helpx.adobe.com/de/legal/product-descriptions/real-time-customer-data-platform-b2c-edition-prime-and-ultimate-packages.html) der Real-time Customer Data Platform definiert ist.
>* Diese Funktion steht Kunden zur Verfügung, die das Prime- oder das Ultimate-Paket von Real-Time CDP erworben haben. Wenden Sie sich für weitere Informationen an Ihren Kundenbetreuer.

In diesem Artikel wird der Workflow erläutert, der zum Exportieren erforderlich ist [Datensätze](/help/catalog/datasets/overview.md) von Adobe Experience Platform zu Ihrem bevorzugten Cloud-Speicher, z. B. [!DNL Amazon S3], SFTP-Speicherorten oder [!DNL Google Cloud Storage] durch Verwendung der Experience Platform-Benutzeroberfläche.

Sie können auch die Experience Platform-APIs verwenden, um Datensätze zu exportieren. Lesen Sie die [API-Tutorial zum Exportieren von Datensätzen](/help/destinations/api/export-datasets.md) für weitere Informationen.

## Unterstützte Ziele {#supported-destinations}

Derzeit können Sie Datensätze zu den im Screenshot hervorgehobenen und unten aufgeführten Cloud-Speicher-Zielen exportieren.

![Ziele, die Datensatzexporte unterstützen](/help/destinations/assets/ui/export-datasets/destinations-supporting-dataset-exports.png)

* [[!DNL (Beta) Azure Data Lake Storage Gen2]](../../destinations/catalog/cloud-storage/adls-gen2.md)
* [[!DNL (Beta) Data Landing Zone]](../../destinations/catalog/cloud-storage/data-landing-zone.md)
* [[!DNL (Beta) Google Cloud Storage]](../../destinations/catalog/cloud-storage/google-cloud-storage.md)
* [[!DNL (Beta) Amazon S3]](../../destinations/catalog/cloud-storage/amazon-s3.md#changelog)
* [[!DNL (Beta) Azure Blob]](../../destinations/catalog/cloud-storage/azure-blob.md#changelog)
* [[!DNL (Beta) SFTP]](../../destinations/catalog/cloud-storage/sftp.md#changelog)

## Wann Zielgruppen aktiviert oder Datensätze exportiert werden {#when-to-activate-audiences-or-activate-datasets}

Einige dateibasierte Ziele im Experience Platform-Katalog unterstützen sowohl die Aktivierung der Zielgruppe als auch den Export von Datensätzen.

* Ziehen Sie die Aktivierung von Zielgruppen in Erwägung, wenn Ihre Daten in Profile strukturiert sein sollen, die nach Zielgruppeninteressen oder Qualifikationen gruppiert sind.
* Alternativ können Sie Datensatzexporte in Betracht ziehen, wenn Sie Rohdatensätze exportieren möchten, die nicht nach Zielgruppeninteressen oder Qualifikationen gruppiert oder strukturiert sind. Sie können diese Daten für Berichte, Datenwissenschaft-Workflows, Compliance-Anforderungen und viele andere Anwendungsfälle verwenden.

Dieses Dokument enthält alle Informationen, die zum Exportieren von Datensätzen erforderlich sind. Wenn Sie Zielgruppen für Cloud-Speicher- oder E-Mail-Marketing-Ziele aktivieren möchten, lesen Sie [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](/help/destinations/ui/activate-batch-profile-destinations.md).

## Voraussetzungen {#prerequisites}

Um Datensätze in Cloud-Speicher-Ziele zu exportieren, müssen Sie erfolgreich [eine Verbindung mit einem Ziel hergestellt haben](./connect-destination.md). Wenn Sie es noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

### Erforderliche Berechtigungen {#permissions}

Zum Exportieren von Datensätzen benötigen Sie die **[!UICONTROL Ziele anzeigen]** und **[!UICONTROL Verwalten und Aktivieren von Datensatzzielen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

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
>abstract="Wählen Sie **Inkrementelle Dateien exportieren** aus, um nur die Daten zu exportieren, die dem Datensatz seit dem letzten Export hinzugefügt wurden. <br> Der erste inkrementelle Dateiexport umfasst alle Daten im Datensatz, sodass eine Aufstockung durchgeführt wird. Weitere inkrementelle Dateien enthalten nur die Daten, die dem Datensatz seit dem ersten Export hinzugefügt wurden."

Im **[!UICONTROL Planung]** Schritt, können Sie ein Startdatum und eine Exportkadenz für Ihre Datensatzexporte festlegen.

Die Option **[!UICONTROL Inkrementelle Dateien exportieren]** ist automatisch ausgewählt. Dies löst einen Export aus, bei dem die erste Datei eine vollständige Momentaufnahme des Datensatzes ist und nachfolgende Dateien inkrementelle Ergänzungen zum Datensatz seit dem vorherigen Export darstellen.

>[!IMPORTANT]
>
>Die erste exportierte inkrementelle Datei enthält alle vorhandenen Daten im Datensatz, sodass eine Aufstockung durchgeführt wird.

![Workflow für den Datensatzexport, der den Planungsschritt zeigt.](/help/destinations/assets/ui/export-datasets/export-incremental-datasets.png)

1. Verwenden Sie den **[!UICONTROL Häufigkeitsselektor]** zur Auswahl der Exportfrequenz:

   * **[!UICONTROL Täglich]**: Planung von inkrementellen Dateiexporten einmal täglich, jeden Tag, zum von Ihnen festgelegten Zeitpunkt.
   * **[!UICONTROL Stündlich]**: Planung von inkrementellen Dateiexporten alle 3, 6, 8 oder 12 Stunden.

2. Verwenden Sie den **[!UICONTROL Zeitselektor]** zur Auswahl der Tageszeit im Format [!DNL UTC], zu der der Export erfolgen soll.

3. Verwenden Sie den **[!UICONTROL Datumsselektor]**, um das Intervall auszuwählen, in dem der Export stattfinden soll. Beachten Sie, dass es in der Betaversion der Funktion nicht möglich ist, ein Enddatum für die Exporte festzulegen. Weitere Informationen finden Sie im Abschnitt [Bekannte Einschränkungen](#known-limitations).

4. Klicken Sie auf **[!UICONTROL Weiter]**, um den Zeitplan zu speichern, und fahren Sie mit dem Schritt **[!UICONTROL Überprüfen]** fort.

>[!NOTE]
> 
>Bei Datensatzexporten haben die Dateinamen ein vordefiniertes Standardformat, das nicht geändert werden kann. Siehe Abschnitt [Überprüfen eines erfolgreichen Datensatzexports](#verify), um weitere Informationen und Beispiele für exportierte Dateien zu erhalten.

## Überprüfung {#review}

Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]** aus, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertigstellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Datensätzen an das Ziel zu beginnen.

![Arbeitsablauf für den Datensatzexport, der den Überprüfungsschritt anzeigt.](/help/destinations/assets/ui/export-datasets/review.png)

## Überprüfen eines erfolgreichen Datensatzexports {#verify}

Beim Exportieren von Datensätzen erstellt Experience Platform eine `.json`- oder `.parquet`-Datei an dem von Ihnen angegebenen Speicherort. Sie können erwarten, dass eine neue Datei entsprechend dem von Ihnen angegebenen Exportplan an Ihrem Speicherort abgelegt wird.

Experience Platform erstellt eine Ordnerstruktur am angegebenen Speicherort, in der die exportierten Datensatzdateien abgelegt werden. Für jeden Exportzeitpunkt wird ein neuer Ordner erstellt, wobei das folgende Muster befolgt wird:

`folder-name-you-provided/datasetID/exportTime=YYYYMMDDHHMM`

Der standardmäßige Dateiname wird nach dem Zufallsprinzip generiert, was sicherstellt, dass die Namen von exportierten Dateien eindeutig sind.

### Beispiele für Datensatzdateien {#sample-files}

Das Vorhandensein dieser Dateien an Ihrem Speicherort bestätigt einen erfolgreichen Export. Um zu verstehen, wie die exportierten Dateien strukturiert sind, können Sie eine [Parquet](../assets/common/part-00000-tid-253136349007858095-a93bcf2e-d8c5-4dd6-8619-5c662e261097-672704-1-c000.parquet)- oder [JSON](../assets/common/part-00000-tid-4172098795867639101-0b8c5520-9999-4cff-bdf5-1f32c8c47cb9-451986-1-c000.json)-Beispieldatei herunterladen.

#### Komprimierte Datensatzdateien {#compressed-dataset-files}

Im [Zielgruppen-Workflow verbinden](/help/destinations/ui/connect-destination.md#file-formatting-and-compression-options)können Sie die zu komprimierenden exportierten Datensatzdateien auswählen, wie unten dargestellt:

![Dateityp und Auswahl der Komprimierung beim Herstellen einer Verbindung zu einem Ziel zum Exportieren von Datensätzen.](/help/destinations/assets/ui/export-datasets/compression-format-datasets.gif)

Beachten Sie bei der Komprimierung den Unterschied im Dateiformat zwischen den beiden Dateitypen:

* Beim Exportieren komprimierter JSON-Dateien ist das exportierte Dateiformat `json.gz`
* Beim Exportieren komprimierter Parquet-Dateien ist das exportierte Dateiformat `gz.parquet`

## Entfernen eines Datensatzes aus dem Ziel {#remove-dataset}

Gehen Sie wie folgt vor, um einen Datensatz aus einem vorhandenen Datenfluss zu entfernen:

1. Melden Sie sich bei der [Experience Platform-Benutzeroberfläche](https://experience.adobe.com/platform/) an und wählen Sie **[!UICONTROL Ziele]** über die linke Navigationsleiste aus. Wählen Sie **[!UICONTROL Durchsuchen]** in der oberen Kopfzeile aus, um Ihre vorhandenen Ziel-Datenflüsse anzuzeigen.

   ![Die Ansicht „Ziel durchsuchen“, wobei eine Zielverbindung angezeigt wird und der Rest unscharf gemacht wurde.](../assets/ui/export-datasets/browse-dataset-connections.png)

   >[!TIP]
   > 
   >Wählen Sie das Symbol ![Filter](../assets/ui/edit-activation/filter.png) oben links, um das Sortier-Bedienfeld zu öffnen. Das Sortier-Bedienfeld bietet eine Liste aller Ihrer Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl von Datenflüssen anzuzeigen, die mit dem ausgewählten Ziel verknüpft sind.

1. Wählen Sie in der Spalte **[!UICONTROL Aktivierungsdaten]** das Steuerelement für Datensätze aus, um alle Datensätze anzuzeigen, die diesem Exportdatenfluss zugeordnet sind.

   ![Die verfügbare Navigationsoption für Datensätze, die in der Spalte „Aktivieriungsdaten“ hervorgehoben ist.](../assets/ui/export-datasets/go-to-datasets-data.png)

1. Die Seite **[!UICONTROL Aktivierungsdaten]** für dieses Ziel wird angezeigt. Wählen Sie **[!UICONTROL Datensatz entfernen]** in der rechten Leiste aus, woraufhin der Bestätigungsdialog zum Entfernen des Datensatzes erscheint.

   ![Der Dialog „Datensatz entfernen“, der die Steuerung „Datensatz entfernen“ in der rechten Leiste anzeigt.](../assets/ui/export-datasets/remove-dataset-control.png)

1. Wählen Sie im Bestätigungsdialog die Option **[!UICONTROL Entfernen]** aus, um den Datensatz sofort aus den Exporten in das Ziel zu entfernen.

   ![Dialogfeld mit der Option „Löschen des Datensatzes aus dem Datenfluss bestätigen“.](../assets/ui/export-datasets/remove-dataset-confirm.png)

## Bekannte Einschränkungen {#known-limitations}

Beachten Sie die folgenden Einschränkungen für die Betaversion von Datensatzexporten:

* Es gibt derzeit eine einzige Berechtigung (**[!UICONTROL Datensatzziele verwalten und aktivieren]**), welche die Berechtigungen zum Verwalten und Aktivieren von Datensatzzielen beinhaltet. Diese Steuerelemente werden in Zukunft in detailliertere Berechtigungen aufgeteilt. Im Abschnitt [Erforderliche Berechtigungen](#permissions) finden Sie eine vollständige Liste der Berechtigungen, die Sie zum Exportieren von Datensätzen benötigen.
* Derzeit können Sie nur inkrementelle Dateien exportieren, und für Ihre Datensatzexporte kann kein Enddatum ausgewählt werden.
* Die Namen von exportierten Dateien können derzeit nicht angepasst werden.
* Die Benutzeroberfläche hindert Sie derzeit nicht daran, einen Datensatz zu löschen, während er an ein Ziel exportiert wird. Löschen Sie keine Datensätze, während sie an Ziele exportiert werden. [Entfernen Sie den Datensatz](#remove-dataset) aus einem Ziel-Datenfluss, bevor Sie ihn löschen.
* Überwachungsmetriken für Datensatzexporte werden derzeit mit Zahlen für Profilexporte gemischt, sodass sie nicht die tatsächlichen Exportzahlen widerspiegeln.
