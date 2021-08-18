---
title: Hochladen und Implementieren von End-to-End-Tests für eine Erweiterung
description: Erfahren Sie, wie Sie Ihre Erweiterung in Adobe Experience Platform validieren, hochladen und testen können.
source-git-commit: 41a394974153883dc300bdd8a00fc3106c4f0ac6
workflow-type: tm+mt
source-wordcount: '2392'
ht-degree: 35%

---

# Hochladen und Implementieren von End-to-End-Tests

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Verwenden Sie zum Testen von Tag-Erweiterungen in Adobe Experience Platform die Tags-API und/oder die Befehlszeilen-Tools, um Ihre Erweiterungspakete hochzuladen. Verwenden Sie anschließend die Datenerfassungs-Benutzeroberfläche, um Ihr Erweiterungspaket in einer Eigenschaft zu installieren und seine Funktionen in einer Tag-Bibliothek und einem Build zu nutzen.

In diesem Dokument wird beschrieben, wie Sie End-to-End-Tests für Ihre Erweiterung implementieren.

>[!NOTE]
>
>In diesem Handbuch wird davon ausgegangen, dass Sie macOS mit installiertem und verfügbarem Node.js und npm verwenden.

## Validieren der Erweiterung {#validate}

Sobald Ihr Team mit der Leistung Ihrer Erweiterung und den Ergebnissen im Tool [Sandbox](https://www.npmjs.com/package/@adobe/reactor-sandbox#running-the-sandbox) zufrieden ist, sollten Sie bereit sein, Ihr Erweiterungspaket auf Tags hochzuladen.

Überprüfen Sie vor dem Hochladen, ob die erforderlichen Felder oder Einstellungen vorhanden sind. Beispielsweise empfiehlt es sich, das [Erweiterungsmanifest](../manifest.md), die [Erweiterungskonfiguration](../configuration.md), die [Ansichten](../web/views.md) und die [Bibliotheksmodule](../web/format.md) (mindestens) zu überprüfen.

Ein konkretes Beispiel ist Ihre Logodatei: Fügen Sie die Zeile `"iconPath": "example.svg",` der Datei `extension.json` hinzu und binden Sie diese Logo-Grafikdatei in Ihr Projekt ein. Dies ist der relative Pfad zum Symbol, das für die Erweiterung angezeigt wird. Er darf nicht mit einem Schrägstrich beginnen. Er muss auf eine SVG-Datei mit der Erweiterung `.svg` verweisen. Die SVG sollte normal angezeigt werden, wenn sie quadratisch dargestellt wird, und kann durch die Benutzeroberfläche skaliert werden. Weitere Informationen finden Sie im Artikel [Skalieren von SVG](https://css-tricks.com/scale-svg/) .

>[!NOTE]
>
>Für öffentliche Erweiterungen fügen Sie in Ihre Datei `extension.json` ein Element mit einem Link zu Ihrem Exchange-Listeneintrag ein. Ihr [Erweiterungsmanifest](../manifest.md) sollte einen Eintrag wie den folgenden enthalten: `"exchangeUrl":"https://www.adobeexchange.com/experiencecloud.details.12345.html"`, der auf die URL Ihrer Exchange-Auflistung verweist.

## Erstellen einer Adobe I/O-Integration {#integration}

Um die API oder die Befehlszeilen-Tools verwenden zu können, benötigen Sie ein technisches Konto bei Adobe I/O. Sie müssen das technische Konto in der I/O-Konsole erstellen und dann das Uploader-Tool verwenden, um das Erweiterungspaket hochzuladen.

Informationen zum Erstellen eines technischen Kontos für die Verwendung mit Tags in Adobe Experience Platform finden Sie im Handbuch [Zugriffstoken](https://developer.adobelaunch.com/api/guides/access_tokens/) .

>[!IMPORTANT]
>
>Um eine Integration in Adobe I/O erstellen zu können, müssen Sie Experience Cloud-Organisationsadministrator oder Experience Cloud-Organisationsentwickler sein.

Wenn Sie keine Integration erstellen können, verfügen Sie wahrscheinlich nicht über die richtigen Berechtigungen. Dazu muss entweder ein Org-Admin die Schritte für Sie durchführen oder Sie als Entwickler zuweisen.

## Hochladen des Erweiterungspakets {#upload}

Nachdem Sie nun über Anmeldeinformationen verfügen, können Sie Ihr Erweiterungspaket durchgängig testen.

Wenn Sie das Erweiterungspaket zum ersten Mal hochladen, wird ihm der Status `development` zugewiesen. Dies bedeutet, dass sie nur für Ihre eigene Organisation sichtbar ist und nur mit einer Eigenschaft, die für die Erweiterungsentwicklung markiert wurde.

Verwenden Sie die Befehlszeile, um den folgenden Befehl in dem Ordner auszuführen, der Ihr ZIP-Paket enthält.

```bash
npx @adobe/reactor-uploader
```

`npx` ermöglicht Ihnen, ein npm-Paket herunterzuladen und auszuführen, ohne es tatsächlich auf Ihrem Computer zu installieren. Dies ist die einfachste Möglichkeit, Uploader auszuführen.

Für den Uploader müssen Sie mehrere Informationen eingeben. Die technische Konto-ID, der API-Schlüssel und andere Informationen können über die Adobe I/O-Konsole abgerufen werden. Navigieren Sie in der I/O-Konsole zur Seite [Integrationen](https://console.adobe.io/integrations). Wählen Sie die richtige Organisation aus der Dropdown-Liste aus, suchen Sie die richtige Integration und wählen Sie **[!UICONTROL Ansicht]** aus.

- Wie lautet der Pfad zu Ihrem privaten Schlüssel? /path/to/private.key. Dies ist der Ort, an dem Sie in Schritt 2 oben Ihren privaten Schlüssel gespeichert haben.
- Wie lautet Ihre Organisations-ID? Kopieren Sie diese aus der Übersichtsseite der I/O-Konsole , die Sie zuvor geöffnet haben, und fügen Sie sie ein.
- Wie lautet die ID Ihres technischen Kontos? Kopieren Sie sie und fügen Sie sie aus der I/O-Konsole ein.
- Wie lautet Ihr API-Schlüssel? Kopieren Sie sie und fügen Sie sie aus der I/O-Konsole ein.
- Was ist das Client-Geheimnis? Kopieren Sie sie und fügen Sie sie aus der I/O-Konsole ein.
- Wie lautet der Pfad des Pakets extension_package, das Sie hochladen möchten? /path/to/extension_package.zip. Wenn Sie Uploader aus dem Verzeichnis heraus aufrufen, das Ihr ZIP-Paket enthält, können Sie dies einfach aus der Liste auswählen, anstatt den Pfad einzugeben.

Das Erweiterungspaket wird dann hochgeladen und Uploader gibt die ID des extension_package aus.

>[!NOTE]
>
>Beim Hochladen oder Patchen werden Erweiterungspakete in einen ausstehenden Status versetzt, während das System das Paket asynchron extrahiert und bereitstellt. Während dieses Vorgangs können Sie die `extension_package`-ID mithilfe der API und in der Datenerfassungs-Benutzeroberfläche nach ihrem Status abfragen. Im Katalog wird eine Erweiterungskarte angezeigt, die als Ausstehend markiert ist.

>[!NOTE]
>
>Wenn Sie Uploader oft ausführen möchten, kann es umständlich sein, diese Informationen jedes Mal einzugeben. Sie können diese auch als Argumente aus der Befehlszeile übergeben. Weitere Informationen finden Sie im Abschnitt [Befehlszeilenargumente](https://www.npmjs.com/package/@adobe/reactor-uploader#command-line-arguments) der NPM-Dokumentation.

## Erstellen einer Entwicklungseigenschaft {#property}

Nachdem Sie sich bei der Datenerfassungs-Benutzeroberfläche angemeldet haben, wird der Bildschirm Eigenschaften angezeigt. Eine Eigenschaft ist ein Container für die Tags, die Sie bereitstellen möchten, und kann auf einer oder mehreren Sites verwendet werden.

![](../images/getting-started/properties-screen.png)

Bei der ersten Anmeldung werden auf Ihrem Bildschirm keine Eigenschaften angezeigt. Klicken Sie auf **Neue Eigenschaft**, um eine Eigenschaft zu erstellen. Geben Sie einen Namen und eine URL ein. Verwenden Sie die URL Ihrer Test-Site oder die Seite, auf der Sie Ihre Erweiterung testen werden. Dieses Domänenfeld kann von einigen Erweiterungen oder von einer Bedingung mithilfe der Haupterweiterung verwendet werden.

>[!NOTE]
>
>`localhost` funktioniert nicht als URL-Wert. Verwenden Sie stattdessen einen beliebigen Nachverfolgungswert zum Testen, wenn Sie eine `localhost`-URL verwenden. Beispiel: example.com.

Um diese Eigenschaft für Entwicklungstests für Erweiterungen zu verwenden, müssen Sie die OPTIONS **ADVANCED** erweitern und das Kontrollkästchen für **Für Erweiterungsentwicklung konfigurieren** aktivieren.

![](../images/getting-started/launch-create-a-dev-property.png)

Wählen Sie unten **Speichern** aus, um Ihre neue Eigenschaft zu speichern.

Der Bildschirm Eigenschaften wird angezeigt. Wählen Sie den Namen der soeben erstellten Eigenschaft aus. Der Bildschirm Eigenschaftsübersicht wird angezeigt. Es enthält Links zu jedem Bereich des Systems mit den globalen Navigationslinks in der Spalte.

## Installieren der Erweiterung {#install-extension}

Um Ihre Erweiterung in dieser Eigenschaft zu installieren, wählen Sie den Link **Erweiterungen** in den Hauptnavigationslinks in der linken Spalte aus. Die Erweiterung **Core** wird auf dem Bildschirm **Installierte** angezeigt. Die Haupterweiterung enthält alle Tag-Management-Funktionen innerhalb der Datenerfassung.

![](../images/getting-started/extensions.png)

Um Ihre Erweiterung hinzuzufügen, wählen Sie die Registerkarte **Katalog** aus.

![](../images/getting-started/catalog.png)

Im Katalog werden Kartensymbole für alle verfügbaren Erweiterungen angezeigt. Wenn Ihre Erweiterung nicht im Katalog angezeigt wird, vergewissern Sie sich, dass Sie die oben beschriebenen Schritte in den Abschnitten Einrichten der Adobe Administration Console und Erstellen Ihres Erweiterungspakets ausgeführt haben. Ihr Erweiterungspaket wird möglicherweise auch als &quot;Ausstehend&quot;angezeigt, wenn Platform die Erstverarbeitung nicht abgeschlossen hat.

Wenn Sie die vorherigen Schritte ausgeführt haben und immer noch kein Erweiterungspaket vom Typ Ausstehend oder Fehlgeschlagen im Katalog angezeigt wird, sollten Sie den Status Ihres Erweiterungspakets direkt mithilfe der API überprüfen. Informationen zum Ausführen des entsprechenden API-Aufrufs finden Sie unter [Abrufen eines ExtensionPackage](https://developer.adobelaunch.com/api/reference/1.0/extension_packages/fetch/) in der API-Dokumentation.

Nachdem das Erweiterungspaket fertig verarbeitet wurde, wählen Sie **Installieren** unten auf der Karte aus.

![](../images/getting-started/install-extension.png)

Der Konfigurationsbildschirm wird geöffnet (sofern die Erweiterung einen hat). Fügen Sie alle zum Konfigurieren der Erweiterung erforderlichen Informationen hinzu und klicken Sie auf **Speichern** am unteren Rand. Das hier dargestellte Konfigurationsbildschirm verwendet die Facebook-Erweiterung, für die eine Pixel-ID erforderlich ist.

![](../images/getting-started/fb-extension.png)

Jetzt sollte unter „Erweiterungen“ der Bildschirm **Installierte** mit der Erweiterung „Core“ und Ihrer Erweiterung angezeigt werden.

![](../images/getting-started/extension-installed.png)

## Erstellen von Ressourcen zum Testen der Erweiterung {#resources}

Erweiterungen bieten neue Funktionen für Benutzer von Adobe Experience Platform. Diese werden normalerweise in Datenelementen oder im Regel-Builder angezeigt.

### Datenelemente

Tag-Datenelemente sollen Benutzern dabei helfen, Werte beizubehalten. Jedes Datenelement ist eine Zuordnung zu Quelldaten oder ein Zeiger auf Quelldaten. Ein einzelnes Datenelement ist eine Variable, die Abfragezeichenfolgen, URLs, Cookie-Werten, JavaScript-Variablen usw. zugeordnet werden kann. Wählen Sie **Datenelemente** aus der linken Navigationsleiste und **Neues Datenelement erstellen**.

![](../images/getting-started/data-element-create-new-link.png)

Erweiterungen können Datenelementtypen definieren, wenn dies für die Funktion der Erweiterung erforderlich ist oder um den Benutzern die Arbeit zu erleichtern. Wenn eine Erweiterung Datenelementtypen bereitstellt, werden diese in einer Dropdown-Liste für Benutzer auf dem Bildschirm **Datenelement erstellen** angezeigt:

![](../images/getting-started/create-data-element.png)

Wenn ein Benutzer Ihre Erweiterung aus der Dropdown-Liste **Erweiterung** auswählt, wird die Dropdown-Liste **Datenelementtyp** mit allen von Ihrer Erweiterung bereitgestellten Datenelementtypen gefüllt. Der Benutzer kann dann jedes Datenelement seinem Quellwert zuordnen. Datenelemente können beim Erstellen von Regeln im Ereignis zur Änderung von Datenelementen (Data Element Change Event) oder im Ereignis für benutzerspezifischen Code (Custom Code Event) verwendet werden, um die Ausführung einer Regel auszulösen. Ein Datenelement kann auch in der Datenelementbedingung oder anderen Bedingungen, Ausnahmen oder Aktionen in einer Regel verwendet werden.

Nachdem das Datenelement erstellt worden ist (die Zuordnung eingerichtet wurde), können Benutzer einfach über einen Verweis auf das Datenelement auf die Quelldaten verweisen. Wenn sich die Quelle des Werts ändert (Site-Umgestaltungen usw.), -Benutzer müssen die Zuordnung nur einmal in der Datenerfassungs-Benutzeroberfläche aktualisieren. Alle Datenelemente erhalten dann automatisch den neuen Quellwert.

### Regeln

Wählen Sie im linken Navigationsbereich den Link **Regeln** und dann **Neue Regel erstellen**.

![](../images/getting-started/rules-link.png)

Geben Sie zunächst einen beschreibenden Namen für die Regel ein. Der Bildschirm **Regel erstellen** ist wie eine `if-then` -Anweisung eingerichtet.

![](../images/getting-started/create-new-rule.png)

Wenn ein Ereignis auftritt, Bedingungen übergeben werden und keine Ausnahmen vorliegen, wird die Aktion ausgelöst. Derselbe Ablauf gilt für Erweiterungen, in denen Sie Ereignis, Bedingungen, Ausnahmen, Datenelemente oder Aktionen erstellen oder verwenden können.

Fügen Sie mithilfe des Beispiels für die Facebook-Erweiterung bei jedem Laden einer Seite auf der Test-Site ein Ereignis hinzu.

![](../images/getting-started/load-event.png)

Der `Window Loaded` **Ereignistyp** stellt sicher, dass diese Regel jedes Mal ausgelöst wird, wenn eine Seite auf der Test-Site geladen wird. Wählen Sie **Änderungen beibehalten** aus. Ignorieren Sie für dieses Beispiel **Bedingungen** , da die Regel für jede Seite der Test-Site ausgelöst werden sollte.

Wählen Sie unter **ACTIONS** **Add** aus. Der Bildschirm **Aktionskonfiguration** wird angezeigt. Als Nächstes müssen Sie die Erweiterung auswählen, auf die die Regel angewendet werden soll, und die Aktion, die ausgeführt werden soll, wenn die Regel ausgelöst wird. Wählen Sie **Facebook Pixel** aus der Dropdownliste **Erweiterung** und **Seitenansicht senden** aus der Dropdownliste **Aktionstyp** aus. Wählen Sie **Keep Changes** und dann **Save** im folgenden Bildschirm **Regel bearbeiten**.

![](../images/getting-started/action-configuration.png)

Wählen Sie beim Testen Ihrer Erweiterung alle relevanten Ereignisse, Bedingungen usw. aus. in einer beliebigen Anzahl von Regeln auswählen.

## Veröffentlichen der Änderungen {#publish}

Klicken Sie im Hauptnavigationsmenü auf **Publishing** und dann auf den Link **Neue Bibliothek hinzufügen**:

![](../images/getting-started/add-new-library.png)

Eine Bibliothek enthält eine Reihe von Anweisungen dafür, wie Erweiterungen, Datenelemente und Regeln miteinander und mit einer Website interagieren. Bibliotheken werden in Builds kompiliert. Eine Bibliothek kann so viele Änderungen enthalten, wie ein Benutzer gleichzeitig durchführen oder testen kann.

Fügen Sie auf dem Bildschirm **Bibliothek erstellen** einen Namen in das Textfeld **Name** ein. Tags bieten eine standardmäßige Entwicklungsumgebung mit dem Namen **Entwicklung**. Wählen Sie **Entwicklung** aus der Dropdown-Liste **Umgebung** aus. Fügen Sie zur Einfachheit alle verfügbaren Ressourcen hinzu. Wählen Sie **Alle geänderten Ressourcen hinzufügen** und dann **Speichern** aus.

>[!NOTE]
>
>Wenn Sie einer Bibliothek eine Ressource hinzufügen, wird eine aktuelle Momentaufnahme dieser Ressource erstellt und der Bibliothek hinzugefügt. Wenn Sie später Änderungen an den Ressourcen vornehmen (z. B. aufgrund von notwendigen Korrekturen), müssen Sie die Bibliothek ebenfalls aktualisieren, um die neuesten Änderungen an den Ressourcen aufzunehmen. Die Schaltfläche **Add All Changed Resources** ist auch zu diesem Zweck nützlich.

![](../images/getting-started/create-new-library.png)

Nachdem alle Änderungen in die neu erstellte Bibliothek aufgenommen wurden (im angegebenen Beispiel **dev** genannt), wählen Sie **Speichern und in Entwicklung erstellen** aus.

![](../images/getting-started/build-for-dev.png)

Nach Abschluss des Build-Prozesses wird neben dem Bibliotheksnamen ein grüner Indikator **success** angezeigt.

![](../images/getting-started/successful-build.png)

Die Tag-Bibliothek ist jetzt veröffentlicht und zur Verwendung verfügbar. Die Testseite muss die neu erstellte Bibliothek verwenden, um das Seitenverhalten für den Endbenutzer in einem Browser zu testen.

## Installieren von Tags auf einer Test-Site {#install-data-collection-tags}

Installationsanweisungen finden Sie auf der Registerkarte Umgebungen . Auf dieser Seite werden alle verfügbaren Umgebungen angezeigt und Sie können auch weitere Umgebungen erstellen. Da die Bibliothek in der Entwicklungsumgebung veröffentlicht wurde, wählen Sie das Kästchensymbol in der Spalte **INSTALL** in der Zeile **Entwicklung** aus.

![](../images/getting-started/launch-installation-instructions.png)

Das Dialogfeld **Web Install Instructions** für die Entwicklungsumgebung wird angezeigt. Wählen Sie das Kopiersymbol aus, um das gesamte Tag `<script>` zu kopieren.

![](../images/getting-started/launch-installation-instructions-dialogue.png)

Schließen Sie die Installation ab, indem Sie dieses einzelne Tag `<script>` in den Abschnitt `<head>` Ihres Dokuments oder Ihrer Site-Vorlage einfügen. Besuchen Sie als Nächstes die Test-Site, um das Verhalten Ihrer veröffentlichten Tag-Bibliothek zu untersuchen.

## Test {#test}

Im Folgenden finden Sie eine Liste mit hilfreichen Konsolenbefehlen zum Überprüfen Ihrer Erweiterung auf Ihrer Testseite oder Site.

- `_satellite.setDebug(true);` aktiviert den Debug-Modus und gibt nützliche Protokollierungsanweisungen an die Konsole aus.
- Das `_satellite._container`-Objekt enthält nützliche Informationen zur bereitgestellten Bibliothek, einschließlich Details zum Build, den enthaltenen Datenelementen, Regeln und Erweiterungen.

Ziel dieser Tests ist es, die Funktionalität der bereitgestellten Bibliothek zu überprüfen und sicherzustellen, dass sich das Erweiterungspaket wie erwartet verhält, nachdem es in einer Bibliothek erfüllt wurde.

Wenn Sie feststellen, dass Sie Änderungen an Ihrem Erweiterungspaket vornehmen müssen, ähnelt der Iterationsvorgang dem Entwicklungsprozess.

1. Vornehmen von Änderungen am Code des Projekts.
1. Validieren der Änderungen mit dem Sandbox-Tool.
1. Erstellen eines neuen ZIP-Pakets mit dem Packager-Tool
1. Verwenden Sie das Uploader-Tool, um Ihr neues ZIP-Paket hochzuladen. Der Prozess folgt hinsichtlich des ersten Uploads denselben Anweisungen wie zuvor. Sie werden jedoch feststellen, dass dieses neue Paket die ältere Version überschreibt, anstatt eine neue zu erstellen, da es bereits ein Erweiterungspaket mit diesem Namen im Entwicklungsmodus gibt.

   >[!NOTE]
   >
   >Argumente können an die Befehlszeile übergeben werden, um Zeit zu sparen, indem die wiederholte Eingabe von Anmeldeinformationen vermieden wird. Weitere Informationen hierzu finden Sie in der [reactor-uploader-Dokumentation](https://www.npmjs.com/package/@adobe/reactor-uploader).
1. Der Installationsschritt kann beim Aktualisieren eines vorhandenen Pakets übersprungen werden.
1. Ändern von Ressourcen: Wenn die Konfiguration für eine Ihrer Erweiterungskomponenten geändert wurde, müssen Sie diese Ressourcen in der Benutzeroberfläche für die Datenerfassung aktualisieren.
1. Hinzufügen der neuesten Änderungen zur Bibliothek und erneutes Erstellen.
1. Schließen Sie eine weitere Testrunde ab.
