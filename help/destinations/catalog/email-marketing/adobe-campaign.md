---
keywords: E-Mail;E-Mail;E-Mail-Ziele;Adobe-Kampagne;Kampagne
title: Adobe Campaign-Verbindung
description: Adobe Campaign umfasst verschiedene Lösungen, mit denen Sie Kampagnen über alle Ihre Online- und Offline-Kanäle hinweg personalisieren und bereitstellen können.
translation-type: tm+mt
source-git-commit: e13a19640208697665b0a7e0106def33fd1e456d
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 41%

---


# Adobe Campaign-Verbindung

Adobe Campaign umfasst verschiedene Lösungen, mit denen Sie Kampagnen über alle Ihre Online- und Offline-Kanäle hinweg personalisieren und bereitstellen können. Weiterführende Informationen finden Sie unter [Info zu Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/starting-with-adobe-campaign/about-adobe-campaign-classic.html).

Um Segmentdaten an Adobe Campaign zu senden, müssen Sie zunächst [das Ziel](#connect-destination) in Adobe Experience Platform verbinden und [dann einen Datenimport](#import-data-into-campaign) von Ihrem Speicherort in der Datenspeicherung in Adobe Campaign einrichten.

## Exporttyp {#export-type}

**Profil-basiert** : Sie exportieren alle Segmentmitglieder zusammen mit den gewünschten Segmentfeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;des Arbeitsablaufs für die  [Ziel-Aktivierung](../../ui/activate-destinations.md#select-attributes) ausgewählt.

## Ziel verbinden {#connect-destination}

Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** Adobe Campaign und dann **[!UICONTROL Verbindungsziel]**.

![Mit Adobe Campaign verbinden](../../assets/catalog/email-marketing/adobe-campaign/catalog.png)

Wählen Sie im Zielverbindungs-Workflow den **[!UICONTROL Verbindungstyp]** für Ihren Speicherort aus. Adobe Campaign: Sie können zwischen **[!UICONTROL Amazon S3]**, **[!UICONTROL SFTP mit Kennwort]**, **[!UICONTROL SFTP mit SSH-Schlüssel]** und **[!UICONTROL Blaue Blase]** wählen. Füllen Sie je nach Verbindungstyp die folgenden Informationen aus und wählen Sie dann **[!UICONTROL Verbinden]**.

![Assistent zum Einrichten von Campaign](../../assets/catalog/email-marketing/adobe-campaign/connection-type.png)

- Bei Verbindungen des Typs **[!UICONTROL Amazon S3]** müssen Sie die Zugriffsschlüsselkennung und den geheimen Zugriffsschlüssel angeben.
- Bei Verbindungen des Typs **[!UICONTROL SFTP mit Passwort]** müssen Sie Domäne, Port, Benutzernamen und Kennwort angeben.
- Bei Verbindungen des Typs **[!UICONTROL SFTP mit SSH-Schlüssel]** müssen Sie Domäne, Port, Benutzernamen und SSH-Schlüssel angeben.
- Für Verbindungen mit **[!UICONTROL Azurblauch]** müssen Sie eine Verbindungszeichenfolge angeben.

Optional können Sie Ihren RSA-formatierten öffentlichen Schlüssel anhängen, um unter dem Abschnitt **[!UICONTROL Schlüssel]** eine Verschlüsselung mit PGP/GPG zu Ihren exportierten Dateien hinzuzufügen. Beachten Sie, dass dieser öffentliche Schlüssel **als Base64-kodierte Zeichenfolge geschrieben werden muss.**

![Campaign-Informationen ausfüllen](../../assets/catalog/email-marketing/adobe-campaign/account-info.png)

Geben Sie unter **[!UICONTROL Grundlegende Informationen]** die entsprechenden Informationen für Ihr Ziel ein, wie nachfolgend dargestellt:
- **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
- **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
- **[!UICONTROL Bucket-Name]**: *Bei S3-Verbindungen*. Geben Sie den Speicherort Ihres S3-Behälters ein, in dem die Plattform Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegt.
- **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad in Ihrer Datenspeicherung an, in dem die Plattform Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegt.
- **[!UICONTROL Container]**:  *Für Blob-Verbindungen*. Der Container, in dem sich der Ordnerpfad Blob befindet.
- **[!UICONTROL Dateiformat]**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.

![Allgemeine Informationen zu Campaign](../../assets/catalog/email-marketing/adobe-campaign/basic-information.png)

Klicken Sie, nachdem Sie die Felder oben ausgefüllt haben, auf **[!UICONTROL Erstellen]**. Ihr Ziel ist nun verbunden und Sie können für das Ziel [Segmente aktivieren](../../ui/activate-destinations.md).

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](../../ui/activate-destinations.md).

## Zielattribute {#destination-attributes}

Beim [Aktivieren von Segmenten](../../ui/activate-destinations.md) für das Adobe Campaign-Ziel empfehlen wir, eine eindeutige Kennung aus Ihrem [Vereinigungsschema](../../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weitere Informationen finden Sie unter [Wählen Sie, welche Schema-Felder als Zielattribute in Ihren exportierten Dateien](./overview.md#destination-attributes) in der Dokumentation zu den E-Mail-Marketing-Zielen verwendet werden sollen.

## Exportierte Daten {#exported-data}

Für [!DNL Adobe Campaign]-Ziele erstellt Platform eine tabulatorgetrennte `.txt`- oder `.csv`-Datenspeicherung im angegebenen Speicherort. Weitere Informationen zu den Aktivierungen finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele](../../ui/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Segmentbildung.

## Datenimport in Adobe Campaign einrichten {#import-data-into-campaign}

>[!IMPORTANT]
>
>- Beachten Sie bei der Durchführung dieser Integration die Einschränkungen der SFTP-Datenspeicherung, die Datenspeicherung der Datenbank und die Einschränkungen des aktiven Profils gemäß Ihrem Adobe Campaign-Vertrag.
>- Sie müssen Ihre exportierten Segmente in Adobe Campaign mit [!DNL Campaign] Workflows planen, importieren und zuordnen. Weitere Informationen finden Sie in der Dokumentation zum Adobe Campaign unter [Einrichten eines wiederkehrenden Imports](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html#automating-with-workflows).



Nachdem Sie die Plattform mit Ihrer [!DNL Amazon S3]- oder SFTP-Datenspeicherung verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort der Datenspeicherung in Adobe Campaign einrichten. Weitere Informationen dazu finden Sie unter [Daten importieren](https://experienceleague.adobe.com/docs/campaign-classic/using/automating-with-workflows/general-operation/importing-data.html) in der Dokumentation zum Adobe Campaign.