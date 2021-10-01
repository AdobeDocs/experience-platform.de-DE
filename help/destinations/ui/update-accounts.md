---
keywords: Zielkonto, Zielkonten aktualisieren, Konten aktualisieren, Ziel aktualisieren
title: Zielkonten aktualisieren
type: Tutorial
description: In diesem Tutorial werden die Schritte zum Aktualisieren von Zielkonten in der Adobe Experience Platform-Benutzeroberfläche aufgeführt
exl-id: afb41878-4205-4c64-af4d-e2740f852785
source-git-commit: 5b72433fcf2318f98538278c6d2650b366e391a2
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 35%

---

# Zielkonten aktualisieren

## Übersicht {#overview}

Der Tab **[!UICONTROL Konten]** zeigt Details zu den Verbindungen an, die Sie mit verschiedenen Zielen hergestellt haben. Die nachstehende Tabelle enthält alle Informationen zu den einzelnen Zielen:

![Registerkarte „Konten“](../assets/ui/update-accounts/destination-accounts.png)

| Element | Beschreibung |
|---|---|
| [!UICONTROL Plattform] | Das Ziel, für das Sie die Verbindung eingerichtet haben. |
| [!UICONTROL Verbindungstyp] | Stellt den Verbindungstyp zu Ihrem Speicher-Bucket oder Ziel dar. <ul><li>Bei E-Mail-Marketing-Zielen: Kann S3 oder FTP sein.</li><li>Bei Echtzeit-Werbezielen: Server-zu-Server.</li><li>Bei Amazon S3-Cloud-Speicherzielen: Zugriffsschlüssel. </li><li>Bei SFTP-Cloud-Speicherzielen: Grundlegende Authentifizierung für SFTP.</li></ul> |
| [!UICONTROL Benutzername] | Der Benutzername, den Sie im [Zielverbindungsassistenten](../catalog/email-marketing/overview.md#connect-destination) ausgewählt haben. |
| [!UICONTROL Ziele] | Gibt die Zahl der eindeutigen erfolgreich verbundenen Zielflüsse mit grundlegenden Informationen an, die für ein Ziel erstellt wurden. |
| [!UICONTROL Autorisiert] | Das Datum, an dem die Verbindung zu diesem Ziel genehmigt wurde. |

## Konten aktualisieren {#update}

Gehen Sie wie folgt vor, um Verbindungsdetails zu vorhandenen Zielen zu aktualisieren.

1. Melden Sie sich bei [Experience Platform UI](https://platform.adobe.com/) an und wählen Sie **[!UICONTROL Ziele]** aus der linken Navigationsleiste aus. Wählen Sie **[!UICONTROL Konten]** in der oberen Kopfzeile aus, um Ihre vorhandenen Konten anzuzeigen.

   ![Registerkarte „Konten“](../assets/ui/update-accounts/accounts-tab.png)

2. Wählen Sie oben links das Filtersymbol ![Filtersymbol](../assets/ui/update-accounts/filter.png) aus, um das Sortierungsfenster zu öffnen. Das Sortierungsfenster bietet eine Liste aller Ziele. Sie können mehr als ein Ziel aus der Liste auswählen, um eine gefilterte Auswahl von Konten anzuzeigen, die mit den ausgewählten Zielen verknüpft sind.

   ![Ziele filtern](../assets/ui/update-accounts/filter-accounts.png)

3. Wählen Sie die Schaltfläche ![Konto bearbeiten](../assets/ui/workspace/pencil-icon.png) **[!UICONTROL Bearbeiten]** in der Spalte **[!UICONTROL Plattform]** aus, um die Kontoinformationen zu bearbeiten.

   ![Registerkarte „Konten“](../assets/ui/update-accounts/accounts-edit.png)

4. Geben Sie Ihre aktualisierten Kontoanmeldeinformationen ein.

   * Wählen Sie für Konten, die einen Verbindungstyp `OAuth2` verwenden, **[!UICONTROL OAuth]** erneut anschließen , um Ihre Kontoanmeldeinformationen zu erneuern.

      ![Details bearbeiten OAuth](../assets/ui/update-accounts/edit-details-oauth.png)


   * Bei Konten, die einen Verbindungstyp vom Typ `Access Key` oder `ConnectionString` verwenden, können Sie Ihre Kontoauthentifizierungsinformationen bearbeiten, einschließlich Informationen wie Zugriffskennung, geheime Schlüssel oder Verbindungszeichenfolgen.

      ![Details bearbeiten Zugriffsschlüssel](../assets/ui/update-accounts/edit-details-key.png)

5. Wählen Sie **[!UICONTROL Save]** aus, um die Aktualisierung der Anmeldeinformationen abzuschließen.
