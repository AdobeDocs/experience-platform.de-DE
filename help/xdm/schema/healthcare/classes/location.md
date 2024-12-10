---
title: Location Class
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

# [!UICONTROL Location] class

Im Experience-Datenmodell (XDM) erfasst die Klasse [!UICONTROL Ort] Informationen zum Live-Event-Standort, wie z. B. einen Reiseraum oder eine Sportarena.

![Location class structure](../../../images/healthcare/classes/location.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- | --- |
| [!UICONTROL ID] | `_id` | [!UICONTROL String] | Eine eindeutige, systemgenerierte Zeichenfolgenkennung für den Datensatz. Dieses Feld wird verwendet, um die Eindeutigkeit eines einzelnen Datensatzes zu verfolgen, Datenduplizierung zu verhindern und diesen Datensatz in nachgelagerten Diensten nachzuschlagen.<br><br>Da dieses Feld vom System generiert wird, muss es bei der Datenerfassung nicht explizit angegeben werden. Sie können jedoch weiterhin Ihre eigenen eindeutigen ID-Werte angeben, wenn Sie möchten. |
| [!UICONTROL Standort-ID] | `locationID` | [!UICONTROL String] | Eine eindeutige Kennung für den Standort. |
| [!UICONTROL Ortsname] | `locationName` | [!UICONTROL String] | Der Name des Standorts. |

Die Klasse kann mit der Feldergruppe [[!UICONTROL Position] ](../field-groups/location.md) erweitert werden, um weitere Details über einen Ort zu beschreiben.
