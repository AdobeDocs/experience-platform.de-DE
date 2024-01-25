---
title: Identity Service-Verknüpfungslogik
description: Erfahren Sie, wie Identity Service-Links Identitäten verteilen, um eine umfassende Ansicht eines Kunden zu erstellen.
exl-id: 1c958c0e-0777-48db-862c-eb12b2e7a03c
source-git-commit: 2b6700b2c19b591cf4e60006e64ebd63b87bdb2a
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 1%

---

# Verknüpfungslogik für Identity Service

Eine Verknüpfung zwischen zwei Identitäten wird hergestellt, wenn der Identitäts-Namespace und die Identitätswerte übereinstimmen.

Es gibt zwei Arten von Identitäten, die verknüpft werden:

* **Profildatensätze**: Diese Identitäten stammen normalerweise aus CRM-Systemen.
* **Erlebnisereignisse**: Diese Identitäten stammen normalerweise aus der WebSDK-Implementierung oder der Adobe Analytics-Quelle.

## Semantische Bedeutung der Herstellung von Verbindungen

Eine Identität repräsentiert eine reale Einheit. Wenn eine Verbindung zwischen zwei Identitäten hergestellt wird, bedeutet dies, dass die beiden Identitäten miteinander verknüpft sind. Im Folgenden finden Sie einige Beispiele, die dieses Konzept illustrieren:

| Aktion | Verknüpfungen | Bedeutung |
| --- | --- | --- |
| Ein Endbenutzer meldet sich über einen Computer an. | CRM-ID und ECID werden miteinander verknüpft. | Eine Person (CRM-ID) besitzt ein Gerät mit einem Browser (ECID). |
| Endbenutzer navigieren anonym mit einer iPhone . | Der IDFA ist mit der ECID verknüpft. | Das Apple-Hardwaregerät (IDFA), z. B. ein iPhone, ist mit dem Browser (ECID) verknüpft. |
| Ein Endbenutzer meldet sich mit Google Chrome und dann Firefox an. | Die CRM-ID ist mit zwei verschiedenen ECIDs verknüpft. | Eine Person (CRM-ID) ist mit zwei Webbrowsern (**Hinweis**: Jeder Browser verfügt über eine eigene ECID.) |
| Ein Data Engineer erfasst einen CRM-Datensatz, der zwei Identitätsfelder enthält: CRM-ID und E-Mail. | CRM-ID und E-Mail sind verknüpft. | Eine Person (CRM-ID) ist mit der E-Mail-Adresse verknüpft. |

## Verstehen der Verknüpfungslogik des Identity Service

Eine Identität besteht aus einem Identitäts-Namespace und einem Identitätswert.

* Ein Identitäts-Namespace ist der Kontext eines bestimmten Identitätswerts. Häufige Beispiele für Identitäts-Namespaces sind CRM-ID, E-Mail und Telefon.
* Ein Identitätswert ist die Zeichenfolge, die eine reale Entität darstellt. Beispiel: &quot;julien<span>@acme.com&quot; kann ein Identitätswert für einen E-Mail-Namespace sein und 555-555-1234 kann ein entsprechender Identitätswert für einen Phone-Namespace sein.

>[!TIP]
>
>Der Identitäts-Namespace ist wichtig, da ohne ihn der Identitätswert seinen Kontext verliert und nicht über genügend Informationen verfügt, um Identitäten erfolgreich zuzuordnen.

In den folgenden Diagrammen finden Sie eine visuelle Darstellung der Funktionsweise der Identity Service-Verknüpfungslogik:

>[!BEGINTABS]

>[!TAB Vorhandenes Diagramm]

Angenommen, Sie verfügen über ein vorhandenes Identitätsdiagramm mit drei verknüpften Identitäten:

* TELEFON:(555)-555-1234
* EMAIL:julien<span>@acme.com
* CRM-ID:60013ABC

![vorhandenes Diagramm](../images/identity-settings/existing-graph.png)

>[!TAB Eingehende Daten]

Ein Paar Identitäten werden in Ihr Diagramm aufgenommen und dieses Paar enthält:

* CRM-ID:60013ABC
* ECID: 100066526

![eingehende Daten](../images/identity-settings/incoming-data.png)

>[!TAB Aktualisiertes Diagramm]

Identity Service erkennt, dass die CRM-ID:60013ABC bereits in Ihrem Diagramm vorhanden ist, sodass nur die neue ECID verknüpft wird.

![aktualisiertes Diagramm](../images/identity-settings/updated-graph.png)

>[!ENDTABS]

## Kundenszenario

Sie sind Dateningenieur und erfassen den folgenden CRM-Datensatz (Profildatensatz) zum Experience Platform.

| CRM-ID* | Phone* | E-Mail* | Vorname | Last name |
| --- | --- | --- | --- | --- |
| 60013ABC | 555-555-1234 | julien<span>@acme.com | Julien | Smith |
| 31260XYZ | 777-777-6890 | evan<span>@acme.com | Evan | Smith |

>[!NOTE]
>
>* `**` - Kennzeichnet das Feld, das als primäre Identität markiert ist.
>* `*` - Kennzeichnet das Feld, das als sekundäre Identität markiert ist.
>
>Identity Service unterscheidet nicht zwischen primärer und sekundärer Identität. Solange ein Feld als Identität markiert ist, wird es in Identity Service erfasst.

Sie haben auch WebSDK implementiert und einen WebSDK-Datensatz (Erlebnisereignis) mit den folgenden Datentabellen erfasst:

| Zeitstempel | Identitäten im Ereignis* | Ereignis |
| --- | --- | --- |
| `t=1` | ECID: 38652 | Startseite anzeigen |
| `t=2` | ECID:38652, CRM ID:31260XYZ | Suchen nach Schuhen |
| `t=3` | ECID: 44675 | Startseite anzeigen |
| `t=4` | ECID:44675, CRM ID: 31260XYZ | Kaufverlauf anzeigen |

Die primäre Identität für jedes Ereignis wird basierend auf [Konfigurieren von Datenelementtypen](../../tags/extensions/client/web-sdk/data-element-types.md).

>[!NOTE]
>
>* Wenn Sie die CRM-ID als primäre Kennung auswählen, haben authentifizierte Ereignisse (Ereignisse mit Identitätszuordnung, die die CRM-ID und ECID enthält) eine primäre Identität mit der CRM-ID. Für nicht authentifizierte Ereignisse (Ereignisse, bei denen die Identitätszuordnung nur ECID enthält) weist ECID als primäre Identität auf. Adobe empfiehlt diese Option.
>
>* Wenn Sie die ECID unabhängig vom Authentifizierungsstatus als primäre Identität auswählen, wird die ECID zur primären Identität.

In diesem Beispiel:

* `t=1`verwendet einen Desktop-Computer (ECID:38652) und zum anonymen Anzeigen des Durchsuchens der Homepage.
* `t=2`verwendet denselben Desktop-Computer, angemeldet (CRM ID:31260XYZ) und suchte dann nach Schuhen.
   * Sobald ein Benutzer angemeldet ist, sendet das Ereignis sowohl die ECID als auch die CRM-ID an den Identity Service.
* `t=3`, einen Laptop-Computer (ECID:44675) verwendet und anonym durchsucht.
* `t=4`verwendet denselben Laptop-Computer, angemeldet (CRM-ID: 31260XYZ) und anschließend den Kaufverlauf angezeigt.


>[!BEGINTABS]

>[!TAB timestamp=0]

At `timestamp=0`haben Sie zwei Identitätsdiagramme für zwei verschiedene Kunden. Beide sind jeweils durch drei verknüpfte Identitäten vertreten.

| | CRM-ID | E-Mail | Telefon |
| --- | --- | --- | --- |
| Customer One | 60013ABC | julien<span>@acme.com | 555-555-1234 |
| Kunde zwei | 31260XYZ | evan<span>@acme.com | 777-777-6890 |

![timestamp-zero](../images/identity-settings/timestamp-zero.png)

>[!TAB timestamp=1]

At `timestamp=1`verwendet ein Kunde einen Laptop, um Ihre E-Commerce-Website zu besuchen, Ihre Homepage anzuzeigen und anonym zu durchsuchen. Dieses anonyme Browsing-Ereignis wird als ECID:38652 identifiziert. Da Identity Service nur Ereignisse mit mindestens zwei Identitäten speichert, werden diese Informationen nicht gespeichert.

![timestamp-one](../images/identity-settings/timestamp-one.png)

>[!TAB timestamp=2]

At `timestamp=2`verwendet ein Kunde denselben Laptop, um Ihre E-Commerce-Website zu besuchen. Sie melden sich mit ihrer Benutzernamen- und Passwortkombination an und suchen nach Schuhen. Identity Service identifiziert das Konto des Kunden bei seiner Anmeldung, da es seiner CRM-ID entspricht: 31260XYZ. Darüber hinaus verknüpft Identity Service ECID:38562 mit CRM ID:31260XYZ, da beide denselben Browser auf demselben Gerät verwenden.

![timestamp-two](../images/identity-settings/timestamp-two.png)

>[!TAB timestamp=3]

At `timestamp=3` Ein Kunde verwendet ein Tablet, um Ihre E-Commerce-Website zu besuchen und anonym zu surfen. Dieses anonyme Browsing-Ereignis wird als ECID:44675 identifiziert. Da Identity Service nur Ereignisse mit mindestens zwei Identitäten speichert, werden diese Informationen nicht gespeichert.

![timestamp-three](../images/identity-settings/timestamp-three.png)

>[!TAB timestamp=4]

At `timestamp=4`verwendet ein Kunde dasselbe Tablet, meldet sich bei seinem Konto an (CRM ID:31260XYZ) und zeigt seinen Kaufverlauf an. Dieses Ereignis verknüpft ihre CRM-ID:31260XYZ mit der Cookie-ID, die der anonymen Browsing-Aktivität zugewiesen wurde, ECID:44675 und verknüpft ECID:44675 mit dem Identitätsdiagramm des Kunden.

![timestamp-four](../images/identity-settings/timestamp-four.png)

>[!ENDTABS]
