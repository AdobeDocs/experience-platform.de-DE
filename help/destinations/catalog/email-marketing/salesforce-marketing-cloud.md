---
keywords: E-Mail;E-Mail;E-Mail-Ziele;E-Mail-Ziele;Verkaufsforce;Verkaufsziel
title: Salesforce-Marketing Cloud-Verbindung
seo-description: Salesforce Marketing Cloud ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.
translation-type: tm+mt
source-git-commit: 709908196bb5df665c7e7df10dc58ee9f3b0edbf
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 48%

---


# [!DNL Salesforce Marketing Cloud] connection

## Übersicht {#overview}

[[!DNL Salesforce Marketing Cloud]](https://www.salesforce.com/de/products/marketing-cloud/email-marketing/) ist eine Digital-Marketing-Suite, die früher als ExactTarget bekannt war und mit der Sie Journeys für Besucher und Kunden erstellen und anpassen können, um deren Erlebnis zu personalisieren.

Um Segmentdaten an [!DNL Salesforce Marketing Cloud] zu senden, müssen Sie zunächst [das Ziel](#connect-destination) in Plattform verbinden und dann [einen Datenimport](#import-data-into-salesforce) von Ihrer Datenspeicherung nach [!DNL Salesforce Marketing Cloud] einrichten.

## Exporttyp {#export-type}

**Profil-basiert** : Sie exportieren alle Segmentmitglieder zusammen mit den gewünschten Segmentfeldern (z. B.: E-Mail-Adresse, Telefonnummer, Nachname), wie im Bildschirm &quot;Attribute auswählen&quot;des Arbeitsablaufs für die  [Ziel-Aktivierung](../../ui/activate-destinations.md#select-attributes) ausgewählt.

## Ziel verbinden {#connect-destination}

Wählen Sie unter **[!UICONTROL Verbindungen]** > **[!UICONTROL Ziele]** [!DNL Salesforce Marketing Cloud] und dann **[!UICONTROL Verbindungsziel]**.

![Mit Salesforce verbinden](../../assets/catalog/email-marketing/salesforce/catalog.png)

Wenn Sie im Schritt **[!UICONTROL Authentifizieren]** zuvor eine Verbindung zu Ihrem Cloud-Speicher-Ziel eingerichtet haben, wählen Sie **[!UICONTROL Vorhandenes Konto]** und eine Ihrer bestehenden Verbindungen aus. Sie können auch **[!UICONTROL Neues Konto]** auswählen, um eine neue Verbindung einzurichten. Geben Sie die Anmeldedaten für die Kontoauthentifizierung ein und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus. Für [!DNL Salesforce Marketing Cloud] können Sie zwischen **[!UICONTROL SFTP mit Kennwort]** und **[!UICONTROL SFTP mit SSH-Schlüssel]** wählen. Füllen Sie je nach Verbindungstyp die folgenden Informationen aus und wählen Sie **[!UICONTROL Mit Ziel verbinden]** aus.

Bei Verbindungen des Typs **[!UICONTROL SFTP mit Passwort]** müssen Sie Domäne, Port, Benutzernamen und Kennwort angeben.

Bei Verbindungen des Typs **[!UICONTROL SFTP mit SSH-Schlüssel]** müssen Sie Domäne, Port, Benutzernamen und SSH-Schlüssel angeben.

![Salesforce-Informationen ausfüllen](../../assets/catalog/email-marketing/salesforce/account-info.png)

Geben Sie im **[!UICONTROL Setup-Schritt]** die entsprechenden Informationen für Ihr Ziel ein (wie folgt):
- **[!UICONTROL Name]**: Wählen Sie einen passenden Namen für Ihr Ziel.
- **[!UICONTROL Beschreibung]**: Geben Sie eine Beschreibung für Ihr Ziel ein.
- **[!UICONTROL Behältername]**: Ihr Amazon S3 Bucket, in dem die Plattform den Datenexport einlagert. Ihre Eingabe muss zwischen 3 und 63 Zeichen lang sein. Muss mit einem Buchstaben oder einer Nummer beginnen und enden. Muss nur Kleinbuchstaben, Zahlen oder Bindestriche (-) enthalten. Darf nicht als IP-Adresse formatiert werden (z. B. 192.100.1.1).
- **[!UICONTROL Ordnerpfad]**: Geben Sie den Pfad in Ihrer Datenspeicherung an, in dem die Plattform Ihre Exportdaten als CSV- oder tabulatorgetrennte Dateien hinterlegt.
- **[!UICONTROL Dateiformat]**: **CSV** oder **TAB_DELIMITED**. Wählen Sie das Dateiformat aus, mit dem Sie an Ihren Speicherort exportieren möchten.
- **[!UICONTROL Marketingaktionen]**: Marketingaktionen geben die Absicht an, für die Daten an das Ziel exportiert werden. Sie können aus von der Adobe definierten Marketingaktionen auswählen oder eine eigene Marketingaktion erstellen. Weitere Informationen zu Marketingaktionen finden Sie auf der Seite [Datenverwaltung in Adobe Experience Platform](../../../data-governance/policies/overview.md). Informationen zu den einzelnen, von der Adobe definierten Marketingaktionen finden Sie unter [Übersicht über Datenverwendungsrichtlinien](../../../data-governance/policies/overview.md).

![Salesforce-Basisinformationen](../../assets/catalog/email-marketing/salesforce/basic-information.png)

Klicken Sie auf **[!UICONTROL Ziel erstellen]**, nachdem Sie die oben stehenden Felder ausgefüllt haben. Ihr Ziel ist nun verbunden und Sie können für das Ziel [Segmente aktivieren](../../ui/activate-destinations.md).

## Aktivieren von Segmenten {#activate-segments}

Informationen zum Workflow für die Segmentaktivierung finden Sie unter [Profile und Segmente für ein Ziel aktivieren](../../ui/activate-destinations.md).

## Zielattribute {#destination-attributes}

Wenn Sie [segmente](../../ui/activate-destinations.md) in das [!DNL Salesforce Marketing Cloud]-Ziel aktivieren, empfehlen wir Ihnen, einen eindeutigen Bezeichner aus Ihrem [Vereinigung-Schema](../../../profile/home.md#profile-fragments-and-union-schemas) auszuwählen. Wählen Sie die eindeutige Kennung und alle anderen XDM-Felder aus, die Sie an das Ziel exportieren möchten. Weiterführende Informationen finden Sie unter [Auswählen, welche Schemafelder in Ihren exportierten Dateien als Zielattribute verwendet werden sollen](./overview.md#destination-attributes) (in E-Mail-Marketing-Zielen).

## Exportierte Daten {#exported-data}

Für [!DNL Salesforce Marketing Cloud]-Ziele erstellt Platform eine tabulatorgetrennte `.txt`- oder `.csv`-Datenspeicherung im angegebenen Speicherort. Weitere Informationen zu den Aktivierungen finden Sie unter [E-Mail-Marketing-Ziele und Cloud-Datenspeicherung-Ziele](../../ui/activate-destinations.md#esp-and-cloud-storage) im Tutorial zur Segmentbildung.

## Einrichten des Datenimports in [!DNL Salesforce Marketing Cloud] {#import-data-into-salesforce}

Nachdem Sie die Plattform mit Ihrer [!DNL Amazon S3]- oder SFTP-Datenspeicherung verbunden haben, müssen Sie den Datenimport von Ihrem Speicherort in [!DNL Salesforce Marketing Cloud] einrichten. Informationen dazu finden Sie unter [Importieren von Abonnenten aus einer Datei](https://help.salesforce.com/articleView?id=mc_es_import_subscribers_from_file.htm&amp;type=5) in [!DNL Salesforce Help Center].