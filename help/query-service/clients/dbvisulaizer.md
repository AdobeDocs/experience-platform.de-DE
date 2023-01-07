---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Db Visualizer; DbVisualizer; db Visualizer; Verbindung mit Query Service;
solution: Experience Platform
title: Verbinden von DbVisualizer mit Query Service
description: In diesem Dokument werden die Schritte zum Verbinden von DbVisualizer mit Adobe Experience Platform Query Service beschrieben.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: 58eadaaf461ecd9598f3f508fab0c192cf058916
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 1%

---

# Verbinden [!DNL DbVisualizer] nach [!DNL Query Service] {#connect-dbvisualizer}

In diesem Dokument werden die Schritte zum Verbinden des [!DNL DbVisualizer] Datenbank-Tool mit Adobe Experience Platform [!DNL Query Service].

## Erste Schritte

Für dieses Handbuch benötigen Sie bereits Zugriff auf [!DNL DbVisualizer] -Desktop-Programm verwenden und mit dem Navigieren in der -Benutzeroberfläche vertraut sind. So laden Sie die [!DNL DbVisualizer] Desktop-Programm oder weitere Informationen finden Sie unter [offiziell [!DNL DbVisualizer] Dokumentation](https://www.dbvis.com/download/).

>[!NOTE]
>
>Es gibt [!DNL Windows], [!DNL macOS]und [!DNL Linux] Versionen von [!DNL DbVisualizer]. Screenshots in diesem Handbuch wurden mit dem [!DNL macOS] Desktop-Programm. In der Benutzeroberfläche können zwischen den Versionen geringfügige Unterschiede bestehen.

So erwerben Sie die erforderlichen Anmeldeinformationen zum Herstellen einer Verbindung [!DNL  DbVisualizer] zur Experience Platform benötigen Sie Zugriff auf den Arbeitsbereich Abfragen in der Platform-Benutzeroberfläche. Wenden Sie sich an Ihren IMS-Organisationsadministrator, wenn Sie derzeit keinen Zugriff auf den Arbeitsbereich &quot;Abfragen&quot;haben.

## Datenbankverbindung erstellen {#connect-database}

Nachdem Sie das Desktop-Programm auf Ihrem lokalen Computer installiert haben, starten Sie das Programm und wählen Sie **[!DNL Create a Database Connection]** von der ersten [!DNL DbVisualizer] Menü. Wählen Sie anschließend **[!DNL Create a Connection]** im Bereich auf der rechten Seite.

![Die [!DNL DbVisualizer] Hauptmenü mit hervorgehobener Option &quot;Datenbankverbindung erstellen&quot;.](../images/clients/dbvisualizer/create-db-connection.png)

Verwenden Sie die Suchleiste oder wählen Sie [!DNL PostgreSQL] aus der Dropdown-Liste für den Treibernamen. Der Arbeitsbereich Datenbankverbindung wird angezeigt.

![Das Dropdown-Menü für den Treibernamen mit [!DNL PostgreSQL] hervorgehoben.](../images/clients/dbvisualizer/driver-name.png)

### Festlegen von Eigenschaften für Ihre Verbindung {#properties}

Wählen Sie im Arbeitsbereich Datenbankverbindung die **[!DNL Properties]** , gefolgt von der **[!DNL Driver Properties]** über die Navigationsseitenleiste aus.

![Der Arbeitsbereich Datenbankverbindung mit den Eigenschaften und Treibereigenschaften wurde hervorgehoben.](../images/clients/dbvisualizer/driver-properties.png)

Geben Sie anschließend die in der folgenden Tabelle beschriebenen Treibereigenschaften ein.

>[!IMPORTANT]
>
>Um DBVisualizer mit Adobe Experience Platform zu verbinden, müssen Sie die Verwendung von SSL aktivieren. Siehe [Dokumentation zu SSL-Modi](./ssl-modes.md) Erfahren Sie mehr über die SSL-Unterstützung für Drittanbieterverbindungen zu Adobe Experience Platform Query Service und über die Verbindung mit `verify-full` SSL-Modus.

| Eigenschaft | Beschreibung |
| ------ | ------ |
| `PGHOST` | Der Hostname für die [!DNL PostgreSQL] Server. Dieser Wert ist Ihre Experience Platform **[!UICONTROL Host] credential**. |
| `ssl` | SSL-Wert definieren `1` , um die Verwendung von SSL zu aktivieren. |
| `sslmode` | Dies steuert den SSL-Schutz. Es wird empfohlen, die `require` SSL-Modus beim Verbinden von Clients von Drittanbietern mit Adobe Experience Platform. Die `require` -Modus stellt sicher, dass bei allen Kommunikationen eine Verschlüsselung erforderlich ist und dass das Netzwerk vertrauenswürdig ist, eine Verbindung zum richtigen Server herzustellen. Die Überprüfung des SSL-Zertifikats des Servers ist nicht erforderlich. |
| `user` | Der mit der Datenbank verbundene Benutzername ist Ihre Organisations-ID. Es handelt sich um eine alphanumerische Zeichenfolge, die auf `@Adobe.Org`. Dieser Wert ist Ihre Experience Platform **[!UICONTROL Benutzername] credential**. |

Verwenden Sie die Suchleiste, um jede Eigenschaft zu suchen, und wählen Sie dann die entsprechende Zelle für den Parameterwert aus. Die Zelle wird blau hervorgehoben. Geben Sie Ihre Platform-Anmeldedaten in das Wertefeld ein und wählen Sie **[!DNL Apply]** , um die Treibereigenschaft hinzuzufügen.

![Die Registerkarte Eigenschaften des DBVisulaizer-Treibers mit einem eingegebenen Wert und hervorgehobenem Anwenden.](../images/clients/dbvisualizer/apply-parameter-value.png)

>[!NOTE]
>
>So fügen Sie eine Sekunde hinzu `user` Profil auswählen `user` Wählen Sie in der Parameterspalte das blaue Plussymbol (+) aus, um Anmeldeinformationen für jeden Benutzer hinzuzufügen. Auswählen **[!DNL Apply]** , um die Treibereigenschaft hinzuzufügen.

Die [!DNL Edited] -Spalte zeigt ein Häkchen an, um anzugeben, dass der Parameterwert aktualisiert wurde.

### Eingabe[!DNL Query Service] Anmeldeinformationen

Um die Anmeldeinformationen zu finden, die zum Verbinden von BBVisualizer mit Query Service erforderlich sind, melden Sie sich bei der Platform-Benutzeroberfläche an und wählen Sie **[!UICONTROL Abfragen]** aus der linken Navigation, gefolgt von **[!UICONTROL Anmeldeinformationen]**. Weitere Informationen zum Auffinden Ihrer **Host**, **port**, **Datenbank**, **Benutzername** und **password** Anmeldeinformationen, lesen Sie bitte die [Handbuch zu Anmeldeinformationen](../ui/credentials.md).

![Auf der Seite &quot;Anmeldeinformationen&quot;im Arbeitsbereich &quot;Experience Platform-Abfragen&quot;werden Anmeldeinformationen und ablaufende Anmeldeinformationen hervorgehoben.](../images/clients/dbvisualizer/query-service-credentials-page.png)

>[!IMPORTANT]
>
>[!DNL Query Service] bietet auch nicht ablaufende Anmeldeinformationen, um eine einmalige Einrichtung mit Drittanbieterclients zu ermöglichen. Weitere Informationen finden Sie in der Dokumentation für [Vollständige Anweisungen zum Generieren und Verwenden von nicht ablaufenden Anmeldedaten](../ui/credentials.md#non-expiring-credentials). Dieser Prozess muss abgeschlossen werden, wenn Sie BDVisualizer als einmaliges Setup verbinden möchten. Die `credential` und `technicalAccountId` Die erworbenen Werte umfassen den Wert für den DBVisualizer `password` Parameter.

## Authentifizierung

Wenn bei jeder Verbindungsherstellung eine Benutzer-ID und eine kennwortbasierte Authentifizierung erforderlich sein sollen, wählen Sie **[!DNL Authentication]** von der Navigationsseitenleiste unter [!DNL PostgreSQL].

Überprüfen Sie im Bereich &quot;Verbindungs-Authentifizierung&quot;beide **[!DNL Require Userid]** und **[!DNL Require Password]** Kontrollkästchen und wählen Sie **[!DNL Apply]**.

![Das Authentifizierungsfenster für [!DNL PostgreSQL] Datenbankverbindung mit den hervorgehobenen Kontrollkästchen &quot;Require Userid&quot;und &quot;Password&quot;.](../images/clients/dbvisualizer/connection-authentication.png)

## Verbinden von  mit Platform

Sie können eine Verbindung mit ablaufenden oder nicht ablaufenden Anmeldeinformationen herstellen. Um eine Verbindung herzustellen, wählen Sie die **[!DNL Connection]** im Arbeitsbereich &quot;Datenbankverbindung&quot;und geben Sie Ihre Anmeldedaten für die Experience Platform für die folgenden Einstellungen ein.

>[!NOTE]
>
>Alle von BDVisualizer in der folgenden Tabelle erforderlichen Anmeldeinformationen sind für ablaufende und nicht ablaufende Anmeldeinformationen identisch, sofern sie nicht in der Parameterbeschreibung angegeben sind.

| Verbindungsparameter | Beschreibung |
|---|---|
| **[!UICONTROL Name]** | Erstellen Sie einen Namen für Ihre Verbindung. Es wird empfohlen, einen benutzerfreundlichen Namen anzugeben, um die Verbindung zu erkennen. |
| **[!UICONTROL Datenbankserver]** | Das ist Ihre Experience Platform **[!UICONTROL Host]** Berechtigung. |
| **[!UICONTROL Datenbankanschluss]** | Der Port für [!DNL Query Service]. Sie müssen Port verwenden **80** zur Verbindung mit [!DNL Query Service]. |
| **[!UICONTROL Datenbank]** | Verwenden Ihrer Experience Platform **[!UICONTROL Datenbank]** credential value: `prod:all`. |
| **[!UICONTROL Database Userid]** | Dies ist Ihre Platform-Organisations-ID. Verwenden Ihrer Experience Platform **[!UICONTROL Benutzername]** Berechtigungswert. Die ID hat das Format `ORG_ID@AdobeOrg`. |
| **[!UICONTROL Datenbankkennwort]** | Diese alphanumerische Zeichenfolge ist Ihre Experience Platform **[!UICONTROL Passwort]** credential.Wenn Sie nicht ablaufende Anmeldeinformationen verwenden möchten, ist dieser Wert die verketteten Argumente aus dem `technicalAccountID` und `credential` in die JSON-Konfigurationsdatei heruntergeladen wurde. Der Kennwortwert hat folgende Form: {technicalAccountId}:{credential}. Die JSON-Konfigurationsdatei für nicht ablaufende Anmeldeinformationen ist ein einmaliger Download während der Initialisierung, von dem die Adobe keine Kopie aufbewahrt. |

Nachdem Sie alle relevanten Anmeldeinformationen eingegeben haben, wählen Sie **[!DNL Connect]**.

![Die [!DNL PostgreSQL] Arbeitsbereich Datenbankverbindung , in dem die Registerkarte Verbindung und die Schaltfläche Verbindung hervorgehoben sind.](../images/clients/dbvisualizer/connect.png)

Die [!DNL Connect] wird zum ersten Mal in der Sitzung angezeigt.

![Die Verbindung: [!DNL PostgreSQL] mit den Textfeldern Datenbankbenutzer-ID und Datenbankkennwort markiert.](../images/clients/dbvisualizer/connect-dialog.png)

Geben Sie Ihre Benutzername und Ihr Kennwort ein und wählen Sie **[!DNL Connect]**. Im Protokoll wird eine Meldung angezeigt, mit der eine erfolgreiche Verbindung bestätigt wird.

## Nächste Schritte

Nachdem Sie eine Verbindung hergestellt haben [!DNL DbVisualizer] mit [!DNL Query Service]können Sie [!DNL DbVisualizer] , um Abfragen zu schreiben. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Abschnitt [Handbuch zur Ausführung von Abfragen](../best-practices/writing-queries.md).
