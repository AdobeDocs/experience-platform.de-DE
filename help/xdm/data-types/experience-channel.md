---
keywords: Experience Platform; Startseite; beliebte Themen; Schema; XDM; Felder; Schemas; Schemas; Webseitendetails; Datentyp; Datentyp; Datentyp; Datentyp; Webseite
solution: Experience Platform
title: Experience-Kanal-Datentyp
description: Dieses Dokument bietet einen Überblick über den Experience-Kanal-Datenmodell (XDM)-Datentyp.
exl-id: 209654f7-0bde-439a-989c-ce2e41599105
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 24%

---

# [!UICONTROL Experience-Kanal] Datentyp

[!UICONTROL Experience-Kanal] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der einen Erlebniskanal beschreibt. Ein Erlebniskanal stellt eine Methode oder einen Pfad für die Nutzung digitaler Erlebnisse dar.

Es gibt mehrere Erlebniskanäle mit jeweils unterschiedlichen Einschränkungen hinsichtlich der Bereitstellung von Inhalten, der Art und Weise, wie Kundeninteraktionen beobachtet werden können und wie Daten erfasst werden. Innerhalb eines Kanals können Erlebnisse an bestimmte Orte bereitgestellt werden. Die Standorte und Standorte in einem Kanal unterscheiden sich von Kanal zu Kanal.

![](../images/data-types/experience-channel.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_id` | Zeichenfolge | Eine ID, die den Kanal eindeutig identifiziert. Jeder spezifische Erlebniskanal definiert eine Konstante `@id`. |
| `_type` | Zeichenfolge | Bietet eine grobe Classification-Beschriftung für Kanäle mit ähnlichen Eigenschaften. |
| `contentTypes` | Zeichenfolgen-Array | Die Content-Typen, die dieser Kanal bereitstellen kann. |
| `locationTypes` | Zeichenfolgen-Array | Die Arten von Orten (virtuellen Orten), aus denen dieser Kanal besteht und an die Inhalte geliefert werden können. |
| `mediaAction` | Zeichenfolge | Beschreibt ggf. eine Medienaktion &quot;Erlebnisereignis&quot;. |
| `mediaType` | Zeichenfolge | Beschreibt, ob der Medientyp gebührenpflichtig, besessen oder verdient ist. |
| `metricTypes` | Zeichenfolgen-Array | Die Metriken, die in diesem Kanal erfasst werden können. |
| `mode` | Zeichenfolge | Art und Weise, wie Erlebnisse in diesem Kanal bereitgestellt werden. |
| `typeAtSource` | Zeichenfolge | Ein benutzerdefinierter Name für den Kanal. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
