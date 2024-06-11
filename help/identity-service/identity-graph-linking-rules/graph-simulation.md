---
title: Diagrammsimulation
description: Erfahren Sie, wie Sie die Diagrammsimulation in der Benutzeroberfläche des Identity Service verwenden.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 2afdfd54b420bcf59423ea64048d928422ea61c9
workflow-type: tm+mt
source-wordcount: '1590'
ht-degree: 5%

---

# Diagrammsimulation

Diagrammsimulation ist ein Tool in der Benutzeroberfläche von Identity Service, mit dem Sie simulieren können, wie sich ein Identitätsdiagramm bei einer bestimmten Kombination von Identitäten verhält und wie Sie die [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md).

In diesem Dokument erfahren Sie, wie Sie mit der Diagrammsimulation das Verhalten von Identitätsdiagrammen und die Funktionsweise des Diagrammalgorithmus besser verstehen können.

## Kennenlernen der Benutzeroberfläche der Diagrammsimulation

Sie können auf die Diagrammsimulation in der Benutzeroberfläche von Adobe Experience Platform zugreifen. Auswählen **[!UICONTROL Identitäten]** aus der linken Navigation und wählen Sie dann **[!UICONTROL Diagrammsimulation]** aus der oberen Kopfzeile.

![Die Benutzeroberfläche für Diagrammsimulation in der Adobe Experience Platform-Benutzeroberfläche.](../images/graph-simulation/graph-simulation.png)

Die Benutzeroberfläche der Diagrammsimulation kann in drei Abschnitte unterteilt werden:

* Ereignisse: Verwenden Sie die **[!UICONTROL Veranstaltungen]** -Bedienfeld, um Identitäten hinzuzufügen, um ein Diagramm zu simulieren. Eine vollständig qualifizierte Identität muss über einen Identitäts-Namespace und den zugehörigen Identitätswert verfügen. Sie müssen mindestens zwei Identitäten hinzufügen, um ein Diagramm zu simulieren. Sie können auch **[!UICONTROL Ladebeispiel]** , um ein vorkonfiguriertes Ereignis und eine Algorithmuseinrichtung einzugeben.

![Das Ereignisfeld des Diagrammsimulations-Tools.](../images/graph-simulation/events.png)

* Algorithmuskonfiguration: Verwenden Sie die **[!UICONTROL Algorithmuskonfiguration]** um den Optimierungsalgorithmus für Ihre Namespaces hinzuzufügen und zu konfigurieren. Sie können einen Namespace per Drag-and-Drop verschieben, um die jeweilige Prioritätsstufe zu ändern. Sie können auch **[!UICONTROL Eindeutige pro Diagramm]** um zu ermitteln, ob ein Namespace eindeutig ist.

![Die Algorithmuskonfiguration des Diagrammsimulations-Tools.](../images/graph-simulation/algorithm-configuration.png)

* Simulierter Diagrammanzeige: Der Viewer für das simulierte Diagramm zeigt das resultierende Diagramm basierend auf den hinzugefügten Ereignissen und dem von Ihnen konfigurierten Algorithmus an. Eine gerade Linie zwischen zwei Knoten bedeutet, dass eine Verbindung hergestellt wird. Eine gepunktete Linie zeigt an, dass ein Link entfernt wurde.


![Der Viewer-Bereich für simulierte Diagramme mit einem Beispiel für ein simuliertes Diagramm.](../images/graph-simulation/simulated-graph.png)

## Ereignisse hinzufügen

Wählen Sie zunächst **[!UICONTROL Ereignisse hinzufügen]**.

![Wählen Sie die Schaltfläche Ereignisse hinzufügen aus.](../images/graph-simulation/add-events.png)

Ein Popup-Fenster wird angezeigt für [!UICONTROL Ereignis 1]. Geben Sie hier Ihre Kombination aus Identitäts-Namespace und Identitätswert ein. Über das Dropdown-Menü können Sie einen Identitäts-Namespace auswählen. Alternativ können Sie die ersten Buchstaben eines Namespace eingeben und dann die Optionen im Dropdown-Menü auswählen. Nachdem Sie Ihren Namespace ausgewählt haben, geben Sie einen Identitätswert an, der Ihrem Namespace entspricht.

![](../images/graph-simulation/event-one.png)

>[!TIP]
>
>Der Identitätswert, den Sie bei Diagrammsimulation-Übungen eingeben, muss keine echten Identitätswerte sein und kann einfache Platzhalter sein.

Nachdem Ihre erste Identität abgeschlossen ist, wählen Sie das Symbol zum Hinzufügen (**`+`**), um eine zweite Identität hinzuzufügen.

![Die erste voll qualifizierte Identität von {E-Mail: tom@acme.com} wird im Bereich &quot;Ereignisse&quot;der Diagrammsimulation eingegeben.](../images/graph-simulation/event-one-added.png)

Wiederholen Sie die gleichen Schritte und fügen Sie eine zweite Identität hinzu. Für die Erstellung eines Identitätsdiagramms sind zwei vollständig qualifizierte Identitäten erforderlich. Im folgenden Beispiel wird eine ECID als Namespace hinzugefügt und der Wert `111`. Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![Eine zweite Identität von {ECID: 111} wird zu Ereignis 1 hinzugefügt.](../images/graph-simulation/first-event.png)

Die [!UICONTROL Veranstaltungen] -Benutzeroberfläche aktualisiert, um Ihr erstes Ereignis anzuzeigen, in diesem Fall: `{Email: tom@acme.com, ECID: 111}`.

![Die aktualisierte Ereignisoberfläche mit {Email: tom@acme.com, ECID: 111}.](../images/graph-simulation/add-second-event.png)

Wiederholen Sie die gleichen Schritte, um ein zweites Ereignis hinzuzufügen. Fügen Sie für Ereignis Nr. 2 `{Email: summer@acme.com}` als erste Identität und fügen Sie dann dasselbe hinzu `{ECID: 111}` als zweite Identität bezeichnet, wodurch ein zweites Ereignis von erstellt wird: `{Email: summer@acme.com}, {ECID: 111}`. Wenn Sie fertig sind, sollten Sie über zwei Ereignisse verfügen: eines für `{Email: tom@acme.com, ECID: 111}` und eines für `{Email: summer@acme.com}, {ECID: 111}`.

![Die aktualisierte Ereignisoberfläche mit zwei Ereignissen.](../images/graph-simulation/two-events.png)

### Beispiel laden

+++Auswählen , um Schritte zur Verwendung von vorab geladenen Diagrammbeispielen anzuzeigen

Um ein Beispieldiagramm mit einem vorkonfigurierten Algorithmus einzurichten, wählen Sie **[!UICONTROL Beispiel laden]**. Es wird ein Popup-Fenster mit verfügbaren Diagrammszenarien angezeigt, aus denen Sie Folgendes auswählen können:

| Beispieldiagramm | Beschreibung | Beispiel |
| --- | --- | --- |
| Gemeinsam genutztes Gerät | Freigegebenes Gerät bezieht sich auf Szenarien, in denen sich zwei verschiedene Benutzer auf demselben Gerät anmelden. | Ein Ehemann und eine Ehefrau teilen sich eine iPad für Internet-Browsing und E-Commerce. |
| Ungültige (nicht eindeutige) Telefonnummer | Ungültiges oder nicht eindeutiges Telefon bezieht sich auf Szenarien, in denen zwei verschiedene Benutzer dieselbe Telefonnummer verwenden, um ein Konto zu erstellen. | Eine Mutter und ihre Tochter verwenden ihre gemeinsam genutzte Festnetztelefonnummer, um sich für E-Commerce-Konten anzumelden. |
| „Ungültige“ Identitätswerte | &quot;Ungültige&quot;Identitätswerte beziehen sich auf Szenarien, in denen Identity Service aufgrund einer fehlerhaften Implementierung nicht eindeutige IDFAs generiert. | WebSDK sendet fälschlicherweise eine `user_null` -Wert für jedes Ereignis aufgrund von Code-Implementierungsproblemen. |

Wählen Sie eine der Optionen aus, um die Diagrammsimulation mit vorkonfigurierten Ereignissen und Algorithmen zu laden. Sie können weiterhin weitere Konfigurationen an allen vorab geladenen Diagrammszenarios vornehmen.

Wählen Sie zum Abschluss **[!UICONTROL Simulieren]**.

+++

### Textversion verwenden

+++Auswählen , um Schritte zur Verwendung der Textversion anzuzeigen

Sie können auch den Textmodus verwenden, um Ereignisse zu konfigurieren. Um den Textmodus zu verwenden, wählen Sie das Zahnrad (?) und wählen Sie **[!UICONTROL Text (erweiterte Benutzer)]**.

Sie können Ihre Identitäten manuell im Textmodus eingeben. Verwenden Sie einen Doppelpunkt (`:`), um den Identitätswert zu unterscheiden, der dem von Ihnen eingegebenen Namespace entspricht, und dann ein Komma (`,`), um Ihre Identitäten zu trennen. Um verschiedene Ereignisse voneinander zu unterscheiden, verwenden Sie für jedes Ereignis eine neue Zeile.

+++

### Ereignis bearbeiten

Um ein Ereignis zu bearbeiten, wählen Sie die Auslassungszeichen (`...`) neben einem bestimmten Ereignis klicken und dann **[!UICONTROL Bearbeiten]**.

### Ereignis löschen

Um ein Ereignis zu löschen, wählen Sie die Auslassungszeichen (`...`) neben einem bestimmten Ereignis klicken und dann **[!UICONTROL Löschen]**.

## Algorithmus konfigurieren

Der von Ihnen konfigurierte Algorithmus bestimmt, wie Identity Service die in Ihre Ereignisse eingegebenen Namespaces behandelt. Jede Konfiguration, die Sie in der Benutzeroberfläche für Diagrammsimulation zusammengestellt haben, wird nicht in den Identitätseinstellungen gespeichert.

Um zu beginnen, wählen Sie Hinzufügen (`+`) in der unteren Ecke des Algorithmuskonfigurationsbereichs.



Eine leere Konfigurationszeile wird angezeigt. Geben Sie zunächst den Namespace ein, den Sie für Ihre Ereignisse verwendet haben. Geben Sie in diesem Fall zunächst die CRM-ID ein. Sobald Sie Ihren Namespace eingeben, werden die Spalten für [!UICONTROL Identitätssymbol] und [!UICONTROL Identitätstyp] automatisch ausgefüllt.



Wiederholen Sie die gleichen Schritte und fügen Sie den zweiten Namespace hinzu, in diesem Fall die ECID. Sobald alle Namespaces eingegeben wurden, können Sie mit der Konfiguration ihrer Prioritäten und Einzigartigkeit beginnen.

* **Namespace-Priorität**: Die Priorität eines Namespace bestimmt seine relative Bedeutung im Vergleich zu den anderen Namespaces in einem bestimmten Identitätsdiagramm. Wenn Ihr Identitätsdiagramm beispielsweise vier verschiedene Namespaces aufweist: CRM-ID, ECID, E-Mail und Apple IDFA, können Sie Prioritäten konfigurieren, um eine Reihenfolge von Bedeutung für den vier Namespace zu bestimmen. (WARUM HINZUFÜGEN)
* **Eindeutiger Namespace**: Wenn ein Namespace als eindeutig gekennzeichnet ist, generiert Identity Service Diagramme mit dem Vorbehalt, dass nur eine Identität mit einem bestimmten eindeutigen Namespace vorhanden sein kann. Wenn beispielsweise die CRM-ID als eindeutiger Namespace bezeichnet wird, darf ein Diagramm nur eine Identität mit CRM-ID enthalten. Wenn mehr als eine Identität mit dem CRM-ID-Namespace vorhanden ist, wird der älteste Link entfernt.

Um die Namespace-Priorität zu konfigurieren, wählen Sie die Namespace-Zeilen aus und ziehen Sie sie in die gewünschte Prioritätsreihenfolge, wobei die oberste Zeile die höhere Priorität und die untere Zeile die niedrigere Priorität darstellt. Um einen Namespace als eindeutig festzulegen, wählen Sie die **[!UICONTROL Eindeutige pro Diagramm]** aktivieren.



Wählen Sie zum Abschluss **[!UICONTROL Simulieren]**.

## Simuliertes Diagramm anzeigen

Die [!UICONTROL Simuliertes Diagramm] zeigt die Identitätsdiagramme an, die basierend auf den von Ihnen hinzugefügten Ereignissen und dem von Ihnen konfigurierten Algorithmus generiert wurden.

| Diagrammsymbole | Beschreibung |
| --- | --- |
| Durchgehende Linie | Eine durchgehende Linie stellt eine festgestellte Verknüpfung zwischen zwei Identitäten dar. |
| gepunktete Linie | Eine gepunktete Linie stellt eine entfernte Verknüpfung zwischen zwei Identitäten dar. |
| Nummer in Zeilen | Eine Zahl in einer Zeile steht für den Zeitstempel des Zeitpunkts, zu dem der angegebene Link generiert wurde. Die niedrigste Zahl (1) stellt die früheste eingerichtete Verknüpfung dar. |

Im unten stehenden Beispieldiagramm existiert eine gepunktete Linie zwischen `{CRM ID: Tom}` und `{ECID: 111}` aus folgenden Gründen:

* Die CRM-ID wurde während des Algorithmuskonfigurationsschritts als eindeutig gekennzeichnet. Daher kann in einem Diagramm nur eine Identität mit einem CRM-ID-Namespace vorhanden sein.
* Die Verbindung zwischen `{CRM ID: Tom}` und `{ECID: 111}` war die erste festgestellte Identität (Ereignis Nr. 1). Es ist der älteste Link und wird daher entfernt.

## Beispieldiagrammszenarien

>[!NOTE]
>
>&quot;CRM-ID&quot;ist ein benutzerdefinierter Namespace. Daher müssen Sie in den unten stehenden Beispielen einen benutzerdefinierten Namespace mit einem Anzeigenamen und Identitätssymbol von &quot;CRM ID&quot;erstellen.

Im folgenden Abschnitt finden Sie Beispiele für Diagrammszenarien, auf die Sie bei der Diagrammsimulation stoßen können.

### Nur CRM-ID

Ereignisse:

* CRM-ID: Tom, ECID: 111

Algorithmuskonfiguration:

| Priorität | Anzeigename | Identitätssymbol | Identitätstyp | Nur einmal im Diagramm |
| ---| --- | --- | --- | --- |
| 1 | CRM-ID | CRM-ID | CROSS_DEVICE | Ja |
| 2 | ECID | ECID | COOKIE | NO |

+++Auswählen zum Anzeigen des simulierten Diagramms

+++

### CRM-ID mit gehashter E-Mail

In diesem Szenario wird eine CRM-ID erfasst und stellt sowohl Online- (Erlebnisereignis-) als auch Offline-Daten (Profildatensatz) dar. Dieses Szenario umfasst auch die Aufnahme einer Hash-E-Mail, die einen anderen Namespace darstellt, der im CRM-Datensatz zusammen mit der CRM-ID gesendet wird.

Ereignisse:

* CRM-ID: Tom, Email_LC_SHA256: tom<span>@acme.com
* CRM-ID: Tom, ECID: 111
* CRM-ID: Summer, Email_LC_SHA256: summer<span>@acme.com
* CRM-ID: Summer, ECID: 222

Algorithmuskonfiguration:

| Priorität | Anzeigename | Identitätssymbol | Identitätstyp | Nur einmal im Diagramm |
| ---| --- | --- | --- | --- |
| 1 | CRM-ID | CRM-ID | CROSS_DEVICE | Ja |
| 2 | E-Mails (SHA256, in Kleinbuchstaben) | Email_LC_SHA256 | E-Mail | NO |
| 3 | ECID | ECID | COOKIE | NO |

+++Auswählen zum Anzeigen des simulierten Diagramms

+++

### CRM-ID mit Hash-E-Mail, Hash-Telefon, GAID und IDFA

Ereignisse:

* CRM-ID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRM-ID: Tom, ECID: 111
* CRM-ID: Tom, ECID: 222, IDFA: A-A-A
* CRM-ID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRM-ID: Summer, ECID: 333
* CRM-ID: Summer, ECID: 444, GAID:B-B

Algorithmuskonfiguration:

| Priorität | Anzeigename | Identitätssymbol | Identitätstyp | Nur einmal im Diagramm |
| ---| --- | --- | --- | --- |
| 1 | CRM-ID | CRM-ID | CROSS_DEVICE | Ja |
| 2 | E-Mails (SHA256, in Kleinbuchstaben) | Email_LC_SHA256 | E-Mail | NO |
| 3 | Telefon (SHA256) | Phone_SHA256 | Telefon | NO |
| 4 | Google Ad ID (GAID) | GAID | GERÄT | NO |
| 5 | Apple IDFA (ID für Apple) | IDFA | GERÄT | NO |
| 6 | ECID | ECID | COOKIE | NO |

+++Auswählen zum Anzeigen des simulierten Diagramms

+++