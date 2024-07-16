---
title: Datentyp der Postanschrift
description: Erfahren Sie mehr über den Datentyp "Postal Address Experience Data Model (XDM)".
exl-id: 92385cd8-60c8-4360-a8e7-e6224e85e4d4
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 51%

---

# Datentyp [!UICONTROL Postanschrift]

[!UICONTROL Postanschrift] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Details zu Adressen bereitstellt.

![Ein Diagramm des Datentyps [!UICONTROL Postanschrift].](../images/data-types/postal-address.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Primär] | `primary` | Boolescher Wert | Primärer Adressindikator. Ein Profil kann zu einem bestimmten Zeitpunkt nur eine `primary` -Adresse haben. |
| [!UICONTROL Titel] | `label` | Zeichenfolge | Freiformname der Adresse. |
| [!UICONTROL Straße 1] | `street1` | Zeichenfolge | Primäre Informationen zu Straße, Wohnungsnummer, Straßennummer und Straßennamen. |
| [!UICONTROL Straße 2] | `street2` | Zeichenfolge | Optionale Straßeninformationen, zweite Zeile. |
| [!UICONTROL Straße 3] | `street3` | Zeichenfolge | Optionale Straßeninformationen, dritte Zeile. |
| [!UICONTROL Straße 4] | `street4` | Zeichenfolge | Optionale Straßeninformationen, vierte Zeile. |
| [!UICONTROL Region] | `region` | Zeichenfolge | Die Region, der Kreis oder der Bezirk der Adresse. |
| [!UICONTROL Post Office Box] | `postOfficeBox` | Zeichenfolge | Postfach der Adresse. |
| [!UICONTROL Country] | `country` | Zeichenfolge | Der Name des von der Regierung verwalteten Gebiets. Mit Ausnahme von ``countryCode`` ist dies ein Freiformfeld, das den Ländernamen in jeder Sprache enthalten kann. |
| [!UICONTROL state] | `state` | Zeichenfolge | Der Name des Landes. Dies ist ein Freiformfeld. |
| [!UICONTROL Status] | `status` | Zeichenfolge | Ein Hinweis auf die Möglichkeit, die Adresse zu verwenden. |
| [!UICONTROL Statusgrund] | `statusReason` | Zeichenfolge | Eine Beschreibung des aktuellen Status. |
| [!UICONTROL Letztes überprüftes Datum] | `lastVerifiedDate` | Zeichenfolge | Das Datum, an dem die Adresse zuletzt als noch mit der Person verbunden bestätigt wurde. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im [vollständigen Schema](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json) im öffentlichen XDM-Repository:
