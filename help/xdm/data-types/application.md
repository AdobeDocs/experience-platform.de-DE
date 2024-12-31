---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Anwendung;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Anwendungsdatentyp
description: Erfahren Sie mehr über den Datentyp des Experience-Anwendungsdatenmodells (XDM).
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 3%

---

# [!UICONTROL Anwendung] Datentyp

[!UICONTROL Application] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Details zu Interaktionen beschreibt, die von einer Anwendung generiert werden. Eine Anwendung bezieht sich auf ein Software-Erlebnis, z. B. eine Mobile- oder Desktop-Anwendung, die von einem Endbenutzer installiert, ausgeführt, geschlossen oder deinstalliert werden kann. Die Eigenschaften für diesen Datentyp sind nicht dazu gedacht, Agenten wie Chatbots, browserbasierte Plug-ins oder andere Erlebnisse zu beschreiben, die nicht für Programme gelten.

<img src="../images/data-types/application.PNG" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt Details zum Beenden einer Anwendung. |
| `crashes` | [[!UICONTROL Maßnahme]](./measure.md) | Diese Eigenschaft ist ein Trigger, wenn die Anwendung nicht wie beabsichtigt beendet wird. |
| `featureUsages` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt alle Daten aus der Aktivierung einer Anwendungsfunktion, die gemessen werden. |
| `firstLaunches` | [[!UICONTROL Maßnahme]](./measure.md) | Enthält Daten zum ersten Launch. Diese Eigenschaft wird beim ersten Start nach einer Installation ausgelöst. |
| `installs` | [[!UICONTROL Maßnahme]](./measure.md) | Zeichnet die Installation einer Anwendung auf einem Gerät auf, wenn ein bestimmtes Installationsereignis verfügbar ist. |
| `launches` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt einen Wert, der mit dem Start einer Anwendung verknüpft ist. Dies wird bei jeder Ausführung ausgelöst, einschließlich Abstürzen, Installationen und der Wiederaufnahme aus dem Hintergrund, wenn die maximale Wartezeit der Sitzung überschritten wurde. |
| `upgrades` | [[!UICONTROL Maßnahme]](./measure.md) | Enthält Daten zum Upgrade einer zuvor installierten Anwendung. Dies wird beim ersten Launch nach einem Upgrade ausgelöst. |
| `id` | String | Eine eindeutige Kennung für die Anwendung. |
| `name` | String | Der Name des Programms. |
| `userPerspective` | String | Die Perspektive oder physische Beziehung zwischen dem Benutzer und der App oder Marke zum Zeitpunkt des Ereignisses. Das Verständnis der Perspektive des Benutzers in Bezug auf die App hilft bei der genauen Erstellung von Sitzungen, da Sie in den meisten Fällen `background` und `detached` Ereignisse nicht als Teil einer „aktiven“ Sitzung einbeziehen möchten. Der Wert dieser Eigenschaft muss einem der unten aufgeführten Aufzählungswerte entsprechen. <li> `foreground`: Der Benutzer und die App interagieren direkt miteinander. </li> <li> `background`: Die App und der Benutzer interagieren indirekt miteinander. Beispielsweise könnte die App einen Wert messen und aktualisieren, während der Bildschirm gesperrt ist oder eine andere App im Vordergrund verwendet wird.  </li> <li> `detached`: Getrennt bedeutet, dass das Ereignis mit der App in Verbindung stand, aber nicht direkt von der App kam, z. B. das Senden einer E-Mail oder Push-Benachrichtigung von einem externen System. |
| `version` | String | Die Version des Programms. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
