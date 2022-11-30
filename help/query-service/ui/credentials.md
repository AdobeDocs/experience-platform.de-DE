---
keywords: Experience Platform; Startseite; beliebte Themen; Abfragedienst; Query Service; Abfrage; Abfrageeditor; Abfrage-Editor; Abfrage-Editor;
solution: Experience Platform
title: Anleitung zu Query Service-Anmeldedaten
topic-legacy: guide
description: Adobe Experience Platform Query Service bietet eine Benutzeroberfläche, über die Abfragen geschrieben und ausgeführt, zuvor ausgeführte Abfragen angezeigt und auf Abfragen zugegriffen werden kann, die von Benutzern in Ihrer IMS-Organisation gespeichert wurden.
exl-id: ea25fa32-809c-429c-b855-fcee5ee31b3e
source-git-commit: 344602a0e828d140ea386daf30a25b8f595f8d04
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 2%

---

# Handbuch zu Anmeldeinformationen

Mit Adobe Experience Platform Query Service können Sie eine Verbindung mit externen Clients herstellen. Sie können eine Verbindung zu diesen externen Clients herstellen, indem Sie entweder ablaufende oder nicht ablaufende Anmeldeinformationen verwenden.

## Ablaufberechtigungen {#expiring-credentials}

>[!CONTEXTUALHELP]
>id="platform_queryservice_credentials_expiringcredentials"
>title="SSL-Modus des Kunden"
>abstract="SSL muss in Clients aktiviert sein, die mit Query Service verbunden sind. Stellen Sie sicher, dass der SSL-Modus auf &quot;erforderlich&quot;eingestellt ist."

Sie können ablaufende Anmeldedaten verwenden, um schnell eine Verbindung zu einem externen Client herzustellen.

![Die Registerkarte &quot;Dashboard-Anmeldedaten für Abfragen&quot;mit dem Abschnitt Ablaufberechtigungen wurde hervorgehoben.](../images/ui/credentials/expiring-credentials.png)

Die **[!UICONTROL Ablaufberechtigungen]** enthält die folgenden Informationen:

- **[!UICONTROL Host]**: Der Name des Hosts, mit dem Sie eine Verbindung herstellen möchten. Für die Verbindung mit Query Service enthält dies den Namen der IMS-Organisation, die Sie derzeit verwenden.
- **[!UICONTROL Port]**: Die Anschlussnummer des Hosts, mit dem Sie eine Verbindung herstellen möchten.
- **[!UICONTROL Datenbank]**: Der Name der Datenbank, mit der Sie eine Verbindung herstellen möchten.
- **[!UICONTROL Benutzername]**: Der Benutzername, mit dem Sie eine Verbindung zu Query Service herstellen.
- **[!UICONTROL Passwort]**: Das Kennwort, mit dem Sie eine Verbindung zu Query Service herstellen.
- **[!UICONTROL PSQL-Befehl]**: Ein Befehl, der automatisch alle relevanten Informationen eingefügt hat, damit Sie über PSQL über die Befehlszeile eine Verbindung zu Query Service herstellen können.
- **[!UICONTROL Läuft ab]**: Das Ablaufdatum für die ablaufenden Anmeldeinformationen. Die Anmeldeinformationen laufen 24 Stunden nach ihrer Erstellung ab.

## Nicht ablaufende Anmeldeinformationen {#non-expiring-credentials}

Sie können nicht ablaufende Anmeldedaten verwenden, um eine permanentere Verbindung zu einem externen Client einzurichten.

### Voraussetzungen

Bevor Sie nicht ablaufende Anmeldeinformationen generieren können, müssen Sie die folgenden Schritte in Adobe Admin Console ausführen:

1. Anmelden [Adobe Admin Console](https://adminconsole.adobe.com/) und wählen Sie in der oberen Navigationsleiste die entsprechende Organisation aus.
2. [Produktprofil auswählen.](../../access-control/ui/browse.md)
3. [Konfigurieren Sie beide **Sandboxes** und **Integration von Query Service verwalten** Berechtigungen](../../access-control/ui/permissions.md) für das Produktprofil.
4. [Neuen Benutzer zu einem Produktprofil hinzufügen](../../access-control/ui/users.md) so erhalten sie die konfigurierten Berechtigungen.
5. [Benutzer als Produktprofiladministrator hinzufügen](https://helpx.adobe.com/de/enterprise/using/manage-product-profiles.html) , um die Erstellung eines Kontos für jedes aktive Produktprofil zu ermöglichen.
6. [Benutzer als Produktprofilentwickler hinzufügen](https://helpx.adobe.com/de/enterprise/using/manage-developers.html) , um eine Integration zu erstellen.

Weitere Informationen zum Zuweisen von Berechtigungen finden Sie in der Dokumentation unter [Zugriffskontrolle](../../access-control/home.md).

Alle erforderlichen Berechtigungen werden jetzt in der Adobe Developer Console konfiguriert, damit der Benutzer die Funktion für ablaufende Anmeldedaten verwenden kann.

### Anmeldeinformationen generieren

Um einen Satz nicht ablaufender Anmeldedaten zu erstellen, kehren Sie zur Platform-Benutzeroberfläche zurück und wählen Sie **[!UICONTROL Abfragen]** über die linke Navigationsleiste auf [!UICONTROL Abfragen] Arbeitsbereich. Wählen Sie als Nächstes die **[!UICONTROL Anmeldeinformationen]** Tab gefolgt von **[!UICONTROL Anmeldeinformationen generieren]**.

![Das Dashboard Abfragen mit der Registerkarte Anmeldedaten und hervorgehobenen Anmeldeinformationen generieren .](../images/ui/credentials/generate-credentials.png)

Es wird ein Dialogfeld angezeigt, in dem Sie Anmeldeinformationen generieren können. Um nicht ablaufende Anmeldedaten zu erstellen, müssen Sie die folgenden Details angeben:

- **[!UICONTROL Name]**: Der Name der Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Beschreibung]**: (Optional) Eine Beschreibung für die Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Zugeordnet zu]**: Der Benutzer, dem die Anmeldeinformationen zugewiesen werden. Dieser Wert sollte die E-Mail-Adresse des Benutzers sein, der die Anmeldeinformationen erstellt.
- **[!UICONTROL Passwort]** (Optional) Ein optionales Kennwort für Ihre Anmeldedaten. Wenn das Kennwort nicht festgelegt ist, generiert Adobe automatisch ein Kennwort für Sie.

Nachdem Sie alle erforderlichen Details angegeben haben, wählen Sie **[!UICONTROL Anmeldeinformationen generieren]** , um Ihre Anmeldedaten zu generieren.

![Das Dialogfeld Anmeldeinformationen generieren wird hervorgehoben.](../images/ui/credentials/create-account.png)

>[!IMPORTANT]
>
>Wann **[!UICONTROL Anmeldeinformationen generieren]** ausgewählt ist, wird eine JSON-Konfigurationsdatei auf Ihren lokalen Computer heruntergeladen. Da Adobe **not** die generierten Anmeldedaten aufzeichnen, müssen Sie die heruntergeladene Datei sicher speichern und die Anmeldedaten speichern.
>
>Wenn die Anmeldeinformationen 90 Tage lang nicht verwendet werden, werden die Anmeldeinformationen ebenfalls gelöscht.

Die JSON-Konfigurationsdatei enthält Informationen wie den Namen des technischen Kontos, die technische Konto-ID und die Anmeldedaten. Sie wird im folgenden Format bereitgestellt.

```json
{"technicalAccountName":"9F0A21EE-B8F3-4165-9871-846D3C8BC49E@TECHACCT.ADOBE.COM","credential":"3d184fa9e0b94f33a7781905c05203ee","technicalAccountId":"4F2611B8613AA3670A495E55"}
```

Nachdem Sie die generierten Anmeldeinformationen gespeichert haben, wählen Sie **[!UICONTROL Schließen]**. Sie können jetzt eine Liste aller nicht ablaufenden Anmeldedaten anzeigen.

![Die Registerkarte &quot;Fragen-Dashboard-Anmeldedaten&quot;mit dem Abschnitt Nicht ablaufende Anmeldedaten wurde hervorgehoben.](../images/ui/credentials/list-credentials.png)

Sie können Ihre nicht ablaufenden Anmeldedaten entweder bearbeiten oder löschen. Um eine nicht ablaufende Berechtigung zu bearbeiten, wählen Sie das Stiftsymbol (![Ein Bleistiftsymbol.](../images/ui/credentials/edit-icon.png)). Um eine nicht ablaufende Berechtigung zu löschen, wählen Sie das Löschsymbol (![Ein Papierkorbsymbol.](../images/ui/credentials/delete-icon.png)).

Beim Bearbeiten einer nicht ablaufenden Berechtigung wird ein Modal angezeigt. Sie können die folgenden Details zur Aktualisierung angeben:

- **[!UICONTROL Name]**: Der Name der Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Beschreibung]**: (Optional) Eine Beschreibung für die Anmeldeinformationen, die Sie generieren.
- **[!UICONTROL Zugeordnet zu]**: Der Benutzer, dem die Anmeldeinformationen zugewiesen werden. Dieser Wert sollte die E-Mail-Adresse des Benutzers sein, der die Anmeldeinformationen erstellt.

![Das Dialogfeld Konto aktualisieren .](../images/ui/credentials/update-credentials.png)

Nachdem Sie alle erforderlichen Details angegeben haben, wählen Sie **[!UICONTROL Konto aktualisieren]** , um die Aktualisierung Ihrer Anmeldedaten abzuschließen.

## Verwenden Sie Anmeldeinformationen, um eine Verbindung zu externen Clients herzustellen. {#use-credential-to-connect}

Sie können die ablaufenden oder nicht ablaufenden Anmeldedaten verwenden, um eine Verbindung mit externen Clients wie Aqua Data Studio, Looker oder Power BI herzustellen. Die Eingabemethode für diese Anmeldeinformationen variiert je nach externem Client. Spezifische Anweisungen zur Verwendung dieser Anmeldeinformationen finden Sie in der Dokumentation des externen Kunden.

Das Bild zeigt den Speicherort der einzelnen Parameter in der Benutzeroberfläche an, mit Ausnahme des Kennworts der nicht ablaufenden Anmeldeinformationen. Während nicht ablaufende Anmeldeinformationen von ihren JSON-Konfigurationsdateien bereitgestellt werden, können Sie Ihre ablaufenden Anmeldeinformationen unter der **Anmeldeinformationen** in der Benutzeroberfläche.

![Die Registerkarte &quot;Query Workspace Credentials&quot;mit dem Abschnitt Expending credentials wurde hervorgehoben.](../images/ui/credentials/expiring-credentials.png)

In der folgenden Tabelle sind die Parameter aufgeführt, die normalerweise für die Verbindung mit externen Clients erforderlich sind.

>[!NOTE]
>
>Bei der Verbindung zu einem Host mit nicht ablaufenden Anmeldeinformationen müssen weiterhin alle in der [!UICONTROL LAUFENDE ANMELDEDATEN] mit Ausnahme des Passworts und des Benutzernamens.
>Das Format für die Eingabe Ihres Benutzernamen und Kennworts verwendet durch Doppelpunkte getrennte Werte, wie in diesem Beispiel gezeigt `username:{your_username}` und `password:{password_string}`.

| Parameter | Beschreibung |
|---|---|
| **Server/Host** | Der Name des Servers/Hosts, mit dem Sie eine Verbindung herstellen. <ul><li>Dieser Wert wird sowohl für ablaufende als auch nicht ablaufende Anmeldeinformationen verwendet und hat die Form `server.adobe.io`. Der Wert befindet sich unter **[!UICONTROL Host]** im [!UICONTROL LAUFENDE ANMELDEDATEN] Abschnitt.</ul></li> |
| **Port** | Der Anschluss für den Server/Host, mit dem Sie eine Verbindung herstellen. <ul><li>Dieser Wert wird sowohl für ablaufende als auch für nicht ablaufende Anmeldeinformationen verwendet und befindet sich unter **[!UICONTROL Port]** im [!UICONTROL LAUFENDE ANMELDEDATEN] Abschnitt. Ein Beispielwert für den Port wäre `80`.</ul></li> |
| **Datenbank** | Die Datenbank, mit der Sie eine Verbindung herstellen. <ul><li>Dieser Wert wird sowohl für ablaufende als auch nicht ablaufende Anmeldeinformationen verwendet und befindet sich unter **[!UICONTROL Datenbank]** im [!UICONTROL LAUFENDE ANMELDEDATEN] Abschnitt. Ein Beispielwert für die Datenbank wäre `prod:all`.</ul></li> |
| **Benutzername** | Der Benutzername für den Benutzer, der eine Verbindung zum externen Client herstellt. <ul><li>Dieser Wert wird sowohl für ablaufende als auch für nicht ablaufende Anmeldeinformationen verwendet. Sie hat die Form einer alphanumerischen Zeichenfolge, bevor `@AdobeOrg`. Dieser Wert befindet sich unter **[!UICONTROL Benutzername]**.</li></ul> |
| **Passwort** | Das Kennwort für den Benutzer, der eine Verbindung zum externen Client herstellt. <ul><li>Wenn Sie ablaufende Anmeldeinformationen verwenden, finden Sie dies unter **[!UICONTROL Passwort]** innerhalb der [!UICONTROL LAUFENDE ANMELDEDATEN] Abschnitt.</li><li>Wenn Sie nicht ablaufende Anmeldeinformationen verwenden, ist dieser Wert die verketteten Argumente aus der technicalAccountID und die Berechtigung aus der JSON-Konfigurationsdatei. Der Kennwortwert hat folgende Form: `{technicalAccountId}:{credential}`.</li></ul> |

## Nächste Schritte

Nachdem Sie nun wissen, wie ablaufende und nicht ablaufende Anmeldeinformationen funktionieren, können Sie diese Anmeldeinformationen verwenden, um eine Verbindung zu externen Clients herzustellen. Weitere Informationen zu externen Clients finden Sie im Abschnitt [Anleitung zum Verbinden von Clients mit Query Service](../clients/overview.md).
