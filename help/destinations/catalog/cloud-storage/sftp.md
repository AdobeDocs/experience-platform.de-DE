---
title: SFTP-Verbindung
description: Stellen Sie mit Ihrem SFTP-Server eine aktive ausgehende Verbindung her, um durch Trennzeichen getrennte Datendateien regelmäßig von Adobe Experience Platform zu exportieren.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1182'
ht-degree: 31%

---

# SFTP-Verbindung

## Ziel-Änderungsprotokoll {#changelog}

Mit der Experience Platform-Version vom Juli 2023 bietet das SFTP-Ziel neue Funktionen, wie unten aufgeführt:

* [Unterstützung für den Datensatzexport](/help/destinations/ui/export-datasets.md).
* Zusätzliche [Dateibenennungsoptionen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Möglichkeit zum Festlegen benutzerdefinierter Datei-Kopfzeilen in exportierten Dateien durch den [verbesserten Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Möglichkeit zum Anpassen der Formatierung exportierter CSV-Datendateien](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Übersicht {#overview}

Stellen Sie mit Ihrem SFTP-Server eine aktive ausgehende Verbindung her, um durch Trennzeichen getrennte Datendateien regelmäßig von Adobe Experience Platform zu exportieren.

>[!IMPORTANT]
>
> Experience Platform unterstützt zwar Datenexporte an SFTP-Server, die empfohlenen Cloud-Speicherorte zum Exportieren von Daten sind jedoch [!DNL Amazon S3] und [!DNL Azure Blob].

## Herstellen einer Verbindung zu SFTP über API oder Benutzeroberfläche {#connect-api-or-ui}

* Um über die Experience Platform-Benutzeroberfläche eine Verbindung zu Ihrem SFTP-Speicherort herzustellen, lesen Sie die Abschnitte [Mit dem Ziel verbinden](#connect) und [Zielgruppen für dieses Ziel aktivieren](#activate).
* Um programmgesteuert eine Verbindung zu Ihrem SFTP-Speicherort herzustellen, lesen Sie den Abschnitt [Aktivieren von Zielgruppen für dateibasierte Ziele mithilfe des Tutorials zur Flow Service-API](../../api/activate-segments-file-based-destinations.md).

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
|---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/audience-portal.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![SFTP-Profil-basierter Exporttyp, der im Zielkatalog hervorgehoben ist.](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Datensätze exportieren {#export-datasets}

Dieses Ziel unterstützt Datensatzexporte. Vollständige Informationen zum Einrichten von Datensatzexporten finden Sie in den Tutorials:

* So [&#x200B; Sie Datensätze mithilfe der Benutzeroberfläche von Experience Platform &#x200B;](/help/destinations/ui/export-datasets.md).
* So [&#x200B; Sie Datensätze mithilfe der Flow Service-API programmgesteuert &#x200B;](/help/destinations/api/export-datasets.md).

## Dateiformat der exportierten Daten {#file-format}

Beim Exportieren *Zielgruppendaten* erstellt Experience Platform eine `.csv`-, `parquet`- oder `.json`-Datei an dem von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie im Abschnitt [Unterstützte Dateiformate für den Export](../../ui/activate-batch-profile-destinations.md#supported-file-formats-export) im Tutorial zur Zielgruppenaktivierung.

Beim Exportieren *Datensätze* erstellt Experience Platform eine `.parquet`- oder `.json`-Datei an dem von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie im Abschnitt [Überprüfen eines erfolgreichen Datensatzexports](../../ui/export-datasets.md#verify) im Tutorial zum Exportieren von Datensätzen.

## Verbindungsanforderungen für SFTP-Server {#sftp-connection-requirements}

Um einen erfolgreichen Datenexport sicherzustellen, müssen Sie Ihren Ziel-SFTP-Server so konfigurieren, dass er eine ausreichende Anzahl gleichzeitiger Verbindungen zulässt. Wenn Ihr SFTP-Server die Anzahl der gleichzeitigen Verbindungen begrenzt, kann es zu Fehlern bei Exportvorgängen kommen, insbesondere wenn mehrere Zielgruppen oder Datensätze gleichzeitig exportiert werden.

**Empfehlung**
Um eine optimale Leistung zu erzielen, sollte Ihr SFTP-Server für jede exportierte Zielgruppe oder jeden exportierten Datensatz mindestens eine gleichzeitige Verbindung zulassen. Der Server sollte mindestens 30 % der Gesamtzahl der Zielgruppen oder Datensätze unterstützen, die gleichzeitig für den Export geplant sind.

**Beispiel**\
Wenn Sie Exporte für 100 Zielgruppen oder Datensätze gleichzeitig planen, sollte Ihr SFTP-Server mindestens 30 gleichzeitige Verbindungen zulassen.

Die ordnungsgemäße Konfiguration der Verbindungsbeschränkungen Ihres SFTP-Servers verhindert fehlgeschlagene Exporte und stellt eine zuverlässige Datenbereitstellung von Adobe Experience Platform sicher.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL View Destinations]** und **[!UICONTROL Manage Destinations]** Zugriffssteuerungsberechtigungen[. &#x200B;](/help/access-control/home.md#permissions) Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Authentifizierungsinformationen {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Öffentlicher RSA-Schlüssel"
>abstract="Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Schlüssel finden Sie im folgenden Dokumentations-Link."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Privater SSH-Schlüssel"
>abstract="Der private SSH-Schlüssel muss eine RSA-formatierte, Base64-kodierte Zeichenfolge sein und darf nicht Passwort-geschützt sein."

Wenn Sie den Authentifizierungstyp **[!UICONTROL SFTP with password]** für die Verbindung mit Ihrem SFTP-Speicherort auswählen:

![Einfache Authentifizierung für SFTP-Ziel mit Passwort.](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Domain]**: die Adresse Ihres SFTP-Speicherorts;
* **[!UICONTROL Username]**: Der Benutzername für die Anmeldung bei Ihrem SFTP-Speicherort.
* **[!UICONTROL Port]**: Der von Ihrem SFTP-Speicherort verwendete Port.
* **[!UICONTROL Password]**: Das Kennwort zum Anmelden bei Ihrem SFTP-Speicherort.
* **[!UICONTROL Encryption key]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der folgenden Abbildung.

  ![Abbildung mit einem Beispiel für einen korrekt formatierten PGP-Schlüssel in der Benutzeroberfläche.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Wenn Sie den Authentifizierungstyp **[!UICONTROL SFTP with SSH key]** für die Verbindung mit Ihrem SFTP-Speicherort auswählen:

![Authentifizierung beim SFTP-Ziel mit SSH-Schlüssel.](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domain]**: Geben Sie die IP-Adresse oder den Domain-Namen Ihres SFTP-Kontos ein.
* **[!UICONTROL Port]**: Der von Ihrem SFTP-Speicherort verwendete Port.
* **[!UICONTROL Username]**: Der Benutzername für die Anmeldung bei Ihrem SFTP-Speicherort.
* **[!UICONTROL SSH Key]**: Der private SSH-Schlüssel, der zum Anmelden bei Ihrem SFTP-Speicherort verwendet wird. Der private Schlüssel muss eine RSA-formatierte, Base64-codierte Zeichenfolge sein und darf nicht kennwortgeschützt sein.
* **[!UICONTROL Encryption key]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der folgenden Abbildung.

  ![Abbildung mit einem Beispiel für einen korrekt formatierten PGP-Schlüssel in der Benutzeroberfläche.](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Zieldetails {#destination-details}

Geben Sie nach Herstellung der Authentifizierungsverbindung zum SFTP-Speicherort die folgenden Informationen für das Ziel ein:

![Felder mit Zieldetails für das SFTP-Ziel.](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels in der Benutzeroberfläche von Experience Platform hilft.
* **[!UICONTROL Description]**: Geben Sie eine Beschreibung für dieses Ziel ein.
* **[!UICONTROL Folder path]**: Geben Sie den Pfad zum Ordner in Ihrem SFTP-Speicherort ein, in den die Dateien exportiert werden sollen.
* **[!UICONTROL File type]**: Wählen Sie das Format aus, das Experience Platform für die exportierten Dateien verwenden soll. Bei Auswahl der Option [!UICONTROL CSV] können Sie auch [die Dateiformatierungsoptionen konfigurieren](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Compression format]**: Wählen Sie den Komprimierungstyp aus, den Experience Platform für die exportierten Dateien verwenden soll.
* **[!UICONTROL Include manifest file]**: Schalten Sie diese Option ein, wenn die Exporte eine JSON-Manifestdatei enthalten sollen, die Informationen zum Exportspeicherort, zur Exportgröße und mehr enthält. Das Manifest wird mit dem Format `manifest-<<destinationId>>-<<dataflowRunId>>.json` benannt. Anzeigen einer [Beispielmanifestdatei](/help/destinations/assets/common/manifest-d0420d72-756c-4159-9e7f-7d3e2f8b501e-0ac8f3c0-29bd-40aa-82c1-f1b7e0657b19.json). Die Manifestdatei enthält die folgenden Felder:
   * `flowRunId`: Die [Datenflussausführung](/help/dataflows/ui/monitor-destinations.md#dataflow-runs-for-batch-destinations) die die exportierte Datei generiert hat.
   * `scheduledTime`: Die Zeit in UTC, zu der die Datei exportiert wurde.
   * `exportResults.sinkPath`: Der Pfad an Ihrem Speicherort, an dem die exportierte Datei abgelegt wird.
   * `exportResults.name`: Der Name der exportierten Datei.
   * `size`: Die Größe der exportierten Datei in Byte.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[&#x200B; &#x200B;](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}

Anweisungen [&#x200B; Aktivieren von Zielgruppen für dieses Ziel finden Sie &#x200B;](../../ui/activate-batch-profile-destinations.md)Aktivieren von Zielgruppendaten für Batch-Profil-).

## Überprüfen auf einen erfolgreichen Datenexport {#exported-data}

Um festzustellen, ob die Daten erfolgreich exportiert wurden, überprüfen Sie Ihren SFTP-Speicher und stellen Sie sicher, dass die exportierten Dateien die erwarteten Profilpopulationen enthalten.

## Zulassungsliste von IP-Adressen {#ip-address-allow-list}

Siehe den Artikel [IP-Adresse](ip-address-allow-list.md) , wenn Sie einer Zulassungsliste Adobe auf die Zulassungsliste setzen-IPs hinzufügen müssen.
