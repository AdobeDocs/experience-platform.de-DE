---
keywords: email;E-Mail;E-Mail;E-Mail-Ziele;Adobe Campaign;Campaign
title: Adobe Campaign-Verbindung
description: Adobe Campaign umfasst verschiedene Lösungen, mit denen Sie Kampagnen über alle Ihre Online- und Offline-Kanäle hinweg personalisieren und bereitstellen können.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: d946d3dbb09c1fe0163fba3a892b4c0f1b331f87
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 29%

---

# [!DNL Adobe Campaign]-Verbindung

## Überblick {#overview}

[!DNL Adobe Campaign] umfasst eine Reihe von Lösungen, mit denen Sie Kampagnen personalisieren und auf allen Online- und Offline-Kanälen versenden können. Weitere Informationen [&#x200B; Sie unter „Erste Schritte &#x200B;](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html) Campaign Classic&quot;.

Um Zielgruppendaten an [!DNL Adobe Campaign] zu senden, müssen Sie zunächst in [&#x200B; &#x200B;](#connect-destination)das Ziel verbinden[!DNL Adobe Experience Platform] und dann [einen Datenimport einrichten](#import-data-into-campaign) von Ihrem Speicherort in [!DNL Adobe Campaign].

## Unterstützte Zielgruppen {#supported-audiences}

In diesem Abschnitt wird beschrieben, welche Arten von Zielgruppen Sie an dieses Ziel exportieren können.

| Zielgruppenherkunft | Unterstützt | Beschreibung |
| ---------|----------|----------|
| [!DNL Segmentation Service] | Ja | Zielgruppen, die über den Experience Platform-[&#x200B; (Segmentierungs-Service) generiert &#x200B;](../../../segmentation/home.md). |
| Alle anderen Ursprünge der Zielgruppe | Ja | Diese Kategorie enthält alle Ursprünge der Zielgruppe außerhalb der Zielgruppen, die durch die [!DNL Segmentation Service] generiert wurden. Lesen Sie mehr über [verschiedene Ursprünge von Audiences](/help/segmentation/ui/audience-portal.md#customize). Einige Beispiele: <ul><li> benutzerdefinierte Upload-Zielgruppen [importiert](../../../segmentation/ui/audience-portal.md#import-audience) aus CSV-Dateien in Experience Platform,</li><li> Lookalike-Zielgruppen, </li><li> Federated Audiences, </li><li> Zielgruppen, die in anderen Experience Platform-Apps generiert werden, z. B. [!DNL Adobe Journey Optimizer], </li><li> und mehr. </li></ul> |

{style="table-layout:auto"}



Unterstützte Zielgruppen nach Zielgruppen-Datentyp:

| Datentyp der Zielgruppe | Unterstützt | Beschreibung | Anwendungsfälle |
|--------------------|-----------|-------------|-----------|
| [Personen-Zielgruppen](/help/segmentation/types/people-audiences.md) | Ja | Basierend auf Kundenprofilen können Sie bestimmte Personengruppen für Marketing-Kampagnen ansprechen. | Häufige Käufer, Warenkorbabbrüche |
| [Konto-Zielgruppen](/help/segmentation/types/account-audiences.md) | Nein | Targeting von Personen in bestimmten Organisationen für Account-basierte Marketing-Strategien. | B2B-Marketing |
| [Interessenten-Zielgruppen](/help/segmentation/types/prospect-audiences.md) | Nein | Targeting von Personen, die noch keine Kunden sind, aber Merkmale mit Ihrer Zielgruppe teilen. | Akquise mit Drittanbieterdaten |
| [Datensatzexporte](/help/catalog/datasets/overview.md) | Nein | Sammlungen strukturierter Daten, die im Data Lake von [!DNL Adobe Experience Platform] gespeichert sind. | Reporting, Datenwissenschaft-Workflows |

{style="table-layout:auto"}


## Exporttyp und -häufigkeit {#export-type-frequency}

Beziehen Sie sich auf die folgende Tabelle, um Informationen zu Typ und Häufigkeit des Zielexports zu erhalten.

| Element | Typ | Anmerkungen |
|---------|----------|---------|
| Exporttyp | **[!UICONTROL Profile-based]** | Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B. E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm „Auswählen der Profilattribute“ im [Zielaktivierungs-Workflow](../../ui/activate-batch-profile-destinations.md#select-attributes) festgelegt. |
| Exporthäufigkeit | **[!UICONTROL Batch]** | Batch-Ziele exportieren Dateien in Schritten von drei, sechs, acht, zwölf oder vierundzwanzig Stunden auf nachgelagerte Plattformen. Weitere Informationen finden Sie unter [Batch-Datei-basierte Ziele](/help/destinations/destination-types.md#file-based). |

{style="table-layout:auto"}

## Zulassungsliste von IP-Adressen {#allow-list}

Beim Einrichten von E-Mail-Marketing-Zielen mit SFTP-Speicher empfiehlt Adobe, Ihrer Zulassungsliste bestimmte IP-Bereiche hinzuzufügen.

Siehe [IP-Adressen-Adobes für SFTP](../cloud-storage/ip-address-allow-list.md)Ziele, wenn Sie Ihrer Zulassungsliste IPs hinzufügen müssen.

## Herstellen einer Verbindung mit dem Ziel {#connect}

>[!IMPORTANT]
>
>Um eine Verbindung zum Ziel herzustellen, benötigen Sie die **[!UICONTROL Manage Destinations]** [Zugriffssteuerungsberechtigung](/help/access-control/home.md#permissions). Lesen Sie die [Zugriffskontrolle - Übersicht](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten

Um eine Verbindung mit diesem Ziel herzustellen, gehen Sie wie im Abschnitt [Tutorial zur Zielkonfiguration](../../ui/connect-destination.md) beschrieben vor.

[!DNL Adobe Campaign] unterstützt die folgenden Verbindungstypen:

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP with Password]**
* **[!UICONTROL SFTP with SSH Key]**
* **[!UICONTROL Azure Blob]**

Die bevorzugte Methode zum Senden von Daten an [!DNL Adobe Campaign] ist über [!DNL Amazon S3] oder [!DNL Azure Blob].

### Verbindungsparameter {#parameters}

Beim [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* Für **[!UICONTROL Amazon S3]** Verbindungen müssen Sie Ihre [!UICONTROL Access Key ID] und [!UICONTROL Secret Access Key] angeben.
* Für **[!UICONTROL SFTP with Password]** müssen Sie [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] und [!UICONTROL Password] angeben.
* Für **[!UICONTROL SFTP with SSH Key]** müssen Sie [!UICONTROL Domain], [!UICONTROL Port], [!UICONTROL Username] und [!UICONTROL SSH Key] angeben.
* Für **[!UICONTROL Azure Blob]** Verbindungen müssen Sie eine Verbindungszeichenfolge angeben.
* Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um Ihren exportierten Dateien unter dem Abschnitt **[!UICONTROL Key]** eine Verschlüsselung mit PGP/GPG hinzuzufügen. Ihr öffentlicher Schlüssel muss als eine mit [!DNL Base64] verschlüsselte Zeichenfolge verfasst sein.
* **[!UICONTROL Name]**: Wählen Sie einen relevanten Namen für Ihr Ziel aus.
* **[!UICONTROL Description]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
* **[!UICONTROL Bucket Name]**: *Für S3-*. Geben Sie den Speicherort Ihres S3-Buckets ein, in dem [!DNL Experience Platform] Ihre Exportdaten als CSV-Dateien ablegen.
* **[!UICONTROL Folder Path]**: Geben Sie den Pfad an Ihrem Speicherort an, an dem [!DNL Experience Platform] Ihre Exportdaten als CSV-Dateien ablegen.
* **[!UICONTROL Container]**: *Für Blob-Verbindungen*. Der Container, der den Blob enthält, in dem sich Ihr Ordnerpfad befindet.
* **[!UICONTROL File Format]**: Wählen Sie **CSV**, um CSV-Dateien an Ihren Speicherort zu exportieren.

### Aktivieren von Warnhinweisen {#enable-alerts}

Sie können Warnhinweise aktivieren, um Benachrichtigungen zum Status des Datenflusses zu Ihrem Ziel zu erhalten. Wählen Sie einen Warnhinweis aus der zu abonnierenden Liste aus, um Benachrichtigungen über den Status Ihres Datenflusses zu erhalten. Weitere Informationen zu Warnhinweisen finden Sie im Handbuch zum [Abonnieren von Zielwarnhinweisen über die Benutzeroberfläche](../../ui/alerts.md).

Wenn Sie mit dem Eingeben der Details für Ihre Zielverbindung fertig sind, wählen Sie **[!UICONTROL Next]** aus.

## Aktivieren von Zielgruppen für dieses Ziel {#activate}

>[!IMPORTANT]
>
>* Zum Aktivieren von Daten benötigen Sie die **[!UICONTROL View Destinations]**, **[!UICONTROL Activate Destinations]**, **[!UICONTROL View Profiles]** und **[!UICONTROL View Segments]** [Zugriffssteuerungsberechtigungen](/help/access-control/home.md#permissions). Lesen Sie die [Übersicht über die Zugriffssteuerung](/help/access-control/ui/overview.md) oder wenden Sie sich an Ihre Produktadmins, um die erforderlichen Berechtigungen zu erhalten.
>* Zum Exportieren *Identitäten* benötigen Sie die **[!UICONTROL View Identity Graph]** Zugriffssteuerungsberechtigung[&#x200B; &#x200B;](/help/access-control/home.md#permissions). <br> ![Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren.](/help/destinations/assets/overview/export-identities-to-destination.png "Wählen Sie einen im Workflow hervorgehobenen Identity-Namespace aus, um Zielgruppen für Ziele zu aktivieren."){width="100" zoomable="yes"}


Anweisungen [&#x200B; Aktivieren von Zielgruppen für dieses Ziel finden Sie &#x200B;](../../ui/activate-batch-profile-destinations.md)Aktivieren von Zielgruppendaten für Batch-Profil-).

### Zielattribute {#destination-attributes}

Beim Aktivieren von Zielgruppen für dieses Ziel empfiehlt Adobe die Auswahl einer eindeutigen Kennung aus Ihrem [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas). Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter „Best [&#x200B; beim Aktivieren von Zielgruppen für E-Mail-Marketing-Ziele](overview.md#best-practices).

## Exportierte Daten {#exported-data}

Für [!DNL Adobe Campaign]-Ziele erstellt [!DNL Experience Platform] eine `.csv`-Datei an dem von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie im Abschnitt [Überprüfen der Zielgruppenaktivierung](../../ui/activate-batch-profile-destinations.md#verify) im Tutorial zur Zielgruppenaktivierung.

## Einrichten des Datenimports in [!DNL Adobe Campaign] {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Beachten Sie bei der Durchführung dieser Integration die [!DNL SFTP] Speicherbeschränkungen, Datenbankspeicherbeschränkungen und Beschränkungen für aktive Profile gemäß Ihrem [!DNL Adobe Campaign].
>* Sie müssen Ihre exportierten Segmente in [!DNL Adobe Campaign] mithilfe [!DNL Campaign] Workflows planen, importieren und zuordnen. Siehe [Einrichten eines wiederkehrenden Imports](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html?lang=de) in [!DNL Adobe Campaign Classic] Dokumentation und [Über Datenverwaltungsaktivitäten](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) in [!DNL Adobe Campaign Standard] Dokumentation.
>* Die bevorzugte Methode zum Senden von Daten an [!DNL Adobe Campaign] ist über [!DNL Amazon S3] oder [!DNL Azure Blob].

Nachdem Sie [!DNL Experience Platform] mit Ihrem [!DNL Amazon S3]- oder [!DNL Azure Blob]-Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort in [!DNL Adobe Campaign] einrichten. Informationen hierzu finden Sie auf den folgenden [!DNL Adobe Campaign] Dokumentationsseiten:

* [Erste Schritte mit dem Datenimport und -export](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=de#getting-started) und [Laden (Datei)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html?lang=de) in der [!DNL Adobe Campaign Classic].
* [Erste Schritte mit Prozessen und Daten](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html)Management und [Datei laden](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) in der [!DNL Adobe Campaign Standard].
