---
keywords: E-Mail; E-Mail; E-Mail; E-Mail-Ziele; Adobe Campaign; Kampagne
title: Adobe Campaign-Verbindung
description: Adobe Campaign umfasst verschiedene Lösungen, mit denen Sie Kampagnen über alle Ihre Online- und Offline-Kanäle hinweg personalisieren und bereitstellen können.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: dd18350387aa6bdeb61612f0ccf9d8d2223a8a5d
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 22%

---

# Adobe Campaign-Verbindung

## Übersicht {#overview}

Adobe Campaign umfasst verschiedene Lösungen, mit denen Sie Kampagnen über alle Ihre Online- und Offline-Kanäle hinweg personalisieren und bereitstellen können. Siehe [Erste Schritte mit Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html?lang=de) für weitere Informationen.

Um Segmentdaten an Adobe Campaign zu senden, müssen Sie zunächst [Ziel verbinden](#connect-destination) in Adobe Experience Platform und dann [Datenimport einrichten](#import-data-into-campaign) von Ihrem Speicherort zu Adobe Campaign.

## Exportart und -frequenz {#export-type-frequency}

Informationen zum Zielexporttyp und zur Häufigkeit finden Sie in der unten stehenden Tabelle.

| Element | Typ | Anmerkungen |
---------|----------|---------|
| Exporttyp | **[!UICONTROL Profilbasiert]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm Profilattribute im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes). |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Mehr dazu [Batch-dateibasierte Ziele](/help/destinations/destination-types.md#file-based). |

{style=&quot;table-layout:auto&quot;}

## IP-Adressen-Zulassungsliste {#allow-list}

Beim Einrichten von E-Mail-Marketing-Zielen mit SFTP-Speicher empfiehlt Adobe, bestimmte IP-Bereiche zu Ihrer Zulassungsliste hinzuzufügen.

Siehe [IP-Adressen-Zulassungsliste für Cloud-Speicher-Ziele](../cloud-storage/ip-address-allow-list.md) , wenn Sie Ihrer Zulassungsliste Adobe-IPs hinzufügen müssen.

## Herstellen einer Verbindung mit der Datenbank {#connect}

>[!IMPORTANT]
> 
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Ziele verwalten]** [Zugriffsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.

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
* Für **[!UICONTROL SFTP mit Kennwort]** Verbindungen, müssen Sie [!UICONTROL Domäne], [!UICONTROL Port], [!UICONTROL Benutzername]und [!UICONTROL Passwort].
* Für **[!UICONTROL SFTP mit SSH-Schlüssel]** Verbindungen, müssen Sie [!UICONTROL Domäne], [!UICONTROL Port], [!UICONTROL Benutzername]und [!UICONTROL SSH-Schlüssel].
* Für **[!UICONTROL Azure Blob]** -Verbindungen, müssen Sie eine Verbindungszeichenfolge angeben.
* Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um eine Verschlüsselung mit PGP/GPG zu Ihren exportierten Dateien unter dem **[!UICONTROL Schlüssel]** Abschnitt. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierter String.
* **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
* **[!UICONTROL Bucket-Name]**: *Bei S3-Verbindungen*. Geben Sie den Speicherort Ihres S3-Buckets ein, in dem [!DNL Platform] Ihre Exportdaten werden als CSV-Dateien hinterlegt.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad in Ihrem Speicherort an, in dem [!DNL Platform] Ihre Exportdaten werden als CSV-Dateien hinterlegt.
* **[!UICONTROL Container]**: *Für Blob-Verbindungen*. Der Container, der den Blob enthält, in dem sich Ihr Ordnerpfad befindet.
* **[!UICONTROL Dateiformat]**: Auswählen **CSV** , um CSV-Dateien an Ihren Speicherort zu exportieren.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen über den Status des Datenflusses an Ihr Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnungen finden Sie im Handbuch zu [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie alle Details für Ihre Zielverbindung angegeben haben, wählen Sie **[!UICONTROL Nächste]**.

## Aktivieren von Segmenten für dieses Ziel {#activate}

>[!IMPORTANT]
> 
>Um Daten zu aktivieren, benötigen Sie die **[!UICONTROL Ziele verwalten]**, **[!UICONTROL Ziele aktivieren]**, **[!UICONTROL Profile anzeigen]** und **[!UICONTROL Segmente anzeigen]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten.


Siehe [Aktivieren von Zielgruppendaten für Batch-Profil-Export-Ziele](../../ui/activate-batch-profile-destinations.md) für Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel.

### Zielattribute {#destination-attributes}

Beim Aktivieren von Segmenten für dieses Ziel empfiehlt Adobe, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter [Best Practices beim Aktivieren von Zielgruppen für E-Mail-Marketing-Ziele](overview.md#best-practices).

## Exportierte Daten {#exported-data}

Für [!DNL Adobe Campaign] Ziele, [!DNL Platform] erstellt eine `.csv` -Datei in dem von Ihnen angegebenen Speicherort gespeichert. Weitere Informationen zu den Dateien finden Sie unter [Segmentaktivierung überprüfen](../../ui/activate-batch-profile-destinations.md#verify) im Tutorial zur Segmentaktivierung.

## Datenimport in Adobe Campaign einrichten {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Beachten Sie Folgendes [!DNL SFTP] Speicherbeschränkungen, Beschränkungen des Datenbankspeichers und Einschränkungen für aktive Profile gemäß Ihrem Adobe Campaign-Vertrag bei der Durchführung dieser Integration.
>* Sie müssen Ihre exportierten Segmente in Adobe Campaign planen, importieren und zuordnen, indem Sie [!DNL Campaign] Workflows. Siehe [Einrichten eines wiederkehrenden Imports](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html?lang=de) in der Dokumentation zu Adobe Campaign Classic und [Über Datenverwaltungsaktivitäten](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) in der Adobe Campaign Standard-Dokumentation.
>* Die bevorzugte Methode zum Senden von Daten an Adobe Campaign besteht darin, [!DNL Amazon S3] oder [!DNL Azure Blob].


Nach Anschluss [!DNL Platform] auf [!DNL Amazon S3] oder [!DNL Azure Blob] speichern, müssen Sie den Datenimport von Ihrem Speicherort zu Adobe Campaign einrichten. Weiterführende Informationen dazu finden Sie auf den folgenden Adobe Campaign-Dokumentationsseiten:
* [Erste Schritte mit dem Datenimport und -export](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=de#getting-started) und [Laden (Datei)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html?lang=de) in der Adobe Campaign Classic-Dokumentation.
* [Erste Schritte mit Prozessen und Daten-Management](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) und [Datei laden](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) in der Adobe Campaign Standard-Dokumentation.
