---
keywords: Profilattribute aktivieren; Ziele aktivieren; Daten aktivieren; E-Mail-Marketing-Ziele aktivieren; Aktivieren von Cloud-Speicher-Zielen
title: Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele
type: Tutorial
seo-title: Activate audience data to batch profile export destinations
description: Erfahren Sie, wie Sie die Zielgruppendaten aktivieren, die Sie in Adobe Experience Platform haben, indem Sie Segmente an Batch-Profil-basierte Ziele senden.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by sending segments to batch profile-based destinations.
exl-id: 82ca9971-2685-453a-9e45-2001f0337cda
source-git-commit: 551b07eac95b560950fe2d70fd2a981ae3a29252
workflow-type: tm+mt
source-wordcount: '2188'
ht-degree: 7%

---

# Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele

## Übersicht {#overview}

In diesem Artikel wird der Workflow erläutert, der zum Aktivieren von Zielgruppendaten in Adobe Experience Platform-Batch-profilbasierten Zielen wie Cloud-Speicher und E-Mail-Marketing-Zielen erforderlich ist.

## Voraussetzungen {#prerequisites}

Um Daten für Ziele aktivieren zu können, müssen Sie erfolgreich [mit Ziel verbunden](./connect-destination.md). Wenn Sie das noch nicht getan haben, gehen Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

## Ziel auswählen {#select-destination}

1. Navigieren Sie zu **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die **[!UICONTROL Katalog]** Registerkarte.

   ![Registerkarte &quot;Zielkatalog&quot;](../assets/ui/activate-batch-profile-destinations/catalog-tab.png)

1. Auswählen **[!UICONTROL Segmente aktivieren]** auf der Karte, die dem Ziel entspricht, an dem Sie Ihre Segmente aktivieren möchten, wie in der Abbildung unten dargestellt.

   ![Schaltfläche &quot;Segmente aktivieren&quot;](../assets/ui/activate-batch-profile-destinations/activate-segments-button.png)

1. Wählen Sie die Zielverbindung aus, die Sie zum Aktivieren Ihrer Segmente verwenden möchten, und wählen Sie dann **[!UICONTROL Nächste]**.

   ![Ziel auswählen](../assets/ui/activate-batch-profile-destinations/select-destination.png)

1. Zum nächsten Abschnitt wechseln, um [Segmente auswählen](#select-segments).

## Segmente auswählen {#select-segments}

Aktivieren Sie die Kontrollkästchen links neben den Segmentnamen, um die Segmente auszuwählen, die Sie für das Ziel aktivieren möchten, und wählen Sie dann **[!UICONTROL Nächste]**.

![Segmente auswählen](../assets/ui/activate-batch-profile-destinations/select-segments.png)


## Segmentexport planen {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_schedule"
>title="Zeitplan"
>abstract="Legen Sie den Dateiexporttyp (vollständige Dateien oder inkrementelle Dateien) und die Exportfrequenz fest."
>additional-url="https://www.adobe.com/go/destinations-profile-batch-en" text="Weitere Informationen finden Sie in der Dokumentation ."

[!DNL Adobe Experience Platform] Exportiert Daten für E-Mail-Marketing- und Cloud-Speicher-Ziele in Form von [!DNL CSV] Dateien. Im **[!UICONTROL Planung]** können Sie den Zeitplan und die Dateinamen für jedes Segment, das Sie exportieren, konfigurieren. Die Konfiguration des Zeitplans ist obligatorisch, die Konfiguration des Dateinamens ist jedoch optional.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] teilt die Exportdateien automatisch mit 5 Millionen Datensätzen (Zeilen) pro Datei auf. Jede Zeile stellt ein Profil dar.
>
>Dateinamen mit Aufspaltung werden mit einer Zahl angehängt, die angibt, dass die Datei Teil eines größeren Exports ist. Dies zeigt an: `filename.csv`, `filename_2.csv`, `filename_3.csv`.

Wählen Sie die **[!UICONTROL Zeitplan erstellen]** -Schaltfläche, die dem Segment entspricht, das Sie an Ihr Ziel senden möchten.

![Schaltfläche &quot;Zeitplan erstellen&quot;](../assets/ui/activate-batch-profile-destinations/create-schedule-button.png)

### Exportieren von vollständigen Dateien {#export-full-files}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_exportoptions"
>title="Dateiexportoptionen"
>abstract="Wählen Sie Vollständige Dateien exportieren aus, um eine vollständige Momentaufnahme aller Profile zu exportieren, die für das Segment qualifiziert sind. Wählen Sie Inkrementelle Dateien exportieren aus, um nur die Profile zu exportieren, die sich seit dem letzten Export für das Segment qualifiziert haben. Der erste inkrementelle Dateiexport umfasst alle Profile, die für das Segment qualifiziert sind, und dient als Aufstockung. Zukünftige inkrementelle Dateien enthalten nur die Profile, die sich seit dem ersten inkrementellen Dateiexport für das Segment qualifiziert haben."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#export-incremental-files" text="Inkrementelle Dateien exportieren"

Auswählen **[!UICONTROL Exportieren von vollständigen Dateien]** , um den Export einer Datei mit einer vollständigen Momentaufnahme aller Profilqualifikationen für das ausgewählte Segment Trigger.

![Exportieren von vollständigen Dateien](../assets/ui/activate-batch-profile-destinations/export-full-files.png)

1. Verwenden Sie die **[!UICONTROL Häufigkeit]** Auswahl zur Auswahl der Exportfrequenz:

   * **[!UICONTROL Einmal]**: einen einmaligen vollständigen Dateiexport bei Bedarf planen.
   * **[!UICONTROL Täglich]**: planen Sie vollständige Dateiexporte einmal täglich, jeden Tag und zum angegebenen Zeitpunkt.

1. Verwenden Sie die **[!UICONTROL Zeit]** Auswahl zur Auswahl der Tageszeit in [!DNL UTC] -Format, wann der Export erfolgen soll.

   >[!IMPORTANT]
   >
   >Aufgrund der Art und Weise, wie interne Experience Platform-Prozesse konfiguriert werden, enthält der erste inkrementelle oder vollständige Dateiexport möglicherweise nicht alle Aufstockungsdaten. <br> <br> Um einen vollständigen und aktuellsten Datenexport für die Aufstockung sowohl für vollständige als auch für inkrementelle Dateien sicherzustellen, empfiehlt Adobe, die erste Dateiexportzeit nach 22:00 Uhr GMT des folgenden Tages festzulegen. Diese Einschränkung wird in zukünftigen Versionen behoben.

1. Verwenden Sie die **[!UICONTROL Datum]** auswählen, um den Tag oder das Intervall auszuwählen, an dem der Export stattfinden soll. Für tägliche Exporte empfiehlt es sich, Ihr Start- und Enddatum so festzulegen, dass es der Dauer Ihrer Kampagnen auf Ihren nachgelagerten Plattformen entspricht.

   >[!IMPORTANT]
   >
   > Bei der Auswahl eines Exportintervalls wird der letzte Tag des Intervalls nicht in die Exporte einbezogen. Wenn Sie beispielsweise ein Intervall vom 4. bis 11. Januar auswählen, findet der letzte Dateiexport am 10. Januar statt.

1. Auswählen **[!UICONTROL Erstellen]** , um den Zeitplan zu speichern.


### Inkrementelle Dateien exportieren {#export-incremental-files}

Auswählen **[!UICONTROL Inkrementelle Dateien exportieren]** , um einen Export Trigger, bei dem die erste Datei eine vollständige Momentaufnahme aller Profilqualifikationen für das ausgewählte Segment darstellt und nachfolgende Dateien seit dem vorherigen Export inkrementelle Profilqualifikationen sind.

>[!IMPORTANT]
>
>Die erste exportierte inkrementelle Datei enthält alle Profile, die sich für ein Segment qualifizieren und als Aufstockung fungieren.

![Inkrementelle Dateien exportieren](../assets/ui/activate-batch-profile-destinations/export-incremental-files.png)

1. Verwenden Sie die **[!UICONTROL Häufigkeit]** Auswahl zur Auswahl der Exportfrequenz:

   * **[!UICONTROL Täglich]**: planen Sie den inkrementellen Dateiexport einmal täglich zum angegebenen Zeitpunkt.
   * **[!UICONTROL Stündlich]**: planen inkrementelle Dateiexporte alle 3, 6, 8 oder 12 Stunden.

1. Verwenden Sie die **[!UICONTROL Zeit]** Auswahl zur Auswahl der Tageszeit in [!DNL UTC] -Format, wann der Export erfolgen soll.

   >[!IMPORTANT]
   >
   >Aufgrund der Art und Weise, wie interne Experience Platform-Prozesse konfiguriert werden, enthält der erste inkrementelle oder vollständige Dateiexport möglicherweise nicht alle Aufstockungsdaten. <br> <br> Um einen vollständigen und aktuellsten Datenexport für die Aufstockung sowohl für vollständige als auch für inkrementelle Dateien sicherzustellen, empfiehlt Adobe, die erste Dateiexportzeit nach 22:00 Uhr GMT des folgenden Tages festzulegen. Diese Einschränkung wird in zukünftigen Versionen behoben.

1. Verwenden Sie die **[!UICONTROL Datum]** auswählen, um das Intervall auszuwählen, in dem der Export stattfinden soll. Es empfiehlt sich, Ihr Start- und Enddatum so festzulegen, dass es der Dauer Ihrer Kampagnen auf Ihren nachgelagerten Plattformen entspricht.

   >[!IMPORTANT]
   >
   >Der letzte Tag des Intervalls ist nicht in den Exporten enthalten. Wenn Sie beispielsweise ein Intervall vom 4. bis 11. Januar auswählen, findet der letzte Dateiexport am 10. Januar statt.

1. Auswählen **[!UICONTROL Erstellen]** , um den Zeitplan zu speichern.

### Dateinamen konfigurieren {#file-names}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_filename"
>title="Dateinamen konfigurieren"
>abstract="Bei dateibasierten Zielen wird pro Segment ein eindeutiger Dateiname generiert. Verwenden Sie den Dateinameneditor, um einen eindeutigen Dateinamen zu erstellen und zu bearbeiten oder den Standardnamen beizubehalten."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-batch-profile-destinations.html?lang=en#file-names" text="Weitere Informationen finden Sie in der Dokumentation ."

Die standardmäßigen Dateinamen bestehen aus Zielname, Segment-ID und einem Datums- und Uhrzeitindikator. Sie können beispielsweise Ihre exportierten Dateinamen bearbeiten, um zwischen verschiedenen Kampagnen zu unterscheiden oder die Datenexportzeit an die Dateien anhängen zu lassen.

Wählen Sie das Stiftsymbol aus, um ein modales Fenster zu öffnen und die Dateinamen zu bearbeiten. Dateinamen sind auf 255 Zeichen begrenzt.

![Dateinamen konfigurieren](../assets/ui/activate-batch-profile-destinations/configure-name.png)

Im Dateinamen-Editor können Sie verschiedene Komponenten auswählen, die zum Dateinamen hinzugefügt werden sollen.

![Optionen zum Bearbeiten von Dateinamen](../assets/ui/activate-batch-profile-destinations/activate-workflow-configure-step-2.png)

Zielname und Segment-ID können nicht aus Dateinamen entfernt werden. Zusätzlich können Sie Folgendes hinzufügen:

* **[!UICONTROL Segmentname]**: Sie können den Segmentnamen an den Dateinamen anhängen.
* **[!UICONTROL Datum und Uhrzeit]**: Wählen Sie zwischen dem Hinzufügen von `MMDDYYYY_HHMMSS` oder einen 10-stelligen Unix-Zeitstempel der Zeit, zu der die Dateien generiert werden. Wählen Sie eine dieser Optionen aus, wenn für Ihre Dateien bei jedem inkrementellen Export ein dynamischer Dateiname erstellt werden soll.
* **[!UICONTROL Benutzerdefinierter Text]**: Fügen Sie den Dateinamen benutzerdefinierten Text hinzu.

Auswählen **[!UICONTROL Änderungen anwenden]** um Ihre Auswahl zu bestätigen.

>[!IMPORTANT]
> 
>Wenn Sie die **[!UICONTROL Datum und Uhrzeit]** -Komponente verwenden, sind die Dateinamen statisch und die neue exportierte Datei überschreibt die vorherige Datei an Ihrem Speicherort bei jedem Export. Bei der Ausführung eines wiederkehrenden Importvorgangs von einem Speicherort zu einer E-Mail-Marketing-Plattform wird diese Option empfohlen.

Nachdem Sie alle Segmente konfiguriert haben, wählen Sie **[!UICONTROL Nächste]** , um fortzufahren.

## Profilattribute auswählen {#select-attributes}

Bei profilbasierten Zielen müssen Sie die Profilattribute auswählen, die Sie an das Ziel senden möchten.


1. Im **[!UICONTROL Attribute auswählen]** Seite, wählen Sie **[!UICONTROL Neues Feld hinzufügen]**.

   ![Neues Mapping hinzufügen](../assets/ui/activate-batch-profile-destinations/add-new-field.png)

1. Wählen Sie den Pfeil rechts neben dem **[!UICONTROL Schemafeld]** eingeben.

   ![Quellfeld auswählen](../assets/ui/activate-batch-profile-destinations/select-target-field.png)

1. Im **[!UICONTROL Feld auswählen]** Seite, wählen Sie die XDM-Attribute aus, die Sie an das Ziel senden möchten, und wählen Sie **[!UICONTROL Auswählen]**.

   ![Quellfeldseite auswählen](../assets/ui/activate-batch-profile-destinations/target-field-page.png)

1. Um weitere Zuordnungen hinzuzufügen, wiederholen Sie die Schritte 1 bis 3.

>[!NOTE]
>
> Adobe Experience Platform füllt Ihre Auswahl mit vier empfohlenen, häufig verwendeten Attributen aus Ihrem Schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Dateiexporte variieren auf folgende Weise, je nachdem, ob `segmentMembership.status` ausgewählt ist:
* Wenn die Variable `segmentMembership.status` ausgewählt ist, enthalten exportierte Dateien **[!UICONTROL Aktiv]** -Mitglieder in der ersten vollständigen Momentaufnahme und **[!UICONTROL Aktiv]** und **[!UICONTROL Abgelaufen]** Mitglieder in nachfolgenden inkrementellen Exporten.
* Wenn die Variable `segmentMembership.status` nicht ausgewählt ist, umfassen exportierte Dateien nur **[!UICONTROL Aktiv]** -Elemente in der ersten vollständigen Momentaufnahme und in nachfolgenden inkrementellen Exporten.

![empfohlene Attribute](../assets/ui/activate-batch-profile-destinations/mandatory-deduplication.png)

### Obligatorische Attribute {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="Über obligatorische Attribute"
>abstract="Wählen Sie die XDM-Schemaattribute aus, die alle exportierten Profile enthalten sollen. Profile ohne obligatorischen Schlüssel werden nicht an das Ziel exportiert. Wenn Sie keinen obligatorischen Schlüssel auswählen, werden alle qualifizierten Profile unabhängig von ihren Attributen exportiert."
>additional-url="http://www.adobe.com/go/destinations-mandatory-attributes-en" text="Weitere Informationen finden Sie in der Dokumentation ."

Ein obligatorisches Attribut ist ein benutzeraktiviertes Kontrollkästchen, mit dem sichergestellt wird, dass alle Profildatensätze das ausgewählte Attribut enthalten. Beispiel: alle exportierten Profile eine E-Mail-Adresse enthalten. &#x200B;

Sie können Attribute als obligatorisch markieren, um sicherzustellen, dass [!DNL Platform] exportiert nur die Profile, die das spezifische Attribut enthalten. Sie kann daher als zusätzliche Filterform verwendet werden. Kennzeichnen eines Attributs als obligatorisch **not** erforderlich.

Wenn kein obligatorisches Attribut ausgewählt wird, werden alle qualifizierten Profile unabhängig von ihren Attributen exportiert.

Es wird empfohlen, dass eines der Attribute eine [eindeutige Kennung](../../destinations/catalog/email-marketing/overview.md#identity) aus Ihrem Schema. Weitere Informationen zu obligatorischen Attributen finden Sie im Abschnitt Identität im [E-Mail-Marketing-Ziele](../../destinations/catalog/email-marketing/overview.md#identity) Dokumentation.

### Deduplizierungsschlüssel {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="Über Deduplizierungsschlüssel"
>abstract="Beseitigen Sie mehrere Datensätze desselben Profils in den Exportdateien, indem Sie einen Deduplizierungsschlüssel auswählen. Wählen Sie einen einzelnen Namespace oder bis zu zwei XDM-Schemaattribute als Deduplizierungsschlüssel aus. Wenn Sie keinen Deduplizierungsschlüssel auswählen, werden in den Exportdateien möglicherweise doppelte Profileinträge angezeigt."
>additional-url="http://www.adobe.com/go/destinations-deduplication-keys-en" text="Weitere Informationen finden Sie in der Dokumentation ."

Ein Deduplizierungsschlüssel ist ein benutzerdefinierter Primärschlüssel, der die Identität bestimmt, anhand derer Benutzer ihre Profile deduplizieren möchten. &#x200B;

Deduplizierungsschlüssel verhindern die Möglichkeit, mehrere Datensätze desselben Profils in einer Exportdatei zu haben.

Es gibt drei Möglichkeiten, Deduplizierungsschlüssel in [!DNL Platform]:

* Verwenden eines einzelnen Identitäts-Namespace als [!UICONTROL Deduplizierungsschlüssel]
* Verwenden eines einzelnen Profilattributs aus einem [!DNL XDM] Profil als [!UICONTROL Deduplizierungsschlüssel]
* Verwenden einer Kombination zweier Profilattribute aus einer [!DNL XDM] Profil als zusammengesetzten Schlüssel

>[!IMPORTANT]
>
> Sie können einen einzelnen Identitäts-Namespace in ein Ziel exportieren und der Namespace wird automatisch als Deduplizierungsschlüssel festgelegt. Das Senden mehrerer Namespaces an ein Ziel wird nicht unterstützt.
> 
> Sie können keine Kombination aus Identitäts-Namespaces und Profilattributen als Deduplizierungsschlüssel verwenden.

### Beispiel einer Deduplizierung {#deduplication-example}

Dieses Beispiel zeigt, wie Deduplizierung je nach ausgewähltem Deduplizierungsschlüssel funktioniert.

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
        "status": "existing",
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
        "status": "existing",
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

### Nutzungsszenario 1: Deduplizierung keine Deduplizierung {#deduplication-use-case-1}

Ohne Deduplizierung würde die Exportdatei die folgenden Einträge enthalten.

| personalEmail | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | Doe |
| johndoe@example.com | John | D |


### Anwendungsfall 2: Deduplizierung Deduplizierung basierend auf Identitäts-Namespace {#deduplication-use-case-2}

Angenommen, die Deduplizierung erfolgt durch die [!DNL Email] -Namespace, würde die Exportdatei die folgenden Einträge enthalten. Profil B ist das neueste Profil, das sich für das Segment qualifiziert hat. Daher wird nur dieses exportiert.

| E-Mail* | personalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | John | D |
| johndoe_2@example.com | johndoe@example.com | John | D |

### Nutzungsszenario 3: Deduplizierung Deduplizierung basierend auf einem einzelnen Profilattribut {#deduplication-use-case-3}

Angenommen, die Deduplizierung erfolgt durch die `personal Email` -Attribut enthalten würde, würde die Exportdatei den folgenden Eintrag enthalten. Profil B ist das neueste Profil, das sich für das Segment qualifiziert hat. Daher wird nur dieses exportiert.

| personalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | D |


### Anwendungsfall 4: Deduplizierung Deduplizierung basierend auf zwei Profilattributen {#deduplication-use-case-4}

Deduplizierung durch den zusammengesetzten Schlüssel `personalEmail + lastName`würde die Exportdatei die folgenden Einträge enthalten.

| personalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | John |
| johndoe@example.com | Doe | John |


Adobe empfiehlt die Auswahl eines Identitäts-Namespace, z. B. einer [!DNL CRM ID] oder eine E-Mail-Adresse als Deduplizierungsschlüssel verwenden, um sicherzustellen, dass alle Profildatensätze eindeutig identifiziert werden.

>[!NOTE]
> 
>Wenn Datennutzungsbezeichnungen auf bestimmte Felder in einem Datensatz angewendet wurden (und nicht auf den gesamten Datensatz), erfolgt die Durchsetzung dieser Feldbezeichnungen bei der Aktivierung unter folgenden Bedingungen:
>
>* Die Felder werden in der Segmentdefinition verwendet.
>* Die Felder werden als projizierte Attribute für das Ziel der Zielgruppe konfiguriert.

>
> Wenn beispielsweise das Feld `person.name.firstName` über bestimmte Datennutzungsbezeichnungen verfügt, die im Konflikt mit der Marketing-Aktion des Ziels stehen, wird Ihnen im Überprüfungsschritt eine Verletzung der Datennutzungsrichtlinien angezeigt. Weitere Informationen finden Sie unter [Data Governance in Adobe Experience Platform](../../rtcdp/privacy/data-governance-overview.md#destinations).

## Überprüfung {#review}

Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

>[!IMPORTANT]
>
>In diesem Schritt prüft Adobe Experience Platform, ob Verstöße gegen Datennutzungsrichtlinien vorliegen. Im Folgenden finden Sie ein Beispiel, bei dem eine Richtlinie verletzt wird. Sie können den Workflow zur Segmentaktivierung erst abschließen, nachdem Sie den Verstoß behoben haben. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Durchsetzung von Richtlinien](../../rtcdp/privacy/data-governance-overview.md#enforcement) im Abschnitt Data Governance-Dokumentation .

![Verletzung von Datenrichtlinien](../assets/common/data-policy-violation.png)

Wenn keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Beenden]** , um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

![Überprüfung](../assets/ui/activate-batch-profile-destinations/review.png)

## Segmentaktivierung überprüfen {#verify}


Für E-Mail-Marketing-Ziele und Cloud-Speicher-Ziele erstellt Adobe Experience Platform eine `.csv` -Datei in dem von Ihnen angegebenen Speicherort gespeichert. An diesem Speicherort wird täglich eine neue Datei erstellt. Das standardmäßige Dateiformat lautet:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

Dateien, die Sie an drei aufeinander folgenden Tagen erhalten, könnten wie folgt aussehen:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

Das Vorhandensein dieser Dateien an Ihrem Speicherort bestätigt die erfolgreiche Aktivierung. Um zu verstehen, wie die exportierten Dateien strukturiert sind, können Sie [Beispieldatei für eine CSV-Datei herunterladen](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv). Diese Beispieldatei enthält die Profilattribute `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear`und `personalEmail.address`.
