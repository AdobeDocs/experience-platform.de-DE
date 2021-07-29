---
title: IAB TCF 2.0-Unterstützung im Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie IAB TCF 2.0-Zustimmungsvoreinstellungen mithilfe des Adobe Experience Platform Web SDK unterstützen.
keywords: Einverständnis; setConsent; Profildatenfeldgruppe; Erlebnisereignis-Datenschutzfeldgruppe; Datenschutzfeldgruppe; IAB TCF 2.0; Echtzeit-Kundendatenplattform; Echtzeit-Kundendatenprofil
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# IAB TCF 2.0-Unterstützung im Adobe Experience Platform Web SDK

Das Adobe Experience Platform Web SDK unterstützt das Interactive Advertising Bureau Transparency &amp; Consent Framework, Version 2.0 (IAB TCF 2.0). In diesem Handbuch werden die Anforderungen für die Unterstützung von IAB TCF 2.0 über das Adobe Experience Platform Web SDK erläutert, das mit der Echtzeit-Kundendatenplattform, dem Audience Manager, Experience Events, Adobe Analytics und Experience Edge integriert wird.

Darüber hinaus stehen die folgenden Handbücher zur Verfügung, mit denen Sie lernen können, wie IAB TCF 2.0 mit und ohne Tags integriert wird.

- [Mit Tags](./with-launch.md)
- [Ohne Tags](./without-launch.md)

## Erste Schritte

Um das Web SDK mit IAB TCF 2.0 zu implementieren, benötigen Sie ein Verständnis des Experience-Datenmodells (XDM) und der Experience-Ereignisse. Bevor Sie beginnen, lesen Sie bitte das folgende Dokument:

- [Experience-Datenmodell (XDM) - Systemübersicht](../../../xdm/home.md): Standardisierung und Interoperabilität sind Schlüsselkonzepte von Adobe Experience Platform. [!DNL Experience Data Model (XDM)]ist eine von Adobe unterstützte Maßnahme, um Kundenerlebnisdaten zu standardisieren und Schemas für das Customer Experience Management zu definieren.

## Integration von Experience Platformen

Um Einwilligungsdaten mit dem SDK an Adobe Experience Platform zu senden, ist Folgendes erforderlich:

- Ein Datensatz, dessen Schema auf der [!DNL XDM Individual Profile]-Klasse basiert und TCF 2.0-Einverständnisfelder enthält, die für die Verwendung in [!DNL Real-time Customer Profile] aktiviert sind.
- Ein mit Platform und dem oben erwähnten profilaktivierten Datensatz eingerichteter Datastream.

Anweisungen zum Erstellen der erforderlichen Datensätze und Datastreams finden Sie im Handbuch zur [TCF 2.0-Kompatibilität](../../../landing/governance-privacy-security/consent/iab/overview.md).

## Audience Manager-Integration

Adobe Audience Manager (AAM) unterstützt das IAB TCF 2.0, mit dem Sie Datenschutzoptionen von Kunden bewerten, berücksichtigen und an nachgelagerte Partner weiterleiten können. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Um über das Adobe Experience Platform Web SDK mit Audience Manager zu integrieren, stellen Sie sicher, dass Sie einen Datastraam eingerichtet haben, um ihn an Adobe Audience Manager weiterzuleiten.

## Integration von Experience Events und Adobe Analytics

Während die Echtzeit-Kundendatenplattform und die Zielgruppen des Audience Managers die aktuellen Zustimmungseinstellungen eines Kunden verfolgen, können Erlebnisereignisse die Zustimmungseinstellungen eines Kunden speichern, die zum Zeitpunkt der Erfassung aktiv waren.

Um Einwilligungsinformationen zu Ereignissen zu erfassen, ist Folgendes erforderlich:

- Ein Datensatz, der auf der [!DNL XDM Experience Event]-Klasse mit der Feldergruppe [!DNL Experience Event] Datenschutzschema basiert.
- Ein mit dem obigen Datensatz [!DNL XDM Experience Event] eingerichteter Datenspeicher.

Weitere Informationen zum Konvertieren eines XDM-Erlebnisereignisses in einen Analytics-Treffer finden Sie in der [Analytics-Übersicht](../../data-collection/adobe-analytics/analytics-overview.md) -Dokumentation.

## Adobe Experience Platform Web SDK-Integration

In den folgenden Abschnitten werden die wichtigsten Integrationspunkte zwischen IAB TCF 2.0 und dem Adobe Experience Platform Web SDK beschrieben.

>[!NOTE]
>
>Selbst wenn die Echtzeit-Kundendatenplattform oder der Audience Manager nicht eingerichtet ist, können Sie IAB TCF 2.0 mit dem Web SDK integrieren. Die Zustimmungsvoreinstellungen können verwendet werden, um die Erfassung von Erlebnisereignissen zu steuern und ein Identitäts-Cookie zu setzen.

### Standardzustimmung

Die Standardzustimmung wird verwendet, wenn für einen Kunden noch keine Zustimmungsvoreinstellung gespeichert ist. Das bedeutet, dass die standardmäßigen Zustimmungsoptionen das Verhalten des Adobe Experience Platform Web SDK steuern und sich je nach Region des Kunden ändern können.

Wenn Sie beispielsweise einen Kunden haben, der nicht in den Zuständigkeitsbereich der Datenschutz-Grundverordnung (DSGVO) fällt, kann die Standardzustimmung auf `in` gesetzt werden, aber innerhalb der Gerichtsbarkeit der DSGVO kann die Standardzustimmung auf `pending` gesetzt werden. Ihre Consent Management Platform (CMP) erkennt möglicherweise die Region des Kunden und stellt das Flag `gdprApplies` für IAB TCF 2.0 bereit. Mit diesem Flag können Sie die Standardzustimmung festlegen.

Weitere Informationen zur Standardzustimmung finden Sie im Abschnitt [Standardzustimmung](../../fundamentals/configuring-the-sdk.md#default-consent) in der SDK-Konfigurationsdokumentation.

### Festlegen der Zustimmung bei Änderungen

Das Adobe Experience Platform Web SDK verfügt über einen `setConsent`-Befehl, mit dem die Zustimmungsvoreinstellungen Ihres Kunden allen Adobe-Services mit IAB TCF 2.0 mitgeteilt werden. Wenn Sie mit der Echtzeit-Kundendatenplattform integriert sind, aktualisiert dies das Kundenprofil. Wenn Sie mit Audience Manager integrieren, werden dadurch die Kundeninformationen aktualisiert. Durch diesen Aufruf wird auch ein Cookie mit der Zustimmungsvoreinstellung &quot;alles oder nichts&quot;gesetzt, das steuert, ob zukünftige Erlebnisereignisse gesendet werden dürfen. Diese Aktion soll immer dann aufgerufen werden, wenn sich die Zustimmung ändert. Beim Laden künftiger Seiten wird das Experience Edge-Zustimmungscookie gelesen, um zu bestimmen, ob Erlebnisereignisse gesendet werden können und ob ein Identitäts-Cookie gesetzt werden kann.

Ähnlich wie bei der IAB TCF 2.0-Integration von Audience Manager erteilt Experience Edge eine Zustimmung, wenn ein Kunde seine ausdrückliche Zustimmung zu folgenden Zwecken erteilt hat:

- **Zweck 1:** Informationen auf einem Gerät speichern und/oder aufrufen
- **Zweck 10:** Entwicklung und Verbesserung von Produkten
- **Sonderzweck 1:** Gewährleistung von Sicherheit, Vermeidung von Betrug und Fehlerbehebung. (Gemäß den IAB-TCF-Vorschriften ist dies immer einverstanden.)
- **Berechtigung des Anbieters von Adoben:** Einverständnis für Adobe (Anbieter 565)

Weitere Informationen zum Befehl `setConsent` finden Sie in der Dokumentation zu [Unterstützende Zustimmung](../../consent/supporting-consent.md).

### Hinzufügen der Zustimmung zu Erlebnisereignissen

Das Adobe Experience Platform Web SDK verfügt über den Befehl `sendEvent` , mit dem ein Erlebnisereignis erfasst wird. Wenn Sie in Experience Events oder Adobe Analytics integrieren und die Zustimmungseinstellungen für jedes Erlebnisereignis wünschen, sollten Sie die Zustimmungsinformationen zu jedem `sendEvent`-Befehl hinzufügen.

Weitere Informationen zum Befehl `sendEvent` finden Sie in der Dokumentation zu [Tracking-Ereignissen](../../fundamentals/tracking-events.md).

## Nächste Schritte

Nachdem Sie jetzt ein grundlegendes Verständnis des IAB Transparency &amp; Consent Framework 2.0 haben, lesen Sie eines der Leitfäden zur Verwendung von IAB TCF 2.0 [mit Tags](./with-launch.md) oder [ohne Tags](./without-launch.md).
