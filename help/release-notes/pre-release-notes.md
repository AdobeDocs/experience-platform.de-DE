---
title: Hinweise zu Vorabversionen von Experience Platform
description: Eine Vorschau der neuesten Versionshinweise für Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: c716bac1db556fe7a47462e38ee64d7b46bbefcc
workflow-type: tm+mt
source-wordcount: '1299'
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
>- [Customer Journey Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/releases/pre-release-notes)
>- [Komposition föderierter Zielgruppen](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/e-release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Veröffentlichungsdatum: Donnerstag, 18. Juni 2025**

Neue Funktionen und Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Zugangssteuerung](#access-control)
- [Erweitertes Daten-Lifecycle-Management](#advanced-data-lifecycle-management)
- [Dashboards](#dashboards)
- [Data Governance](#data-governance)
- [Ziele](#destinations)
- [Komposition föderierter Zielgruppen](#fac)
- [Privacy Service](#privacy-service)
- [Sandboxes](#sandboxes)
- [Quellen](#sources)

## Zugriffskontrolle {#access-control}

Experience Platform nutzt [Adobe Admin Console](https://adminconsole.adobe.com)-Produktprofile, um Benutzer mit Berechtigungen und Sandboxes zu verknüpfen. Berechtigungen steuern den Zugriff auf eine Vielzahl von Experience Platform-Funktionen, einschließlich Datenmodellierung, Profilverwaltung und Sandbox-Administration.

**Wichtigste Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Berechtigung zum Exportieren von Dashboard-Daten | Die **[!UICONTROL CSV herunterladen]** und **[!UICONTROL Als E-Mail senden]** in Dashboards erfordern jetzt die Berechtigung **[!UICONTROL Dashboard-Daten exportieren]**. Diese Berechtigung stellt sicher, dass nur autorisierte Benutzende tabellarische insight-Daten exportieren können, was strengere Richtlinien für Governance und Datenzugriffssteuerung unterstützt. |

Weiterführende Informationen finden Sie unter [Zugriffskontrolle – Übersicht](../access-control/home.md).

## Erweitertes Daten-Lifecycle-Management {#advanced-data-lifecycle-management}

Experience Platform bietet eine Reihe von Datenhygiene-Funktionen, mit denen Sie Ihre gespeicherten Daten durch programmgesteuerte Löschungen von Verbraucherdatensätzen verwalten können. Mithilfe des Datenlebenszyklus-Arbeitsbereichs in der Benutzeroberfläche oder durch Aufrufe der Datenhygiene-API können Sie Ihre Datenspeicher effektiv verwalten. Verwenden Sie diese Funktionen, um sicherzustellen, dass Informationen erwartungsgemäß verwendet werden, aktualisiert werden, wenn falsche Daten korrigiert werden müssen, und gelöscht werden, wenn dies aufgrund von Unternehmensrichtlinien erforderlich ist.

**Neue Dokumentation**

| Neue Dokumentation | Beschreibung |
| --- | --- |
| Allgemeine Verfügbarkeit zum Löschen von Datensätzen | Sie können jetzt einzelne Datensätze basierend auf Identitätsfeldern mithilfe der Benutzeroberfläche oder API löschen. Mit dieser Funktion können Sie die Speicherung reduzieren, die Governance durchsetzen und die Datenhygiene verbessern, indem Sie Löschungen aus einem einzelnen Datensatz oder über alle Datensätze hinweg zulassen. Es gelten Volumenbeschränkungen und Berechtigungsanforderungen. |

Weitere Informationen finden Sie im Abschnitt [Übersicht über das erweiterte Daten-Lifecycle-Management](../hygiene/home.md).

## Dashboards {#dashboards}

Experience Platform bietet mehrere Dashboards, in denen Sie wichtige Einblicke in die Daten Ihres Unternehmens erhalten, die in täglichen Schnappschüssen erfasst werden.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| ------- | ----------- |
| Als E-Mail senden - Exportoption | Sie können jetzt bis zu 10.000 Datensätze aus Query Pro-Modus-Dashboards exportieren, indem Sie **[!UICONTROL Als E-Mail senden]** im Menü **[!UICONTROL Mehr anzeigen]** auswählen. Mit dieser Option wird ein Downloadlink für größere Exporte sicher an Ihre Adobe-E-Mail gesendet. |

Weitere Informationen zu Dashboards, einschließlich der Gewährung von Zugriffsberechtigungen und der Erstellung benutzerdefinierter Widgets, finden Sie in der [Übersicht über Dashboards](../dashboards/home.md).

## Data Governance {#data-governance}

Adobe Experience Platform Data Governance besteht aus einer Reihe von Strategien und Technologien zur Verwaltung von Kundendaten sowie zur Gewährleistung der Einhaltung von Vorschriften, Beschränkungen und Datennutzungsrichtlinien. Die Funktion spielt in [!DNL Experience Platform] auf verschiedenen Ebenen eine wichtige Rolle, wie z. B. bei Katalogisierung, Bestimmung der Datenherkunft, Datennutzungsbezeichnung, Datenzugriffsrichtlinien und Zugriffssteuerung für Daten bei Marketing-Aktionen.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Auf die Zulassungsliste setzen Azure CMK-Warnhinweise und IP-Adresskonfiguration | Auf die Zulassungsliste setzen Sie können jetzt die statische IP-Adresse von Adobe im Azure-Schlüsseltresor ändern, um den kontinuierlichen Zugriff bei aktivierten Netzwerkbeschränkungen sicherzustellen. Dadurch werden Unterbrechungen von Platform-Services aufgrund des eingeschränkten Schlüsselzugriffs verhindert. |
| CMK-Konfigurationswarnungen und -auflösungen | Experience Platform warnt jetzt Trigger auf die Zulassungsliste setzen, wenn Adobe-Services den Zugriff auf Ihren Azure-Schlüsseltresor verlieren (z. B. aufgrund entfernter IP-Schlüsseleinträge oder deaktivierter Schlüssel). Eine neue Anleitung hilft Ihnen, jeden Warnhinweis zu verstehen und Korrekturmaßnahmen zu ergreifen. |

Weitere Informationen finden Sie im Abschnitt [Übersicht über Data Governance](../data-governance/home.md).

## Ziele {#destinations}

[!DNL Destinations] sind vorkonfigurierte Integrationen mit Zielplattformen, die eine nahtlose Aktivierung von Daten aus Adobe Experience Platform ermöglichen. Mit Zielen können Sie Ihre bekannten und unbekannten Daten für kanalübergreifende Marketing-Kampagnen, E-Mail-Kampagnen, zielgruppengerechte Werbung und viele andere Anwendungsfälle aktivieren.

**Neue Ziele**

| Ziel | Beschreibung |
| --- | --- |
| Algolia-Benutzersegmente | Das Ziel Algolia-Benutzersegmente ermöglicht es Marketing-Experten, eine konsistente Personalisierung für alle Sites von der Startseite bis zur Suche bereitzustellen. Erstellen Sie vielfältige Audiences aus verschiedenen Datenquellen und teilen Sie sie über verschiedene Kanäle hinweg, um verbesserte Targeting-Strategien und die Kampagnen-Personalisierung zu erzielen. |

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| LinkedIn-Kontoablaufinformationen | Informationen zum Ablauf von Konten für LinkedIn-Ziele sind jetzt direkt in den Ansichten [!UICONTROL Durchsuchen] und [!UICONTROL Konten] verfügbar. Zuvor waren diese Informationen nur in der Dokumentation verfügbar. Diese Verbesserung bietet eine bessere Sichtbarkeit des LinkedIn-Authentifizierungsstatus und der Verwaltung von Berechtigungen. |
| Google Customer Match + DV360 - allgemeine Verfügbarkeit und Erweiterung | Das Ziel Google Customer Match + DV360 ist jetzt für alle Experience Platform-Benutzerinnen und -Benutzer verfügbar. Die Dokumentation enthält jetzt eine detaillierte Anleitung für die Kontoverknüpfung zwischen Adobe- und Google-Werbekonten. |
| Unterstützung der Data Landing Zone (DLZ)-Zielverschlüsselung | Es wurde Verschlüsselungsunterstützung für das Data Landing Zone-Ziel hinzugefügt. Sie können jetzt RSA-formatierte öffentliche Schlüssel anhängen, um Ihren exportierten Dateien eine Verschlüsselung hinzuzufügen. |
| Überwachung auf Zielgruppenebene für Unternehmensziele | Die Überwachung auf Zielgruppenebene ist jetzt für die folgenden Unternehmensziele verfügbar: [[!DNL Azure Event Hubs]](/help/destinations/catalog/cloud-storage/azure-event-hubs.md), [[!DNL HTTP API]](/help/destinations/catalog/streaming/http-destination.md), [[!DNL Amazon Kinesis]](/help/destinations/catalog/cloud-storage/amazon-kinesis.md). |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Ziele - Übersicht](../destinations/home.md).

## Komposition föderierter Zielgruppen {#fac}

Die föderierte Zielgruppenkomposition ermöglicht es Unternehmen, Daten für eine bessere Anwendung in verschiedenen Anwendungsfällen zu erstellen. Mit diesem neuen Ansatz können Sie als Adobe Real-Time Customer Data Platform- und/oder Adobe Journey Optimizer-Anwender Datensätze direkt aus Ihrem bestehenden Data Warehouse zusammenführen, um Adobe Experience Platform-Zielgruppen und -Attribute in einem System zu erstellen und anzureichern.

| Neue Funktion | Beschreibung |
| ----------- | ----------- |
| HIPAA-Bereitschaft | Die Federated Audience-Komposition ist jetzt HIPAA-kompatibel. Weitere Informationen zu den Datenschutz- und Sicherheitsmaßnahmen der Federated Audience Composition finden Sie unter [Datenschutz und Sicherheit in der Übersicht über die Federated Audience ](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/start/privacy-security). Weitere Informationen zur HIPAA-Konformität für Experience Platform-Produkte im Allgemeinen finden Sie in der [Übersicht über HIPAA und Adobe-Produkte und -Services](https://www.adobe.com/trust/compliance/hipaa-ready.html). |

Weitere Informationen finden Sie in der [Dokumentation zur Federated Audience-Komposition](https://experienceleague.adobe.com/de/docs/federated-audience-composition/using/home).

## [!DNL Privacy Service] {#privacy}

Verschiedene gesetzliche und organisatorische Vorschriften geben Benutzern das Recht, auf Anfrage auf ihre personenbezogenen Daten zuzugreifen oder sie aus Ihren Datenspeichern zu löschen. Adobe Experience Platform [!DNL Privacy Service] bietet eine RESTful-API und eine Benutzeroberfläche, die Sie bei der Verwaltung dieser Datenanfragen Ihrer Kunden unterstützen. Mit [!DNL Privacy Service] können Sie Anfragen für den Zugriff auf und die Löschung von personenbezogenen oder privaten Kundendaten aus Adobe Experience Cloud-Programmen stellen, was die automatische Einhaltung gesetzlicher und unternehmensinterner Datenschutzbestimmungen erleichtert.

**Neue Funktionen**

| Funktion | Beschreibung |
|--- | ---|
| Unterstützung der Datenschutzgesetze von Tennessee und Minnesota | Privacy Service unterstützt jetzt den Tennessee Information Protection Act (`tipa_tn_usa`) und den Minnesota Consumer Data Privacy Act (`mcdpa_mn_usa`). Sie können Zugriffs- und Löschanfragen in Übereinstimmung mit diesen neuen Vorschriften auf Statusebene verarbeiten. Weitere Einzelheiten finden Sie [ &quot;](https://experienceleague.adobe.com/en/docs/experience-platform/privacy/regulations/overview)&quot;. |

Weitere Informationen zu dem Service finden Sie in [&#128279;](../privacy-service/home.md) Übersicht über Privacy Service .

## Sandboxes {#sandboxes}

Adobe Experience Platform dient dazu, Programme für digitale Erlebnisse auf globaler Ebene anzureichern. Oft führen Unternehmen verschiedene Programme für digitale Erlebnisse parallel aus und müssen diese Programme entwickeln, testen und bereitstellen, während gleichzeitig die Einhaltung betrieblicher Vorschriften gewährleistet werden muss.

**Neue oder aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Migration von Objektkonfigurationsaktualisierungen | Sie können jetzt nach der ersten Replikation iterative Objektkonfigurationsaktualisierungen über Sandboxes hinweg migrieren. Diese Verbesserung unterstützt Entwicklungs-Workflows, in denen Konfigurationen aktualisiert und über Umgebungen hinweg propagiert werden müssen, ohne die gesamte Sandbox-Einrichtung neu zu erstellen. |

{style="table-layout:auto"}

Weitere Informationen zu Sandboxes finden Sie unter [Sandbox-Übersicht](../sandboxes/home.md).

## Quellen {#sources}

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Unterstützung für neuen Authentifizierungstyp für [!DNL Azure Synapse Analytics] | Die [!DNL Azure Synapse Analytics] unterstützt jetzt zusätzlich zur vorhandenen Authentifizierung über die Verbindungszeichenfolge auch die Authentifizierung für Service-Prinzipale. |

**Wichtige Authentifizierungsaktualisierungen**

| Update | Beschreibung |
| --- | --- |
| [!DNL Salesforce] Standard-Authentifizierungs-Einstellung | Die Standardauthentifizierung für Salesforce CRM und Salesforce Service Cloud wird ab Januar 2026 eingestellt. Kunden müssen zur OAuth 2.0-Authentifizierung migrieren, um die Konnektivität aufrechtzuerhalten. Diese Änderung wirkt sich auf beide Quell-Connectoren aus und sorgt für eine verbesserte Sicherheit und die Einhaltung der Authentifizierungsstandards von Salesforce. |

{style="table-layout:auto"}

Weitere Informationen finden Sie unter [Quelle – Übersicht](../sources/home.md).
