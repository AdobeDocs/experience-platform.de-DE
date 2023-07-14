---
keywords: Profilattribute aktivieren;Ziele aktivieren;Daten aktivieren;E-Mail-Marketing-Ziele aktivieren;Cloud-Speicher-Ziele aktivieren
title: Aktivieren von Zielgruppen für Batch-Profil-Export-Ziele
type: Tutorial
description: Erfahren Sie, wie Sie die in Adobe Experience Platform vorhandenen Zielgruppen aktivieren können, indem Sie sie an profilbasierte Batch-Ziele senden.
exl-id: 82ca9971-2685-453a-9e45-2001f0337cda
source-git-commit: 37819b5a6480923686d327e30b1111ea29ae71da
workflow-type: tm+mt
source-wordcount: '3961'
ht-degree: 65%

---


# Aktivieren von Zielgruppen für Batch-Profil-Export-Ziele

>[!IMPORTANT]
> 
> * So aktivieren Sie Zielgruppen und aktivieren die [Zuordnungsschritt](#mapping) des Workflows benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions).
> * So aktivieren Sie Zielgruppen, ohne die [Zuordnungsschritt](#mapping) des Workflows benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Segment ohne Zuordnung aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions).
> 
> Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.
>
> Bei einigen Kundinnen und Kunden, die am Beta-Programm mit der verbesserten Dateiexportfunktion teilnehmen, erfolgt der neue **[!UICONTROL Zuordnungsschritt]** im Rahmen ihres Aktivierungs-Workflows zu den [neuen Beta-Cloud-Speicherzielen](/help/release-notes/2022/october-2022.md#destinations). Beachten Sie die [bekannte Einschränkungen](#known-limitations) als Teil der -Version.

## Übersicht {#overview}

In diesem Artikel wird der Workflow erläutert, der zum Aktivieren von Zielgruppen in Adobe Experience Platform-Batch-profilbasierten Zielen wie Cloud-Speicher und E-Mail-Marketing-Zielen erforderlich ist.

## Voraussetzungen {#prerequisites}

Um Zielgruppen für Ziele aktivieren zu können, müssen Sie erfolgreich [mit Ziel verbunden](./connect-destination.md). Wenn Sie das noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

## Auswählen des Ziels {#select-destination}

1. Navigieren Sie zu **[!UICONTROL Verbindungen und Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Katalog]**.

   ![Abbildung mit hervorgehobenen Informationen zum Zugriff auf die Registerkarte „Zielkatalog“](../assets/ui/activate-batch-profile-destinations/catalog-tab.png)

1. Auswählen **[!UICONTROL Aktivieren von Zielgruppen]** auf der Karte, die dem Ziel entspricht, in dem Sie Ihre Zielgruppen aktivieren möchten, wie in der Abbildung unten dargestellt.

   ![Bild mit der Schaltfläche Zielgruppen aktivieren](../assets/ui/activate-batch-profile-destinations/activate-audiences-button.png)

1. Wählen Sie die Zielverbindung aus, die Sie zum Aktivieren Ihrer Zielgruppen verwenden möchten, und wählen Sie dann **[!UICONTROL Nächste]**.

   ![Bild, das die Auswahl eines oder mehrerer Ziele zum Aktivieren von Zielgruppen für](../assets/ui/activate-batch-profile-destinations/select-destination.png)

1. Zum nächsten Abschnitt wechseln, um [Zielgruppen auswählen](#select-audiences).

## Audiences auswählen {#select-audiences}

Um die Zielgruppen auszuwählen, die Sie für das Ziel aktivieren möchten, aktivieren Sie die Kontrollkästchen links neben den Zielgruppennamen und wählen Sie **[!UICONTROL Nächste]**.

Je nach Herkunft können Sie aus mehreren Zielgruppentypen auswählen:

* **[!UICONTROL Segmentierungsdienst]**: Zielgruppen, die in der Experience Platform vom Segmentierungsdienst generiert wurden. Siehe [Segmentierungsdokumentation](../../segmentation/ui/overview.md) für weitere Details.
* **[!UICONTROL Benutzerdefinierter Upload]**: Zielgruppen, die außerhalb von Experience Platform generiert und als CSV-Dateien in Platform hochgeladen wurden. Weitere Informationen zu externen Zielgruppen finden Sie in der Dokumentation unter [Audience importieren](../../segmentation/ui/overview.md#import-audience).
* Andere Zielgruppentypen, die aus anderen Adobe-Lösungen stammen, z. B. [!DNL Audience Manager].

![Bild, das die Auswahl einer oder mehrerer Zielgruppen zur Aktivierung vorstellt](../assets/ui/activate-batch-profile-destinations/select-audiences.png)

>[!TIP]
>
>Auswählen von Audiences, die von **[!UICONTROL Benutzerdefinierte Uploads]** aktiviert automatisch die [Anreicherungsattribute auswählen](#select-enrichment-attributes) Schritt.

## Zielgruppenexport planen {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_schedule"
>title="Zeitplan"
>abstract="Verwenden Sie das Stiftsymbol, um den Dateiexporttyp (vollständige Dateien oder inkrementelle Dateien) und die Exporthäufigkeit festzulegen."

[!DNL Adobe Experience Platform] exportiert Daten für E-Mail-Marketing- und Cloud-Speicher-Ziele in Form von [!DNL CSV]-Dateien. Im **[!UICONTROL Planung]** können Sie den Zeitplan und die Dateinamen für jede Zielgruppe konfigurieren, die Sie exportieren. Die Konfiguration des Zeitplans ist obligatorisch, die Konfiguration des Dateinamens ist jedoch optional.

>[!IMPORTANT]
>
>[!DNL Adobe Experience Platform] teilt die Exportdateien automatisch mit 5 Millionen Datensätzen (Zeilen) pro Datei auf. Jede Zeile stellt ein Profil dar.
>
>Bei aufgeteilten Dateien wird eine Nummer an den Namen angehängt, die anzeigt, dass die Datei Teil eines größeren Exports ist, z. B. `filename.csv`, `filename_2.csv`, `filename_3.csv`.

Wählen Sie die **[!UICONTROL Zeitplan erstellen]** -Schaltfläche, die der Zielgruppe entspricht, die Sie an Ihr Ziel senden möchten.

![Abbildung mit hervorgehobener Schaltfläche „Zeitplan erstellen“](../assets/ui/activate-batch-profile-destinations/create-schedule-button.png)

### Exportieren von vollständigen Dateien {#export-full-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_exportoptions"
>title="Dateiexportoptionen"
>abstract="Auswählen **Exportieren von vollständigen Dateien** um eine vollständige Momentaufnahme aller Profile zu exportieren, die für die Zielgruppe qualifiziert sind. Auswählen **Inkrementelle Dateien exportieren** um nur die Profile zu exportieren, die sich seit dem letzten Export für die Audience qualifiziert haben. <br> Der erste inkrementelle Dateiexport umfasst alle Profile, die sich für die Zielgruppe qualifizieren und als Aufstockung fungieren. Zukünftige inkrementelle Dateien enthalten nur die Profile, die sich seit dem ersten inkrementellen Dateiexport für die Zielgruppe qualifiziert haben."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=de#export-incremental-files" text="Exportieren von inkrementellen Dateien"

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_aftersegmentevaluation"
>title="Aktivieren nach Zielgruppenbewertung"
>abstract="Die Aktivierung erfolgt unmittelbar nach Abschluss des täglichen Segmentierungsvorgangs. Dadurch wird sichergestellt, dass die aktuellen Profile exportiert werden."

>[!CONTEXTUALHELP]
>id="platform_destinations_activationchaining_scheduled"
>title="Geplante Aktivierung"
>abstract="Die Aktivierung erfolgt zu einer festen Tageszeit."

Auswählen **[!UICONTROL Exportieren von vollständigen Dateien]** , um den Dateiexport mit einer vollständigen Momentaufnahme aller Profilqualifikationen für die ausgewählte Audience Trigger.

![Abbildung der Benutzeroberfläche mit aktiviertem Umschalter „Vollständige Dateien exportieren“](../assets/ui/activate-batch-profile-destinations/export-full-files.png)

1. Verwenden Sie den **[!UICONTROL Häufigkeitsselektor]** zur Auswahl der Exportfrequenz:

   * **[!UICONTROL Einmal]**: plant einen einmaligen, bedarfsgesteuerten Export einer vollständigen Datei.
   * **[!UICONTROL Täglich]**: plant vollständige Dateiexporte einmal täglich zum angegebenen Zeitpunkt.

1. Verwenden Sie die **[!UICONTROL Zeit]** umschalten, um festzulegen, ob der Export unmittelbar nach der Zielgruppenbewertung oder auf geplanter Basis zu einem bestimmten Zeitpunkt erfolgen soll. Bei Auswahl der Option **[!UICONTROL Geplant]** können Sie mit dem Selektor die Tageszeit für den Export im [!DNL UTC]-Format wählen.

   >[!NOTE]
   >
   >Die **[!UICONTROL Nach Segmentbewertung]** Die unten beschriebene Option steht nur zur Auswahl von Beta-Kunden zur Verfügung.

   Verwenden Sie die Option **[!UICONTROL Nach der Segmentevaluierung]**, damit der Aktivierungsvorgang unmittelbar nach Abschluss des täglichen Platform-Batch-Segmentierungsvorgangs ausgeführt wird. Mit dieser Option wird sichergestellt, dass bei Ausführung des Aktivierungsauftrags die aktuellsten Profile nach Ihrem Ziel exportiert werden.

   <!-- Batch segmentation currently runs at {{insert time of day}} and lasts for an average {{x hours}}. Adobe reserves the right to modify this schedule. -->

   ![Abbildung mit hervorgehobener Option „Nach der Segmentevaluierung“ im Aktivierungsfluss für Batch-Ziele](../assets/ui/activate-batch-profile-destinations/after-segment-evaluation-option.png)
Verwenden Sie die Option **[!UICONTROL Geplant]**, damit der Aktivierungsvorgang zu einem festen Zeitpunkt ausgeführt wird. Mit dieser Option wird sichergestellt, dass Experience Platform-Profildaten täglich zur gleichen Zeit exportiert werden. Je nachdem, ob der Batch-Segmentierungsauftrag vor dem Start des Aktivierungsauftrags abgeschlossen wurde, sind die exportierten Profile jedoch möglicherweise nicht die aktuellsten.

   ![Abbildung mit hervorgehobener Option „Geplant“ im Aktivierungsfluss für Batch-Ziele und Anzeige der Zeitauswahl](../assets/ui/activate-batch-profile-destinations/scheduled-option.png)

   >[!IMPORTANT]
   >
   >Aufgrund der Art und Weise, wie interne Experience Platform-Prozesse konfiguriert werden, enthält der erste inkrementelle oder vollständige Dateiexport möglicherweise nicht alle Aufstockungsdaten. <br> <br> Um den vollständigen und aktuellsten Datenexport für die Aufstockung sowohl für vollständige als auch für inkrementelle Dateien sicherzustellen, empfiehlt Adobe, die erste Dateiexportzeit nach 12:00 Uhr GMT des folgenden Tages festzulegen. Diese Einschränkung wird in zukünftigen Versionen behoben.

1. Verwenden Sie den **[!UICONTROL Datumsselektor]**, um den Tag oder das Intervall auszuwählen, an dem der Export stattfinden soll. Für tägliche Exporte empfiehlt es sich, Ihr Start- und Enddatum so festzulegen, dass es der Dauer Ihrer Kampagnen auf Ihren nachgelagerten Plattformen entspricht.

   >[!IMPORTANT]
   >
   > Bei der Auswahl eines Exportintervalls wird der letzte Tag des Intervalls nicht in die Exporte einbezogen. Wenn Sie beispielsweise ein Intervall vom 4. bis 11. Januar auswählen, findet der letzte Dateiexport am 10. Januar statt.

1. Klicken Sie auf **[!UICONTROL Erstellen]**, um den Zeitplan zu speichern.

### Exportieren von inkrementellen Dateien {#export-incremental-files}

Auswählen **[!UICONTROL Inkrementelle Dateien exportieren]** um einen Export Trigger, bei dem die erste Datei eine vollständige Momentaufnahme aller Profilqualifikationen für die ausgewählte Zielgruppe ist und nachfolgende Dateien seit dem letzten Export inkrementelle Profilqualifikationen sind.

>[!IMPORTANT]
>
>Die erste exportierte inkrementelle Datei enthält alle Profile, die sich für eine Zielgruppe qualifizieren und als Aufstockung fungieren.

![Abbildung der Benutzeroberfläche mit aktiviertem Umschalter „Inkrementelle Dateien exportieren“](../assets/ui/activate-batch-profile-destinations/export-incremental-files.png)

1. Verwenden Sie den **[!UICONTROL Häufigkeitsselektor]** zur Auswahl der Exportfrequenz:

   * **[!UICONTROL Täglich]**: plant inkrementelle Dateiexporte einmal täglich zum angegebenen Zeitpunkt.
   * **[!UICONTROL Stündlich]**: plant inkrementelle Dateiexporte alle 3, 6, 8 oder 12 Stunden.

1. Verwenden Sie den **[!UICONTROL Zeitselektor]** zur Auswahl der Tageszeit im [!DNL UTC]-Format, zu der der Export erfolgen soll.

   >[!IMPORTANT]
   >
   >Aufgrund der Art und Weise, wie interne Experience Platform-Prozesse konfiguriert werden, enthält der erste inkrementelle oder vollständige Dateiexport möglicherweise nicht alle Aufstockungsdaten. <br> <br> Um den vollständigen und aktuellsten Datenexport für die Aufstockung sowohl für vollständige als auch für inkrementelle Dateien sicherzustellen, empfiehlt Adobe, die erste Dateiexportzeit nach 12:00 Uhr GMT des folgenden Tages festzulegen. Diese Einschränkung wird in zukünftigen Versionen behoben.

1. Verwenden Sie den **[!UICONTROL Datumsselektor]**, um das Intervall auszuwählen, in dem der Export stattfinden soll. Es empfiehlt sich, Ihr Start- und Enddatum so festzulegen, dass es der Dauer Ihrer Kampagnen auf Ihren nachgelagerten Plattformen entspricht.

   >[!IMPORTANT]
   >
   >Der letzte Tag des Intervalls ist nicht in den Exporten enthalten. Wenn Sie beispielsweise ein Intervall vom 4. bis 11. Januar auswählen, findet der letzte Dateiexport am 10. Januar statt.

1. Klicken Sie auf **[!UICONTROL Erstellen]**, um den Zeitplan zu speichern.

### Konfigurieren der Dateinamen {#file-names}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_filename"
>title="Konfigurieren des Dateinamens"
>abstract="Bei dateibasierten Zielen wird pro Zielgruppe ein eindeutiger Dateiname generiert. Verwenden Sie den Dateinamen-Editor, um einen eindeutigen Dateinamen zu erstellen und zu bearbeiten oder den Standardnamen beizubehalten."

Bei den meisten Zielen bestehen die Standarddateinamen aus Zielname, Zielgruppen-ID und einem Datums- und Uhrzeitindikator. Sie können beispielsweise Ihre exportierten Dateinamen bearbeiten, um zwischen verschiedenen Kampagnen zu unterscheiden, oder die Datenexportzeit an die Dateien anhängen zu lassen. Beachten Sie, dass manche Zielentwickler möglicherweise festlegen, dass für ihre Ziele andere Optionen zum Anhängen von standardmäßigen Dateinamen angezeigt werden.

Um ein modales Fenster zu öffnen und die Dateinamen zu bearbeiten, wählen Sie das Stiftsymbol aus. Dateinamen sind auf 255 Zeichen begrenzt.

>[!NOTE]
>
>Die folgende Abbildung zeigt, wie Dateinamen für [!DNL Amazon S3]-Ziele bearbeitet werden können, aber der Vorgang ist für alle Batch-Ziele identisch (z. B. SFTP, [!DNL Azure Blob Storage] oder [!DNL Google Cloud Storage]).

![Abbildung mit hervorgehobenem Stiftsymbol zum Konfigurieren von Dateinamen](../assets/ui/activate-batch-profile-destinations/configure-name.png)

Im Dateinamen-Editor können Sie verschiedene Komponenten auswählen, die zum Dateinamen hinzugefügt werden sollen.

![Abbildung mit allen verfügbaren Dateinamenoptionen](../assets/ui/activate-batch-profile-destinations/activate-workflow-configure-step-2.png)

Zielname und Zielgruppen-ID können nicht aus Dateinamen entfernt werden. Zusätzlich zu diesen Optionen können Sie die folgenden Optionen hinzufügen:

| Dateinamenoption | Beschreibung |
|---------|----------|
| **[!UICONTROL Zielgruppenname]** | Der Name der exportierten Zielgruppe. |
| **[!UICONTROL Datum und Uhrzeit]** | Wählen Sie zwischen dem Hinzufügen von `MMDDYYYY_HHMMSS` oder einen UNIX-10-stelligen Zeitstempel der Zeit, zu der die Dateien generiert werden. Wählen Sie eine dieser Optionen aus, wenn für Ihre Dateien bei jedem inkrementellen Export ein dynamischer Dateiname erstellt werden soll. |
| **[!UICONTROL Benutzerdefinierter Text]** | Beliebiger benutzerdefinierter Text, den Sie den Dateinamen hinzufügen möchten. |
| **[!UICONTROL Ziel-ID]** | Die ID des Ziel-Datenflusses, den Sie zum Exportieren der Zielgruppe verwenden. <br> **Hinweis**: Diese Option zum Anhängen von Dateinamen steht nur Beta-Kundinnen und -Kunden zur Verfügung, die am Beta-Programm mit der verbesserten Dateiexportfunktion teilnehmen. Wenden Sie sich an den Adobe-Support-Mitarbeiter oder die Kundenunterstützung, wenn Sie Zugang zum Beta-Programm erhalten möchten. |
| **[!UICONTROL Zielname]** | Der Name des Ziel-Datenflusses, den Sie zum Exportieren der Zielgruppe verwenden. <br> **Hinweis**: Diese Option zum Anhängen von Dateinamen steht nur Beta-Kundinnen und -Kunden zur Verfügung, die am Beta-Programm mit der verbesserten Dateiexportfunktion teilnehmen. Wenden Sie sich an den Adobe-Support-Mitarbeiter oder die Kundenunterstützung, wenn Sie Zugang zum Beta-Programm erhalten möchten. |
| **[!UICONTROL Organisationsname]** | Ihr Organisationsname in Experience Platform. <br> **Hinweis**: Diese Option zum Anhängen von Dateinamen steht nur Beta-Kundinnen und -Kunden zur Verfügung, die am Beta-Programm mit der verbesserten Dateiexportfunktion teilnehmen. Wenden Sie sich an den Adobe-Support-Mitarbeiter oder die Kundenunterstützung, wenn Sie Zugang zum Beta-Programm erhalten möchten. |
| **[!UICONTROL Sandbox-Name]** | Die Kennung der Sandbox, die Sie zum Exportieren der Audience verwenden. <br> **Hinweis**: Diese Option zum Anhängen von Dateinamen steht nur Beta-Kundinnen und -Kunden zur Verfügung, die am Beta-Programm mit der verbesserten Dateiexportfunktion teilnehmen. Wenden Sie sich an den Adobe-Support-Mitarbeiter oder die Kundenunterstützung, wenn Sie Zugang zum Beta-Programm erhalten möchten. |

{style="table-layout:auto"}

Klicken Sie auf **[!UICONTROL Änderungen übernehmen]**, um Ihre Auswahl zu bestätigen.

>[!IMPORTANT]
> 
>Wenn Sie die Komponente **[!UICONTROL Datum und Uhrzeit]** nicht verwenden, sind die Dateinamen statisch und die neue exportierte Datei überschreibt die vorherige Datei an Ihrem Speicherort bei jedem Export. Diese Option wird bei der Ausführung eines wiederkehrenden Importvorgangs von einem Speicherort zu einer E-Mail-Marketing-Plattform empfohlen.

Nachdem Sie alle Ihre Zielgruppen konfiguriert haben, wählen Sie **[!UICONTROL Nächste]** , um fortzufahren.

## Auswählen der Profilattribute {#select-attributes}

Bei profilbasierten Zielen müssen Sie die Profilattribute auswählen, die Sie an das Ziel senden möchten.

1. Wählen Sie auf der Seite **[!UICONTROL Attribute auswählen]** die Option **[!UICONTROL Neues Feld hinzufügen]**.

   ![Abbildung mit hervorgehobener Schaltfläche „Neues Feld hinzufügen“](../assets/ui/activate-batch-profile-destinations/add-new-field.png)

1. Wählen Sie den Pfeil rechts neben dem Eintrag **[!UICONTROL Schemafeld]**.

   ![Abbildung mit hervorgehobenen Informationen zur Auswahl eines Quellfelds](../assets/ui/activate-batch-profile-destinations/select-source-field.png)

1. Im **[!UICONTROL Feld auswählen]** Seite, wählen Sie die XDM-Attribute oder Identitäts-Namespaces aus, die Sie an das Ziel senden möchten, und wählen Sie **[!UICONTROL Auswählen]**.

   ![Abbildung mit den verschiedenen als Quellfelder verfügbaren Feldern](../assets/ui/activate-batch-profile-destinations/target-field-page.png)

1. Um weitere Zuordnungen hinzuzufügen, wiederholen Sie die Schritte 1 bis 3. 

>[!NOTE]
>
> Adobe Experience Platform füllt Ihre Auswahl vorab mit vier empfohlenen, häufig verwendeten Attributen aus Ihrem Schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

![Bild mit vorausgefüllten empfohlenen Attributen im Zuordnungsschritt des Zielgruppenaktivierungs-Workflows.](../assets/ui/activate-batch-profile-destinations/prefilled-fields.png)

>[!IMPORTANT]
>
>Aufgrund einer bekannten Einschränkung können Sie das Fenster **[!UICONTROL Feld auswählen]** derzeit nicht verwenden, um `segmentMembership.status` zu Ihren Dateiexporten hinzuzufügen. Stattdessen müssen Sie den Wert manuell einfügen `xdm: segmentMembership.status` in das Schemafeld ein, wie unten dargestellt.
>
>![Bildschirmaufzeichnung, die die Problemumgehung für die Zielgruppenzugehörigkeit im Zuordnungsschritt des Aktivierungs-Workflows anzeigt.](..//assets/ui/activate-batch-profile-destinations/segment-membership.gif)

Dateiexporte variieren je nach dem, ob `segmentMembership.status` ausgewählt ist:
* Wenn das Feld `segmentMembership.status` ausgewählt ist, enthalten exportierte Dateien in der ersten vollständigen Momentaufnahme die **[!UICONTROL aktiven]** Mitglieder und in nachfolgenden inkrementellen Exporten die **[!UICONTROL aktiven]** und die **[!UICONTROL abgelaufenen]** Mitglieder.
* Wenn die Variable `segmentMembership.status` nicht ausgewählt ist, umfassen exportierte Dateien sowohl in der ersten vollständigen Momentaufnahme als auch in nachfolgenden inkrementellen Exporten nur die **[!UICONTROL aktiven]** Mitglieder.

### Obligatorische Attribute {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="Über obligatorische Attribute"
>abstract="Wählen Sie die XDM-Schemaattribute aus, die alle exportierten Profile enthalten sollen. Profile ohne den obligatorischen Schlüssel werden nicht an das Ziel exportiert. Wenn Sie keinen obligatorischen Schlüssel auswählen, werden alle qualifizierten Profile unabhängig von ihren Attributen exportiert."

Ein obligatorisches Attribut ist ein vom Benutzer aktiviertes Kontrollkästchen, mit dem sichergestellt wird, dass alle Profildatensätze das ausgewählte Attribut enthalten. Beispiel: alle exportierten Profile enthalten eine E-Mail-Adresse.

Sie können Attribute als obligatorisch markieren, um sicherzustellen, dass [!DNL Platform] nur die Profile exportiert, die das spezifische Attribut enthalten. Dies kann daher als eine zusätzliche Form des Filterns verwendet werden. Das Kennzeichnen eines Attributs als obligatorisch ist **nicht** erforderlich.

Wenn kein obligatorisches Attribut ausgewählt wird, werden alle qualifizierten Profile unabhängig von ihren Attributen exportiert.

Es wird empfohlen, dass eines der Attribute eine [eindeutige Kennung](../../destinations/catalog/email-marketing/overview.md#identity) aus Ihrem Schema ist. Weitere Informationen zu obligatorischen Attributen finden Sie im Abschnitt „Identität“ in der Dokumentation [E-Mail-Marketing-Ziele](../../destinations/catalog/email-marketing/overview.md#identity).

### Deduplizierungsschlüssel {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="Über Deduplizierungsschlüssel"
>abstract="Beseitigen Sie mehrfach vorkommende Datensätze desselben Profils in den Exportdateien, indem Sie einen Deduplizierungsschlüssel auswählen. Sie können einen einzelnen Namespace oder bis zu zwei XDM-Schemaattribute als Deduplizierungsschlüssel auswählen. Wenn Sie keinen Deduplizierungsschlüssel auswählen, sind in den Exportdateien möglicherweise doppelte Profileinträge enthalten."

Ein Deduplizierungsschlüssel ist ein benutzerdefinierter Primärschlüssel, der die Identität bestimmt, anhand derer Benutzer ihre Profile deduplizieren lassen möchten.

Deduplizierungsschlüssel verhindern die Möglichkeit, mehrere Datensätze desselben Profils in einer Exportdatei zu haben.

Es gibt drei Möglichkeiten, Deduplizierungsschlüssel in [!DNL Platform] zu verwenden:

* Verwenden eines einzelnen Identitäts-Namespace als [!UICONTROL Deduplizierungsschlüssel]
* Verwenden eines einzelnen Profilattributs aus einem [!DNL XDM]-Profil als [!UICONTROL Deduplizierungsschlüssel]
* Verwenden einer Kombination zweier Profilattribute aus einem [!DNL XDM]-Profil als zusammengesetzten Schlüssel

>[!IMPORTANT]
>
> Sie können einen einzelnen Identitäts-Namespace in ein Ziel exportieren, wobei der Namespace automatisch als Deduplizierungsschlüssel festgelegt wird. Das Senden mehrerer Namespaces an ein Ziel wird nicht unterstützt.
> 
> Sie können keine Kombination aus Identitäts-Namespaces und Profilattributen als Deduplizierungsschlüssel verwenden.

### Beispiel einer Deduplizierung {#deduplication-example}

Dieses Beispiel zeigt, wie die Deduplizierung je nach ausgewähltem Deduplizierungsschlüssel funktioniert.

Betrachten wir die beiden folgenden Profile.

**Profil A**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "realized",
        "lastQualificationTime": "2021-03-10 10:03:08"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "Doe",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

**Profil B**

```json
{
  "identityMap": {
    "Email": [
      {
        "id": "johndoe_1@example.com"
      },
      {
        "id": "johndoe_2@example.com"
      }
    ]
  },
  "segmentMembership": {
    "ups": {
      "fa5c4622-6847-4199-8dd4-8b7c7c7ed1d6": {
        "status": "realized",
        "lastQualificationTime": "2021-04-10 11:33:28"
      }
    }
  },
  "person": {
    "name": {
      "lastName": "D",
      "firstName": "John"
    }
  },
  "personalEmail": {
    "address": "johndoe@example.com"
  }
}
```

### Deduplizierungs-Anwendungsfall 1: keine Deduplizierung {#deduplication-use-case-1}

Ohne Deduplizierung würde die Exportdatei die folgenden Einträge enthalten.

| personalEmail | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | Doe |
| johndoe@example.com | John | D |


### Deduplizierungs-Anwendungsfall 2: Deduplizierung basierend auf Identitäts-Namespace {#deduplication-use-case-2}

Unter der Annahme einer Deduplizierung durch den [!DNL Email]-Namespace würde die Exportdatei die folgenden Einträge enthalten. Profil B ist das neueste Profil, das sich für die Zielgruppe qualifiziert hat. Daher wird nur dieses exportiert.

| E-Mail* | personalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | John | D |
| johndoe_2@example.com | johndoe@example.com | John | D |

### Deduplizierungsanwendungsfall 3: Deduplizierung basierend auf einem einzigen Profilattribut {#deduplication-use-case-3}

Angenommen, die Deduplizierung würde anhand des Attributs des Typs `personal Email` erfolgen, dann würde die Exportdatei den folgenden Eintrag enthalten. Profil B ist das neueste Profil, das sich für die Zielgruppe qualifiziert hat. Daher wird nur dieses exportiert.

| personalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | D |


### Deduplizierungsanwendungsfall 4: Deduplizierung basierend auf zwei Profilattributen {#deduplication-use-case-4}

Angenommen, die Deduplizierung würde anhand des zusammengesetzten Schlüssels `personalEmail + lastName` erfolgen, dann würde die Exportdatei die folgenden Einträge enthalten.

| personalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | John |
| johndoe@example.com | Doe | John |


Adobe empfiehlt das Auswählen eines Identitäts-Namespace, z. B. einer [!DNL CRM ID] oder einer E-Mail-Adresse, als Deduplizierungsschlüssel, um sicherzustellen, dass alle Profildatensätze eindeutig identifiziert werden.

>[!NOTE]
> 
>Wenn Datennutzungsbeschriftungen auf bestimmte Felder innerhalb eines Datensatzes angewendet wurden (und nicht auf den gesamten Datensatz), erfolgt die Durchsetzung dieser Beschriftungen auf Feldebene bei der Aktivierung unter folgenden Bedingungen:
>
>* Die Felder werden in der Zielgruppendefinition verwendet.
>* Die Felder werden als projizierte Attribute für das Ziel der Zielgruppe konfiguriert.
>
> Wenn beispielsweise das Feld `person.name.firstName` über bestimmte Datennutzungsbeschriftungen verfügt, die im Konflikt mit der Marketing-Aktion des Ziels stehen, wird Ihnen im Überprüfungsschritt eine Verletzung der Datennutzungsrichtlinien angezeigt. Weitere Informationen finden Sie unter [Data Governance in Adobe Experience Platform](../../rtcdp/privacy/data-governance-overview.md#destinations).

## (Beta) Zuordnung {#mapping}

>[!IMPORTANT]
> 
>Ausgewählte Beta-Kundinnen und -Kunden profitieren von einem verbesserten **[!UICONTROL Zuordnungsschritt]**, der den weiter oben beschriebenen Schritt [Auswählen der Profilattribute](#select-attributes) ersetzt. Mit diesem neuen **[!UICONTROL Zuordnungsschritt]** können Sie die Header exportierter Dateien bearbeiten und ihnen beliebige benutzerdefinierte Namen geben.
> 
> Die Funktionalität und Dokumentation können sich ändern. Wenden Sie sich an den Adobe-Support-Mitarbeiter oder die Kundenunterstützung, wenn Sie Zugang zu diesem Beta-Programm erhalten möchten.

In diesem Schritt müssen Sie die Profilattribute auswählen, die Sie zu den an das Ziel exportierten Dateien hinzufügen möchten. So wählen Sie Profilattribute und Identitäten für den Export aus:

1. Wählen Sie auf der Seite **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neues Feld hinzufügen]** aus.

   ![Hervorgehobene Steuerung „Neues Feld hinzufügen“ im Zuordnungs-Workflow](../assets/ui/activate-batch-profile-destinations/add-new-field-mapping.png)

1. Wählen Sie den Pfeil rechts neben dem Eintrag **[!UICONTROL Quellfeld]** aus.

   ![Hervorgehobene Steuerung zur Auswahl des Quellfelds im Zuordnungs-Workflow](../assets/ui/activate-batch-profile-destinations/select-source-field.png)

1. Wählen Sie auf der Seite **[!UICONTROL Quellfeld auswählen]** die Profilattribute und Identitäten aus, die Sie in die exportierten Dateien am Ziel einbeziehen möchten, und wählen Sie dann **[!UICONTROL Auswählen]**.

   >[!TIP]
   > 
   >Sie können das Suchfeld verwenden, um die Auswahl einzugrenzen, wie in der Abbildung unten dargestellt.

   ![Modales Fenster mit Profilattributen, die an das Ziel exportiert werden können](../assets/ui/activate-batch-profile-destinations/select-source-field-modal.png)


1. Das für den Export ausgewählte Feld wird jetzt in der Zuordnungsansicht angezeigt. Bei Bedarf können Sie den Namen des Headers in der exportierten Datei bearbeiten. Wählen Sie dazu das Symbol im Zielfeld aus.

   ![Modales Fenster mit Profilattributen, die an das Ziel exportiert werden können](../assets/ui/activate-batch-profile-destinations/mapping-step-select-target-field.png)

1. Geben Sie auf der Seite **[!UICONTROL Zielfeld auswählen]** den gewünschten Namen für den Header in der exportierten Datei ein und wählen Sie **[!UICONTROL Auswählen]**.

   ![Modales Fenster mit eingegebenem Anzeigenamen für einen Header](../assets/ui/activate-batch-profile-destinations/select-target-field-mapping.png)

1. Das für den Export ausgewählte Feld wird jetzt in der Zuordnungsansicht mit dem bearbeiteten Header in der exportierten Datei angezeigt.

   ![Modales Fenster mit Profilattributen, die an das Ziel exportiert werden können](../assets/ui/activate-batch-profile-destinations/select-target-field-updated.png)

1. (Optional) Sie können das exportierte Feld als [obligatorischen Schlüssel](#mandatory-keys) oder [Deduplizierungsschlüssel](#deduplication-keys) festlegen.

   ![Modales Fenster mit Profilattributen, die an das Ziel exportiert werden können](../assets/ui/activate-batch-profile-destinations/select-mandatory-deduplication-key.png)

1. Um weitere Felder zum Exportieren hinzuzufügen, wiederholen Sie die obigen Schritte.

### Bekannte Einschränkungen {#known-limitations}

Die neue Seite **[!UICONTROL Zuordnung]** weist die folgenden bekannten Einschränkungen auf:

#### Das Attribut &quot;Zielgruppenzugehörigkeit&quot;kann nicht über den Zuordnungs-Workflow ausgewählt werden

Aufgrund einer bekannten Einschränkung können Sie das Fenster **[!UICONTROL Feld auswählen]** derzeit nicht verwenden, um `segmentMembership.status` zu Ihren Dateiexporten hinzuzufügen. Stattdessen müssen Sie den Wert `xdm: segmentMembership.status` wie unten dargestellt manuell in das Schemafeld einfügen.

![Bildschirmaufzeichnung, die die Problemumgehung für die Zielgruppenzugehörigkeit im Zuordnungsschritt des Aktivierungs-Workflows anzeigt.](../assets/ui/activate-batch-profile-destinations/segment-membership-mapping-step.gif)

Dateiexporte variieren auf folgende Weise, je nachdem, ob `segmentMembership.status` ausgewählt ist:
* Wenn das Feld `segmentMembership.status` ausgewählt ist, enthalten exportierte Dateien in der ersten vollständigen Momentaufnahme die **[!UICONTROL aktiven]** Mitglieder und in nachfolgenden inkrementellen Exporten die **[!UICONTROL aktiven]** und die **[!UICONTROL abgelaufenen]** Mitglieder.
* Wenn die Variable `segmentMembership.status` nicht ausgewählt ist, umfassen exportierte Dateien sowohl in der ersten vollständigen Momentaufnahme als auch in nachfolgenden inkrementellen Exporten nur die **[!UICONTROL aktiven]** Mitglieder.

#### Identitäts-Namespaces derzeit nicht für Exporte auswählbar

Die Auswahl von Identitäts-Namespaces für den Export, wie in der Abbildung unten dargestellt, wird derzeit nicht unterstützt. Die Auswahl von Identitäts-Namespaces für den Export führt zu einem Fehler im **[!UICONTROL Überprüfungsschritt]**.

![Nicht unterstützte Zuordnung mit Identitätsexporten](../assets/ui/activate-batch-profile-destinations/unsupported-identity-mapping.png)

Wenn Sie zu Ihren exportierten Dateien während der Beta-Phase Identitäts-Namespaces hinzufügen müssen, haben Sie zur temporären Problemumgehung folgende Möglichkeiten:
* Verwenden Sie die Legacy-Cloud-Speicherziele für die Datenflüsse, bei denen Sie Identitäts-Namespaces in die Exporte einbeziehen möchten.
* Laden Sie Identitäten als Attribute in Experience Platform hoch, um sie dann in Ihre Cloud-Speicherziele zu exportieren.

## Anreicherungsattribute auswählen {#select-enrichment-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_exclude_enrichment_attributes"
>title="Ausschließen von Anreicherungsattributen"
>abstract="Aktivieren Sie diese Option, um die Profile aus den ausgewählten benutzerdefinierten, hochgeladenen Zielgruppen zu exportieren und dabei alle zugehörigen Attribute auszuschließen."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html#select-enrichment-attributes" text="Weitere Informationen finden Sie in der Dokumentation"

>[!IMPORTANT]
>
>Dieser Schritt wird nur angezeigt, wenn Sie **[!UICONTROL Benutzerdefinierter Upload]** Zielgruppen während der [Zielgruppenauswahl](#select-audiences) Schritt.

Anreicherungsattribute entsprechen benutzerdefinierten, hochgeladenen Zielgruppen, die in Experience Platform als **[!UICONTROL Benutzerdefinierte Uploads]**. In diesem Schritt können Sie für jede ausgewählte externe Zielgruppe auswählen, welche Attribute Sie an Ihr Ziel exportieren möchten.

![UI-Bild, das den Auswahlschritt für Anreicherungsattribute anzeigt.](../assets/ui/activate-batch-profile-destinations/select-enrichment-attributes-step.png)

Gehen Sie wie folgt vor, um Anreicherungsattribute für jede externe Zielgruppe auszuwählen:

1. Im **[!UICONTROL Anreicherungsattribute]** auswählen, wählen Sie die ![Schaltfläche &quot;Bearbeiten&quot;](../assets/ui/activate-batch-profile-destinations/edit-button.svg) Schaltfläche (Bearbeiten).
2. Auswählen **[!UICONTROL Anreicherungsattribut hinzufügen]**. Ein neues leeres Schemafeld wird angezeigt.
   ![UI-Bild, das den modalen Bildschirm mit den Anreicherungsattributen anzeigt.](../assets/ui/activate-batch-profile-destinations/add-enrichment-attribute.png)
3. Wählen Sie die Schaltfläche rechts neben dem leeren Feld aus, um den Bildschirm zur Feldauswahl zu öffnen.
4. Wählen Sie die Attribute aus, die Sie für die Zielgruppe exportieren möchten.
   ![UI-Bild, das die Liste der Anreicherungsattribute anzeigt.](../assets/ui/activate-batch-profile-destinations/select-enrichment-attributes.png)
5. Nachdem Sie alle Attribute hinzugefügt haben, die Sie exportieren möchten, wählen Sie **[!UICONTROL Speichern und schließen]**.
6. Wiederholen Sie diese Schritte für jede externe Zielgruppe.

Wenn Sie externe Zielgruppen für Ihre Ziele aktivieren möchten, ohne ein Attribut zu exportieren, aktivieren Sie die **[!UICONTROL Ausschließen von Anreicherungsattributen]** umschalten. Diese Option exportiert die Profile aus externen Zielgruppen, aber keines der entsprechenden Attribute wird an Ihr Ziel gesendet.

![UI-Bild, das den Umschalter zum Ausschließen von Anreicherungsattributen anzeigt.](../assets/ui/activate-batch-profile-destinations/exclude-enrichment-attributes.png)

Auswählen **[!UICONTROL Nächste]** , um zum [Überprüfen](#review) Schritt.

## Überprüfung {#review}

Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

![Auswahlzusammenfassung im Überprüfungsschritt.](../assets/ui/activate-batch-profile-destinations/review.png)

### Auswertung der Einverständnisrichtlinie {#consent-policy-evaluation}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_viewApplicableConsentPolicies"
>title="Aktuelle Einverständnisrichtlinien anzeigen"
>abstract="Wenn Ihr Unternehmen **Adobe Healthcare Shield** oder **Adobe Privacy &amp; Security Shield** erworben hat, wählen Sie **[!UICONTROL Aktuelle Einverständnisrichtlinien anzeigen]** aus, um zu sehen, welche Einverständnisrichtlinien angewendet werden und wie viele Profile in der Aktivierung enthalten sind. Diese Option ist deaktiviert, wenn Ihr Unternehmen keinen Zugriff auf die oben genannten Produkte hat."

Wenn Ihr Unternehmen **Adobe Healthcare Shield** oder **Adobe Privacy &amp; Security Shield** erworben hat, wählen Sie **[!UICONTROL Aktuelle Einverständnisrichtlinien anzeigen]** aus, um zu sehen, welche Einverständnisrichtlinien angewendet werden und wie viele Profile in der Aktivierung enthalten sind. Informationen [Bewertung der Einwilligungsrichtlinie](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) für weitere Informationen.

### Prüfungen von Datennutzungsrichtlinien {#data-usage-policy-checks}

Im **[!UICONTROL Überprüfen]** -Schritt, überprüft Experience Platform auch auf Verstöße gegen Datennutzungsrichtlinien. Nachstehend ist ein Beispiel angegeben, bei dem eine Richtlinie verletzt wird. Sie können den Aktivierungs-Workflow für die Zielgruppe erst abschließen, nachdem Sie den Verstoß behoben haben. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Verstöße gegen Datennutzungsrichtlinien](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) im Abschnitt Data Governance-Dokumentation .

![Verletzung von Datenrichtlinien](../assets/common/data-policy-violation.png)

### Filtern von Zielgruppen {#filter-audiences}

Außerdem können Sie in diesem Schritt die verfügbaren Filter auf der Seite verwenden, um nur die Zielgruppen anzuzeigen, deren Zeitplan oder Zuordnung im Rahmen dieses Workflows aktualisiert wurde. Sie können auch umschalten, welche Tabellenspalten angezeigt werden sollen.

![Bildschirmaufzeichnung mit den verfügbaren Zielgruppenfiltern im Überprüfungsschritt.](../assets/ui/activate-batch-profile-destinations/filter-audiences-batch-review.gif)

Wenn Sie mit Ihrer Auswahl zufrieden sind und keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Beenden]** , um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

## Überprüfung der Zielgruppenaktivierung {#verify}

Bei E-Mail-Marketing- und Cloud-Speicher-Zielen erstellt Adobe Experience Platform eine Datei des Typs `.csv` am von Ihnen angegebenen Speicherort. Wahrscheinlich wird eine neue Datei an Ihrem Speicherort entsprechend dem Zeitplan erstellt, den Sie im Workflow festgelegt haben. Das standardmäßige Dateiformat ist unten dargestellt, Sie können jedoch [Bearbeiten der Komponenten des Dateinamens](#file-names):
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

Wenn Sie beispielsweise eine tägliche Exportfrequenz auswählen, könnten die Dateien, die Sie an drei aufeinander folgenden Tagen erhalten würden, wie folgt aussehen:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

Das Vorhandensein dieser Dateien an Ihrem Speicherort bestätigt die erfolgreiche Aktivierung. Um zu verstehen, wie die exportierten Dateien strukturiert sind, können Sie ein [Beispiel für eine CSV-Datei herunterladen](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). Diese Beispieldatei enthält die Profilattribute `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear` und `personalEmail.address`.
