---
title: Verbinden von GitHub-Copilot und Visual Studio-Code mit Query Service
description: Erfahren Sie, wie Sie GitHub-Copilot und Visual Studio-Code mit Adobe Experience Platform Query Service verbinden.
source-git-commit: f0c5b311721497bf2a14ca49dc5f1c9653e85efc
workflow-type: tm+mt
source-wordcount: '1366'
ht-degree: 2%

---

# Verbinden von [!DNL GitHub Copilot] und [!DNL Visual Studio Code] mit Query Service

>[!IMPORTANT]
>
>Bevor Sie dieses integrierte Tool verwenden, müssen Sie wissen, welche Daten für GitHub freigegeben werden. Zu den freigegebenen Daten gehören kontextbezogene Informationen über den Code und die Dateien, die bearbeitet werden (&quot;Aufforderungen&quot;), sowie Details zu Benutzeraktionen (&quot;Benutzerinteraktionsdaten&quot;).  Lesen Sie die Datenschutzanweisung von [[!DNL GitHub Copilot]](https://docs.github.com/en/site-policy/privacy-policies/github-general-privacy-statement#github-privacy-statement) , um mehr über die erfassten Daten zu erfahren. Sie müssen auch die Sicherheitsauswirkungen der Einbeziehung von Drittanbieterdiensten berücksichtigen, da Sie dafür verantwortlich sind, die Einhaltung der Data Governance-Richtlinien Ihres Unternehmens sicherzustellen. Adobe ist nicht für datenbezogene Bedenken oder Probleme verantwortlich, die sich aus der Verwendung dieses Tools ergeben können. Weitere Informationen finden Sie in der GitHub-Dokumentation .

[!DNL GitHub Copilot], basierend auf OpenAI Codex, ist ein KI-gesteuertes Tool, das Ihre Kodierungserfahrung verbessert, indem Code-Snippets und komplette Funktionen direkt in Ihrem Editor vorgeschlagen werden. Durch die Integration von [!DNL Visual Studio Code] ([!DNL VS Code]) kann [!DNL Copilot] den Workflow erheblich beschleunigen, insbesondere bei der Arbeit mit komplexen Abfragen. In diesem Handbuch erfahren Sie, wie Sie [!DNL GitHub Copilot] und [!DNL VS Code] mit dem Query Service verbinden, um Ihre Abfragen effizienter zu schreiben und zu verwalten. Weitere Informationen zu [!DNL Copilot] finden Sie auf der [GitHub-Copilot-Produktseite](https://github.com/pricing) und in der [offiziellen [!DNL Copilot] Dokumentation](https://docs.github.com/en/copilot/about-github-copilot/what-is-github-copilot).

In diesem Dokument werden die Schritte beschrieben, die zum Verbinden von [!DNL GitHub Copilot] und [!DNL VS Code] mit dem Adobe Experience Platform Query Service erforderlich sind.

## Erste Schritte {#get-started}

Für dieses Handbuch müssen Sie bereits Zugriff auf ein GitHub-Konto haben und sich für [!DNL GitHub Copilot] angemeldet haben. Sie können [sich von der GitHub-Website aus anmelden](https://github.com/github-copilot/signup). Sie benötigen auch [!DNL VS Code]. Sie können [  [!DNL VS Code] von ihrer offiziellen Website herunterladen](https://code.visualstudio.com/download).

Nachdem Sie [!DNL VS Code] installiert und Ihr [!DNL Copilot] -Abonnement aktiviert haben, erwerben Sie Ihre Anmeldedaten für die Verbindung zu Experience Platform. Diese Anmeldeinformationen befinden sich auf der Registerkarte [!UICONTROL Anmeldeinformationen] im Arbeitsbereich [!UICONTROL Abfragen] der Platform-Benutzeroberfläche. Lesen Sie das Handbuch mit Anmeldeinformationen zu [erfahren Sie, wie Sie diese Werte in der Platform-Benutzeroberfläche finden](../ui/credentials.md). Wenden Sie sich an Ihren Organisationsadministrator, wenn Sie derzeit keinen Zugriff auf den Arbeitsbereich [!UICONTROL Abfragen] haben.

### Erforderliche [!DNL Visual Studio Code] Erweiterungen {#required-extensions}

Die folgenden [!DNL Visual Studio Code] -Erweiterungen sind erforderlich, um Ihre Platform SQL-Datenbanken direkt im Code-Editor zu verwalten und abzufragen. Laden Sie diese Erweiterungen herunter und installieren Sie sie.

- [SQLTools](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools): Verwenden Sie die SQLTools-Erweiterung, um mehrere SQL-Datenbanken zu verwalten und abzufragen. Es enthält Funktionen wie einen Abfrage-Runner, SQL-Formatierer und Verbindungsexplorer mit Unterstützung für zusätzliche Treiber zur Steigerung der Entwicklerproduktivität. Weitere Informationen finden Sie in der Übersicht zu Visual Studio Marketplace .
- [SQLTools PostgreSQL/Cockroach Driver](https://marketplace.visualstudio.com/items?itemName=mtxr.sqltools-driver-pg): Mit dieser Erweiterung können Sie PostgreSQL- und CockroachDB-Datenbanken direkt in Ihrem Code-Editor verbinden, abfragen und verwalten.

Die nächsten Erweiterungen aktivieren [!DNL GitHub Copilot] und die Chat-Funktionen.

- [[!DNL GitHub Copilot]](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot): Bietet Vorschläge zur Inline-Codierung während der Eingabe.
- [[!DNL GitHub Copilot] Chat](https://marketplace.visualstudio.com/items?itemName=GitHub.copilot-chat): Eine begleitende Erweiterung, die kommunikative KI-Unterstützung bietet.

## Verbindung erstellen {#create-connection}

Wählen Sie das Zylindersymbol (![Das Zylindersymbol) aus.](../images/clients/github-copilot/cylinder-icon.png)) im linken Navigationsbereich von [!DNL VS Code], gefolgt von **[!DNL Add New Connection]** oder dem Zylinderplus-Symbol (![Das Zylinderplus-Symbol.](../images/clients/github-copilot/cylinder-plus-icon.png)).

![Die Visual Studio-Code-Benutzeroberfläche mit der SQL Tool-Erweiterung und der hervorgehobenen Option Neue Verbindung hinzufügen.](../images/clients/github-copilot/add-new-connection.png)

Der **[!DNL Connection Assistant]** wird angezeigt. Wählen Sie den Datenbanktreiber **[!DNL PostgreSQL]** aus.

![Die SQLTools-Einstellungsseite in [!DNL VS Code] mit PostgreSQl hervorgehoben.](../images/clients/github-copilot/postgres-database-driver.png)

### Einstellungen für die Eingabeverbindung {#input-connection-settings}

Die Ansicht [!DNL Connection Settings] wird angezeigt. Geben Sie Ihre Anmeldedaten für die Verbindung mit Platform in die entsprechenden Felder von SQLTools [!DNL Connection Assistant] ein. Die erforderlichen Werte werden in der folgenden Tabelle erläutert.

| Eigenschaft | Beschreibung |
| --- |--- |
| [!DNL Connection name] | Geben Sie einen &quot;[!DNL Connection name]&quot; wie `Prod_MySQL_Server` an, der beschreibend ist und den Zweck klar angibt (z. B. eine Produktionsumgebung für einen MySQL-Server). Zu den Best Practices gehören:<br><ul><li>Befolgen Sie die Benennungskonventionen Ihres Unternehmens, um sicherzustellen, dass es innerhalb des Systems eindeutig ist.</li><li>Halten Sie es kurz, um Klarheit zu erhalten und Verwirrung mit anderen Verbindungen zu vermeiden.</li><li>Schließen Sie relevante Details zur Funktion oder Umgebung der Verbindung in den Namen ein.</li></ul> |
| [!DNL Connect using] | Verwenden Sie die Option &quot;**[!DNL Server and Port]**&quot;, um die Adresse des Servers (Hostname) und die Portnummer anzugeben, um eine direkte Verbindung zu Platform herzustellen. |
| [!DNL Server address] | Geben Sie den Wert **[!UICONTROL Host]** ein, der in Ihren Platform Postgres-Anmeldedaten angegeben ist, z. B. `acmeprod.platform-query.adobe.io`. |
| [!DNL Port] | Dieser Wert ist normalerweise `80` für Platform-Dienste. |
| [!DNL Database] | Geben Sie den Wert **[!UICONTROL Database]** ein, der in Ihren Platform Postgres-Anmeldedaten angegeben ist, z. B. `prod:all`. |
| [!DNL Username] | Diese Eigenschaft bezieht sich auf Ihre Organisations-ID. Geben Sie den Wert **[!UICONTROL Benutzername]** ein, der in Ihren Platform Postgres-Anmeldedaten angegeben ist. |
| [!DNL Password] | Diese Eigenschaft ist Ihr Zugriffstoken. Geben Sie den Wert **[!UICONTROL Kennwort]** ein, der in Ihren Platform Postgres-Anmeldedaten angegeben ist. |

![Der Arbeitsbereich &quot;Verbindungsassistent&quot;mit mehreren hervorgehobenen Einstellungen.](../images/clients/github-copilot/connection-settings.png)

Wählen Sie als Nächstes **[!DNL Use Password]** und danach **[!DNL Save as plaintext in settings]** aus dem angezeigten Dropdown-Menü aus. Das Feld [!DNL Password] wird angezeigt. Verwenden Sie dieses Texteingabefeld, um Ihr Zugriffstoken einzugeben.

![Das Feld Kennwort verwenden, sein Dropdown-Menü und Kennwort wurden hervorgehoben.](../images/clients/github-copilot/access-token.png)

Um SSL zu aktivieren, wählen Sie abschließend das Eingabefeld [!DNL SSL] aus und dann im angezeigten Dropdown-Menü die Option [!DNL Enabled].

![Das SSL-Feld mit &quot;Aktiviert&quot;im Dropdown-Menü wurde hervorgehoben.](../images/clients/github-copilot/ssl-enabled.png)

>[!TIP]
>
>Nachdem Sie alle Anmeldedaten eingegeben haben, können Sie Ihre Verbindung testen, bevor Sie die Verbindung speichern. Scrollen Sie nach unten zum unteren Rand des Arbeitsbereichs und wählen Sie **[!DNL Test Connection]** aus.
>
>![Der Arbeitsbereich Verbindungsassistent mit hervorgehobener Testverbindung.](../images/clients/github-copilot/test-connection.png " Der Arbeitsbereich &quot;Verbindungsassistent&quot;mit hervorgehobener Testverbindung."){width="100" zoomable="yes"}

Nachdem Sie die Verbindungsdetails korrekt eingegeben haben, wählen Sie **[!DNL Save Connection]** aus, um Ihre Einstellungen zu bestätigen.

![Der Arbeitsbereich &quot;Verbindungsassistent&quot;mit hervorgehobener Option &quot;Verbindung speichern&quot;.](../images/clients/github-copilot/save-connection.png)

Die Ansicht [!DNL Review connection details] wird angezeigt und zeigt Ihre Anmeldedaten für die Verbindung an. Wenn Sie sicher sind, dass Ihre Verbindungsdetails korrekt sind, wählen Sie **[!DNL Connect Now]** aus.

![Die Ansicht &quot;Überprüfen der Verbindungsdetails&quot;mit &quot;Connect Now&quot;wurde hervorgehoben.](../images/clients/github-copilot/review-and-connect.png)

Ihr [!DNL VS Code]-Arbeitsbereich wird mit einem Vorschlag von [!DNL GitHub Copilot] angezeigt.

![Eine verbundene SQL-Sitzung in [!DNL VS Code].](../images/clients/github-copilot/connected.png)

## [!DNL GitHub Copilot] Kurzanleitung

Sobald Sie mit Ihrer Platform-Instanz verbunden sind, können Sie [!DNL Copilot] als KI-Kodierungs-Assistent verwenden, um Code schneller und sicherer zu schreiben. In diesem Abschnitt werden die wichtigsten Funktionen und deren Verwendung beschrieben.

## Erste Schritte mit [!DNL GitHub Copilot] {#get-started-with-copilot}

Stellen Sie zunächst sicher, dass Sie die neueste Version von [!DNL VS Code] installiert haben. Eine veraltete [!DNL VS Code] -Version kann verhindern, dass wichtige [!DNL Copilot]-Funktionen wie gewünscht funktionieren. Stellen Sie als Nächstes sicher, dass die Einstellung [!DNL Enable Auto Completions] aktiviert ist. Wenn [!DNL Copilot] ordnungsgemäß ausgeführt wird, wird das **[!DNL Copilot]-Symbol** (![Das Copilot-Symbol](../images/clients/github-copilot/copilot-icon.png)) in Ihrer Statusleiste angezeigt (bei Auftreten eines Problems wird stattdessen das Fehlersymbol [!DNL Copilot] angezeigt). Wählen Sie das Symbol **[!DNL Copilot]** aus, um das Menü [!DNL [!DNL GitHub Copilot] zu öffnen. Wählen Sie **[!DNL [!DNL GitHub Copilot] Menu]** **[!DNL Edit Settings]** aus.

![Der [!DNL VS Code]-Editor mit dem angezeigten [!DNL GitHub Copilot Menu] und dem [!DNL Copilot]-Symbol und hervorgehobenen Einstellungen bearbeiten](../images/clients/github-copilot/github-copilot-menu.png).

Scrollen Sie nach unten zu den Optionen und stellen Sie sicher, dass das Kontrollkästchen für die Einstellung [!DNL Enable Auto Completions] aktiviert ist.

![Das Einstellungsbedienfeld für [!DNL GitHub Copilot] mit aktiviertem Kontrollkästchen &quot;Automatische Vervollständigung aktivieren&quot;.](../images/clients/github-copilot/enable-auto-completions.png)

## Codeabschlüsse {#code-completions}

Nachdem Sie die Erweiterung [!DNL GitHub Copilot] installiert und sich angemeldet haben, wird automatisch eine Funktion mit dem Namen **Ghost Text** aktiviert, die auf Codeabschlüsse bei der Eingabe hinweist. Diese Vorschläge helfen Ihnen, Code effizienter und mit weniger Unterbrechungen zu schreiben. Sie können auch Kommentare verwenden, um die KI-Codevorschläge zu leiten. Das bedeutet, dass nicht-technische Benutzer einfache Sprache in Code konvertieren können, um ihre Daten zu untersuchen.

![Die VSCode-Benutzeroberfläche mit einem Codevorschlag und das [!DNL GitHub Copilot]-Symbol hervorgehoben.](../images/clients/github-copilot/ghost-text.png)

>[!TIP]
>
>Wenn Sie [!DNL Copilot] für eine bestimmte Datei oder Sprache deaktivieren möchten, wählen Sie das Symbol in der Statusleiste aus und deaktivieren Sie es.

### Vollständige oder teilweise Ghost-Textvorschläge akzeptieren {#accept-suggestions}

Wenn [!DNL GitHub Copilot] Codeabschlüsse vorschlägt, können Sie entweder partielle oder vollständige Vorschläge akzeptieren. Wählen Sie **Tab** aus, um den gesamten Vorschlag zu akzeptieren, oder halten Sie die Taste **Strg (oder Befehl bei Mac)** gedrückt und drücken Sie die Taste **Nach-rechts-Taste**, um Teiltext zu akzeptieren. Um einen Vorschlag zu schließen, drücken Sie **Escape**.

>[!TIP]
>  
>Wenn Sie keine Vorschläge erhalten, stellen Sie sicher, dass [[!DNL Copilot] in der Sprache Ihrer Datei](#get-started-with-copilot) aktiviert ist.

![ Der [!DNL VS Code]-Editor, der einen schwachen grauen Textvorschlag von [!DNL GitHub Copilot] als Geistertext neben dem teilweise eingegebenen Code anzeigt.](../images/clients/github-copilot/accept-partial-suggestions.png)

### Alternative Vorschläge {#alternative-suggestions}

Um alternative Codevorschläge zu durchlaufen, wählen Sie die Pfeile im Dialogfeld [!DNL Copilot] aus.

![ Der [!DNL VS Code]-Editor, der den Bereich Alternative Vorschläge für Copilot anzeigt.](../images/clients/github-copilot/code-suggestions.png)


## Inline-Chat verwenden {#inline-chat}

Sie können auch mit [!DNL Copilot] direkt über Ihren Code chatten. Verwenden Sie **Strg (oder Befehl) + I** , um das Inline-Chat-Dialogfeld Trigger. Diese Funktion wird verwendet, um Ihren Code zu iterieren und Vorschläge im Kontext zu verfeinern. Sie können einen Codeblock markieren und Inline-Chat verwenden, um eine andere Lösung zu sehen, die von der KI vorgeschlagen wurde, bevor Sie sie akzeptieren.

![Das Inline-Chat-Fenster mit Diff-Ansicht](../images/clients/github-copilot/inline-chat.png)

<!-- THis section is poss unnecessary:
There are inline features for chat including doc, expalin, fix and test
![fix, document, explain](../images/clients/github-copilot/fix-document-explain.png)
 -->

## Dedizierte Chat-Ansicht {#dedicated-chat}

Sie können eine herkömmlichere Chat-Oberfläche mit einer dedizierten Chat-Seitenleiste verwenden, um Ideen und Strategien zu entwickeln, Kodierungsprobleme zu lösen und Implementierungsdetails zu besprechen. Wählen Sie das Chat-Symbol (![Das Symbol Chat kopieren .](../images/clients/github-copilot/chat-icon.png)) in der [!DNL VS Code] Seitenleiste, um ein dediziertes Chat-Fenster zu öffnen.

![Die [!DNL GitHub Copilot] Chat-Seitenleiste mit hervorgehobenem Chat-Symbol.](../images/clients/github-copilot/chat-sidebar.png)

Sie können auch auf den Chat-Verlauf zugreifen, indem Sie das Verlaufssymbol (![Verlaufssymbol ) auswählen.](../images/clients/github-copilot/history-icon.png)) am oberen Rand des Chat-Bedienfelds.

## Nächste Schritte

Jetzt können Sie Ihre Platform-Datenbanken effizient direkt über Ihren Code-Editor abfragen und die KI-gestützten Codevorschläge von [!DNL GitHub Copilot] verwenden, um das Schreiben und die Optimierung von SQL-Abfragen zu optimieren. Weiterführende Informationen zum Schreiben und Ausführen von Abfragen finden Sie in der [Anleitung zur Ausführung von Abfragen](../best-practices/writing-queries.md).
