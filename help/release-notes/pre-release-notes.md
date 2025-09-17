---
title: Hinweise zu Vorabversionen von Experience Platform
description: Eine Vorschau der neuesten Versionshinweise für Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: c592d007932835f5263d7f78b2e8155790313840
workflow-type: tm+mt
source-wordcount: '1217'
ht-degree: 24%

---

# Hinweise zu Vorabversionen von Adobe Experience Platform

>[!IMPORTANT]
>
>Dieses Dokument ist als **Vorschau** der Versionshinweise für den aktuellen Monat gedacht. Release-Elemente können sich ändern und in der endgültigen Version hinzugefügt oder entfernt werden.

>[!TIP]
>
>Versionshinweise zu anderen Adobe Experience Platform-Programmen finden Sie in der folgenden Dokumentation:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/de/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/de/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/de/docs/analytics-platform/using/releases/pre-release-notes)
>- [Komposition föderierter Zielgruppen](https://experienceleague.adobe.com/de/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/de/docs/real-time-cdp-collaboration/using/latest)

**Veröffentlichungsdatum: September 2025**

Neue Funktionen und Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [KI-Assistent](#ai-assistant)
- [Warnhinweise](#alerts)
- [Ziele](#destinations)
- [Experience-Datenmodell (XDM)](#xdm)
- [Query Service](#query-service)
- [Echtzeit-Kundenprofil](#profile)
- [Segmentierungs-Service](#segmentation-service)
- [Quellen](#sources)

## KI-Assistent {#ai-assistant}

Der Adobe Experience Platform-KI-Assistent ist ein Gesprächserlebnis, mit dem Sie Workflows in Adobe Experience Cloud-Anwendungen beschleunigen und optimieren können.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Agent Orchestrator | Adobe Experience Platform Agent Orchestrator ist die intelligente Ebene, die den KI-Assistenten antreibt. Wenn Sie Fragen stellen oder Hilfe anfordern, ruft Agent Orchestrator automatisch spezialisierte Agenten auf, um die richtigen Antworten zu erhalten. Agent Orchestrator speichert Ihren Gesprächsverlauf, sodass Sie auf natürliche Weise auf früheren Fragen aufbauen können, ohne den Kontext zu wiederholen, und kombiniert Einblicke aus mehreren Agenten, um Ihnen klare, einheitliche Antworten zu bieten. |
| Audience Agent | Mit der Audience Agent können Sie Einblicke zu Zielgruppen erhalten, einschließlich der Erkennung signifikanter Änderungen der Zielgruppengröße, der Erkennung doppelter Zielgruppen, der Untersuchung Ihres Zielgruppeninventars und des Abrufs der Zielgruppengröße. |

Weitere Informationen finden Sie unter [KI-Assistent - Übersicht](../ai-assistant/home.md).

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise für verschiedene Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise] in der Benutzeroberfläche von Experience Platform abonnieren. Zusätzlich können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Warnhinweise zur Aufnahme von Streaming-Profilen | Sie können jetzt zwei neue Warnhinweise für die Streaming-Aufnahme auf Datenflussebene abonnieren: <ul><li>Fehlerrate bei Streaming-Aufnahme überschritten</li><li>Rate der übersprungenen Streaming-Aufnahme überschritten</li></ul> Plattforminterne oder E-Mail-Warnungen benachrichtigen Sie, wenn die Schwellenwerte für den Standardschwellenwert oder einen von Ihnen definierten benutzerdefinierten Schwellenwert überschritten werden. Weitere Informationen finden Sie im Handbuch [Warnhinweise für Profile](../observability/alerts/rules.md#profile). |

{style="table-layout:auto"}

Weitere Informationen zu Warnhinweisen finden Sie im Abschnitt [[!DNL Observability Insights] Übersicht](../observability/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue oder aktualisierte Funktionen**

| Ziel | Beschreibung |
| --- | --- |
| [!BADGE Beta]{type=Informative} [!DNL Snowflake Batch] Connector | Ein neuer [!DNL Snowflake Batch]-Connector ist jetzt verfügbar und bietet eine Alternative zum Streaming-Connector für bestimmte Anwendungsfälle. |
| [!DNL Adform] | [!DNL Adform] ist ein führender Anbieter von Kauf- und Verkaufslösungen für programmatische Medien. Durch die Verbindung von Adform mit der Adobe Experience Platform können Sie Ihre Erstanbieter-Zielgruppen über Adform aktivieren, basierend auf der Experience Cloud ID (ECID). |
| [!DNL Data Landing Zone] Verschlüsselungsunterstützung | Sie können jetzt RSA-formatierte öffentliche Schlüssel anhängen, um Ihre exportierten Dateien zu verschlüsseln, sodass Sie dasselbe Sicherheitsniveau erhalten, das andere Cloud-Speicherziele für Ihre vertraulichen Informationen bieten. |
| Details zum Authentifizierungsablauf für [!DNL Pinterest] Ziele | Informationen zum Authentifizierungsablauf für [!DNL Pinterest] Ziele sind jetzt direkt in der Experience Platform-Benutzeroberfläche sichtbar, sodass Sie sehen können, wann Ihre Authentifizierung abläuft und erneuert wird, bevor sie zu Unterbrechungen Ihrer Datenflüsse führt. Sie können das Ablaufdatum Ihres Tokens über die Spalte **[!UICONTROL Account-Ablaufdatum]** entweder auf den Registerkarten **[[!UICONTROL Konten]](../destinations/ui/destinations-workspace.md#accounts)** oder **[[!UICONTROL Durchsuchen]](../destinations/ui/destinations-workspace.md#browse)** überwachen. |

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserte Funktionen zur Zielverwaltung in der Experience Platform-Benutzeroberfläche | Verbessern Sie Ihren Zielverwaltungs-Workflow mit neuen Sortierfunktionen auf den Registerkarten [[!UICONTROL Durchsuchen]](../destinations/ui/destinations-workspace.md#browse) und [[!UICONTROL Konten]](../destinations/ui/destinations-workspace.md#accounts). Sie können jetzt auch einen visuellen Indikator sehen, wenn Ihre Kontoauthentifizierung bald abläuft. |

Weitere Informationen finden Sie unter [Ziele - Übersicht](../destinations/home.md).

## Experience-Datenmodell (XDM) {#xdm}

XDM ist eine Open-Source-Spezifikation, die allgemeine Strukturen und Definitionen (Schemata) für Daten bereitstellt, die in Experience Platform importiert werden. Durch die Einhaltung von XDM-Standards können alle Kundenerlebnisdaten in eine gemeinsame Darstellung integriert werden, die Erkenntnisse schneller und besser integriert liefert. Sie können wertvolle Einblicke aus Kundenaktionen gewinnen, Zielgruppen durch Segmente definieren und Kundenattribute für Personalisierungszwecke verwenden.

**Neue Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Modellbasierte Schemata | Vereinfachen Sie Ihre Datenmodellierung mit modellbasierten Schemata. Sie können jetzt Schemas einfacher mit umfassenden Beispielen und Anleitungen erstellen. Diese Funktion steht derzeit Lizenzinhabern von Campaign Orchestration zur Verfügung und wird auf Kunden von Data Distiller bei GA ausgeweitet, was die Datenmodellierung zugänglicher und effizienter macht. Die Funktion unterstützt auch Zeitreihendaten und Funktionen zur Datenerfassung bei Änderungen. |

Weitere Informationen finden Sie in der [XDM-Übersicht](../xdm/home.md).

## Echtzeit-Kundenprofil {#profile}

Adobe Experience Platform ermöglicht die Bereitstellung koordinierter, konsistenter und relevanter Erlebnisse für Ihre Kundinnen und Kunden, unabhängig davon, wo und wann sie mit Ihrer Marke interagieren. Das Echtzeit-Kundenprofil liefert eine ganzheitliche Sicht auf jede einzelne Kundin und jeden einzelnen Kunden, indem es Daten aus verschiedenen Kanälen, darunter Online-, Offline-, CRM- und Drittanbieter-Datenquellen, miteinander kombiniert. Mit dem Profil können Sie Ihre Kundendaten in einer zentralen Ansicht zusammenführen, die eine aussagekräftige Darstellung jeder Kundeninteraktion mit Zeitstempel bietet.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Verbesserungen am Profil-Viewer | Die Version September 2025 enthält die folgenden Verbesserungen für den Profil-Viewer. <ul><li>**Kombinierte Ansicht**: Attribute, Ereignisse und Einblicke wurden in einer einzigen Ansicht kombiniert.</li><li>**KI-generierte Insights**: Auf der Seite mit Profildetails werden jetzt KI-generierte Insights angezeigt, sodass Sie über die aus Ihrem Profil generierten Details informiert sind. Diese Einblicke können Informationen wie Tendenz-Scores und Trendanalysen enthalten.</li><li>**Stilaktualisierung**: Die Seite mit den Profildetails wurde visuell aktualisiert.</li><li>**Durchsuchen**: Sie können jetzt Ihre Profile durch ein interaktives kartenbasiertes Karussell mit Suche und Anpassung durchsuchen.</li></ul> |

Weitere Informationen finden Sie unter [Übersicht über das Echtzeit-Kundenprofil](../profile/home.md).

## Segmentierungs-Service {#segmentation-service}

[!DNL Segmentation Service] definiert eine bestimmte Teilmenge von Profilen, indem das Kriterium beschrieben wird, das eine vermarktbare Personengruppe innerhalb Ihres Kundenstamms unterscheidet. Zielgruppen können auf Datensatzdaten (z. B. demografische Informationen) oder Zeitreihenereignissen basieren, die Kundeninteraktionen mit Ihrer Marke darstellen.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Konto-Zielgruppen mit veralteten Erlebnisereignissen | Nach dem Upgrade der B2B-Architektur werden Konto-Zielgruppen mit Erlebnisereignissen nicht mehr unterstützt. Verwenden Sie stattdessen den Ansatz „Neues Segment von Segmenten“: Erstellen Sie eine Zielgruppe „Personen“ mit Erlebnisereignissen und verweisen Sie dann beim Erstellen einer Konto-Zielgruppe auf diese Zielgruppe. Dies bietet einen flexibleren und verwaltbareren Ansatz zur Erstellung von B2B-Zielgruppen. |

**Wichtige Updates**

| Update | Beschreibung |
| ------- | ----------- |
| Rücksetzung der automatischen Aktualisierung der Zielgruppenschätzungen | Die Verbesserung der automatischen Aktualisierung für Zielgruppenschätzungen wurde rückgängig gemacht. Zielgruppenschätzungen werden weiterhin in Segment Builder generiert, aber die Funktion zur automatischen Aktualisierung wurde entfernt. |

Weitere Informationen finden Sie in der [[!DNL Segmentation Service] Übersicht](../segmentation/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Quellen in allgemeiner Verfügbarkeit | Die folgenden Quellen sind jetzt allgemein verfügbar: Mehrere Quell-Connectoren wurden von Beta auf allgemein verfügbar aktualisiert: <ul><li>[Acxiom-Datenaufnahme](../sources/connectors/data-partners/acxiom-data-ingestion.md)</li><li>[Datenaufnahme des potenziellen Kunden Acxiom](../sources/connectors/data-partners/acxiom-prospecting-data-import.md)</li><li>[Merkury Enterprise](../sources/connectors/data-partners/merkury.md)</li><li>[SAP Commerce](../sources/connectors/ecommerce/sap-commerce.md)</li></ul>. Diese Quellen werden jetzt vollständig unterstützt und sind für die Verwendung in der Produktion bereit. |
| Unterstützung der [!DNL Snowflake] Schlüsselpaar-Authentifizierung | Die Sicherheit für Snowflake-Verbindungen wurde durch die Unterstützung der Schlüsselpaar-Authentifizierung verbessert. Die Standardauthentifizierung (Benutzername/Kennwort) wird ab November 2025 eingestellt, sodass Kunden ermutigt werden, zur Verbesserung der Sicherheit zur Schlüsselpaar-Authentifizierung zu migrieren. |

Weitere Informationen finden Sie unter [Quelle – Übersicht](../sources/home.md).