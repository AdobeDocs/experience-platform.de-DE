---
title: Anleitung zur Diagrammsimulation in der Benutzeroberfläche
description: Erfahren Sie, wie Sie die Diagrammsimulation in der Benutzeroberfläche des Identity Service verwenden.
badge: Beta
exl-id: 89f0cf6e-c43f-40ec-859a-f3b73a6da8c8
source-git-commit: 4c49bec7974dafe18d18deded6ddc936ece47dc3
workflow-type: tm+mt
source-wordcount: '1438'
ht-degree: 1%

---

# Handbuch für die [!DNL Graph Simulation]-Benutzeroberfläche

>[!AVAILABILITY]
>
>Diese Funktion ist noch nicht verfügbar. Das Betaprogramm für Regeln zur Identitätsdiagrammverlinkung wird voraussichtlich im Juli für Entwicklungs-Sandboxes beginnen. Wenden Sie sich an Ihr Adobe-Account-Team, um Informationen zu den Teilnahmekriterien zu erhalten.

[!DNL Graph Simulation] ist ein Tool in der Identity Service-Benutzeroberfläche, mit dem Sie simulieren können, wie sich ein Identitätsdiagramm bei einer bestimmten Kombination von Identitäten verhält und wie Sie den [Identitätsoptimierungsalgorithmus](./identity-optimization-algorithm.md) konfigurieren.

In diesem Dokument erfahren Sie, wie Sie mit [!DNL Graph Simulation] das Verhalten von Identitätsdiagrammen und die Funktionsweise des Diagrammalgorithmus besser verstehen können.

## Erfahren Sie mehr über die [!DNL Graph Simulation]-Oberfläche {#interface}

Sie können auf [!DNL Graph Simulation] in der Adobe Experience Platform-Benutzeroberfläche zugreifen. Wählen Sie **[!UICONTROL Identitäten]** aus der linken Navigation und dann **[!UICONTROL Diagrammsimulation]** aus der oberen Kopfzeile.

![Die Diagrammsimulation-Benutzeroberfläche in der Adobe Experience Platform-Benutzeroberfläche.](../images/graph-simulation/graph-simulation.png)

Die [!DNL Graph Simulation] -Schnittstelle kann in drei Abschnitte unterteilt werden:

>[!BEGINTABS]

>[!TAB Ereignisse]

Ereignisse: Verwenden Sie das Bedienfeld **[!UICONTROL Ereignisse]** , um Identitäten hinzuzufügen und ein Diagramm zu simulieren. Eine vollständig qualifizierte Identität muss über einen Identitäts-Namespace und den zugehörigen Identitätswert verfügen. Sie müssen mindestens zwei Identitäten hinzufügen, um ein Diagramm zu simulieren. Sie können auch **[!UICONTROL Beispiel laden]** auswählen, um ein vorkonfiguriertes Ereignis und eine Algorithmuseinrichtung einzugeben.

![Das Ereignisbedienfeld des Diagrammsimulations-Tools.](../images/graph-simulation/events.png)

>[!TAB Algorithmuskonfiguration]

Algorithmuskonfiguration: Verwenden Sie den Bereich **[!UICONTROL Algorithmuskonfiguration]** , um den Optimierungsalgorithmus für Ihre Namespaces hinzuzufügen und zu konfigurieren. Sie können einen Namespace per Drag-and-Drop verschieben, um die jeweilige Prioritätsstufe zu ändern. Sie können auch **[!UICONTROL Eindeutig pro Diagramm]** auswählen, um zu bestimmen, ob ein Namespace eindeutig ist.

![Die Algorithmuskonfiguration des Diagrammsimulations-Tools.](../images/graph-simulation/algorithm-configuration.png)

>[!TAB  Simulierter Diagramm-Viewer]

Simulierter Diagramm-Viewer: Der simulierte Diagramm-Viewer zeigt das resultierende Diagramm basierend auf den hinzugefügten Ereignissen und dem von Ihnen konfigurierten Algorithmus an. Eine gerade Linie zwischen zwei Identitäten bedeutet, dass eine Verbindung hergestellt wird. Eine gepunktete Linie zeigt an, dass ein Link entfernt wurde.

![Der Viewer-Bereich für das simulierte Diagramm mit einem Beispiel für ein simuliertes Diagramm.](../images/graph-simulation/simulated-graph.png)

>[!ENDTABS]

## Ereignisse hinzufügen {#add-events}

Wählen Sie zunächst **[!UICONTROL Ereignisse hinzufügen]** aus.

![ Die Schaltfläche Ereignisse hinzufügen wurde ausgewählt.](../images/graph-simulation/add-events.png)

Für [!UICONTROL Ereignis 1] wird ein Popup-Fenster angezeigt. Geben Sie hier Ihre Kombination aus Identitäts-Namespace und Identitätswert ein. Über das Dropdown-Menü können Sie einen Identitäts-Namespace auswählen. Alternativ können Sie die ersten Buchstaben eines Namespace eingeben und dann die Optionen im Dropdown-Menü auswählen. Nachdem Sie Ihren Namespace ausgewählt haben, geben Sie einen Identitätswert an, der Ihrem Namespace entspricht.

![Das Fenster Ereignis Nr. 1 mit einer leeren Oberfläche.](../images/graph-simulation/event-one.png)

>[!TIP]
>
>Der Identitätswert, den Sie bei [!DNL Graph Simulation] Übungen eingeben, muss keine echten Identitätswerte sein und kann einfache Platzhalter sein.

Nachdem Ihre erste Identität abgeschlossen ist, wählen Sie das Symbol zum Hinzufügen (**`+`**) aus, um eine zweite Identität hinzuzufügen.

![Die erste voll qualifizierte Identität von {Email: tom@acme.com} wird im Ereignisbereich der Diagrammsimulation eingegeben.](../images/graph-simulation/event-one-added.png)

Wiederholen Sie die gleichen Schritte und fügen Sie eine zweite Identität hinzu. Für die Erstellung eines Identitätsdiagramms sind zwei vollständig qualifizierte Identitäten erforderlich. Im folgenden Beispiel wird eine ECID als Namespace hinzugefügt und mit dem Wert `111` angegeben. Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![ Eine zweite Identität von {ECID: 111} wird zu Ereignis Nr. 1 hinzugefügt.](../images/graph-simulation/first-event.png)

Die Oberfläche [!UICONTROL Ereignisse] wird aktualisiert, um Ihr erstes Ereignis anzuzeigen, in diesem Fall: `{Email: tom@acme.com, ECID: 111}`.

![Die aktualisierte Ereignisschnittstelle mit {Email: tom@acme.com, ECID: 111}.](../images/graph-simulation/add-second-event.png)

Wiederholen Sie die gleichen Schritte, um ein zweites Ereignis hinzuzufügen. Fügen Sie für Ereignis Nr. 2 `{Email: summer@acme.com}` als erste Identität hinzu und fügen Sie dann denselben `{ECID: 111}` als zweite Identität hinzu, wodurch ein zweites Ereignis von `{Email: summer@acme.com}, {ECID: 111}` erstellt wird. Wenn Sie fertig sind, sollten Sie zwei Ereignisse haben, eines für `{Email: tom@acme.com, ECID: 111}` und eines für `{Email: summer@acme.com}, {ECID: 111}`.

![Die aktualisierte Ereignisschnittstelle mit zwei Ereignissen.](../images/graph-simulation/two-events.png)

### Beispiel laden {#load-example}

Wählen Sie **[!UICONTROL Beispiel laden]** aus, um ein Beispieldiagramm mit einem voreingestellten Algorithmus und einer Ereigniskonfiguration einzurichten.

![Die Option &quot;Beispiel laden&quot;wurde ausgewählt.](../images/graph-simulation/load-example.png)

Es wird ein Popup-Fenster mit verfügbaren Diagrammszenarien angezeigt, aus denen Sie Folgendes auswählen können:

| Beispieldiagramm | Beschreibung | Beispiel |
| --- | --- | --- |
| Gemeinsam genutztes Gerät | Freigegebenes Gerät bezieht sich auf Szenarien, in denen sich zwei verschiedene Benutzer auf demselben Gerät anmelden. | Ein Ehemann und eine Ehefrau teilen sich eine iPad für Internet-Browsing und E-Commerce. |
| Ungültige (nicht eindeutige) Telefonnummer | Ungültiges oder nicht eindeutiges Telefon bezieht sich auf Szenarien, in denen zwei verschiedene Benutzer dieselbe Telefonnummer verwenden, um ein Konto zu erstellen. | Eine Mutter und ihre Tochter verwenden ihre gemeinsam genutzte Festnetztelefonnummer, um sich für E-Commerce-Konten anzumelden. |
| „Ungültige“ Identitätswerte | &quot;Ungültige&quot;Identitätswerte beziehen sich auf Szenarien, in denen Identity Service aufgrund einer fehlerhaften Implementierung nicht eindeutige IDFAs generiert. | WebSDK sendet fälschlicherweise einen `user_null` -Wert für jedes Ereignis aufgrund von Code-Implementierungsproblemen. |

![Ein Fenster, in dem die verfügbaren vorkonfigurierten Beispiele angezeigt werden: freigegebenes Gerät, ungültiges Telefon und ungültige Identitätswerte.](../images/graph-simulation/example-options.png)

Wählen Sie eine der Optionen aus, um [!DNL Graph Simulation] mit vorkonfigurierten Ereignissen und Algorithmen zu laden. Sie können weiterhin weitere Konfigurationen an allen vorab geladenen Diagrammszenarios vornehmen.

![Die für ein ungültiges Telefon konfigurierten Ereignisse und Algorithmen.](../images/graph-simulation/example-loaded.png)

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Simulieren]**.

![Ein Beispieldiagramm, das für ungültiges Telefon simuliert wird.](../images/graph-simulation/example-simulated.png)

### Textversion verwenden {#use-text-version}

Sie können auch den Textmodus verwenden, um Ereignisse zu konfigurieren. Um den Textmodus zu verwenden, wählen Sie das Einstellungssymbol und dann **[!UICONTROL Text (erweiterte Benutzer)]**.

![Das ausgewählte Einstellungssymbol.](../images/graph-simulation/settings.png)

Sie können Ihre Identitäten manuell im Textmodus eingeben. Verwenden Sie einen Doppelpunkt (`:`), um den Identitätswert zu unterscheiden, der dem eingegebenen Namespace entspricht, und verwenden Sie dann ein Komma (`,`), um Ihre Identitäten zu trennen. Um verschiedene Ereignisse voneinander zu unterscheiden, verwenden Sie für jedes Ereignis eine neue Zeile.

![Der Ereignisbereich, der die Textmodusversion verwendet.](../images/graph-simulation/text-version.png)

### Ereignis bearbeiten {#edit-event}

Um ein Ereignis zu bearbeiten, wählen Sie die Auslassungszeichen (`...`) neben einem bestimmten Ereignis aus und klicken Sie dann auf **[!UICONTROL Bearbeiten]**.

![Das Symbol &quot;Ereignis bearbeiten&quot;wurde ausgewählt.](../images/graph-simulation/edit.png)

### Ereignis löschen {#delete-event}

Um ein Ereignis zu löschen, wählen Sie die Auslassungszeichen (`...`) neben einem bestimmten Ereignis aus und klicken Sie auf **[!UICONTROL Löschen]**.

![Das Symbol zum Löschen eines Ereignisses wurde ausgewählt.](../images/graph-simulation/delete.png)

## Algorithmus konfigurieren {#configure-algorithm}

>[!IMPORTANT]
>
>Der von Ihnen konfigurierte Algorithmus bestimmt, wie Identity Service die in Ihre Ereignisse eingegebenen Namespaces behandelt. Alle Konfigurationen, die Sie in &quot;[!DNL Graph Simulation UI]&quot;zusammengestellt haben, werden nicht in den Identitätseinstellungen gespeichert.

Nachdem Sie Ihre Ereignisse hinzugefügt haben, können Sie jetzt den Algorithmus konfigurieren, der zur Simulation Ihres Diagramms verwendet wird. Wählen Sie zunächst **[!UICONTROL config hinzufügen]** aus.

![Das Konfigurationsfenster für den Algorithmus.](../images/graph-simulation/add-config.png)

Eine leere Konfigurationszeile wird angezeigt. Geben Sie zunächst den Namespace ein, den Sie für Ihre Ereignisse verwendet haben. Beginnen Sie in diesem Fall mit der Eingabe von E-Mail. Sobald Sie Ihren Namespace eingeben, werden die Spalten für [!UICONTROL Identitätssymbol] und [!UICONTROL Identitätstyp] automatisch ausgefüllt.

![Der erste Konfigurationseintrag.](../images/graph-simulation/add-namespace.png)

Wiederholen Sie die gleichen Schritte und fügen Sie den zweiten Namespace hinzu, in diesem Fall die ECID. Sobald alle Namespaces eingegeben wurden, können Sie mit der Konfiguration ihrer Prioritäten und Einzigartigkeit beginnen.

* **Namespace-Priorität**: Die Priorität eines Namespace bestimmt seine relative Bedeutung im Vergleich zu den anderen Namespaces in einem bestimmten Identitätsdiagramm. Wenn Ihr Identitätsdiagramm beispielsweise vier verschiedene Namespaces aufweist: CRM-ID, ECID, E-Mail und Apple IDFA, können Sie Prioritäten konfigurieren, um eine Reihenfolge von Bedeutung für den vier Namespace zu bestimmen.
* **Eindeutiger Namespace**: Wenn ein Namespace als eindeutig gekennzeichnet ist, generiert Identity Service Diagramme mit dem Vorbehalt, dass nur eine Identität mit einem bestimmten eindeutigen Namespace vorhanden sein kann. Wenn beispielsweise der E-Mail-Namespace als eindeutiger Namespace gekennzeichnet ist, kann ein Diagramm nur eine Identität mit E-Mail enthalten. Wenn mehr als eine Identität mit dem E-Mail-Namespace vorhanden ist, wird der älteste Link entfernt.

Um die Namespace-Priorität zu konfigurieren, wählen Sie die Namespace-Zeilen aus und ziehen Sie sie in die gewünschte Prioritätsreihenfolge, wobei die oberste Zeile die höhere Priorität und die untere Zeile die niedrigere Priorität darstellt. Um einen Namespace als eindeutig festzulegen, aktivieren Sie das Kontrollkästchen **[!UICONTROL Eindeutig pro Diagramm]** .

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Simulieren]**.

![Alle konfigurierten Namespaces.](../images/graph-simulation/all-namespaces.png)

## Simuliertes Diagramm anzeigen

Im Abschnitt [!UICONTROL Simuliertes Diagramm] werden die Identitätsdiagramme angezeigt, die basierend auf den von Ihnen hinzugefügten Ereignissen und dem von Ihnen konfigurierten Algorithmus generiert wurden.

| Diagrammsymbole | Beschreibung |
| --- | --- |
| Durchgehende Linie | Eine durchgehende Linie stellt eine festgestellte Verknüpfung zwischen zwei Identitäten dar. |
| gepunktete Linie | Eine gepunktete Linie stellt eine entfernte Verknüpfung zwischen zwei Identitäten dar. |
| Nummer in Zeilen | Eine Zahl in einer Zeile steht für den Zeitstempel des Zeitpunkts, zu dem der angegebene Link generiert wurde. Die niedrigste Zahl (1) stellt die früheste eingerichtete Verknüpfung dar. |

Im unten stehenden Beispieldiagramm existiert eine gepunktete Linie zwischen `{Email: tom@acme.com}` und `{ECID: 111}` aus folgenden Gründen:

* E-Mail wurde während des Algorithmuskonfigurationsschritts als eindeutig gekennzeichnet. Daher kann in einem Diagramm nur eine Identität mit einem E-Mail-Namespace vorhanden sein.
* Die Verknüpfung zwischen `{Email: tom@acme.com}` und `{ECID: 111}` war die erste festgestellte Identität (Ereignis #1). Es ist der älteste Link und wird daher entfernt.

![Der Viewer-Bereich für das simulierte Diagramm mit einem Beispiel für ein simuliertes Diagramm.](../images/graph-simulation/simulated-graph.png)

## Nächste Schritte

Durch Lesen dieses Dokuments wissen Sie jetzt, wie Sie mit dem Tool [!DNL Graph Simulation] besser verstehen können, wie Ihre Identitätsdaten mit bestimmten Regeln und Konfigurationen behandelt werden. Weitere Informationen finden Sie in den folgenden Dokumenten:

* [Verknüpfungsregeln für Identitätsdiagramme](overview.md)
* [Identitätsoptimierungsalgorithmus](identity-optimization-algorithm.md)
* [Namespace-Priorität](namespace-priority.md)
