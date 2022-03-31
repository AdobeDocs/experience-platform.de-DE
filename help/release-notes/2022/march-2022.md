---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
exl-id: 0d499aa6-e25d-4d34-ad32-5e4ab361cba1
source-git-commit: 5be8eac1603f1b81e45b4c0aeace5c2017b46149
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 25%

---

# Adobe Experience Platform – Versionshinweise

**Veröffentlichungsdatum: 30. März 2022**

Neue Funktionen in Adobe Experience Platform:

- [Auditprotokolle](#audit-logs)
- [Related accounts in Real-Time CDP B2B Edition](#related-accounts)

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Warnhinweise](#alerts)
- [[!DNL Dashboards]](#dashboards)
- [[!DNL Query Service]](#query-service)
- [Quellen](#sources)
<!-- - [Experience Data Model (XDM)](#xdm) -->

## Auditprotokolle {#audit-logs}

Mit Experience Platform können Sie die Benutzeraktivität für verschiedene Dienste und Funktionen überprüfen. Die Prüfprotokolle enthalten Informationen darüber, wer wann was getan hat.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Prüfprotokolle für Datensatz, Schema, Klasse, Feldergruppe, Datentyp, Sandbox, Ziel, Segment, Zusammenführungsrichtlinie, berechnetes Attribut, Produktprofil und Konto (Adobe) | Dies sind die Ressourcen, die von Prüfprotokollen aufgezeichnet werden. Wenn die Funktion aktiviert ist, werden die Prüfprotokolle automatisch erfasst, sobald eine Aktivität stattfindet. Sie müssen die Protokollerfassung nicht manuell aktivieren. |
| Audit-Protokolle exportieren | The audit logs can be downloaded as a `CSV` or `JSON` file. Die erzeugten Dateien werden direkt auf Ihrem Computer gespeichert. |

{style=&quot;table-layout:auto&quot;}

For more information on audit logs in Platform, refer to the [audit logs overview](../../landing/governance-privacy-security/audit-logs/overview.md).

## Verwandte Konten in Real-Time CDP B2B Edition {#related-accounts}

>[!NOTE]
>
>Die Funktion &quot;Ähnliche Konten&quot;ist nur für Kunden der Real-Time CDP B2B Edition verfügbar.

B2B-Unternehmen haben häufig ihre Kundeninformationen in mehreren Systemen gespeichert, von denen jede nur teilweise oder sogar widersprüchliche Daten für dieselbe reale Geschäftseinheit enthält. This creates a massive challenge of arriving at an accurate view of their customers, therefore reducing the efficiency and effectiveness of their B2B marketing and sales efforts. Mit der Freigabe der entsprechenden Konten [!DNL Real-time CDP B2B] zeigt Ihnen jetzt eine Liste von Konten an, die dem Konto, das Sie durchsuchen, ähnlich sind. You can include the related accounts in your segment definitions to broaden your reach or apply wider criteria in your segments.

Weitere Informationen zur Funktion finden Sie auf den folgenden Dokumentationsseiten:

- [Übersicht über verwandte Konten in Real-Time CDP B2B Edition](../../rtcdp/b2b-ai-ml-services/related-accounts.md)
- [Registerkarte &quot;Zugehörige Konten&quot;im UI-Handbuch für Kontoprofile](../../rtcdp/accounts/account-profile-ui-guide.md#related-accounts-tab)
- [How to use related accounts in segment definitions](../../rtcdp/segmentation/b2b.md#related-accounts)

Weitere Informationen zur Echtzeit-Kundendatenplattform B2B Edition finden Sie in der [Übersicht](../../rtcdp/overview.md).

## Warnhinweise {#alerts}

Mit Experience Platform können Sie ereignisbasierte Warnhinweise zu Adobe Experience Platform-Aktivitäten abonnieren. Sie können unterschiedliche Warnhinweisregeln über die Registerkarte [!UICONTROL Warnhinweise] in der Platform-Benutzeroberfläche abonnieren. Zusätzlch können Sie auswählen, ob Warnhinweise in der Benutzeroberfläche oder über E-Mail-Benachrichtigungen angezeigt werden sollen.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Warnhinweisregeln | Für Quellen, die mit der Datenerfassung in Verbindung stehen, stehen nun zwei neue Warnhinweisregeln zur Verfügung. Die aktualisierte Liste der Warnhinweistypen finden Sie in der Übersicht zu [Warnhinweisregeln](../../observability/alerts/rules.md). |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Warnhinweisen in Platform finden Sie im Abschnitt [Warnhinweise – Übersicht](../../observability/alerts/overview.md).

## Dashboards {#dashboards}

Adobe Experience Platform provides multiple [!DNL dashboards] through which you can view important information about your organization’s data, as captured during daily snapshots.

### Profile Dashboards

Im Dashboard &quot;Profile&quot;wird eine Momentaufnahme der Attributdaten (Datensatzdaten) angezeigt, die Ihr Unternehmen im Profilspeicher in der Experience Platform hat.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Widget &quot;Nicht segmentierte Profile&quot; | Das Widget stellt die Gesamtanzahl aller Profile bereit, die an kein Segment angehängt sind. Die generierte Zahl ist ab der letzten Momentaufnahme korrekt und stellt die Möglichkeit zur Profilaktivierung in Ihrer gesamten Organisation dar. Siehe [Dokumentation zu Standard-Widgets für Profile](../../dashboards/guides/profiles.md#standard-widgets) für weitere Informationen. |
| Trend-Widget &quot;Nicht segmentierte Profile&quot; | Dieses Widget bietet eine grafische Darstellung der Anzahl der Profile, die in einem bestimmten Zeitraum nicht an ein Segment angehängt sind. Der Trend kann über einen Zeitraum von 30 Tagen, 90 Tagen und 12 Monaten visualisiert werden. See the [profiles standard widgets documentation](../../dashboards/guides/profiles.md#standard-widgets) for more information. |
| Unsegmented Profiles by Identity widget | Dieses Widget kategorisiert die Gesamtzahl der nicht segmentierten Profile anhand ihrer eindeutigen Kennung. Die Daten werden in einem Balkendiagramm visualisiert. Siehe [Dokumentation zu Standard-Widgets für Profile](../../dashboards/guides/profiles.md#standard-widgets) für weitere Informationen. |
| Single identity profiles widget | Dieses Widget gibt einen Überblick über die Profile Ihrer Organisation, die nur über einen ID-Typ verfügen, der ihre Identität erstellt, entweder eine E-Mail oder eine ECID. See the [profiles standard widgets documentation](../../dashboards/guides/profiles.md#standard-widgets) for more information. |

{style=&quot;table-layout:auto&quot;}

Weiterführende Informationen zu Profil-Dashboards finden Sie im Abschnitt [Profil-Dashboards - Übersicht](../../dashboards/guides/profiles.md).

### Ziele-Dashboards

Das Dashboard Ziele zeigt eine Momentaufnahme der Ziele an, die Ihr Unternehmen in Experience Platform aktiviert hat.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Destinations count widget | The widget provides the total number of available endpoints where an audience can be activated and delivered within the system. This number includes both active and inactive destinations. Siehe [Dokumentation zum Standard-Widget für Ziele](../../dashboards/guides/destinations.md#standard-widgets) für weitere Informationen. |

{style=&quot;table-layout:auto&quot;}

Weiterführende Informationen zu Ziel-Dashboards in Platform finden Sie im Abschnitt [Ziele-Dashboards - Übersicht](../../dashboards/guides/destinations.md).

<!-- ## Experience Data Model (XDM) {#xdm}

Experience Data Model (XDM) is an open-source specification that provides common structures and definitions (schemas) for data that is brought into Adobe Experience Platform. By adhering to XDM standards, all customer experience data can be incorporated into a common representation to deliver insights in a faster, more integrated way. You can gain valuable insights from customer actions, define customer audiences through segments, and use customer attributes for personalization purposes.

| Feature | Description |
| --- | --- |
| Add or remove individual standard fields for a schema | The Schema Editor UI now allows you to add portions of standard field groups to your schemas, providing more flexibility for the fields you choose to include without needing to build custom resources from scratch.<br><br>You can now also define ad-hoc custom fields directly within the schema structure and assign them to a new or existing custom field group without needing to create or edit the field group beforehand.<br><br>See the guide on [creating and editing schemas in the UI](../../xdm/ui/resources/schemas.md) for more information on these new workflows. |

{style="table-layout:auto"}

For more information on XDM in Platform, see the [XDM System overview](../../xdm/home.md). -->

## Abfrage-Service {#query-service}

[!DNL Query Service] ermöglicht Ihnen die Verwendung von Standard-SQL zur Abfrage von Daten in Adobe Experience Platform [!DNL Data Lake]. Sie können beliebige Datensätze aus dem [!DNL Data Lake] verbinden und die Abfrageergebnisse als neuen Datensatz für die Verwendung in Berichten, im Data Science Workspace oder für die Aufnahme in das Echtzeit-Kundenprofil verwenden.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| `table_exists` | Mit dem Befehl &quot;Neue Funktion&quot;wird bestätigt, ob im System derzeit eine Tabelle vorhanden ist. Der Befehl gibt einen booleschen Wert zurück: `true` , wenn die Tabelle **does** vorhanden und `false` , wenn die Tabelle **not** existieren. Siehe [SQL-Syntaxdokumentation](../../query-service/sql/syntax.md) für weitere Informationen. |

{style=&quot;table-layout:auto&quot;}

For more information on available features, refer to the [Query Service overview](../../query-service/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Speichersystemen und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und die Datenerfassung überall verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Quellen für die B2B-Nutzung verfügbar | You can now use all the available sources on Platform for B2B use cases. See the [sources catalog](../../sources/home.md) for a complete list of available sources. |
| Allgemeine Verfügbarkeit neuer [!DNL Oracle Eloqua] source | Sie können jetzt die [!DNL Oracle Eloqua] -Quelle, um Daten aus Ihrem [!DNL Oracle Eloqua] -Instanz (Konto, Kampagne, Kontakte) zu Platform. Weitere Informationen finden Sie in der Dokumentation unter [Erstellen einer [!DNL Oracle Eloqua] Quellverbindung](../../sources/connectors/marketing-automation/oracle-eloqua.md) für weitere Informationen. |
| API-Verbesserungen für [!DNL Data Landing Zone] | Die [!DNL Data Landing Zone] -Quelle unterstützt jetzt die automatische Erkennung von Dateieigenschaften bei Verwendung der [!DNL Flow Service] API. Weitere Informationen finden Sie in der Dokumentation unter [Erstellen einer [!DNL Data Landing Zone] Quellverbindung](../../sources/tutorials/api/create/cloud-storage/data-landing-zone.md) für weitere Informationen. |

{style=&quot;table-layout:auto&quot;}

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
