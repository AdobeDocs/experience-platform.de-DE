---
title: Übersicht über das IAB-Transparenz- und -Consent-Framework 2.0
seo-title: Unterstützende Adobe Experience Platform Web SDK-Genehmigungsvoreinstellungen des Interactive Advertising Bureau Transparency & Consent Framework 2.0
description: Erfahren Sie, wie Sie die IAB TCF 2.0-Voreinstellungen für die Zustimmung mit Experience Platform Web SDK unterstützen.
seo-description: Erfahren Sie, wie Sie die IAB TCF 2.0-Voreinstellungen für die Zustimmung mit Experience Platform Web SDK unterstützen.
keywords: consent;setConsent;Profile Privacy Mixin;Experience Event Privacy Mixin;Privacy Mixin;IAB TCF 2.0;Real-time CDP;Real-time Customer Data Profile
translation-type: tm+mt
source-git-commit: 48cebe994b450b0dac5e6f256ab81827a7e8a0d5
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---


# Übersicht über das IAB-Transparenz- und -Consent-Framework 2.0

Das Adobe Experience Platform Web SDK (AEP Web SDK) unterstützt das Interactive Advertising Bureau Transparency &amp; Consent Framework, Version 2.0 (IAB TCF 2.0). In diesem Handbuch werden die Anforderungen für die Unterstützung von IAB TCF 2.0 über das AEP Web SDK erläutert, das in die Echtzeit-Kundendatenplattform, den Audience Manager, Experience Ereignisses, Analytics und Experience Edge integriert ist.

Darüber hinaus stehen die folgenden Handbücher zur Verfügung, um zu lernen, wie man IAB TCF 2.0 mit und ohne Adobe Experience Platform Launch integriert.

- [Mit Adobe Experience Platform Launch](./with-launch.md)
- [Ohne Adobe Experience Platform Launch](./without-launch.md)

## Erste Schritte

Um das AEP Web SDK mit IAB TCF 2.0 zu implementieren, müssen Sie über ein funktionierendes Verständnis des Experience Data Model (XDM) und Experience Ereignisses verfügen. Bevor Sie den Beginn ausführen, lesen Sie bitte das folgende Dokument:

- [Systemübersicht](../../../xdm/home.md)zum Erlebnis-Datenmodell (XDM): Normung und Interoperabilität sind Schlüsselkonzepte für Adobe Experience Platform. [!DNL Experience Data Model] (XDM), angetrieben von der Adobe, ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schema für das Kundenerlebnis-Management zu definieren.

## Integration der Kundendatenplattform in Echtzeit

Die auf Adobe Experience Platform aufbauende Adobe Echtzeit-Kundendatenplattform (Echtzeit-CDP) hilft Ihnen, bekannte und anonyme Daten aus mehreren Unternehmensquellen zusammenzuführen. Auf diese Weise können Sie Kundendaten erstellen, die dazu verwendet werden können, personalisierte Kundenerlebnisse auf allen Kanälen und Geräten in Echtzeit bereitzustellen. Zum Senden von Genehmigungsdaten an Echtzeit-CDP über das AEP Web SDK ist Folgendes erforderlich:

- Ein auf der [!DNL XDM Individual Profile] Klasse basierender Datensatz, der für die Verwendung in aktiviert ist, [!DNL Real-time Customer Profile]mit dem Profil Privacy mixin.
- Eine Edge-Konfiguration mit Echtzeit-CDP und dem oben erwähnten Profil-Datensatz.

Informationen zum Erstellen des erforderlichen Datensatzes finden Sie im Lernprogramm zum [Erstellen von Datensätzen zur Erfassung der TCF 2.0-Zustimmung](../../../rtcdp/privacy/iab/dataset-preparation.md) .

Anweisungen zum Erstellen der Edge-Konfiguration finden Sie in der [IAB TCF 2.0-Compliance-Übersicht](../../../rtcdp/privacy/privacy-overview.md) .

## Integration von Audience Managern

Adobe Audience Manager (AAM) unterstützt die IAB TCF 2.0, mit der Sie Entscheidungen zum Schutz der Privatsphäre von Kunden bewerten, berücksichtigen und an nachgeschaltete Partner weiterleiten können. Weitere Informationen finden Sie in der Dokumentation zum [Senden von Daten an Audience Manager](../audience-manager/audience-manager-overview.md).

>[!TIP]
>
>Um über das AEP Web SDK mit Audience Manager zu integrieren, müssen Sie eine Edge-Konfiguration für die Weiterleitung an Adobe Audience Manager einrichten.

## Experience Ereignisses- und Adobe Analytics-Integration

Während die Echtzeit-CDP und die Audiencen des Audience Managers die aktuellen Voreinstellungen für die Zustimmung des Kunden verfolgen, kann Experience Ereignisses die Voreinstellungen des Kunden für die Zustimmung speichern, die bei der Erfassung des Ereignisses aktiv waren.

Zur Erhebung von Informationen über die Zustimmung zu Ereignissen ist Folgendes erforderlich:

- Ein auf der [!DNL XDM Experience Event] Klasse basierender Datensatz mit dem [!DNL Experience Event] Datenschutz-Mixin.
- Eine Kantenkonfiguration, die mit dem obigen [!DNL XDM Experience Event] Datensatz eingerichtet wurde.

Weitere Informationen zum Konvertieren eines XDM Experience Ereignisses in einen Analytics-Treffer finden Sie in der [Analytics-Übersichtsdokumentation](../analytics/analytics-overview.md) .

## AEP Web SDK-Integration

Die folgenden Abschnitte beschreiben die wichtigsten Integrationspunkte zwischen dem IAB TCF 2.0 und dem AEP Web SDK.

>[!NOTE]
>
>Auch ohne Echtzeit-CDP oder Audience Manager-Einrichtung können Sie IAB TCF 2.0 mit dem Web SDK integrieren. Mit den Voreinstellungen für die Zustimmung können Sie die Erfassung von Experience Ereignisses steuern und ein Identitäts-Cookie einrichten.

### Standardgenehmigung

Die Standardgenehmigung wird verwendet, wenn für einen Kunden noch keine Einwilligung gespeichert wurde. Das bedeutet, dass die standardmäßigen Zustimmungsoptionen das Verhalten des AEP Web SDK steuern und je nach Region des Kunden ändern können.

Wenn Sie z. B. einen Kunden haben, der nicht in den Zuständigkeitsbereich der Allgemeinen Datenschutzverordnung (GDPR) fällt, könnte die Standardgenehmigung auf `in`, jedoch innerhalb des Zuständigkeitsbereichs von GDPR, festgelegt werden, dass die Standardgenehmigung auf `pending`festgelegt werden kann. Ihre Cloud-Management-Plattform (CMP) könnte die Region des Kunden ermitteln und die Kennzeichnung `gdprApplies` für die IAB TCF 2.0 bereitstellen. Mit diesem Flag können Sie die Standardgenehmigung festlegen.

Weitere Informationen zur Standardgenehmigung finden Sie im Abschnitt zur [Standardgenehmigung](../../fundamentals/configuring-the-sdk.md#default-consent) in der SDK-Konfigurationsdokumentation.

### Einwilligung beim Ändern

Das AEP Web SDK verfügt über einen `setConsent` Befehl, der die Voreinstellungen Ihres Kunden für die Einwilligung an alle Adoben mit IAB TCF 2.0 weiterleitet. Wenn Sie eine Integration mit CDP in Echtzeit durchführen, wird dadurch das Profil Ihres Kunden aktualisiert. Wenn Sie in Audience Manager integriert sind, werden die Kundeninformationen aktualisiert. Durch Aufruf dieser Funktion wird auch ein Cookie mit einer &quot;Alles-oder-nichts-Zustimmungsvoreinstellung&quot;gesetzt, das steuert, ob zukünftige Experience Ereignisses gesendet werden dürfen. Diese Aktion soll bei jeder Änderung der Zustimmung aufgerufen werden. Beim Laden zukünftiger Seiten wird das Experience Edge-Cookie für die Zustimmung gelesen, um zu ermitteln, ob Experience Ereignisses gesendet werden kann und ob ein Identitäts-Cookie gesetzt werden kann.

Ähnlich wie bei der IAB TCF 2.0-Integration des Audience Managers gibt Experience Edge seine Zustimmung, wenn ein Kunde seine ausdrückliche Zustimmung zu folgenden Zwecken erteilt hat:

- **Zweck 1:** Store- und/oder Zugriffsinformationen auf einem Gerät
- **Zweck 10:** Entwicklung und Verbesserung von Produkten
- **Sonderzweck 1:** Sicherstellen der Sicherheit, Vermeiden von Betrug und Debuggen. (Gemäß den IAB-TCF-Vorschriften ist dies immer einverstanden)
- **Berechtigung des Anbieters der Adobe:** Zustimmung zur Adobe (Hersteller 565)

Weitere Informationen zum `setConsent` Befehl finden Sie in der Dokumentation zur [Unterstützungszustimmung](../../fundamentals/supporting-consent.md).

### Hinzufügen der Zustimmung zu Experience Ereignisses

AEP Web SDK verfügt über einen `sendEvent` Befehl, mit dem ein Experience Ereignis erfasst wird. Wenn Sie in Experience Ereignisses oder Adobe Analytics integriert sind und die Voreinstellungen für die Zustimmung bei jedem Experience Ereignis einholen möchten, sollten Sie die Informationen zur Einwilligung jedem `sendEvent` Befehl hinzufügen.

Weitere Informationen zum `sendEvent` Befehl finden Sie in der Dokumentation zu [Tracking-Ereignissen](../../fundamentals/tracking-events.md).

## Nächste Schritte

Da Sie sich mit dem IAB Transparency &amp; Consent Framework 2.0 auskennen, lesen Sie bitte eine der Leitfäden zur Verwendung von IAB TCF 2.0 [mit Adobe Experience Platform Launch](./with-launch.md) oder [ohne Adobe Experience Platform Launch](./without-launch.md).
