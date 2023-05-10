---
keywords: SFTP;sftp
title: SFTP-Verbindung
description: Stellen Sie mit Ihrem SFTP-Server eine aktive ausgehende Verbindung her, um durch Trennzeichen getrennte Datendateien regelmäßig von Adobe Experience Platform zu exportieren.
exl-id: 27abfc38-ec19-4321-b743-169370d585a0
source-git-commit: cb0b80f79a849d81216c5500c54b62ac5d85e2f6
workflow-type: tm+mt
source-wordcount: '870'
ht-degree: 92%

---

# SFTP-Verbindung

## Ziel-Änderungsprotokoll {#changelog}

>[!IMPORTANT]
>
>Mit der Beta-Version der Funktion zum Exportieren von Datensätzen und der verbesserten Dateiexportfunktion werden Ihnen jetzt möglicherweise zwei [!DNL SFTP]-Karten im Zielkatalog angezeigt.
>* Falls Sie bereits Dateien zum **[!UICONTROL SFTP]**-Ziel exportieren, erstellen Sie bitte neue Datenflüsse zum neuen **[!UICONTROL SFTP-Beta]**-Ziel.
>* Wenn Sie noch keinen Datenfluss zum **[!UICONTROL SFTP]**-Ziel erstellt haben, verwenden Sie bitte die neue **[!UICONTROL SFTP-Beta]**-Karte zum Exportieren von Dateien in **[!UICONTROL SFTP]**.


![Abbildung der beiden SFTP-Zielkarten, die diese nebeneinander in einer Ansicht zeigt.](../../assets/catalog/cloud-storage/sftp/two-sftp-destination-cards.png)

Zu den Verbesserungen bei den neuen [!DNL SFTP]-Zielkarte gehören:

* [Unterstützung für den Datensatzexport](/help/destinations/ui/export-datasets.md).
* Zusätzliche [Dateibenennungsoptionen](/help/destinations/ui/activate-batch-profile-destinations.md#scheduling).
* Möglichkeit zum Festlegen benutzerdefinierter Datei-Kopfzeilen in exportierten Dateien durch den [verbesserten Zuordnungsschritt](/help/destinations/ui/activate-batch-profile-destinations.md#mapping).
* [Möglichkeit zum Anpassen der Formatierung exportierter CSV-Datendateien](/help/destinations/ui/batch-destinations-file-formatting-options.md).

## Übersicht {#overview}

Stellen Sie mit Ihrem SFTP-Server eine aktive ausgehende Verbindung her, um durch Trennzeichen getrennte Datendateien regelmäßig von Adobe Experience Platform zu exportieren.

>[!IMPORTANT]
>
> Experience Platform unterstützt zwar Datenexporte an SFTP-Server, die empfohlenen Cloud-Speicherorte zum Exportieren von Daten sind jedoch [!DNL Amazon S3] und [!DNL SFTP].

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

![SFTP-Profil-basierter Exporttyp](../../assets/catalog/cloud-storage/sftp/catalog.png)

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle – Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor. Füllen Sie im Workflow zum Konfigurieren des Ziels die Felder aus, die in den beiden folgenden Abschnitten aufgeführt sind.

### Authentifizierungsinformationen {#authentication-information}

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_rsa"
>title="Öffentlicher RSA-Schlüssel"
>abstract="Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Schlüssel finden Sie im folgenden Dokumentations-Link."

>[!CONTEXTUALHELP]
>id="platform_destinations_connect_sftp_ssh"
>title="Privater SSH-Schlüssel"
>abstract="Der private SSH-Schlüssel muss als eine mit Base64 verschlüsselte Zeichenfolge formatiert sein und darf nicht kennwortgeschützt sein."

Wenn Sie den Typ **[!UICONTROL Einfache Authentifizierung]** wählen, um eine Verbindung zu Ihrem SFTP-Speicherort herzustellen:

![Einfache Authentifizierung für SFTP-Ziel](../../assets/catalog/cloud-storage/sftp/stfp-basic-authentication.png)

* **[!UICONTROL Host]**: Die Adresse Ihres SFTP-Speicherorts.
* **[!UICONTROL Benutzername]**: Der Benutzername, mit dem Sie sich bei Ihrem SFTP-Speicherort anmelden.
* **[!UICONTROL Passwort]**: Das Passwort, mit dem Sie sich bei Ihrem SFTP-Speicherort anmelden.
* **[!UICONTROL Verschlüsselungsschlüssel]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der folgenden Abbildung.

   ![Abbildung eines Beispiels für einen korrekt formatierten PGP-Schlüssel in der Benutzeroberfläche](../../assets/catalog/cloud-storage/sftp/pgp-key.png)


Wenn Sie den Authentifizierungstyp **[!UICONTROL SFTP mit SSH-Schlüssel]** für die Verbindung mit Ihrem SFTP-Speicherort auswählen:

![Authentifizierung bei SFTP-Ziel mit SSH-Schlüssel](../../assets/catalog/cloud-storage/sftp/sftp-ssh-key-authentication.png)

* **[!UICONTROL Domain]**: Geben Sie die IP-Adresse oder den Domain-Namen Ihres SFTP-Kontos ein.
* **[!UICONTROL Port]**: Der von Ihrem SFTP-Speicherort verwendete Port.
* **[!UICONTROL Benutzername]**: Der Benutzername, mit dem Sie sich bei Ihrem SFTP-Speicherort anmelden.
* **[!UICONTROL SSH-Schlüssel]**: Der private SSH-Schlüssel, der zum Anmelden bei Ihrem SFTP-Speicherort verwendet wird. Der private Schlüssel muss als eine mit Base64 verschlüsselte Zeichenfolge formatiert sein und darf nicht kennwortgeschützt sein.
* **[!UICONTROL Verschlüsselungsschlüssel]**: Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. Ein Beispiel für einen korrekt formatierten Verschlüsselungsschlüssel finden Sie in der folgenden Abbildung.

   ![Abbildung eines Beispiels für einen korrekt formatierten PGP-Schlüssel in der Benutzeroberfläche](../../assets/catalog/cloud-storage/sftp/pgp-key.png)

### Zieldetails {#destination-details}

Geben Sie nach Herstellung der Authentifizierungsverbindung zum SFTP-Speicherort die folgenden Informationen für das Ziel ein:

![Verfügbare Zieldetails für SFTP-Ziel](../../assets/catalog/cloud-storage/sftp/sftp-destination-details.png)

* **[!UICONTROL Name]**: Geben Sie einen Namen ein, der Ihnen bei der Identifizierung dieses Ziels in der Benutzeroberfläche von Experience Platform hilft.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für das Ziel ein.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad zum Ordner in Ihrem SFTP-Speicherort ein, in den die Dateien exportiert werden sollen.
* **[!UICONTROL Dateityp]**: Wählen Sie die Format-Experience Platform aus, die für die exportierten Dateien verwendet werden soll. Diese Option steht nur für die **[!UICONTROL SFTP-Beta]** Ziel. Bei der Auswahl der [!UICONTROL CSV] können Sie auch [Dateiformatierungsoptionen konfigurieren](../../ui/batch-destinations-file-formatting-options.md).
* **[!UICONTROL Komprimierungsformat]**: Wählen Sie den Komprimierungstyp aus, den die Experience Platform für die exportierten Dateien verwenden soll. Diese Option steht nur für die **[!UICONTROL SFTP-Beta]** Ziel.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]**. Lesen Sie die [Übersicht über die Zugriffskontrolle](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../../ui/activate-batch-profile-destinations.md).

## (Beta) Exportieren von Datensätzen {#export-datasets}

Dieses Ziel unterstützt Datensatzexporte. Umfassende Informationen zum Einrichten von Datensatzexporten finden Sie im [Tutorial zum Exportieren von Datensätzen](/help/destinations/ui/export-datasets.md).

## Exportierte Daten {#exported-data}

Für [!DNL SFTP]-Ziele erstellt Platform eine `.csv`-Datei an dem von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profil-Exportziele](../../ui/activate-batch-profile-destinations.md) im Tutorial zur Segmentaktivierung.

## IP-Adressen-Zulassungsliste

Siehe [IP-Adressen-Zulassungsliste für Cloud-Speicher-Ziele](ip-address-allow-list.md), wenn Sie Adobe-IPs zu einer Zulassungsliste hinzufügen müssen.
