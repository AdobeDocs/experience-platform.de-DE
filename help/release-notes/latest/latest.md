---
title: Adobe Experience Platform – Versionshinweise
description: Die neuesten Versionshinweise für Adobe Experience Platform.
source-git-commit: 6d360721a598ff3fa82169aea608263a09c1f05f
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 41%

---

# Adobe Experience Platform – Versionshinweise

**Versionsdatum: 23. Februar 2022**

Aktualisierungen vorhandener Funktionen in Adobe Experience Platform:

- [Datenerfassung](#data-collection)
- [[!DNL Data Prep]](#data-prep)
- [[!DNL Identity Service]](#identity)
- [Quellen](#sources)

## Datenerfassung {#data-collection}

Platform bietet eine Reihe von Technologien, mit denen Sie clientseitige Kundenerlebnisdaten erfassen und an das Adobe Experience Platform Edge Network senden können, wo sie angereichert, transformiert und an Ziele außerhalb der Adobe oder der Adobe verteilt werden können.

**Neue Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Verbesserter UI-Workflow für die Konfiguration von Datastreams | Der Arbeitsablauf zum Erstellen eines neuen Datastreams in der Datenerfassungs-Benutzeroberfläche wurde aktualisiert. Beim Hinzufügen von Diensten zu einem Datastream werden nur die Dienste, auf die Sie Zugriff haben, in die Optionsliste aufgenommen. Siehe Handbuch unter [Konfigurieren eines Datenspeichers](../../edge/fundamentals/datastreams.md) für weitere Informationen. |
| Datenvorbereitung für die Datenerfassung | Wenn Sie das Adobe Experience Platform Web SDK verwenden, können Sie jetzt Datenvorlagenfunktionen nutzen, um Ihre Daten serverseitig dem Experience-Datenmodell (XDM) zuzuordnen. Siehe Abschnitt zu [Datenvorbereitung für die Datenerfassung](../../edge/fundamentals/datastreams.md#data-prep) Weitere Informationen finden Sie im Datenspeicher-Handbuch. |
| Erstanbieter-Geräte-IDs | Sie können jetzt Ihre eigenen Geräte-IDs beim Erfassen von Kundendaten mit dem Platform Web SDK an das Adobe Experience Platform Edge Network senden, um eine Problemumgehung für aktuelle Browserbeschränkungen bei Cookie-Lebenszyklen von Drittanbietern zu bieten. Siehe Handbuch unter [Erstanbieter-Geräte-IDs](../../edge/identity/first-party-device-ids.md) für weitere Informationen. |

Weitere Informationen zur Datenerfassung in Platform finden Sie im [Datenerfassung - Übersicht](../../collection/home.md).

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

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Neue Berechtigung für `view-identity-graph` | Sie können jetzt die `view-identity-graph` Berechtigung zum Steuern, ob Benutzer in Ihrer Organisation Identitätsdiagrammdaten anzeigen können. Benutzer ohne diese Berechtigung haben keinen Zugriff auf den Identitätsdiagramm-Viewer in der Benutzeroberfläche oder beim Zugriff auf [!DNL Identity Service] APIs, die Identitäten zurückgeben. Siehe [Zugriffskontrolle - Übersicht](../../access-control/home.md) für weitere Informationen zu Berechtigungen. |

Weitere allgemeine Informationen zu [!DNL Identity Service] finden Sie unter [Identity Service – Übersicht](../../identity-service/home.md).

## Quellen {#sources}

Mit Adobe Experience Platform können Sie Daten aus externen Quellen erfassen und diese Daten mithilfe von Platform-Diensten strukturieren, kennzeichnen und verbessern. Daten können Sie aus verschiedenen Quellen erfassen, z. B. aus Adobe-Anwendungen, Cloud-basiertem Speicher, Software von Drittanbietern und Ihrem CRM-System.

Im Rahmen von Experience Platform stehen eine RESTful-API und interaktive Benutzeroberfläche zur Verfügung, mit deren Hilfe Sie auf unkomplizierte Weise Verbindungen zu Datenquellen verschiedener Anbieter einrichten können. Mit diesen Quellverbindungen können Sie sich authentifizieren und eine Verbindung zu externen Datenspeichern und CRM-Diensten herstellen, Zeiten für Erfassungsläufe festlegen und den Durchsatz der Datenerfassung verwalten.

**Aktualisierte Funktionen**

| Funktion | Beschreibung |
| --- | --- |
| Wechsel von Betaquellen zu allgemeiner Verfügbarkeit | Die folgenden Quellen wurden von der Betaversion auf allgemeine Verfügbarkeit umgestellt: <ul><li>[[!DNL Mailchimp Campaigns]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Mailchimp Members]](../../sources/connectors/marketing-automation/mailchimp.md)</li><li>[[!DNL Zoho CRM]](../../sources/connectors/crm/zoho.md)</li></ul> |

Weitere Informationen zu Quellen finden Sie in der [Quellen – Übersicht](../../sources/home.md).
