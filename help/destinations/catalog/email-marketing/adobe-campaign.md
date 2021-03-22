---
keywords: E-Mail;E-Mail;E-Mail-Ziele;Adobe-Kampagne;Kampagne
title: Adobe Campaign-Verbindung
description: Adobe Campaign umfasst verschiedene Lösungen, mit denen Sie Kampagnen über alle Ihre Online- und Offline-Kanäle hinweg personalisieren und bereitstellen können.
translation-type: tm+mt
source-git-commit: 7d579d85d427c45f39d000288ed883c7ffd003bf
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 26%

---


# Adobe Campaign-Verbindung

Adobe Campaign umfasst verschiedene Lösungen, mit denen Sie Kampagnen über alle Ihre Online- und Offline-Kanäle hinweg personalisieren und bereitstellen können. Weitere Informationen finden Sie unter [Erste Schritte mit Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html).

Um Segmentdaten an Adobe Campaign zu senden, müssen Sie zunächst [das Ziel](#connect-destination) in Adobe Experience Platform verbinden und [dann einen Datenimport](#import-data-into-campaign) von Ihrem Speicherort in der Datenspeicherung in Adobe Campaign einrichten.

## Exporttyp {#export-type}

**Profil-basiert** : Sie exportieren alle Segmentmitglieder zusammen mit den gewünschten Segmentfeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Schritt  **[!UICONTROL Attribute]** auswählen des Arbeitsablaufs für die  [Aktivierung](../../ui/activate-destinations.md#select-attributes) ausgewählt.

## Ziel verbinden {#connect-destination}

Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** Adobe Campaign und dann **[!UICONTROL Konfigurieren]**.

>[!NOTE]
>
>Wenn bereits eine Verbindung zu diesem Ziel besteht, wird auf der Zielkarte die Schaltfläche **[!UICONTROL Aktivieren]** angezeigt. Weitere Informationen zum Unterschied zwischen [!UICONTROL Aktivieren] und [!UICONTROL Konfigurieren] finden Sie im Abschnitt [Katalog](../../ui/destinations-workspace.md#catalog) der Dokumentation zum Zielarbeitsbereich.

![Verbindung mit Adobe Campaign](../../assets/catalog/email-marketing/adobe-campaign/catalog.png)

Wählen Sie im Schritt **[!UICONTROL Account]** des Arbeitsablaufs für das Verbinden von Zielen **[!UICONTROL Verbindungstyp]** für den Speicherort Ihrer Datenspeicherung aus. Adobe Campaign: Sie können zwischen **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP mit Kennwort]**, **[!UICONTROL SFTP mit SSH-Schlüssel]** und **[!UICONTROL Blaue Blase]** wählen. Die bevorzugte Methode zum Senden von Daten an Adobe Campaign ist [!DNL Amazon S3] oder [!DNL Azure Blob]. Füllen Sie je nach Verbindungstyp die folgenden Informationen aus und wählen Sie dann **[!UICONTROL Verbinden]**.


![Assistent zum Einrichten von Campaign](../../assets/catalog/email-marketing/adobe-campaign/connection-type.png)

- Bei Verbindungen des Typs **[!UICONTROL Amazon S3]** müssen Sie die Zugriffsschlüsselkennung und den geheimen Zugriffsschlüssel angeben.
- Bei Verbindungen des Typs **[!UICONTROL SFTP mit Passwort]** müssen Sie Domäne, Port, Benutzernamen und Kennwort angeben.
- Bei Verbindungen des Typs **[!UICONTROL SFTP mit SSH-Schlüssel]** müssen Sie Domäne, Port, Benutzernamen und SSH-Schlüssel angeben.
- Für Verbindungen mit **[!UICONTROL Azurblauch]** müssen Sie eine Verbindungszeichenfolge angeben.

Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um unter dem Abschnitt **[!UICONTROL Schlüssel]** eine Verschlüsselung mit PGP/GPG zu Ihren exportierten Dateien hinzuzufügen. Beachten Sie, dass dieser öffentliche Schlüssel **als Base64-kodierte Zeichenfolge geschrieben werden muss.**

![Campaign-Informationen ausfüllen](../../assets/catalog/email-marketing/adobe-campaign/account-info.png)

Geben Sie unter **[!UICONTROL Kontoauthentifizierung]** die relevanten Informationen für Ihr Ziel ein, wie nachfolgend gezeigt:
- **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
- **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
- **[!UICONTROL Bucket-Name]**: *Bei S3-Verbindungen*. Geben Sie den Speicherort Ihres S3-Behälters ein, in dem [!DNL Platform] Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegt.
- **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad an, an dem die Exportdaten als CSV- oder tabulatorgetrennte Datenspeicherung hinterlegt  [!DNL Platform] werden sollen.
- **[!UICONTROL Container]**:  *Für Blob-Verbindungen*. Der Container, in dem sich der Ordnerpfad Blob befindet.
- **[!UICONTROL Dateiformat]**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.
- **[!UICONTROL Marketingaktionen]**: Marketingaktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketingaktionen auswählen oder eine eigene Marketingaktion erstellen. Weitere Informationen zu Marketingaktionen finden Sie auf der Seite [Übersicht über Datenverwendungsrichtlinien](../../../data-governance/policies/overview.md). Siehe auch [Adobe-definierte Marketingaktionen](../../../data-governance/policies/overview.md#core-actions) im selben Dokument.

![Allgemeine Informationen zu Campaign](../../assets/catalog/email-marketing/adobe-campaign/basic-information.png)

Wählen Sie **[!UICONTROL Ziel]** erstellen, nachdem Sie die oben stehenden Felder ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können für das Ziel [Segmente aktivieren](../../ui/activate-destinations.md).

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](../../ui/activate-destinations.md).

## Zielattribute {#destination-attributes}

Beim [Aktivieren von Segmenten](../../ui/activate-destinations.md) für das Adobe Campaign-Ziel empfehlen wir, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter [Wählen Sie, welche Schema-Felder als Zielattribute in Ihren exportierten Dateien](./overview.md#destination-attributes) in der Dokumentation zu den E-Mail-Marketing-Zielen verwendet werden sollen.

## Exportierte Daten {#exported-data}

Für [!DNL Adobe Campaign]-Ziele erstellt [!DNL Platform] eine tabulatorgetrennte `.txt`- oder `.csv`-Datenspeicherung im angegebenen Speicherort. Weitere Informationen zu den Aktivierungen finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele](../../ui/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Segmentbildung.

## Datenimport in Adobe Campaign einrichten {#import-data-into-campaign}

>[!IMPORTANT]
>
>- Beachten Sie bei der Durchführung dieser Integration die Einschränkungen der SFTP-Datenspeicherung, die Datenspeicherung der Datenbank und die Einschränkungen des aktiven Profils gemäß Ihrem Adobe Campaign-Vertrag.
>- Sie müssen Ihre exportierten Segmente in Adobe Campaign mit [!DNL Campaign] Workflows planen, importieren und zuordnen. Weitere Informationen finden Sie unter [Einrichten eines wiederkehrenden Imports](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html) in der Adobe Campaign Classic-Dokumentation und [Informationen zu Data Management-Aktivitäten](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) in der Adobe Campaign Standard-Dokumentation.
>- Die bevorzugte Methode zum Senden von Daten an Adobe Campaign ist [!DNL Amazon S3] oder [!DNL Azure Blob].



Nachdem Sie [!DNL Platform] mit Ihrer [!DNL Amazon S3]- oder [!DNL Azure Blob]-Datenspeicherung verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort in Adobe Campaign einrichten. Informationen dazu finden Sie auf den folgenden Adobe Campaign-Dokumentationsseiten:
- [Beginnen Sie mit dem Datenimport und -](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html) export sowie dem Laden von  [Daten (Datei)](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) in der Adobe Campaign Classic-Dokumentation.
- [Beginnen Sie mit Prozessen und ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) Datenverwaltung und  [laden Sie die ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) Datei in der Adobe Campaign Standard-Dokumentation.