---
title: Datentyp der Postanschrift
description: Erfahren Sie mehr über den Datentyp "Postal Address Experience Data Model (XDM)".
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '226'
ht-degree: 36%

---

# [!UICONTROL Postanschrift] Datentyp

[!UICONTROL Postanschrift] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Adressdetails bereitstellt.

![Ein Diagramm des [!UICONTROL Postanschrift] Datentyp.](../images/data-types/postal-address.png)

| Anzeigename | Eigenschaft | Datentyp | Beschreibung |
|------------------------------------|------------------|-----------|-----------------------------------------------------------------------------------------------|
| [!UICONTROL Primäre Instanz] | `primary` | boolean | Primärer Adressindikator. Ein Profil kann nur eine `primary` Adresse zu einem bestimmten Zeitpunkt. |
| [!UICONTROL Titel] | `label` | Zeichenfolge | Der Name der Adresse ist kostenlos. |
| [!UICONTROL Straße 1] | `street1` | Zeichenfolge | Primäre Straßeninformationen, Wohnungsnummer, Straßennummer und Straßenname. |
| [!UICONTROL Straße 2] | `street2` | Zeichenfolge | Optionale Straßeninformationen, zweite Zeile. |
| [!UICONTROL Straße 3] | `street3` | Zeichenfolge | Optionale Straßeninformationen, dritte Zeile. |
| [!UICONTROL Straße 4] | `street4` | Zeichenfolge | Optionale Straßeninformationen, vierte Zeile. |
| [!UICONTROL Region] | `region` | Zeichenfolge | Die Region, der Kreis oder der Bezirk der Adresse. |
| [!UICONTROL Postfach] | `postOfficeBox` | Zeichenfolge | Postfach der Adresse. |
| [!UICONTROL Land] | `country` | Zeichenfolge | Der Name des von der Regierung verwalteten Gebiets. Mit Ausnahme von ``countryCode`` ist dies ein Freiformfeld, das den Ländernamen in jeder Sprache enthalten kann. |
| [!UICONTROL Bundesland] | `state` | Zeichenfolge | Der Name des Staates. Dies ist ein Freiformfeld. |
| [!UICONTROL Status] | `status` | Zeichenfolge | Ein Hinweis auf die Möglichkeit, die Adresse zu verwenden. |
| [!UICONTROL Statusgrund] | `statusReason` | Zeichenfolge | Eine Beschreibung des aktuellen Status. |
| [!UICONTROL Datum der letzten Überprüfung] | `lastVerifiedDate` | Zeichenfolge | Das Datum, an dem die Adresse zuletzt als noch mit der Person verbunden bestätigt wurde. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im Abschnitt [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/docs/reference/datatypes/address.schema.json) im öffentlichen XDM-Repository:
