---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
source-git-commit: 762a4b7336f1c26b79883db9484d8f5fc7bff53c
workflow-type: tm+mt
source-wordcount: '362'
ht-degree: 62%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 23. Februar 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Identity Service]](#identity)
- [Quellen](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] ermöglicht es Dateningenieuren, Daten mit dem Experience-Datenmodell (XDM) zu mappen sowie sie umzuformen und zu validieren.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| [!DNL Data Prep] Unterstützung für Adobe Analytics-Quell-Connector | Der Adobe Analytics-Quell-Connector unterstützt jetzt Data Prep-Funktionen, mit denen Sie Ihre Analytics Report Suite-Daten bei der Erstellung eines Datenflusses einem Ziel-XDM-Schema zuordnen können. Siehe Tutorial zu [Erstellen eines Quell-Connectors für Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) für weitere Informationen. |

Weitere Informationen zu [!DNL Data Prep] finden Sie in der [[!DNL Data Prep] Übersicht](../../data-prep/home.md).

## [!DNL Identity Service] {#identity}

Für die Bereitstellung relevanter digitaler Erlebnisse ist ein umfassendes Verständnis Ihres Kunden erforderlich. Dies wird erschwert, wenn Ihre Kundendaten über unterschiedliche Systeme hinweg fragmentiert sind, so dass jeder einzelne Kunde mehrere „Identitäten“ zu haben scheint.

Adobe Experience Platform [!DNL Identity Service] hilft Ihnen, einen besseren Überblick über Ihren Kunden und sein Verhalten zu erhalten, indem Identitäten über Geräte und Systeme hinweg überbrückt werden, sodass Sie in Echtzeit wirkungsvolle, persönliche digitale Erlebnisse bereitstellen können.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Berechtigung für `view-identity-graph` | Sie können jetzt die `view-identity-graph` Berechtigung zum Steuern, ob Benutzer in Ihrer Organisation Identitätsdiagrammdaten anzeigen können. Benutzer ohne diese Berechtigung haben keinen Zugriff auf den Identitätsdiagramm-Viewer in der Benutzeroberfläche oder beim Zugriff auf [!DNL Identity Service] APIs, die Identitäten zurückgeben. Siehe [Zugriffskontrolle - Übersicht](../../access-control/home.md) für weitere Informationen zu Berechtigungen. |

Weitere allgemeine Informationen zu [!DNL Identity Service] finden Sie unter [Identity Service – Übersicht](../../identity-service/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

| Funktion | Beschreibung |
| --- | --- |
| Wechsel von Betaquellen zu allgemeiner Verfügbarkeit | Die folgenden Quellen wurden von der Betaversion auf allgemeine Verfügbarkeit umgestellt: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
