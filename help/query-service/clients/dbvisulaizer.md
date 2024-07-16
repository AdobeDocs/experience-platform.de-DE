---
keywords: Experience Platform;home;popular topics;query service;Query service;Db Visualizer;DbVisualizer;db visulaizer;connect to query service;
solution: Experience Platform
title: Verbinden von DbVisualizer mit Query Service
description: In diesem Dokument werden die Schritte zum Verbinden von DbVisualizer mit Adobe Experience Platform Query Service beschrieben.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 5%

---

# [!DNL DbVisualizer] mit [!DNL Query Service] verbinden {#connect-dbvisualizer}

In diesem Dokument werden die Schritte zum Verbinden des [!DNL DbVisualizer]-Datenbank-Tools mit Adobe Experience Platform [!DNL Query Service] beschrieben.

## Erste Schritte

Für dieses Handbuch müssen Sie bereits Zugriff auf die [!DNL DbVisualizer] Desktop-App haben und mit dem Navigieren in der zugehörigen Benutzeroberfläche vertraut sein. Weitere Informationen zum Herunterladen des [!DNL DbVisualizer] -Desktop-Programms finden Sie in der [offiziellen [!DNL DbVisualizer] Dokumentation](https://www.dbvis.com/download/).

Um die erforderlichen Anmeldeinformationen zum Verbinden von [!DNL  DbVisualizer] mit Experience Platform zu erhalten, benötigen Sie Zugriff auf den Arbeitsbereich „Abfragen“ in der Platform-Benutzeroberfläche. Wenden Sie sich an Ihren Organisationsadministrator, wenn Sie derzeit keinen Zugriff auf den Arbeitsbereich &quot;Abfragen&quot;haben.

## Datenbankverbindung erstellen {#connect-database}

Nachdem Sie das Desktop-Programm auf Ihrem lokalen Computer installiert haben, befolgen Sie die offiziellen BDVisualizer-Anweisungen, um [eine neue Datenbankverbindung zu erstellen](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

Nachdem Sie **[!DNL PostgreSQL]** aus der Liste [!DNL Connections] ausgewählt haben, wird die Registerkarte [!DNL Object View] für die neue Verbindung [!DNL PostgreSQL] angezeigt.

### Festlegen der Treibereigenschaften für Ihre Verbindung {#properties}

Wählen Sie auf der Registerkarte [!DNL PostgreSQL] Objektansicht die Registerkarte **[!DNL Properties]** und dann die Registerkarte **[!DNL Driver Properties]** in der Navigationsseitenleiste aus. Weitere Informationen zu [Treibereigenschaften](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) finden Sie in der offiziellen Dokumentation.

Geben Sie anschließend die in der folgenden Tabelle beschriebenen Treibereigenschaften ein.

>[!IMPORTANT]
>
>Um DBVisualizer mit Adobe Experience Platform zu verbinden, müssen Sie die Verwendung von SSL aktivieren. Informationen zur SSL-Unterstützung für Verbindungen von Drittanbietern mit dem Adobe Experience Platform Query Service und zur Verbindung mit dem SSL-Modus finden Sie in der Dokumentation zu [SSL-Modi](./ssl-modes.md) .`verify-full`

| Eigenschaft | Beschreibung |
| ------ | ------ |
| `PGHOST` | Der Hostname für den [!DNL PostgreSQL] -Server. Dieser Wert ist Ihre Experience Platform **[!UICONTROL Host]-Berechtigung**. |
| `ssl` | Definieren Sie den SSL-Wert `1` , um die Verwendung von SSL zu aktivieren. |
| `sslmode` | Dies steuert den SSL-Schutz. Es wird empfohlen, den SSL-Modus `require` zu verwenden, wenn Sie Clients von Drittanbietern mit Adobe Experience Platform verbinden. Der Modus `require` stellt sicher, dass für alle Kommunikation eine Verschlüsselung erforderlich ist und dass das Netzwerk vertrauenswürdig ist, eine Verbindung zum richtigen Server herzustellen. Die Überprüfung des SSL-Zertifikats des Servers ist nicht erforderlich. |
| `user` | Der mit der Datenbank verbundene Benutzername ist Ihre Organisations-ID. Es handelt sich um eine alphanumerische Zeichenfolge, die auf `@Adobe.Org` endet. Dieser Wert ist Ihre Experience Platform **[!UICONTROL Benutzername] Anmeldedaten**. |

Verwenden Sie die Suchleiste, um jede Eigenschaft zu suchen, und wählen Sie dann die entsprechende Zelle für den Parameterwert aus. Die Zelle wird blau hervorgehoben. Geben Sie Ihre Platform-Berechtigung in das Wertefeld ein und wählen Sie **[!DNL Apply]** aus, um die Treibereigenschaft hinzuzufügen.

>[!NOTE]
>
>Um ein zweites `user` -Profil hinzuzufügen, wählen Sie `user` aus der Parameterspalte und wählen Sie dann das blaue Pluszeichen (+) aus, um Anmeldeinformationen für jeden Benutzer hinzuzufügen. Wählen Sie **[!DNL Apply]** aus, um die Treibereigenschaft hinzuzufügen.

In der Spalte [!DNL Edited] wird ein Häkchen angezeigt, das angibt, dass der Parameterwert aktualisiert wurde.

### Input Query Service-Anmeldeinformationen {#query-service-credentials}

Um die Anmeldeinformationen zu finden, die zum Verbinden von BBVisualizer mit Query Service erforderlich sind, melden Sie sich bei der Platform-Benutzeroberfläche an und wählen Sie im linken Navigationsbereich **[!UICONTROL Abfragen]** gefolgt von **[!UICONTROL Anmeldeinformationen]** aus. Weitere Informationen zum Auffinden Ihrer Anmeldedaten für **host**, **port**, **database**, **username** und **password** finden Sie im [Benutzerhandbuch](../ui/credentials.md).

![Die Seite &quot;Anmeldeinformationen&quot;im Arbeitsbereich &quot;Experience Platform-Abfragen&quot;mit Anmeldeinformationen und Kennungen zum Ablauf der Anmeldedaten sind hervorgehoben.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] bietet auch nicht ablaufende Anmeldeinformationen, um eine einmalige Einrichtung mit Clients von Drittanbietern zu ermöglichen. Eine vollständige Anleitung zum Generieren und Verwenden von nicht ablaufenden Anmeldedaten finden Sie in der Dokumentation für [. ](../ui/credentials.md#non-expiring-credentials) Dieser Prozess muss abgeschlossen werden, wenn Sie BDVisualizer als einmaliges Setup verbinden möchten. Die erworbenen Werte `credential` und `technicalAccountId` bilden den Wert für den Parameter DBVisualizer `password` .

## Authentifizierung {#authentication}

Um bei jeder Verbindungsherstellung eine Benutzer-ID und eine kennwortbasierte Authentifizierung erforderlich zu machen, navigieren Sie zur Registerkarte &quot;[!DNL Properties]&quot;und wählen Sie &quot;**[!DNL Authentication]**&quot;aus der Navigationsseitenleiste unter &quot;[!DNL PostgreSQL]&quot;.

Aktivieren Sie im Bedienfeld &quot;Verbindungsauthentifizierung&quot;die Kontrollkästchen **[!DNL Require Userid]** und **[!DNL Require Password]** und wählen Sie dann **[!DNL Apply]** aus. Weitere Informationen zu [Authentifizierungsoptionen festlegen](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) finden Sie in der offiziellen Dokumentation.

## Verbindung zu Platform herstellen

Sie können eine Verbindung mit ablaufenden oder nicht ablaufenden Anmeldeinformationen herstellen. Um eine Verbindung herzustellen, wählen Sie auf der Registerkarte [!DNL PostgreSQL] &quot;Objektansicht&quot;die Registerkarte **[!DNL Connection]** aus und geben Sie Ihre Experience Platform-Anmeldedaten für die folgenden Einstellungen ein. Ergänzende Anweisungen zu [Einrichten einer manuellen Verbindung](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) finden Sie auf der offiziellen Website von DBVisualizer.

>[!NOTE]
>
>Alle von BDVisualizer in der folgenden Tabelle erforderlichen Anmeldeinformationen sind für ablaufende und nicht ablaufende Anmeldeinformationen identisch, sofern sie nicht in der Parameterbeschreibung angegeben sind.

| Verbindungsparameter | Beschreibung |
|---|---|
| **[!UICONTROL Name]** | Erstellen Sie einen Namen für Ihre Verbindung. Es wird empfohlen, einen benutzerfreundlichen Namen anzugeben, um die Verbindung zu erkennen. |
| **[!UICONTROL Datenbankserver]** | Dies ist Ihre Experience Platform **[!UICONTROL Host]**-Berechtigung. |
| **[!UICONTROL Datenbankanschluss]** | Der Port für [!DNL Query Service]. Sie müssen den Port **80** oder **5432** verwenden, um eine Verbindung mit [!DNL Query Service] herzustellen. |
| **[!UICONTROL Datenbank]** | Verwenden Sie Ihren Experience Platform **[!UICONTROL Database]**-Berechtigungswert: `prod:all`. |
| **[!UICONTROL Database Userid]** | Dies ist Ihre Platform-Organisations-ID. Verwenden Sie Ihren Experience Platform **[!UICONTROL Benutzernamen]**-Berechtigungswert. Die ID hat das Format `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Datenbankkennwort]** | Diese alphanumerische Zeichenfolge ist Ihre Experience Platform **[!UICONTROL Kennwort]**-Berechtigung. Wenn Sie nicht ablaufende Anmeldeinformationen verwenden möchten, ist dieser Wert die verketteten Argumente aus den `technicalAccountID` und den `credential`, die in der JSON-Konfigurationsdatei heruntergeladen wurden. Der Kennwortwert hat das folgende Format: {technicalAccountId}:{credential}. Die JSON-Konfigurationsdatei für nicht ablaufende Anmeldeinformationen ist ein einmaliger Download während der Initialisierung, von dem Adobe keine Kopie aufbewahrt. |

Nachdem Sie alle relevanten Anmeldeinformationen eingegeben haben, wählen Sie **[!DNL Connect]** aus.

Das Dialogfeld [!DNL Connect] wird beim ersten Mal der Sitzung angezeigt. Geben Sie Ihre Benutzername und Ihr Kennwort ein und wählen Sie **[!DNL Connect]** aus. Im Protokoll wird eine Meldung angezeigt, mit der eine erfolgreiche Verbindung bestätigt wird.

## Nächste Schritte

Nachdem Sie [!DNL DbVisualizer] mit [!DNL Query Service] verbunden haben, können Sie mit [!DNL DbVisualizer] Abfragen schreiben. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im [Handbuch zur Ausführung von Abfragen](../best-practices/writing-queries.md).
