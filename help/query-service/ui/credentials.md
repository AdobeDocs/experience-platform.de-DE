---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Abfrage; Abfrageeditor; Abfrage-Editor; Abfrage-Editor;
solution: Experience Platform
title: UI-Anleitung für Query Service
topic-legacy: guide
description: Adobe Experience Platform Query Service bietet eine Benutzeroberfläche, über die Abfragen geschrieben und ausgeführt, zuvor ausgeführte Abfragen angezeigt und auf Abfragen zugegriffen werden kann, die von Benutzern in Ihrer IMS-Organisation gespeichert wurden.
exl-id: 99ad25e4-0ca4-4bd1-b701-ab463197930b
source-git-commit: aabe89f236bc68a51f14ee1909687982f4fe5973
workflow-type: tm+mt
source-wordcount: '824'
ht-degree: 0%

---


# Handbuch zu Anmeldeinformationen

Mit Adobe Experience Platform Query Service können Sie eine Verbindung mit externen Clients herstellen. Sie können eine Verbindung zu diesen externen Clients herstellen, indem Sie entweder ablaufende oder nicht ablaufende Anmeldeinformationen verwenden.

## Ablaufberechtigungen

Sie können ablaufende Anmeldedaten verwenden, um schnell eine Verbindung zu einem externen Client herzustellen.

![](../images/ui/credentials/expiring-credentials.png)

Der Abschnitt **[!UICONTROL Ablaufende Anmeldedaten]** enthält die folgenden Informationen:

- **[!UICONTROL Host]**: Der Name des Hosts, mit dem Sie eine Verbindung herstellen möchten. Für die Verbindung mit Query Service enthält dies den Namen der IMS-Organisation, die Sie derzeit verwenden.
- **[!UICONTROL Port]**: Die Anschlussnummer des Hosts, mit dem Sie eine Verbindung herstellen möchten.
- **[!UICONTROL Datenbank]**: Der Name der Datenbank, mit der Sie eine Verbindung herstellen möchten.
- **[!UICONTROL Benutzername]**: Der Benutzername, mit dem Sie eine Verbindung zu Query Service herstellen.
- **[!UICONTROL Kennwort]**: Das Kennwort, mit dem Sie eine Verbindung zu Query Service herstellen.
- **[!UICONTROL PSQL-Befehl]**: Ein Befehl, der automatisch alle relevanten Informationen eingefügt hat, damit Sie über PSQL über die Befehlszeile eine Verbindung zu Query Service herstellen können.
- **[!UICONTROL Läuft ab]**: Das Ablaufdatum für die ablaufenden Anmeldeinformationen. Die Anmeldeinformationen laufen 24 Stunden nach ihrer Erstellung ab.

## Nicht ablaufende Anmeldeinformationen

Sie können nicht ablaufende Anmeldedaten verwenden, um eine permanentere Verbindung zu einem externen Client einzurichten.

Um einen Satz nicht ablaufender Anmeldeinformationen zu erstellen, wählen Sie **[!UICONTROL Anmeldeinformationen generieren]** aus.

>[!NOTE]
>
>Bevor Sie nicht ablaufende Anmeldeinformationen erstellen können, müssen Sie über die Berechtigungen **Sandboxes** und **Query Service-Integration verwalten** verfügen. Informationen zum Zuweisen dieser Berechtigungen finden Sie in der Dokumentation unter [Zugriffssteuerung](../../access-control/home.md).

![](../images/ui/credentials/generate-credentials.png)

Das Modal zum Generieren von Anmeldeinformationen wird angezeigt. Um nicht ablaufende Anmeldedaten zu erstellen, müssen Sie die folgenden Details angeben:

- **[!UICONTROL Name]**: Der Name der Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Beschreibung]**: (Optional) Eine Beschreibung für die Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Zugeordnet zu]**: Der Benutzer, dem die Anmeldeinformationen zugewiesen werden. Dieser Wert sollte die E-Mail-Adresse des Benutzers sein, der die Anmeldeinformationen erstellt.
- **[!UICONTROL Kennwort]**  (Optional) Ein optionales Kennwort für Ihre Anmeldedaten. Wenn das Kennwort nicht festgelegt ist, generiert Adobe automatisch ein Kennwort für Sie.

Nachdem Sie alle erforderlichen Details angegeben haben, wählen Sie **[!UICONTROL Anmeldeinformationen generieren]** aus, um Ihre Anmeldeinformationen zu generieren.

![](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Sobald die Schaltfläche **[!UICONTROL Anmeldeinformationen generieren]** ausgewählt ist, enthält eine Konfigurationsdatei Informationen wie den Namen des technischen Kontos, die ID des technischen Kontos und die Anmeldedaten. Da in Adobe **nicht** die generierten Anmeldedaten aufgezeichnet werden, müssen Sie **die heruntergeladene Datei sicher speichern und die Anmeldedaten speichern.**
>
>Wenn die Anmeldeinformationen 90 Tage lang nicht verwendet werden, werden die Anmeldeinformationen ebenfalls aktualisiert.

Nachdem Sie die generierten Anmeldeinformationen gespeichert haben, wählen Sie **[!UICONTROL Close]** aus. Sie können jetzt eine Liste aller nicht ablaufenden Anmeldedaten anzeigen.

![](../images/ui/credentials/list-credentials.png)

Sie können Ihre nicht ablaufenden Anmeldedaten entweder bearbeiten oder löschen. Um eine nicht ablaufende Berechtigung zu bearbeiten, wählen Sie das Stiftsymbol (![](../images/ui/credentials/edit-icon.png)) aus. Um eine nicht ablaufende Berechtigung zu löschen, wählen Sie das Löschsymbol (![](../images/ui/credentials/delete-icon.png)) aus.

Beim Bearbeiten einer nicht ablaufenden Berechtigung wird ein Modal angezeigt. Sie können die folgenden Details zur Aktualisierung angeben:

- **[!UICONTROL Name]**: Der Name der Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Beschreibung]**: (Optional) Eine Beschreibung für die Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Zugeordnet zu]**: Der Benutzer, dem die Anmeldeinformationen zugewiesen werden. Dieser Wert sollte die E-Mail-Adresse des Benutzers sein, der die Anmeldeinformationen erstellt.

![](../images/ui/credentials/update-credentials.png)

Nachdem Sie alle erforderlichen Details angegeben haben, wählen Sie **[!UICONTROL Konto aktualisieren]** aus, um die Aktualisierung Ihrer Anmeldedaten abzuschließen.

## Verwenden von Anmeldeinformationen zum Herstellen einer Verbindung zu externen Clients

Sie können die ablaufenden oder nicht ablaufenden Anmeldedaten verwenden, um eine Verbindung mit externen Clients wie Aqua Data Studio, Looker oder Power BI herzustellen.

Bei der Verbindung mit diesen externen Clients müssen Sie im Allgemeinen die folgenden Informationen einschließen:

- **Server/Host**: Der Name des Servers/Hosts, mit dem Sie eine Verbindung herstellen. Dieser Wert hat die Form `server.adobe.io` und kann im Abschnitt **[!UICONTROL Host]** unter den ablaufenden Anmeldedaten gefunden werden.
- **Port**: Der Anschluss für den Server/Host, mit dem Sie eine Verbindung herstellen. Dieser Wert befindet sich unter **[!UICONTROL Port]** im Abschnitt mit ablaufenden Anmeldedaten. Ein Beispielwert für den Port wäre `80`.
- **Benutzername**: Der Benutzername für den Benutzer, der eine Verbindung zum externen Client herstellt. Dies hat die Form `ID@AdobeOrg` und kann unter **[!UICONTROL Benutzername]** im Abschnitt mit ablaufenden Anmeldedaten gefunden werden.
- **Kennwort**: Das Kennwort für den Benutzer, der eine Verbindung zum externen Client herstellt. Wenn Sie ablaufende Anmeldeinformationen verwenden, finden Sie diese unter **[!UICONTROL Kennwort]** im Abschnitt für ablaufende Anmeldeinformationen. Wenn Sie nicht ablaufende Anmeldedaten verwenden, besteht dieser Wert sowohl aus der technischen Konto-ID als auch aus der Anmeldedaten im Formular: `technicalAccountId:credential`.
- **Datenbank**: Die Datenbank, mit der Sie eine Verbindung herstellen. Dieser Wert befindet sich unter **[!UICONTROL Database]** im Abschnitt mit ablaufenden Anmeldedaten. Ein Beispielwert für die Datenbank wäre `prod:all`.

## Nächste Schritte

Nachdem Sie nun wissen, wie ablaufende und nicht ablaufende Anmeldeinformationen funktionieren, können Sie diese Anmeldeinformationen verwenden, um eine Verbindung zu externen Clients herzustellen. Weitere Informationen zu externen Clients finden Sie im Handbuch [Clients mit Query Service verbinden](../clients/overview.md).