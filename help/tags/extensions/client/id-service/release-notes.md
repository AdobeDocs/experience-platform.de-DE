---
title: Versionshinweise zur Adobe Experience Cloud Identity Service-Erweiterung
description: Aktuelle Versionshinweise für die Tag-Erweiterung „Adobe Experience Cloud Identity Service“ in Adobe Experience Platform.
exl-id: f9bfbed7-1eec-4916-9235-a75b5e2efcf8
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '643'
ht-degree: 76%

---

# Adobe Experience Cloud Identity Service-Erweiterung – Versionshinweise

In diesem Dokument werden die Versionshinweise für die Tag-Erweiterung &quot;Adobe Experience Cloud Identity Service“ behandelt. Versionshinweise zu Experience Cloud Identity Service selbst finden Sie in der [Identity Service-Dokumentation](https://experienceleague.adobe.com/docs/id-service/using/release-notes/release-notes.html?lang=de).

## &#x200B;17. Oktober 2022

### Experience Cloud ID-Erweiterung 5.5.0

* Die Erweiterung unterstützt jetzt Version 5.5.0 des [Visitor JS Client](https://github.com/Adobe-Marketing-Cloud/id-service). Spezifische Aktualisierungen finden Sie [ den ](https://github.com/Adobe-Marketing-Cloud/id-service/releases/tag/5.5.0)Besucherhinweisen“.

## &#x200B;9. März 2022

### Experience Cloud ID-Erweiterung 5.4.0

* Diese Version enthält die neueste Version Visitor 5.4.0 mit den folgenden Aktualisierungen:

   * Möglichkeit, die Lebensdauer des `s_ecid` Cookies mithilfe der cookieLifetime-Konfiguration zu konfigurieren
   * Aktualisierung für ein Problem mit dem Firefox-Browser, das auftritt, wenn eine Seite in einen untergeordneten iFrame geladen wird

## &#x200B;10. Oktober 2021

### Experience Cloud ID-Erweiterung 5.3.1

* Diese Version enthält die neueste Version Visitor 5.3.0 mit den folgenden neuen Aktualisierungen:

   * Algorithmus zum Generieren einer lokalen ECID aktualisiert
   * Neuestes Opt-in mit `Secure`- und `SameSite` für das Datenschutz-Cookie
   * Behebung eines Firefox-Browser-Problems, wenn eine Seite in einen untergeordneten iFrame geladen wird

## 12. Januar 2021

### Experience Cloud ID-Erweiterung 5.2.0

* Das Aktualisieren auf den Patch „VisitorJS 5.2.0“ mit einer Fehlerbehebung für „ECID DataElement“ konnte bei Eingang der Zustimmung nicht aktualisiert werden.

## 3. November 2020

### Experience Cloud ID-Erweiterung 5.2.1

* Dieser Patch enthält eine Fehlerbehebung für das Schreiben von Cookies aus einem iFrame mit dem Attribut `SameSite=None` im Google Chrome-Browser.

## 27. Oktober 2020

### Experience Cloud ID-Erweiterung 5.1.0

* Hinzufügen der Konfiguration `sameSiteCookie`, um das `SameSite`-Attribut des `AMCV`-Cookies zu spezifizieren.
Diese Konfiguration unterstützt die folgenden Werte für das `SameSite`-Attribut:

   * `Strict`
   * `Lax`
   * `None`

Details zu diesen Attributwerten finden Sie unter [web.dev](https://web.dev/samesite-cookies-explained/) und [chromium](https://www.chromium.org/updates/same-site)


## &#x200B;13. August 2020

### Experience Cloud ID-Erweiterung 5.0.1

* Aktualisierung auf den Patch VisitorJS 5.0.1 mit einer Fehlerbehebung zum Hinzufügen des Flag d_cf, wenn die IAB-Zustimmungszeichenfolge geändert wurde.

## 15. Juni 2020

### Experience Cloud ID-Erweiterung 5.0.0

* Unterstützung für as `IAB TCF` – Transparency &amp; Consent Framework – `Version 2.0` wurde hinzugefügt.

## 13. April 2020

### Experience Cloud ID-Erweiterung 4.6.0

* Markierung `loadSSL` standardmäßig aktiviert. Alle Aufrufe von Identity Service sind standardmäßig auf `https` gesetzt. Kunden können den Wert auf „false“ setzen, wenn sie Identity Services auf HTTP von ihren Nicht-SSL-Seiten aufrufen möchten.
* Die Funktion zur Erkennung der Internet Explorer-Version (IE) wurde aktualisiert, um ein von ESLint gemeldetes Problem zu beheben.
* Fehlerbehebung für ein Performance-Problem in Internet Explorer (IE) 11, wenn die ECID mit der OptIn-Vorabgenehmigung versehen und später aktualisiert wird.

## 22. Januar 2020

### Experience Cloud ID-Erweiterung 4.5.2

* „visitor.js“ in 4.5.2 aktualisiert
* Visitor 4.5.1 enthält eine Fehlerbehebung für das IAB-Plugin für Optin
* Die `setCustomerIDs`-Methode zur Ablehnung von gesendeten leeren IDs wurde aktualisiert.

## 7. Januar 2020

### Experience Cloud ID-Erweiterung 4.4.2

* „visitor.js“ in 4.4.2 aktualisiert
* Verbesserungen bei der `getVisitorValues`-Methode zum schnelleren Abrufen von Werten.


## 19. September 2019

### Experience Cloud ID-Erweiterung 4.4.1

* „visitor.js“ in 4.4.1 aktualisiert
* Ein Fehler für Eingabe von „get Opt-In preApprovals“ wurde behoben
* VIDEO_ANALYTICS in MEDIA_ANALYTICS in preOptInApprovals umbenannt

  ![](../../../images/ecid-media-analytics.png)

## 17. Juli 2019

### Experience Cloud ID-Erweiterung 4.4.0

* „visitor.js“ in 4.4.0 aktualisiert
* SHA256-Hashing-Unterstützung für setCustomerIDs hinzugefügt

  ![](../../../images/ecid-setCustomerIDs-hash.png)

## &#x200B;13. Mai 2019

### Experience Cloud ID-Erweiterung 4.3.1

* „visitor.js“ in 4.3 aktualisiert
* Datenelementtyp für ECID als Teil der Tag-Erweiterung hinzugefügt

  ![](../../../images/ecid-data-element.png)

## &#x200B;9. April 2019

### Experience Cloud ID-Erweiterung 4.2.0

* Aktualisierung von visitor.js auf Version 4.2 mit Unterstützung für das IAB TCF-Plug-in für Audience Manager.

## 25. Februar 2019

### Experience Cloud ID-Erweiterung 4.1.0

* Die Datei visitor.js wurde auf Version 4.1 aktualisiert, mit der die Datei „publishDestinations“ entsprechend der neuen API-Änderung aktualisiert wurde. Mit dieser Aktualisierung können die Referrer-Informationen der Seite während der ID-Synchronisierung offengelegt werden, wenn gewünscht.

## &#x200B;15. Februar 2019

### Experience Cloud ID-Erweiterung 4.0.0

* „visitor.js“ in 4.0 aktualisiert
* Hinzufügung von Konfigurationsoptionen für das neue integrierte Opt-in-Objekt. Opt-in-Einstellungen können verwendet werden, um Cookie- und Signalaufrufe von Adobe Solutions zu unterdrücken und so bessere Supportregeln wie DSGVO zu erhalten.

  ![](../../../images/ext-mcid-opt-in.png)

## &#x200B;20. März 2018

### Experience Cloud ID-Erweiterung 3.1.0

* „visitor.js“ in 3.1 aktualisiert
* Fügt zwei Konfigurationseigenschaften hinzu: `resetBeforeVersion` und `serverState`.
