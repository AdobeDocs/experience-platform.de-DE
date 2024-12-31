---
title: Schemafeldgruppe Advertising-Details
description: Erfahren Sie mehr über die Schemafeldgruppe "Advertising-Details“.
exl-id: 25de09bd-eedd-489c-9cd5-8acd0c52ddbe
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '992'
ht-degree: 29%

---

# [!UICONTROL Advertising-Details] Schemafeldgruppe

[!UICONTROL Advertising-]: ist eine Standardschemafeldgruppe für die [[!DNL XDM ExperienceEvent] class](../../classes/experienceevent.md). Die Feldergruppe stellt ein einzelnes `advertising` für ein Schema bereit, das Informationen zu Werbeimpressionen, Clickthroughs und Attribution erfasst.

![Feldergruppenstruktur](../../images/field-groups/advertising-details/structure.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `adAssetReference` | Objekt | Erfasst Asset-Informationen über die Anzeige. Weitere Informationen [ Struktur dieses Objekts ](#adAssetReference) Sie im Abschnitt „Unterabschnitt unten“. |
| `adAssetViewDetails` | Objekt | Erfasst Ansichtsdetails für die Anzeigenwiedergabe. Weitere Informationen [ Struktur dieses Objekts ](#adAssetViewDetails) Sie im Abschnitt „Unterabschnitt unten“. |
| `adViewability` | Objekt | Erfasst die Anzahl der Impressionen, die von Endbenutzenden angezeigt werden, z. B. Player-Lautstärke, Bibliotheksversion, Fensterstatus und Anzeigenansichtsfenster-Dimensionen. Weitere Informationen [ Struktur dieses Objekts ](#adViewability) Sie im Abschnitt „Unterabschnitt unten“. |
| `clicks` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Die Anzahl der Klickaktionen auf die Anzeige. |
| `completes` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Die Häufigkeit, mit der ein zeitgesteuertes Medien-Asset bis zum Ende angesehen wurde. Dies bedeutet nicht unbedingt, dass der Endbenutzer das gesamte Video angesehen hat, da er möglicherweise vorgesprungen ist. |
| `conversions` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Die Häufigkeit, mit der eine vordefinierte Aktion (oder Aktionen) ein Ereignis zur Leistungsbewertung ausgelöst hat. |
| `federated` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Zeigt an, ob ein Erlebnisereignis durch Datenverbund erstellt wurde, z. B. durch gemeinsame Nutzung von Daten durch Kunden. |
| `firstQuartiles` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Die Häufigkeit, mit der eine digitale Videoanzeige 25 % ihrer Dauer mit normaler Geschwindigkeit wiedergegeben hat. |
| `impressions` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Die Anzahl der an einen Endbenutzer gesendeten Anzeigen-Impressions mit dem Potenzial, angezeigt zu werden. |
| `midpoints` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Die Häufigkeit, mit der eine digitale Videoanzeige 50 % ihrer Dauer mit normaler Geschwindigkeit wiedergegeben hat. |
| `starts` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Die Häufigkeit, mit der die Wiedergabe einer digitalen Videoanzeige begonnen hat. |
| `thirdQuartiles` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Die Häufigkeit, mit der eine digitale Videoanzeige 75 % ihrer Dauer mit normaler Geschwindigkeit wiedergegeben hat. |
| `timePlayed` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Die Zeit, die ein Endbenutzer mit einem bestimmten zeitgesteuerten Medien-Asset verbracht hat. |
| `downloadedPlayback` | Boolesch | Wenn auf `true` gesetzt, bedeutet dies, dass der Treffer aufgrund der Wiedergabe einer heruntergeladenen Anzeigensitzung erzeugt wird. |

{style="table-layout:auto"}

## `adAssetReference` {#adAssetReference}

Das `adAssetReference` erfasst Asset-Informationen über die Anzeige.

![adAssetReference-Struktur](../../images/field-groups/advertising-details/adAssetReference.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `_dc.title` | Zeichenfolge | Der benutzerfreundliche und menschenlesbare Name des Anzeigen-Assets. |
| `_xmpDM.duration` | Ganzzahl | Die Dauer des Assets in Sekunden. |
| `_id` | String | Eine eindeutige Kennung des Anzeigen-Assets, die dem [Ad-ID-Standard) ](https://datatracker.ietf.org/doc/html/rfc8107). |
| `advertiser` | String | Die Firma oder Marke, deren Produkt in der Anzeige zu sehen ist. |
| `campaign` | String | Die ID der Anzeigenkampagne. |
| `creativeID` | String | Die ID des Kreativinhalts der Anzeige. |
| `creativeURL` | String | Die URL des Kreativinhalts der Anzeige. |
| `placementID` | String | Die Platzierungs-ID der Anzeige. |
| `siteID` | String | Die ID der Anzeigen-Site. |

{style="table-layout:auto"}

## `adAssetViewDetails` {#adAssetViewDetails}

Das `adAssetViewDetails`-Objekt erfasst Ansichtsdetails für die Anzeigenwiedergabe.

![adAssetViewDetails-Struktur](../../images/field-groups/advertising-details/adAssetViewDetails.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `adBreak` | [[!UICONTROL Werbeunterbrechung]](../../data-types/ad-break.md) | Beschreibt, wie eine zeitgesteuerte Anzeige in zeitgesteuerte Medien eingefügt wird. |
| `index` | Ganzzahl | Der Index der Anzeige innerhalb der übergeordneten Anzeigenunterbrechung. Beispielsweise verfügt die erste Anzeige über Index `0` und die zweite Anzeige über Index `1`. |
| `playerName` | String | Der Name des Players, der für das Rendering der Werbeanzeige verantwortlich ist. |

{style="table-layout:auto"}

## `adViewability` {#adViewability}

Das `adViewability`-Objekt erfasst die Anzahl der Impressionen, die von Endbenutzenden angezeigt werden, z. B. die Player-Lautstärke, die Bibliotheksversion, den Fensterstatus und die Abmessungen des Anzeigenansichtsfensters.

![adVieability-Struktur](../../images/field-groups/advertising-details/adViewability.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `implementationDetails` | [[!UICONTROL Implementierungsdetails]](../../data-types/implementation-details.md) | Name und Version der Bibliothek, die zur Messung der Sichtbarkeitsmetriken verwendet wird. |
| `measuredAdNotVisible` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Zeigt an, dass die Anzeige, gemessen anhand einer Sichtbarkeitsbibliothek zum Zeitpunkt der Impression, nicht sichtbar ist. |
| `measuredMuted` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Gibt an, dass die Anzeige stummgeschaltet ist, was anhand einer Sichtbarkeitsbibliothek zum Zeitpunkt der Impression gemessen wird. |
| `unmeasurableIframe` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Gibt an, dass die Anzeige in einem inaktiven Fenster angezeigt wird, gemessen anhand einer Sichtbarkeitsbibliothek zum Zeitpunkt der Impression. |
| `unmeasurableOther` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Zeigt an, dass die Sichtbarkeitsbibliothek aufgrund der Anzeige innerhalb eines iFrames nicht in der Lage ist, Messungen korrekt auszuführen. |
| `viewabilityEligibleImpressions` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Impression(en) einer Anzeige für einen Endbenutzer unter Verwendung einer Sichtbarkeitsbibliothek. |
| `viewabilityCompletes` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Beendigungen einer Werbeanzeige für einen Endbenutzer, die zum Zeitpunkt der Beendigung von einer Sichtbarkeitsbibliothek als sichtbar erachtet wird. |
| `viewableFirstQuartiles` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Erste(s) Quartil(e) einer Anzeige für einen Endbenutzer, die von einer Sichtbarkeitsbibliothek im ersten Quartil der Wiedergabe als sichtbar erachtet wird. |
| `viewableImpressions` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Impressionen einer Anzeige für einen Endbenutzer, die von einer Sichtbarkeitsbibliothek nach zwei Sekunden der Wiedergabe als sichtbar erachtet wird. |
| `viewableMidpoints` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Mittelpunkte einer Anzeige für einen Endbenutzer, die von einer Sichtbarkeitsbibliothek im Mittelpunkt der Wiedergabe als sichtbar erachtet wird. |
| `viewableThirdQuartiles` | [[!UICONTROL Maßnahme]](../../data-types/measure.md) | Dritte(s) Quartil(e) einer Anzeige für einen Endbenutzer, die von einer Sichtbarkeitsbibliothek im dritten Quartil der Wiedergabe als sichtbar erachtet wird. |
| `activeWindow` | Boolesch | Zeigt an, ob die Anzeige im aktiven Fenster des Geräts des Benutzers angezeigt wurde. |
| `adHeight` | Ganzzahl | Die Anzahl der zur Laufzeit gemessenen vertikalen Pixel des Players. Diese kann größer sein als die Größe der Anzeige, wenn der Player über zusätzliche Steuerelemente oder Miniaturansichten verfügt. |
| `adUnitDepth` | Ganzzahl | Publisher können Anzeigeneinheiten in Container (iFrames) einbetten, um den Zugriff der Anzeige ausschließlich auf den Code der Seite zu beschränken. Dieser Wert beschreibt, in wie vielen Containern die Werbeeinheit angezeigt wird. |
| `adWidth` | Ganzzahl | Die Anzahl der zur Laufzeit gemessenen horizontalen Pixel des Players. Diese kann größer sein als die Größe der Anzeige, wenn der Player über zusätzliche Steuerelemente oder Miniaturansichten verfügt. |
| `measurementEligible` | Boolesch | Ob die Sichtbarkeitsmessungen für die Anzeige zulässig sind. Eine Anzeige ist zulässig, wenn das Gerät über ein unterstütztes kreatives Format und einen unterstützten Tag-Typ verfügt. |
| `percentViewable` | Ganzzahl | Der Prozentsatz der Pixel in der Anzeige, die zum Zeitpunkt der Messung als sichtbar erachtet werden. |
| `playerVolume` | Ganzzahl | Der Prozentsatz der Player-Lautstärke, gemessen zur Laufzeit, wobei `0` stummgeschaltet und `100` die maximale Lautstärke ist. |
| `viewable` | Boolesch | Gibt an, ob die Anzeige zur Laufzeit sichtbar war. Display-Anzeigen gelten als sichtbar, wenn mindestens 50 % der Anzeige mindestens eine Sekunde lang sichtbar sind. Videoanzeigen werden als sichtbar betrachtet, wenn mindestens 50 % der Anzeige sichtbar sind, während das Video mindestens zwei aufeinander folgende Sekunden lang wiedergegeben wird. |
| `viewportHeight` | Ganzzahl | Die vertikale Größe (in Pixeln) des Fensters, in dem das Erlebnis angezeigt wurde, gemessen zur Laufzeit. Bei einem Web-Ansichtsereignis gibt dieser Wert die Höhe des Browser-Ansichtsfensters an. |
| `viewportWidth` | Ganzzahl | Die horizontale Größe (in Pixeln) des Fensters, in dem das Erlebnis angezeigt wurde, gemessen zur Laufzeit. Bei einem Web-Ansichtsereignis gibt dieser Wert die Breite des Browser-Ansichtsfensters an. |

{style="table-layout:auto"}

Weitere Informationen zur Feldergruppe finden Sie unter [öffentliches XDM-Repository](https://github.com/adobe/xdm/blob/master/components/fieldgroups/experience-event/experienceevent-advertising.schema.json).
