---
keywords: Profilattribute aktivieren; Ziele aktivieren; Daten aktivieren; E-Mail-Marketing-Ziele aktivieren; Aktivieren von Cloud-Speicher-Zielen
title: Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele
type: Tutorial
seo-title: Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele
description: Erfahren Sie, wie Sie die Zielgruppendaten aktivieren, die Sie in Adobe Experience Platform haben, indem Sie Segmente an Batch-Profil-basierte Ziele senden.
seo-description: Erfahren Sie, wie Sie die Zielgruppendaten aktivieren, die Sie in Adobe Experience Platform haben, indem Sie Segmente an Batch-Profil-basierte Ziele senden.
source-git-commit: 02c22453470d55236d4235c479742997e8407ef3
workflow-type: tm+mt
source-wordcount: '2011'
ht-degree: 7%

---


# Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele

## Übersicht {#overview}

In diesem Artikel wird der Workflow erläutert, der zum Aktivieren von Zielgruppendaten in Adobe Experience Platform-Batch-profilbasierten Zielen wie Cloud-Speicher und E-Mail-Marketing-Zielen erforderlich ist.

## Voraussetzungen {#prerequisites}

Um Daten für Ziele aktivieren zu können, müssen Sie über eine erfolgreiche [Verbindung zu einem Ziel](./connect-destination.md) verfügen. Wenn Sie dies noch nicht getan haben, navigieren Sie zum [Zielkatalog](../catalog/overview.md), durchsuchen Sie die unterstützten Ziele und konfigurieren Sie das Ziel, das Sie verwenden möchten.

## Ziel auswählen {#select-destination}

1. Gehen Sie zu **[!UICONTROL Verbindungen > Ziele]** und wählen Sie die Registerkarte **[!UICONTROL Durchsuchen]** aus.

   ![Registerkarte &quot;Ziel durchsuchen&quot;](../assets/ui/activate-batch-profile-destinations/browse-tab.png)

1. Wählen Sie die Schaltfläche **[!UICONTROL Segmente hinzufügen]** aus, die dem Ziel entspricht, an dem Sie Ihre Segmente aktivieren möchten, wie in der Abbildung unten dargestellt.

   ![Schaltflächen aktivieren](../assets/ui/activate-batch-profile-destinations/activate-buttons-browse.png)

1. Navigieren Sie zum nächsten Abschnitt [wählen Sie Ihre Segmente](#select-segments) aus.

## Segmente auswählen {#select-segments}

Verwenden Sie die Kontrollkästchen links neben den Segmentnamen, um die Segmente auszuwählen, die Sie für das Ziel aktivieren möchten, und wählen Sie dann **[!UICONTROL Weiter]** aus.

![Segmente auswählen](../assets/ui/activate-batch-profile-destinations/select-segments.png)


## Segmentexport planen {#scheduling}

[!DNL Adobe Experience Platform] exportiert Daten für E-Mail-Marketing- und Cloud-Speicher-Ziele in Form von  [!DNL CSV] Dateien. Auf der Seite **[!UICONTROL Planung]** können Sie den Zeitplan und die Dateinamen für jedes Segment, das Sie exportieren, konfigurieren. Die Konfiguration des Zeitplans ist obligatorisch, die Konfiguration des Dateinamens ist jedoch optional.

>[!IMPORTANT]
> 
>[!DNL Adobe Experience Platform] teilt die Exportdateien automatisch mit 5 Millionen Datensätzen (Zeilen) pro Datei auf. Jede Zeile stellt ein Profil dar.
>
>Dateinamen mit Aufspaltung werden mit einer Zahl angehängt, die angibt, dass die Datei Teil eines größeren Exports ist. Dies zeigt an: `filename.csv`, `filename_2.csv`, `filename_3.csv`.

Wählen Sie die Schaltfläche **[!UICONTROL Zeitplan]** erstellen , die dem Segment entspricht, das Sie an Ihr Ziel senden möchten.

![Schaltfläche &quot;Zeitplan erstellen&quot;](../assets/ui/activate-batch-profile-destinations/create-schedule-button.png)

### Exportieren von vollständigen Dateien {#export-full-files}

Wählen Sie **[!UICONTROL Vollständige Dateien exportieren]** aus, damit Ihre exportierten Dateien eine vollständige Momentaufnahme aller Profile enthalten, die für dieses Segment qualifiziert sind.

![Exportieren von vollständigen Dateien](../assets/ui/activate-batch-profile-destinations/export-full-files.png)

1. Verwenden Sie den Selektor **[!UICONTROL Häufigkeit]**, um zwischen einmaligen (**[!UICONTROL Einmal]**) oder **[!UICONTROL Täglichen]** Exporten zu wählen. Durch den Export einer vollständigen Datei **[!UICONTROL Täglich]** wird die Datei täglich vom Startdatum bis zum Enddatum um 12:00 Uhr UTC (19:00 Uhr EST) exportiert.
2. Verwenden Sie die Auswahl **[!UICONTROL Zeit]** , um die Tageszeit im Format [!DNL UTC] festzulegen, zu der der Export erfolgen soll. Durch den Export einer Datei **[!UICONTROL Täglich]** wird die Datei täglich vom Startdatum bis zum Enddatum zum ausgewählten Zeitpunkt exportiert.

   >[!IMPORTANT]
   >
   >Die Option zum Exportieren von Dateien zu einem bestimmten Tageszeitpunkt befindet sich derzeit in der Beta-Phase und steht nur einer ausgewählten Anzahl von Kunden zur Verfügung.<br> <br> Aufgrund der Art und Weise, wie interne Experience Platform-Prozesse konfiguriert werden, enthält der erste inkrementelle oder vollständige Dateiexport möglicherweise nicht alle Aufstockungsdaten.  <br> <br> Um einen vollständigen und aktuellsten Datenexport für die Aufstockung sowohl für vollständige als auch für inkrementelle Dateien sicherzustellen, empfiehlt Adobe, die erste Dateiexportzeit nach 22:00 Uhr GMT des folgenden Tages festzulegen. Dies ist eine Einschränkung, die in zukünftigen Versionen behoben wird.

3. Verwenden Sie den Selektor **[!UICONTROL Datum]** , um den Tag oder das Intervall auszuwählen, an dem der Export stattfinden soll.
4. Wählen Sie **[!UICONTROL Erstellen]** aus, um den Zeitplan zu speichern.


### Inkrementelle Dateien exportieren {#export-incremental-files}

Wählen Sie **[!UICONTROL Inkrementelle Dateien exportieren]** aus, damit Ihre exportierten Dateien nur die Profile enthalten, die sich seit dem letzten Export für dieses Segment qualifiziert haben.

>[!IMPORTANT]
>
>Die erste exportierte inkrementelle Datei enthält alle Profile, die sich für ein Segment qualifizieren und als Aufstockung fungieren.

![Inkrementelle Dateien exportieren](../assets/ui/activate-batch-profile-destinations/export-incremental-files.png)

1. Verwenden Sie den Selektor **[!UICONTROL Häufigkeit]**, um zwischen **[!UICONTROL täglichen]** oder **[!UICONTROL stündlichen]** Exporten zu wählen. Durch den Export einer inkrementellen Datei **[!UICONTROL Täglich]** wird die Datei täglich vom Startdatum bis zum Enddatum um 22:00 Uhr UTC (07:00 Uhr EST) exportiert.
   * Verwenden Sie bei der Auswahl von **[!UICONTROL Stündlich]** den Selektor **[!UICONTROL Jedes]**, um zwischen den Optionen **[!UICONTROL 3]**, **[!UICONTROL 6]**, **[!UICONTROL 8]** und **[!UICONTROL 12]** zu wählen.

      >[!IMPORTANT]
      >
      >Die Option, inkrementelle Dateien alle 3, 6, 8 oder 12 Stunden zu exportieren, befindet sich derzeit in der Beta-Phase und steht nur einer bestimmten Anzahl von Kunden zur Verfügung. Nicht-Beta-Kunden können inkrementelle Dateien einmal täglich exportieren.

2. Verwenden Sie die Auswahl **[!UICONTROL Zeit]** , um die Tageszeit im Format [!DNL UTC] festzulegen, zu der der Export erfolgen soll.

   >[!IMPORTANT]
   >
   >Die Option zur Auswahl der Tageszeit für den Export ist nur für eine ausgewählte Anzahl von Kunden verfügbar. <br> <br> Aufgrund der Art und Weise, wie interne Experience Platform-Prozesse konfiguriert werden, enthält der erste inkrementelle oder vollständige Dateiexport möglicherweise nicht alle Aufstockungsdaten.  <br> <br> Um einen vollständigen und aktuellsten Datenexport für die Aufstockung sowohl für vollständige als auch für inkrementelle Dateien sicherzustellen, empfiehlt Adobe, die erste Dateiexportzeit nach 22:00 Uhr GMT des folgenden Tages festzulegen. Dies ist eine Einschränkung, die in zukünftigen Versionen behoben wird.

3. Verwenden Sie den Selektor **[!UICONTROL Datum]** , um den Tag oder das Intervall auszuwählen, an dem der Export stattfinden soll.
4. Wählen Sie **[!UICONTROL Erstellen]** aus, um den Zeitplan zu speichern.

### Dateinamen konfigurieren {#file-names}

Die standardmäßigen Dateinamen bestehen aus Zielname, Segment-ID und einem Datums- und Uhrzeitindikator. Sie können beispielsweise Ihre exportierten Dateinamen bearbeiten, um zwischen verschiedenen Kampagnen zu unterscheiden oder die Datenexportzeit an die Dateien anhängen zu lassen.

Wählen Sie das Stiftsymbol aus, um ein modales Fenster zu öffnen und die Dateinamen zu bearbeiten. Dateinamen sind auf 255 Zeichen begrenzt.

![Dateinamen konfigurieren](../assets/ui/activate-batch-profile-destinations/configure-name.png)

Im Dateinamen-Editor können Sie verschiedene Komponenten auswählen, die zum Dateinamen hinzugefügt werden sollen.

![Optionen zum Bearbeiten von Dateinamen](../assets/ui/activate-batch-profile-destinations/activate-workflow-configure-step-2.png)

Zielname und Segment-ID können nicht aus Dateinamen entfernt werden. Zusätzlich können Sie Folgendes hinzufügen:

* **[!UICONTROL Segmentname]**: Sie können den Segmentnamen an den Dateinamen anhängen.
* **[!UICONTROL Datum und Uhrzeit]**: Wählen Sie zwischen dem Hinzufügen eines  `MMDDYYYY_HHMMSS` Formats oder eines Unix-10-stelligen Zeitstempels der Zeit, zu der die Dateien generiert werden. Wählen Sie eine dieser Optionen aus, wenn für Ihre Dateien bei jedem inkrementellen Export ein dynamischer Dateiname erstellt werden soll.
* **[!UICONTROL Benutzerdefinierter Text]**: Fügen Sie den Dateinamen benutzerdefinierten Text hinzu.

Wählen Sie **[!UICONTROL Änderungen anwenden]** aus, um Ihre Auswahl zu bestätigen.

>[!IMPORTANT]
> 
>Wenn Sie die Komponente **[!UICONTROL Datum und Uhrzeit]** nicht auswählen, sind die Dateinamen statisch und die neue exportierte Datei überschreibt die vorherige Datei an Ihrem Speicherort bei jedem Export. Bei der Ausführung eines wiederkehrenden Importvorgangs von einem Speicherort zu einer E-Mail-Marketing-Plattform wird diese Option empfohlen.

Nachdem Sie alle Ihre Segmente konfiguriert haben, wählen Sie **[!UICONTROL Weiter]** aus, um fortzufahren.

## Profilattribute auswählen {#select-attributes}

Bei profilbasierten Zielen müssen Sie die Profilattribute auswählen, die Sie an das Ziel senden möchten.


1. Wählen Sie auf der Seite **[!UICONTROL Attribute]** auswählen **[!UICONTROL Neues Feld hinzufügen]** aus.

   ![Neues Mapping hinzufügen](../assets/ui/activate-batch-profile-destinations/add-new-field.png)

1. Wählen Sie den Pfeil rechts neben dem Eintrag **[!UICONTROL Schema field]** aus.

   ![Quellfeld auswählen](../assets/ui/activate-batch-profile-destinations/select-target-field.png)

1. Wählen Sie auf der Seite **[!UICONTROL Feld]** auswählen die XDM-Attribute aus, die Sie an das Ziel senden möchten, und wählen Sie dann **[!UICONTROL Auswählen]**.

   ![Quellfeldseite auswählen](../assets/ui/activate-batch-profile-destinations/target-field-page.png)


1. Um weitere Zuordnungen hinzuzufügen, wiederholen Sie die Schritte 1 bis 3.


>[!NOTE]
>
> Adobe Experience Platform füllt Ihre Auswahl mit vier empfohlenen, häufig verwendeten Attributen aus Ihrem Schema: `person.name.firstName`, `person.name.lastName`, `personalEmail.address`, `segmentMembership.status`.

Dateiexporte variieren auf folgende Weise, je nachdem, ob `segmentMembership.status` ausgewählt ist:
* Wenn das Feld `segmentMembership.status` ausgewählt ist, enthalten exportierte Dateien **[!UICONTROL Aktive]** Mitglieder im ersten vollständigen Snapshot und **[!UICONTROL Aktive]** und **[!UICONTROL Abgelaufene]** Mitglieder in nachfolgenden inkrementellen Exporten.
* Wenn das Feld `segmentMembership.status` nicht ausgewählt ist, enthalten exportierte Dateien nur **[!UICONTROL aktive]**-Mitglieder im ersten vollständigen Snapshot und in nachfolgenden inkrementellen Exporten.

![empfohlene Attribute](../assets/ui/activate-batch-profile-destinations/mandatory-deduplication.png)

### Obligatorische Attribute {#mandatory-attributes}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_mandatorykey"
>title="Über obligatorische Attribute"
>abstract="Wählen Sie die XDM-Schemaattribute aus, die alle exportierten Profile enthalten sollen. Profile ohne obligatorischen Schlüssel werden nicht an das Ziel exportiert. Wenn Sie keinen obligatorischen Schlüssel auswählen, werden alle qualifizierten Profile unabhängig von ihren Attributen exportiert."
>additional-url="http://www.adobe.com/go/destinations-mandatory-attributes-en" text="Weitere Informationen finden Sie in der Dokumentation ."

Sie können Attribute als obligatorisch markieren, um sicherzustellen, dass [!DNL Platform] nur die Profile exportiert, die das spezifische Attribut enthalten. Sie kann daher als zusätzliche Filterform verwendet werden. Die Kennzeichnung eines Attributs als obligatorisch ist **nicht** erforderlich.

Wenn kein obligatorisches Attribut ausgewählt wird, werden alle qualifizierten Profile unabhängig von ihren Attributen exportiert.

Es wird empfohlen, eines der Attribute aus Ihrem Schema eine [eindeutige Kennung](../../destinations/catalog/email-marketing/overview.md#identity) zu verwenden. Weitere Informationen zu obligatorischen Attributen finden Sie im Abschnitt Identität in der Dokumentation [E-Mail-Marketing-Ziele](../../destinations/catalog/email-marketing/overview.md#identity) .

### Deduplizierungsschlüssel {#deduplication-keys}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_deduplicationkey"
>title="Über Deduplizierungsschlüssel"
>abstract="Beseitigen Sie mehrere Datensätze desselben Profils in den Exportdateien, indem Sie einen Deduplizierungsschlüssel auswählen. Wählen Sie einen einzelnen Namespace oder bis zu zwei XDM-Schemaattribute als Deduplizierungsschlüssel aus. Wenn Sie keinen Deduplizierungsschlüssel auswählen, werden in den Exportdateien möglicherweise doppelte Profileinträge angezeigt."
>additional-url="http://www.adobe.com/go/destinations-deduplication-keys-en" text="Weitere Informationen finden Sie in der Dokumentation ."

>[!IMPORTANT]
>
>Die Option zur Verwendung von Deduplizierungsschlüsseln befindet sich derzeit in der Beta-Phase und steht nur einer ausgewählten Anzahl von Kunden zur Verfügung.

Deduplizierungsschlüssel verhindern die Möglichkeit, mehrere Datensätze desselben Profils in einer Exportdatei zu haben.

Es gibt drei Möglichkeiten, Deduplizierungsschlüssel in [!DNL Platform] zu verwenden:

* Verwenden eines einzelnen Identitäts-Namespace als [!UICONTROL Deduplizierungsschlüssel]
* Verwenden eines einzelnen Profilattributs aus einem [!DNL XDM]-Profil als [!UICONTROL Deduplizierungsschlüssel]
* Verwenden einer Kombination zweier Profilattribute aus einem [!DNL XDM]-Profil als zusammengesetzten Schlüssel

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

### Nutzungsszenario 1: Deduplizierung keine Deduplizierung

Ohne Deduplizierung würde die Exportdatei die folgenden Einträge enthalten.

| personalEmail | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | Doe |
| johndoe@example.com | John | D |


### Anwendungsfall 2: Deduplizierung Deduplizierung basierend auf Identitäts-Namespace

Unter der Annahme einer Deduplizierung durch den Namespace [!DNL Email] enthält die Exportdatei die folgenden Einträge. Profil B ist das neueste Profil, das sich für das Segment qualifiziert hat. Daher wird nur dieses exportiert.

| E-Mail* | personalEmail | firstName | lastName |
|---|---|---|---|
| johndoe_1@example.com | johndoe@example.com | John | D |
| johndoe_2@example.com | johndoe@example.com | John | D |

### Nutzungsszenario 3: Deduplizierung Deduplizierung basierend auf einem einzelnen Profilattribut

Unter der Annahme einer Deduplizierung durch das Attribut `personal Email` würde die Exportdatei den folgenden Eintrag enthalten. Profil B ist das neueste Profil, das sich für das Segment qualifiziert hat. Daher wird nur dieses exportiert.

| personalEmail* | firstName | lastName |
|---|---|---|
| johndoe@example.com | John | D |


### Anwendungsfall 4: Deduplizierung Deduplizierung basierend auf zwei Profilattributen (zusammengesetzter Deduplizierungsschlüssel)

Bei Deduplizierung durch den zusammengesetzten Schlüssel `personalEmail + lastName` enthält die Exportdatei die folgenden Einträge.

| personalEmail* | lastName* | firstName |
|---|---|---|
| johndoe@example.com | D | John |
| johndoe@example.com | Doe | John |


Adobe empfiehlt die Auswahl eines Identitäts-Namespace wie [!DNL CRM ID] oder einer E-Mail-Adresse als Deduplizierungsschlüssel, um sicherzustellen, dass alle Profildatensätze eindeutig identifiziert werden.

>[!NOTE]
> 
>Wenn Datennutzungsbezeichnungen auf bestimmte Felder in einem Datensatz angewendet wurden (und nicht auf den gesamten Datensatz), erfolgt die Durchsetzung dieser Feldbezeichnungen bei der Aktivierung unter folgenden Bedingungen:
>
>* Die Felder werden in der Segmentdefinition verwendet.
>* Die Felder werden als projizierte Attribute für das Ziel der Zielgruppe konfiguriert.

>
> 
Wenn beispielsweise das Feld `person.name.firstName` bestimmte Datennutzungsbezeichnungen enthält, die mit der Marketing-Aktion des Ziels in Konflikt stehen, wird Ihnen im Überprüfungsschritt eine Verletzung der Datennutzungsrichtlinien angezeigt. Weitere Informationen finden Sie unter [Data Governance in Adobe Experience Platform](../../rtcdp/privacy/data-governance-overview.md#destinations).

## Überprüfung {#review}

Auf der Seite **[!UICONTROL Überprüfen]** können Sie eine Zusammenfassung Ihrer Auswahl sehen. Wählen Sie **[!UICONTROL Abbrechen]**, um den Fluss abzubrechen, **[!UICONTROL Zurück]**, um die Einstellungen zu ändern, oder **[!UICONTROL Fertig stellen]**, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

>[!IMPORTANT]
>
>In diesem Schritt prüft Adobe Experience Platform, ob Verstöße gegen Datennutzungsrichtlinien vorliegen. Im Folgenden finden Sie ein Beispiel, bei dem eine Richtlinie verletzt wird. Sie können den Workflow zur Segmentaktivierung erst abschließen, nachdem Sie den Verstoß behoben haben. Informationen zum Beheben von Richtlinienverletzungen finden Sie unter [Richtliniendurchsetzung](../../rtcdp/privacy/data-governance-overview.md#enforcement) im Abschnitt zur Data Governance-Dokumentation.

![Verletzung von Datenrichtlinien](../assets/common/data-policy-violation.png)

Wenn keine Richtlinienverletzungen festgestellt wurden, wählen Sie **[!UICONTROL Beenden]** aus, um Ihre Auswahl zu bestätigen und mit dem Senden von Daten an das Ziel zu beginnen.

![Überprüfung](../assets/ui/activate-batch-profile-destinations/review.png)

## Segmentaktivierung überprüfen {#verify}


Für E-Mail-Marketing-Ziele und Cloud-Speicher-Ziele erstellt Adobe Experience Platform eine tabulatorgetrennte `.csv`-Datei am von Ihnen angegebenen Speicherort. An diesem Speicherort wird täglich eine neue Datei erstellt. Das standardmäßige Dateiformat lautet:
`<destinationName>_segment<segmentID>_<timestamp-yyyymmddhhmmss>.csv`

Dateien, die Sie an drei aufeinander folgenden Tagen erhalten, könnten wie folgt aussehen:

```console
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200409052200.csv
Salesforce_Marketing_Cloud_segment12341e18-abcd-49c2-836d-123c88e76c39_20200410061130.csv
```

Das Vorhandensein dieser Dateien an Ihrem Speicherort bestätigt die erfolgreiche Aktivierung. Um zu verstehen, wie die exportierten Dateien strukturiert sind, können Sie [eine .csv-Beispieldatei](../assets/common/sample_export_file_segment12341e18-abcd-49c2-836d-123c88e76c39_20200408061804.csv) herunterladen. Diese Beispieldatei enthält die Profilattribute `person.firstname`, `person.lastname`, `person.gender`, `person.birthyear` und `personalEmail.address`.
