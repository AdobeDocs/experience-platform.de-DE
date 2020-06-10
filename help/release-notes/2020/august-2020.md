---
title: Adobe Experience Platform  – Versionshinweise
description: Versionshinweise zur Experience Platform vom 10. August 2020
doc-type: release notes
last-update: August 10, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 7f9d1120ac323c60f899cb1cf855e55db20437ed
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 17%

---


# Adobe Experience Platform – Versionshinweise

**Releasedatum: 10. Juni 2020**

Neue Funktionen in Adobe Experience Platform:

- [Zugangssteuerung](#access-control)
- [Sandboxes](#sandboxes)

## Zugangssteuerung {#access-control}

Die Experience Platform nutzt die [Adobe Admin Console](https://adminconsole.adobe.com) -Profil, um Benutzer mit Berechtigungen und Sandboxen zu verknüpfen. Berechtigungen steuern den Zugriff auf verschiedene Plattformfunktionen, einschließlich Datenmodellierung, Profil-Management und Sandbox-Verwaltung.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Zugriffsberechtigung | In der Admin-Konsole können Sie mithilfe der Registerkarte &quot; _Berechtigungen_ &quot;in einem Platform-Profil anpassen, welche Plattformfunktionen für die an dieses Profil angeschlossenen Benutzer verfügbar sind. Zu den verfügbaren Kategorien für Berechtigungen gehören: Datenmodellierung, Data Management, Profil-Management, Identitäten, Datenüberwachung, Sandbox-Administration, Ziele, Quellen. |
| Zugriff auf Sandboxen | Über die Registerkarte _Berechtigungen_ in einem Platform-Profil können Benutzer Zugriff auf bestimmte Sandboxen erhalten. Weitere Informationen finden Sie im Abschnitt zu [Sandboxen](#sandboxes) unten. |

Weitere Informationen finden Sie in der Übersicht über die [Zugriffskontrolle](../../access-control/home.md).

## Sandboxes {#sandboxes}

Die Experience Platform wurde entwickelt, um Anwendungen für digitale Erlebnisse auf globaler Ebene zu bereichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und implementieren, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss. Um diese Anforderungen zu erfüllen, stellt Experience Platform Sandboxes bereit, die eine Plattform-Instanz in separate virtuelle Umgebung unterteilen, um Anwendungen für digitale Erlebnisse zu entwickeln und weiterzuentwickeln.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Produktions-Sandbox | Experience Platform bietet eine einzige Produktions-Sandbox, die weder gelöscht noch zurückgesetzt werden kann. |
| Sandboxen ohne Produktion | Für eine einzige Plattforminstanz können mehrere Sandboxen ohne Produktionscharakter erstellt werden, mit denen Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen können, ohne die Produktionssandbox zu beeinträchtigen. |
| Sandbox-Umschalter | In der Benutzeroberfläche von Experience Platform können Sie mit dem Sandbox-Umschalter in der oberen linken Ecke des Bildschirms über ein Dropdown-Menü zwischen verfügbaren Sandboxen wechseln. |
| `x-sandbox-name` header | Alle Aufrufe von Experience Platform-APIs müssen jetzt die neue `x-sandbox-name` Kopfzeile enthalten, deren Wert auf das `name` Attribut der Sandbox verweist, in der der Vorgang ausgeführt wird. |

Weitere Informationen finden Sie in der [Sandbox-Übersicht](../../sandboxes/home.md).