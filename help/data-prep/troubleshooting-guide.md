---
keywords: Experience Platform;Startseite;beliebte Themen;
title: Handbuch zur Fehlerbehebung bei der Datenvorbereitung
description: Dieses Dokument enthält Antworten auf häufig gestellte Fragen zur Adobe Experience Platform-Datenvorbereitung.
exl-id: 810cfb2f-f80a-4aa7-ab3c-beb5de78708e
source-git-commit: ff8f660c2b3a04d8b4b9d4f19891816a44069088
workflow-type: tm+mt
source-wordcount: '1256'
ht-degree: 28%

---

# [!DNL Data Prep] – Handbuch zur Fehlerbehebung

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zur [!DNL Data Prep] von Adobe Experience Platform sowie eine Anleitung zur Behebung gängiger Fehler. Antworten zu Fragen und allgemeine Informationen zur Fehlerbehebung bei Platform-APIs finden Sie im [Handbuch zur Fehlerbehebung bei Adobe Experience Platform-APIs](../landing/troubleshooting.md).

## FAQs

Im Folgenden finden Sie eine Liste häufig gestellter Fragen zur [!DNL Data Prep] und die zugehörigen Antworten.

### Wie werden Umwandlungsfehler behoben?

Bei der [!DNL Data Prep] werden alle Umwandlungsfehler in der Spalte gefunden, in der sie aufgetreten sind. In der Folge wird diese Spalte ungültig gemacht, wobei der Rest der Zeile weiterhin verarbeitet wird. Diese Umwandlungsprobleme werden in Form von **Warnungen** protokolliert. Es wird empfohlen, die Warnungen regelmäßig zu überprüfen und die Umwandlungslogik entsprechend der Umwandlungsprobleme anzupassen. Dadurch erhöht sich die Qualität der in Experience Platform aufgenommenen Daten.

Wenn die mit **Erforderlich** markierten Spalten aufgrund von Umwandlungsproblemen ungültig gemacht werden, wird die Zeile nicht aufgenommen. Wenn die partielle Datenaufnahme aktiviert ist, können Sie den Schwellenwert für solche Zurückweisungen festlegen, bevor der gesamte Fluss fehlschlägt. Wenn sich das Attribut „ungültig“ nicht auf Validierungen auf Schemaebene ausgewirkt hat, wird die Aufnahme der Zeile fortgesetzt.

Alle Zeilen, die ungültig sind, obwohl keine Umwandlungsfehler vorliegen, werden ebenfalls zurückgewiesen. Beispielsweise kann ein Datenaufnahme-Fluss eine Durchleitungszuordnung (keine Umwandlungslogik) zu einem erforderlichen Feld aufweisen, aber es gibt keinen eingehenden Wert für dieses Attribut. Diese Zeile wird zurückgewiesen.

### Wie kann ich Sonderzeichen in einem Feld mit Escape-Zeichen versehen?

Sie können Sonderzeichen in einem Feld durch die Verwendung von `${...}` mit Escape-Zeichen versehen. Allerdings werden JSON-Dateien, die Felder mit einem Punkt (`.`) enthalten, von diesem Mechanismus nicht unterstützt. Wenn Sie mit Hierarchien arbeiten und ein untergeordnetes Attribut einen Punkt (`.`) enthält, müssen Sie einen Backslash (`\`) verwenden, um Sonderzeichen zu umgehen. Ein Beispiel: `address` ist ein Objekt, das das Attribut `street.name` enthält. Auf dieses kann sich dann durch `address.street\.name` anstelle von `address.street.name` bezogen werden.

### Wie lang können berechnete Felder maximal sein?

Berechnete Felder haben eine maximale Länge von 4096 Zeichen.

### Meine Aufnahme ist aufgrund der Validierung eines Attributs fehlgeschlagen, aber dieses Attribut ist korrekt in meiner Datei enthalten. Was genau stimmt nicht?

Stellen Sie sicher, dass der Datentyp für jedes Feld mit dem im Schema definierten Typ übereinstimmt. Darüber hinaus müssen Einschränkungen wie „erforderlich“, „Aufzählung“ und „Format“ eingehalten werden.

Die aufgenommenen Daten müssen dem in Experience Platform definierten Experience-Datenmodell-Schema (XDM) entsprechen. Wenn das Attribut nicht mit dem erwarteten Typ oder Format übereinstimmt, der im Schema angegeben ist, schlägt die Aufnahme fehl.

Wenn die Funktionen zur Datenvorbereitung verwendet werden, stellen Sie sicher, dass die Umwandlung zu den richtigen Attributen führt. Sie können die Attribute während des Einrichtungsprozesses des Quell-Workflows überprüfen. Wählen Sie während des Zuordnungsschritts die Option **[!UICONTROL Neuer Feldtyp]** und dann **[!UICONTROL Berechnetes Feld hinzufügen]** aus. Verwenden Sie als Nächstes die Schnittstelle für berechnete Felder, um jede Funktion in der Vorschau anzuzeigen.

### Wie kann ich fehlerhafte Datenwerte aus Streaming- oder Batch-Aufnahme-Datensätzen entfernen?

Sie können die Datenvorbereitungs-Zuordnungsschnittstelle verwenden, um eine Filterung auf Spaltenebene durchzuführen, indem Sie nur Spalten zuordnen, die die erforderlichen Daten aufweisen. Sie können auch berechnete Felder verwenden, um die Daten mithilfe der Support-Funktionen umzuwandeln.

Die Filterung auf Zeilenebene ist derzeit nur für den [Adobe Analytics-Quell-Connector verfügbar](../sources/tutorials/ui/create/adobe-applications/analytics.md#row-level-filtering).

Nach der Aufnahme können Sie Data Distiller verwenden, um die Daten mithilfe von SQL zu bereinigen, zu formen und zu bearbeiten. Dieser Prozess erfordert jedoch das Löschen des Batches mit den fehlerhaften Datensätzen und die erneute Aufnahme eines neuen Batches, der aus dem Ergebnis der SQL erstellt wurde.

>[!IMPORTANT]
>
>* Data Lake: Sie können nur Datensätze entfernen, die bereits aufgenommen wurden, indem Sie den Batch löschen und erneut aufnehmen, in dem sich der Datensatz befindet.
>
>* Echtzeit-Kundenprofil: Attributbasierte Datensätze können durch die Aufnahme neuer Datensätze überschrieben werden, Erlebnisereignis-Datensätze können jedoch nicht entfernt werden.
>
>* Identity Service: Datensätze können nicht direkt aus Identity Service entfernt werden. Sie müssen das gesamte Profil löschen und dann das Profil mit den richtigen Datensätzen erneut hochladen, indem Sie die API zum Löschen von Profilen verwenden.

### Was sind die Best Practices für die Verwendung von berechneten Feldern beim GIF von Daten?

Sie können die Funktionen zur Datenvorbereitung während des Zuordnungsschritts von Quelldaten zum XDM-Schema verwenden, um ein neues berechnetes Feld zu erstellen.

### Wenn Sie Adobe Analytics-Daten als Quelle einbringen, wird das automatisch erstellte Schema für das Profil aktiviert?

Analytics-Daten werden nicht automatisch für Profil konfiguriert. Nachdem Sie den Quell-Connector konfiguriert haben, müssen Sie den Datensatz und das Schema aufrufen und für die Profilaufnahme aktivieren.

Beim Erstellen eines Analytics-Quell-Datenflusses in einer Produktions-Sandbox werden zwei Datenflüsse erstellt:

* Ein Datenfluss, der eine 13-monatige Aufstockung historischer Report Suite-Daten in den Data Lake durchführt. Dieser Datenfluss endet, wenn die Aufstockung abgeschlossen ist.
* Ein Datenfluss, der Live-Daten an den Data Lake und an das Profil sendet. Dieser Datenfluss läuft kontinuierlich.

### Wie kann ich einen Wert innerhalb eines Zuordnungsobjekts mithilfe von Datenvorbereitungsfunktionen in Kleinbuchstaben schreiben?

Sie können den Wert mit der Funktion `map_get_values` abrufen und ihn dann mit der Funktion Kleinbuchstaben festlegen:

```shell
lower(map_get_values(mapObject, 'keyName'))
```

Sie können dieselbe Funktion verwenden, um ein Zuordnungsobjekt in Kleinbuchstaben zu schreiben. Sie können jedoch nicht eine gesamte Zuordnung durchlaufen und jedes Element klein schreiben.

### Kann ich Datenvorbereitungsfunktionen verschachtelt verwenden?

Ja, Sie können eine Datenvorbereitungsfunktion innerhalb einer anderen Funktion verwenden, um komplexe Datenvorbereitungsfunktionen während der Datenaufnahme zu lösen.

Wenn Sie beispielsweise ein Feld basierend auf einer bestimmten Bedingung als null definieren möchten, können Sie die Funktion „if“ verwenden, um nach diesem Feld zu suchen. Wenn die Funktion &quot;`true`&quot; zurückgibt, können Sie „nullify()“ verwenden. Wenn sie &quot;`false`&quot; zurückgibt, können Sie das entsprechende Feld verwenden.

Wenn „marketing_type“ das Feld war, können Sie &quot;.equals“ verwenden, um den Wert im Feld „marketing_type“ zu überprüfen. Dieser kann in einer „if“-Funktion verschachtelt werden. Wenn er `true` zurückgibt, können Sie die Funktion „nullify()“ verwenden, wie unten dargestellt:

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

Im Folgenden finden Sie Beispiele für die Verschachtelung von Datenvorbereitungsfunktionen mithilfe von if, equals und NULLIFY:

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| --- | --- | --- | --- | --- | --- |
| IIF | Wertet einen gegebenen booleschen Ausdruck aus und gibt den angegebenen Wert basierend auf dem Ergebnis zurück. | <ul><li>AUSDRUCK: **Erforderlich** Der boolesche Ausdruck, der ausgewertet wird.</li><li>TRUE_VALUE: **Erforderlich** Der Wert, der zurückgegeben wird, wenn der Ausdruck „true“ ergibt.</li><li>FALSE_VALUE: **Erforderlich** Der Wert, der zurückgegeben wird, wenn der Ausdruck als „false“ ausgewertet wird.</li></ul> | IF(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | if(„s“.equalsIgnoreCase(„S„), „True“, „False„) | „TRUE“ |
| ist gleich | Vergleicht zwei Zeichenfolgen, um zu bestätigen, ob sie gleich sind. Bei dieser Funktion wird zwischen Groß- und Kleinschreibung unterschieden. | <ul><li>STRING1: **Erforderlich** Die erste Zeichenfolge, die Sie vergleichen möchten.</li><li>STRING2: **Erforderlich** Die zweite Zeichenfolge, die Sie vergleichen möchten. | STRING1..&#x200B;Equals(&#x200B;STRING2) | „string1“..&#x200B;Equals&#x200B;(„STRING1„) | false |
| für nichtig erklären | Setzt den Wert des Attributs auf null. Dies sollte verwendet werden, wenn Sie das Feld nicht in das Zielschema kopieren möchten. | | nullify() | nullify() | null |

{style="table-layout:auto"}

Im Folgenden finden Sie ein Beispiel dafür, wie die Funktionen verschachtelt werden können, unter der Annahme, dass das auszuwertende Feld „marketing_type“ ist.

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

Als Nächstes, da Sie die folgenden drei Felder haben:

* marketing_type: (E-Mail, PhyMail, Push, SMS, Telefon)
* total_consents: Zahlenbereich von 4000 bis 5500
* Datum: von Februar bis März 2024

Sie können die drei oben aufgeführten Funktionen verwenden und verschachteln, um die drei Felder zu bearbeiten:

* iif(marketing_type.equals(„email„), ungültig(), iif(marketing_type.equals(„Push„), „Push-Benachrichtigung“, marketing_type))
* iif(marketing_type.equals(„phyMail„), nullify(), iif(marketing_type.equals(„sms„), „text-message“, marketing_type))
* iif(total_consents > 5000, iif(marketing_type.equals(„phone„), nullify(), marketing_type), „unzureichende Einverständnisse„)
* iif(date.equals(„3/21/24„), iif(marketing_type.equals(„Push„), nullify(), marketing_type), „not-March„)
* iif(total_consents &lt; 4500, iif(marketing_type.equals(„sms„), „low-consent-sms“, marketing_type), „high-consent„)
* iif(marketing_type.equals(„email„), iif(total_consents > 5000, nullify(), „email-low-consent„), marketing_type)
* iif(marketing_type.equals(„Push„), iif(total_consents &lt; 4500, „low-consent-push“, nullify()), marketing_type)
* iif(total_consents >= 5500, iif(marketing_type.equals(„phyMail„), nullify(), „High-Consents„), marketing_type)