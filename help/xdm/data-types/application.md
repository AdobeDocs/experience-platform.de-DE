---
keywords: Experience Platform;Home;beliebte Themen;Schema;Schema;XDM;Felder;Schemas;Schemas;Anwendung;Datentyp;Datentyp; Datentyp;
solution: Experience Platform
title: Anwendungsdatentyp
topic-legacy: overview
description: Dieses Dokument bietet eine Übersicht über den Datentyp des Application Experience Data Model (XDM).
exl-id: ac7d6761-7b58-4e0d-85e7-6f157fb2eea5
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '438'
ht-degree: 3%

---

#  Anwendungs-Datentyp

[!UICONTROL Bei ] Application handelt es sich um einen standardmäßigen XDM-Datentyp (Experience Data Model), der Details zu den von der Anwendung generierten Interaktionen beschreibt. Eine Anwendung bezieht sich auf ein Softwareerlebnis, z. B. eine Mobil- oder Desktopanwendung, die von einem Endbenutzer installiert, ausgeführt, geschlossen oder deinstalliert werden kann. Die Eigenschaften für diesen Datentyp sind nicht dazu gedacht, Agenten wie chatbots, browserbasierte Plugins oder andere Erlebnisse zu beschreiben, die nicht für Anwendungen gelten.

<img src="../images/data-types/application.PNG" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `applicationCloses` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt Details zum Beenden einer Anwendung. |
| `crashes` | [[!UICONTROL Maßnahme]](./measure.md) | Diese Eigenschaft wird Trigger, wenn die Anwendung nicht wie beabsichtigt beendet wird. |
| `featureUsages` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt Daten aus der Aktivierung einer zu messenden Anwendungsfunktion. |
| `firstLaunches` | [[!UICONTROL Maßnahme]](./measure.md) | Enthält Daten zum ersten Start. Diese Eigenschaft wird beim ersten Start nach einer Installation ausgelöst. |
| `installs` | [[!UICONTROL Maßnahme]](./measure.md) | Zeichnet die Installation einer Anwendung auf einem Gerät auf, wenn ein bestimmtes Ereignis verfügbar ist. |
| `launches` | [[!UICONTROL Maßnahme]](./measure.md) | Beschreibt einen Wert, der mit dem Start einer Anwendung verknüpft ist. Dies wird bei jeder Ausführung ausgelöst, einschließlich Abstürzen, Installationen und Wiederaufnahme aus dem Hintergrund, wenn der Sitzungs-Timeout überschritten wurde. |
| `upgrades` | [[!UICONTROL Maßnahme]](./measure.md) | Enthält Daten zur Aktualisierung einer Anwendung, die bereits installiert wurde. Dies wird beim ersten Start nach einer Aktualisierung ausgelöst. |
| `id` | Zeichenfolge | Eine eindeutige Kennung für die Anwendung. |
| `name` | Zeichenfolge | Der Name der Anwendung. |
| `userPerspective` | Zeichenfolge | Die Perspektive oder physische Beziehung zwischen dem Benutzer und der App oder Marke zum Zeitpunkt des Ereignisses. Die Kenntnis der Benutzerperspektive in Bezug auf die App hilft beim präzisen Generieren von Sitzungen, da die meiste Zeit keine `background`- und `detached`-Ereignis im Rahmen einer &quot;aktiven&quot;Sitzung enthalten sein sollen. Der Wert dieser Eigenschaft muss mit einem der unten aufgeführten Enum-Werte übereinstimmen. <li> `foreground`: Benutzer und App interagieren direkt miteinander. </li> <li> `background`: Die App und der Benutzer interagieren indirekt miteinander. Beispielsweise kann die App einen Wert messen und aktualisieren, während der Bildschirm gesperrt ist oder eine andere App im Vordergrund verwendet wird.  </li> <li> `detached`: &quot;Getrennt&quot;bedeutet, dass das Ereignis mit der App in Zusammenhang stand, aber nicht direkt von der App kam, z. B. das Senden einer E-Mail oder eine Push-Benachrichtigung von einem externen System. |
| `version` | Zeichenfolge | Die Version der Anwendung. |

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/application.schema.json)
