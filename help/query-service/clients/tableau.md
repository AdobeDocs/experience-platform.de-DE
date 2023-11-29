---
keywords: Experience Platform; home; beliebte Themen; tableau; Tableau; Query Service; Query Service; Verbindung mit Query Service
solution: Experience Platform
title: Verbinden von Tableau mit dem Abfrage-Service verbinden
description: In diesem Dokument werden die Schritte zum Verbinden von Tableau mit Adobe Experience Platform Query Service beschrieben.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 12%

---

# Verbinden von [!DNL Tableau] mit dem Abfrage-Service

Dieses Dokument enthält Informationen zum Verbinden von [!DNL Tableau] mit Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL Tableau] und sind mit dem Navigieren in der Benutzeroberfläche vertraut. Weitere Informationen über [!DNL Tableau] finden Sie im Abschnitt [offiziell [!DNL Tableau] Dokumentation](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Anleitung zum [Verbindung zu einem PostgreSQL-Server mit Tableau herstellen](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) sind auf der offiziellen Tableau-Website verfügbar. Sobald das Dialogfeld für die Verbindungseinstellungen angezeigt wird, geben Sie Ihre Platform-Anmeldedaten in die Parameterfelder ein, um eine Verbindung mit Adobe Experience Platform herzustellen. Nachfolgend finden Sie eine Liste der erforderlichen Verbindungsparameter.

| Verbindungsparameter | Beschreibung |
|---|---|
| **[!DNL Server]** | Die Adresse Ihres SFTP-Speicherorts. Den Wert Ihrer Experience Platform verwenden **[!UICONTROL Host]** Anmeldedaten. |
| **[!DNL Port]:** | Der Port für [!DNL Query Service]. Sie müssen Port verwenden **80** oder **5432** zur Verbindung mit [!DNL Query Service]. |
| **[!DNL Database]** | Die Datenbanken, auf die Sie zugreifen möchten. Den Wert Ihrer Experience Platform verwenden **[!UICONTROL Datenbank]** credential: `prod:all`. |
| **[!DNL Authentication]:** | Die gewählte Methode zum Nachweis der Benutzeridentität. Sie sollten [!DNL Username and Password] aus den verfügbaren Optionen des Dropdown-Menüs. |
| **[!DNL Username]** | Dies ist Ihre Platform-Organisations-ID. Den Wert Ihrer Experience Platform verwenden **[!UICONTROL Benutzername]** Anmeldedaten. Die ID hat das Format `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Diese alphanumerische Zeichenfolge ist Ihre Experience Platform **[!UICONTROL Passwort]** Anmeldedaten. Wenn Sie nicht ablaufende Anmeldeinformationen verwenden möchten, ist dieser Wert die verketteten Argumente aus dem `technicalAccountID` und `credential` in die JSON-Konfigurationsdatei heruntergeladen. Der Kennwortwert hat folgende Form: {technicalAccountId}:{credential}. Die JSON-Konfigurationsdatei für nicht ablaufende Anmeldeinformationen ist ein einmaliger Download während der Initialisierung, von dem Adobe keine Kopie aufbewahrt. |

Weitere Informationen zum Auffinden Ihres Benutzernamens, Passworts und Ihrer Anmeldedaten finden Sie in der [Handbuch zu Anmeldeinformationen](../ui/credentials.md). Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei [!DNL Platform], wählen Sie **[!UICONTROL Abfragen]**, gefolgt von **[!UICONTROL Anmeldeinformationen]**.

Vergewissern Sie sich, dass Sie die **[!UICONTROL SSL erforderlich]** vor dem Versuch, eine Verbindung herzustellen. Siehe [Dokumentation zu SSL-Modi](./ssl-modes.md) , um mehr über die SSL-Unterstützung für Drittanbieterverbindungen zu Adobe Experience Platform Query Service zu erfahren.

>[!IMPORTANT]
>
>Verschachtelte Datenstrukturen in BI-Tools von Drittanbietern können vereinfacht werden, um ihre Benutzerfreundlichkeit zu verbessern und den erforderlichen Arbeitsaufwand beim Abrufen, Analysieren, Transformieren und Berichten von Daten zu reduzieren. Anweisungen zum Aktivieren dieser Einstellung beim Herstellen einer Verbindung zu einer Datenbank finden Sie in der Dokumentation zur Funktion [`FLATTEN`](../key-concepts/flatten-nested-data.md).

Bestätigen Sie nach dem Ausfüllen aller Anmeldedaten Ihre Einstellungen, um fortzufahren. Sie haben jetzt eine Verbindung mit Adobe Experience Platform hergestellt.

## Nächste Schritte

Jetzt, da Sie mit [!DNL Query Service], können Sie [!DNL Tableau] , um Abfragen zu schreiben. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Handbuch unter [Ausführen von Abfragen](../best-practices/writing-queries.md).
