---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Db Visualizer; DbVisualizer; db Visualizer; Verbindung mit Query Service;
solution: Experience Platform
title: Verbinden von DbVisualizer mit Query Service
topic-legacy: connect
description: In diesem Dokument werden die Schritte zum Verbinden von DbVisualizer mit Adobe Experience Platform Query Service beschrieben.
exl-id: badb0d89-1713-438c-8a9c-d1404051ff5f
source-git-commit: ad3e1b0de6dd3b82cc82f0dc3d0f36b12cd3899e
workflow-type: tm+mt
source-wordcount: '726'
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

Wählen Sie im Arbeitsbereich Datenbankverbindung die **[!DNL Properties]** , gefolgt von der **[!DNL Driver Properties]** über die Navigationsseitenleiste aus.

![Der Arbeitsbereich Datenbankverbindung , in dem die Registerkarte Eigenschaften hervorgehoben ist.](../images/clients/dbvisualizer/driver-properties.png)

Die drei erforderlichen Treibereigenschaften sind in der folgenden Tabelle aufgeführt.

| Eigenschaft | Beschreibung |
| ------ | ------ |
| `PGHOST` | Der Hostname für die [!DNL PostgreSQL] Server. Dieser Wert ist Ihre Experience Platform [!UICONTROL Host] Berechtigung. |
| `SSL` | Dies steuert die Verwendung von SSL-Anforderungen. You **must** Verwenden Sie den Wert &quot;1&quot;, um diese Anforderung zu aktivieren. |
| `user` | Der mit der Datenbank verbundene Benutzername ist Ihre Organisations-ID. Es handelt sich um eine alphanumerische Zeichenfolge, die auf `@adobe.org` |

>[!IMPORTANT]
>
>Siehe [[!DNL Query Service] SSL-Dokumentation](./ssl-modes.md) Erfahren Sie mehr über die SSL-Unterstützung für Drittanbieterverbindungen zu Adobe Experience Platform Query Service und über die Verbindung mit `verify-full` SSL-Modus.

### [!DNL Query Service] Anmeldeinformationen

Die `PGHOST` und `user` -Werte aus Ihren Adobe Experience Platform-Anmeldedaten entnommen werden. Um Ihre Anmeldeinformationen zu finden, melden Sie sich bei der Platform-Benutzeroberfläche an und wählen Sie **[!UICONTROL Abfragen]** aus der linken Navigation, gefolgt von **[!UICONTROL Anmeldeinformationen]**. Weitere Informationen zum Auffinden Ihres Datenbanknamens, Hosts, Ports und Ihrer Anmeldedaten finden Sie in der [Handbuch zu Anmeldeinformationen](../ui/credentials.md).

![Experience Platform Query Credentials Dashboard mit hervorgehobenen Anmeldeinformationen.](../images/clients/dbvisualizer/query-service-credentials-page.png)

[!DNL Query Service] bietet auch nicht ablaufende Anmeldeinformationen, um eine einmalige Einrichtung mit Drittanbieterclients zu ermöglichen. Weitere Informationen finden Sie in der Dokumentation für [Vollständige Anweisungen zum Generieren und Verwenden von nicht ablaufenden Anmeldedaten](../ui/credentials.md#non-expiring-credentials).

Verwenden Sie die Suchleiste, um jede Eigenschaft zu suchen, und wählen Sie dann die entsprechende Zelle für den Parameterwert aus. Die Zelle wird blau hervorgehoben. Geben Sie Ihre Platform-Anmeldedaten in das Wertefeld ein und wählen Sie **[!DNL Apply]** , um die Treibereigenschaft hinzuzufügen.

>[!NOTE]
>
>So fügen Sie eine Sekunde hinzu `user` Profil auswählen `user` Wählen Sie in der Parameterspalte das blaue Plussymbol (+) aus, um Anmeldeinformationen für jeden Benutzer hinzuzufügen. Auswählen **[!DNL Apply]** , um die Treibereigenschaft hinzuzufügen.

Die [!DNL Edited] -Spalte zeigt ein Häkchen an, um anzugeben, dass der Parameterwert aktualisiert wurde.

## Authentifizierung

Wenn bei jeder Verbindungsherstellung eine Benutzer-ID und eine kennwortbasierte Authentifizierung erforderlich sein sollen, wählen Sie **[!DNL Authentication]** von der Navigationsseitenleiste unter [!DNL PostgreSQL].

Überprüfen Sie im Bereich &quot;Verbindungs-Authentifizierung&quot;beide **[!DNL Require Userid]** und **[!DNL Require Password]** Kontrollkästchen und wählen Sie **[!DNL Apply]**.

![Das Bedienfeld Verbindungs-Authentifizierung mit den Kontrollkästchen &quot;Benutzername&quot;und &quot;Kennwort&quot;wurde hervorgehoben.](../images/clients/dbvisualizer/connection-authentication.png)

## Verbinden von  mit Platform

Um eine Verbindung herzustellen, wählen Sie die **[!DNL Connection]** im Arbeitsbereich &quot;Datenbankverbindung&quot;und geben Sie Ihre Anmeldedaten für die Experience Platform für die folgenden Einstellungen ein.

- **Name**: Es wird empfohlen, einen benutzerfreundlichen Namen anzugeben, um die Verbindung zu erkennen.
- **Datenbankserver**: Das ist Ihre Experience Platform [!UICONTROL Host] Berechtigung.
- **Datenbankanschluss**: Der Port für [!DNL Query Service]. Sie müssen Port 80 verwenden, um eine Verbindung mit [!DNL Query Service].
- **Datenbank**: Berechtigung verwenden `dbname` value `prod:all`.
- **Database Userid**: Dies ist Ihre Platform-Organisations-ID. Die Benutzer-ID hat das Format `ORG_ID@AdobeOrg`.
- **Datenbankkennwort**: Dies ist eine alphanumerische Zeichenfolge, die auf der [!DNL Query Service] Anmeldedaten-Dashboard.

Nachdem Sie alle relevanten Anmeldeinformationen eingegeben haben, wählen Sie **[!DNL Connect]**.

![Der Arbeitsbereich Datenbankverbindung mit der Registerkarte Verbindung und der hervorgehobenen Schaltfläche Verbindung .](../images/clients/dbvisualizer/connect.png)

Die [!DNL Connect] wird zum ersten Mal in der Sitzung angezeigt.

![Das Dialogfeld Verbindung mit den Textfeldern Datenbankbenutzer und Datenbankkennwort wird hervorgehoben.](../images/clients/dbvisualizer/connect-dialog.png)

Geben Sie Ihre Benutzername und Ihr Kennwort ein und wählen Sie **[!DNL Connect]**. Im Protokoll wird eine Meldung angezeigt, mit der eine erfolgreiche Verbindung bestätigt wird.

## Nächste Schritte

Nachdem Sie eine Verbindung hergestellt haben [!DNL DbVisualizer] mit [!DNL Query Service]können Sie [!DNL DbVisualizer] , um Abfragen zu schreiben. Weitere Informationen zum Schreiben und Ausführen von Abfragen finden Sie im Abschnitt [Handbuch zur Ausführung von Abfragen](../best-practices/writing-queries.md).
