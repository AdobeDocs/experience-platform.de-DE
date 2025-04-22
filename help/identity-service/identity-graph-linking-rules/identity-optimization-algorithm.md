---
title: Algorithmus zur Identitätsoptimierung
description: Erfahren Sie mehr über den Algorithmus zur Identitätsoptimierung in Identity Service.
exl-id: 5545bf35-3f23-4206-9658-e1c33e668c98
source-git-commit: a309f0dca5ebe75fcb7abfeb98605aec2692324d
workflow-type: tm+mt
source-wordcount: '1617'
ht-degree: 5%

---

# Algorithmus zur Identitätsoptimierung {#identity-optimization-algorithm}

>[!CONTEXTUALHELP]
>id="platform_identities_uniquenamespace"
>title="Eindeutiger Namespace"
>abstract="Ein Diagramm darf nicht zwei Identitäten mit einem eindeutigen Namespace aufweisen. Wenn ein Diagramm versucht, dieses Limit zu überschreiten, werden die neuesten Links beibehalten und die ältesten Links entfernt."

>[!AVAILABILITY]
>
>Regeln zur Identitätsdiagramm-Verknüpfung sind derzeit nur eingeschränkt verfügbar und können von allen Kunden in Entwicklungs-Sandboxes aufgerufen werden.
>
>* **Aktivierungsanforderungen**: Die Funktion bleibt inaktiv, bis Sie Ihre [!DNL Identity Settings] konfigurieren und speichern. Ohne diese Konfiguration funktioniert das System weiterhin normal, ohne dass sich das Verhalten ändert.
>* **Wichtige Hinweise**: Während dieser eingeschränkten Verfügbarkeitsphase kann die Segmentierung nach Edge zu unerwarteten Segmentzugehörigkeitsergebnissen führen. Streaming und Batch-Segmentierung funktionieren jedoch erwartungsgemäß.
>* **Nächste Schritte**: Informationen zum Aktivieren dieser Funktion in Produktions-Sandboxes erhalten Sie von Ihrem Adobe-Account-Team.

Der Identitätsoptimierungsalgorithmus ist ein Diagrammalgorithmus in Identity Service, der sicherstellt, dass ein Identitätsdiagramm für eine einzelne Person repräsentativ ist, und daher das unerwünschte Zusammenführen von Identitäten im Echtzeit-Kundenprofil verhindert.

## Eingabeparameter {#input-parameters}

In diesem Abschnitt finden Sie Informationen zu eindeutigen Namespaces und Namespace-Priorität. Diese beiden Konzepte dienen als Eingabeparameter, die für den Algorithmus zur Identitätsoptimierung erforderlich sind.

### Eindeutiger Namespace {#unique-namespace}

Ein eindeutiger Namespace bestimmt die Links, die entfernt werden, wenn das Diagramm reduziert wird.

Ein einzelnes zusammengeführtes Profil und das zugehörige Identitätsdiagramm sollten eine einzelne Person (Entität) darstellen. Eine einzelne Person wird in der Regel durch CRMIDs und/oder Anmelde-IDs dargestellt. Es wird erwartet, dass keine zwei Personen (CRMIDs) zu einem einzigen Profil oder Diagramm zusammengeführt werden.

Sie müssen mithilfe des Identitätsoptimierungs-Algorithmus angeben, welche Namespaces eine Personenentität im Identity Service darstellen. Wenn eine CRM-Datenbank beispielsweise ein Benutzerkonto definiert, das mit einer einzelnen CRMID und einer einzelnen E-Mail-Adresse verknüpft werden soll, würden die Identitätseinstellungen für diese Sandbox wie folgt aussehen:

* CRMID-Namespace = eindeutig
* E-Mail-Namespace = eindeutig

Ein Namespace, den Sie als eindeutig deklarieren, wird automatisch so konfiguriert, dass er innerhalb eines bestimmten Identitätsdiagramms eine maximale Anzahl von 1 aufweist. Wenn Sie beispielsweise einen CRMID-Namespace als eindeutig deklarieren, kann ein Identitätsdiagramm nur eine Identität haben, die einen CRMID-Namespace enthält. Wenn Sie einen Namespace nicht als eindeutig deklarieren, kann das Diagramm mehr als eine Identität mit diesem Namespace enthalten.

>[!NOTE]
>
>* Die Darstellung von Haushaltsentitäten („Haushaltsdiagramme„) wird derzeit nicht unterstützt.
>
>* Alle Namespaces, bei denen es sich um Personen-IDs handelt und die in der Sandbox zum Generieren von Identitätsdiagrammen verwendet werden, müssen als eindeutiger Namespace markiert werden. Andernfalls kann es zu unerwünschten Verknüpfungsergebnissen kommen.

### Namespace-Priorität {#namespace-priority}

Die Namespace-Priorität bestimmt, wie der Algorithmus zur Identitätsoptimierung Links entfernt.

Namespaces in Identity Service haben eine implizite relative Wichtigkeitsreihenfolge. Betrachten wir ein Diagramm, das wie eine Pyramide strukturiert ist. Es gibt einen Knoten auf der oberen Ebene, zwei Knoten auf der mittleren Ebene und vier Knoten auf der unteren Ebene. Die Namespace-Priorität muss diese relative Reihenfolge widerspiegeln, um sicherzustellen, dass eine Personenentität korrekt dargestellt wird.

Einen detaillierten Überblick über die Namespace-Priorität und ihre vollständigen Funktionen und Verwendungen finden Sie im [Handbuch zur Namespace-Priorität](./namespace-priority.md).

![Diagrammebenen und Namespace-Priorität](../images/namespace-priority/graph-layers.png)

## Prozess {#process}

Bei der Aufnahme neuer Identitäten prüft Identity Service, ob die neuen Identitäten und die entsprechenden Namespaces den eindeutigen Namespace-Konfigurationen entsprechen. Wenn die Konfigurationen befolgt werden, wird die Aufnahme fortgesetzt und die neuen Identitäten werden mit dem Diagramm verknüpft. Wenn die Konfigurationen jedoch nicht befolgt werden, wird der Algorithmus zur Identitätsoptimierung:

* Nehmen Sie unter Berücksichtigung der Namespace-Priorität das neueste Ereignis auf.
* Entfernen Sie die Relation, die zwei Personenentitäten aus der entsprechenden Diagrammschicht zusammenführen würde.

## Details zum Identitätsoptimierungsalgorithmus

Wenn die Eindeutigkeits-Namespace-Beschränkung verletzt wird, gibt der Algorithmus für die Identitätsoptimierung die Links „erneut wieder“ und erstellt das Diagramm von Grund auf neu.

* Links werden nach der folgenden Reihenfolge sortiert:
   * Letztes Ereignis.
   * Zeitstempel nach Summe der Namespace-Priorität (niedrigere Summe = höhere Reihenfolge).
* Das Diagramm wird basierend auf der obigen Reihenfolge wiederhergestellt. Wenn das Hinzufügen des Links gegen die Beschränkung verstößt (z. B. wenn das Diagramm zwei oder mehr Identitäten mit einem eindeutigen Namespace enthält), werden die Links entfernt.
* Das resultierende Diagramm ist dann mit der konfigurierten Beschränkung für eindeutige Namespaces konform.

![Ein Diagramm, das den Algorithmus zur Identitätsoptimierung visualisiert.](../images/ido_algorithm.png)

## Beispielszenarien für den Algorithmus zur Identitätsoptimierung

Im folgenden Abschnitt wird beschrieben, wie sich der Algorithmus zur Identitätsoptimierung unter Szenarien wie einem gemeinsam genutzten Gerät oder der Aufnahme von Daten mit demselben Zeitstempel verhält.

### Freigegebenes Gerät

Ein gemeinsam genutztes Gerät bezieht sich auf ein Gerät, das von mehr als einer Person verwendet wird. Ein gemeinsam genutztes Gerät kann beispielsweise ein Laptop oder ein Tablet sein, den Sie mit einem Partner oder Familienmitglied, einem Bibliothekscomputer oder einem öffentlichen Kiosk teilen.

>[!BEGINTABS]

>[!TAB Beispiel 1]

| Namespace | Eindeutiger Namespace |
| --- | --- |
| CRMID | Ja |
| E-Mail | Ja |
| ECID | Nein |

In diesem Beispiel werden sowohl CRMID als auch E-Mail als eindeutige Namespaces bezeichnet. `timestamp=0` wird ein CRM-Datensatz aufgenommen, der aufgrund der eindeutigen Namespace-Konfiguration zwei verschiedene Diagramme erstellt. Jedes Diagramm enthält eine CRMID und einen E-Mail-Namespace.

* `timestamp=1`: Jane meldet sich mit einem Laptop bei Ihrer E-Commerce-Website an. Jane wird durch ihre CRMID und E-Mail dargestellt, während der Webbrowser auf ihrem Laptop, den sie verwendet, durch eine ECID dargestellt wird.
* `timestamp=2`: John meldet sich mit demselben Laptop bei Ihrer E-Commerce-Website an. John wird durch seine CRMID und E-Mail dargestellt, während der von ihm verwendete Webbrowser bereits durch eine ECID dargestellt wird. Da dieselbe ECID mit zwei verschiedenen Diagrammen verknüpft ist, kann Identity Service erkennen, dass dieses Gerät (Laptop) ein gemeinsam genutztes Gerät ist.
* Aufgrund der eindeutigen Namespace-Konfiguration, die pro Diagramm maximal einen CRMID-Namespace und einen E-Mail-Namespace festlegt, teilt der Identitätsoptimierungsalgorithmus das Diagramm jedoch in zwei Teile auf.
   * Da John der letzte authentifizierte Benutzer ist, bleibt die ECID für den Laptop mit seinem Diagramm verknüpft statt mit dem von Jane.

![Freigegebener Gerätefall eins](../images/identity-settings/shared-device-case-one.png)

>[!TAB Beispiel 2]

| Namespace | Eindeutiger Namespace |
| --- | --- |
| CRMID | Ja |
| ECID | Nein |

In diesem Beispiel wird der CRMID-Namespace als eindeutiger Namespace bezeichnet.

* `timestamp=1`: Jane meldet sich mit einem Laptop bei Ihrer E-Commerce-Website an. Sie wird durch ihre CRMID und der Webbrowser auf dem Laptop durch die ECID dargestellt.
* `timestamp=2`: John meldet sich mit demselben Laptop bei Ihrer E-Commerce-Website an. Er wird durch seine CRMID und den von ihm verwendeten Webbrowser durch dieselbe ECID dargestellt.
   * Dieses Ereignis verknüpft zwei unabhängige CRMIDs mit derselben ECID, wodurch das konfigurierte Limit von einer CRMID überschritten wird.
   * Infolgedessen entfernt der Identitätsoptimierungsalgorithmus den älteren Link, in diesem Fall die CRMID von Jane, die unter `timestamp=1` verknüpft war.
   * Während Janes CRMID jedoch nicht mehr als Diagramm auf Identity Service vorhanden ist, bleibt sie weiterhin als Profil im Echtzeit-Kundenprofil bestehen. Dies liegt daran, dass ein Identitätsdiagramm mindestens zwei verknüpfte Identitäten enthalten muss und dass infolge des Entfernens der Links Janes CRMID keine andere Identität mehr hat, mit der sie eine Verknüpfung herstellen kann.

![shared-device-case-two](../images/identity-settings/shared-device-case-two.png)

>[!ENDTABS]

### Fehlerhafte E-Mail

Es gibt Fälle, in denen Benutzende fehlerhafte Werte für ihre E-Mail-Adresse und/oder Telefonnummern eingeben können.

| Namespace | Eindeutiger Namespace |
| --- | --- |
| CRMID | Ja |
| E-Mail | Ja |
| ECID | Nein |

In diesem Beispiel werden die Namespaces CRM und E-Mail als eindeutig gekennzeichnet. Betrachten wir das Szenario, in dem Jane und John sich mit einem ungültigen E-Mail-Wert auf Ihrer E-Commerce-Website angemeldet haben (z. B. test<span>@test.com).

* `timestamp=1`: Jane meldet sich über Safari auf ihrer iPhone bei Ihrer E-Commerce-Website an und erstellt ihre CRMID (Anmeldeinformationen) und ihre ECID (Browser).
* `timestamp=2`: John meldet sich auf seiner iPhone mit Google Chrome bei Ihrer E-Commerce-Website an und legt seine CRMID (Anmeldeinformationen) und ECID (Browser) fest.
* `timestamp=3`: Ihr Datentechniker nimmt Janes CRM-Datensatz auf, was dazu führt, dass ihre CRMID mit der fehlerhaften E-Mail verknüpft wird.
* `timestamp=4`: Ihr Dateningenieur nimmt Johns CRM-Datensatz auf, was dazu führt, dass seine CRMID mit der fehlerhaften E-Mail verknüpft wird.
   * Dies wird dann zu einem Verstoß gegen die Konfiguration eindeutiger Namespaces, da ein einzelnes Diagramm mit zwei CRMID-Namespaces erstellt wird.
   * Daher löscht der Identitätsoptimierungsalgorithmus die ältere Verknüpfung, in diesem Fall die Verknüpfung zwischen der Identität von Jane mit dem CRMID-Namespace und der Identität mit dem Test<span>@test.

Bei einem Algorithmus zur Identitätsoptimierung werden fehlerhafte Identitätswerte wie falsche E-Mails oder Telefonnummern nicht auf mehrere verschiedene Identitätsdiagramme übertragen.

![bad-email](../images/identity-settings/bad-email.png)

### Anonyme Ereignisverknüpfung

ECIDs speichern nicht authentifizierte (anonyme) Ereignisse, während CRMID authentifizierte Ereignisse speichert. Bei gemeinsam genutzten Geräten wird die ECID (Träger nicht authentifizierter Ereignisse) mit dem (**authentifizierten)** verknüpft.

Sehen Sie sich das folgende Diagramm an, um besser zu verstehen, wie die anonyme Ereigniszuordnung funktioniert:

* Kevin und Nora teilen sich ein Tablet.
   * `timestamp=1`: Kevin meldet sich über sein Konto bei einer E-Commerce-Website an und stellt dabei seine CRMID (Anmeldeinformationen) und eine ECID (Browser) fest. Zum Zeitpunkt der Anmeldung gilt Kevin jetzt als der letzte authentifizierte Benutzer.
   * `timestamp=2`: Nora meldet sich mit ihrem Konto bei einer E-Commerce-Website an und stellt dabei ihre CRMID (Anmeldeinformationen) und dieselbe ECID fest. Zum Zeitpunkt der Anmeldung wird Nora jetzt als der letzte authentifizierte Benutzer betrachtet.
   * `timestamp=3`: Kevin verwendet das Tablet, um die E-Commerce-Website zu durchsuchen, meldet sich jedoch nicht mit seinem Konto an. Kevins Navigationsaktivitäten werden dann in der ECID gespeichert, die wiederum mit Nora verknüpft ist, da sie die letzte authentifizierte Benutzerin bzw. der letzte authentifizierte Benutzer ist. Zu diesem Zeitpunkt ist Nora Eigentümerin der anonymen Ereignisse.
      * Bis sich Kevin erneut anmeldet, wird das zusammengeführte Nora-Profil mit allen nicht authentifizierten Ereignissen verknüpft, die für die ECID gespeichert sind (wobei Ereignisse sind, bei denen ECID die primäre Identität ist).
   * `timestamp=4`: Kevin meldet sich ein zweites Mal an. An dieser Stelle wird er erneut der letzte authentifizierte Benutzer und steuert jetzt auch die nicht authentifizierten Ereignisse:
      * vor seiner ersten Anmeldung vor dem `timestamp=1` und
      * Alle Aktivitäten, die er oder Nora beim anonymen Durchsuchen zwischen Kevins ersten und zweiten Anmeldedaten ausgeführt haben.

![anon-event-associated](../images/identity-settings/anon-event-association.png)


## Nächste Schritte

Weitere Informationen zu [!DNL Identity Graph Linking Rules] finden Sie in der folgenden Dokumentation:

* [[!DNL Identity Graph Linking Rules] – Übersicht](./overview.md)
* [Implementierungshandbuch](./implementation-guide.md)
* [Beispiele für Diagrammkonfigurationen](./example-configurations.md)
* [Fehlerbehebung und häufig gestellte Fragen](./troubleshooting.md)
* [Namespace-Priorität](./namespace-priority.md)
* [Benutzeroberfläche für die Diagrammsimulation](./graph-simulation.md)
* [Benutzeroberfläche für Identitätseinstellungen](./identity-settings-ui.md)