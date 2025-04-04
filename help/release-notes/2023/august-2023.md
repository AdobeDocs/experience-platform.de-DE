---
title: Adobe Experience Platform – Versionshinweise August 2023
description: Versionshinweise August 2023 für Adobe Experience Platform.
exl-id: c67dca3a-eccb-427e-8ab3-b69c51b57938
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1743'
ht-degree: 40%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: Donnerstag, 23. August 2023**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Real-Time Customer Data Platform](#rtcdp)
- [Attributbasierte Zugriffssteuerung](#abac)
- [Dashboards](#dashboards)
- [Datenerfassung](#data-collection)
- [Datenaufnahme](#data-ingestion)
- [Datenvorbereitung](#data-prep)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Identity Service](#identity-service)
- [Segmentierungs-Service](#segmentation)
- [Quellen](#sources)

## Real-Time Customer Data Platform {#rtcdp}

Real-Time Customer Data Platform ([!DNL Real-Time CDP]) basiert auf Experience Platform und hilft Unternehmen dabei, bekannte und unbekannte Daten zusammenzuführen, um Kundenprofile mit intelligenter Entscheidungsfindung auf dem gesamten Kunden-Journey zu aktivieren.

[!DNL Real-Time CDP] kombiniert mehrere Unternehmensdatenquellen, um Kundenprofile in Echtzeit zu erstellen. Segmente, die aus diesen Profilen erstellt wurden, können dann an nachgelagerte Ziele gesendet werden, um eine personalisierte Eins-zu-Eins-Kundenerfahrung über alle Kanäle und Geräte hinweg bereitzustellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Handbuch für den Anwendungsfall „Intelligente Rückgewinnung“ | Das [Handbuch zur intelligenten Rückgewinnung](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) enthält Details dazu, wie Kunden, die eine Konversion abgebrochen haben, erneut kontaktiert werden können, bevor sie sie auf intelligente und verantwortungsvolle Weise abschließen. In diesem Handbuch werden die folgenden Beispiel-Journey verwendet, um erneut mit Kunden zu interagieren: <ul><li>Journey zur Rückgewinnung - Targeting von Kunden, die die Produktsuche abgebrochen haben.</li><li>Journey bei Transaktionsabbruch - Targeting von Kunden, die Produkte in den Warenkorb gelegt haben, den Kauf jedoch noch nicht abgeschlossen haben.</li><li>Journey zur Bestellbestätigung - Fokus auf Produktkäufe</li></ul> Verwenden Sie den Link mit den detaillierten Feedback-Optionen unten im Handbuch [Anwendungsfall für die intelligente Rückgewinnung](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md), um Feedback zu geben. |
| Partner Data Support | Führen Sie Marketing im oberen Bereich des Trichters in Real-Time CDP mit durch Partner beschafften Interessentenprofilen und Partner-IDs durch, um neue Kunden zu erreichen und Ihre First-Party-Daten zu ergänzen: <ul><li>Kundenakquise und Adressierbarkeit: Nutzen Sie Cookie-lose Kennungen und gehashte PII von Datenpartnern der Wahl, um neue Kunden zu erreichen und die Abhängigkeit von Drittanbieter-Cookies zu reduzieren.</li><li>Vollständiges Trichtermarketing in einem einzigen System: Self-Service-Segmentierung, Zielgruppenkuratierung und native Aktivierung für potenzielle und bekannte Kunden in einem einzigen System.</li><li>Vertrauensgrundlage: Partnerdaten und -profile mit patentierter Datennutzung, Beschriftung, Zugriffskontrolle und mehr verantwortungsvoll zu vermarkten. Lesen Sie die folgenden Handbücher zu Anwendungsfällen für weitere Informationen: Die Handbücher zu Anwendungsfällen für Interessenten sind jetzt verfügbar. Lesen Sie die Leitfäden zu Anwendungsfällen für die Interessentengewinnung , um zu erfahren, wie Sie mithilfe von Anwendungsfällen für die Interessentengewinnung neue Kunden gewinnen und ansprechen können:<ul><li>[Kundenakquise](../../rtcdp/partner-data/prospecting.md)</li><li>[Onsite-Personalisierung](../../rtcdp/partner-data/onsite-personalization.md)</li><li>[Erstanbieterprofile ergänzen](../../rtcdp/partner-data/supplement-first-party-profiles.md)</li><li>[Interessenten-Zielgruppen aktivieren](../../destinations/ui/activate-prospect-audiences.md)</li></ul> |

{style="table-layout:auto"}

Weiterführende Informationen finden Sie in der Übersicht zu [Real-Time CDP](../../rtcdp/overview.md).

## Attributbasierte Zugriffssteuerung {#abac}

Die attributbasierte Zugriffssteuerung ist eine Funktion von Adobe Experience Platform, die datenschutzbewussten Marken größere Flexibilität bei der Verwaltung von Benutzerzugriffen gibt. Einzelne Objekte wie Schemafelder und Segmente können Benutzerrollen zugewiesen werden. Mit dieser Funktion können Sie bestimmten Experience Platform-Benutzenden in Ihrem Unternehmen den Zugriff auf einzelne Objekte gewähren oder sperren.

Durch attributbasierte Zugriffssteuerung können Admins Ihres Unternehmens den Zugriff von Benutzenden auf sensible persönliche Daten (SPD), persönlich identifizierbare Informationen (PII) und andere benutzerdefinierte Datentypen in allen Workflows und Ressourcen von Experience Platform steuern. Admins können Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Sandbox-Konfiguration der Berechtigungsrichtlinie | Mit der neuen Funktion [Berechtigungsrichtlinien - Sandbox](../../access-control/abac/ui/policies.md)Konfiguration) können Sie je nach Ihren Anforderungen und Anforderungen eine attributbasierte Zugriffssteuerungsrichtlinie für alle oder für eine ausgewählte Anzahl von Sandboxes durchsetzen. |

{style="table-layout:auto"}

Weitere Informationen zur attributbasierten Zugriffssteuerung finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](../../access-control/abac/overview.md). Eine umfassende Anleitung zum attributbasierten Zugriffssteuerungs-Workflow finden Sie im [Handbuch zur attributbasierten Zugriffskontrolle](../../access-control/abac/end-to-end-guide.md).

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, über die Sie wichtige Einblicke zu den Daten Ihres Unternehmens erhalten, die in täglichen Schnappschüssen erfasst werden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Anwendungsfall für Einverständnisanalyse und -Tracking | Erfahren Sie, wie Sie mit dem Dokument „Einverständnisanalyse und -[&quot; ein Einverständnis-Dashboard für verschiedene Marketing-Anwendungsfälle für Real-Time CDP-Daten ](../../dashboards/insights-use-cases/consent-analysis.md). Es wird beschrieben, wie Sie eine Zielgruppe mit den entsprechenden Attributen für Ihre Geschäftsanforderungen erstellen und dann die Erkenntnisse mithilfe vorkonfigurierter Widgets in der Adobe Experience Platform-Benutzeroberfläche nutzen können. Es enthält auch Anweisungen dazu, wie Sie mit der benutzerdefinierten Dashboards-Funktion Ihr eigenes benutzerdefiniertes Widget erstellen. Das Dokument behandelt Einverständnis-Trends und Anwendungsfälle mit Einverständnisüberschneidungen. |

{style="table-layout:auto"}

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, erhalten Sie in der [Übersicht über Dashboards](../../dashboards/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Typ | Funktion | Beschreibung |
| --- | --- | --- |
| Tags und Ereignisweiterleitung | [Experience Platform-Tags (China)](/help/tags/ui/publishing/premium-cdn.md) | Die neue Funktion &quot;Experience Platform Tags (China)“ verbessert die Zuverlässigkeit und Latenz von Websites, was zu schnelleren Antwortzeiten für Kunden führt, die Tags auf Websites in China bereitstellen. Kunden können jetzt den JavaScript-Code in der Tags-Bibliothek verwenden, wenn sie Websites in China implementieren. Diese Funktion wurde auch zum Unified Provisioning Protocol (UPP) hinzugefügt, sodass die Produktbereitstellung nach dem Kauf automatisiert werden kann. |

{style="table-layout:auto"}

Weitere Informationen finden Sie im Abschnitt [Übersicht über Datenerfassungen](../../tags/home.md).

## Datenerfassung {#data-ingestion}

Adobe Experience Platform bietet eine Vielzahl von Funktionen zur Aufnahme von Datentypen aller Art und beliebiger Latenz. Die Datenaufnahme kann anhand von Batch- oder Streaming-APIs, von Adobe bereitgestellten Quellen, Datenintegrationspartnern oder der Benutzeroberfläche von Adobe Experience Platform erfolgen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Änderungen an Workflows zur Datenaufnahme | Datenzeilen, die Werte enthalten, die größer sind als der angegebene Datentyp (z. B. lange Daten, die als ganzzahliger Datentyp übergeben werden), werden jetzt zurückgewiesen und Fehlermeldungen werden gemeldet. Zuvor wurden diese Zeilen ohne Warnung abgelehnt. |

Weitere Informationen finden Sie unter [Übersicht über die Datenaufnahme](../../ingestion/home.md).

## Datenvorbereitung {#data-prep}

Die Datenvorbereitung ermöglicht es Dateningenieurinnen und -ingenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für das Filtern sekundärer Identitäten | Sie können jetzt die Datenvorbereitung verwenden, um Identitäten aus Adobe Analytics herauszufiltern, z. B. AAID und AACUSTOMID. Wenn diese Identitäten herausgefiltert werden, werden sie nicht in das Echtzeit-Kundenprofil aufgenommen. Nicht gefilterte Daten werden weiterhin in den Data Lake aufgenommen. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Datenvorbereitung - Übersicht](../../data-prep/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

- Sie können jetzt [Zielgruppen von Interessenten aktivieren](../../destinations/ui/activate-prospect-audiences.md) zu Cloud-Speicherzielen hinzufügen.
- Die allgemeine [Aktivierungsleitplanke](../../destinations/guardrails.md#general-activation-guardrails) von maximal 100 Zielen pro Sandbox wurde aktualisiert und ist jetzt eine _feste Grenze_.

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Klasse | [[!UICONTROL XDM Individual Prospect Profile]](https://github.com/adobe/xdm/pull/1758/files) | Verwenden Sie diese Klasse, um Interessentenprofile einzubringen, die aus den Top-of-the-Funnel-Anwendungsfällen der Kundenakquise von Datenanbietern stammen. In der Dokumentation [[!UICONTROL XDM Individual Prospect Profile]](../../xdm/classes/prospect.md) finden Sie Beispiele und weitere Informationen. |

{style="table-layout:auto"}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung der Aktualisierung |
| --- | --- | --- |
| Erweiterung ([!UICONTROL Adobe Analytics ExperienceEvent Full Extension]) | [[!UICONTROL Kontextdaten]](https://github.com/adobe/xdm/pull/1761/files) | [!UICONTROL Kontextdaten: ] wurde zur vollständigen Erweiterung [!UICONTROL Adobe Analytics ExperienceEvent hinzugefügt] um Kontextdaten für Adobe Analytics bereitzustellen. |
| Feldergruppe | Mehrfach | Mehrere Felder wurden zu &quot;[[!UICONTROL  Ereignissegmentdetails“ ]](https://github.com/adobe/xdm/pull/1760/files). |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [Übersicht zum XDM-System](../../xdm/home.md).

## Identity Service {#identity-service}

Der Adobe Experience Platform Identity Service hilft Ihnen, sich einen besseren Überblick über Ihre Kundinnen und Kunden und deren Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle und persönliche digitale Erlebnisse sorgen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Änderungen an den Beschränkungen für Identitätsdiagramme | Bis Ende September wird das Identitätsdiagramm auf 50 Identitäten pro Diagramm geändert, und die neueste Identität wird aufgenommen. Infolgedessen wird die älteste Identität basierend auf dem Aufnahmezeitstempel und dem Identitätstyp gelöscht, wobei Cookie-Identitätstypen zuerst gelöscht werden. Heute haben Identitätsdiagramme ein Limit von 150 Identitäten pro Diagramm, und sobald dieses Limit erreicht ist, werden Diagramme nicht mehr aktualisiert. Wenden Sie sich an Ihren Kundenbetreuer, um eine Änderung des Identitätstyps anzufordern, wenn Ihre Produktions-Sandbox Folgendes enthält: <ul><li>Ein benutzerdefinierter Namespace, in dem die Personen-IDs (z. B. CRM-IDs) als Cookie-/Geräte-Identitätstyp konfiguriert sind.</li><li>Ein benutzerdefinierter Namespace, in dem Cookie-/Geräte-IDs als geräteübergreifender Identitätstyp konfiguriert sind.</li></ul> Adobe Engineering verarbeitet diese Anfragen manuell. Weitere Informationen finden Sie unter [ für Identity Service-Daten](../../identity-service/guardrails.md). |

Weitere Informationen finden Sie unter [Identity Service - Übersicht](../../identity-service/home.md).

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] ermöglicht es Ihnen, in [!DNL Experience Platform] gespeicherte Daten, die sich auf Einzelpersonen (wie Kundinnen und Kunden, Interessierte, Benutzerinnen und Benutzer oder Organisationen) beziehen, in Zielgruppen zu segmentieren. Sie können Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten erstellen. Diese Zielgruppen werden zentral auf [!DNL Experience Platform] konfiguriert und verwaltet und stehen jeder Adobe-Lösung zur Verfügung.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Lookalike-Zielgruppen (eingeschränkte Verfügbarkeit) | Lookalike-Zielgruppen bieten intelligente Einblicke in jede Ihrer Zielgruppen und nutzen auf maschinellem Lernen basierende Einblicke, um mit Ihren Marketing-Kampagnen hochwertige Kunden zu identifizieren und anzusprechen. Mit Lookalike-Zielgruppen können Sie erweiterte Zielgruppen erstellen, die Kundinnen und Kunden ähnlich Ihren hochleistungsfähigen Zielgruppen ansprechen oder Kundinnen und Kunden ähnlich wie zuvor konvertierte Zielgruppen ansprechen. Weitere Informationen zu Lookalike-Zielgruppen finden Sie unter [Lookalike-Zielgruppen - Übersicht](../../segmentation/types/account-audiences.md). |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Segmentierung - Übersicht](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Allgemeine Verfügbarkeit von [!DNL SugarCRM] | [!DNL SugarCRM] sind jetzt verfügbar. Verwenden Sie die Quellen [!DNL SugarCRM Accounts & Contacts] und [!DNL SugarCRM Events] zum Übermitteln von Daten aus Ihrem [!DNL SugarCRM]-Konto an Experience Platform. Weitere Informationen finden Sie im [[!DNL SugarCRM] Überblick](../../sources/connectors/crm/sugarcrm.md). |
| Unterstützung der On-Demand-Aufnahme von Quellen für Datenflüsse in der Benutzeroberfläche | Sie können jetzt Flussausführungen bei Bedarf für einen vorhandenen Datenfluss von Quellen in der Benutzeroberfläche erstellen. Weitere Informationen finden sich im Handbuch unter [Erstellen einer On-Demand-Flussausführung für Quellen mithilfe der Benutzeroberfläche](../../sources/tutorials/ui/on-demand-ingestion.md). |
| Unterstützung für neues `correlationID` für Adobe Analytics | Das Feld `_experience.decisioning.propositions.scopeDetails.correlationID` ist jetzt im Quell-Connector-Schema von Adobe Analytics verfügbar. Dieses Feld wird zur Unterstützung von A4T-Klassifizierungen verwendet und wird ab September 2023 ausgefüllt. |

{style="table-layout:auto"}

Weitere Informationen finden Sie im Abschnitt [Quellen - Übersicht](../../sources/home.md).
