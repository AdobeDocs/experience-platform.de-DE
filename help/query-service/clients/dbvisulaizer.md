---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;Db Visualizer;DbVisualizer;db Visualizer;Verbindung zum Abfrage-Service herstellen;
solution: Experience Platform
title: Verbinden von DbVisualizer mit dem Abfrage-Service
description: In diesem Dokument werden die Schritte zum Verbinden von DbVisualizer mit dem Abfrage-Service von Adobe Experience Platform erläutert.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '891'
ht-degree: 5%

---

# [!DNL DbVisualizer] mit [!DNL Query Service] verbinden {#connect-dbvisualizer}

In diesem Dokument werden die Schritte zum Verbinden des [!DNL DbVisualizer]-Datenbanktools mit Adobe Experience Platform [!DNL Query Service] beschrieben.

## Erste Schritte

Für dieses Handbuch müssen Sie bereits Zugriff auf die [!DNL DbVisualizer] Desktop-App haben und mit dem Navigieren in der zugehörigen Benutzeroberfläche vertraut sein. Informationen zum Herunterladen der [!DNL DbVisualizer] Desktop-App oder weitere Informationen finden Sie unter [Official [!DNL DbVisualizer] Documentation](https://www.dbvis.com/download/).

Um die erforderlichen Anmeldedaten zum Verbinden von [!DNL  DbVisualizer] mit Experience Platform zu erhalten, benötigen Sie Zugriff auf den Arbeitsbereich „Abfragen“ in der Platform-Benutzeroberfläche. Wenden Sie sich an den Admin Ihrer Organisation, wenn Sie derzeit keinen Zugriff auf den Arbeitsbereich „Abfragen“ haben.

## Erstellen einer Datenbankverbindung {#connect-database}

Nachdem Sie die Desktop-App auf Ihrem lokalen Computer installiert haben, befolgen Sie die offiziellen BDVisualizer-Anweisungen, um [eine neue Datenbankverbindung zu erstellen](https://confluence.dbvis.com/display/UG130/Create+a+New+Database+Connection).

Nachdem Sie **[!DNL PostgreSQL]** aus der Liste [!DNL Connections] ausgewählt haben, wird die Registerkarte [!DNL Object View] für die neue [!DNL PostgreSQL] angezeigt.

### Festlegen von Treibereigenschaften für Ihre Verbindung {#properties}

Wählen Sie auf der Registerkarte [!DNL PostgreSQL] die Registerkarte **[!DNL Properties]** und dann in der Navigationsseitenleiste die **[!DNL Driver Properties]** aus. Weitere Informationen zu [Fahrereigenschaften](https://confluence.dbvis.com/display/UG130/Configuring+Connection+Properties#ConfiguringConnectionProperties-DriverProperties) finden Sie in der offiziellen Dokumentation.

Geben Sie als Nächstes die in der folgenden Tabelle beschriebenen Treibereigenschaften ein.

>[!IMPORTANT]
>
>Um DBVisualizer mit Adobe Experience Platform zu verbinden, müssen Sie die Verwendung von SSL aktivieren. Siehe die [SSL-Modi](./ssl-modes.md) um mehr über die SSL-Unterstützung für Drittanbieterverbindungen zum Abfrage-Service von Adobe Experience Platform zu erfahren und darüber, wie Sie eine Verbindung mit `verify-full` SSL-Modus herstellen.

| Eigenschaft | Beschreibung |
| ------ | ------ |
| `PGHOST` | Der Hostname für den [!DNL PostgreSQL]. Dieser Wert ist Ihre Experience Platform **[!UICONTROL Host]-**. |
| `ssl` | Definieren Sie den SSL-`1`, um die Verwendung von SSL zu aktivieren. |
| `sslmode` | Dies steuert das SSL-Schutzniveau. Es wird empfohlen, beim Verbinden von Drittanbieter-Clients mit Adobe Experience Platform den `require`-SSL-Modus zu verwenden. Der `require`-Modus stellt sicher, dass alle Kommunikationen verschlüsselt werden müssen und dass das Netzwerk für die Verbindung mit dem richtigen Server vertrauenswürdig ist. Die Validierung des SSL-Zertifikats des Servers ist nicht erforderlich. |
| `user` | Der mit der Datenbank verbundene Benutzername ist Ihre Organisations-ID. Es handelt sich um eine alphanumerische Zeichenfolge, die auf `@Adobe.Org` endet. Dieser Wert ist Ihre Experience Platform **[!UICONTROL Benutzername]-**. |

Verwenden Sie die Suchleiste, um jede Eigenschaft zu finden, und wählen Sie dann die entsprechende Zelle für den Parameterwert aus. Die Zelle wird blau hervorgehoben. Geben Sie Ihre Platform-Anmeldeinformationen in das Feld Wert ein und wählen Sie **[!DNL Apply]** aus, um die Treibereigenschaft hinzuzufügen.

>[!NOTE]
>
>Um ein zweites `user` hinzuzufügen, wählen Sie in der Spalte Parameter die Option `user` und dann das blaue Pluszeichen (+) aus, um Anmeldeinformationen für die einzelnen Benutzer hinzuzufügen. Wählen Sie **[!DNL Apply]** aus, um die Treibereigenschaft hinzuzufügen.

Die Spalte [!DNL Edited] enthält ein Häkchen, das anzeigt, dass der Parameterwert aktualisiert wurde.

### Anmeldedaten für den Abfrage-Service eingeben {#query-service-credentials}

Um die Anmeldeinformationen zu finden, die zum Verbinden von BBVisualizer mit dem Abfrage-Service erforderlich sind, melden Sie sich bei der Platform-Benutzeroberfläche an und wählen Sie **[!UICONTROL Abfragen]** aus der linken Navigation aus, gefolgt von **[!UICONTROL Anmeldeinformationen]**. Weitere Informationen zum Auffinden der Anmeldeinformationen **host**, **port**, **database**, **username** und **password** finden Sie im Handbuch [credentials](../ui/credentials.md).

![Die Seite mit den Anmeldeinformationen des Arbeitsbereichs &quot;Experience Platform-Abfragen“ mit hervorgehobenen Anmeldeinformationen und den ablaufenden Anmeldeinformationen.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] bietet auch nicht ablaufende Anmeldeinformationen, um eine einmalige Einrichtung mit Drittanbieter-Clients zu ermöglichen. Siehe die Dokumentation für [vollständige Anweisungen zum Generieren und Verwenden nicht ablaufender Anmeldeinformationen](../ui/credentials.md#non-expiring-credentials). Es ist notwendig, diesen Prozess abzuschließen, wenn Sie BDVisualizer als einmaliges Setup verbinden möchten. Die erfassten `credential`- und `technicalAccountId`-Werte umfassen den Wert für den DBVisualizer-`password`.

## Authentifizierung {#authentication}

Um bei jeder Verbindung eine Benutzer-ID und eine kennwortbasierte Authentifizierung erforderlich zu machen, navigieren Sie zur Registerkarte [!DNL Properties] und wählen Sie **[!DNL Authentication]** in der Navigations-Seitenleiste unter [!DNL PostgreSQL] aus.

Aktivieren Sie im Bedienfeld „Verbindungsauthentifizierung“ die Kontrollkästchen **[!DNL Require Userid]** und **[!DNL Require Password]** und wählen Sie dann **[!DNL Apply]** aus. Weitere Informationen zum [Festlegen von Authentifizierungsoptionen](https://confluence.dbvis.com/display/UG140/Setting+Common+Authentication+Options) finden Sie in der offiziellen Dokumentation.

## Verbindung mit Platform herstellen

Sie können eine Verbindung mit ablaufenden oder nicht ablaufenden Anmeldeinformationen herstellen. Um eine Verbindung herzustellen, wählen Sie die Registerkarte **[!DNL Connection]** auf der Registerkarte [!DNL PostgreSQL]-Objektansicht und geben Sie Ihre Experience Platform-Anmeldeinformationen für die folgenden Einstellungen ein. Ergänzende Anweisungen zum [Einrichten einer manuellen Verbindung](https://confluence.dbvis.com/display/UG100/Setting+Up+a+Connection+Manually) finden Sie auf der offiziellen DBVisualizer-Website.

>[!NOTE]
>
>Alle von BDVisualizer in der folgenden Tabelle erforderlichen Anmeldeinformationen sind für ablaufende und nicht ablaufende Anmeldeinformationen identisch, es sei denn, dies wird in der Parameterbeschreibung angegeben.

| Verbindungsparameter | Beschreibung |
|---|---|
| **[!UICONTROL Name]** | Erstellen Sie einen Namen für Ihre Verbindung. Es wird empfohlen, einen benutzerfreundlichen Namen anzugeben, um die Verbindung zu erkennen. |
| **[!UICONTROL Datenbankserver]** | Dies ist Ihre Experience Platform **[!UICONTROL Host]**-Berechtigung. |
| **[!UICONTROL Datenbank-Port]** | Der Port für [!DNL Query Service]. Sie müssen Port **80** oder **5432** verwenden, um eine Verbindung mit [!DNL Query Service] herzustellen. |
| **[!UICONTROL Datenbank]** | Verwenden Sie den Berechtigungswert **[!UICONTROL Experience Platform]** Datenbank): `prod:all`. |
| **[!UICONTROL Datenbank-Benutzer-ID]** | Dies ist Ihre Platform-Organisations-ID. Verwenden Sie den Berechtigungswert **[!UICONTROL Experience Platform]** Benutzername). Die ID hat das Format `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Datenbankkennwort]** | Diese alphanumerische Zeichenfolge ist Ihre Experience Platform **[!UICONTROL Kennwort]**-Berechtigung. Wenn Sie nicht ablaufende Anmeldeinformationen verwenden möchten, ist dieser Wert die verketteten Argumente aus der `technicalAccountID` und der in die JSON-Konfigurationsdatei heruntergeladenen `credential`. Das Kennwort hat folgende Form: {technicalAccountId}:{credential}. Die JSON-Konfigurationsdatei für nicht ablaufende Anmeldeinformationen ist ein einmaliger Download während ihrer Initialisierung, von dem Adobe keine Kopie speichert. |

Nachdem Sie alle relevanten Anmeldeinformationen eingegeben haben, wählen Sie **[!DNL Connect]** aus.

Das [!DNL Connect] Dialogfeld wird bei der ersten Sitzung angezeigt. Geben Sie Ihre Benutzer-ID und Ihr Kennwort ein und wählen Sie **[!DNL Connect]** aus. Im Protokoll wird eine Meldung angezeigt, die eine erfolgreiche Verbindung bestätigt.

## Nächste Schritte

Nachdem Sie [!DNL DbVisualizer] mit [!DNL Query Service] verbunden haben, können Sie [!DNL DbVisualizer] verwenden, um Abfragen zu schreiben. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im [Handbuch zur Ausführung von Abfragen](../best-practices/writing-queries.md).
