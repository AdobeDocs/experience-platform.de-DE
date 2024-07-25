---
keywords: Experience Platform;Startseite;beliebte Themen;Abfrage-Service;Abfrage-Service;Abfrage;Abfrageeditor;Abfrage-Editor;Abfrage-Editor;
solution: Experience Platform
title: Anleitung zu Query Service-Anmeldedaten
description: Adobe Experience Platform Query Service bietet eine Benutzeroberfläche, mit der Sie Abfragen schreiben und ausführen, zuvor ausgeführte Abfragen anzeigen und auf Abfragen zugreifen können, die von Benutzern in Ihrer Organisation gespeichert wurden.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '1807'
ht-degree: 3%

---

# Handbuch zu Anmeldedaten

Mit Adobe Experience Platform Query Service können Sie eine Verbindung mit externen Clients herstellen. Sie können eine Verbindung zu diesen externen Clients herstellen, indem Sie entweder ablaufende oder nicht ablaufende Anmeldeinformationen verwenden.

>[!NOTE]
>
>Der Bereich für Anmeldedaten steht nicht automatisch allen Benutzenden zur Verfügung. Wenden Sie sich an Ihr Adobe-Account-Team, um bei Bedarf die Aufnahme der Registerkarte [!UICONTROL Anmeldedaten] in den Query Service-Arbeitsbereich anzufordern. Auf Wunsch wird diese Änderung organisationsweit durchgeführt und vom Adobe Engineering Team durchgeführt. Es handelt sich nicht um eine Einstellung, die von Benutzern gesteuert wird.

## Ablaufende Anmeldeinformationen {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="Client-SSL-Modus"
>abstract="In Clients, die mit dem Abfragedienst verbunden sind, muss SSL aktiviert sein. Stellen Sie sicher, dass der SSL-Modus auf „erforderlich“ eingestellt ist."

Sie können ablaufende Anmeldedaten verwenden, um schnell eine Verbindung zu einem externen Client herzustellen.

![Die Registerkarte &quot;Dashboard-Anmeldedaten für Abfragen&quot;, auf der der Abschnitt &quot;Ablaufberechtigungen&quot;hervorgehoben ist.](../images/ui/credentials/expiring-credentials.png)

Im Abschnitt **[!UICONTROL Ablaufberechtigungen]** finden Sie die folgenden Informationen:

- **[!UICONTROL Host]**: Der Name des Hosts, mit dem Ihr Client verbunden werden soll. Dies beinhaltet den Namen Ihres Unternehmens, der im oberen Band der Platform-Benutzeroberfläche angezeigt wird.
- **[!UICONTROL Port]**: Die Portnummer des Hosts, mit dem eine Verbindung hergestellt werden soll.
- **[!UICONTROL Datenbank]**: Der Name der Datenbank, mit der ein Client verbunden werden soll.
- **[!UICONTROL Benutzername]**: Der Benutzername, mit dem eine Verbindung zu Query Service hergestellt wird.
- **[!UICONTROL Kennwort]**: Das Kennwort für die Verbindung mit Query Service. Passwörter in der Benutzeroberfläche wurden aus Sicherheitsgründen gehasht. Wählen Sie das Kopiersymbol (![Kopiersymbol) aus.](/help/images/icons/copy.png)), um Ihre vollständigen, nicht gehashten Anmeldedaten in die Zwischenablage zu kopieren.
- **[!UICONTROL PSQL-Befehl]**: Ein Befehl, der automatisch alle relevanten Informationen eingefügt hat, damit Sie über PSQL über die Befehlszeile eine Verbindung zu Query Service herstellen können.
- **[!UICONTROL Läuft ab]**: Das Ablaufdatum und die Ablaufzeit für die ablaufenden Anmeldeinformationen. Die standardmäßige Gültigkeitsdauer des Tokens beträgt 24 Stunden. Sie kann jedoch in den erweiterten Einstellungen der Admin Console geändert werden.

>[!TIP]
>
>Um die Sitzungsdauer für die Verbindung Ihrer ablaufenden Anmeldedaten mit Query Service zu ändern, navigieren Sie zur Admin Console [1} und wählen Sie die folgenden Optionen auf dem Bildschirm aus: **Einstellungen** > **Datenschutz und Sicherheit** > **Authentifizierungseinstellungen** > **Erweiterte Einstellungen** > **Max. Sitzungsdauer**.](https://adminconsole.adobe.com/)
>
>![Die Registerkarte &quot;Admin Console settings&quot;mit den Einstellungen für Datenschutz und Sicherheit, Authentifizierungseinstellungen und maximaler Sitzungsdauer hervorgehoben.](../images/ui/credentials/max-session-life.png)
>
>Weitere Informationen zu den von der Admin Console bereitgestellten [erweiterten Einstellungen](https://helpx.adobe.com/enterprise/using/authentication-settings.html#advanced-settings) finden Sie in der Dokumentation zur Adobe-Hilfe .

### Verbindung zu Customer Journey Analytics-Daten in Abfragesitzungen herstellen {#connect-to-customer-journey-analytics}

Verwenden Sie die Customer Journey Analytics BI-Erweiterung mit Power BI oder Tableau, um auf Ihre Customer Journey Analytics [Datenansichten](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/data-views) mit SQL zuzugreifen. Durch die Integration von Query Service mit der BI-Erweiterung können Sie direkt in Query Service-Sitzungen auf Ihre Datenansichten zugreifen. Diese Integration optimiert die Funktionalität für BI-Tools, die Query Service als PostgreSQL-Schnittstelle verwenden. Dadurch entfällt die Notwendigkeit, Datenansichten in BI-Tools zu duplizieren, sorgt für eine plattformübergreifende konsistente Berichterstellung und vereinfacht die Integration von Customer Journey Analytics-Daten mit anderen Quellen in BI-Plattformen.

In der Dokumentation erfahren Sie, wie Sie [Query Service mit verschiedenen Desktop-Client-Anwendungen verbinden](../clients/overview.md), z. B. [Power BI](../clients/power-bi.md) oder [Tableau](../clients/tableau.md)

>[!IMPORTANT]
>
>Für die Verwendung dieser Funktion sind ein Customer Journey Analytics Workspace-Projekt und eine Datenansicht erforderlich.

Um auf Ihre Customer Journey Analytics-Daten in Power BI oder Tableau zuzugreifen, wählen Sie das Dropdown-Menü [!UICONTROL Datenbank] und dann `prod:cja` aus den verfügbaren Optionen aus. Kopieren Sie anschließend Ihre Parameter für [!DNL Postgres]-Anmeldedaten (Host, Port, Datenbank, Benutzername und andere) zur Verwendung in Ihrer Power BI- oder Tableau-Konfiguration.

![Die Registerkarte &quot;Anmeldeinformationen für Query Service&quot;mit dem Dropdown-Menü &quot;Datenbank&quot;.](../images/ui/credentials/database-dropdown.png)

>[!NOTE]
>
>Wenn Sie Power BI oder Tableau mit Customer Journey Analytics verbinden, wird die Berechtigung &quot;Gleichzeitige Sitzungen&quot;des Abfragedienstes genutzt. Wenn zusätzliche Sitzungen und Abfragen erforderlich sind, kann ein zusätzliches Ad-hoc-Abfragebenutzer-Pack-Add-on erworben werden, um fünf weitere gleichzeitige Sitzungen und eine zusätzliche gleichzeitige Abfrage zu erhalten.

Sie können auch direkt über den Abfrage-Editor oder die Postgres-CLI auf Ihre Customer Journey Analytics-Daten zugreifen. Referenzieren Sie dazu beim Schreiben Ihrer Abfrage die `cja` -Datenbank. Weitere Informationen zum Schreiben, Ausführen und Speichern von Abfragen finden Sie im Leitfaden zum Abfragen-Editor [Query Authoring](./user-guide.md#query-authoring) .

Vollständige Anweisungen zum Zugriff auf Ihre Customer Journey Analytics-Datenansichten mit SQL finden Sie im [BI-Erweiterungshandbuch](https://experienceleague.adobe.com/en/docs/analytics-platform/using/cja-dataviews/bi-extension) .

## Unbefristete Anmeldedaten {#non-expiring-credentials}

Sie können nicht ablaufende Anmeldedaten verwenden, um eine permanentere Verbindung zu einem externen Client einzurichten.

>[!NOTE]
>
>Für nicht ablaufende Anmeldedaten gelten die folgenden Einschränkungen:<br><ul><li>Benutzer müssen sich mit ihrem Benutzernamen und Kennwort, bestehend aus `{technicalAccountId}:{credential}`, anmelden. Weitere Informationen finden Sie im Abschnitt [Anmeldeinformationen generieren](#generate-credentials) .</li><li>Nach der Erstellung ablaufender Anmeldeinformationen wird eine neue Rolle mit grundlegenden Berechtigungen erstellt, die es Benutzern ermöglicht, Schemas und Datensätze anzuzeigen. Diese Rolle erhält auch die Berechtigung &quot;Abfragen verwalten&quot;zur Verwendung mit Query Service.</li><li>Bei der Auflistung von Abfrageobjekten kann es vorkommen, dass Clients von Drittanbietern eine andere Leistung als erwartet ausführen. Einige Clients von Drittanbietern wie [!DNL DB Visualizer] zeigen beispielsweise den Ansichtsnamen nicht im linken Bereich an. Der Ansichtsname ist jedoch verfügbar, wenn er in einer SELECT-Abfrage aufgerufen wird. Ebenso darf [!DNL PowerUI] die temporären Ansichten, die über die SQL erstellt wurden, nicht auflisten, um sie für die Dashboard-Erstellung auszuwählen.</li></ul>

### Voraussetzungen

Bevor Sie nicht ablaufende Anmeldeinformationen generieren können, müssen Sie die folgenden Schritte in Adobe Admin Console ausführen:

1. Melden Sie sich bei [Adobe Admin Console](https://adminconsole.adobe.com/) an und wählen Sie in der oberen Navigationsleiste die entsprechende Organisation aus.
2. [Wählen Sie ein Produktprofil aus.](../../access-control/ui/browse.md)
3. [Konfigurieren Sie sowohl die Berechtigungen **Sandboxes** als auch die Berechtigung **Query Service Integration verwalten**](../../access-control/ui/permissions.md) für das Produktprofil.
4. [Fügen Sie einem Produktprofil einen neuen Benutzer hinzu](../../access-control/ui/users.md), damit ihm die konfigurierten Berechtigungen erteilt werden.
5. [Fügen Sie den Benutzer als Produktprofiladministrator hinzu](https://helpx.adobe.com/de/enterprise/using/manage-product-profiles.html), um die Erstellung eines Kontos für jedes aktive Produktprofil zu ermöglichen.
6. [Fügen Sie den Benutzer als Produktprofilentwickler hinzu](https://helpx.adobe.com/de/enterprise/using/manage-developers.html), um eine Integration zu erstellen.

Weitere Informationen zum Zuweisen von Berechtigungen finden Sie in der Dokumentation zu [Zugriffskontrolle](../../access-control/home.md).

Alle erforderlichen Berechtigungen sind jetzt in Adobe Developer Console konfiguriert, damit der Benutzer die Funktion für ablaufende Anmeldedaten verwenden kann.

### Anmeldedaten erstellen {#generate-credentials}

Um einen Satz nicht ablaufender Anmeldedaten zu erstellen, kehren Sie zur Platform-Benutzeroberfläche zurück und wählen Sie im linken Navigationsbereich **[!UICONTROL Abfragen]** aus, um auf den Arbeitsbereich [!UICONTROL Abfragen] zuzugreifen. Wählen Sie als Nächstes die Registerkarte **[!UICONTROL Anmeldeinformationen]** und danach **[!UICONTROL Anmeldeinformationen generieren]** aus.

![Das Dashboard &quot;Abfragen&quot;mit der Registerkarte &quot;Anmeldeinformationen&quot;und hervorgehobenen &quot;Anmeldeinformationen generieren&quot;.](../images/ui/credentials/generate-credentials.png)

Es wird ein Dialogfeld angezeigt, in dem Sie Anmeldeinformationen generieren können. Um nicht ablaufende Anmeldedaten zu erstellen, müssen Sie die folgenden Details angeben:

- **[!UICONTROL Name]**: Der Name der Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Beschreibung]**: (Optional) Eine Beschreibung für die Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Zugeordneter Benutzer]**: Der Benutzer, dem die Anmeldeinformationen zugewiesen werden. Dieser Wert sollte die E-Mail-Adresse des Benutzers sein, der die Anmeldeinformationen erstellt.
- **[!UICONTROL Kennwort]** (Optional) Ein optionales Kennwort für Ihre Anmeldedaten. Wenn das Kennwort nicht festgelegt ist, generiert Adobe automatisch ein Kennwort für Sie.

Nachdem Sie alle erforderlichen Details angegeben haben, wählen Sie **[!UICONTROL Anmeldeinformationen generieren]** aus, um Ihre Anmeldeinformationen zu generieren.

![Das Dialogfeld &quot;Anmeldeinformationen generieren&quot;ist hervorgehoben.](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Wenn **[!UICONTROL Anmeldeinformationen generieren]** ausgewählt ist, wird eine JSON-Konfigurationsdatei auf Ihren lokalen Computer heruntergeladen. Da Adobe die generierten Anmeldeinformationen **nicht** aufzeichnet, müssen Sie die heruntergeladene Datei sicher speichern und einen Datensatz mit den Anmeldedaten speichern.
>
>Wenn die Anmeldeinformationen 90 Tage lang nicht verwendet werden, werden die Anmeldeinformationen ebenfalls gelöscht.

Die JSON-Konfigurationsdatei enthält Informationen wie den Namen des technischen Kontos, die technische Konto-ID und die Anmeldedaten. Sie wird im folgenden Format bereitgestellt.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

Nachdem Sie die generierten Anmeldeinformationen gespeichert haben, wählen Sie **[!UICONTROL Schließen]** aus. Sie können jetzt eine Liste aller nicht ablaufenden Anmeldedaten anzeigen.

![Die Registerkarte &quot;Dashboard-Anmeldedaten für Abfragen&quot;, auf der der Abschnitt &quot;Nicht ablaufende Anmeldedaten&quot;hervorgehoben ist.](../images/ui/credentials/list-credentials.png)

Sie können Ihre nicht ablaufenden Anmeldedaten entweder bearbeiten oder löschen. Um eine nicht ablaufende Berechtigung zu bearbeiten, wählen Sie das Stiftsymbol (![Stiftsymbol) aus.](/help/images/icons/edit.png)). Um eine nicht ablaufende Berechtigung zu löschen, wählen Sie das Löschsymbol (![Papierkorbsymbol.](/help/images/icons/delete.png)).

Beim Bearbeiten einer nicht ablaufenden Berechtigung wird ein Modal angezeigt. Sie können die folgenden Details zur Aktualisierung angeben:

- **[!UICONTROL Name]**: Der Name der Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Beschreibung]**: (Optional) Eine Beschreibung für die Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Zugeordneter Benutzer]**: Der Benutzer, dem die Anmeldeinformationen zugewiesen werden. Dieser Wert sollte die E-Mail-Adresse des Benutzers sein, der die Anmeldeinformationen erstellt.

![Das Dialogfeld Konto aktualisieren.](../images/ui/credentials/update-credentials.png)

Nachdem Sie alle erforderlichen Details angegeben haben, wählen Sie **[!UICONTROL Konto aktualisieren]** aus, um die Aktualisierung Ihrer Anmeldedaten abzuschließen.

## Verwenden Sie Anmeldeinformationen, um eine Verbindung zu externen Clients herzustellen. {#use-credential-to-connect}

Sie können die ablaufenden oder nicht ablaufenden Anmeldedaten verwenden, um eine Verbindung mit externen Clients wie Aqua Data Studio, Looker oder Power BI herzustellen. Die Eingabemethode für diese Anmeldeinformationen variiert je nach externem Client. Spezifische Anweisungen zur Verwendung dieser Anmeldeinformationen finden Sie in der Dokumentation des externen Kunden.

Das Bild zeigt den Speicherort der einzelnen Parameter in der Benutzeroberfläche an, mit Ausnahme des Kennworts der nicht ablaufenden Anmeldeinformationen. Während nicht ablaufende Anmeldedaten von ihren JSON-Konfigurationsdateien bereitgestellt werden, können Sie Ihre ablaufenden Anmeldedaten auf der Registerkarte **Anmeldedaten** in der Benutzeroberfläche anzeigen.

![Die Registerkarte &quot;Anmeldeinformationen des Arbeitsbereichs &quot;Abfragen&quot;, auf der der Abschnitt Ablaufberechtigungen hervorgehoben ist.](../images/ui/credentials/expiring-credentials.png)

In der folgenden Tabelle sind die Parameter aufgeführt, die normalerweise für die Verbindung mit externen Clients erforderlich sind.

>[!NOTE]
>
>Beim Herstellen einer Verbindung zu einem Host mit nicht ablaufenden Anmeldeinformationen müssen weiterhin alle im Abschnitt [!UICONTROL EXPIRING CREDENTIALS] aufgelisteten Parameter verwendet werden, mit Ausnahme des Kennworts und des Benutzernamens.
>Das Format für die Eingabe Ihres Benutzernamens und Kennworts verwendet durch Doppelpunkte getrennte Werte, wie in diesem Beispiel `username:{your_username}` und `password:{password_string}` dargestellt.

| Parameter | Beschreibung | Beispiel |
|---|---|---|
| **Server/Host** | Der Name des Servers/Hosts, mit dem Sie eine Verbindung herstellen. <ul><li>Dieser Wert wird sowohl für ablaufende als auch nicht ablaufende Anmeldeinformationen verwendet und hat die Form &quot;`server.adobe.io`&quot;. Der Wert befindet sich unter **[!UICONTROL Host]** im Abschnitt [!UICONTROL EXPIRING CREDENTIALS] .</ul></li> | `acme.platform.adobe.io` |
| **Port** | Der Anschluss für den Server/Host, mit dem Sie eine Verbindung herstellen. <ul><li>Dieser Wert wird sowohl für ablaufende als auch für nicht ablaufende Anmeldeinformationen verwendet und befindet sich unter **[!UICONTROL Port]** im Abschnitt [!UICONTROL EXPIRING CREDENTIALS] .</ul></li> | `80` |
| **Datenbank** | Die Datenbank, mit der Sie eine Verbindung herstellen. <ul><li>Dieser Wert wird sowohl für ablaufende als auch für nicht ablaufende Anmeldeinformationen verwendet und befindet sich unter **[!UICONTROL Datenbank]** im Abschnitt [!UICONTROL EXPIRING CREDENTIALS] . </ul></li> | `prod:all` |
| **Benutzername** | Der Benutzername für den Benutzer, der eine Verbindung zum externen Client herstellt. <ul><li>Dieser Wert wird sowohl für ablaufende als auch für nicht ablaufende Anmeldeinformationen verwendet. Sie hat die Form einer alphanumerischen Zeichenfolge vor `@AdobeOrg`. Dieser Wert befindet sich unter **[!UICONTROL Benutzername]**.</li></ul> | `ECBB80245ECFC73E8A095EC9@AdobeOrg` |
| **Passwort** | Das Kennwort für den Benutzer, der eine Verbindung zum externen Client herstellt. <ul><li>Wenn Sie ablaufende Anmeldeinformationen verwenden, finden Sie dies unter **[!UICONTROL Kennwort]** im Abschnitt [!UICONTROL EXPIRING CREDENTIALS] .</li><li>Wenn Sie nicht ablaufende Anmeldeinformationen verwenden, ist dieser Wert die verketteten Argumente aus der technicalAccountID und die Berechtigung aus der JSON-Konfigurationsdatei. Der Kennwortwert hat das folgende Format: `{technicalAccountId}:{credential}`.</li></ul> | <ul><li>Ein ablaufendes Berechtigungskennwort ist mehr als tausend Zeichen eine alphanumerische Zeichenfolge. Es wird kein Beispiel gegeben.</li><li>Ein nicht ablaufendes Berechtigungskennwort lautet wie folgt:<br>`4F2611B8613DK3670V495N55:3d182fa9e0b54f33a7881305c06203ee`</li></ul> |

{style="table-layout:auto"}

## Nächste Schritte

Nachdem Sie nun wissen, wie ablaufende und nicht ablaufende Anmeldeinformationen funktionieren, können Sie diese Anmeldeinformationen verwenden, um eine Verbindung zu externen Clients herzustellen. Weitere Informationen zu externen Clients finden Sie im Handbuch [Clients mit Query Service verbinden](../clients/overview.md).
