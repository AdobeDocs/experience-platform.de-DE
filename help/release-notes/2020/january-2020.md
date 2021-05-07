---
title: Versionshinweise zu Adobe Experience Platform
description: Versionshinweise zur Experience Platform vom 15. Januar 2020
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 40%

---

# Versionshinweise zu Adobe Experience Platform

**Releasedatum: 15. Januar 2020**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] (XDM) System  {#xdm}

Normung und Interoperabilität sind Schlüsselkonzepte hinter [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), angetrieben von der Adobe, ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schema für das Kundenerlebnis-Management zu definieren.

XDM ist eine öffentlich dokumentierte Spezifikation, die die Leistungsfähigkeit digitaler Erlebnisse verbessern soll. Es stellt allgemeine Strukturen und Definitionen für Anwendungen bereit, die mit Diensten in Adobe Experience Platform kommunizieren. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Feldtypeinschränkungen für Felder gleicher Hierarchie | Nachdem ein XDM-Feld als ein bestimmter Typ definiert wurde, müssen alle anderen Felder mit demselben Namen und derselben Hierarchie unabhängig von den Klassen oder Schema-Feldgruppen, in denen sie verwendet werden, denselben Feldtyp verwenden. Wenn beispielsweise eine Feldgruppe für die XDM [!DNL Profile]-Klasse ein `profile.age`-Feld des Typs &quot;integer&quot;enthält, kann eine ähnliche Feldgruppe für XDM [!DNL ExperienceEvent] kein `profile.age`-Feld des Typs &quot;string&quot;haben. Um einen anderen Feldtyp zu verwenden, muss das Feld eine andere Hierarchie aufweisen als das zuvor definierte Feld (z. B. `profile.person.age`). Diese Funktion soll Konflikte verhindern, wenn Schema in einer Vereinigung zusammengeführt werden. Die Beschränkung wirkt sich nicht rückwirkend auf vorhandene Schema aus. Es wird jedoch dringend empfohlen, Ihre Schema auf Feldkonflikte zu überprüfen und sie nach Bedarf zu bearbeiten. |
| Groß-/Kleinschreibung bei der Feldüberprüfung | Benutzerdefinierte Felder auf derselben Ebene müssen unabhängig von der Groß-/Kleinschreibung unterschiedliche Namen haben. Wenn Sie beispielsweise ein benutzerdefiniertes Feld mit dem Namen &quot;E-Mail&quot;hinzufügen, können Sie kein weiteres benutzerdefiniertes Feld mit dem Namen &quot;E-Mail&quot;hinzufügen. |

**Bekannte Probleme**

* Keine

Weitere Informationen zum Arbeiten mit XDM mit der [!DNL Schema Registry]-API und [!DNL Schema Editor]-Benutzeroberfläche finden Sie in der [XDM-Systemdokumentation](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

Neue gesetzliche und organisatorische Vorschriften geben Benutzern das Recht, auf Anfrage auf ihre personenbezogenen Daten zuzugreifen bzw. diese Daten aus Ihren Datenspeichern löschen zu lassen. Adobe Experience Platform [!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, die Sie bei der Verwaltung dieser Datenanforderungen von Ihren Kunden unterstützen. Mit [!DNL Privacy Service] können Sie Anfragen zum Zugriff und Löschen von persönlichen oder privaten Kundendaten aus Adobe Experience Cloud-Anwendungen stellen, wodurch die automatische Einhaltung der gesetzlichen und organisatorischen Datenschutzbestimmungen erleichtert wird.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| [!DNL Privacy Service] umgestalten | Der frühere Name &quot;GDPR Service&quot; wurde in [!DNL Privacy Service] umbenannt, da der Dienst zu anderen Vorschriften als dem GDPR wächst. |
| Neue API-Endpunkte | Der Basispfad für die API [!DNL Privacy Service] wurde von `/data/privacy/gdpr` auf `/data/core/privacy/jobs` aktualisiert. |
| Neue erforderliche `regulation`-Eigenschaft | Beim Erstellen neuer Aufträge in der API [!DNL Privacy Service] muss eine `regulation`-Eigenschaft in der Anforderungs-Nutzlast angegeben werden, unter welcher Regel der Auftrag verfolgt werden soll. Die zulässigen Werte sind `gdpr` und `ccpa`. |
| Unterstützung für [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] akzeptiert jetzt Zugriff-/Löschanforderungen aus der Adobe  [!DNL Primetime Authentication]und verwendet  `primetimeAuthentication` als Produktwert. |
| Verbesserungen der Benutzeroberfläche von Privacy Service | Separate Auftragsverfolgungsseiten für DSGVO- und CCPA-Vorschriften. Neuer **Regelungstyp **Dropdown-Liste zum Wechseln zwischen Tracking-Daten für GDPR und CCPA. |

**Bekannte Probleme**

* Keine

Weitere Informationen zu [!DNL Privacy Service] erhalten Sie im Beginn unter [Übersicht über Privacy Service](../../privacy-service/home.md).

## Quellen {#sources}

Adobe Experience Platform kann Daten aus externen Quellen erfassen, während Sie diese Daten mithilfe der [!DNL Platform]-Dienste strukturieren, beschriften und erweitern können. Daten können aus verschiedenen Quellen erfasst werden, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

[!DNL Experience Platform]Im Rahmen von stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Unterstützung für Kundenattributdaten | UI- und API-Unterstützung zum Erstellen von Streaming-Connectors zum Erfassen von Kundenattributdaten. |
| Zusätzliche Dateiformatunterstützung für Cloud-Datenspeicherung | Die Dateierfassung aus Cloud-Datenspeicherung unterstützt jetzt XDM-konforme Dateiformate wie Parquet und JSON. |
| Unterstützung für Zugriffskontrollen | Das Zugriffskontrolle-Framework in Adobe Experience Platform bietet die erforderlichen Berechtigungen, um den Zugriff auf Quellen bei der Datenerfassung zu ermöglichen. Je nach Berechtigungsstufe kann ein Benutzer Ansichten- und Quelldateien ausführen, Quellen verwalten oder den Zugriff ganz verweigern. |

**Berechtigungen für Zugriffskontrollen**

| Kategorie | Berechtigung | Beschreibung |
|--- | --- | ---|
| Datenerfassung | Verwalten von Quellen | Zugriff zum Lesen, Erstellen, Bearbeiten und Deaktivieren von Quellen. |
| Datenerfassung | Anzeigen von Quellen | Schreibgeschützter Zugriff auf verfügbare Quellen auf der Registerkarte **[!UICONTROL Katalog]** und authentifizierte Quellen auf der Registerkarte **[!UICONTROL Durchsuchen]**. |

**Bekannte Probleme**

* Keine

Weiterführende Informationen zu Quellen finden Sie in der [Quellenübersicht](../../sources/home.md)

## Ziele {#destinations}

In [Echtzeit-CDP](../../rtcdp/overview.md) sind Ziele vordefinierte Integrationen mit Zielplattformen, die Daten auf nahtlose Weise an diese Partner aktivieren.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Unterstützung für Zugriffskontrollen | Die Funktion Ziele in der Echtzeit-Kundendatenplattform funktioniert mit Zugangssteuerungsberechtigungen von Adobe Experience Platform. Je nach Berechtigungsstufe Ihres Anwenders können Sie Ziele anzeigen, verwalten und aktivieren. |

**Berechtigungen für Zugriffskontrollen**

| Kategorie | Berechtigung | Beschreibung |
|--- | --- | ---|
| Ziele | Verwalten von Zielen | Zugriff auf das Lesen, Erstellen, Bearbeiten und Deaktivieren von Zielen. |
| Ziele | Anzeigen von Zielen | Schreibgeschützter Zugriff auf verfügbare Ziele auf der Registerkarte **[!UICONTROL Katalog]** und authentifizierte Ziele auf der Registerkarte **Durchsuchen.** |
| Ziele | Aktivieren von Zielen | Möglichkeit, Daten an Ziele zu aktivieren. Für diese Berechtigung muss dem Profil &quot;Ansicht&quot;entweder &quot;Ziele verwalten&quot;oder &quot;Zielorte verwalten&quot;hinzugefügt werden. |

**Bekannte Probleme**

* Keine

Weiterführende Informationen dazu finden Sie unter [Ziele – Übersicht](../../destinations/home.md).
