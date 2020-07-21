---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise zur Experience Platform vom 15. Januar 2020
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: f881c1365684b1ca9e6bf9a8ce866d234dc54128
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 43%

---


# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 15. Januar 2020**

Aktualisierungen vorhandener Funktionen in der Adobe Experience Platform:

* [!DNL Experience Data Model (XDM) System](#xdm)
* [!DNL Privacy Service](#privacy)
* [!DNL Sources](#sources)
* [!DNL Destinations](#destinations)

## [!DNL Experience Data Model] (XDM) System {#xdm}

Standardization and interoperability are key concepts behind [!DNL Experience Platform]. [!DNL Experience Data Model]Das von Adobe unterstützte  (XDM) ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Feldtypeinschränkungen für Felder gleicher Hierarchie | Nachdem ein XDM-Feld als ein bestimmter Typ definiert wurde, müssen alle anderen Felder mit demselben Namen und derselben Hierarchie unabhängig von den Klassen oder Mixins, in denen sie verwendet werden, denselben Feldtyp verwenden. Wenn beispielsweise ein Mixin für die XDM- [!DNL Profile] Klasse ein Feld vom Typ &quot;integer&quot;enthält, `profile.age` kann ein ähnliches Mixin für XDM kein [!DNL ExperienceEvent] `profile.age` Feld vom Typ &quot;string&quot;haben. Um einen anderen Feldtyp zu verwenden, muss das Feld eine andere Hierarchie aufweisen als das zuvor definierte Feld (z. B. `profile.person.age`). Diese Funktion soll Konflikte verhindern, wenn Schema in einer Vereinigung zusammengeführt werden. Die Beschränkung wirkt sich nicht rückwirkend auf vorhandene Schema aus. Es wird jedoch dringend empfohlen, Ihre Schema auf Feldkonflikte zu überprüfen und sie nach Bedarf zu bearbeiten. |
| Groß-/Kleinschreibung bei der Feldüberprüfung | Benutzerdefinierte Felder auf derselben Ebene müssen unabhängig von der Groß-/Kleinschreibung unterschiedliche Namen haben. Wenn Sie beispielsweise ein benutzerdefiniertes Feld mit dem Namen &quot;E-Mail&quot;hinzufügen, können Sie kein weiteres benutzerdefiniertes Feld mit dem Namen &quot;E-Mail&quot;hinzufügen. |

**Bekannte Probleme**

* Keine

To learn more about working with XDM using the [!DNL Schema Registry] API and [!DNL Schema Editor] user interface, please read the [XDM System documentation](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

Neue gesetzliche und organisatorische Vorschriften geben Benutzern das Recht, auf Anfrage auf ihre personenbezogenen Daten zuzugreifen bzw. diese Daten aus Ihren Datenspeichern löschen zu lassen. Adobe Experience Platform [!DNL Privacy Service] provides a RESTful API and user interface to help you manage these data requests from your customers. With [!DNL Privacy Service], you can submit requests to access and delete private or personal customer data from Adobe Experience Cloud applications, facilitating automated compliance with legal and organizational privacy regulations.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| [!DNL Privacy Service] umgestalten | The formerly named &quot;GDPR Service&quot; has been rebranded to [!DNL Privacy Service] as the service has grown to support other regulations in addition to GDPR. |
| Neue API-Endpunkte | Base path for the [!DNL Privacy Service] API has been updated from `/data/privacy/gdpr` to `/data/core/privacy/jobs`. |
| Neue erforderliche `regulation`-Eigenschaft | When creating new jobs in the [!DNL Privacy Service] API, a `regulation` property must be supplied in the request payload to indicate which regulation to track the job under. Die zulässigen Werte sind `gdpr` und `ccpa`. |
| Unterstützung für [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] akzeptiert jetzt Zugriff-/Löschanforderungen von Adobe [!DNL Primetime Authentication], wobei `primetimeAuthentication` als Produktwert verwendet wird. |
| Verbesserungen der Benutzeroberfläche von Privacy Service | Separate Auftragsverfolgungsseiten für DSGVO- und CCPA-Vorschriften. Neue Dropdown-Liste _Vorschriftentyp_, um zwischen den Verfolgungsdaten für DSGVO und CCPA zu wechseln. |

**Bekannte Probleme**

* Keine

For more information about [!DNL Privacy Service], please start by reading the [Privacy Service overview](../../privacy-service/home.md).

## Quellen {#sources}

Adobe Experience Platform can ingest data from external sources while allowing you to structure, label, and enhance that data using [!DNL Platform] services. Daten lassen sich aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, damit Sie für verschiedene Datenanbieter bequem Quellverbindungen einrichten können. Diese Quellverbindungen ermöglichen Ihnen das Authentifizieren und Verbinden mit externen Speichersystemen und CRM-Diensten, das Festlegen von Zeiten für Erfassungsläufe und das Verwalten des Datendurchsatzes bei der Erfassung.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Unterstützung für Kundenattributdaten | UI- und API-Unterstützung zum Erstellen von Streaming-Connectors zum Erfassen von Kundenattributdaten. |
| Zusätzliche Dateiformatunterstützung für Cloud-Datenspeicherung | Die Dateierfassung aus Cloud-Datenspeicherung unterstützt jetzt XDM-konforme Dateiformate wie Parquet und JSON. |
| Unterstützung für Zugriffskontrollen | Das Zugriffskontrolle-Framework in Adobe Experience Platform bietet die erforderlichen Berechtigungen, um den Zugriff auf Quellen bei der Datenerfassung zu gewähren. Je nach Berechtigungsstufe kann ein Benutzer Ansichten- und Quelldateien ausführen, Quellen verwalten oder den Zugriff ganz verweigern. |

**Berechtigungen für Zugriffskontrollen**

| Kategorie | Berechtigung | Beschreibung |
|--- | --- | ---|
| Datenaufnahme | Verwalten von Quellen | Zugriff zum Lesen, Erstellen, Bearbeiten und Deaktivieren von Quellen. |
| Datenaufnahme | Anzeigen von Quellen | Schreibgeschützter Zugriff auf verfügbare Quellen auf der Registerkarte *[!UICONTROL Katalog]* und authentifizierte Quellen auf der Registerkarte *[!UICONTROL Durchsuchen]*. |

**Bekannte Probleme**

* Keine

Weiterführende Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md)

## Ziele {#destinations}

In [Adobe Real-time CDP](../../rtcdp/overview.md), destinations are pre-built integrations with destination platforms that activate data to those partners in a seamless way.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Unterstützung für Zugriffskontrollen | Die Funktion Ziele in der Echtzeit-Kundendatenplattform funktioniert mit Zugangssteuerungsberechtigungen von Adobe Experience Platform. Je nach Berechtigungsstufe Ihres Anwenders können Sie Ziele anzeigen, verwalten und aktivieren. |

**Berechtigungen für Zugriffskontrollen**

| Kategorie | Berechtigung | Beschreibung |
|--- | --- | ---|
| Ziele | Verwalten von Zielen | Zugriff auf das Lesen, Erstellen, Bearbeiten und Deaktivieren von Zielen. |
| Ziele | Anzeigen von Zielen | Schreibgeschützter Zugriff auf verfügbare Ziele auf der Registerkarte [!UICONTROL _Katalog _]und authentifizierte Ziele auf der Registerkarte_ Durchsuchen._ |
| Ziele | Aktivieren von Zielen | Möglichkeit, Daten an Ziele zu aktivieren. Für diese Berechtigung muss dem Profil &quot;Ansicht&quot;entweder &quot;Ziele verwalten&quot;oder &quot;Zielorte verwalten&quot;hinzugefügt werden. |

**Bekannte Probleme**

* Keine

Weiterführende Informationen dazu finden Sie unter [Ziele – Übersicht](../../rtcdp/destinations/destinations-overview.md).