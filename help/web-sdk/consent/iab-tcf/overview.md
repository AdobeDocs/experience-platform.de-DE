---
title: IAB TCF 2.0-Unterstützung im Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie IAB TCF 2.0-Zustimmungsvoreinstellungen mithilfe des Adobe Experience Platform Web SDK unterstützen.
keywords: consent; setConsent; Profildatenschutzfeldgruppe; Experience Event Privacy Field-Gruppe; Datenschutzfeldgruppe; IAB TCF 2.0; Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: b08c6cf12a38f79e019544dea91913a77bd6490a
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 0%

---

# IAB TCF 2.0-Unterstützung im Adobe Experience Platform Web SDK

Das Adobe Experience Platform Web SDK unterstützt das Interactive Advertising Bureau Transparency &amp; Consent Framework, Version 2.0 (IAB TCF 2.0). In diesem Handbuch werden die Anforderungen für die Unterstützung von IAB TCF 2.0 über das Adobe Experience Platform Web SDK erläutert, das mit Adobe Real-time Customer Data Platform, Audience Manager, Experience Events, Adobe Analytics und Edge Network integriert wird.

Darüber hinaus stehen die folgenden Handbücher zur Verfügung, mit denen Sie lernen können, wie IAB TCF 2.0 mit und ohne Tags integriert wird.

- [Mit Tags](./with-tags.md)
- [Ohne Tags](./without-tags.md)

## Erste Schritte

Um das Web SDK mit IAB TCF 2.0 zu implementieren, benötigen Sie ein Verständnis des Experience-Datenmodells (XDM) und der Experience-Ereignisse. Bevor Sie beginnen, lesen Sie bitte das folgende Dokument:

- [Übersicht über das Experience-Datenmodell (XDM)-System](../../../xdm/home.md): Standardisierung und Interoperabilität sind Schlüsselkonzepte von Adobe Experience Platform. [!DNL Experience Data Model (XDM)], unterstützt von Adobe, ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemas für das Customer Experience Management zu definieren.

## Experience Platform-Integration

Um Einwilligungsdaten mit dem SDK an Adobe Experience Platform zu senden, ist Folgendes erforderlich:

- Ein Datensatz, dessen Schema auf der Variablen [!DNL XDM Individual Profile] -Klasse und enthält TCF 2.0-Zustimmungsfelder, die für die Verwendung in aktiviert sind [!DNL Real-Time Customer Profile].
- Ein mit Platform und dem oben erwähnten profilaktivierten Datensatz eingerichteter Datastream.

Weitere Informationen finden Sie im Handbuch unter [Einhaltung von TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md) für Anweisungen zum Erstellen der erforderlichen Datensätze und Datastreams.

## Audience Manager-Integration

Adobe Audience Manager (AAM) unterstützt das IAB TCF 2.0, mit dem Sie Datenschutzoptionen von Kunden bewerten, berücksichtigen und an nachgelagerte Partner weiterleiten können. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Um über das Adobe Experience Platform Web SDK mit Audience Manager zu integrieren, stellen Sie sicher, dass Sie einen Datastraam eingerichtet haben, um ihn an Adobe Audience Manager weiterzuleiten.

## Integration von Experience Events und Adobe Analytics

Während die Zielgruppen von Real-Time CDP und Audience Manager die aktuellen Zustimmungsvoreinstellungen eines Kunden verfolgen, können Erlebnisereignisse die Zustimmungseinstellungen eines Kunden speichern, die zum Zeitpunkt der Erfassung des Ereignisses aktiv waren.

Um Einwilligungsinformationen zu Ereignissen zu erfassen, ist Folgendes erforderlich:

- Ein Datensatz, der auf der [!DNL XDM Experience Event] -Klasse, mit der [!DNL Experience Event] Datenschutzschema-Feldergruppe.
- Ein mit der Variablen [!DNL XDM Experience Event] Datensatz weiter oben.

Weitere Informationen zum Konvertieren eines XDM-Erlebnisereignisses in einen Analytics-Treffer finden Sie unter [Senden von Daten an Adobe Analytics mithilfe des Web SDK](/help/web-sdk/use-cases/adobe-analytics.md).

## Adobe Experience Platform Web SDK-Integration

In den folgenden Abschnitten werden die wichtigsten Integrationspunkte zwischen IAB TCF 2.0 und dem Adobe Experience Platform Web SDK beschrieben.

>[!NOTE]
>
>Selbst wenn Real-Time CDP oder Audience Manager nicht eingerichtet sind, können Sie IAB TCF 2.0 mit dem Web SDK integrieren. Die Zustimmungsvoreinstellungen können verwendet werden, um die Erfassung von Erlebnisereignissen zu steuern und ein Identitäts-Cookie zu setzen.

### Standardzustimmung

Die Standardzustimmung wird verwendet, wenn für einen Kunden noch keine Zustimmungsvoreinstellung gespeichert ist. Das bedeutet, dass die standardmäßigen Zustimmungsoptionen das Verhalten des Adobe Experience Platform Web SDK steuern und sich je nach Region des Kunden ändern können.

Wenn Sie beispielsweise einen Kunden haben, der nicht in den Zuständigkeitsbereich der Datenschutz-Grundverordnung (DSGVO) fällt, kann die Standardzustimmung auf `in`, aber innerhalb der Gerichtsbarkeit der DSGVO kann die standardmäßige Zustimmung auf `pending`. Ihre Consent Management Platform (CMP) erkennt möglicherweise die Region des Kunden und stellt die Kennzeichnung bereit `gdprApplies` nach IAB TCF 2.0. Mit diesem Flag können Sie die Standardzustimmung festlegen. Siehe [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) für weitere Informationen.

### Festlegen der Zustimmung bei Änderungen

Das Adobe Experience Platform Web SDK verfügt über eine `setConsent` -Befehl, der die Zustimmungsvoreinstellungen Ihres Kunden an alle Adobe-Dienste übermittelt, die IAB TCF 2.0 verwenden. Wenn Sie mit Real-Time CDP integrieren, wird dadurch das Kundenprofil aktualisiert. Wenn Sie mit Audience Manager integrieren, werden dadurch die Kundeninformationen aktualisiert. Durch diesen Aufruf wird auch ein Cookie mit der Zustimmungsvoreinstellung &quot;alles oder nichts&quot;gesetzt, das steuert, ob zukünftige Erlebnisereignisse gesendet werden dürfen. Diese Aktion soll immer dann aufgerufen werden, wenn sich die Zustimmung ändert. Beim Laden einer zukünftigen Edge Network-Seite wird das Cookie zur Zustimmung gelesen, um zu bestimmen, ob Erlebnisereignisse gesendet werden können und ob ein Identitäts-Cookie gesetzt werden kann.

Ähnlich wie bei der IAB TCF 2.0-Integration des Audience Managers erteilt das Edge Network eine Zustimmung, wenn ein Kunde seine ausdrückliche Zustimmung zu folgenden Zwecken erteilt hat:

- **Zweck 1:** Informationen auf einem Gerät speichern und/oder aufrufen
- **Zweck 10:** Produkte entwickeln und verbessern
- **Zweckbestimmung 1:** Sicherheit, Vermeidung von Betrug und Fehlerbehebung. (Gemäß den IAB-TCF-Vorschriften wird dies immer zugestimmt.)
- **Adobe Vendor-Berechtigung:** Zustimmung für Adobe (Hersteller 565)

Weitere Informationen über `setConsent` -Befehl, lesen Sie die dedizierte Web SDK-Dokumentation unter [setConsent](../../../web-sdk/commands/setconsent.md).

### Hinzufügen der Zustimmung zu Erlebnisereignissen

Das Adobe Experience Platform Web SDK verfügt über eine [`sendEvent`](/help/web-sdk/commands/sendevent/overview.md) -Befehl, der ein Erlebnisereignis erfasst. Wenn Sie in Experience Events oder Adobe Analytics integrieren und die Zustimmungsvoreinstellungen für jedes Erlebnisereignis nutzen möchten, fügen Sie jedem `sendEvent` Befehl.

## Nächste Schritte

Nachdem Sie jetzt über grundlegende Kenntnisse des IAB Transparency &amp; Consent Framework 2.0 verfügen, lesen Sie bitte eines der Handbücher zur Verwendung von IAB TCF 2.0. [mit Tags](./with-tags.md) oder [ohne Tags](./without-tags.md).
