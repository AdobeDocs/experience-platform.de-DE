---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise Januar 2024 für Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: a4d6c72cc2c3f5f547a3c66e509d520d3fed29ea
workflow-type: tm+mt
source-wordcount: '974'
ht-degree: 40%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: Mittwoch, 30. Januar 2024**

Neue Funktionen in Adobe Experience Platform:

- [Anwendungsbeispiele für Playbooks](#use-case-playbooks)

Aktualisierungen vorhandener Funktionen im Experience Platform:

- [Dashboards](#dashboards)
- [Datenvorbereitung](#data-prep)
- [Ziele](#destinations)
- [Real-Time Customer Data Platform](#rtcdp)
- [Echtzeit-Kundenprofil](#profile)
- [Quellen](#sources)

## Anwendungsbeispiele für Playbooks {#use-case-playbooks}

Die [!UICONTROL Anwendungsbeispiele für Playbooks] -Funktion ist jetzt allgemein für alle Kunden von Real-Time CDP und Adobe Journey Optimizer verfügbar. [!UICONTROL Anwendungsbeispiele für Playbooks] sind so konzipiert, dass Benutzer beim Einstieg in Real-time Customer Data Platform oder Adobe Journey Optimizer bei der Bewältigung von Herausforderungen unterstützt werden. Wenn Sie sich nicht sicher sind, wo Sie beginnen oder wie Sie die richtigen Assets für Ihre gewünschten Anwendungsfälle erstellen, können Sie mithilfe von &quot;Case Playbooks&quot;verschiedene Assets erstellen, damit Sie sie testen und in Produktionsumgebungen importieren können, sobald sie bereit sind.

Erste Schritte mit [!UICONTROL Anwendungsbeispiele für Playbooks], lesen Sie die folgenden Dokumentationsseiten:

- Lesen Sie die [Übersichtsseite](/help/use-case-playbooks/playbooks/overview.md) um den Zweck und die Verfügbarkeitsdaten zu verstehen und eine umfassende Demonstration der Funktionsweise von Playbooks zu erhalten, von der Entdeckung über das Erstellen von Instanzen bis hin zum Importieren generierter Assets in andere Sandbox-Umgebungen.
- Liste aller [verfügbare Playbooks](/help/use-case-playbooks/playbooks/playbooks-list.md), nach Produkt gruppiert (Real-Time CDP oder Journey Optimizer)
- Informationen zu allen [erforderliche Berechtigungen](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) , um die Bücher und die von den Büchern erzeugten Assets zu verwenden.
- Verstehen Sie die [Datenerfassungsfunktion](/help/use-case-playbooks/playbooks/data-awareness.md) , mit dem Sie generierte Assets in andere Sandbox-Umgebungen kopieren können
- Get [Tipps zur Fehlerbehebung](/help/use-case-playbooks/playbooks/troubleshooting.md) wenn bei der Verwendung von Anwendungsfall-Playbooks Fehler oder Schwierigkeiten auftreten.

## Datenvorbereitung {#data-prep}

Die Datenvorbereitung ermöglicht es Dateningenieurinnen und -ingenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Zuordnungsfunktionen | <ul><li>`object_to_map`: Verwenden Sie die `object_to_map` -Funktion zum Erstellen von Zuordnungs-Datentypen. Diese Funktion unterstützt mehrere verschiedene Syntaxen. Weitere Informationen finden Sie im Handbuch unter [Funktionen für Hierarchien - Objekte](../../data-prep/functions.md#objects). </li><li>`to_map`: Verwenden Sie die `to_map` -Funktion verwenden, um eine Zuordnung mit den angegebenen Feldnamen- und Wertpaaren mithilfe von Objekten zu erstellen. Weitere Informationen finden Sie im Handbuch unter [Funktionen für Hierarchien - Maps](../../data-prep/functions.md#map). </li><li>`array_to_map`: Verwenden Sie die `array_to_map` -Funktion verwenden, um eine Zuordnung mit den angegebenen Feld-Namen- und Wertpaaren mithilfe von Objekt-Arrays zu erstellen. Weitere Informationen finden Sie im Handbuch unter [Funktionen für Hierarchien - Maps](../../data-prep/functions.md#map). |

{style="table-layout:auto"}

Weitere Informationen zur Datenvorbereitung finden Sie im Abschnitt [Datenvorbereitung - Übersicht](../../data-prep/home.md).

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, über die Sie wichtige Einblicke zu den Daten Ihres Unternehmens erhalten, die in täglichen Schnappschüssen erfasst werden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| SQL anzeigen | Jetzt können Sie die SQL hinter Ihren Profilen, Audiences, Zielen und benutzerdefinierten Einblicken anzeigen und die Abfrage dann über den Abfrage-Editor nach Bedarf ausführen. Lassen Sie sich von der SQL von über 40 vorhandenen Einblicken inspirieren, um neue Abfragen zu erstellen, die anhand Ihrer geschäftlichen Anforderungen einzigartige Einblicke aus Platform-Daten gewinnen. Weitere Informationen finden Sie im Handbuch unter [Anzeigen von Insight SQL](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, finden Sie in der [Übersicht über Dashboards](../../dashboards/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue Ziele** {#new-destinations}

| Ziel | Beschreibung |
| ----------- | ----------- |
| [Öffentliche Verbindung](../../destinations/catalog/advertising/pubmatic.md) | Verwenden Sie dieses Ziel, um Zielgruppendaten an die [!DNL PubMatic Connect] Plattform. |

{style="table-layout:auto"}

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Real-Time Customer Data Platform {#rtcdp}

Die auf Experience Platform aufbauende Real-Time Customer Data Platform ([!DNL Real-Time CDP]) hilft Unternehmen dabei, bekannte und unbekannte Daten zusammenzuführen, sodass sich während der gesamten Customer Journey Kundenprofile mit intelligenten Entscheidungen aktivieren lassen. [!DNL Real-Time CDP] kombiniert mehrere Unternehmensdatenquellen, um Kundenprofile in Echtzeit zu erstellen. Segmente, die aus diesen Profilen erstellt wurden, können dann an nachgelagerte Ziele gesendet werden, um eine personalisierte Eins-zu-Eins-Kundenerfahrung über alle Kanäle und Geräte hinweg bereitzustellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktualisierungen der [Real-Time CDP-Startseite](https://experience.adobe.com) | <ul><li>**Profil-Widget**: Sie können jetzt das Profil -Widget verwenden, um zur Profilübersichtsseite zu navigieren und Profilmetriken für Ihre Organisation anzuzeigen.</li><li>**Profilmetrikkarte**: Die Karte Profilmetriken im Dashboard der Startseite zeigt jetzt die Gesamtanzahl der Profile in Ihrer Organisation an, abhängig von Ihrer jeweiligen Zusammenführungsrichtlinie.</li><li>**Schemas-Widget**: Sie können jetzt das Schemas-Widget verwenden, um zum Workflow für die Schemaerstellung in der Benutzeroberfläche zu navigieren.</li></ul> |

Weitere Informationen zu Real-Time CDP finden Sie unter [Übersicht über Real-Time CDP](../../rtcdp/overview.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus verschiedenen Kanälen, darunter Online-, Offline-, CRM- und Drittanbieter-Datenquellen, miteinander kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen bei der Lokalisierung der Standard-Dashboard-Karten des Profil-Viewers | Die Standardprofilkarten haben jetzt dynamisch lokalisierte Namen. Benutzerdefinierte Profilkarten können weiterhin benutzerdefinierte Namen haben, die bearbeitet werden können. |

{style="table-layout:auto"}

Weitere Informationen zum Echtzeit-Kundenprofil finden Sie in der [Profilübersicht](../../profile/home.md)

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative}[!DNL Oracle NetSuite] sources | Verwenden Sie die [!DNL Oracle NetSuite] Integrationen im Quellkatalog, um Daten aus Ihrem [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md) und [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md) Konten zu Experience Platform. |
| [!BADGE Beta]{type=Informative}[!DNL Braze Currents] source | Verwenden Sie die [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) Integration in den Quellkatalog, um Daten aus Ihrer [!DNL Braze] -Konto auf Experience Platform. |
| Unterstützung der Authentifizierung für Schlüsselpaare [!DNL Snowflake] Batch-Quelle | Sie können jetzt die Schlüsselpaar-Authentifizierung beim Erstellen einer neuen [!DNL Snowflake] Batch-Daten. Weitere Informationen finden Sie im Handbuch unter [Erstellen einer [!DNL Snowflake] -Konto mithilfe der API](../../sources/tutorials/api/create/databases/snowflake.md) oder das Handbuch [Erstellen einer [!DNL Snowflake] Konto über die Benutzeroberfläche](../../sources/tutorials/ui/create/databases/snowflake.md). |

{style="table-layout:auto"}

Weiterführende Informationen zu Quellen finden Sie in der [Übersicht über Quellen](../../sources/home.md).