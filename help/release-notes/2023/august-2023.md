---
title: Adobe Experience Platform – Versionshinweise
description: Versionshinweise August 2023 für Adobe Experience Platform.
exl-id: c67dca3a-eccb-427e-8ab3-b69c51b57938
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '1739'
ht-degree: 43%

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

Real-time Customer Data Platform ([!DNL Real-Time CDP]) basiert auf Experience Platform und hilft Unternehmen dabei, bekannte und unbekannte Daten zusammenzuführen, um Kundenprofile durch intelligente Entscheidungen auf der gesamten Journey zu aktivieren.

[!DNL Real-Time CDP] kombiniert mehrere Unternehmensdatenquellen, um Kundenprofile in Echtzeit zu erstellen. Segmente, die aus diesen Profilen erstellt wurden, können dann an nachgelagerte Ziele gesendet werden, um eine personalisierte Eins-zu-Eins-Kundenerfahrung über alle Kanäle und Geräte hinweg bereitzustellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Leitfaden für intelligente Wiedergewinnungsinteraktion | Im Benutzerhandbuch zu [Intelligent Re-Engagement](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) finden Sie Details dazu, wie Sie Kunden, die eine Konversion abgebrochen haben, erneut ansprechen können, bevor Sie sie auf intelligente und verantwortungsvolle Weise abschließen. In diesem Handbuch werden die folgenden Journey verwendet, um Kunden erneut anzusprechen: <ul><li>Journey zur erneuten Interaktion - Targeting von Kunden, die das Durchsuchen von Produkten abgebrochen haben.</li><li>Warenkorb-Journey - Targeting von Kunden, die Produkte in den Warenkorb gelegt, aber den Kauf noch nicht abgeschlossen haben.</li><li>Journey zur Bestellbestätigung - Fokus auf Produktkäufe</li></ul> Verwenden Sie den Link zu den detaillierten Feedback-Optionen unten im Benutzerhandbuch zu den [intelligenten Erneute-Interaktion](../../rtcdp/use-case-guides/intelligent-re-engagement/intelligent-re-engagement.md) , um Feedback zu geben. |
| Partnerdatenunterstützung | Führen Sie das Marketing über den oberen Trichter in Real-Time CDP mit Partnerprofilen und Partner-IDs aus, um neue Kunden zu erreichen und Ihre Erstanbieterdaten anzureichern: <ul><li>Kundenakquise und -adressierbarkeit: Nutzen Sie Cookie-Identifikatoren und Hash-PII von Datenpartnern Ihrer Wahl, um neue Nettokunden zu erreichen und die Abhängigkeit von Drittanbieter-Cookies zu reduzieren.</li><li>Vollständiges Trichtermarketing in einem einzigen System: Self-Service-Segmentierung, Zielgruppenkuratierung und native Aktivierung für potenzielle und bekannte Kunden in einem einzigen System.</li><li>Vertrauensgrundlage: Verwaltung von Partnerdaten und -profilen mit patentierter Datennutzung, Kennzeichnung, Zugriffskontrollen und mehr auf verantwortungsvolles Marketing. Lesen Sie die folgenden Fallhandbücher für weitere Informationen: Die Leitfäden für das Nutzungsszenario für Interessenten sind jetzt verfügbar. Lesen Sie die Anleitungen für Nutzungsszenarien, um zu erfahren, wie neue Kunden durch Nutzungsszenarios für die Prospektion kontaktiert und akquiriert werden:<ul><li>[prospecting](../../rtcdp/partner-data/prospecting.md)</li><li>[Onsite-Personalisierung](../../rtcdp/partner-data/onsite-personalization.md)</li><li>[Erstanbieterprofile ergänzen](../../rtcdp/partner-data/supplement-first-party-profiles.md)</li><li>[Interessenten-Zielgruppen aktivieren](../../destinations/ui/activate-prospect-audiences.md)</li></ul> |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [Real-Time CDP - Übersicht](../../rtcdp/overview.md) .

## Attributbasierte Zugriffssteuerung {#abac}

Die attributbasierte Zugriffssteuerung ist eine Funktion von Adobe Experience Platform, die datenschutzbewussten Marken größere Flexibilität bei der Verwaltung von Benutzerzugriffen gibt. Einzelne Objekte wie Schemafelder und Segmente können Benutzerrollen zugewiesen werden. Mit dieser Funktion können Sie bestimmten Platform-Benutzenden in Ihrer Organisation den Zugriff auf einzelne Objekte gewähren oder sperren.

Mit der attributbasierten Zugriffssteuerung können Administratoren bzw. Administratorinnen Ihres Unternehmens den Zugriff von Benutzenden auf sensible persönliche Daten (SPD), persönlich identifizierbare Informationen (PII) und andere benutzerdefinierte Datentypen in allen Workflows und Ressourcen von Platform steuern. Admins können Benutzerrollen definieren, die nur Zugriff auf bestimmte Felder und Daten haben, die diesen Feldern entsprechen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Sandbox-Konfiguration für Berechtigungs-Richtlinie | Mit der neuen Funktion für die Sandbox-Konfiguration von [Berechtigungsrichtlinien-Sandboxes](../../access-control/abac/ui/policies.md) können Sie je nach Ihren Anforderungen und Anforderungen eine attributbasierte Zugriffssteuerungsrichtlinie für alle oder eine ausgewählte Anzahl von Sandboxes erzwingen. |

{style="table-layout:auto"}

Weitere Informationen zur attributbasierten Zugriffssteuerung finden Sie unter [Attributbasierte Zugriffssteuerung – Übersicht](../../access-control/abac/overview.md). Eine umfassende Anleitung zum attributbasierten Zugriffssteuerungs-Workflow finden Sie im [Handbuch zur attributbasierten Zugriffskontrolle](../../access-control/abac/end-to-end-guide.md).

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere Dashboards, über die Sie wichtige Einblicke zu den Daten Ihres Unternehmens erhalten, die in täglichen Schnappschüssen erfasst werden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Anwendungsfall für Einverständnisanalyse und Tracking | Erfahren Sie, wie Sie mit dem Dokument [Einwilligungsanalyse und Tracking](../../dashboards/insights-use-cases/consent-analysis.md) ein Einwilligungs-Dashboard für verschiedene Marketing-Anwendungsfälle für Real-Time CDP-Daten erstellen. Es wird beschrieben, wie Sie eine Zielgruppe mit den entsprechenden Attributen für Ihre geschäftlichen Anforderungen erstellen und die Einblicke anschließend mithilfe von vorkonfigurierten Widgets in der Adobe Experience Platform-Benutzeroberfläche nutzen. Es enthält außerdem Anweisungen zum Erstellen Ihres eigenen benutzerdefinierten Widgets mit der benutzerdefinierten Dashboards-Funktion. Das Dokument behandelt die Zustimmungstrends und Einverständnisüberschneidungen bei Nutzungsszenarios. |

{style="table-layout:auto"}

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, erhalten Sie in der [Übersicht über Dashboards](../../dashboards/home.md).

## Datenerfassung {#data-collection}

Adobe Experience Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert und transformiert und an Adobe- oder Drittanbieter-Ziele weitergegeben werden können.

**Neue oder aktualisierte Funktionen**

| Typ | Funktion | Beschreibung |
| --- | --- | --- |
| Tags und Ereignisweiterleitung | [Experience Platform-Tags (China)](/help/tags/ui/publishing/premium-cdn.md) | Die neue Funktion für Experience Platform-Tags (China) verbessert die Zuverlässigkeit und Latenz von Websites, was zu schnelleren Reaktionszeiten für Kunden führt, die Tags auf Websites in China bereitstellen. Kunden können jetzt den JavaScript-Code in der Tag-Bibliothek bei der Implementierung von Websites in China verwenden. Diese Funktion wurde auch zum Unified Provisioning Protocol (UPP) hinzugefügt, sodass die Produktbereitstellung nach dem Kauf automatisiert werden kann. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [Übersicht über Datenerfassungen](../../tags/home.md).

## Datenerfassung {#data-ingestion}

Adobe Experience Platform bietet eine Vielzahl von Funktionen zur Aufnahme von Datentypen aller Art und beliebiger Latenz. Die Datenaufnahme kann anhand von Batch- oder Streaming-APIs, von Adobe bereitgestellten Quellen, Datenintegrationspartnern oder der Benutzeroberfläche von Adobe Experience Platform erfolgen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Änderungen an Datenaufnahme-Workflows | Datenzeilen, die Werte enthalten, die größer als der angegebene Datentyp sind (z. B. lange Daten, die als ganzzahliger Datentyp weitergegeben werden), werden jetzt zurückgewiesen und es werden Fehlermeldungen gemeldet. Zuvor wurden diese Zeilen ohne Vorankündigung abgelehnt. |

Weitere Informationen finden Sie in der [Datenerfassung - Übersicht](../../ingestion/home.md) .

## Datenvorbereitung {#data-prep}

Die Datenvorbereitung ermöglicht es Dateningenieurinnen und -ingenieuren, Daten dem Experience-Datenmodell (XDM) zuzuordnen, umzuformen und zu validieren.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für das Filtern von sekundären Identitäten | Sie können jetzt Data Prep verwenden, um Identitäten aus Adobe Analytics herauszufiltern, z. B. AAID und AACUSTOMID. Wenn diese Identitäten herausgefiltert werden, werden sie nicht in das Echtzeit-Kundenprofil aufgenommen. Ungefilterte Daten werden weiterhin in den Daten-Pool aufgenommen. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [Datenvorbereitung - Übersicht](../../data-prep/home.md) .

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen** {#destinations-new-updated-functionality}

- Sie können jetzt [Interessenten-Zielgruppen aktivieren](../../destinations/ui/activate-prospect-audiences.md), um Cloud-Speicher-Ziele zu erreichen.
- Der allgemeine [Aktivierungsschutz](../../destinations/guardrails.md#general-activation-guardrails) für maximal 100 Ziele pro Sandbox wurde auf eine _harte Grenze_ aktualisiert.

Weitere allgemeine Informationen zu Zielen finden Sie in der [Übersicht zu Zielen](../../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Adobe Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung |
| --- | --- | --- |
| Klasse | [[!UICONTROL XDM Individual Prospect Profile]](https://github.com/adobe/xdm/pull/1758/files) | Verwenden Sie diese Klasse, um Interessenten-Profile einzubringen, die aus den wichtigsten Anwendungsfällen für die Kundenakquise von Datenanbietern stammen. In der Dokumentation zu [[!UICONTROL XDM Individual Prospect Profile]](../../xdm/classes/prospect.md) finden Sie Beispiele und weitere Informationen. |

{style="table-layout:auto"}

**Aktualisierte XDM-Komponenten**

| Typ der Komponente | Name | Beschreibung der Aktualisierung |
| --- | --- | --- |
| Erweiterung ([!UICONTROL Adobe Analytics ExperienceEvent Full Extension]) | [[!UICONTROL Kontextdaten]](https://github.com/adobe/xdm/pull/1761/files) | [!UICONTROL Kontextdaten] -Zuordnungsobjekt, das zu [!UICONTROL Adobe Analytics ExperienceEvent Full Extension] hinzugefügt wurde, um Kontextdaten für Adobe Analytics bereitzustellen. |
| Feldergruppe | Mehrfach | Mehrere Felder wurden zu [[!UICONTROL Details des erweiterten Ereignissegments]](https://github.com/adobe/xdm/pull/1760/files) hinzugefügt. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [XDM-Systemübersicht](../../xdm/home.md).

## Identity Service {#identity-service}

Der Adobe Experience Platform Identity Service hilft Ihnen, sich einen besseren Überblick über Ihre Kundinnen und Kunden und deren Verhalten zu verschaffen, indem Identitäten geräte- und systemübergreifend zusammengeführt werden. So können Sie in Echtzeit für eindrucksvolle und persönliche digitale Erlebnisse sorgen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Änderungen an den Identitätsdiagrammbeschränkungen | Ende September wird das Identitätsdiagramm zu 50 Identitäten pro Diagramm geändert und die neueste Identität wird erfasst. Daher wird die älteste Identität basierend auf dem Erfassungszeitstempel und Identitätstyp gelöscht, wobei zuerst die Cookie-Identitätstypen gelöscht werden. Identitätsdiagramme sind heute auf 150 Identitäten pro Diagramm beschränkt. Sobald diese Grenze erreicht ist, werden Diagramme nicht mehr aktualisiert. Wenden Sie sich an Ihren Kundenbetreuer, wenn Ihre Produktions-Sandbox eine Änderung des Identitätstyps anfordern soll: <ul><li>einen benutzerdefinierten Namespace, bei dem die Personen-IDs (z. B. CRM-IDs) als Cookie-/Geräte-Identitätstyp konfiguriert sind.</li><li>einen benutzerdefinierten Namespace, bei dem Cookie-/Geräte-IDs als geräteübergreifender Identitätstyp konfiguriert sind.</li></ul> Adobe Engineering verarbeitet diese Anfragen manuell. Weitere Informationen finden Sie in den [Limits für Identity Service-Daten](../../identity-service/guardrails.md). |

Weitere Informationen finden Sie in der [Übersicht über den Identity Service](../../identity-service/home.md) .

## Segmentierungs-Service {#segmentation}

[!DNL Segmentation Service] ermöglicht es Ihnen, in [!DNL Experience Platform] gespeicherte Daten, die sich auf Einzelpersonen (wie Kundinnen und Kunden, Interessierte, Benutzerinnen und Benutzer oder Organisationen) beziehen, in Zielgruppen zu segmentieren. Sie können Zielgruppen über Segmentdefinitionen oder andere Quellen aus Ihren [!DNL Real-Time Customer Profile]-Daten erstellen. Diese Zielgruppen werden zentral auf [!DNL Platform] konfiguriert und verwaltet und stehen jeder Adobe-Lösung zur Verfügung.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Look-alike-Zielgruppen (begrenzte Verfügbarkeit) | Look-alike-Zielgruppen bieten intelligente Einblicke in jede Ihrer Zielgruppen und nutzen auf maschinellem Lernen basierende Einblicke, um hochwertige Kunden mit Ihren Marketing-Kampagnen zu identifizieren und anzusprechen. Mit Look-alike-Zielgruppen können Sie erweiterte Zielgruppen erstellen, die Kunden ähnlich Ihren leistungsstarken Zielgruppen ansprechen oder Kunden ähnlich wie zuvor konvertierten Zielgruppen ansprechen. Weitere Informationen zu Look-alike-Zielgruppen finden Sie in der [Übersicht über Look-alike-Zielgruppen](../../segmentation/ui/lookalike-audiences.md) . |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [Segmentierungsübersicht](../../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Allgemeine Verfügbarkeit von [!DNL SugarCRM] | [!DNL SugarCRM] -Quellen sind jetzt verfügbar. Verwenden Sie die Quellen [!DNL SugarCRM Accounts & Contacts] und [!DNL SugarCRM Events] zum Übermitteln von Daten aus Ihrem [!DNL SugarCRM]-Konto an Experience Platform. Weitere Informationen finden Sie im [[!DNL SugarCRM] Überblick](../../sources/connectors/crm/sugarcrm.md). |
| Unterstützung der On-Demand-Erfassung für Datenflüsse zu Quellen in der Benutzeroberfläche | Sie können jetzt für einen vorhandenen Datenfluss in der Benutzeroberfläche Flüsse nach Bedarf erstellen. Weitere Informationen finden Sie im Handbuch zum Erstellen eines On-Demand-Workflows für Quellen, die die Benutzeroberfläche verwenden](../../sources/tutorials/ui/on-demand-ingestion.md).[ |
| Unterstützung für neues `correlationID` -Feld für Adobe Analytics | Das Feld `_experience.decisioning.propositions.scopeDetails.correlationID` ist jetzt im Quell-Connector-Schema von Adobe Analytics verfügbar. Dieses Feld wird zur Unterstützung von A4T-Klassifizierungen verwendet und ab September 2023 ausgefüllt. |

{style="table-layout:auto"}

Weitere Informationen finden Sie in der [Quellenübersicht](../../sources/home.md).
