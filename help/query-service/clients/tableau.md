---
keywords: Experience Platform; home; beliebte Themen; tableau; Tableau; Query Service; Query Service; Verbindung mit Query Service
solution: Experience Platform
title: Verbinden von Tableau mit Query Service
description: In diesem Dokument werden die Schritte zum Verbinden von Tableau mit Adobe Experience Platform Query Service beschrieben.
exl-id: f380aacd-5091-41bc-97ca-593e0b1670fd
source-git-commit: 26f0725f0f239707bd719ed46929648f8d557155
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 10%

---

# Verbinden von [!DNL Tableau] mit dem Abfrage-Service

Dieses Dokument enthält Informationen zum Verbinden von [!DNL Tableau] mit Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL Tableau] haben und mit der Navigation in der Benutzeroberfläche vertraut sind. Weitere Informationen zu [!DNL Tableau] finden Sie in der [offiziellen [!DNL Tableau] Dokumentation](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Anweisungen zum Herstellen einer Verbindung mit einem PostgreSQL-Server mit Tableau](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) finden Sie auf der offiziellen Tableau-Website. [ Sobald das Dialogfeld für die Verbindungseinstellungen angezeigt wird, geben Sie Ihre Platform-Anmeldedaten in die Parameterfelder ein, um eine Verbindung mit Adobe Experience Platform herzustellen. Nachfolgend finden Sie eine Liste der erforderlichen Verbindungsparameter.

| Verbindungsparameter | Beschreibung |
|---|---|
| **[!DNL Server]** | Die Adresse Ihres SFTP-Speicherorts. Verwenden Sie den Wert Ihrer Experience Platform **[!UICONTROL Host]**-Berechtigung. |
| **[!DNL Port]:** | Der Port für [!DNL Query Service]. Sie müssen den Port **80** oder **5432** verwenden, um eine Verbindung mit [!DNL Query Service] herzustellen. |
| **[!DNL Database]** | Die Datenbanken, auf die Sie zugreifen möchten. Verwenden Sie den Wert Ihrer Experience Platform **[!UICONTROL Database]**-Berechtigung: `prod:all`. |
| **[!DNL Authentication]:** | Die gewählte Methode zum Nachweis der Benutzeridentität. Es wird empfohlen, [!DNL Username and Password] aus den verfügbaren Optionen des Dropdown-Menüs auszuwählen. |
| **[!DNL Username]** | Dies ist Ihre Platform-Organisations-ID. Verwenden Sie den Wert Ihrer Experience Platform **[!UICONTROL Benutzername]**-Berechtigung. Die ID hat das Format `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Diese alphanumerische Zeichenfolge ist Ihre Experience Platform **[!UICONTROL Kennwort]**-Berechtigung. Wenn Sie nicht ablaufende Anmeldeinformationen verwenden möchten, ist dieser Wert die verketteten Argumente aus den `technicalAccountID` und den `credential`, die in der JSON-Konfigurationsdatei heruntergeladen wurden. Der Kennwortwert hat das folgende Format: {technicalAccountId}:{credential}. Die JSON-Konfigurationsdatei für nicht ablaufende Anmeldeinformationen ist ein einmaliger Download während der Initialisierung, von dem Adobe keine Kopie aufbewahrt. |

Weitere Informationen zum Auffinden Ihres Benutzernamen, Passworts und Ihrer Anmeldedaten finden Sie im [Benutzerhandbuch zu Anmeldeinformationen](../ui/credentials.md). Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei [!DNL Platform] an, wählen Sie dann **[!UICONTROL Abfragen]**, gefolgt von **[!UICONTROL Anmeldeinformationen]**.

>[!IMPORTANT]
>
>Als Tableau- oder Power BI-Benutzer können Sie über den Tab Anmeldedaten für Query Service eine Verbindung zu Ihren BI-Tools herstellen. Anweisungen zum Verbinden Ihrer BI-Tools mit Customer Journey Analytics](../ui/credentials.md#connect-to-customer-journey-analytics) finden Sie in der Dokumentation zu den Anmeldedaten .[

Stellen Sie sicher, dass Sie die Option **[!UICONTROL SSL erforderlich]** aktiviert haben, bevor Sie versuchen, eine Verbindung herzustellen. Weitere Informationen zur SSL-Unterstützung für Verbindungen von Drittanbietern mit Adobe Experience Platform Query Service finden Sie in der Dokumentation zu [SSL-Modi](./ssl-modes.md) .

>[!IMPORTANT]
>
>Verschachtelte Datenstrukturen in BI-Tools von Drittanbietern können vereinfacht werden, um ihre Benutzerfreundlichkeit zu verbessern und den erforderlichen Arbeitsaufwand beim Abrufen, Analysieren, Transformieren und Berichten von Daten zu reduzieren. Anweisungen zum Aktivieren dieser Einstellung beim Herstellen einer Verbindung zu einer Datenbank finden Sie in der Dokumentation zur Funktion [`FLATTEN`](../key-concepts/flatten-nested-data.md).

Bestätigen Sie nach dem Ausfüllen aller Anmeldedaten Ihre Einstellungen, um fortzufahren. Sie haben jetzt eine Verbindung mit Adobe Experience Platform hergestellt.

## Nächste Schritte

Nachdem Sie sich mit [!DNL Query Service] angemeldet haben, können Sie mit [!DNL Tableau] Abfragen schreiben. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Handbuch zu [ausgeführten Abfragen](../best-practices/writing-queries.md).
