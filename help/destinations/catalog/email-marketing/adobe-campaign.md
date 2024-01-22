---
keywords: E-Mail; E-Mail; E-Mail; E-Mail-Ziele; Adobe Campaign; Kampagne
title: Adobe Campaign-Verbindung
description: Adobe Campaign umfasst verschiedene Lösungen, mit denen Sie Kampagnen über alle Ihre Online- und Offline-Kanäle hinweg personalisieren und bereitstellen können.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: c3ef732ee82f6c0d56e89e421da0efc4fbea2c17
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 38%

---

# Adobe Campaign-Verbindung

## Übersicht {#overview}

Adobe Campaign umfasst verschiedene Lösungen, mit denen Sie Kampagnen über alle Ihre Online- und Offline-Kanäle hinweg personalisieren und bereitstellen können. Siehe [Erste Schritte mit Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html?lang=de) für weitere Informationen.

Um Zielgruppendaten an Adobe Campaign zu senden, müssen Sie zunächst [Ziel verbinden](#connect-destination) in Adobe Experience Platform und dann [Datenimport einrichten](#import-data-into-campaign) von Ihrem Speicherort zu Adobe Campaign.

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Zielgruppentypen Sie an dieses Ziel exportieren können.

| Audience Origin | Unterstützt | Beschreibung |
---------|----------|----------|
| [!DNL Segmentation Service] | ✓ | Über die Experience Platform generierte Zielgruppen [Segmentierungsdienst](../../../segmentation/home.md). |
| Benutzerdefinierte Uploads | ✓ | Zielgruppen, die aus CSV-Dateien in Experience Platform [importiert](../../../segmentation/ui/overview.md#import-audience) werden. |

{style="table-layout:auto"}

## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Zulassungsliste von IP-Adressen {#allow-list}

Beim Einrichten von E-Mail-Marketing-Zielen mit SFTP-Speicher empfiehlt Adobe, bestimmte IP-Bereiche zu Ihrer Zulassungsliste hinzuzufügen.

Siehe Abschnitt [IP-Adressen-Zulassungsliste für SFTP-Ziele](../cloud-storage/ip-address-allow-list.md) , wenn Sie Ihrer Zulassungsliste Adobe-IPs hinzufügen müssen.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die [Zugriffsberechtigung](/help/access-control/home.md#permissions) **[!UICONTROL Ziele verwalten]**. Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

Adobe Campaign unterstützt die folgenden Verbindungstypen:

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP mit Kennwort]**
* **[!UICONTROL SFTP mit SSH-Schlüssel]**
* **[!UICONTROL Azure Blob]**

Die bevorzugte Methode zum Senden von Daten an Adobe Campaign besteht darin, [!DNL Amazon S3] oder [!DNL Azure Blob].

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* Für **[!UICONTROL Amazon S3]** Verbindungen, müssen Sie Ihre [!UICONTROL Zugriffsschlüssel-ID] und [!UICONTROL Geheimer Zugriffsschlüssel].
* Für **[!UICONTROL SFTP mit Kennwort]** Verbindungen, müssen Sie [!UICONTROL Domäne], [!UICONTROL Port], [!UICONTROL Benutzername], und [!UICONTROL Passwort].
* Für **[!UICONTROL SFTP mit SSH-Schlüssel]** Verbindungen, müssen Sie [!UICONTROL Domäne], [!UICONTROL Port], [!UICONTROL Benutzername], und [!UICONTROL SSH-Schlüssel].
* Für **[!UICONTROL Azure Blob]** -Verbindungen, müssen Sie eine Verbindungszeichenfolge angeben.
* Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um eine Verschlüsselung mit PGP/GPG zu Ihren exportierten Dateien unter dem **[!UICONTROL Schlüssel]** Abschnitt. Ihr öffentlicher Schlüssel muss als eine mit [!DNL Base64] verschlüsselte Zeichenfolge verfasst sein.
* **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
* **[!UICONTROL Bucket-Name]**: *Bei S3-Verbindungen*. Geben Sie den Speicherort Ihres S3-Buckets ein, in dem [!DNL Platform] Ihre Exportdaten werden als CSV-Dateien hinterlegt.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad Ihres Speicherorts an, unter dem [!DNL Platform] Ihre Exportdaten werden als CSV-Dateien hinterlegt.
* **[!UICONTROL Container]**: *Für Blob-Verbindungen*. Der Container, der den Blob enthält, in dem sich Ihr Ordnerpfad befindet.
* **[!UICONTROL Dateiformat]**: Auswählen **CSV** , um CSV-Dateien an Ihren Speicherort zu exportieren.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung eingegeben haben, klicken Sie auf **[!UICONTROL Weiter]**.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>* Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele anzeigen]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Anzeigen von Profilen]**, und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Export *identities*, benötigen Sie die **[!UICONTROL Identitätsdiagramm anzeigen]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). <br> ![Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie im Workflow hervorgehobenen Identitäts-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}


Siehe [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppen für dieses Ziel.

### Zielattribute {#destination-attributes}

Beim Aktivieren von Zielgruppen für dieses Ziel empfiehlt Adobe, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter [Best Practices beim Aktivieren von Zielgruppen für E-Mail-Marketing-Ziele](overview.md#best-practices).

## Exportierte Daten {#exported-data}

Für [!DNL Adobe Campaign]-Ziele erstellt [!DNL Platform] eine `.csv`-Datei an dem von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie unter [Überprüfen der Zielgruppenaktivierung](../../ui/activate-batch-profile-destinations.md#verify) im Tutorial zur Aktivierung der Zielgruppe.

## Datenimport in Adobe Campaign einrichten {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Beachten Sie Folgendes [!DNL SFTP] Speicherbeschränkungen, Beschränkungen des Datenbankspeichers und Einschränkungen für aktive Profile gemäß Ihrem Adobe Campaign-Vertrag bei der Durchführung dieser Integration.
>* Sie müssen Ihre exportierten Segmente in Adobe Campaign planen, importieren und zuordnen, indem Sie [!DNL Campaign] Workflows. Siehe Abschnitt [Einrichten eines wiederkehrenden Imports](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html?lang=de) in der Dokumentation zu Adobe Campaign Classic und [Über Datenverwaltungsaktivitäten](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) in der Adobe Campaign Standard-Dokumentation.
>* Die bevorzugte Methode zum Senden von Daten an Adobe Campaign besteht darin, [!DNL Amazon S3] oder [!DNL Azure Blob].

Nach Anschluss [!DNL Platform] auf [!DNL Amazon S3] oder [!DNL Azure Blob] speichern, müssen Sie den Datenimport von Ihrem Speicherort zu Adobe Campaign einrichten. Weiterführende Informationen dazu finden Sie auf den folgenden Adobe Campaign-Dokumentationsseiten:
* [Erste Schritte mit dem Datenimport und -export](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=de#getting-started) und [Laden (Datei)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html?lang=de) in der Adobe Campaign Classic-Dokumentation.
* [Erste Schritte mit Prozessen und Daten-Management](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) und [Datei laden](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) in der Adobe Campaign Standard-Dokumentation.
