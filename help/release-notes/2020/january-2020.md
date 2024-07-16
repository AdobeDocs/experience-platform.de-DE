---
title: Adobe Experience Platform – Versionshinweise Januar 2020
description: Versionshinweise Januar 2020 für Adobe Experience Platform.
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 41%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: Donnerstag, 15. Januar 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] (XDM)-System {#xdm}

Standardisierung und Interoperabilität sind Schlüsselkonzepte von [!DNL Experience Platform]. Das von Adobe unterstützte [!DNL Experience Data Model] (XDM)-System ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemata für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Feldtypbeschränkungen für Felder gleicher Hierarchie | Nachdem ein XDM-Feld als ein bestimmter Typ definiert wurde, müssen alle anderen Felder mit demselben Namen und derselben Hierarchie denselben Feldtyp verwenden, unabhängig von den Klassen oder Schemafeldgruppen, in denen sie verwendet werden. Wenn beispielsweise eine Feldergruppe für die XDM [!DNL Profile]-Klasse ein `profile.age` -Feld vom Typ &quot;integer&quot;enthält, kann eine ähnliche Feldergruppe für XDM [!DNL ExperienceEvent] kein `profile.age` -Feld vom Typ &quot;string&quot;haben. Um einen anderen Feldtyp zu verwenden, muss das Feld eine andere Hierarchie aufweisen als das zuvor definierte Feld (z. B. `profile.person.age`). Diese Funktion soll Konflikte verhindern, wenn Schemas in einer Vereinigung zusammengeführt werden. Die Beschränkung wirkt sich zwar nicht rückwirkend auf vorhandene Schemas aus, es wird jedoch dringend empfohlen, Ihre Schemas auf Konflikte mit Feldtypen zu überprüfen und sie nach Bedarf zu bearbeiten. |
| Feldvalidierung unter Berücksichtigung der Groß-/Kleinschreibung | Benutzerdefinierte Felder auf derselben Ebene müssen unabhängig von der Groß-/Kleinschreibung unterschiedliche Namen haben. Wenn Sie beispielsweise ein benutzerdefiniertes Feld namens &quot;E-Mail&quot;hinzufügen, können Sie kein weiteres benutzerdefiniertes Feld auf derselben Ebene namens &quot;E-Mail&quot;hinzufügen. |

**Bekannte Probleme**

* Keine

Weitere Informationen zum Arbeiten mit XDM unter Verwendung der [!DNL Schema Registry]-API und der [!DNL Schema Editor]-Benutzeroberfläche finden Sie in der [XDM-Systemdokumentation](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

Neue gesetzliche und organisatorische Vorschriften geben Benutzern das Recht, auf Anfrage auf ihre personenbezogenen Daten zuzugreifen bzw. diese Daten aus Ihren Datenspeichern löschen zu lassen. Adobe Experience Platform [!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, mit der Sie diese Datenanforderungen Ihrer Kunden verwalten können. Mit [!DNL Privacy Service] können Sie Anfragen zum Zugriff auf und zum Löschen von personenbezogenen oder privaten Kundendaten aus Adobe Experience Cloud-Anwendungen stellen, was die automatische Einhaltung gesetzlicher und organisatorischer Datenschutzbestimmungen erleichtert.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| [!DNL Privacy Service]-Rebranding | Der früher als „GDPR Service“ bezeichnete Service wurde in [!DNL Privacy Service] umbenannt, da der Service erweitert wurde, um neben der DSGVO auch andere Vorschriften zu unterstützen. |
| Neue API-Endpunkte | Der Basispfad für die [!DNL Privacy Service] -API wurde von `/data/privacy/gdpr` auf `/data/core/privacy/jobs` aktualisiert. |
| Neue erforderliche `regulation`-Eigenschaft | Bei der Erstellung neuer Aufträge in der [!DNL Privacy Service]-API muss eine `regulation`-Eigenschaft in der Anfrage-Payload angegeben werden, die angibt, nach welcher Vorschrift der Auftrag verfolgt werden soll. Zulässige Werte sind `gdpr` und `ccpa`. |
| Unterstützung für [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] akzeptiert jetzt Zugriffs-/Löschanfragen von Adobe [!DNL Primetime Authentication], wobei `primetimeAuthentication` als Produktwert verwendet wird. |
| Verbesserungen der Privacy Service-Benutzeroberfläche | Separate Auftragsverfolgungsseiten für DSGVO- und CCPA-Vorschriften. Neue Dropdown-Liste **Regelungstyp **Dropdown, um zwischen Tracking-Daten für DSGVO und CCPA zu wechseln. |

**Bekannte Probleme**

* Keine

Weitere Informationen zu [!DNL Privacy Service] erhalten Sie in der [Privacy Service-Übersicht](../../privacy-service/home.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen und gleichzeitig diese Daten mithilfe von [!DNL Platform] -Diensten strukturieren, beschriften und erweitern. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie auf einfache Weise Quellverbindungen für verschiedene Datenanbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Unterstützung für Kundenattributdaten | Benutzeroberflächen- und API-Unterstützung für die Erstellung von Streaming-Connectoren zur Erfassung von Kundenattributdaten. |
| Zusätzliche Dateiformatunterstützung für Cloud-Speicher | Die Dateiaufnahme aus Cloud-Speichern unterstützt jetzt XDM-konforme Parquet- und JSON-Dateiformate. |
| Unterstützung für Zugriffssteuerungsberechtigungen | Das Framework für die Zugriffskontrolle in Adobe Experience Platform bietet die Berechtigungen, die erforderlich sind, um bei der Datenerfassung Zugriff auf Quellen zu gewähren. Je nach Berechtigungsstufe kann ein Benutzer Quellen anzeigen, Quellen verwalten oder den Zugriff ganz verweigern. |

**Zugriffssteuerungsberechtigungen**

| Kategorie | Berechtigung | Beschreibung |
|--- | --- | ---|
| Datenerfassung | Verwalten von Quellen | Zugriff zum Lesen, Erstellen, Bearbeiten und Deaktivieren von Quellen. |
| Datenerfassung | Anzeigen von Quellen | Schreibgeschützter Zugriff auf verfügbare Quellen auf der Registerkarte **[!UICONTROL Katalog]** und authentifizierte Quellen auf der Registerkarte **[!UICONTROL Durchsuchen]**. |

**Bekannte Probleme**

* Keine

Weitere Informationen zu Quellen finden Sie unter [Quellen - Übersicht](../../sources/home.md)

## Ziele {#destinations}

In [Real-Time CDP](../../rtcdp/overview.md) sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten für diese Partner nahtlos aktivieren.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Unterstützung für Zugriffssteuerungsberechtigungen | Die Funktion Ziele in Real-Time CDP funktioniert mit Zugriffssteuerungsberechtigungen von Adobe Experience Platform. Je nach Berechtigungsstufe Ihres Benutzers können Sie Ziele anzeigen, verwalten und aktivieren. |

**Zugriffssteuerungsberechtigungen**

| Kategorie | Berechtigung | Beschreibung |
|--- | --- | ---|
| Ziele | Verwalten von Zielen | Zugriff auf das Lesen, Erstellen, Bearbeiten und Deaktivieren von Zielen. |
| Ziele | Anzeigen von Zielen | Schreibgeschützter Zugriff auf verfügbare Ziele auf der Registerkarte **[!UICONTROL Katalog]** und authentifizierte Ziele auf der Registerkarte **Durchsuchen**. |
| Ziele | Aktivieren von Zielen | Möglichkeit, Daten für Ziele zu aktivieren. Für diese Berechtigung muss entweder &quot;Ziele verwalten&quot;oder &quot;Ziele anzeigen&quot;zum Produktprofil hinzugefügt werden. |

**Bekannte Probleme**

* Keine

Weiterführende Informationen dazu finden Sie unter [Ziele – Übersicht](../../destinations/home.md).
