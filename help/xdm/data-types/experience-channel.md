---
keywords: Experience Platform;Startseite;beliebte Themen;Schema;Schema;XDM;Felder;Schemata;Schemata;Webseitendetails;Datentyp;Datentyp;WebPage
solution: Experience Platform
title: Experience Channel-Datentyp
description: Erfahren Sie mehr über den Datentyp des Experience-Kanal-Experience-Datenmodells (XDM).
exl-id: 209654f7-0bde-439a-989c-ce2e41599105
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 24%

---

# Datentyp [!UICONTROL Experience]Kanal)

[!UICONTROL Experience Channel] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der einen Erlebniskanal beschreibt. Ein Erlebniskanal stellt eine Methode oder einen Pfad dar, mit der bzw. dem digitale Erlebnisse genutzt werden.

Es gibt mehrere Erlebniskanäle mit jeweils unterschiedlichen Einschränkungen, wie Inhalte bereitgestellt werden, wie die Kundeninteraktion beobachtet werden kann und wie Daten erfasst werden. Innerhalb eines Kanals können Erlebnisse an bestimmten Orten bereitgestellt werden. Die Standorte und Arten von Standorten, die in einem Kanal vorhanden sind, unterscheiden sich von Kanal zu Kanal.

![](../images/data-types/experience-channel.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_id` | Zeichenfolge | Eine ID, die den Kanal eindeutig identifiziert. Jeder spezifische Erlebniskanal definiert eine konstante `@id`. |
| `_type` | String | Bietet eine grobe Klassifizierungskennzeichnung für Kanäle mit ähnlichen Eigenschaften. |
| `contentTypes` | Zeichenfolgen-Array | Die Content-Typen, die dieser Kanal bereitstellen kann. |
| `locationTypes` | Zeichenfolgen-Array | Die Arten von Orten (virtuellen Orten), aus denen dieser Kanal besteht und an die Inhalte geliefert werden können. |
| `mediaAction` | String | Beschreibt eine Medienaktion für Erlebnisereignisse, falls zutreffend. |
| `mediaType` | String | Beschreibt, ob der Medientyp bezahlt, in Besitz oder verdient ist. |
| `metricTypes` | Zeichenfolgen-Array | Die Metriken, die in diesem Kanal erfasst werden können. |
| `mode` | String | Art und Weise, wie Erlebnisse in diesem Kanal bereitgestellt werden. |
| `typeAtSource` | String | Ein benutzerdefinierter Name für den Kanal. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/channels/channel.schema.json)
