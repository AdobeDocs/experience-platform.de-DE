---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;Abfrage;Abfrageeditor;Abfrage-Editor;Abfrage-Editor;
solution: Experience Platform
title: Handbuch zu Query Service-Anmeldeinformationen
description: Der Abfrage-Service von Adobe Experience Platform bietet eine Benutzeroberfläche, über die Abfragen geschrieben und ausgeführt, zuvor ausgeführte Abfragen angezeigt und auf Abfragen zugegriffen werden kann, die von Benutzenden in Ihrem Unternehmen gespeichert wurden.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1975'
ht-degree: 6%

---

# Handbuch zu Anmeldedaten

Mit dem Abfrage-Service von Adobe Experience Platform können Sie eine Verbindung zu externen Clients herstellen. Sie können eine Verbindung zu diesen externen Clients herstellen, indem Sie entweder ablaufende oder nicht ablaufende Anmeldeinformationen verwenden.

>[!NOTE]
>
>Der Bereich für Anmeldedaten steht nicht automatisch allen Benutzenden zur Verfügung. Wenden Sie sich an Ihr Adobe-Accountteam , um bei Bedarf die Registerkarte &quot;[!UICONTROL Credentials]&quot; in den Arbeitsbereich „Abfrage-Service“ aufzunehmen. Auf Anforderung ist diese Änderung organisationsweit und wird vom Engineering-Team von Adobe durchgeführt. Es handelt sich nicht um eine von Benutzern gesteuerte Einstellung.

## Ablaufende Anmeldeinformationen {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="Client-SSL-Modus"
>abstract="In Clients, die mit dem Abfragedienst verbunden sind, muss SSL aktiviert sein. Stellen Sie sicher, dass der SSL-Modus auf „erforderlich“ eingestellt ist."

Sie können ablaufende Anmeldeinformationen verwenden, um schnell eine Verbindung zu einem externen Client herzustellen.

![Die Registerkarte „Anmeldeinformationen“ des Abfrage-Dashboards mit hervorgehobenem Abschnitt „Ablaufende Anmeldeinformationen“.](../images/ui/credentials/expiring-credentials.png)

Im Abschnitt **[!UICONTROL Expiring credentials]** finden Sie die folgenden Informationen:

- **[!UICONTROL Host]**: Der Name des Hosts, mit dem Ihr Client verbunden werden soll. Diese enthält den Namen Ihres Unternehmens, wie er im oberen Menüband der Experience Platform-Benutzeroberfläche zu sehen ist.
- **[!UICONTROL Port]**: Die Port-Nummer des Hosts, mit dem eine Verbindung hergestellt werden soll.
- **[!UICONTROL Database]**: Der Name der Datenbank, mit der ein Client verbunden werden soll.
- **[!UICONTROL Username]**: Der Benutzername, mit dem die Verbindung mit dem Abfrage-Service hergestellt wird.
- **[!UICONTROL Password]**: Das Kennwort für die Verbindung mit dem Abfrage-Service. Kennwörter in der Benutzeroberfläche wurden aus Sicherheitsgründen gehasht. Wählen Sie das Kopiersymbol (![Das Kopiersymbol.](/help/images/icons/copy.png)), um Ihre vollständigen, nicht gehashten Anmeldeinformationen in die Zwischenablage zu kopieren.
- **[!UICONTROL PSQL command]**: Ein Befehl, der automatisch alle relevanten Informationen für die Verbindung mit dem Abfrage-Service mithilfe von PSQL in der Befehlszeile eingefügt.
- **[!UICONTROL Expires]**: Ablaufdatum und -uhrzeit der ablaufenden Anmeldeinformationen. Die Standardgültigkeitsdauer des Tokens beträgt 24 Stunden, kann jedoch in den erweiterten Einstellungen der Admin Console geändert werden.

>[!TIP]
>
>Um die Sitzungsdauer für Ihre ablaufenden Anmeldedaten für die Verbindung zum Abfrage-Service zu ändern, navigieren Sie zu [Admin Console](https://adminconsole.adobe.com/) und wählen Sie die folgenden Optionen auf dem Bildschirm aus: **Einstellungen** > **Datenschutz und Sicherheit** > **Authentifizierungseinstellungen** > **Erweiterte Einstellungen** > **Max Sitzungsdauer**.
>
>![Die Registerkarte &quot;Admin Console-Einstellungen“ mit hervorgehobenen Optionen „Datenschutz und Sicherheit“, „Authentifizierungseinstellungen“ und „Maximale Sitzungsdauer“.](../images/ui/credentials/max-session-life.png)
>
>Weitere Informationen zu den von der Admin Console angebotenen [Erweiterten Einstellungen](https://helpx.adobe.com/enterprise/using/authentication-settings.html#advanced-settings) finden Sie in der Adobe-Hilfedokumentation.

### Verbinden mit Customer Journey Analytics-Daten in Abfragesitzungen {#connect-to-customer-journey-analytics}

Verwenden Sie die Customer Journey Analytics BI-Erweiterung mit Power BI oder Tableau, um mit SQL auf Ihre [Datenansichten](https://experienceleague.adobe.com/de/docs/analytics-platform/using/cja-dataviews/data-views) von Customer Journey Analytics zuzugreifen. Durch die Integration des Abfrage-Service mit der BI-Erweiterung können Sie direkt in den Sitzungen des Abfrage-Service auf Ihre Datenansichten zugreifen. Diese Integration optimiert die Funktionalität für BI-Tools, die den Abfrage-Service als PostgreSQL-Schnittstelle verwenden. Durch diese Funktion entfällt die Notwendigkeit, Datenansichten in BI-Tools zu duplizieren. Darüber hinaus wird ein plattformübergreifendes konsistentes Reporting sichergestellt und die Integration von Customer Journey Analytics-Daten mit anderen Quellen in BI-Plattformen vereinfacht.

In der Dokumentation erfahren Sie, wie Sie [Query Service mit einer Vielzahl von Desktop-Client-Anwendungen verbinden](../clients/overview.md) z. B. [Power BI](../clients/power-bi.md) oder [Tableau](../clients/tableau.md)

>[!IMPORTANT]
>
>Um diese Funktion verwenden zu können, sind ein Customer Journey Analytics Workspace-Projekt und eine Datenansicht erforderlich.

Um entweder in Power BI oder Tableau auf Ihre Customer Journey Analytics-Daten zuzugreifen, wählen Sie das Dropdown-Menü [!UICONTROL Database] und dann `prod:cja` aus den verfügbaren Optionen aus. Kopieren Sie als Nächstes Ihre [!DNL Postgres] Anmeldedaten-Parameter (Host, Port, Datenbank, Benutzername und andere) zur Verwendung in Ihrer Power BI- oder Tableau-Konfiguration.

![Die Registerkarte „Anmeldeinformationen für den Abfrage-Service“ mit hervorgehobenem Datenbank-Dropdown-Menü.](../images/ui/credentials/database-dropdown.png)

>[!NOTE]
>
>Wenn Sie Power BI oder Tableau mit Customer Journey Analytics verbinden, wird die Berechtigung „Gleichzeitige Sitzungen“ des Abfrage-Services genutzt. Wenn zusätzliche Sitzungen und Abfragen erforderlich sind, kann ein zusätzliches Add-on für das Benutzerpaket für Ad-hoc-Abfragen erworben werden, um fünf zusätzliche gleichzeitige Sitzungen und eine zusätzliche gleichzeitige Abfrage zu erhalten.

Sie können auf Ihre Customer Journey Analytics-Daten auch direkt über den Abfrage-Editor oder die Postgres-CLI zugreifen. Verweisen Sie dazu beim Schreiben Ihrer Abfrage auf die `cja`-Datenbank. Weitere Informationen zum Schreiben[ Ausführen und Speichern von Abfragen finden ](./user-guide.md#query-authoring) im Abfrage-Editor (Handbuch zur Abfrageerstellung).

Umfassende Anweisungen für den Zugriff auf [ Datenansichten mit SQL finden ](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/bi-extension) im Handbuch zur Customer Journey Analytics-Erweiterung .

## Unbefristete Anmeldedaten {#non-expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_migratenonexpiringcredentials"
>title="Migration zu OAuth-Server-zu-Server-Anmeldedaten"
>abstract="Diese Migration ist erforderlich, da die JWT-Anmeldedaten nach dem 30. Juni 2025 nicht mehr funktionieren. Der Vorgang dauert etwa 30–40 Sekunden und kann nach dem Start nicht mehr abgebrochen werden. Alle vorhandenen Vorgänge und Integrationen funktionieren nach der Migration weiterhin mit OAuth. Sie können diesen Bildschirm verlassen und jederzeit zurückkehren, um den Status zu überprüfen."

Sie können nicht ablaufende Anmeldeinformationen verwenden, um eine permanentere Verbindung zu einem externen Client herzustellen.

>[!IMPORTANT]
>
>Wenn Sie zum ersten Mal eine nicht ablaufende Berechtigung für OAuth Server-zu-Server erstellen oder migrieren, müssen Sie ein Systemadministratorkonto verwenden. Nur ein Systemadministrator kann diese Aktion für Ihre Organisation ausführen. Wenn ein Nicht-Systemadministrator bzw. eine Nicht-Systemadministratorin diesen Schritt versucht, schlägt der Prozess mit einem Autorisierungsfehler fehl. Nach der Ersteinrichtung können nachfolgende, nicht ablaufende Anmeldedaten von Benutzern mit den erforderlichen Berechtigungen erstellt oder migriert werden.

>[!NOTE]
>
>Für nicht ablaufende Zugangsdaten gelten die folgenden Einschränkungen:
>
>- Benutzer müssen sich mit ihrem Benutzernamen und Kennwort im Format `{technicalAccountId}:{credential}` anmelden. Weitere Informationen finden Sie im Abschnitt [Anmeldeinformationen generieren](#generate-credentials) .
>- Standardmäßig erhalten nicht ablaufende Anmeldeinformationen die Berechtigung, nur `SELECT` Abfragen auszuführen. Um `CTAS` oder `ITAS` Abfragen auszuführen, fügen Sie die Berechtigungen „Datensatz verwalten“ und „Schemata verwalten“ manuell zu der Rolle hinzu, die mit den nicht ablaufenden Anmeldedaten verknüpft ist. Die Berechtigung „Schemata verwalten“ befindet sich im Abschnitt „Datenmodellierung“ und die Berechtigung „Datensätze verwalten“ befindet sich im Abschnitt „Daten-Management“ der [Adobe Developer Console](https://developer.adobe.com/console/).
>- Die Leistung von Drittanbieter-Clients beim Auflisten von Abfrageobjekten kann anders als erwartet ausfallen. Beispielsweise zeigen einige Drittanbieter-Clients wie [!DNL DB Visualizer] den Ansichtsnamen nicht im linken Bereich an. Der Ansichtsname ist jedoch verfügbar, wenn er in einer `SELECT` Abfrage aufgerufen wird. Ebenso führen [!DNL PowerUI] möglicherweise die temporären Ansichten, die durch SQL zur Auswahl bei der Dashboard-Erstellung erstellt wurden, nicht auf.

### Voraussetzungen

Bevor Sie nicht ablaufende Zugangsdaten generieren können, müssen Sie die folgenden Schritte in Adobe Admin Console ausführen:

1. Melden Sie sich bei [Adobe Admin Console](https://adminconsole.adobe.com/) an und wählen Sie die entsprechende Organisation in der oberen Navigationsleiste aus.
2. [Produktprofil auswählen.](../../access-control/ui/browse.md)
3. [Konfigurieren Sie sowohl die **Sandboxes** als auch **Integration des Abfrage-** verwalten](../../access-control/ui/permissions.md) für das Produktprofil.
4. [Fügen Sie einen neuen Benutzer zu einem Produktprofil hinzu](../../access-control/ui/users.md) sodass er die konfigurierten Berechtigungen erhält.
5. [Fügen Sie den Benutzer als Produktprofil-Admin hinzu](https://helpx.adobe.com/de/enterprise/using/manage-product-profiles.html) um die Erstellung eines Kontos für ein beliebiges aktives Produktprofil zu ermöglichen.
6. [Fügen Sie den Benutzer als Produktprofil-Entwickler hinzu](https://helpx.adobe.com/de/enterprise/using/manage-developers.html) um eine Integration zu erstellen.

Nach diesen Schritten werden die erforderlichen Berechtigungen in [Adobe Developer Console](https://developer.adobe.com/console/) konfiguriert, damit Sie OAuth-Server-zu-Server-Anmeldeinformationen generieren und die Funktionen für ablaufende oder nicht ablaufende Anmeldeinformationen verwenden können.

Ausführliche Informationen zum Zuweisen von Berechtigungen finden Sie in der [Dokumentation zur Zugriffssteuerung](../../access-control/home.md).

### Anmeldedaten erstellen {#generate-credentials}

Um einen Satz nicht ablaufender Anmeldeinformationen zu erstellen, kehren Sie zur Experience Platform-Benutzeroberfläche zurück und wählen Sie in der linken Navigationsleiste **[!UICONTROL Queries]** aus, um auf den [!UICONTROL Queries] Workspace zuzugreifen. Wählen Sie als Nächstes die Registerkarte **[!UICONTROL Credentials]** und dann **[!UICONTROL Generate credentials]** aus.

![Das Dashboard „Abfragen“ mit hervorgehobener Registerkarte „Anmeldeinformationen“ und hervorgehobener Option „Anmeldeinformationen generieren“.](../images/ui/credentials/generate-credentials.png)

Es wird ein Dialogfeld angezeigt, in dem Sie Anmeldeinformationen generieren können. Um nicht ablaufende Zugangsdaten zu erstellen, müssen Sie die folgenden Details angeben:

- **[!UICONTROL Name]**: Der Name der Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Description]**: (Optional) Eine Beschreibung für die Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Assigned to]**: Der Benutzer, dem die Anmeldeinformationen zugewiesen werden. Dieser Wert sollte die E-Mail-Adresse des Benutzers sein, der die Anmeldeinformationen erstellt.
- **[!UICONTROL Password]** (Optional) Ein optionales Kennwort für Ihre Anmeldeinformationen. Wenn das Kennwort nicht festgelegt ist, generiert Adobe automatisch ein Kennwort für Sie.

Nachdem Sie alle erforderlichen Details angegeben haben, wählen Sie **[!UICONTROL Generate credentials]** aus, um Ihre Anmeldeinformationen zu generieren.

![Das Dialogfeld „Anmeldeinformationen generieren“ ist hervorgehoben.](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Wenn **[!UICONTROL Generate credentials]** ausgewählt ist, wird eine JSON-Konfigurationsdatei auf den lokalen Computer heruntergeladen. Da Adobe **generierten** nicht aufzeichnet, müssen Sie die heruntergeladene Datei sicher speichern und die Anmeldeinformationen aufzeichnen.
>
>Wenn die Anmeldeinformationen 90 Tage lang nicht verwendet werden, werden sie außerdem gelöscht.

Die JSON-Konfigurationsdatei enthält Informationen wie den Namen des technischen Kontos, die ID des technischen Kontos und die Anmeldeinformationen. Sie wird im folgenden Format bereitgestellt.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

Nachdem Sie die generierten Anmeldedaten gespeichert haben, klicken Sie auf **[!UICONTROL Close]**. Sie können jetzt eine Liste aller Ihrer nicht ablaufenden Anmeldedaten sehen.

![Die Registerkarte „Anmeldeinformationen“ des Abfrage-Dashboards mit hervorgehobenem Abschnitt „Nicht ablaufende Anmeldeinformationen“.](../images/ui/credentials/list-credentials.png)

Sie können Ihre nicht ablaufenden Anmeldedaten entweder bearbeiten oder löschen. Um nicht ablaufende Zugangsdaten zu bearbeiten, klicken Sie auf das Stiftsymbol (![Stiftsymbol).](/help/images/icons/edit.png)). Um nicht ablaufende Anmeldedaten zu löschen, klicken Sie auf das Löschsymbol (![Papierkorbsymbol.](/help/images/icons/delete.png)).

Beim Bearbeiten von nicht ablaufenden Zugangsdaten wird ein Modal angezeigt. Sie können die folgenden Details angeben, um zu aktualisieren:

- **[!UICONTROL Name]**: Der Name der Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Description]**: (Optional) Eine Beschreibung für die Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Assigned to]**: Der Benutzer, dem die Anmeldeinformationen zugewiesen werden. Dieser Wert sollte die E-Mail-Adresse des Benutzers sein, der die Anmeldeinformationen erstellt.

![Der Dialog Konto aktualisieren.](../images/ui/credentials/update-credentials.png)

Nachdem Sie alle erforderlichen Details angegeben haben, wählen Sie **[!UICONTROL Update account]** aus, um die Aktualisierung Ihrer Anmeldeinformationen abzuschließen.

### Migrieren von Anmeldeinformationen zu OAuth {#migrate-credentials}

Wenn Sie nicht ablaufende JWT-Anmeldeinformationen verwenden, müssen Sie jeden vor dem 30. Juni 2025 auf OAuth Server-zu-Server migrieren, um eine Unterbrechung des Services zu vermeiden.

>[!IMPORTANT]
>
>Die JWT-Anmeldeinformationen funktionieren nach dem 30. Juni 2025 nicht mehr. Sie müssen diese Migration manuell abschließen, um die Autorisierung beizubehalten.

Informationen zum Identifizieren der betroffenen Anmeldeinformationen und Abschließen der Migration finden Sie im [Handbuch zur Migration von JWT zu OAuth-Server-zu-Server-Anmeldeinformationen](./migrate-jwt-to-oauth.md).

Häufige Fragen finden Sie unter [Häufig gestellte Fragen zur Migration](./migrate-jwt-to-oauth.md#faq).

## Verwenden von Anmeldeinformationen zur Verbindung mit externen Clients {#use-credential-to-connect}

Sie können die ablaufenden oder nicht ablaufenden Anmeldeinformationen verwenden, um eine Verbindung mit externen Clients wie Aqua Data Studio, Looker oder Power BI herzustellen. Die Eingabemethode für diese Anmeldeinformationen variiert je nach externem Client. Spezifische Anweisungen zur Verwendung dieser Anmeldeinformationen finden Sie in der Dokumentation des externen Clients .

Die Abbildung zeigt den Speicherort der einzelnen Parameter in der Benutzeroberfläche mit Ausnahme des Kennworts der nicht ablaufenden Anmeldeinformationen an. Während nicht ablaufende Anmeldeinformationen von ihren JSON-Konfigurationsdateien bereitgestellt werden, können Sie Ihre ablaufenden Anmeldeinformationen auf der Registerkarte **Anmeldeinformationen** in der Benutzeroberfläche anzeigen.

![Die Registerkarte „Anmeldeinformationen“ des Arbeitsbereichs „Abfragen“ mit hervorgehobenem Abschnitt „Ablaufende Anmeldeinformationen“.](../images/ui/credentials/expiring-credentials.png)

In der folgenden Tabelle sind die Parameter aufgeführt, die normalerweise für die Verbindung mit externen Clients erforderlich sind.

>[!NOTE]
>
>Wenn Sie eine Verbindung zu einem Host mit nicht ablaufenden Anmeldeinformationen herstellen, ist es weiterhin erforderlich, alle im Abschnitt [!UICONTROL EXPIRING CREDENTIALS] aufgeführten Parameter mit Ausnahme des Kennworts und des Benutzernamens zu verwenden.
>>Das Format für die Eingabe Ihres Benutzernamens und Kennworts verwendet durch Doppelpunkt getrennte Werte, wie in diesem Beispiel `username:{your_username}` und `password:{password_string}` dargestellt.

| Parameter | Beschreibung | Beispiel |
|---|---|---|
| **Server/Host** | Der Name des Servers/Hosts, mit dem Sie eine Verbindung herstellen. <ul><li>Dieser Wert wird sowohl für ablaufende als auch für nicht ablaufende Anmeldeinformationen verwendet und hat die Form von `server.adobe.io`. Der Wert befindet sich unter **[!UICONTROL Host]** im [!UICONTROL EXPIRING CREDENTIALS].</ul></li> | `acme.platform.adobe.io` |
| **Port** | Der Port für den Server/Host, zu dem Sie eine Verbindung herstellen. <ul><li>Dieser Wert wird sowohl für ablaufende als auch für nicht ablaufende Anmeldeinformationen verwendet und befindet sich unter **[!UICONTROL Port]** im Abschnitt [!UICONTROL EXPIRING CREDENTIALS] .</ul></li> | `80` |
| **Datenbank** | Die Datenbank, mit der Sie eine Verbindung herstellen. <ul><li>Dieser Wert wird sowohl für ablaufende als auch für nicht ablaufende Anmeldeinformationen verwendet und befindet sich unter **[!UICONTROL Database]** im Abschnitt [!UICONTROL EXPIRING CREDENTIALS] . </ul></li> | `prod:all` |
| **Benutzername** | Der Benutzername für den Benutzer, der eine Verbindung zum externen Client herstellt. <ul><li>Dieser Wert wird sowohl für ablaufende als auch für nicht ablaufende Anmeldeinformationen verwendet. Sie hat die Form einer alphanumerischen Zeichenfolge vor der `@AdobeOrg`. Dieser Wert befindet sich unter **[!UICONTROL Username]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **Passwort** | Das Kennwort des Benutzers, der eine Verbindung zum externen Client herstellt. <ul><li>Wenn Sie ablaufende Anmeldeinformationen verwenden, finden Sie diese unter **[!UICONTROL Password]** im Abschnitt [!UICONTROL EXPIRING CREDENTIALS] .</li><li>Wenn Sie nicht ablaufende Anmeldeinformationen verwenden, ist dieser Wert die verketteten Argumente aus der TechnicalAccountID und die Anmeldeinformationen aus der JSON-Konfigurationsdatei. Der Kennwortwert hat folgende Form: `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>Ein ablaufendes Berechtigungskennwort umfasst mehr als tausend Zeichen alphanumerische Zeichenfolge. Es wird kein Beispiel gegeben.</li><li>Ein nicht ablaufendes Berechtigungskennwort lautet wie folgt:<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## Nächste Schritte

Nachdem Sie nun wissen, wie ablaufende und nicht ablaufende Anmeldedaten funktionieren, können Sie diese Anmeldedaten verwenden, um eine Verbindung zu externen Clients herzustellen. Ausführlichere Informationen zu externen Clients finden Sie im Handbuch [Verbinden von Clients mit dem Abfrage-Service](../clients/overview.md).
