---
title: LiveRamp - Onboarding-Verbindung
description: Erfahren Sie, wie Sie mit dem LiveRamp-Connector Zielgruppen von Adobe Real-time Customer Data Platform in LiveRamp Connect integrieren können.
last-substantial-update: 2023-07-26T00:00:00Z
exl-id: b8ce7ec2-7af9-4d26-b12f-d38c85ba488a
source-git-commit: 804cc13d9f672e87ad56b328bae73216500e07dd
workflow-type: tm+mt
source-wordcount: '1814'
ht-degree: 69%

---

# [!DNL LiveRamp - Onboarding]-Verbindung {#liveramp-onboarding}

Verwenden Sie die [!DNL LiveRamp - Onboarding] Verbindung zu integrierten Zielgruppen von Adobe Real-time Customer Data Platform zu [!DNL LiveRamp Connect].

## Anwendungsfälle {#use-cases}

Damit Sie besser verstehen können, wie und wann Sie das [!DNL LiveRamp - Onboarding]-Ziel verwenden sollten, finden Sie hier ein Anwendungsbeispiel, das für Kundinnen und Kunden von Adobe Experience Platform mit diesem Ziel geeignet ist.

Als Marketer möchte ich Zielgruppen von Adobe Experience Platform an integrierte Identitäten in senden [!DNL LiveRamp Connect] , damit ich Benutzer auf Mobilgeräten, im Web, in sozialen Netzwerken und [!DNL CTV] Plattformen, die die [!DNL Ramp ID] Kennung.

## Voraussetzungen {#prerequisites}

Die [!DNL LiveRamp - Onboarding]-Verbindung exportiert Dateien mithilfe des [LiveRamp-SFTP](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html)-Speichers.

Um Daten von Experience Platform an [!DNL LiveRamp - Onboarding] senden zu können, benötigen Sie [!DNL LiveRamp]-Anmeldeinformationen. Wenden Sie sich an den für Sie zuständigen [!DNL LiveRamp]-Mitarbeiter bzw. -Mitarbeiterin, um Ihre Anmeldeinformationen zu beziehen, falls Sie noch nicht über diese verfügen.

## Unterstützte Identitäten {#supported-identities}

[!DNL LiveRamp - Onboarding] unterstützt die Aktivierung von Identitäten wie PII-basierten Kennungen, bekannten Kennungen und benutzerdefinierten IDs, die in der offiziellen [LiveRamp-Dokumentation](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers) beschrieben werden.

Im [Zuordnungsschritt](#map) des Aktivierungs-Workflows müssen Sie die Zielzuordnungen als benutzerdefinierte Attribute definieren.

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt werden alle Zielgruppen beschrieben, die Sie an dieses Ziel exportieren können.

Dieses Ziel unterstützt die Aktivierung von Zielgruppen, die durch die Experience Platform generiert wurden [Segmentierungsdienst](../../../segmentation/home.md).

Darüber hinaus unterstützt dieses Ziel auch die Aktivierung der zusätzlichen Zielgruppen, die in der folgenden Tabelle beschrieben sind.

| Zielgruppentyp | Beschreibung |
---------|----------|
| Benutzerdefinierte Uploads | Zielgruppen [importiert](../../../segmentation/ui/overview.md#importing-an-audience) in die Experience Platform aus CSV-Dateien. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Zielgruppenexport]** | Sie exportieren alle Mitglieder einer Zielgruppe mit den IDs (Name, Telefonnummer oder andere), die im [!DNL LiveRamp - Onboarding] Ziel. |
| Exporthäufigkeit | **[!UICONTROL Täglicher Batch]** | Da Profile in Experience Platform auf der Grundlage einer Zielgruppenbewertung aktualisiert werden, werden die Profile (Identitäten) einmal täglich nachgelagert zur Zielplattform aktualisiert. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

**SFTP-Authentifizierung mit Passwort** {#sftp-password}

![Beispiel-Screenshot, der zeigt, wie eine Authentifizierung beim Ziel mithilfe von SFTP mit Passwort erfolgt](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-password.png)

* **[!UICONTROL Benutzername]**: Der Benutzername für Ihren [!DNL LiveRamp - Onboarding]-Speicherort.
* **[!UICONTROL Passwort]**: Das Passwort für Ihren [!DNL LiveRamp - Onboarding]-Speicherort.
* **[!UICONTROL PGP/GPG-Verschlüsselungsschlüssel]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihre exportierten Dateien zu verschlüsseln. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der folgenden Abbildung.
  ![Abbildung eines Beispiels für einen korrekt formatierten PGP-Schlüssel in der Benutzeroberfläche](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)
* **[!UICONTROL Subkey-ID]**:Wenn Sie einen Verschlüsselungsschlüssel bereitstellen, müssen Sie auch eine Verschlüsselung bereitstellen **[!UICONTROL Subkey-ID]**. Informationen zum Abrufen der Unterschlüssel-ID finden Sie in der [!DNL LiveRamp] [Verschlüsselungsdokumentation](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key).

**SFTP mit SSH-Schlüsselauthentifizierung** {#sftp-ssh}

![Beispiel-Screenshot, der zeigt, wie eine Authentifizierung beim Ziel mithilfe eines SSH-Schlüssels erfolgt](../../assets/catalog/advertising/liveramp-onboarding/liveramp-sftp-ssh.png)

* **[!UICONTROL Benutzername]**: Der Benutzername für Ihren [!DNL LiveRamp - Onboarding]-Speicherort.
* **[!UICONTROL SSH-Schlüssel]**: Der private [!DNL SSH]-Schlüssel für die Anmeldung bei Ihrem [!DNL LiveRamp - Onboarding]-Speicherort. Der private Schlüssel muss als eine [!DNL Base64]-verschlüsselte Zeichenfolge formatiert sein und darf nicht passwortgeschützt sein.

   * Um Ihren [!DNL SSH]-Schlüssel mit dem [!DNL LiveRamp - Onboarding]-Server zu verbinden, müssen Sie ein Ticket über das [!DNL LiveRamp]-Portal für technischen Support einreichen und Ihren öffentlichen Schlüssel bereitstellen. Weitere Informationen finden Sie in der [LiveRamp-Dokumentation](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client).

* **[!UICONTROL PGP/GPG-Verschlüsselungsschlüssel]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihre exportierten Dateien zu verschlüsseln. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der folgenden Abbildung.
  ![Abbildung eines Beispiels für einen korrekt formatierten PGP-Schlüssel in der Benutzeroberfläche](../../assets/catalog/advertising/liveramp-onboarding/pgp-key.png)
* **[!UICONTROL Subkey-ID]**:Wenn Sie einen Verschlüsselungsschlüssel bereitstellen, müssen Sie auch eine Verschlüsselung bereitstellen **[!UICONTROL Subkey-ID]**. Informationen zum Abrufen der Unterschlüssel-ID finden Sie in der [!DNL LiveRamp] [Verschlüsselungsdokumentation](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key).

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="Verschlüsselungs-Unterschlüssel-ID"
>abstract="Die für die Verschlüsselung verwendete Unterschüssel-ID, die auf dem öffentlichen LiveRamp-Verschlüsselungsschlüssel basiert. Dieses Feld ist erforderlich, wenn Sie im Authentifizierungsschritt einen Verschlüsselungsschlüssel bereitgestellt haben."
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="Erfahren Sie, wie Sie die Unterschlüssel-ID abrufen"

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Screenshot der Platform-Benutzeroberfläche mit Informationen zum Ausfüllen von Details für Ihr Ziel](../../assets/catalog/advertising/liveramp-onboarding/liveramp-connection-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Ordnerpfad]**: Der Pfad zum [!DNL LiveRamp] `uploads`-Unterordner, in dem die exportierten Dateien gespeichert werden. Das `uploads`-Präfix wird automatisch zum Ordnerpfad hinzugefügt. [!DNL LiveRamp] empfiehlt die Erstellung eines dedizierten Unterordners für Sendungen aus Adobe Real-Time CDP, um die Dateien von anderen vorhandenen Feeds getrennt zu halten und eine reibungslose Ausführung aller Automatisierungen zu gewährleisten.
   * Wenn Sie beispielsweise Ihre Dateien nach `uploads/my_export_folder` exportieren möchten, geben Sie `my_export_folder` in das Feld **[!UICONTROL Ordnerpfad]** ein.
* **[!UICONTROL Komprimierungsformat]**: Wählen Sie den Komprimierungstyp aus, den Experience Platform für die exportierten Dateien verwenden soll. Verfügbare Optionen sind **[!UICONTROL GZIP]** oder **[!UICONTROL Keines]**.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Warnhinweisen zu Zielen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffskontrollberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](/help/destinations/ui/activate-batch-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel.

### Planung {#scheduling}

Im [!UICONTROL Planung] erstellen Sie für jede Audience einen Exportzeitplan mit den unten aufgeführten Einstellungen.

* **[!UICONTROL Dateiexportoptionen]**: [!UICONTROL Exportieren Sie vollständige Dateien]. [Inkrementelle Dateiexporte](../../ui/activate-batch-profile-destinations.md#export-incremental-files) werden derzeit nicht für das [!DNL LiveRamp]-Ziel unterstützt.
* **[!UICONTROL Häufigkeit]**: [!UICONTROL Täglich]
* **[!UICONTROL Datum]**: Wählen Sie die Start- und Endzeiten für den Export wie gewünscht aus.

![Screenshot der Platform-Benutzeroberfläche mit dem Schritt zur Zielgruppenplanung.](../../assets/catalog/advertising/liveramp-onboarding/liveramp_scheduling_screenshot.png)

Der Name der exportierten Datei kann derzeit nicht benutzerseitig konfiguriert werden. Alle an das [!DNL LiveRamp - Onboarding]-Ziel exportierten Dateien werden automatisch anhand der folgenden Vorlage benannt:

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![Screenshot der Platform-Benutzeroberfläche mit der Namensvorlage für exportierte Dateien.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-file-name.png)

Beispielsweise könnte der Name einer exportierten Datei für eine Organisation mit dem Namen [!DNL Luma] in etwa wie folgt aussehen:

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### Zuordnen von Attributen und Identitäten {#map}

Im **[!UICONTROL Zuordnungsschritt]** können Sie auswählen, welche Attribute und Identitäten für Ihre Profile exportiert werden sollen.

>[!IMPORTANT]
>
>Dieses Ziel unterstützt die Aktivierung eines Quell-Identity-Namespace pro Aktivierungsfluss. Wenn Sie mehrere Identity-Namespaces exportieren müssen, z. B. `Email` und `Phone`, müssen Sie für jede Identität [einen separaten Aktivierungsfluss erstellen](../../ui/activate-batch-profile-destinations.md).

Im **[!UICONTROL Zuordnungsschritt]** definiert die **[!UICONTROL Zielfeld]**-Zuordnung den Namen der Spaltenüberschrift in der exportierten CSV-Datei. Sie können die CSV-Spaltenüberschriften in der exportierten Datei in einen beliebigen Anzeigenamen ändern, indem Sie einen benutzerdefinierten Namen für das **[!UICONTROL Zielfeld]** angeben.

>[!IMPORTANT]
>
>Für alle Änderungen, die an den Zielfeldern nach der ersten Dateibereitstellung an [!DNL LiveRamp]benachrichtigen Sie bitte [!DNL LiveRamp] Kontoteam oder [Senden eines Tickets an den LiveRamp-Support](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#creating-a-support-case) , um sicherzustellen, dass die Änderungen im Automatisierungsprozess berücksichtigt werden.

1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird eine neue Zuordnungszeile angezeigt.

   ![Screenshot der Experience Platform-Benutzeroberfläche mit dem Bildschirm „Zuordnung“.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-add-new-mapping.png)

2. Wählen Sie im Fenster **[!UICONTROL Quellfeld auswählen]** die Kategorie **[!UICONTROL Attribute auswählen]** und dann das XDM-Attribut aus, das Sie zuordnen möchten, oder wählen Sie die Kategorie **[!UICONTROL Identity-Namespace auswählen]** und dann eine Identität aus, die Ihrem Ziel zugeordnet werden soll.

   ![Screenshot der Experience Platform-Benutzeroberfläche mit dem Bildschirm für die Quellzuordnung.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-source-mapping.png)

3. Geben Sie im Fenster **[!UICONTROL Zielfeld auswählen]** den Attributnamen ein, dem Sie das ausgewählte Quellfeld zuordnen möchten. Der hier definierte Attributname spiegelt sich in der exportierten CSV-Datei als Spaltenüberschrift wider.

   ![Screenshot der Experience Platform-Benutzeroberfläche mit dem Bildschirm für die Zielzuordnung.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-mapping.png)

   Sie können den Attributnamen auch direkt in das **[!UICONTROL Zielfeld]** eingeben.

   ![Screenshot der Experience Platform-Benutzeroberfläche mit dem Bildschirm für die Zielzuordnung.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-target-field.png)

Wählen Sie nach dem Hinzufügen aller gewünschten Zuordnungen die Option **[!UICONTROL Weiter]** aus und beenden Sie den Aktivierungs-Workflow.

## Exportierte Daten/Datenexport validieren {#exported-data}

Ihre Daten werden an den von Ihnen konfigurierten [!DNL LiveRamp - Onboarding]-Speicherort als CSV-Dateien exportiert.

Beim Exportieren von Dateien an das [!DNL LiveRamp - Onboarding]-Ziel generiert Platform eine CSV-Datei für jede [Zusammenführungsrichtlinien-ID](../../../profile/merge-policies/overview.md).

Betrachten wir beispielsweise die folgenden Zielgruppen:

* Zielgruppe A (Zusammenführungsrichtlinie 1)
* Zielgruppe B (Zusammenführungsrichtlinie 2)
* Zielgruppe C (Zusammenführungsrichtlinie 1)
* Zielgruppe D (Zusammenführungsrichtlinie 1)

Platform exportiert zwei CSV-Dateien nach [!DNL LiveRamp - Onboarding]:

* Eine CSV-Datei mit den Zielgruppen A, C und D;
* Eine CSV-Datei, die Audience B enthält.

Exportierte CSV-Dateien enthalten Profile mit den ausgewählten Attributen und dem entsprechenden Zielgruppenstatus in separaten Spalten mit dem Attributnamen und `audience_namespace:audience_ID` -Paare als Spaltenüberschriften verwenden, wie im folgenden Beispiel gezeigt:

`ATTRIBUTE_NAME, AUDIENCE_NAMESPACE_1:AUDIENCE_ID_1, AUDIENCE_NAMESPACE_2:AUDIENCE_ID_2,..., AUDIENCE_NAMESPACE_X:AUDIENCE_ID_X`

Die in den exportierten Dateien enthaltenen Profile können mit einem der folgenden Status der Zielgruppenqualifizierung übereinstimmen:

* `Active`: Das Profil ist derzeit für die Zielgruppe qualifiziert.
* `Expired`: Das Profil ist nicht mehr für die Zielgruppe qualifiziert, hat sich aber in der Vergangenheit qualifiziert.
* `""`(leere Zeichenfolge): Das Profil, das für die Zielgruppe nie qualifiziert wurde.

Beispiel: eine exportierte CSV-Datei mit einer `email` -Attribut zwei aus der Experience Platform stammende Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md), und einem [importiert](../../../segmentation/ui/overview.md#importing-an-audience) eine externe Zielgruppe wie folgt aussehen könnte:

```csv
email,ups:aa2e3d98-974b-4f8b-9507-59f65b6442df,ups:45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,CustomerAudienceUpload:7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

Im obigen Beispiel wird die Variable `ups:aa2e3d98-974b-4f8b-9507-59f65b6442df` und `ups:45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f` -Abschnitte beschreiben Zielgruppen, die aus dem Segmentierungsdienst stammen, während `CustomerAudienceUpload:7729e537-4e42-418e-be3b-dce5e47aaa1e` beschreibt eine in Platform als [benutzerdefinierter Upload](../../../segmentation/ui/overview.md#importing-an-audience).

Da Platform eine CSV-Datei für jede [Zusammenführungsrichtlinien-ID](../../../profile/merge-policies/overview.md) generiert, wird auch eine separate Datenflussausführung für jede Zusammenführungsrichtlinien-ID erzeugt.

Das bedeutet, dass die Variable **[!UICONTROL Aktivierte Identitäten]** und **[!UICONTROL Vorgenommene Profile]** Metriken in [Datenfluss-Ausführung](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) -Seite werden für jede Gruppe von Zielgruppen aggregiert, die dieselbe Zusammenführungsrichtlinie verwenden, anstatt für jede Zielgruppe angezeigt zu werden.

Da Datenflüsse für eine Gruppe von Zielgruppen generiert werden, die dieselbe Zusammenführungsrichtlinie verwenden, werden die Zielgruppennamen nicht in der [Monitoring-Dashboard](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).

![Screenshot der Experience Platform-Benutzeroberfläche mit der Metrik „Aktivierte Identitäten“.](../../assets/catalog/advertising/liveramp-onboarding/liveramp-metrics.png)

## Hochladen exportierter Daten nach LiveRamp {#upload-to-liveramp}

Nach dem erfolgreichen Export Ihrer Daten in den [!DNL LiveRamp - Onboarding]-Speicher müssen Sie die Daten in die [!DNL LiveRamp]-Plattform hochladen.

Weitere Informationen zum Hochladen Ihrer Dateien aus dem [!DNL LiveRamp - Onboarding]-Speicher in eine [!DNL LiveRamp]-Zielgruppe finden Sie in der Dokumentation mit [Hinweisen zum Hochladen der ersten Datei in eine Zielgruppe](https://docs.liveramp.com/connect/en/considerations-when-uploading-the-first-file-to-an-audience.html#considerations-when-uploading-the-first-file-to-an-audience).

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Informationen zur Konfiguration der [!DNL LiveRamp - Onboarding] -Speicher, siehe [amtliche Dokumentation](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).