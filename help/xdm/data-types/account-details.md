---
title: Datentyp "Kontodetails"
description: Erfahren Sie mehr über den XDM-Datentyp (Account Details Experience Data Model).
exl-id: 17254393-263e-4000-9bd2-815a9e842533
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 22%

---

# Datentyp [!UICONTROL Kontodetails]

[!UICONTROL Kontodetails] ist ein standardmäßiger XDM-Datentyp (Experience-Datenmodell), der Details zu einem Unternehmen beschreibt.

![Datentypstruktur](../images/data-types/account-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL Währung]](./currency.md) | Der geschätzte Betrag der jährlichen Einnahmen der Organisation. |
| `DUNSNumber` | Zeichenfolge | Die Dun &amp; Bradstreet D-U-N-S Nummer der Organisation. Dies ist eine nicht indikative, neunstellige Zahl, die jedem Geschäftsstandort in der Dun &amp; Bradstreet-Datenbank zugewiesen wird und einen eindeutigen, separaten und eindeutigen Betrieb aufweist und ausschließlich von Dun &amp; Bradstreet verwaltet wird. |
| `NAICSCode` | Zeichenfolge | Die Klassifizierung der Organisation innerhalb des nordamerikanischen Klassifizierungssystems für die Industrie. |
| `NAICSDescription` | Zeichenfolge | Eine kurze Beschreibung des Geschäftsbereichs einer Organisation, basierend auf ihrem NAICS-Code. |
| `SICCode` | Zeichenfolge | Der SIC-Code (Standard Industrial Classification) der Organisation. Dies ist ein vierstelliger Code, der die Branche kategorisiert, zu der Unternehmen gehören, basierend auf ihrer Geschäftstätigkeit. |
| `SICDescription` | Zeichenfolge | Eine kurze Beschreibung des Geschäftsbereichs einer Organisation, basierend auf ihrem SIC-Code. |
| `companyProductAndServices` | Zeichenfolge | Die Produkte und Dienstleistungen, mit denen die Organisation handelt oder in denen sie Geschäfte tätigt. |
| `facebookPageUrl` | Zeichenfolge | Ein Website-Link zum Facebook-Konto der Organisation. |
| `industry` | Zeichenfolge | Die Branche, zu der diese Organisation gehört. Dies ist ein Freiformfeld. Es empfiehlt sich, einen strukturierten Wert für Abfragen oder die `xdm:classifier`-Eigenschaft zu verwenden. |
| `jigsaw` | Zeichenfolge | Der Data.com -Schlüssel für die Organisation. |
| `linkedinPageUrl` | Zeichenfolge | Ein Website-Link zum LinkedIn-Konto der Organisation. |
| `logoUrl` | Zeichenfolge | Ein Pfad, der mit der URL einer Salesforce-Instanz kombiniert werden kann (z. B. `https://yourInstance.salesforce.com/`), um eine URL zu generieren, mit der das Profilbild des sozialen Netzwerks abgerufen werden kann, das mit der Organisation verknüpft ist. Die generierte URL gibt eine HTTP-Umleitung (Code 302) zum Profilbild des sozialen Netzwerks für das Unternehmen zurück. |
| `marketSegment` | Zeichenfolge | Die benannte Marktzielgruppe, an der das Unternehmen teilnimmt. Dies ist ein Freiformfeld. Es empfiehlt sich, einen strukturierten Wert für Abfragen oder die `xdm:identifier`-Eigenschaft zu verwenden. |
| `numberOfEmployees` | Ganzzahl | Die Anzahl der Mitarbeiter in der Organisation. |
| `organizationType` | Zeichenfolge | Eine Bezeichnung, die den Organisationstyp beschreibt. |
| `primaryEmailDomain` | Zeichenfolge | Die primäre E-Mail-Domäne, die das Unternehmen für sein Personal verwendet. |
| `rating` | Double | Die berechnete Bewertung oder die Sternbewertung für diese Organisation. `1` gibt die maximale Bewertung an, und `0` ist die minimale mögliche Bewertung. |
| `tickerSymbol` | Zeichenfolge | Das Börsensymbol für dieses Konto. Maximal 20 Zeichen. |
| `twitterHandleUrl` | Zeichenfolge | Ein Website-Link zum twitter-Handle des Unternehmens. |
| `website` | Zeichenfolge | Die URL der Website der Organisation. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
