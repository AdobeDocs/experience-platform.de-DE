---
title: IAB TCF 2.0-Unterstützung im Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie mithilfe des Adobe Experience Platform Web SDK die IAB TCF 2.0-Genehmigungsvoreinstellungen unterstützen.
keywords: approval;setConsent;Profil Privacy Field group;Experience Ereignis Privacy Field group;Privacy Field group;IAB TCF 2.0;Real-time CDP;Real-time Customer Data Profil
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
translation-type: tm+mt
source-git-commit: 7d7502b238f96eda1a15b622ba10bbccc289b725
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 0%

---

# IAB TCF 2.0-Unterstützung im Adobe Experience Platform Web SDK

Das Adobe Experience Platform Web SDK unterstützt das Interactive Advertising Bureau Transparency &amp; Consent Framework, Version 2.0 (IAB TCF 2.0). In diesem Handbuch werden die Anforderungen für die Unterstützung von IAB TCF 2.0 durch Adobe Experience Platform Web SDK erläutert, die in die Echtzeit-Kundendatenplattform, Audience Manager, Experience Ereignisses, Adobe Analytics und Experience Edge integriert werden.

Darüber hinaus stehen die folgenden Handbücher zur Verfügung, um zu lernen, wie man IAB TCF 2.0 mit und ohne Adobe Experience Platform Launch integriert.

- [Mit Adobe Experience Platform Launch](./with-launch.md)
- [Ohne Adobe Experience Platform Launch](./without-launch.md)

## Erste Schritte

Um das Web SDK mit IAB TCF 2.0 zu implementieren, benötigen Sie ein funktionierendes Verständnis der Experience Data Model (XDM)- und Experience Ereignis. Bevor Sie den Beginn ausführen, lesen Sie bitte das folgende Dokument:

- [Systemübersicht](../../../xdm/home.md) zum Erlebnis-Datenmodell (XDM): Normung und Interoperabilität sind Schlüsselkonzepte für Adobe Experience Platform. [!DNL Experience Data Model (XDM)]auf der Grundlage der Adobe eine Standardisierung der Kundenerlebnisdaten und die Definition von Schemas für das Kundenerlebnis-Management.

## Integration von Experience Platformen

Zum Senden von Genehmigungsdaten mit dem SDK an Adobe Experience Platform ist Folgendes erforderlich:

- Ein Datensatz, dessen Schema auf der [!DNL XDM Individual Profile]-Klasse basiert und die Eingabefelder TCF 2.0 für die Zustimmung enthält, die für [!DNL Real-time Customer Profile] aktiviert sind.
- Eine Edge-Konfiguration, die mit Platform und dem oben erwähnten Profil-aktivierten Datensatz eingerichtet wurde.

Anweisungen zum Erstellen der erforderlichen Datensätze und zur Edge-Konfiguration finden Sie im Handbuch [TCF 2.0 compliance](../../../landing/governance-privacy-security/consent/iab/overview.md).

## Integration von Audience Managern

Adobe Audience Manager (AAM) unterstützt die IAB TCF 2.0, mit der Sie Entscheidungen zum Schutz der Privatsphäre von Kunden bewerten, berücksichtigen und an nachgeschaltete Partner weiterleiten können. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Um über das Adobe Experience Platform Web SDK mit Audience Manager zu integrieren, müssen Sie eine Edge-Konfiguration für die Weiterleitung an Adobe Audience Manager eingerichtet haben.

## Experience Ereignisses- und Adobe Analytics-Integration

Während die Echtzeit-CDP und die Audiencen des Audience Managers die aktuellen Voreinstellungen für die Zustimmung des Kunden verfolgen, kann Experience Ereignisses die Präferenzen des Kunden für die Zustimmung speichern, die zum Zeitpunkt der Erfassung des Ereignisses aktiv waren.

Zur Erhebung von Informationen über die Zustimmung zu Ereignissen ist Folgendes erforderlich:

- Ein Datensatz, der auf der [!DNL XDM Experience Event]-Klasse mit der [!DNL Experience Event]-Schema-Feldgruppe zum Schutz der Privatsphäre basiert.
- Eine Edge-Konfiguration, die mit dem Dataset [!DNL XDM Experience Event] oben eingerichtet wurde.

Weitere Informationen zum Konvertieren eines XDM Experience Ereignisses in einen Analytics-Treffer finden Sie im Beginn [Analytics overview](../../data-collection/adobe-analytics/analytics-overview.md).

## Adobe Experience Platform Web SDK-Integration

Die folgenden Abschnitte beschreiben die wichtigsten Integrationspunkte zwischen IAB TCF 2.0 und Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Auch ohne Echtzeit-CDP oder Audience Manager-Einrichtung können Sie IAB TCF 2.0 mit dem Web SDK integrieren. Mit den Voreinstellungen für die Zustimmung können Sie die Erfassung von Experience Ereignisses steuern und ein Identitäts-Cookie einrichten.

### Standardgenehmigung

Die Standardgenehmigung wird verwendet, wenn für einen Kunden noch keine Einwilligung gespeichert wurde. Das bedeutet, dass die standardmäßigen Zustimmungsoptionen das Verhalten des Adobe Experience Platform Web SDK steuern und je nach Region des Kunden ändern können.

Wenn Sie z. B. einen Kunden haben, der nicht unter die Gerichtsbarkeit der Allgemeinen Datenschutzverordnung (GDPR) fällt, könnte die Standardgenehmigung auf `in` eingestellt werden, aber innerhalb der Gerichtsbarkeit von GDPR könnte die Standardgenehmigung auf `pending` eingestellt werden. Ihre Consent Management Platform (CMP) könnte die Region des Kunden erkennen und die Kennzeichnung `gdprApplies` für IAB TCF 2.0 bereitstellen. Mit diesem Flag können Sie die Standardgenehmigung festlegen.

Weitere Informationen zur Standardgenehmigung finden Sie im Abschnitt [Standardgenehmigung](../../fundamentals/configuring-the-sdk.md#default-consent) in der SDK-Konfigurationsdokumentation.

### Einwilligung beim Ändern

Adobe Experience Platform Web SDK verfügt über einen Befehl `setConsent`, mit dem die Voreinstellungen für die Zustimmung Ihres Kunden an alle Adoben mit IAB TCF 2.0 weitergeleitet werden. Wenn Sie eine Integration mit CDP in Echtzeit durchführen, wird dadurch das Profil Ihres Kunden aktualisiert. Wenn Sie in Audience Manager integriert sind, werden die Kundeninformationen aktualisiert. Durch Aufruf dieser Funktion wird auch ein Cookie mit einer &quot;Alles-oder-nichts-Zustimmungsvoreinstellung&quot;gesetzt, das steuert, ob zukünftige Experience Ereignisses gesendet werden dürfen. Diese Aktion soll bei jeder Änderung der Zustimmung aufgerufen werden. Beim Laden zukünftiger Seiten wird das Experience Edge-Cookie für die Zustimmung gelesen, um zu ermitteln, ob Experience Ereignisses gesendet werden kann und ob ein Identitäts-Cookie gesetzt werden kann.

Ähnlich wie bei der IAB TCF 2.0-Integration des Audience Managers gibt Experience Edge seine Zustimmung, wenn ein Kunde seine ausdrückliche Zustimmung zu folgenden Zwecken erteilt hat:

- **Zweck 1:** Speichern und/oder Zugreifen auf ein Gerät
- **Zweck 10:** Entwicklung und Verbesserung von Produkten
- **Sonderzweck 1:** Sicherstellen der Sicherheit, Verhinderung von Betrug und Debuggen. (Gemäß den IAB-TCF-Vorschriften ist dies immer einverstanden)
- **Adobe Vendor Permission:** Consent for Adobe (Hersteller 565)

Weitere Informationen zum Befehl `setConsent` finden Sie in der Dokumentation zu [Unterstützende Zustimmung](../../consent/supporting-consent.md).

### Hinzufügen der Zustimmung zu Experience Ereignisses

Adobe Experience Platform Web SDK verfügt über den Befehl `sendEvent`, mit dem ein Experience Ereignis erfasst wird. Wenn Sie in Experience Ereignisses oder Adobe Analytics integriert sind und die Voreinstellungen für die Zustimmung bei jedem Experience Ereignis einholen möchten, sollten Sie die Informationen zur Einwilligung jedem `sendEvent`-Befehl hinzufügen.

Weitere Informationen zum Befehl `sendEvent` finden Sie in der Dokumentation zu [Tracking-Ereignissen](../../fundamentals/tracking-events.md).

## Nächste Schritte

Nachdem Sie sich mit dem IAB-Transparenz- und -Zustimmung-Framework 2.0 vertraut gemacht haben, lesen Sie bitte eines der Leitfäden zur Verwendung von IAB TCF 2.0 [mit Adobe Experience Platform Launch](./with-launch.md) oder [ohne Adobe Experience Platform Launch](./without-launch.md).
