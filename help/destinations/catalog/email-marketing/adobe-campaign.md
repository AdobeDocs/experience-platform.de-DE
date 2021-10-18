---
keywords: E-Mail; E-Mail; E-Mail; E-Mail-Ziele; Adobe Campaign; Kampagne
title: Adobe Campaign-Verbindung
description: Adobe Campaign umfasst verschiedene Lösungen, mit denen Sie Kampagnen über alle Ihre Online- und Offline-Kanäle hinweg personalisieren und bereitstellen können.
exl-id: 0de91738-8f56-41f5-8745-9b14b15db76a
source-git-commit: 3aac1e7c7fe838201368379da8504efc8e316e1c
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 18%

---

# Adobe Campaign-Verbindung

## Übersicht {#overview}

Adobe Campaign umfasst verschiedene Lösungen, mit denen Sie Kampagnen über alle Ihre Online- und Offline-Kanäle hinweg personalisieren und bereitstellen können. Weitere Informationen finden Sie unter [Erste Schritte mit Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html?lang=de) .

Um Segmentdaten an Adobe Campaign zu senden, müssen Sie zunächst [das Ziel](#connect-destination) in Adobe Experience Platform verbinden und dann [einen Datenimport](#import-data-into-campaign) von Ihrem Speicherort zu Adobe Campaign einrichten.

## Exporttyp {#export-type}

**Profilbasiert**  - Sie exportieren alle Mitglieder eines Segments zusammen mit den gewünschten Schemafeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Schritt  **[!UICONTROL Auswählen von]** Attributen im Workflow für die  [Zielgruppenaktivierung](../../ui/activate-batch-profile-destinations.md#select-attributes) ausgewählt.

## IP-Adressen-Zulassungsliste {#allow-list}

Beim Einrichten von E-Mail-Marketing-Zielen mit SFTP-Speicher empfiehlt Adobe, bestimmte IP-Bereiche zu Ihrer Zulassungsliste hinzuzufügen.

Informationen zum Hinzufügen von Adobe-IPs zu Ihrer Zulassungsliste finden Sie unter [IP-Adressen-Zulassungsliste für Cloud-Speicher-Ziele](../cloud-storage/ip-address-allow-list.md) .

## Mit Ziel verbinden {#connect}

Um eine Verbindung zu diesem Ziel herzustellen, führen Sie die Schritte aus, die im Tutorial [Zielkonfiguration](../../ui/connect-destination.md) beschrieben sind.

Adobe Campaign unterstützt die folgenden Verbindungstypen:

* **[!UICONTROL Amazon S3]**
* **[!UICONTROL SFTP mit Kennwort]**
* **[!UICONTROL SFTP mit SSH-Schlüssel]**
* **[!UICONTROL Azure Blob]**

Die bevorzugte Methode zum Senden von Daten an Adobe Campaign ist [!DNL Amazon S3] oder [!DNL Azure Blob].

### Verbindungsparameter {#parameters}

Während [Einrichten](../../ui/connect-destination.md) dieses Ziels müssen Sie die folgenden Informationen angeben:

* Bei Verbindungen des Typs **[!UICONTROL Amazon S3]** müssen Sie die [!UICONTROL Zugriffsschlüssel-ID] und den geheimen Zugriffsschlüssel ] angeben.[!UICONTROL 
* Bei Verbindungen des Typs **[!UICONTROL SFTP mit Kennwort]** müssen Sie [!UICONTROL Domäne], [!UICONTROL Port], [!UICONTROL Benutzername] und [!UICONTROL Kennwort] angeben.
* Bei Verbindungen des Typs **[!UICONTROL SFTP mit SSH-Schlüssel]** müssen Sie [!UICONTROL Domäne], [!UICONTROL Port], [!UICONTROL Benutzername] und [!UICONTROL SSH-Schlüssel] angeben.
* Bei Verbindungen des Typs **[!UICONTROL Azure Blob]** müssen Sie eine Verbindungszeichenfolge angeben.
* Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um eine Verschlüsselung mit PGP/GPG zu Ihren exportierten Dateien im Abschnitt **[!UICONTROL Schlüssel]** hinzuzufügen. Ihr öffentlicher Schlüssel muss als [!DNL Base64] kodierte Zeichenfolge geschrieben werden.
* **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
* **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
* **[!UICONTROL Bucket-Name]**: *Bei S3-Verbindungen*. Geben Sie den Speicherort Ihres S3-Buckets ein, in dem [!DNL Platform] Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien ablegt.
* **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad an Ihrem Speicherort an, an dem Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegt  [!DNL Platform] werden.
* **[!UICONTROL Container]**:  *Für Blob-Verbindungen*. Der Container, der den Blob enthält, in dem sich Ihr Ordnerpfad befindet.
* **[!UICONTROL Dateiformat]**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.

## Aktivieren von Segmenten für dieses Ziel {#activate}

Anweisungen zum Aktivieren von Zielgruppensegmenten für dieses Ziel finden Sie unter [Aktivieren von Zielgruppendaten für Batch-Profilexportziele](../../ui/activate-batch-profile-destinations.md) .

### Zielattribute {#destination-attributes}

Beim Aktivieren von Segmenten für dieses Ziel empfiehlt Adobe, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter [Best Practices beim Aktivieren von Zielgruppen für E-Mail-Marketing-Ziele](overview.md#best-practices).

## Exportierte Daten {#exported-data}

Für [!DNL Adobe Campaign]-Ziele erstellt [!DNL Platform] eine tabulatorgetrennte `.csv`-Datei am von Ihnen angegebenen Speicherort. Weitere Informationen zu den Dateien finden Sie unter [Segmentaktivierung überprüfen](../../ui/activate-batch-profile-destinations.md#verify) im Tutorial zur Segmentaktivierung.

## Datenimport in Adobe Campaign einrichten {#import-data-into-campaign}

>[!IMPORTANT]
>
>* Beachten Sie bei der Durchführung dieser Integration die Speicherbeschränkungen für [!DNL SFTP], die Speicherbeschränkungen für Datenbanken und die Beschränkungen für aktive Profile gemäß Ihrem Adobe Campaign-Vertrag.
>* Sie müssen Ihre exportierten Segmente in Adobe Campaign mithilfe von [!DNL Campaign]-Workflows planen, importieren und zuordnen. Weitere Informationen finden Sie unter [Einrichten eines wiederkehrenden Imports](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/use-cases/data-management/recurring-import-workflow.html?lang=de) in der Adobe Campaign Classic-Dokumentation und unter [Über Datenverwaltungsaktivitäten](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/about-data-management-activities.html) in der Adobe Campaign Standard-Dokumentation.
>* Die bevorzugte Methode zum Senden von Daten an Adobe Campaign ist [!DNL Amazon S3] oder [!DNL Azure Blob].


Nachdem Sie [!DNL Platform] mit Ihrem [!DNL Amazon S3]- oder [!DNL Azure Blob]-Speicher verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort zu Adobe Campaign einrichten. Weiterführende Informationen dazu finden Sie auf den folgenden Adobe Campaign-Dokumentationsseiten:
* [Erste Schritte mit dem Datenimport und -export ](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/importing-and-exporting-data/get-started-data-import-export.html?lang=de#getting-started) sowie dem Laden ( [Datei) ](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/action-activities/data-loading--file-.html) in der Adobe Campaign Classic-Dokumentation.
* [Beginnen Sie mit Prozessen und Daten-](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/get-started-workflows.html) Management und  [laden Sie die Datei ](https://experienceleague.adobe.com/docs/campaign-standard/using/managing-processes-and-data/data-management-activities/load-file.html) in der Adobe Campaign Standard-Dokumentation.
