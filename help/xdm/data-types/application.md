---
keywords: Experience Platform; home; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Anwendung; Datentyp; Datentyp; Datentyp;
solution: Experience Platform
title: Anwendungsdatentyp
description: Erfahren Sie mehr über den Datentyp des Anwendungs-Experience-Datenmodells (XDM).
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '416'
ht-degree: 3%

---

# [!UICONTROL Application]-Datentyp

[!UICONTROL Anwendung] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der Details zu von einer Anwendung generierten Interaktionen beschreibt. Eine Anwendung bezieht sich auf ein Softwareerlebnis, z. B. eine mobile oder Desktop-Anwendung, die von einem Endbenutzer installiert, ausgeführt, geschlossen oder deinstalliert werden kann. Die Eigenschaften für diesen Datentyp sind nicht zur Beschreibung von Agenten wie Chatbots, browserbasierten Plugins oder anderen Erlebnissen gedacht, die nicht für Anwendungen gelten.

<img src="../images/data-types/application.PNG" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt Details zum Beenden einer Anwendung. |
| `crashes` | [[!UICONTROL Maßnahme]](./measure.md) | Diese Eigenschaft wird Trigger, wenn die Anwendung nicht wie gewünscht beendet wird. |
| `featureUsages` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt alle Daten aus der Aktivierung einer zu messenden Anwendungsfunktion. |
| `firstLaunches` | [[!UICONTROL Maßnahme]](./measure.md) | Enthält Daten zum ersten Start. Diese Eigenschaft wird beim ersten Start nach einer Installation ausgelöst. |
| `installs` | [[!UICONTROL Maßnahme]](./measure.md) | Zeichnet die Installation einer Anwendung auf einem Gerät auf, wenn ein bestimmtes Installationsereignis verfügbar ist. |
| `launches` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt einen Wert, der mit dem Start einer Anwendung verknüpft ist. Dies wird bei jeder Ausführung ausgelöst, einschließlich Abstürzen, Installationen und der Wiederaufnahme aus dem Hintergrund, wenn das Sitzungs-Timeout überschritten wurde. |
| `upgrades` | [[!UICONTROL Maßnahme]](./measure.md) | Enthält Daten zum Upgrade einer bereits installierten Anwendung. Diese wird beim ersten Start nach einem Upgrade ausgelöst. |
| `id` | Zeichenfolge | Eine eindeutige Kennung für die Anwendung. |
| `name` | Zeichenfolge | Der Name der Anwendung. |
| `userPerspective` | Zeichenfolge | Die Perspektive oder physische Beziehung zwischen dem Benutzer und der App oder Marke zum Zeitpunkt des Ereignisses. Das Verständnis der Perspektive des Benutzers im Verhältnis zur App hilft bei der präzisen Generierung von Sitzungen, da Sie in der Mehrzahl der Fälle keine `background` - und `detached` -Ereignisse als Teil einer &quot;aktiven&quot;Sitzung einbeziehen möchten. Der Wert dieser Eigenschaft muss mit einem der unten aufgeführten Enum-Werte übereinstimmen. <li> `foreground`: Benutzer und App interagieren direkt miteinander. </li> <li> `background`: Die App und der Benutzer interagieren indirekt. Beispielsweise kann das Programm einen Wert messen und aktualisieren, während der Bildschirm gesperrt ist oder eine andere App im Vordergrund verwendet wird.  </li> <li> `detached`: Getrennt bedeutet, dass das Ereignis mit der App in Verbindung stand, aber nicht direkt von der App kam, z. B. das Senden einer E-Mail oder einer Push-Benachrichtigung von einem externen System. |
| `version` | Zeichenfolge | Die Version der Anwendung. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
