---
title: Adobe Experience Platform – Versionshinweise Januar 2024
description: Versionshinweise Januar 2024 für Adobe Experience Platform.
exl-id: d4b3c5b2-3adb-41fd-91ad-f4c0f21d2325
source-git-commit: 8be502c9eea67119dc537a5d63a6c71e0bff1697
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 40%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: Mittwoch, 30. Januar 2024**

Neue Funktionen in Adobe Experience Platform:

- [Anwendungsfall-Playbooks](#use-case-playbooks)

Aktualisierungen vorhandener Funktionen im Experience Platform:

- [Attributbasierte Zugriffssteuerung](#abac)
- [Datenvorbereitung](#data-prep)
- [Dashboards](#dashboards)
- [Ziele](#destinations)
- [Identity Service](#identity-service)
- [Real-Time Customer Data Platform](#rtcdp)
- [Echtzeit-Kundenprofil](#profile)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Anwendungsfall-Playbooks {#use-case-playbooks}

Die Funktion [!UICONTROL Anwendungsfall-Playbooks] ist jetzt allgemein für alle Real-Time CDP- und Adobe Journey Optimizer-Kunden verfügbar. [!UICONTROL Anwendungsfall-Playbooks] sind so konzipiert, dass sie Benutzer bei der Bewältigung von Problemen unterstützen, wenn sie mit Real-time Customer Data Platform oder Adobe Journey Optimizer beginnen. Wenn Sie sich nicht sicher sind, wo Sie beginnen oder wie Sie die richtigen Assets für Ihre gewünschten Anwendungsfälle erstellen, können Sie mithilfe von &quot;Case Playbooks&quot;verschiedene Assets erstellen, damit Sie sie testen und in Produktionsumgebungen importieren können, sobald sie bereit sind.

Lesen Sie die folgenden Dokumentationsseiten, um mit [!UICONTROL Nutzungsszenario-Playbooks] zu beginnen:

- Lesen Sie die [Übersichtsseite](/help/use-case-playbooks/playbooks/overview.md) , um den Zweck und die Verfügbarkeitsinformationen zu verstehen und eine umfassende Demonstration der Funktionsweise von Playbooks von der Erkennung über das Erstellen von Instanzen bis hin zum Importieren generierter Assets in andere Sandbox-Umgebungen zu erhalten.
- Eine Liste aller [verfügbaren Playbooks](/help/use-case-playbooks/playbooks/playbooks-list.md) abrufen, gruppiert nach Produkt (Real-Time CDP oder Journey Optimizer)
- Hier erhalten Sie Informationen zu allen [erforderlichen Berechtigungen](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) für die Verwendung von Playbooks und den von den Playbooks generierten Assets.
- Grundlegendes zur [Datenerfassungsfunktion](/help/use-case-playbooks/playbooks/data-awareness.md), mit der Sie generierte Assets in andere Sandbox-Umgebungen kopieren können
- Besorgen Sie sich [Tipps zur Fehlerbehebung](/help/use-case-playbooks/playbooks/troubleshooting.md) , wenn Sie bei der Verwendung von &quot;Use Case Playbooks&quot;auf Fehler oder Schwierigkeiten stoßen.

## Attributbasierte Zugriffssteuerung {#abac}

Die attributbasierte Zugriffssteuerung ist eine Funktion von Adobe Experience Platform, die datenschutzbewussten Marken größere Flexibilität bei der Verwaltung von Benutzerzugriffen gibt. Einzelne Objekte wie Schemafelder und Segmente können Benutzerrollen zugewiesen werden. Mit dieser Funktion können Sie bestimmten Platform-Benutzenden in Ihrer Organisation den Zugriff auf einzelne Objekte gewähren oder sperren.

Mit der attributbasierten Zugriffssteuerung können Administratoren bzw. Administratorinnen Ihres Unternehmens den Zugriff von Benutzenden auf sensible persönliche Daten (SPD), persönlich identifizierbare Informationen (PII) und andere benutzerdefinierte Datentypen in allen Workflows und Ressourcen von Platform steuern. Admins können Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.

**Neue oder aktualisierte Dokumentation**

| Aktualisierung der Dokumentation | Beschreibung |
| --- | --- |
| Neue API-Endpunkte für attributbasierte Zugriffskontrolle dokumentiert | Die Referenzdokumentation zur API für die Zugriffskontrolle ](https://developer.adobe.com/experience-platform-apis/references/access-control/) enthält jetzt API-Rollen, Richtlinien und Produktendpunkte für die attributbasierte Zugriffskontrolle. [ Diese Endpunkte können zum Abrufen relevanter Rollen, Richtlinien und Produkte für einen Benutzer für bestimmte Ressourcen in einer angegebenen Sandbox verwendet werden. |

{style="table-layout:auto"}

Weitere Informationen zur attributbasierten Zugriffssteuerung finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](../../access-control/abac/overview.md). Eine umfassende Anleitung zum attributbasierten Zugriffssteuerungs-Workflow finden Sie im [Handbuch zur attributbasierten Zugriffskontrolle](../../access-control/abac/end-to-end-guide.md).

## Datenvorbereitung {#data-prep}

Die Datenvorbereitung ermöglicht es Dateningenieurinnen und -ingenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Zuordnungsfunktionen | <ul><li>`object_to_map`: Verwenden Sie die Funktion `object_to_map` , um Zuordnungs-Datentypen zu erstellen. Diese Funktion unterstützt mehrere verschiedene Syntaxen. Weitere Informationen finden Sie im Handbuch zu [Funktionen für Hierarchien - Objekte](../../data-prep/functions.md#objects) . </li><li>`to_map`: Verwenden Sie die Funktion `to_map` , um eine Zuordnung mit den angegebenen Feld- und Wertpaaren mithilfe von Objekten zu erstellen. Weitere Informationen finden Sie im Handbuch zu [Funktionen für Hierarchien - maps](../../data-prep/functions.md#map) . </li><li>`array_to_map`: Verwenden Sie die Funktion `array_to_map` , um eine Zuordnung mit den angegebenen Feld- und Wertpaaren mithilfe von Objekt-Arrays zu erstellen. Weitere Informationen finden Sie im Handbuch zu [Funktionen für Hierarchien - maps](../../data-prep/functions.md#map) . |

{style="table-layout:auto"}

Weitere Informationen zur Datenvorbereitung finden Sie in der [Datenvorbereitung - Übersicht](../../data-prep/home.md) .

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, über die Sie wichtige Einblicke zu den Daten Ihres Unternehmens erhalten, die in täglichen Schnappschüssen erfasst werden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| SQL anzeigen | Jetzt können Sie die SQL hinter Ihren Profilen, Audiences, Zielen und benutzerdefinierten Insights mit dem Umschalter SQL anzeigen anzeigen und die Abfrage dann über den Abfrage-Editor bei Bedarf ausführen. Der Zugriff auf die SQL-Datenbank, die Ihre Real-time Customer Data Platform-Einblicke unterstützt, hilft Ihnen, die Logik hinter der Analyse Ihres Datenmodells zu verstehen. Diese Transparenz macht Ihre Adobe-CDP-Daten in Echtzeit leichter zugänglich, verständlich und für die Entscheidungsfindung wirkungsvoll.<br>Lassen Sie sich von der SQL von über 40 vorhandenen Einblicken inspirieren, um neue Abfragen zu erstellen, die anhand Ihrer geschäftlichen Anforderungen eindeutige Einblicke aus Platform-Daten gewinnen. Die SQL ist auch für Ihre Einblicke in [Profile](../../dashboards/insights/profiles.md), [Zielgruppen](../../dashboards/insights/audiences.md) und [Ziele](../../dashboards/insights/destinations.md) in der Experience League-Dokumentation verfügbar. In diesen Dokumenten werden die geschäftlichen Anwendungsfälle hervorgehoben, die mit den Standardeinblicken beantwortet werden können. Weitere Informationen finden Sie im Handbuch zu [Anzeigen von Insight SQL](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, finden Sie in der [Übersicht über Dashboards](../../dashboards/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue Ziele** {#new-destinations}

| Ziel | Beschreibung |
| ----------- | ----------- |
| [Öffentliche Verbindung](../../destinations/catalog/advertising/pubmatic.md) | Verwenden Sie dieses Ziel, um Zielgruppendaten an die [!DNL PubMatic Connect]-Plattform zu senden. |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| Neuer Authentifizierungstyp **für übernommene Rolle** für Amazon S3-Ziele | Verwenden Sie den neuen Authentifizierungstyp für Rollen, wenn Sie Experience Platform mit Ihren Amazon S3-Buckets verbinden, wenn Sie Kontoschlüssel und geheime Schlüssel nicht mit Experience Platform teilen möchten. Weitere Informationen zur neuen Authentifizierungsmethode finden Sie im Abschnitt [Authentifizierung](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication) der Amazon S3-Dokumentation. |

{style="table-layout:auto"}

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Identity Service {#identity-service}

Der Adobe Experience Platform Identity Service hilft Ihnen, sich einen besseren Überblick über Ihre Kundinnen und Kunden und deren Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle und persönliche digitale Erlebnisse sorgen.

**Neue oder aktualisierte Dokumentation**

| Aktualisierung der Dokumentation | Beschreibung |
| --- | --- |
| Dokumentationsumstrukturierung | Die Dokumentation zum Identity Service wurde umstrukturiert, um die Präsentation und Übersichtlichkeit von Konzepten in Identity Service zu verbessern:<ul><li>Besuchen Sie die [Identity Service - Übersichtsseite](../../identity-service/home.md) , um eine erweiterte Terminologieanleitung, ein Anwendungsbeispiel mit detaillierten Informationen zu einer typischen Journey, eine Aufschlüsselung der Art und Weise zu erhalten, wie Identity Service Identitäten miteinander verknüpft, und eine Zusammenfassung der Rolle, die Identity Service innerhalb des Experience Platform-Ökosystems spielt.</li><li>Lesen Sie das Handbuch zu [Verständnis der Beziehung zwischen Identity Service und Echtzeit-Kundenprofil](../../identity-service/identity-and-profile.md) , um eine detaillierte Zusammenfassung der Zusammenarbeit zwischen den beiden Diensten und der Unterschiede zwischen ihren Zwecken, Prozessen, Eingaben und Ausgaben zu erhalten.</li><li>Erläuterungen und Visualisierungen zum Verhalten des Identitätsdiagramms bei verschiedenen Szenarien und Zeitstempeln finden Sie im Leitfaden zur Verknüpfungslogik des [Identitätsdienstes](../../identity-service/features/identity-linking-logic.md) .</li></ul> |

{style="table-layout:auto"}

Weiterführende Informationen zum Identity Service finden Sie in der [Übersicht zum Identity Service](../../identity-service/home.md) .

## Real-Time Customer Data Platform {#rtcdp}

Die auf Experience Platform aufbauende Real-Time Customer Data Platform ([!DNL Real-Time CDP]) hilft Unternehmen dabei, bekannte und unbekannte Daten zusammenzuführen, sodass sich während der gesamten Customer Journey Kundenprofile mit intelligenten Entscheidungen aktivieren lassen. [!DNL Real-Time CDP] kombiniert mehrere Unternehmensdatenquellen, um Kundenprofile in Echtzeit zu erstellen. Segmente, die aus diesen Profilen erstellt wurden, können dann an nachgelagerte Ziele gesendet werden, um eine personalisierte Eins-zu-Eins-Kundenerfahrung über alle Kanäle und Geräte hinweg bereitzustellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktualisierungen der [Real-Time CDP-Startseite](https://experience.adobe.com) | <ul><li>**Profil-Widget**: Sie können jetzt das Profil-Widget verwenden, um zur Profilübersichtsseite zu navigieren und Profilmetriken für Ihre Organisation anzuzeigen.</li><li>**Karte Profilmetriken**: Die Karte Profilmetriken im Dashboard der Startseite zeigt jetzt die Gesamtanzahl der Profile in Ihrer Organisation an, je nach Ihrer jeweiligen Zusammenführungsrichtlinie.</li><li>**Schemas-Widget**: Sie können jetzt das Schemas-Widget verwenden, um zum Workflow für die Schemaerstellung in der Benutzeroberfläche zu navigieren.</li></ul> |

{style="table-layout:auto"}

**Neue oder aktualisierte Dokumentation**

| Aktualisierung der Dokumentation | Beschreibung |
| --- | --- |
| Startseite der neuen Real-Time CDP-Dokumentation | Besuchen Sie die [neue Real-Time CDP-Dokumentationsseite](/help/rtcdp/home.md) , um einen Überblick über die ersten Schritte mit dem Produkt, Limits, Beispielanwendungsfällen und vieles mehr zu erhalten. |
| Anwendungsbeispiele für Real-Time CDP - Überblick | Besuchen Sie die Seite [Übersicht über neue Beispielanwendungsfälle](/help/rtcdp/use-case-guides/overview.md) , um eine Sammlung von Beispielanwendungsfällen zu erhalten, die Ihr Unternehmen mit Real-Time CDP erreichen kann. |

{style="table-layout:auto"}

Weitere Informationen zu Real-Time CDP finden Sie in der [Real-Time CDP - Übersicht](../../rtcdp/overview.md) .

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus verschiedenen Kanälen, darunter Online-, Offline-, CRM- und Drittanbieter-Datenquellen, miteinander kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen bei der Lokalisierung der Standard-Dashboard-Karten des Profil-Viewers | Die Standardprofilkarten haben jetzt dynamisch lokalisierte Namen. Benutzerdefinierte Profilkarten können weiterhin benutzerdefinierte Namen haben, die bearbeitet werden können. |

{style="table-layout:auto"}

Weitere Informationen zum Echtzeit-Kundenprofil finden Sie in der [Profilübersicht](../../profile/home.md) .

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Extern generierte Zielgruppen-Upload | Die maximale Anzahl von Spalten wurde auf **25** erhöht. |
| Schätzungen von Segment Builder | Schätzungen und qualifizierte Profile werden jetzt im Bereich der Zielgruppeneigenschaften angezeigt. Weitere Informationen zu dieser Änderung finden Sie im [UI-Handbuch für Segment Builder](../../segmentation/ui/segment-builder.md). |

{style="table-layout:auto"}

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Oracle NetSuite] sources | Verwenden Sie die [!DNL Oracle NetSuite] -Integrationen im Quellkatalog, um Daten aus Ihren [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md) - und [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md) -Konten an die Experience Platform zu übertragen. |
| Quelle [!BADGE Beta]{type=Informative} [!DNL Braze Currents] | Verwenden Sie die Integration von [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) im Quellkatalog, um Daten von Ihrem [!DNL Braze]-Konto an die Experience Platform zu übertragen. |
| Unterstützung der Authentifizierung für Schlüssel-Paar-Batch-Quellen für [!DNL Snowflake] | Sie können jetzt die Schlüsselpaar-Authentifizierung beim Erstellen eines neuen [!DNL Snowflake] -Kontos für Batch-Daten verwenden. Weitere Informationen finden Sie im Handbuch zum Erstellen eines [!DNL Snowflake] Kontos mithilfe der API](../../sources/tutorials/api/create/databases/snowflake.md) oder im Handbuch zum Erstellen eines  [!DNL Snowflake]  Kontos mithilfe der Benutzeroberfläche ](../../sources/tutorials/ui/create/databases/snowflake.md).[[ |

{style="table-layout:auto"}

Weiterführende Informationen zu Quellen finden Sie in der [Übersicht über Quellen](../../sources/home.md).
