---
title: IAB TCF 2.0-Unterstützung in der Adobe Experience Platform Web SDK
description: Erfahren Sie, wie Sie die Einverständnisvoreinstellungen für IAB TCF 2.0 mit der Adobe Experience Platform Web SDK unterstützen.
keywords: Einverständnis;setConsent;Profil-Datenschutz-Feldergruppe;Experience Event Privacy-Feldergruppe;Datenschutz-Feldergruppe;IAB TCF 2.0;Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%

---

# IAB TCF 2.0-Unterstützung in der Adobe Experience Platform Web SDK

Adobe Experience Platform Web SDK unterstützt das Interactive Advertising Bureau Transparency &amp; Consent Framework, Version 2.0 (IAB TCF 2.0). In diesem Handbuch werden die Anforderungen für die Unterstützung von IAB TCF 2.0 durch Adobe Experience Platform Web SDK zur Integration in Adobe Real-Time Customer Data Platform, Audience Manager, Experience Events, Adobe Analytics und Edge Network erläutert.

Darüber hinaus stehen die folgenden Handbücher zur Verfügung, in denen Sie lernen, wie Sie IAB TCF 2.0 mit und ohne Tags integrieren.

- [Mit Tags](./with-tags.md)
- [Ohne Tags](./without-tags.md)

## Erste Schritte

Um Web SDK mit IAB TCF 2.0 implementieren zu können, müssen Sie über Grundkenntnisse des Experience-Datenmodells (XDM) und der Erlebnisereignisse verfügen. Bevor Sie beginnen, lesen Sie bitte das folgende Dokument:

- [Übersicht über das Experience-Datenmodell-System (XDM](../../../xdm/home.md): Standardisierung und Interoperabilität sind Schlüsselkonzepte von Adobe Experience Platform. [!DNL Experience Data Model (XDM)] von Adobe unterstützt ist ein Versuch, Kundenerlebnisdaten zu standardisieren und Schemata für das Kundenerlebnis-Management zu definieren.

## Experience Platform-Integration

Um Einverständnisdaten mithilfe der SDK an Adobe Experience Platform zu senden, ist Folgendes erforderlich:

- Ein Datensatz, dessen Schema auf der [!DNL XDM Individual Profile]-Klasse basiert und TCF 2.0-Einverständnisfelder enthält, die für die Verwendung in [!DNL Real-Time Customer Profile] aktiviert sind.
- Ein mit Experience Platform eingerichteter Datenstrom und der oben erwähnte profilaktivierte Datensatz.

Anweisungen zum Erstellen der [&#x200B; Datensätze und des Datenstroms finden Sie &#x200B;](../../../landing/governance-privacy-security/consent/iab/overview.md) Handbuch zur TCF 2.0-Konformität .

## Audience Manager-Integration

Adobe Audience Manager (AAM) bietet Unterstützung für IAB TCF 2.0, mit dem Sie Datenschutzentscheidungen von Kundinnen und Kunden bewerten, berücksichtigen und an nachgelagerte Partnerinnen und Partner weiterleiten können. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Um über Adobe Experience Platform Web SDK eine Integration mit Audience Manager zu ermöglichen, stellen Sie sicher, dass ein Datenstrom für die Weiterleitung an Adobe Audience Manager eingerichtet ist.

## Integration von Experience Events und Adobe Analytics

Während die Zielgruppen von Real-Time CDP und Audience Manager die aktuellen Einverständnisvoreinstellungen eines Kunden verfolgen, können Erlebnisereignisse die Einverständnisvoreinstellungen eines Kunden enthalten, die zum Zeitpunkt der Erfassung des Ereignisses aktiv waren.

Um Einverständnisinformationen zu Ereignissen zu erfassen, ist Folgendes erforderlich:

- Ein Datensatz, der auf der [!DNL XDM Experience Event]-Klasse mit der [!DNL Experience Event]-Datenschutzschemafeldgruppe basiert.
- Ein Datenstrom, der mit dem oben [!DNL XDM Experience Event] Datensatz eingerichtet wird.

Weitere Informationen zum Konvertieren eines XDM-Erlebnisereignisses in einen Analytics-Treffer finden Sie unter [Senden von Daten an Adobe Analytics mithilfe der Web-SDK](/help/web-sdk/use-cases/adobe-analytics.md).

## Adobe Experience Platform Web SDK-Integration

In den folgenden Abschnitten werden die wichtigsten Integrationspunkte zwischen IAB TCF 2.0 und Adobe Experience Platform Web SDK beschrieben.

>[!NOTE]
>
>Selbst ohne Einrichtung von Real-Time CDP oder Audience Manager können Sie IAB TCF 2.0 weiterhin mit der Web-SDK integrieren. Die Einverständnisvoreinstellungen können verwendet werden, um die Erfassung von Erlebnisereignissen zu steuern und ein Identitäts-Cookie zu setzen.

### Standard-Einverständnis

Das Standardeinverständnis wird verwendet, wenn für einen Kunden bereits keine Einverständnisvoreinstellung gespeichert wurde. Dies bedeutet, dass die standardmäßigen Einverständnisoptionen das Verhalten von Adobe Experience Platform Web SDK steuern und sich je nach Region des Kunden ändern können.

Wenn Sie beispielsweise einen Kunden haben, der nicht unter die Datenschutz-Grundverordnung (DSGVO) fällt, könnte die standardmäßige Einwilligung auf `in` festgelegt werden, aber innerhalb der Gerichtsbarkeit der DSGVO könnte die standardmäßige Einwilligung auf `pending` festgelegt werden. Ihre Consent Management Platform (CMP) erkennt möglicherweise die Region des Kunden und stellt das Flag `gdprApplies` IAB TCF 2.0 bereit. Diese Markierung kann verwendet werden, um das Standardeinverständnis festzulegen. Weitere Informationen finden Sie unter [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) .

### Festlegen des Einverständnisses bei Änderungen

Adobe Experience Platform Web SDK verfügt über einen `setConsent`-Befehl, der die Einverständnisvoreinstellungen Ihres Kunden mithilfe von IAB TCF 2.0 an alle Adobe-Services übermittelt. Wenn Sie mit Real-Time CDP integrieren, wird dadurch das Kundenprofil aktualisiert. Wenn Sie mit Audience Manager integrieren, werden dadurch die Kundeninformationen aktualisiert. Durch den Aufruf dieser Methode wird auch ein Cookie mit einer Alles-oder-Nichts-Einverständnisvoreinstellung gesetzt, die steuert, ob zukünftige Erlebnisereignisse gesendet werden dürfen. Diese Aktion soll aufgerufen werden, wenn sich das Einverständnis ändert. Bei zukünftigen Seitenladevorgängen wird das Edge Network-Einverständnis-Cookie gelesen, um zu bestimmen, ob Erlebnisereignisse gesendet werden können und ob ein Identitäts-Cookie gesetzt werden kann.

Ähnlich wie bei der Audience Manager IAB TCF 2.0-Integration erteilt die Edge Network ihr Einverständnis, wenn ein Kunde zu folgenden Zwecken seine ausdrückliche Zustimmung erteilt hat:

- **Zweck 1:** Speichern und/oder Zugreifen auf Informationen auf einem Gerät
- **Zweck 10:** Entwicklung und Verbesserung von Produkten
- **Sonderzweck 1:** Gewährleistung der Sicherheit, Verhinderung von Betrug und Fehlerbehebung. (Gemäß den IAB-TCF-Vorschriften ist dies immer zulässig.)
- **Berechtigung für Adobe-Anbieter:** Einverständnis für Adobe (Anbieter 565)

Weitere Informationen zum Befehl `setConsent` finden Sie in der entsprechenden Web SDK-Dokumentation unter [setConsent](../../../web-sdk/commands/setconsent.md).

### Hinzufügen des Einverständnisses zu Erlebnisereignissen

Adobe Experience Platform Web SDK verfügt über einen [`sendEvent`](/help/web-sdk/commands/sendevent/overview.md), der ein Erlebnisereignis erfasst. Wenn Sie mit Erlebnisereignissen oder Adobe Analytics integrieren und die Einverständnisvoreinstellungen für jedes Erlebnisereignis wünschen, fügen Sie jedem `sendEvent`-Befehl Einverständnisinformationen hinzu.

## Nächste Schritte

Nachdem Sie nun über ein grundlegendes Verständnis des IAB Transparency &amp; Consent Framework 2.0 verfügen, lesen Sie bitte eine der Anleitungen zur Verwendung von IAB TCF 2.0 [mit Tags](./with-tags.md) oder [ohne Tags](./without-tags.md).
