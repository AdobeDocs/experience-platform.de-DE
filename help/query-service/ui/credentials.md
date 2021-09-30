---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Abfrage; Abfrageeditor; Abfrage-Editor; Abfrage-Editor;
solution: Experience Platform
title: UI-Anleitung für Query Service
topic-legacy: guide
description: Adobe Experience Platform Query Service bietet eine Benutzeroberfläche, über die Abfragen geschrieben und ausgeführt, zuvor ausgeführte Abfragen angezeigt und auf Abfragen zugegriffen werden kann, die von Benutzern in Ihrer IMS-Organisation gespeichert wurden.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 696db8081ab8225d79cd468b7435770d407d3e3d
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 1%

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

### Voraussetzungen

Bevor Sie nicht ablaufende Anmeldeinformationen generieren können, müssen Sie die folgenden Schritte in Adobe Admin Console ausführen:

1. Melden Sie sich bei [Adobe Admin Console](https://adminconsole.adobe.com/) an und wählen Sie in der oberen Navigationsleiste die entsprechende Organisation aus.
2. [Produktprofil auswählen.](../../access-control/ui/browse.md)
3. [Konfigurieren Sie sowohl die Berechtigungen  **** Sandboxes als auch  **Query Service-** ](../../access-control/ui/permissions.md) Integrationen verwalten für das Produktprofil.
4. [Fügen Sie einem Produktprofil einen neuen Benutzer hinzu, ](../../access-control/ui/users.md) wenn ihm die konfigurierten Berechtigungen erteilt wurden.
5. [Fügen Sie den Benutzer als Produktprofiladministrator hinzu, ](https://helpx.adobe.com/enterprise/using/manage-product-profiles.html) um die Erstellung eines Kontos für jedes aktive Produktprofil zu ermöglichen.
6. [Fügen Sie den Benutzer als Produktprofilentwickler hinzu, ](https://helpx.adobe.com/de/enterprise/using/manage-developers.html) um eine Integration zu erstellen.

Weitere Informationen zum Zuweisen von Berechtigungen finden Sie in der Dokumentation zu [Zugriffskontrolle](../../access-control/home.md).

Alle erforderlichen Berechtigungen werden jetzt in der Adobe Developer Console konfiguriert, damit der Benutzer die Funktion für ablaufende Anmeldedaten verwenden kann.

### Anmeldeinformationen generieren

Um einen Satz nicht ablaufender Anmeldedaten zu erstellen, kehren Sie zur Platform-Benutzeroberfläche zurück und wählen Sie **[!UICONTROL Abfragen]** aus dem linken Navigationsbereich aus, um auf den Arbeitsbereich [!UICONTROL Abfragen] zuzugreifen. Wählen Sie anschließend die Registerkarte **[!UICONTROL Anmeldeinformationen]** und anschließend die Registerkarte **[!UICONTROL Anmeldeinformationen generieren]**.

![](../images/ui/credentials/generate-credentials.png)

Es wird ein Dialogfeld angezeigt, in dem Sie Anmeldeinformationen generieren können. Um nicht ablaufende Anmeldedaten zu erstellen, müssen Sie die folgenden Details angeben:

- **[!UICONTROL Name]**: Der Name der Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Beschreibung]**: (Optional) Eine Beschreibung für die Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Zugeordnet zu]**: Der Benutzer, dem die Anmeldeinformationen zugewiesen werden. Dieser Wert sollte die E-Mail-Adresse des Benutzers sein, der die Anmeldeinformationen erstellt.
- **[!UICONTROL Kennwort]**  (Optional) Ein optionales Kennwort für Ihre Anmeldedaten. Wenn das Kennwort nicht festgelegt ist, generiert Adobe automatisch ein Kennwort für Sie.

Nachdem Sie alle erforderlichen Details angegeben haben, wählen Sie **[!UICONTROL Anmeldeinformationen generieren]** aus, um Ihre Anmeldeinformationen zu generieren.

![](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Sobald die Schaltfläche **[!UICONTROL Anmeldeinformationen generieren]** ausgewählt ist, wird eine JSON-Konfigurationsdatei auf Ihren lokalen Computer heruntergeladen. Da in Adobe **nicht** die generierten Anmeldeinformationen aufgezeichnet werden, müssen Sie die heruntergeladene Datei sicher speichern und die Anmeldeinformationen aufbewahren.
>
>Wenn die Anmeldeinformationen 90 Tage lang nicht verwendet werden, werden die Anmeldeinformationen ebenfalls gelöscht.

Die JSON-Konfigurationsdatei enthält Informationen wie den Namen des technischen Kontos, die technische Konto-ID und die Anmeldedaten. Sie wird im folgenden Format bereitgestellt.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

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

Sie können die ablaufenden oder nicht ablaufenden Anmeldedaten verwenden, um eine Verbindung mit externen Clients wie Aqua Data Studio, Looker oder Power BI herzustellen. Die Eingabemethode für diese Anmeldeinformationen variiert je nach externem Client. Spezifische Anweisungen zur Verwendung dieser Anmeldeinformationen finden Sie in der Dokumentation des externen Kunden.

Das Bild zeigt den Speicherort der einzelnen Parameter in der Benutzeroberfläche an, mit Ausnahme des Kennworts der nicht ablaufenden Anmeldeinformationen. Während nicht ablaufende Anmeldeinformationen von ihren JSON-Konfigurationsdateien bereitgestellt werden, können Sie Ihre ablaufenden Anmeldeinformationen auf der Registerkarte **Anmeldedaten** in der Benutzeroberfläche anzeigen.

![](../images/ui/credentials/expiring-credentials.png)

In der folgenden Tabelle sind die Parameter aufgeführt, die normalerweise für die Verbindung mit externen Clients erforderlich sind.

>[!NOTE]
>
>Beim Herstellen einer Verbindung zu einem Host mit nicht ablaufenden Anmeldeinformationen müssen weiterhin alle im Abschnitt [!UICONTROL EXPIRING CREDENTIALS] aufgeführten Parameter verwendet werden, mit Ausnahme des Kennworts und des Benutzernamens.

| Parameter | Beschreibung |
|---|---|
| Server/Host | Der Name des Servers/Hosts, mit dem Sie eine Verbindung herstellen. <ul><li>Dieser Wert wird für ablaufende und nicht ablaufende Anmeldeinformationen verwendet und hat die Form `server.adobe.io`. Der Wert befindet sich unter **[!UICONTROL Host]** im Abschnitt [!UICONTROL EXPIRING CREDENTIALS] .</ul></li> |
| Port | Der Anschluss für den Server/Host, mit dem Sie eine Verbindung herstellen. <ul><li>Dieser Wert wird sowohl für ablaufende als auch für nicht ablaufende Anmeldeinformationen verwendet und befindet sich unter **[!UICONTROL Port]** im Abschnitt [!UICONTROL EXPIRING CREDENTIALS] . Ein Beispielwert für den Port wäre `80`.</ul></li> |
| Datenbank | Die Datenbank, mit der Sie eine Verbindung herstellen. <ul><li>Dieser Wert wird sowohl für ablaufende als auch für nicht ablaufende Anmeldeinformationen verwendet und befindet sich unter **[!UICONTROL Database]** im Abschnitt [!UICONTROL EXPIRING CREDENTIALS] . Ein Beispielwert für die Datenbank wäre `prod:all`.</ul></li> |
| Benutzername | Der Benutzername für den Benutzer, der eine Verbindung zum externen Client herstellt. <ul><li>Wenn Sie ablaufende Anmeldeinformationen verwenden, wird diese in Form einer alphanumerischen Zeichenfolge vor `@AdobeOrg` angezeigt. Dieser Wert befindet sich unter **[!UICONTROL Benutzername]**.</li><li>Wenn Sie nicht ablaufende Anmeldeinformationen verwenden, ist dies eine Zeichenfolge Ihrer Wahl, obwohl **nicht** derselbe Wert wie der `technicalAccountID`-Wert in der JSON-Konfigurationsdatei sein kann.</li></ul> |
| Passwort | Das Kennwort für den Benutzer, der eine Verbindung zum externen Client herstellt. <ul><li>Wenn Sie ablaufende Anmeldeinformationen verwenden, finden Sie diese unter **[!UICONTROL Kennwort]** im Abschnitt [!UICONTROL EXPIRING CREDENTIALS] .</li><li>Wenn Sie nicht ablaufende Anmeldeinformationen verwenden, ist dieser Wert die verketteten Argumente aus der technicalAccountID und die Berechtigung aus der JSON-Konfigurationsdatei. Der Kennwortwert hat folgende Form: `{technicalAccountId}:{credential}`.</li></ul> |

## Nächste Schritte

Nachdem Sie nun wissen, wie ablaufende und nicht ablaufende Anmeldeinformationen funktionieren, können Sie diese Anmeldeinformationen verwenden, um eine Verbindung zu externen Clients herzustellen. Weitere Informationen zu externen Clients finden Sie im Handbuch [Clients mit Query Service verbinden](../clients/overview.md).
