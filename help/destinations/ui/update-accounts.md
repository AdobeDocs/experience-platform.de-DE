---
keywords: Zielkonto aktualisieren,Zielkonten
title: Zielkonten aktualisieren
type: Tutorial
description: In diesem Lernprogramm werden die Schritte zum Aktualisieren von Zielkonten in der Adobe Experience Platform-Benutzeroberfläche Liste
exl-id: afb41878-4205-4c64-af4d-e2740f852785
translation-type: tm+mt
source-git-commit: 07869d63f395bbab6c49a3976051facdf94d43b7
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 36%

---

# Zielkonten aktualisieren

## Übersicht {#overview}

Das Register **[!UICONTROL Konten]** zeigt Details zu den Verbindungen an, die Sie mit verschiedenen Zielen hergestellt haben. Die nachstehende Tabelle enthält alle Informationen zu den einzelnen Zielen:

![Registerkarte „Konten“](../assets/ui/update-accounts/destination-accounts.png)

| Element | Beschreibung |
|---|---|
| [!UICONTROL Plattform] | Das Ziel, für das Sie die Verbindung eingerichtet haben. |
| [!UICONTROL Verbindungstyp] | Stellt den Verbindungstyp zu Ihrem Speicher-Bucket oder Ziel dar. <ul><li>Bei E-Mail-Marketing-Zielen: Kann S3 oder FTP sein.</li><li>Bei Echtzeit-Werbezielen: Server-zu-Server.</li><li>Bei Amazon S3-Cloud-Speicherzielen: Zugriffsschlüssel. </li><li>Bei SFTP-Cloud-Speicherzielen: Grundlegende Authentifizierung für SFTP.</li></ul> |
| [!UICONTROL Benutzername] | Der Benutzername, den Sie im [Zielverbindungsassistenten](../catalog/email-marketing/overview.md#connect-destination) ausgewählt haben. |
| [!UICONTROL Ziele] | Gibt die Zahl der eindeutigen erfolgreich verbundenen Zielflüsse mit grundlegenden Informationen an, die für ein Ziel erstellt wurden. |
| [!UICONTROL Autorisiert] | Das Datum, an dem die Verbindung zu diesem Ziel genehmigt wurde. |

## Aktualisieren von Konten {#update}

Gehen Sie wie folgt vor, um Verbindungsdetails zu bestehenden Zielen zu aktualisieren.

1. Melden Sie sich bei [Experience Platform UI](https://platform.adobe.com/) an und wählen Sie **[!UICONTROL Ziele]** in der linken Navigationsleiste aus. Wählen Sie **[!UICONTROL Konten]** aus der oberen Kopfzeile aus, um Ihre bestehenden Konten Ansicht.

   ![Registerkarte „Konten“](../assets/ui/update-accounts/accounts-tab.png)

2. Wählen Sie oben links das Filtersymbol ![Filtersymbol](../assets/ui/update-accounts/filter.png) aus, um das Sortierfeld zu starten. Der Bereich &quot;Sortieren&quot;enthält eine Liste aller Ziele. Sie können mehrere Ziele in der Liste auswählen, um eine gefilterte Auswahl von Konten anzuzeigen, die mit den ausgewählten Zielen verknüpft sind.

   ![Ziele filtern](../assets/ui/update-accounts/filter-accounts.png)

3. Wählen Sie die Schaltfläche ![Konto bearbeiten](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Bearbeiten]** in der Spalte **[!UICONTROL Plattform]**, um die Kontoinformationen zu bearbeiten.

   ![Registerkarte „Konten“](../assets/ui/update-accounts/accounts-edit.png)

4. Geben Sie Ihre aktualisierten Kontoanmeldeinformationen ein.

   * Für Konten, die einen Verbindungstyp `OAuth2` verwenden, wählen Sie **[!UICONTROL OAuth]** erneut verbinden, um Ihre Kontoanmeldeinformationen zu verlängern.

      ![Details bearbeiten OAuth](../assets/ui/update-accounts/edit-details-oauth.png)


   * Bei Konten mit einem Verbindungstyp `Access Key` oder `ConnectionString` können Sie Ihre Kontoauthentifizierungsinformationen bearbeiten, einschließlich Informationen wie Zugriffskennung, geheime Schlüssel oder Verbindungszeichenfolgen.

      ![Detailzugriffsschlüssel bearbeiten](../assets/ui/update-accounts/edit-details-key.png)

5. Wählen Sie **[!UICONTROL Speichern]**, um die Aktualisierung der Anmeldeinformationen abzuschließen.
