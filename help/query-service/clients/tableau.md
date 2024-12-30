---
keywords: Experience Platform;Startseite;beliebte Themen;tableau;Tableau;Abfrage-Service;Abfrage-Service;Verbindung zum Abfrage-Service;
solution: Experience Platform
title: Verbinden von Tableau mit dem Abfrage-Service
description: In diesem Dokument werden die Schritte zum Verbinden von Tableau mit dem Abfrage-Service von Adobe Experience Platform erläutert.
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
> In diesem Handbuch wird davon ausgegangen, dass Sie bereits Zugriff auf [!DNL Tableau] haben und mit dem Navigieren in der zugehörigen Benutzeroberfläche vertraut sind. Weitere Informationen zu [!DNL Tableau] finden Sie in der [offiziellen [!DNL Tableau] Dokumentation](https://help.tableau.com/current/pro/desktop/en-us/default.htm).

Anleitungen zum Verbinden [ PostgreSQL-Servers mit Tableau ](https://help.tableau.com/current/pro/desktop/en-us/examples_postgresql.htm) Sie auf der offiziellen Tableau-Website. Sobald das Dialogfeld für die Verbindungseinstellungen angezeigt wird, geben Sie Ihre Platform-Anmeldeinformationen in die Parameterfelder ein, um eine Verbindung mit Adobe Experience Platform herzustellen. Eine Liste der erforderlichen Verbindungsparameter finden Sie unten.

| Verbindungsparameter | Beschreibung |
|---|---|
| **[!DNL Server]** | Die Adresse Ihres SFTP-Speicherorts. Verwenden Sie den Wert Ihrer Experience Platform-**[!UICONTROL -]**. |
| **[!DNL Port]:** | Der Port für [!DNL Query Service]. Sie müssen Port **80** oder **5432** verwenden, um eine Verbindung mit [!DNL Query Service] herzustellen. |
| **[!DNL Database]** | Die Datenbank(en), auf die Sie zugreifen möchten. Verwenden Sie den Wert Ihrer Experience Platform-/**[!UICONTROL -]**: `prod:all`. |
| **[!DNL Authentication]:** | Ihre gewählte Methode zum Nachweis der Benutzeridentität. Es wird empfohlen, [!DNL Username and Password] aus den verfügbaren Optionen im Dropdown-Menü auszuwählen. |
| **[!DNL Username]** | Dies ist Ihre Platform-Organisations-ID. Verwenden Sie den Wert Ihrer Experience Platform-Anmeldedaten **[!UICONTROL Benutzername]**. Die ID hat das Format `ORG_ID@AdobeOrg`. |
| **[!DNL Password]** | Diese alphanumerische Zeichenfolge ist Ihre Experience Platform **[!UICONTROL Kennwort]**-Berechtigung. Wenn Sie nicht ablaufende Anmeldeinformationen verwenden möchten, ist dieser Wert die verketteten Argumente aus der `technicalAccountID` und der in die JSON-Konfigurationsdatei heruntergeladenen `credential`. Das Kennwort hat folgende Form: {technicalAccountId}:{credential}. Die JSON-Konfigurationsdatei für nicht ablaufende Anmeldeinformationen ist ein einmaliger Download während ihrer Initialisierung, von dem Adobe keine Kopie speichert. |

Weiterführende Informationen dazu, wie Sie Ihren Benutzernamen, Ihr Kennwort und Ihre Anmeldedaten finden, finden Sie im [Handbuch zu Anmeldedaten](../ui/credentials.md). Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei [!DNL Platform] an und wählen Sie **[!UICONTROL Abfragen]** gefolgt von **[!UICONTROL Anmeldeinformationen]**.

>[!IMPORTANT]
>
>Als Tableau- oder Power BI-Anwender können Sie auf der Registerkarte Anmeldeinformationen des Abfrage-Service eine Verbindung zwischen Customer Journey Analytics und Ihren BI-Tools herstellen. Anleitungen zum Verbinden (Verbinden [ BI-Tools mit dem Customer Journey Analytics) finden Sie in der Dokumentation ](../ui/credentials.md#connect-to-customer-journey-analytics) Anmeldedaten .

Vergewissern Sie sich, dass Sie das **[!UICONTROL SSL erforderlich]** aktiviert haben, bevor Sie versuchen, eine Verbindung herzustellen. Weitere Informationen zur SSL[Unterstützung für Drittanbieterverbindungen ](./ssl-modes.md) Adobe Experience Platform Query Service finden Sie in der Dokumentation zu SSL-Modi .

>[!IMPORTANT]
>
>Verschachtelte Datenstrukturen in BI-Tools von Drittanbietern können vereinfacht werden, um ihre Benutzerfreundlichkeit zu verbessern und den erforderlichen Arbeitsaufwand beim Abrufen, Analysieren, Transformieren und Berichten von Daten zu reduzieren. Anweisungen zum Aktivieren dieser Einstellung beim Herstellen einer Verbindung zu einer Datenbank finden Sie in der Dokumentation zur Funktion [`FLATTEN`](../key-concepts/flatten-nested-data.md).

Nachdem Sie alle Ihre Anmeldedaten eingegeben haben, bestätigen Sie Ihre Einstellungen, um fortzufahren. Sie haben sich jetzt mit Adobe Experience Platform verbunden.

## Nächste Schritte

Nachdem Sie sich mit [!DNL Query Service] verbunden haben, können Sie [!DNL Tableau] verwenden, um Abfragen zu schreiben. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Handbuch unter [Ausführen von Abfragen](../best-practices/writing-queries.md).
