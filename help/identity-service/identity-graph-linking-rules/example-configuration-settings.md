---
title: Beispielkonfigurationen
description: Erfahren Sie mehr über Beispielkonfigurationen mit dem Tool für die Diagrammsimulation.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: ba72abd9febc6d9e6491748519199b54a26ae1c5
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 21%

---

# Beispieldiagrammkonfigurationen

>[!NOTE]
>
>&quot;CRM-ID&quot;ist ein benutzerdefinierter Namespace. Daher müssen Sie in den unten stehenden Beispielen einen benutzerdefinierten Namespace mit einem Anzeigenamen und Identitätssymbol von &quot;CRM ID&quot;erstellen.

Im folgenden Abschnitt finden Sie Beispiele für Diagrammszenarien, auf die Sie bei der Diagrammsimulation stoßen können.

## Nur CRM-ID

Ereignisse:

* CRM-ID: Tom, ECID: 111

Algorithmuskonfiguration:

| Priorität | Anzeigename | Identitätssymbol | Identitätstyp | Nur einmal im Diagramm |
| ---| --- | --- | --- | --- |
| 1 | CRM-ID | CRM-ID | CROSS_DEVICE | Ja |
| 2 | ECID | ECID | COOKIE | NO |

+++Auswählen zum Anzeigen des simulierten Diagramms

+++

## CRM-ID mit gehashter E-Mail

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

## CRM-ID mit Hash-E-Mail, Hash-Telefon, GAID und IDFA

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