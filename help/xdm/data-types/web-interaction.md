---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Web-Interaktion;Datentyp;Datentyp;Datentyp;
solution: Experience Platform
title: Datentyp Web Interaction
description: Erfahren Sie mehr über den Datentyp Web Interaction Experience Data Model (XDM).
exl-id: 772d96c5-9fa3-4fed-8b38-16b8e7101743
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 10%

---

# [!UICONTROL Web-Interaktion] Datentyp

[!UICONTROL Web Interaction] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Informationen zu Interaktionen beschreibt, die auf einer Web-Seite nach Abschluss des anfänglichen Seitenladevorgangs stattfanden. Sie ist für die Aufzeichnung von Interaktionen in Rich-Web-Anwendungen vorgesehen, die keinen Trigger für ein neues Laden von Seiten bieten, z. B. Single Page Web Apps (SPA).

<img src="../images/data-types/web-interaction.PNG" width="500" /><br />

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `linkClicks` | [[!UICONTROL Maßnahme]](./measure.md) | Eine Messung, die den Klick auf einen Weblink verfolgt. |
| `URL` | String | Der tatsächliche Link oder die URL, die für diese Web-Interaktion verwendet wird. |
| `name` | String | Der für diesen Weblink verwendete normative Name. Dies wird für Klassifizierungszwecke verwendet. |
| `type` | String | Der Link-Typ. Diese Eigenschaft muss einem der folgenden Enum-Werte entsprechen: <li> `download` </li> <li> `exit` </li> <li> `other` </li> |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/deprecated/webinteraction.schema.json)
