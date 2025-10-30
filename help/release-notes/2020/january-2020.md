---
title: Adobe Experience Platform – Versionshinweise Januar 2020
description: Versionshinweise Januar 2020 für Adobe Experience Platform.
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 39%

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
| Feldtyp-Einschränkungen für Felder gleicher Hierarchie | Nachdem ein XDM-Feld als bestimmter Typ definiert wurde, müssen alle anderen Felder desselben Namens und derselben Hierarchie denselben Feldtyp verwenden, unabhängig von den Klassen oder Schemafeldgruppen, in denen sie verwendet werden. Wenn beispielsweise eine Feldergruppe für die XDM-[!DNL Profile] ein `profile.age` Feld vom Typ „integer“ enthält, kann eine ähnliche Feldergruppe für XDM-[!DNL ExperienceEvent] kein `profile.age` Feld vom Typ „string“ haben. Um einen anderen Feldtyp zu verwenden, muss das Feld eine andere Hierarchie als das zuvor definierte Feld aufweisen (z. B. `profile.person.age`). Diese Funktion soll Konflikte verhindern, wenn Schemas in einer Vereinigung zusammengeführt werden. Obwohl sich die Einschränkung nicht rückwirkend auf vorhandene Schemata auswirkt, wird dringend empfohlen, die Schemata auf Konflikte von Feldtypen zu überprüfen und nach Bedarf zu bearbeiten. |
| Validierung von Feldern mit Unterscheidung von Groß- und Kleinschreibung | Benutzerdefinierte Felder auf derselben Ebene müssen unabhängig von der Groß-/Kleinschreibung unterschiedliche Namen haben. Wenn Sie beispielsweise ein benutzerdefiniertes Feld mit dem Namen „E-Mail“ hinzufügen, können Sie auf derselben Ebene kein weiteres benutzerdefiniertes Feld mit dem Namen „E-Mail“ hinzufügen. |

**Bekannte Probleme**

* Keine

Weitere Informationen zum Arbeiten mit XDM mithilfe der [!DNL Schema Registry]-API und [!DNL Schema Editor] Benutzeroberfläche finden Sie in der [XDM-Systemdokumentation](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

Neue gesetzliche und organisatorische Vorschriften geben Benutzern das Recht, auf Anfrage auf ihre personenbezogenen Daten zuzugreifen bzw. diese Daten aus Ihren Datenspeichern löschen zu lassen. Adobe Experience Platform [!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, die Sie bei der Verwaltung dieser Datenanfragen Ihrer Kunden unterstützen. Mit [!DNL Privacy Service] können Sie Anfragen für den Zugriff auf und die Löschung von personenbezogenen oder privaten Kundendaten aus Adobe Experience Cloud-Programmen stellen, was die automatische Einhaltung gesetzlicher und unternehmensinterner Datenschutzbestimmungen erleichtert.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| [!DNL Privacy Service]-Rebranding | Der früher als „GDPR Service“ bezeichnete Service wurde in [!DNL Privacy Service] umbenannt, da der Service erweitert wurde, um neben der DSGVO auch andere Vorschriften zu unterstützen. |
| Neue API-Endpunkte | Der Basispfad für die [!DNL Privacy Service]-API wurde von `/data/privacy/gdpr` auf `/data/core/privacy/jobs` aktualisiert. |
| Neue erforderliche `regulation`-Eigenschaft | Bei der Erstellung neuer Aufträge in der [!DNL Privacy Service]-API muss eine `regulation`-Eigenschaft in der Anfrage-Payload angegeben werden, die angibt, nach welcher Vorschrift der Auftrag verfolgt werden soll. Akzeptierte Werte sind `gdpr` und `ccpa`. |
| Unterstützung für [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] akzeptiert jetzt Zugriffs-/Löschanfragen von Adobe [!DNL Primetime Authentication] und verwendet `primetimeAuthentication` als Produktwert. |
| Verbesserungen der Privacy Service-Benutzeroberfläche | Separate Auftrags-Tracking-Seiten für DSGVO- und CCPA-Vorschriften. Neue Dropdown-Liste **Vorschriftentyp**, um zwischen den Verfolgungsdaten für DSGVO und CCPA zu wechseln. |

**Bekannte Probleme**

* Keine

Für weitere Informationen zu [!DNL Privacy Service] lesen Sie zunächst die [Übersicht über Privacy Service](../../privacy-service/home.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen aufnehmen und ermöglicht es Ihnen gleichzeitig, diese Daten mithilfe von [!DNL Experience Platform]-Services zu strukturieren, zu kennzeichnen und anzureichern. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform] bietet eine RESTful-API und eine interaktive Benutzeroberfläche, mit der Sie auf einfache Weise Quellverbindungen für verschiedene Datenanbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Unterstützung für Kundenattributdaten | UI- und API-Unterstützung für die Erstellung von Streaming-Connectoren zur Aufnahme von Kundenattributdaten. |
| Zusätzliche Unterstützung von Dateiformaten für Cloud-Speicher | Die Dateiaufnahme aus Cloud-Speichern unterstützt jetzt XDM-konforme Parquet- und JSON-Dateiformate. |
| Unterstützung für Zugriffssteuerungsberechtigungen | Das Zugriffssteuerungs-Framework in Adobe Experience Platform bietet die Berechtigungen, die erforderlich sind, um Zugriff auf Quellen in der Datenaufnahme zu gewähren. Je nach Berechtigungsstufe kann ein Benutzer Quellen anzeigen, Quellen verwalten oder den Zugriff ganz verweigern. |

**Zugriffssteuerungsberechtigungen**

| Kategorie | Berechtigung | Beschreibung |
|--- | --- | ---|
| Datenerfassung | Verwalten von Quellen | Zugriff zum Lesen, Erstellen, Bearbeiten und Deaktivieren von Quellen. |
| Datenerfassung | Anzeigen von Quellen | Schreibgeschützter Zugriff auf verfügbare Quellen auf der Registerkarte **[!UICONTROL Catalog]** und authentifizierte Quellen auf der Registerkarte **[!UICONTROL Browse]** . |

**Bekannte Probleme**

* Keine

Weitere Informationen zu Quellen finden Sie unter [Quellen - Übersicht](../../sources/home.md)

## Ziele {#destinations}

In [Real-Time CDP](../../rtcdp/overview.md) sind Ziele vorgefertigte Integrationen mit Zielplattformen, die Daten nahtlos für diese Partner aktivieren.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Unterstützung für Zugriffssteuerungsberechtigungen | Die Funktion „Ziele“ in Real-Time CDP arbeitet mit Zugriffssteuerungsberechtigungen für Adobe Experience Platform. Abhängig von der Berechtigungsstufe Ihrer Benutzerin bzw. Ihres Benutzers können Sie Ziele anzeigen, verwalten und aktivieren. |

**Zugriffssteuerungsberechtigungen**

| Kategorie | Berechtigung | Beschreibung |
|--- | --- | ---|
| Ziele | Verwalten von Zielen | Zugriff auf das Lesen, Erstellen, Bearbeiten und Deaktivieren von Zielen. |
| Ziele | Anzeigen von Zielen | Schreibgeschützter Zugriff auf verfügbare Ziele auf der Registerkarte **[!UICONTROL Catalog]** und authentifizierte Ziele auf der Registerkarte **Durchsuchen**. |
| Ziele | Aktivieren von Zielen | Möglichkeit, Daten für Ziele zu aktivieren. Für diese Berechtigung ist es erforderlich, dass dem Produktprofil entweder „Ziele verwalten“ oder „Ziele anzeigen“ hinzugefügt wird. |

**Bekannte Probleme**

* Keine

Weiterführende Informationen dazu finden Sie unter [Ziele – Übersicht](../../destinations/home.md).
