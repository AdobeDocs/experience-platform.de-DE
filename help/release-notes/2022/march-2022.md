---
title: Adobe Experience Platform – Versionshinweise März 2022
description: Versionshinweise März 2022 für Adobe Experience Platform.
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: ht
source-wordcount: '1194'
ht-degree: 100%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 30. März 2022**

Neue Funktionen in Adobe Experience Platform:

- [Auditprotokolle](#audit-logs)
- [Verwandte Konten in Real-Time CDP B2B Edition](#related-accounts)

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Warnhinweise](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [Datenerfassung](#data-collection)
- [[!DNL Query Service]](#query-service)
- [Quellen](#sources)

## Auditprotokolle {#audit-logs}

Mit Experience Platform können Sie die Benutzeraktivität in Verbindung mit verschiedenen Services und Funktionen überprüfen. Die Auditprotokolle enthalten Informationen darüber, wer wann was getan hat.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Auditprotokolle für Datensatz, Schema, Klasse, Feldergruppe, Datentyp, Sandbox, Ziel, Segment, Zusammenführungsrichtlinie, berechnetes Attribut, Produktprofil und Konto (Adobe) | Dies sind die Ressourcen, die von Auditprotokollen aufgezeichnet werden. Wenn die Funktion aktiviert ist, werden Daten automatisch in den Auditprotokollen erfasst, sobald eine Aktivität stattfindet. Sie müssen die Datenerfassung in Auditprotokollen nicht manuell aktivieren. |
| Auditprotokolle exportieren | Auditprotokolle können als `CSV`- oder `JSON`-Datei heruntergeladen werden. Die generierten Dateien werden direkt auf Ihrem Computer gespeichert. |

{style=&quot;table-layout:auto&quot;}

Weiterführende Informationen zu Auditprotokollen in Platform finden Sie im Abschnitt [Übersicht über Auditprotokolle](../../landing/governance-privacy-security/audit-logs/overview.md).

## Verwandte Konten in Real-Time CDP B2B Edition {#related-accounts}

>[!NOTE]
>
>Die Funktion „verwandte Konten“ ist nur für Kunden der Real-Time CDP B2B Edition verfügbar.

B2B-Unternehmen haben häufig ihre Kundeninformationen in mehreren Systemen gespeichert, von denen jedes nur teilweise oder sogar widersprüchliche Daten für dieselbe reale Geschäftseinheit enthält. Dies stellt eine enorme Herausforderung dar, eine präzise Ansicht der Unternehmenskunden zu erhalten und mindert die Effizienz und Effektivität der B2B-Marketing- und Verkaufsaktivitäten. Mit der Einführung verwandter Konten zeigt [!DNL Real-Time CDP B2B] jetzt eine Liste von Konten an, die dem Konto, das Sie durchsuchen, ähnlich sind. Sie können die verwandten Konten in Ihre Segmentdefinitionen einbeziehen, um Ihre Reichweite zu erweitern oder umfassendere Kriterien auf Ihre Segmente anzuwenden.

Weitere Informationen zur Funktion finden Sie auf den folgenden Dokumentationsseiten:

- [Übersicht über verwandte Konten in Real-Time CDP B2B Edition](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Registerkarte „Verwandte Konten“ im Handbuch zur Benutzeroberfläche für Kontoprofile](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [Verwendung verwandter Konten in Segmentdefinitionen](../../rtcdp/segmentation/b2b.md#related-accounts)

Weitere Informationen zu Real-Time CDP B2B Edition finden Sie in der [Übersicht](../../rtcdp/overview.md).

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise zu Adobe Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise] in der Platform-Benutzeroberfläche abonnieren. Zusätzlich können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Warnhinweisregeln | Für Quellen im Zusammenhang mit der Datenaufnahme stehen nun zwei neue Warnhinweisregeln zur Verfügung. Die aktualisierte Liste der Warnhinweistypen finden Sie in der Übersicht zu [Warnhinweisregeln](../../observability/alerts/rules.md). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Warnhinweisen in Platform finden Sie im Abschnitt [Warnhinweise – Übersicht](../../observability/alerts/overview.md).

## Dashboards {#dashboards}

Adobe Experience Platform bietet mehrere [!DNL dashboards], in denen basierend auf täglichen Momentaufnahmen der Daten wichtige Informationen zu den Unternehmensdaten dargestellt werden.

### Profil-Dashboards

Im Dashboard „Profile“ wird eine Momentaufnahme der Attributdaten (Datensatzdaten) wiedergegeben, die sich in Ihrem Unternehmen im Profilspeicher in Experience Platform befinden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Widget „Nicht segmentierte Profile“ | Dieses Widget gibt die Gesamtanzahl aller Profile an, die mit keinem Segment verbunden sind. Der generierte Wert gibt die zum Zeitpunkt der letzten Momentaufnahme korrekte Anzahl an und zeigt, wie viele Profile in Ihrem gesamten Unternehmen aktiviert werden können. Weitere Informationen dazu finden Sie in der [Dokumentation zu Standard-Widgets für Profile](../../dashboards/guides/profiles.md#standard-widgets). |
| Widget „Trend unsegmentierter Profile“ | Dieses Widget bietet eine grafische Darstellung der Anzahl der Profile, die in einem bestimmten Zeitraum nicht mit einem Segment verbunden sind. Der Trend kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. Weitere Informationen dazu finden Sie in der [Dokumentation zu Standard-Widgets für Profile](../../dashboards/guides/profiles.md#standard-widgets). |
| Widget „Nicht segmentierte Profile nach Identität“ | Dieses Widget kategorisiert die Gesamtzahl der nicht segmentierten Profile anhand ihrer eindeutigen Kennung. Die Daten werden in einem Balkendiagramm visualisiert. Weitere Informationen dazu finden Sie in der [Dokumentation zu Standard-Widgets für Profile](../../dashboards/guides/profiles.md#standard-widgets). |
| Widget „Einzelidentitätsprofile“ | Dieses Widget gibt die Anzahl der Profile in Ihrem Unternehmen an, die zur Erstellung ihrer Identität nur über einen einzigen ID-Typ verfügen (entweder eine E-Mail oder eine ECID). Weitere Informationen dazu finden Sie in der [Dokumentation zu Standard-Widgets für Profile](../../dashboards/guides/profiles.md#standard-widgets). |

{style=&quot;table-layout:auto&quot;}

Weiterführende Informationen zu Profil-Dashboards finden Sie im Abschnitt [Profil-Dashboards – Übersicht](../../dashboards/guides/profiles.md).

### Ziele-Dashboards

Im Dashboard „Ziele“ finden Sie eine Momentaufnahme der Ziele, die Ihr Unternehmen in Experience Platform aktiviert hat.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Zielanzahl-Widget | Dieses Widget gibt die Gesamtzahl der verfügbaren Endpunkte an, an denen eine Zielgruppe im System aktiviert und bereitgestellt werden kann. Diese Zahl umfasst sowohl aktive als auch inaktive Ziele. Weitere Informationen dazu finden Sie in der [Dokumentation zum Standard-Widget für Ziele](../../dashboards/guides/destinations.md#standard-widgets). |

{style=&quot;table-layout:auto&quot;}

Weiterführende Informationen zu Ziel-Dashboards in Platform finden Sie im Abschnitt [Ziele-Dashboards – Übersicht](../../dashboards/guides/destinations.md).

## Datenerfassung {#data-collection}

Platform bietet eine Reihe von Technologien, mit denen Sie Client-seitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie an Adobe oder andere Ziele weitergegeben, transformiert und verteilt werden können.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Globale Datenstromeinstellungen | Sie können jetzt beim Konfigurieren eines Datenstroms mehrere neue globale Einstellungen konfigurieren: Ort, First-Party-ID-Cookie und Third-Party-ID-Synchronisierung. Weitere Informationen dazu finden Sie im Handbuch zur Datenstrom-Benutzeroberfläche im Abschnitt [Konfigurieren eines Datenstroms](../../edge/datastreams/overview.md#create). |
| [Edge Network Server-API](../../server-api/overview.md) | Mit der Server-API können Kunden mithilfe eines neuen, authentifizierten Endpunkts mit dem Experience Platform Edge Network interagieren, wodurch eine Vielzahl von Datenerfassungs-, Personalisierungs-, Werbungs- und Marketing-Anwendungsfällen ermöglicht wird. |

Weitere Informationen zur Datenerfassung in Platform finden Sie in der [Übersicht zur Datenerfassung](../../collection/home.md).

## Abfrage-Service {#query-service}

[!DNL Query Service] ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Datenwissenschafts-Arbeitsbereich oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| `table_exists` | Mit diesem neuen Befehl wird bestätigt, ob im System derzeit eine Tabelle vorhanden ist oder nicht. Der Befehl gibt einen booleschen Wert zurück: `true`, wenn eine Tabelle **vorhanden** ist, und `false`, wenn **keine** Tabelle vorhanden ist. Weitere Informationen finden Sie in der [SQL-Syntax-Dokumentation](../../query-service/sql/syntax.md). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu den verfügbaren Funktionen finden Sie im Abschnitt [Query Service – Übersicht](../../query-service/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Services herstellen, Zeiten für Aufnahmedurchgänge festlegen und den Durchsatz der Datenaufnahme verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Quellen für die B2B-Nutzung jetzt verfügbar | Sie können jetzt alle verfügbaren Quellen in Platform für B2B-Anwendungsfälle verwenden. Eine vollständige Liste der verfügbaren Quellen finden Sie im [Quellkatalog](../../sources/home.md). |
| Allgemeine Verfügbarkeit der neuen [!DNL Oracle Eloqua]-Quelle | Sie können jetzt die [!DNL Oracle Eloqua]-Quelle verwenden, um Daten aus Ihrer [!DNL Oracle Eloqua]-Instanz (Konto, Kampagne, Kontakte) nahtlos in Platform aufzunehmen. Weitere Informationen finden Sie in der Dokumentation zur [Erstellung einer  [!DNL Oracle Eloqua] -Quellverbindung](../../sources/connectors/marketing-automation/oracle-eloqua.md). |
| API-Verbesserungen für [!DNL Data Landing Zone] | Die [!DNL Data Landing Zone]-Quelle unterstützt jetzt die automatische Erkennung von Dateieigenschaften bei Verwendung der [!DNL Flow Service]-API. Weitere Informationen finden Sie in der Dokumentation zur [Erstellung einer  [!DNL Data Landing Zone] -Quellverbindung](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Quellen finden Sie im Abschnitt [Quellen – Übersicht](../../sources/home.md).
