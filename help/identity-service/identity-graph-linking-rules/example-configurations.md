---
title: Beispielkonfigurationen
description: Erfahren Sie mehr über Beispielkonfigurationen mit dem Tool für die Diagrammsimulation.
badge: Beta
source-git-commit: 536770d0c3e7e93921fe40887dafa5c76e851f5e
workflow-type: tm+mt
source-wordcount: '814'
ht-degree: 12%

---

# Beispieldiagrammkonfigurationen

>[!AVAILABILITY]
>
>Die Regeln zur Verknüpfung von Identitätsdiagrammen befinden sich derzeit in der Beta-Phase. Wenden Sie sich an Ihr Adobe-Account-Team, um Informationen zu den Teilnahmekriterien zu erhalten. Die Funktion und die Dokumentation können sich ändern.

>[!NOTE]
>
>* &quot;CRMID&quot;und &quot;loginID&quot;sind benutzerdefinierte Namespaces. In diesem Dokument ist &quot;CRMID&quot;eine Personen-ID und &quot;loginID&quot;eine Anmelde-Kennung, die mit einer bestimmten Person verknüpft ist.
>* Um die in diesem Dokument beschriebenen Beispieldiagrammszenarien zu simulieren, müssen Sie zunächst zwei benutzerdefinierte Namespaces erstellen, einen mit dem Identitätssymbol &quot;CRMID&quot;und einen anderen mit dem Identitätssymbol &quot;loginID&quot;. Bei Identitätssymbolen wird zwischen Groß- und Kleinschreibung unterschieden.

In diesem Dokument werden Beispieldiagrammkonfigurationen allgemeiner Szenarien beschrieben, auf die Sie beim Arbeiten mit Identitätsdaten stoßen können.

## Nur CRMID

Dies ist ein Beispiel für ein einfaches Implementierungsszenario, bei dem Online-Ereignisse (CRMID und ECID) erfasst und Offline-Ereignisse (Profildatensätze) nur für die CRMID gespeichert werden.

**Implementierung:**

| Verwendete Namespaces | Webverhalten-Erfassungsmethode |
| --- | --- |
| CRMID, ECID | Web SDK |

**Ereignisse:**

Sie können dieses Szenario in der Diagrammsimulation erstellen, indem Sie die folgenden Ereignisse in den Textmodus kopieren:

* CRMID: Tom, ECID: 111

**Algorithmuskonfiguration:**

Sie können dieses Szenario in der Diagrammsimulation erstellen, indem Sie die folgende Einrichtung für Ihre Algorithmuskonfiguration konfigurieren:

| Priorität | Anzeigename | Identitätstyp | Eindeutig pro Diagramm |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Ja |
| 2 | ECID | COOKIE | Nein |

**Primäre Identitätsauswahl für Echtzeit-Kundenprofil:**

Im Kontext dieser Konfiguration wird die primäre Identität wie folgt definiert:

| Authentifizierungsstatus | Namespace(s) in Ereignissen | Primäre Identität |
| --- | --- | --- |
| Authentifiziert | CRMID, ECID | CRMID |
| Nicht authentifiziert | ECID | ECID |

>[!BEGINTABS]

>[!TAB Ideal single-person graph scenario]

Im Folgenden finden Sie ein Beispiel für ein ideales Diagramm für eine Einzelperson, in dem CRMID eindeutig ist und die höchste Priorität erhält.

![Ein simuliertes Beispiel für ein ideales Diagramm für eine Person, bei dem CRMID eindeutig ist und die höchste Priorität hat.](../images/graph-examples/crmid_only_single.png)

>[!TAB Diagramm für mehrere Personen]

Im Folgenden finden Sie ein Beispiel für ein Diagramm mit mehreren Personen. In diesem Beispiel wird ein Szenario mit einem &quot;freigegebenen Gerät&quot;angezeigt, in dem zwei CRMIDs vorhanden sind und die mit dem älteren eingerichteten Link entfernt wird.

![Ein simuliertes Beispiel für ein Diagramm mit mehreren Personen. In diesem Beispiel wird ein Szenario mit einem gemeinsam genutzten Gerät angezeigt, in dem zwei CRMIDs vorhanden sind und der ältere eingerichtete Link entfernt wird.](../images/graph-examples/crmid_only_multi.png)

>[!ENDTABS]

## CRMID mit Hash-E-Mail

In diesem Szenario wird eine CRMID erfasst und stellt sowohl Online- (Erlebnisereignis-) als auch Offline-Daten (Profildatensatz) dar. Dieses Szenario umfasst auch die Erfassung einer Hash-E-Mail, die einen anderen Namespace darstellt, der im CRM-Datensatz zusammen mit der CRMID gesendet wird.

**Implementierung:**

| Verwendete Namespaces | Webverhalten-Erfassungsmethode |
| --- | --- |
| CRMID, Email_LC_SHA256, ECID | Web SDK |

**Ereignisse:**

Sie können dieses Szenario in der Diagrammsimulation erstellen, indem Sie die folgenden Ereignisse in den Textmodus kopieren:

* CRMID: Tom, Email_LC_SHA256: tom<span>@acme.com
* CRMID: Tom, ECID: 111
* CRMID: Summer, Email_LC_SHA256: summer<span>@acme.com
* CRMID: Summer, ECID: 222

**Algorithmuskonfiguration:**

Sie können dieses Szenario in der Diagrammsimulation erstellen, indem Sie die folgende Einrichtung für Ihre Algorithmuskonfiguration konfigurieren:

| Priorität | Anzeigename | Identitätstyp | Eindeutig pro Diagramm |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Ja |
| 2 | E-Mails (SHA256, in Kleinbuchstaben) | E-Mail | Nein |
| 3 | ECID | COOKIE | Nein |

**Primäre Identitätsauswahl für Profil:**

Im Kontext dieser Konfiguration wird die primäre Identität wie folgt definiert:

| Authentifizierungsstatus | Namespace(s) in Ereignissen | Primäre Identität |
| --- | --- | --- |
| Authentifiziert | CRMID, ECID | CRMID |
| Nicht authentifiziert | ECID | ECID |

>[!BEGINTABS]

>[!TAB Ideal single-person graph scenario]

![In diesem Beispiel werden zwei separate Diagramme generiert, die jeweils eine Entität mit einer Person darstellen.](../images/graph-examples/crmid_hashed_single.png)

>[!TAB Diagramm für mehrere Personen: freigegebenes Gerät]

![In diesem Beispiel zeigt das simulierte Diagramm ein Szenario mit einem &quot;gemeinsam genutzten Gerät&quot;an, da sowohl Tom als auch Sommer mit derselben ECID verknüpft sind.](../images/graph-examples/crmid_hashed_shared_device.png)

>[!TAB Diagramm für mehrere Personen: nicht eindeutige E-Mail-Adresse]

![Dieses Szenario ähnelt einem Szenario vom Typ &quot;freigegebenes Gerät&quot;. Anstatt jedoch die ECID der Personenentitäten gemeinsam zu nutzen, sind sie stattdessen mit demselben E-Mail-Konto verknüpft.](../images/graph-examples/crmid_hashed_nonunique_email.png)

>[!ENDTABS]

## CRMID mit Hash-E-Mail, Hash-Telefon, GAID und IDFA

Dieses Szenario ähnelt dem vorherigen. In diesem Szenario werden Hash-E-Mails und -Telefone jedoch als Identitäten markiert, die bei der Segmentübereinstimmung verwendet werden sollen.

**Implementierung:**

| Verwendete Namespaces | Webverhalten-Erfassungsmethode |
| --- | --- |
| CRMID, Email_LC_SHA256, Phone_SHA256, GAID, IDFA, ECID | Web SDK |

**Ereignisse:**

Sie können dieses Szenario in der Diagrammsimulation erstellen, indem Sie die folgenden Ereignisse in den Textmodus kopieren:

* CRMID: Tom, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRMID: Tom, ECID: 111
* CRMID: Tom, ECID: 222, IDFA: A-A-A
* CRMID: Summer, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRMID: Summer, ECID: 333
* CRMID: Summer, ECID: 444, GAID:B-B-B

**Algorithmuskonfiguration:**

Sie können dieses Szenario in der Diagrammsimulation erstellen, indem Sie die folgende Einrichtung für Ihre Algorithmuskonfiguration konfigurieren:

| Priorität | Anzeigename | Identitätstyp | Eindeutig pro Diagramm |
| ---| --- | --- | --- |
| 1 | CRMID | CROSS_DEVICE | Ja |
| 2 | E-Mails (SHA256, in Kleinbuchstaben) | E-Mail | Nein |
| 3 | Telefon (SHA256) | Telefon | Nein |
| 4 | Google Ad ID (GAID) | GERÄT | Nein |
| 5 | Apple IDFA (ID für Apple) | GERÄT | Nein |
| 6 | ECID | COOKIE | Nein |

**Primäre Identitätsauswahl für Profil:**

Im Kontext dieser Konfiguration wird die primäre Identität wie folgt definiert:

| Authentifizierungsstatus | Namespace(s) in Ereignissen | Primäre Identität |
| --- | --- | --- |
| Authentifiziert | CRMID, IDFA, ECID | CRMID |
| Authentifiziert | CRMID, GAID, ECID | CRMID |
| Authentifiziert | CRMID, ECID | CRMID |
| Nicht authentifiziert | GAID, ECID | GAID |
| Nicht authentifiziert | IDFA, ECID | IDFA |
| Nicht authentifiziert | ECID | ECID |

>[!BEGINTABS]

>[!TAB Ideal single-person graph scenario]

![](../images/graph-examples/crmid_hashed_single_seg_match.png)

>[!ENDTABS]

<!-- 
## Single CRMID with multiple login IDs (simple)

In this scenario, there is a single CRMID that represents a person entity. However, a person entity may have multiple login identifiers:

* A given person entity can have different account account types (personal vs. business, account by state, account by brand, etc.)
* A given person entity may use different email addresses for any number of accounts.

Therefore, **it is crucial that the CRMID is always sent for every user**. Failure to do so may result in a "dangling" login ID scenario, where a single person entity is assumed to be sharing a device with another person.

**Implementation:**

| Namespaces used | Web behavior collection method |
| --- | --- |
| CRMID, loginID, ECID | Web SDK |

**Events:**

You can create this scenario in graph simulation by copying the following events to text mode:

* CRMID: John, loginID: ID_A
* CRMID: John, loginID: ID_B
* loginID: ID_A, ECID: 111
* CRMID: Jane, loginID: ID_C
* CRMID: Jane, loginID: ID_D
* loginID: ID_C, ECID: 222

**Algorithm configuration:**

You can create this scenario in graph simulation by configuring the following setup for your algorithm configuration:

| Priority | Display name | Identity symbol | Identity type | Unique per graph |
| ---| --- | --- | --- | --- |
| 1 | CRMID | CRMID | CROSS_DEVICE | Yes |
| 2 | loginID | loginID | CROSS_DEVICE | No |
| 3 | ECID | ECID | COOKIE | No |

## Single CRMID with multiple login IDs (complex)

In this scenario, there is a single CRMID that represents a person entity. However, a person entity may have multiple login identifiers:

* A given person entity can have different account account types (personal vs. business, account by state, account by brand, etc.)
* A given person entity may use different email addresses for any number of accounts.

The case of "dangling" loginID also applies for this scenario.

**Implementation:**

| Namespaces used | Web behavior collection method |
| --- | --- |
| CRMID, Email_LC_SHA256, Phone_SHA256, loginID, ECID, AAID | Adobe Analytics source connector |


**Events:**

You can create this scenario in graph simulation by copying the following events to text mode:

* CRMID: John, Email_LC_SHA256: aabbcc, Phone_SHA256: 123-4567
* CRMID: John, loginID: ID_A
* CRMID: John, loginID: ID_B
* loginID:ID_A, ECID: 111, AAID: AAA
* CRMID: Jane, Email_LC_SHA256: ddeeff, Phone_SHA256: 765-4321
* CRMID: Jane, loginID: ID_C
* CRMID: Jane, loginID: ID_D
* loginID: ID_C, ECID: 222, AAID: BBB

**Algorithm configuration:**

You can create this scenario in graph simulation by configuring the following setup for your algorithm configuration:

| Priority | Display name | Identity symbol | Identity type | Unique per graph |
| ---| --- | --- | --- | --- |
| 1 | CRMID | CRMID | CROSS_DEVICE | Yes |
| 2 | Email_LC_SHA256 | Email_LC_SHA256 | EMAIL | No |
| 3 | Phone_SHA256 | Phone_SHA256 | PHONE | No |
| 4 | loginID | loginID | CROSS_DEVICE | No |
| 5 | ECID | ECID | COOKIE | No |
| 6 | AAID | AAID | COOKIE | No |
 -->
