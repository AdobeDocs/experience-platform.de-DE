---
title: (Alpha) [!DNL LiveRamp SFTP] connection
description: Erfahren Sie, wie Sie mit dem LiveRamp-Connector Zielgruppen von Adobe Real-time Customer Data Platform nach LiveRamp Connect integrieren können.
hidefromtoc: true
hide: true
source-git-commit: 875610178449ddade78462dc74ea4e3dbadb2907
workflow-type: tm+mt
source-wordcount: '1725'
ht-degree: 19%

---


# (Alpha) [!DNL LiveRamp - SFTP] connection {#liveramp-destination}

Verwenden Sie die LiveRamp-Verbindung, um Zielgruppen von Adobe Real-time Customer Data Platform nach zu integrieren. [!DNL LiveRamp Connect].

>[!IMPORTANT]
>
><p>Diese Zielverbindung befindet sich derzeit in der Alpha-Phase und steht nur einer begrenzten Auswahl von Kunden zur Verfügung. Die Funktionalität und Dokumentation können sich ändern.</p>
&gt;<p>Die endgültige Version dieser Zielverbindung erfordert möglicherweise eine Kundenmigration.</p>


## Anwendungsfälle {#use-cases}

Um Ihnen zu helfen, besser zu verstehen, wie und wann Sie die [!DNL LiveRamp SFTP] Ziel, hier ein Beispielanwendungsfall, den Adobe Experience Platform-Kunden mit diesem Ziel lösen können.

Als Marketer möchte ich Zielgruppen von Adobe Experience Platform an integrierte Identitäten in senden [!DNL LiveRamp Connect] damit ich Benutzer ansprechen kann in [!DNL CTV] Plattformen, die die [!DNL Ramp ID] Kennung.

## Voraussetzungen {#prerequisites}

Die [!DNL LiveRamp - SFTP] Verbindungsexporte verwenden [LiveRamp-SFTP](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html) Speicher.

Bevor Sie Daten von Experience Platform an senden können [!DNL LiveRamp SFTP], benötigen Sie [!DNL LiveRamp] Anmeldedaten. Bitte wenden Sie sich an Ihre [!DNL LiveRamp] -Mitarbeiter, um Ihre Anmeldeinformationen zu erhalten, falls Sie noch nicht über diese verfügen.

## Unterstützte Identitäten {#supported-identities}

LiveRamp SFTP unterstützt die Aktivierung von Identitäten wie PII-basierten Kennungen, bekannten Kennungen und benutzerdefinierten Kennungen, die im offiziellen Dokument beschrieben werden [LiveRamp-Dokumentation](https://docs.liveramp.com/connect/en/identity-and-identifier-terms-and-concepts.html#known-identifiers).

Im [Zuordnungsschritt](#map) des Aktivierungs-Workflows müssen Sie die Zielgruppen-Mappings als benutzerdefinierte Attribute definieren.

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Segmentexport]** | Sie exportieren alle Mitglieder eines Segments (Zielgruppe) mit den IDs (Name, Telefonnummer oder andere), die im [!DNL LiveRamp SFTP] Ziel. |
| Exporthäufigkeit | **[!UICONTROL Täglicher Batch]** | Da Profile in Experience Platform auf der Grundlage einer Segmentbewertung aktualisiert werden, werden die Profile (Identitäten) einmal täglich nachgelagert zur Zielplattform aktualisiert. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Beim Ziel authentifizieren {#authenticate}

Um sich beim Ziel zu authentifizieren, füllen Sie die erforderlichen Felder aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

**SFTP-Authentifizierung mit Passwort** {#sftp-password}

![Screenshot eines Beispiels, in dem gezeigt wird, wie eine Authentifizierung am Ziel mithilfe von SFTP mit Kennwort erfolgt](../../assets/catalog/advertising/liveramp/liveramp-sftp-password.png)

* **[!UICONTROL Benutzername]**: Der Benutzername für Ihre [!DNL LiveRamp SFTP] Speicherort.
* **[!UICONTROL Passwort]**: Das Kennwort für Ihre [!DNL LiveRamp SFTP] Speicherort.
* **[!UICONTROL PGP/GPG-Verschlüsselungsschlüssel]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der Abbildung unten. Wenn Sie einen Verschlüsselungsschlüssel bereitstellen, müssen Sie auch einen **[!UICONTROL Verschlüsselungs-Unterschlüssel-ID]** im [Zieldetails](#destination-details) Abschnitt.

   ![Bild, das ein Beispiel eines korrekt formatierten PGP-Schlüssels in der Benutzeroberfläche anzeigt](../../assets/catalog/advertising/liveramp/pgp-key.png)

**SFTP mit SSH-Schlüsselauthentifizierung** {#sftp-ssh}

![Beispiel-Screenshot, der zeigt, wie eine Authentifizierung für das Ziel mithilfe des SSH-Schlüssels erfolgt](../../assets/catalog/advertising/liveramp/liveramp-sftp-ssh.png)

* **[!UICONTROL Benutzername]**: Der Benutzername für Ihre [!DNL LiveRamp SFTP] Speicherort.
* **[!UICONTROL SSH-Schlüssel]**: Der private [!DNL SSH] Schlüssel für die Anmeldung bei [!DNL LiveRamp SFTP] Speicherort. Der private Schlüssel muss als [!DNL Base64]-kodierte Zeichenfolge und dürfen nicht kennwortgeschützt sein.

   * Um eine Verbindung herzustellen [!DNL SSH] Schlüssel zum [!DNL LiveRamp SFTP] Server, müssen Sie ein Ticket über senden [!DNL LiveRamp]das Portal für technischen Support und stellen Sie Ihren öffentlichen Schlüssel bereit. Weitere Informationen finden Sie unter [LiveRamp-Dokumentation](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html#upload-with-an-sftp-client).

* **[!UICONTROL PGP/GPG-Verschlüsselungsschlüssel]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien Verschlüsselung hinzuzufügen. Wenn Sie einen Verschlüsselungsschlüssel bereitstellen, müssen Sie auch einen **[!UICONTROL Verschlüsselungs-Unterschlüssel-ID]** im [Zieldetails](#destination-details) Abschnitt. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der Abbildung unten.

   ![Bild, das ein Beispiel eines korrekt formatierten PGP-Schlüssels in der Benutzeroberfläche anzeigt](../../assets/catalog/advertising/liveramp/pgp-key.png)

### Ausfüllen der Zieldetails {#destination-details}

>[!CONTEXTUALHELP]
>id="platform_destinations_liveramp_subkey"
>title="Verschlüsselungs-Unterschlüssel-ID"
>abstract="Die für die Verschlüsselung verwendete Subkey-ID, die auf dem öffentlichen LiveRamp-Verschlüsselungsschlüssel basiert. Dieses Feld ist erforderlich, wenn Sie im Authentifizierungsschritt einen Verschlüsselungsschlüssel bereitgestellt haben."
>additional-url="https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key" text="Erfahren Sie, wie Sie die Subkey-ID abrufen."

Füllen Sie die folgenden erforderlichen und optionalen Felder aus, um Details für das Ziel zu konfigurieren. Ein Sternchen neben einem Feld in der Benutzeroberfläche zeigt an, dass das Feld erforderlich ist.

![Screenshot der Platform-Benutzeroberfläche mit Informationen zum Ausfüllen von Details für Ihr Ziel](../../assets/catalog/advertising/liveramp/liveramp-connection-details.png)

* **[!UICONTROL Name]**: Ein Name, durch den Sie dieses Ziel in Zukunft erkennen können.
* **[!UICONTROL Beschreibung]**: Eine Beschreibung, die Ihnen hilft, dieses Ziel in Zukunft zu identifizieren.
* **[!UICONTROL Ordnerpfad]**: Der Pfad zum [!DNL LiveRamp] `uploads` -Unterordner, in dem die exportierten Dateien gehostet werden. Die `uploads` -Präfix wird automatisch zum Ordnerpfad hinzugefügt.
   * Wenn Sie beispielsweise Ihre Dateien in `uploads/my_export_folder`, Typ in `my_export_folder` im **[!UICONTROL Ordnerpfad]** -Feld.
* **[!UICONTROL Komprimierungsformat]**: Wählen Sie den Komprimierungstyp aus, den die Experience Platform für die exportierten Dateien verwenden soll. Verfügbare Optionen sind **[!UICONTROL GZIP]** oder **[!UICONTROL Keines]**.
* **[!UICONTROL Verschlüsselungs-Unterschlüssel-ID]**: Der für die Verschlüsselung verwendete Unterschlüssel, basierend auf der [!DNL LiveRamp] öffentlichen Verschlüsselungsschlüssel. Dieses Feld ist erforderlich, wenn Sie im [Authentifizierung](#authenticate) Schritt. Siehe [!DNL LiveRamp] [Verschlüsselungsdokumentation](https://docs.liveramp.com/connect/en/encrypting-files-for-uploading.html#downloading-the-current-encryption-key) , um zu erfahren, wie Sie die Subkey-ID abrufen.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch unter [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Lesen [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](/help/destinations/ui/activate-batch-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

### Planung {#scheduling}

Im [!UICONTROL Planung] erstellen Sie für jedes Segment einen Exportzeitplan mit den unten aufgeführten Einstellungen.

>[!IMPORTANT]
>
>Alle für dieses Ziel aktivierten Segmente müssen mit exakt demselben Zeitplan konfiguriert werden, wie unten dargestellt.

* **[!UICONTROL Dateiexportoptionen]**: [!UICONTROL Exportieren von vollständigen Dateien]. [Inkrementelle Dateiexporte](../../ui/activate-batch-profile-destinations.md#export-incremental-files) werden derzeit nicht unterstützt für [!DNL LiveRamp] Ziel.
* **[!UICONTROL Häufigkeit]**: [!UICONTROL Täglich]
* Festlegen der Exportzeit auf **[!UICONTROL Nach Segmentbewertung]**. Geplante Segmentexporte und [On-Demand-Dateiexporte](../../ui/export-file-now.md) werden derzeit nicht unterstützt für [!DNL LiveRamp] Ziel.
* **[!UICONTROL Datum]**: Wählen Sie die Start- und Endzeiten des Exports nach Wunsch aus.

![Screenshot der Platform-Benutzeroberfläche mit dem Schritt zur Segmentplanung.](../../assets/catalog/advertising/liveramp/liveramp-segment-scheduling.png)

Der exportierte Dateiname kann derzeit nicht vom Benutzer konfiguriert werden. Alle Dateien, die in die [!DNL LiveRamp SFTP] Ziel wird automatisch anhand der folgenden Vorlage benannt:

`%ORGANIZATION_NAME%_%DESTINATION%_%DESTINATION_INSTANCE_ID%_%DATETIME%`

![Screenshot der Platform-Benutzeroberfläche mit der Vorlage für den exportierten Dateinamen.](../../assets/catalog/advertising/liveramp/liveramp-file-name.png)

Beispielsweise der Name einer exportierten Datei für eine Organisation mit dem Namen [!DNL Luma] könnte in etwa wie folgt aussehen:

```json
Luma_LiveRamp_52137231-4a99-442d-804c-39a09ddd005d_20230330_153857.csv
```

### Zuordnen von Attributen und Identitäten {#map}

Im **[!UICONTROL Zuordnung]** Schritt, können Sie auswählen, welche Attribute und Identitäten Sie für Ihre Profile exportieren möchten.

>[!IMPORTANT]
>
>Dieses Ziel unterstützt die Aktivierung eines Quell-Identitäts-Namespace pro Aktivierungsfluss. Wenn Sie mehrere Identitäts-Namespaces exportieren müssen, z. B. `Email` und `Phone`, müssen Sie [Erstellen eines separaten Aktivierungsflusses](../../ui/activate-batch-profile-destinations.md) für jede Identität.

Im **[!UICONTROL Zuordnung]** Schritt, die **[!UICONTROL Zielfeld]** -Zuordnung definiert den Namen der Spaltenüberschrift in der exportierten CSV-Datei. Sie können die CSV-Spaltenüberschriften in der exportierten Datei in einen beliebigen Anzeigenamen ändern, indem Sie einen benutzerdefinierten Namen für die **[!UICONTROL Zielfeld]**.

1. Wählen Sie Im Schritt **[!UICONTROL Zuordnung]** die Option **[!UICONTROL Neue Zuordnung hinzufügen]** aus. Auf dem Bildschirm wird eine neue Zuordnungszeile angezeigt.

   ![Bildschirme der Benutzeroberfläche der Experience Platform zeigen den Bildschirm &quot;Zuordnung&quot;.](../../assets/catalog/advertising/liveramp/liveramp-add-new-mapping.png)

2. Im **[!UICONTROL Quellfeld auswählen]** Fenster, wählen Sie die **[!UICONTROL Attribute auswählen]** und wählen Sie das XDM-Attribut aus, das Sie zuordnen möchten, oder wählen Sie die **[!UICONTROL Identitäts-Namespace auswählen]** und wählen Sie eine Identität aus, die Ihrem Ziel zugeordnet werden soll.

   ![Bildschirme der Experience Platform-Benutzeroberfläche zeigen den Bildschirm &quot;Quellzuordnung&quot;.](../../assets/catalog/advertising/liveramp/liveramp-source-mapping.png)

3. Im **[!UICONTROL Zielgruppenfeld auswählen]** eingeben, geben Sie den Attributnamen ein, dem Sie das ausgewählte Quellfeld zuordnen möchten. Der hier definierte Attributname spiegelt sich in der exportierten CSV-Datei als Spaltenüberschrift wider.

   ![Bildschirme der Benutzeroberfläche der Experience Platform zeigen den Bildschirm Zielzuordnung an.](../../assets/catalog/advertising/liveramp/liveramp-target-mapping.png)

   Sie können den Attributnamen auch eingeben, indem Sie ihn direkt in die **[!UICONTROL Zielfeld]**.

   ![Bildschirme der Benutzeroberfläche der Experience Platform zeigen den Bildschirm Zielzuordnung an.](../../assets/catalog/advertising/liveramp/liveramp-target-field.png)

Nachdem Sie alle gewünschten Zuordnungen hinzugefügt haben, wählen Sie **[!UICONTROL Nächste]** und beenden Sie den Aktivierungs-Workflow.

## Export von Daten/Export validieren {#exported-data}

Ihre Daten werden in die [!DNL LiveRamp SFTP] Speicherort, den Sie konfiguriert haben, als CSV-Dateien.

Beim Exportieren von Dateien in [!DNL LiveRamp SFTP] Ziel: Platform generiert für jede [Zusammenführungsrichtlinienkennung](../../../profile/merge-policies/overview.md).

Betrachten wir beispielsweise die folgenden Segmente:

* Segment A (Zusammenführungsrichtlinie 1)
* Segment B (Zusammenführungsrichtlinie 2)
* Segment C (Zusammenführungsrichtlinie 1)
* Segment D (Zusammenführungsrichtlinie 1)

Platform exportiert zwei CSV-Dateien nach [!DNL LiveRamp SFTP]:

* Eine CSV-Datei mit den Segmenten A, C und D;
* Eine CSV-Datei, die Segment B enthält.

Exportierte CSV-Dateien enthalten Profile mit den ausgewählten Attributen und dem entsprechenden Segmentstatus in separaten Spalten mit dem Attributnamen und den Segment-IDs als Spaltenüberschriften.

Die in den exportierten Dateien enthaltenen Profile können mit einem der folgenden Segmentqualifikationsstatus übereinstimmen:

* `Active`: Das Profil ist derzeit für das Segment qualifiziert.
* `Expired`: Das Profil ist nicht mehr für das Segment qualifiziert, hat sich jedoch in der Vergangenheit qualifiziert.
* `""`(leere Zeichenfolge): Das Profil hat sich nie für das Segment qualifiziert.


Beispiel: eine exportierte CSV-Datei mit einer `email` -Attribut und drei Segmente könnten wie folgt aussehen:

```csv
email,aa2e3d98-974b-4f8b-9507-59f65b6442df,45d4e762-6e57-4f2f-a3e0-2d1893bcdd7f,7729e537-4e42-418e-be3b-dce5e47aaa1e
abc117@testemailabc.com,active,,
abc111@testemailabc.com,,,active
abc102@testemailabc.com,,,active
abc116@testemailabc.com,active,,
abc107@testemailabc.com,active,expired,active
abc101@testemailabc.com,active,active,
```

Da Platform eine CSV-Datei für jede [Zusammenführungsrichtlinienkennung](../../../profile/merge-policies/overview.md), generiert es außerdem einen separaten Datenfluss für jede Zusammenführungsrichtlinien-ID.

Das bedeutet, dass die Variable **[!UICONTROL Aktivierte Identitäten]** und **[!UICONTROL Vorgenommene Profile]** Metriken in [Datenfluss-Ausführung](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) -Seite werden für jede Gruppe von Segmenten aggregiert, die dieselbe Zusammenführungsrichtlinie verwenden, anstatt für jedes Segment angezeigt zu werden.

Infolge der Generierung von Datenfluss-Läufen für eine Gruppe von Segmenten, die dieselbe Zusammenführungsrichtlinie verwenden, werden die Segmentnamen nicht in der [Monitoring-Dashboard](../../../dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations).

![Bildschirme der Experience Platform-Benutzeroberfläche zeigen die aktivierte Metrik der Identitäten an.](../../assets/catalog/advertising/liveramp/liveramp-metrics.png)

## Hochladen exportierter Daten in LiveRamp {#upload-to-liveramp}

Nachdem Ihre Daten erfolgreich in die [!DNL LiveRamp - SFTP] speichern, müssen Sie die Daten in die [!DNL LiveRamp] Plattform.

Siehe **Nächste Schritte** im Abschnitt [Daten in LiveRamp übertragen](https://docs.liveramp.com/connect/en/getting-your-data-into-liveramp.html) Dokumentation finden Sie weitere Anweisungen.

## Datennutzung und -Governance {#data-usage-governance}

Alle [!DNL Adobe Experience Platform]-Ziele sind bei der Verarbeitung Ihrer Daten mit Datennutzungsrichtlinien konform. Ausführliche Informationen darüber, wie [!DNL Adobe Experience Platform] Data Governance erzwingt, finden Sie unter [Data Governance - Übersicht](/help/data-governance/home.md).

## Zusätzliche Ressourcen {#additional-resources}

Weitere Informationen zum Konfigurieren des LiveRamp SFTP-Speichers finden Sie unter [amtliche Dokumentation](https://docs.liveramp.com/connect/en/upload-a-file-via-liveramp-s-sftp.html).
