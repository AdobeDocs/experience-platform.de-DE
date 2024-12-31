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

Aktualisierungen vorhandener Funktionen in Experience Platform:

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

Die [!UICONTROL Nutzungsszenario-Playbooks]-Funktion ist jetzt allgemein für alle Kunden von Real-Time CDP und Adobe Journey Optimizer verfügbar. [!UICONTROL Anwendungsfall-Playbooks] wurden entwickelt, um Benutzende bei der Überwindung von Herausforderungen zu unterstützen, wenn sie mit Real-time Customer Data Platform oder Adobe Journey Optimizer beginnen. Wenn Sie sich nicht sicher sind, wo Sie anfangen sollen oder wie Sie die richtigen Assets für Ihre gewünschten Anwendungsfälle erstellen, bieten die Playbooks für Anwendungsfälle eine Inspiration und erstellen verschiedene Assets, die Sie testen und in Produktionsumgebungen importieren können, wenn Sie bereit sind.

Lesen Sie die folgenden Dokumentationsseiten, um mit [!UICONTROL Playbooks für Anwendungsfälle] zu beginnen:

- Lesen Sie die [Übersichtsseite](/help/use-case-playbooks/playbooks/overview.md) um den Zweck und die Verfügbarkeitsinformationen zu verstehen und eine durchgängige Demonstration der Funktionsweise von Playbooks von der Erkennung über die Erstellung von Instanzen bis zum Import generierter Assets in andere Sandbox-Umgebungen zu erhalten.
- Abrufen einer Liste aller [verfügbaren Playbooks](/help/use-case-playbooks/playbooks/playbooks-list.md) gruppiert nach Produkt (Real-Time CDP oder Journey Optimizer)
- Erhalten Sie Informationen zu allen [erforderlichen Berechtigungen](/help/use-case-playbooks/playbooks/get-started.md#grant-your-team-the-required-access-permissions) um Playbooks und die von den Playbooks generierten Assets zu verwenden.
- Machen Sie sich mit der [Funktionalität zur Datenerkennung](/help/use-case-playbooks/playbooks/data-awareness.md) vertraut, mit der Sie generierte Assets in andere Sandbox-Umgebungen kopieren können
- Erhalten Sie [Tipps zur Fehlerbehebung](/help/use-case-playbooks/playbooks/troubleshooting.md) wenn Sie bei der Verwendung von Anwendungsfall-Playbooks auf Fehler oder Schwierigkeiten stoßen.

## Attributbasierte Zugriffssteuerung {#abac}

Die attributbasierte Zugriffssteuerung ist eine Funktion von Adobe Experience Platform, die datenschutzbewussten Marken größere Flexibilität bei der Verwaltung von Benutzerzugriffen gibt. Einzelne Objekte wie Schemafelder und Segmente können Benutzerrollen zugewiesen werden. Mit dieser Funktion können Sie bestimmten Platform-Benutzenden in Ihrer Organisation den Zugriff auf einzelne Objekte gewähren oder sperren.

Mit der attributbasierten Zugriffssteuerung können Administratoren bzw. Administratorinnen Ihres Unternehmens den Zugriff von Benutzenden auf sensible persönliche Daten (SPD), persönlich identifizierbare Informationen (PII) und andere benutzerdefinierte Datentypen in allen Workflows und Ressourcen von Platform steuern. Admins können Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.

**Neue oder aktualisierte Dokumentation**

| Dokumentation aktualisieren | Beschreibung |
| --- | --- |
| Neue API-Endpunkte für die attributbasierte Zugriffssteuerung dokumentiert | Die [Referenzdokumentation zur Zugriffssteuerungs-](https://developer.adobe.com/experience-platform-apis/references/access-control/)&quot; enthält jetzt attributbasierte Zugriffssteuerungs-API-Rollen, Richtlinien und Produktendpunkte. Diese Endpunkte können verwendet werden, um relevante Rollen, Richtlinien und Produkte für einen Benutzer bzw. eine Benutzerin in bestimmten Ressourcen in einer bestimmten Sandbox abzurufen. |

{style="table-layout:auto"}

Weitere Informationen zur attributbasierten Zugriffssteuerung finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](../../access-control/abac/overview.md). Eine umfassende Anleitung zum attributbasierten Zugriffssteuerungs-Workflow finden Sie im [Handbuch zur attributbasierten Zugriffskontrolle](../../access-control/abac/end-to-end-guide.md).

## Datenvorbereitung {#data-prep}

Die Datenvorbereitung ermöglicht es Dateningenieurinnen und -ingenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Zuordnungsfunktionen | <ul><li>`object_to_map`: Verwenden Sie die Funktion `object_to_map` , um Zuordnungsdatentypen zu erstellen. Diese Funktion unterstützt mehrere verschiedene Syntaxen. Weitere Informationen finden Sie im Handbuch unter [Funktionen für Hierarchien - Objekte](../../data-prep/functions.md#objects). </li><li>`to_map`: Verwenden Sie die Funktion `to_map` , um mithilfe von -Objekten eine Zuordnung mit den angegebenen Feldnamen- und Wertepaaren zu erstellen. Weitere Informationen finden Sie im Handbuch unter [Funktionen für Hierarchien - Karten](../../data-prep/functions.md#map). </li><li>`array_to_map`: Verwenden Sie die Funktion `array_to_map` , um eine Zuordnung mit den angegebenen Feldnamen- und Wertepaaren mithilfe von Objekt-Arrays zu erstellen. Weitere Informationen finden Sie im Handbuch unter [Funktionen für Hierarchien - Karten](../../data-prep/functions.md#map). |

{style="table-layout:auto"}

Weitere Informationen zur Datenvorbereitung finden Sie unter [Datenvorbereitung - Übersicht](../../data-prep/home.md).

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, über die Sie wichtige Einblicke zu den Daten Ihres Unternehmens erhalten, die in täglichen Schnappschüssen erfasst werden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| SQL anzeigen | Sie können jetzt mit dem Umschalter SQL anzeigen den SQL-Code hinter Ihren Profilen, Zielgruppen, Zielen und benutzerdefinierten Einblicken anzeigen und dann die Abfrage bei Bedarf über den Abfrage-Editor ausführen. Der Zugriff auf den SQL-Code, der Ihren Real-time Customer Data Platform-Einblicken zugrunde liegt, hilft Ihnen, die Logik hinter der Analyse Ihres Datenmodells zu verstehen. Diese Transparenz macht Ihre Adobe-Real-Time CDP-Daten zugänglicher, verständlicher und wirkungsvoller für die Entscheidungsfindung.<br>Nutzen Sie die Inspiration aus dem SQL-Code von über 40 vorhandenen Einblicken, um neue Abfragen zu erstellen, die basierend auf Ihren Geschäftsanforderungen eindeutige Einblicke aus Platform-Daten gewinnen. Die SQL-Abfrage ist auch für Ihre [Profile](../../dashboards/insights/profiles.md), [Audiences](../../dashboards/insights/audiences.md) und [Ziele](../../dashboards/insights/destinations.md) in der Experience League-Dokumentation verfügbar. In diesen Dokumenten werden die geschäftlichen Anwendungsfälle beschrieben, die mit den standardmäßigen Einblicken beantwortet werden können. Weitere Informationen finden Sie im Handbuch unter [Anzeigen von Insight SQL](../../dashboards/view-sql.md). |

{style="table-layout:auto"}

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, finden Sie in der [Übersicht über Dashboards](../../dashboards/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue Ziele** {#new-destinations}

| Ziel | Beschreibung |
| ----------- | ----------- |
| [PubMatische Verbindung](../../destinations/catalog/advertising/pubmatic.md) | Verwenden Sie dieses Ziel, um Zielgruppendaten an die [!DNL PubMatic Connect]-Plattform zu senden. |

{style="table-layout:auto"}

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

| Funktionalität | Beschreibung |
| ----------- | ----------- |
| Neuer Authentifizierungstyp **übernommene Rolle** für Amazon S3-Ziele | Verwenden Sie den neuen Authentifizierungstyp Angenommene Rolle beim Verbinden von Experience Platform mit Ihren Amazon S3-Buckets, wenn Sie keine Kontoschlüssel und Geheimschlüssel für Experience Platform freigeben möchten. Weitere Informationen über die neue Authentifizierungsmethode finden Sie [ Abschnitt „Authentifizierung](/help/destinations/catalog/cloud-storage/amazon-s3.md#assumed-role-authentication) in der Dokumentation zu Amazon S3. |

{style="table-layout:auto"}

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Identity Service {#identity-service}

Der Adobe Experience Platform Identity Service hilft Ihnen, sich einen besseren Überblick über Ihre Kundinnen und Kunden und deren Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle und persönliche digitale Erlebnisse sorgen.

**Neue oder aktualisierte Dokumentation**

| Dokumentation aktualisieren | Beschreibung |
| --- | --- |
| Neustrukturierung der Dokumentation | Die Dokumentation zum Identity Service wurde umstrukturiert, um die Darstellung und Klarheit von Konzepten in Identity Service zu verbessern:<ul><li>Auf der [Identity Service-Übersichtsseite](../../identity-service/home.md) finden Sie ein erweitertes Terminologiehandbuch, ein Anwendungsbeispiel mit einer typischen Kunden-Journey, eine Aufschlüsselung der Verknüpfung von Identitäten mit Identity Service und eine Zusammenfassung der Rolle, die Identity Service im Experience Platform-Ökosystem spielt.</li><li>Lesen Sie das Handbuch unter [Verstehen der Beziehung zwischen Identity Service und Echtzeit-Kundenprofil](../../identity-service/identity-and-profile.md) für eine detaillierte Zusammenfassung, wie die beiden Services zusammenarbeiten und die Unterschiede zwischen ihren Zwecken, Prozessen, Eingaben und Ausgaben.</li><li>Erläuterungen und Visualisierungen [ Verhaltens des Identitätsdiagramms bei verschiedenen Szenarien und Zeitstempeln finden Sie ](../../identity-service/features/identity-linking-logic.md) Handbuch zur Identitätsdienst-Verknüpfungslogik .</li></ul> |

{style="table-layout:auto"}

Weitere Informationen zu Identity Service finden Sie unter [Identity Service - Übersicht](../../identity-service/home.md).

## Real-Time Customer Data Platform {#rtcdp}

Die auf Experience Platform aufbauende Real-Time Customer Data Platform ([!DNL Real-Time CDP]) hilft Unternehmen dabei, bekannte und unbekannte Daten zusammenzuführen, sodass sich während der gesamten Customer Journey Kundenprofile mit intelligenten Entscheidungen aktivieren lassen. [!DNL Real-Time CDP] kombiniert mehrere Unternehmensdatenquellen, um Kundenprofile in Echtzeit zu erstellen. Segmente, die aus diesen Profilen erstellt wurden, können dann an nachgelagerte Ziele gesendet werden, um eine personalisierte Eins-zu-Eins-Kundenerfahrung über alle Kanäle und Geräte hinweg bereitzustellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Aktualisierungen der Startseite von [Real-Time CDP](https://experience.adobe.com) | <ul><li>**Profile-Widget**: Sie können jetzt das Widget Profile verwenden, um zur Seite „Profile - Übersicht“ zu navigieren und Profilmetriken für Ihr Unternehmen anzuzeigen.</li><li>**Karte Profilmetriken**: Die Karte Profilmetriken im Dashboard der Startseite zeigt jetzt die Gesamtzahl der Profile in Ihrer Organisation an, abhängig von Ihrer jeweiligen Zusammenführungsrichtlinie.</li><li>**Widget „Schemata**: Sie können jetzt das Widget „Schemata“ verwenden, um zum Workflow für die Schemaerstellung in der Benutzeroberfläche zu navigieren.</li></ul> |

{style="table-layout:auto"}

**Neue oder aktualisierte Dokumentation**

| Dokumentation aktualisieren | Beschreibung |
| --- | --- |
| Neue Startseite zur Dokumentation zu Real-Time CDP | Auf der [neuen Homepage der Real-Time CDP](/help/rtcdp/home.md)Dokumentation) finden Sie Informationen zu den ersten Schritten mit dem Produkt, Leitplanken, Beispielanwendungsfällen und vieles mehr. |
| Beispiele für Real-Time CDP-Anwendungsfälle - Übersicht | Auf der [neuen Seite mit der Übersicht über Beispielanwendungsfälle](/help/rtcdp/use-case-guides/overview.md) finden Sie eine Sammlung von Beispielanwendungsfällen, die Ihr Unternehmen mit Real-Time CDP erreichen kann. |

{style="table-layout:auto"}

Weitere Informationen zu Real-Time CDP finden Sie in der [Übersicht über Real-Time CDP](../../rtcdp/overview.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus verschiedenen Kanälen, darunter Online-, Offline-, CRM- und Drittanbieter-Datenquellen, miteinander kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserungen bei der Lokalisierung der Standard-Dashboard-Karten des Profil-Viewers | Die Standardprofilkarten haben jetzt dynamisch lokalisierte Namen. Benutzerdefinierte Profilkarten können weiterhin benutzerdefinierte Namen haben, die bearbeitet werden können. |

{style="table-layout:auto"}

Weitere Informationen zum Echtzeit-Kundenprofil finden Sie in der [Profilübersicht](../../profile/home.md)

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] definiert eine bestimmte Untergruppe von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Segmente können auf Datensatzdaten (z. B. demografische Daten) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Extern generierter Zielgruppen-Upload | Die maximale Anzahl von Spalten wurde auf **25** erhöht. |
| Schätzungen von Segment Builder | Schätzungen und qualifizierte Profile werden jetzt im Abschnitt Zielgruppeneigenschaften angezeigt. Weitere Informationen zu dieser Änderung finden Sie im [Handbuch zur Benutzeroberfläche von Segment Builder](../../segmentation/ui/segment-builder.md). |

{style="table-layout:auto"}

Weitere Informationen zu [!DNL Segmentation Service] finden Sie in der [Übersicht zu Segmentierung](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Oracle NetSuite] | Verwenden Sie die [!DNL Oracle NetSuite] Integrationen im Quellkatalog, um Daten aus Ihren [[!DNL Oracle NetSuite Activities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-activities.md)- und [[!DNL Oracle NetSuite Entities]](../../sources/tutorials/ui/create/marketing-automation/oracle-netsuite-entities.md) auf Experience Platform zu übertragen. |
| [!BADGE Beta]{type=Informative} [!DNL Braze Currents] | Verwenden Sie die [[!DNL Braze Currents]](../../sources/tutorials/ui/create/marketing-automation/braze.md) Integration im Quellkatalog, um Daten von Ihrem [!DNL Braze]-Konto auf Experience Platform zu übertragen. |
| Unterstützung der Schlüsselpaar-Authentifizierung für [!DNL Snowflake] Batch-Quelle | Sie können jetzt die Schlüsselpaar-Authentifizierung verwenden, wenn Sie ein neues [!DNL Snowflake] für Batch-Daten erstellen. Weitere Informationen finden sich im Handbuch unter [Erstellen eines  [!DNL Snowflake] -Kontos mithilfe der ](../../sources/tutorials/api/create/databases/snowflake.md)) oder im Handbuch [Erstellen eines  [!DNL Snowflake] -Kontos mithilfe der Benutzeroberfläche](../../sources/tutorials/ui/create/databases/snowflake.md). |

{style="table-layout:auto"}

Weiterführende Informationen zu Quellen finden Sie in der [Übersicht über Quellen](../../sources/home.md).
