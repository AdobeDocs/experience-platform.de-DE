---
title: Datentyp der Kontodetails
description: Erfahren Sie mehr über den Datentyp Kontodetails, Experience-Datenmodell (XDM) .
exl-id: 17254393-263e-4000-9bd2-815a9e842533
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 22%

---

# [!UICONTROL Kontodetails] Datentyp

[!UICONTROL Kontodetails] ist ein standardmäßiger Experience-Datenmodell (XDM)-Datentyp, der Details zu einer Geschäftsorganisation beschreibt.

![Datentypstruktur](../images/data-types/account-details.png)

| Eigenschaft | Datentyp | Beschreibung |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL Währung]](./currency.md) | Die geschätzte Höhe des Jahresumsatzes der Organisation. |
| `DUNSNumber` | String | Die Dun &amp; Bradstreet D-U-N-S-Nummer der Organisation. Dies ist eine nicht-indikative, neunstellige Nummer, die jedem Geschäftsstandort in der Dun &amp; Bradstreet-Datenbank zugewiesen wird, der einen einzigartigen, separaten und unterschiedlichen Betrieb hat, und die ausschließlich von Dun &amp; Bradstreet gepflegt wird. |
| `NAICSCode` | String | Die Klassifizierung der Organisation innerhalb des North American Industry Classification System. |
| `NAICSDescription` | String | Eine kurze Beschreibung des Geschäftszweigs einer Organisation, basierend auf ihrem NAICS-Code. |
| `SICCode` | String | Der Standard Industrial Classification (SIC)-Code der Organisation. Dies ist ein vierstelliger Code, der die Branche, zu der Unternehmen gehören, basierend auf ihren Geschäftsaktivitäten kategorisiert. |
| `SICDescription` | String | Eine kurze Beschreibung des Geschäftszweigs einer Organisation, basierend auf ihrem SIC-Code. |
| `companyProductAndServices` | String | Die Produkte und Services, mit denen das Unternehmen handelt oder Geschäfte macht. |
| `facebookPageUrl` | String | Ein Website-Link zum Facebook-Konto des Unternehmens. |
| `industry` | String | Die Branche, zu der diese Organisation gehört. Dies ist ein Freiformfeld. Es empfiehlt sich, einen strukturierten Wert für Abfragen oder die `xdm:classifier`-Eigenschaft zu verwenden. |
| `jigsaw` | String | Der Schlüssel Data.com für die Organisation. |
| `linkedinPageUrl` | String | Ein Website-Link zum LinkedIn-Konto des Unternehmens. |
| `logoUrl` | String | Ein Pfad, der mit der URL einer Salesforce-Instanz (z. B. `https://yourInstance.salesforce.com/`) kombiniert werden soll, um eine URL zu generieren, mit der das mit dem Unternehmen verknüpfte Profilbild der Social Media angefordert werden kann. Die generierte URL gibt eine HTTP-Umleitung (Code 302) zum Profilbild der Social Media für das Unternehmen zurück. |
| `marketSegment` | String | Die benannte MarkZielgruppe, an der die Organisation teilnimmt. Dies ist ein Freiformfeld. Es empfiehlt sich, einen strukturierten Wert für Abfragen oder die `xdm:identifier`-Eigenschaft zu verwenden. |
| `numberOfEmployees` | Ganzzahl | Die Anzahl der Mitarbeiter in der Organisation. |
| `organizationType` | String | Ein Titel, der den Typ der Organisation beschreibt. |
| `primaryEmailDomain` | String | Die primäre E-Mail-Domain, die das Unternehmen für seine Mitarbeiter verwendet. |
| `rating` | Double | Die berechnete Bewertung oder Sternebewertung für diese Organisation. `1` gibt die maximal mögliche Bewertung an, und `0` ist die minimal mögliche Bewertung. |
| `tickerSymbol` | String | Das Börsensymbol für dieses Konto. Maximal 20 Zeichen. |
| `twitterHandleUrl` | String | Ein Website-Link zum twitter-Handle des Unternehmens. |
| `website` | String | Die URL der Website der Organisation. |

{style="table-layout:auto"}

Weitere Informationen zum Datentyp finden Sie im öffentlichen XDM-Repository:

* [Ausgefülltes Beispiel](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [Vollständiges Schema](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
