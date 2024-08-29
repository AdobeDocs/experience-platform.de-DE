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

### Meine Aufnahme schlug aufgrund der Validierung eines Attributs fehl, aber dieses Attribut ist in meiner Datei korrekt. Was genau ist falsch?

Stellen Sie sicher, dass der Datentyp für jedes Feld mit dem im Schema definierten Typ übereinstimmt. Darüber hinaus müssen Einschränkungen wie &quot;Erforderlich&quot;, &quot;Enum&quot;und &quot;Format&quot;beachtet werden.

Die aufgenommenen Daten müssen dem im Experience Platform definierten Experience-Datenmodell (XDM)-Schema entsprechen. Wenn das Attribut nicht dem im Schema angegebenen erwarteten Typ oder Format entspricht, schlägt die Aufnahme fehl.

Wenn die Data Prep-Funktionen verwendet werden, stellen Sie sicher, dass die Transformation zu den richtigen Attributen führt. Sie können die Attribute während des Einrichtungsprozesses des Ursprungs-Workflows überprüfen. Wählen Sie im Zuordnungsschritt **[!UICONTROL Neuer Feldtyp]** und dann **[!UICONTROL Berechnetes Feld hinzufügen]** aus. Verwenden Sie anschließend die berechnete Feldoberfläche, um eine Vorschau der einzelnen Funktionen anzuzeigen.

### Wie kann ich fehlerhafte Datenwerte aus Streaming- oder Batch-Erfassungsdatensätzen entfernen?

Sie können die Zuordnungsschnittstelle &quot;Datenvorbereitung&quot;verwenden, um auf Spaltenebene Filtern durchzuführen, indem nur Spalten zugeordnet werden, die über erforderliche Daten verfügen. Sie können auch berechnete Felder verwenden, um die Daten mithilfe der Funktionen zur Unterstützung umzuwandeln.

Die Filterung auf Zeilenebene ist derzeit nur für den [Adobe Analytics-Quell-Connector](../sources/tutorials/ui/create/adobe-applications/analytics.md#row-level-filtering) verfügbar.

Nach der Erfassung können Sie mithilfe von Data Destiller die Daten mit SQL bereinigen, gestalten und bearbeiten. Dieser Prozess erfordert jedoch das Löschen des Batches mit den fehlerhaften Datensätzen und das erneute Erfassen eines neuen Batches, der aus dem SQL-Ergebnis erstellt wurde.

>[!IMPORTANT]
>
>* Data Lake: Sie können Datensätze, die bereits erfasst wurden, nur entfernen, indem Sie den Batch löschen und erneut erfassen, in dem sich der Datensatz befindet.
>
>* Echtzeit-Kundenprofil: Sie können attributbasierte Datensätze überschreiben, indem Sie neue Datensätze erfassen. Erlebnisereignisdatensätze können jedoch nicht entfernt werden.
>
>* Identity Service: Im Identity Service können keine Datensätze vollständig entfernt werden. Sie müssen das gesamte Profil löschen und das Profil mit den richtigen Datensätzen mithilfe der API zum Löschen des Profils erneut hochladen.

### Was sind die Best Practices für die Verwendung berechneter Felder in GIF-Daten?

Sie können die Zuordnungsfunktionen der Datenvorbereitung während des Zuordnungsschritts von Quelldaten zum XDM-Schema verwenden, um ein neues berechnetes Feld zu erstellen.

### Wird das erstellte Schema automatisch für das Profil aktiviert, wenn Sie Adobe Analytics-Daten als Quelle importieren?

Analytics-Daten werden nicht automatisch für Profil konfiguriert. Nachdem Sie den Quell-Connector konfiguriert haben, müssen Sie in den Datensatz und das Schema wechseln und sie für die Profilaufnahme aktivieren.

Wenn Sie einen Analytics-Quell-Datenfluss in einer Produktions-Sandbox erstellen, werden zwei Datenflüsse erstellt:

* Ein Datenfluss, der eine 13-monatige Aufstockung historischer Report Suite-Daten in den Data Lake ausführt. Dieser Datenfluss endet, wenn die Aufstockung abgeschlossen ist.
* Ein Datenfluss, der Live-Daten an den Data Lake und an Profil sendet. Dieser Datenfluss wird kontinuierlich ausgeführt.

### Wie kann ich mithilfe von Datenvorbereitungsfunktionen einen Wert innerhalb eines Zuordnungsobjekts in Kleinbuchstaben schreiben?

Sie können den Wert mit der Funktion `map_get_values` abrufen und ihn dann mithilfe der Funktion lower in Kleinbuchstaben umwandeln:

```shell
lower(map_get_values(mapObject, 'keyName'))
```

Sie können dieselbe Funktion verwenden, um ein map -Objekt in Kleinbuchstaben zu schreiben. Es ist jedoch nicht möglich, eine ganze Karte zu durchlaufen und jedes Element in Kleinbuchstaben zu schreiben.

### Kann ich Data Prep-Funktionen verschachtelt verwenden?

Ja, Sie können eine Datenvorbereitung-Funktion innerhalb einer anderen Funktion verwenden, um komplexe Datenvorvorbereitungsfunktionen während der Datenerfassung zu lösen.

Wenn Sie beispielsweise ein Feld basierend auf einer bestimmten Bedingung als null definieren möchten, können Sie die Funktion &quot;if&quot;verwenden, um nach diesem Feld zu suchen. Wenn die Funktion den Wert `true` zurückgibt, können Sie &quot;nullify()&quot; verwenden und wenn sie den Wert `false` zurückgibt, können Sie das entsprechende Feld verwenden.

Wenn marketing_type das Feld war, können Sie &quot;.equals&quot;verwenden, um den Wert im Feld marketing_type zu überprüfen. Dieser Wert kann in einer &quot;if&quot;-Funktion verschachtelt sein. Wenn es `true` zurückgibt, können Sie die Funktion &quot;nullify()&quot; wie unten gezeigt verwenden:

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

Die folgenden Beispiele zeigen, wie Sie Datenvorlagenfunktionen mit if, equals und nullify verschachteln können:

| Funktion | Beschreibung | Parameter | Aufbau | Ausdruck | Beispielausgabe |
| --- | --- | --- | --- | --- | --- |
| iif | Wertet einen bestimmten booleschen Ausdruck aus und gibt den angegebenen Wert basierend auf dem Ergebnis zurück. | <ul><li>AUSDRUCK: **Erforderlich** Der boolesche Ausdruck, der ausgewertet wird.</li><li>TRUE_VALUE: **Erforderlich** Der Wert, der zurückgegeben wird, wenn der Ausdruck &quot;true&quot;ergibt.</li><li>FALSE_VALUE: **Erforderlich** Der Wert, der zurückgegeben wird, wenn der Ausdruck &quot;false&quot;ergibt.</li></ul> | iif(EXPRESSION, TRUE_VALUE, FALSE_VALUE) | iif(&quot;s&quot;.equalsIgnoreCase(&quot;S&quot;), &quot;True&quot;, &quot;False&quot;) | &quot;True&quot; |
| ist gleich | Vergleicht zwei Zeichenketten, um sicherzustellen, dass sie gleich sind. Diese Funktion unterscheidet zwischen Groß- und Kleinschreibung. | <ul><li>STRING1: **Erforderlich** Die erste Zeichenfolge, die Sie vergleichen möchten.</li><li>STRING2: **Erforderlich** Die zweite Zeichenfolge, die Sie vergleichen möchten. | STRING1. &#x200B;equals( &#x200B; STRING2) | &quot;string1&quot;. &#x200B;equals &#x200B;(&quot;STRING1&quot;) | false |
| nullify | Legt den Wert des Attributs auf null fest. Dies sollte verwendet werden, wenn Sie das Feld nicht in das Zielschema kopieren möchten. | | nullify() | nullify() | null |

{style="table-layout:auto"}

Im Folgenden finden Sie ein Beispiel dafür, wie die Funktionen verschachtelt werden können, vorausgesetzt, das ausgewertete Feld lautet &quot;marketing_type&quot;.

```shell
iif(marketing_type.equals("phyMail"), nullify(), marketing_type)
```

Als Nächstes haben Sie die folgenden drei Felder:

* marketing_type: (email, phyMail, push, sms, phone)
* total_approval: Zahlenbereich von 4000 bis 5500
* Datum: von Februar bis März 2024

Sie können die drei oben aufgeführten Funktionen verwenden und verschachteln, um die drei Felder zu bearbeiten:

* iif(marketing_type.equals(&quot;email&quot;), nullify(), if(marketing_type.equals(&quot;push&quot;), &quot;push-notification&quot;, marketing_type))
* if(marketing_type.equals(&quot;phyMail&quot;), nullify(), if(marketing_type.equals(&quot;sms&quot;), &quot;text-message&quot;, marketing_type)
* iif(total_consent > 5000, if(marketing_type.equals(&quot;phone&quot;), nullify(), marketing_type), &quot;unzureichende Zustimmung&quot;)
* iif(date.equals(&quot;3/21/24&quot;), if(marketing_type.equals(&quot;push&quot;), nullify(), marketing_type), &quot;not-March&quot;)
* iif(total_consent &lt; 4500, iif(marketing_type.equals(&quot;sms&quot;), &quot;low-consent-sms&quot;, marketing_type), &quot;high-consent&quot;)
* iif(marketing_type.equals(&quot;email&quot;), iif(total_consent > 5000, nullify(), &quot;email-low-consent&quot;), marketing_type)
* iif(marketing_type.equals(&quot;push&quot;), iif(total_consent &lt; 4500, &quot;low-consent-push&quot;, nullify()), marketing_type)
* iif(total_consent >= 5500, if(marketing_type.equals(&quot;phyMail&quot;), nullify(), &quot;high-consent&quot;), marketing_type)