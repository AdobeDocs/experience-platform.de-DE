---
title: Location-Klasse
description: Erfahren Sie mehr über die Location-Klasse im Experience-Datenmodell (XDM).
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
exl-id: 1d100981-49fb-4f02-b2c6-324f9c541f76
source-git-commit: 3071d16b6b98040ea3f2e3a34efffae517253b8e
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 8%

---

# [!UICONTROL Location]-Klasse

Im Experience-Datenmodell (XDM) erfasst die [!UICONTROL Location]-Klasse Live-Informationen zum Veranstaltungsort, z. B. eine Reisehalle oder eine Sportarena.

![Standort-Klassenstruktur](../../../images/healthcare/classes/location.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL ID] | `_id` | [!UICONTROL String] | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes nachzuverfolgen, Doppelungen von Daten zu verhindern und diesen Datensatz in nachgelagerten Services nachzuschlagen.<br><br>Da dieses Feld systemgeneriert ist, muss bei der Datenaufnahme kein expliziter Wert angegeben werden. Sie können jedoch auch weiterhin eigene eindeutige ID-Werte angeben, wenn Sie dies wünschen. |
| [!UICONTROL Standortkennung] | `locationID` | [!UICONTROL String] | Eine eindeutige Kennung für den Speicherort. |
| [!UICONTROL Speicherort-Name] | `locationName` | [!UICONTROL String] | Der Name des Speicherorts. |

Die Klasse kann mit der Feldergruppe [[!UICONTROL Standort] erweitert werden, &#x200B;](../field-groups/location.md) weitere Details zu einem Standort zu beschreiben.
