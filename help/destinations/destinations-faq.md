---
keywords: Ziele; Fragen; häufig gestellte Fragen; FAQ; Ziele FAQ
title: Häufig gestellte Fragen
description: Antworten auf die am häufigsten gestellten Fragen zu Adobe Experience Platform-Zielen
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1670'
ht-degree: 3%

---

# Häufig gestellte Fragen {#faq}

## Überblick {#overview}

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Adobe Experience Platform-Zielen. Fragen und Fehlerbehebungen für andere [!DNL Experience Platform]-Services, einschließlich solcher, die für alle [!DNL Experience Platform]-APIs gelten, finden Sie im [Handbuch zur Fehlerbehebung bei Experience Platform](../landing/troubleshooting.md).

## Fragen zu allgemeinen Zielen {#general}

### Warum werden in der Experience Platform-Benutzeroberfläche und in den exportierten CSV-Dateien unterschiedliche Profilzahlen angezeigt?

+++Antwort
Dieses Verhalten ist aufgrund der Art und Weise, wie Experience Platform die Segmentierung durchführt, normal.

Bei der Streaming-Segmentierung wird die Profilanzahl für Streaming-Zielgruppen über den ganzen Tag hinweg aktualisiert, während bei der Batch-Segmentierung die Profilanzahl für Batch-Zielgruppen einmal alle 24 Stunden aktualisiert wird.

Wenn sich der Zeitplan für den Zielgruppenexport vom Segmentierungsplan unterscheidet, unterscheiden sich die Profilzahlen zwischen der Benutzeroberfläche und der exportierten [!DNL CSV], insbesondere bei Streaming-Zielgruppen.

Weitere Informationen finden [&#x200B; in der &#x200B;](../segmentation/home.md) zum Segmentierungs-Service .
+++

### Warum werden niedrige Übereinstimmungsraten beim Deaktivieren und erneuten Aktivieren einer aktualisierten Zielgruppe für dasselbe Ziel angezeigt?

+++Antwort

Durch die Deaktivierung und Aktivierung einer Zielgruppe über ein Streaming-Ziel wird bei der erneuten Aktivierung der Zielgruppe an dasselbe Streaming-Ziel keine Aufstockung Trigger.

**Beispiel**

Sie haben eine Zielgruppe bestehend aus 10 Profilen für ein Streaming-Ziel aktiviert.

Nach der Aktivierung der Zielgruppe ist klar, dass Sie die Zielgruppenkonfiguration ändern möchten, sodass Sie die Zielgruppe deaktivieren und ihre Populationskriterien ändern, was zu einer Zielgruppenpopulation von 100 Profilen führt.

Sie aktivieren die aktualisierte Zielgruppe erneut für dasselbe Ziel, aber da keine Aufstockung ausgelöst wird, erhält Ihr Ziel nicht die zusätzlichen 90 Profile.

**Lösung**

Um sicherzustellen, dass alle Profile an Ihr Ziel gesendet werden, müssen Sie eine neue Zielgruppe mit der neuen Konfiguration erstellen und sie dann für Ihr Ziel aktivieren.

+++

### Gibt es ein Signal, das an ein Ziel gesendet wird, wenn eine Zielgruppe aus einem Ziel entfernt wird, und damit angibt, dass die Zielgruppe entfernt wird?

+++Antwort

Nein, es besteht keine Abhängigkeit zwischen dem Experience Platform-Ziel und der Kundeninstanz des Zielsystems. Auf der empfangenden Seite ist der einzige Hinweis, den das Zielsystem sehen würde,, dass es diese Zielgruppendaten nicht mehr erhält.

+++

<!--
## [!DNL Experience Cloud Audiences] {#eca-faq}

### What are the differences between the Experience Cloud Audiences and Adobe Target destinations?

+++Answer

See the table below for a feature comparison between the Experience Cloud Audiences and Adobe Target destinations.

||Experience Cloud Audiences|Adobe Target|
|---|---|---|
| **Supported Experience Cloud apps** | Supports audience activation to Audience Manager, Adobe Target, Adobe Analytics, Advertising Cloud, Marketo, Adobe Campaign | Supports audience activation only to Adobe Target |
| **Supports audience activation** | ✓ | ✓ |
| **Supports attribute activation** | X | ✓ |
| **Latency** | Profiles begin activating in 6 hours. Full population is visible in 48 hours​. |Depends on implementation​ type. <ul><li>Web SDK enables same-page/next-page​ personalization.</li><li>AT.js enables next-session personalization.</li></ul> |
| **DULE support** | ✓ | ✓ |
| **Marketing actions support** | ✓ | ✓ |
| **Supported IDs** | [!DNL ECID], [!DNL GAID], [!DNL IDFA], [!DNL email_lc_sha256] | Any ID type |
| **Sandbox support** | One sandbox | Multiple sandboxes |
| **Consent support** | X | Yes. Requires Privacy & Security Shield. |
| **Edge segmentation support** | Supports activation of edge audiences. Does not support edge segmentation. | Supports edge segmentation and activation of edge audiences. |
| **Supported audiences** | All types of audiences  | Edge merge policy required for activation.|

+++

-->

## [!DNL Facebook Custom Audiences] {#facebook-faq}

### Was muss ich tun, bevor ich Zielgruppen in [!DNL Facebook Custom Audiences] aktivieren kann?

+++Antwort
Bevor Sie Ihre Zielgruppen an [!DNL Facebook] senden können, müssen Sie die folgenden Anforderungen erfüllen:

* Für Ihr [!DNL Facebook]-Benutzerkonto muss die **[!DNL Manage campaigns]** für das Werbekonto aktiviert sein, das Sie verwenden möchten.
* Adobe Experience Cloud Das Geschäftskonto **&#x200B;**&#x200B;muss Werbepartner in Ihrem [!DNL Facebook Ad Account] hinzugefügt werden. Verwenden Sie `business ID=206617933627973`. Weitere Informationen finden [&#x200B; in der Facebook](https://www.facebook.com/business/help/1717412048538897)Dokumentation unter „Partner zu Ihrem Business Manager hinzufügen“.

  >[!IMPORTANT]
  >
  > Beim Konfigurieren der Berechtigungen für Adobe Experience Cloud müssen Sie die Berechtigung **Kampagnen verwalten** aktivieren. Dies ist für die [!DNL Adobe Experience Platform]-Integration erforderlich.
* Lesen und unterschreiben Sie die [!DNL Facebook Custom Audiences]-Nutzungsbedingungen. Rufen Sie dazu `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]` auf, wobei `accountID` Ihre [!DNL Facebook Ad Account ID] ist.
+++

### Muss ich meinem [!DNL Facebook] Advertiser-Konto irgendwelche Apps oder Pixel hinzufügen?

+++Antwort
Nein. Da es sich hierbei nicht um eine pixelbasierte Integration handelt, müssen Sie keine Pixel zu Ihrem Advertiser-Konto hinzufügen.
+++

### Wie lange braucht Facebook, um Informationen aus Adobe Experience Platform zu verarbeiten?

+++Antwort
Ab März 2021 benötigt [!DNL Facebook Custom Audiences] bis zu einer Stunde, um die von [!DNL Experience Platform] erhaltenen Informationen zu verarbeiten.
+++

### Kann ich [!DNL Facebook Custom Audiences] für Zielgruppen-Targeting in anderen [!DNL Facebook]-Apps wie [!DNL Instagram] verwenden?

+++Antwort
Sie können das [!DNL Facebook Custom Audiences]-Ziel für das Audience-Targeting in der gesamten Facebook-Familie von Apps verwenden, die von [!DNL Facebook Custom Audiences] unterstützt werden, einschließlich [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] und [!DNL Messenger]. Die Auswahl der App, in der Werbetreibende Kampagnen durchführen möchten, wird auf der Platzierungsebene in [!DNL Facebook Ads Manager] angezeigt.
+++

### Was ist der Unterschied zwischen der [!DNL Facebook Custom Audiences]-Verbindung und [!DNL Facebook Pixel] Erweiterung?

+++Antwort
Die [!DNL Facebook Custom Audiences]-Verbindung verwendet [!DNL Experience Platform] Identitäten beim Senden von Zielgruppen an [!DNL Facebook], während die [[!DNL Facebook Pixel] Verbindung](../destinations/catalog/advertising/facebook-pixel.md) das [!DNL Facebook] Pixel verwendet, das in einer Website integriert ist.

Diese beiden Integrationen ergänzen sich gegenseitig. Sie können beide verwenden, um eine bessere Zielgruppenabdeckung zu gewährleisten. Beispielsweise können Sie die [!DNL Facebook Pixel]-Erweiterung für Interessenten verwenden, die kein Konto erstellt haben, während [!DNL Facebook Custom Audiences] Ihnen helfen können, bestehende Kundinnen und Kunden auf der Grundlage [!DNL Experience Platform] Identitäten anzusprechen.
+++

### Unterstützt die Adobe Experience Platform-Integration mit [!DNL Facebook Custom Audiences] die Disqualifizierung von Benutzenden aus einer Zielgruppe, wenn sie sich nicht mehr dafür qualifizieren?**

+++Antwort
Ja, die Integration unterstützt das Entfernen von Benutzern aus [!DNL Facebook Custom Audiences], wenn sie sich nicht mehr qualifizieren.
+++

### Wie sollte ich die Zielgruppendaten hashen, bevor ich sie an [!DNL Facebook] sende?

+++Antwort
[!DNL Facebook] erfordert, dass keine personenbezogenen Daten (PII) in klarer Form gesendet werden. Daher können die für [!DNL Facebook] aktivierten Zielgruppen als Hash-*(*) verschlüsselt werden, z. B. E-Mail-Adressen oder Telefonnummern.

Ausführliche Erläuterungen zu den Anforderungen für den ID-Abgleich finden Sie unter [ID-Abgleichanforderungen](catalog/social/facebook.md#id-matching-requirements).
+++

### Welche Arten von Identitäten kann ich in [!DNL Facebook Custom Audiences] aktivieren?

+++Antwort
[!DNL Facebook Custom Audiences] unterstützt die Aktivierung der folgenden Identitäten: gehashte E-Mails, gehashte Telefonnummern, [!DNL GAID], [!DNL IDFA] und benutzerdefinierte externe IDs.
+++

### Kann ich in der Experience Platform-Benutzeroberfläche mehrere Facebook-Ziele für separate Facebook-Konten erstellen?

+++Antwort
Ja. Ein Facebook-Ziel in Experience Platform ist 1:1 zu einem Werbekonto in Facebook. Sie können für jedes Facebook-Werbekonto in Ihrem Unternehmen ein eigenes Facebook-Ziel erstellen. Befolgen Sie die [Tutorial zur Zielverbindung](/help/destinations/ui/connect-destination.md) und stellen Sie in der Experience Platform-Benutzeroberfläche eine Verbindung zu einem separaten Facebook-Konto für jedes neue Facebook-Ziel her. Die Anzahl der Facebook-Werbekonten, mit denen Sie eine Verbindung herstellen können, ist unbegrenzt.
+++

## Google Customer Match {#google-customer-match}

### Warum sehe ich beim Exportieren von Zielgruppen in Google Customer Match zusätzliche Zahlen, die am Ende der Zielgruppennamen in der Google-Benutzeroberfläche angehängt werden?

+++Antwort
Google erfordert, dass Zielgruppennamen eindeutig sind. Die angezeigten Zahlen sind [UNIX-Zeitstempel](https://www.unixtimestamp.com/) und werden angehängt, um die Zielgruppennamen eindeutig zu halten, wenn Sie dieselbe Zielgruppe mehreren Google-Zielen zugeordnet haben.
+++

## Abgestimmte LinkedIn-Zielgruppen {#linkedin}

### Muss ich meinem [!DNL LinkedIn] Advertiser-Konto irgendwelche Apps oder Pixel hinzufügen?

+++Antwort
Nein. Da es sich hierbei nicht um eine pixelbasierte Integration handelt, müssen Sie keine Pixel zu Ihrem Advertiser-Konto hinzufügen.
+++

### Was muss ich tun, bevor ich Zielgruppen in [!DNL LinkedIn Matched Audiences] aktivieren kann?

+++Antwort
Bevor Sie das [!UICONTROL LinkedIn Matched Audience]-Ziel verwenden können, stellen Sie sicher, dass Ihr [!DNL LinkedIn Campaign Manager]-Konto die [!DNL Creative Manager] Berechtigungsstufe oder höher hat.

Informationen zum Bearbeiten Ihrer [!DNL LinkedIn Campaign Manager]-Benutzerberechtigungen finden Sie unter [Hinzufügen, Bearbeiten und Entfernen von Benutzerberechtigungen für Advertising-Konten](https://www.linkedin.com/help/lms/answer/5753) in der LinkedIn-Dokumentation.
+++

### Wie sollte ich die Zielgruppendaten hashen, bevor ich sie an [!DNL LinkedIn] sende?

+++Antwort
[!DNL LinkedIn] erfordert, dass keine personenbezogenen Daten (PII) in klarer Form gesendet werden. Daher können die für [!DNL LinkedIn] aktivierten Zielgruppen als Hash-*(*) verschlüsselt werden, z. B. E-Mail-Adressen oder Telefonnummern.

Ausführliche Erläuterungen zu den Anforderungen für den ID-Abgleich finden Sie unter [ID-Abgleichanforderungen](catalog/social/linkedin.md#id-matching-requirements).
+++

### Welche Arten von Identitäten kann ich in [!DNL LinkedIn] aktivieren?

+++Antwort
[!DNL LinkedIn Matched Audiences] unterstützt die Aktivierung der folgenden Identitäten: gehashte E-Mails, [!DNL GAID] und [!DNL IDFA].

+++

## Personalisierung der gleichen und der nächsten Seite über die Adobe Target- und benutzerdefinierten Personalization-Ziele {#same-next-page-personalization}

### Muss ich die Experience Platform Web SDK verwenden, um Zielgruppen und Attribute an Adobe Target zu senden?

+++Antwort
Nein, die Web-SDK ist nicht erforderlich, um Zielgruppen für [Adobe Target zu aktivieren](catalog/personalization/adobe-target-connection.md).

Wenn jedoch [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html) anstelle von Web SDK verwendet wird, wird nur die Personalisierung der nächsten Sitzung unterstützt.

Bei [Personalisierung der gleichen Seite und der nächsten Seite](ui/activate-edge-personalization-destinations.md) müssen Sie entweder Web SDK oder die [Edge Network-API verwenden](https://developer.adobe.com/data-collection-apis/docs/api/). Weitere Informationen finden Sie in [&#x200B; Dokumentation unter Aktivieren von Zielgruppen für Edge](ui/activate-edge-personalization-destinations.md)Ziele .
+++

### Gibt es eine Begrenzung für die Anzahl der Attribute, die ich von Real-time Customer Data Platform an Adobe Target oder ein benutzerdefiniertes Personalization-Ziel senden kann?

+++Antwort
Ja, Anwendungsfälle für die Personalisierung derselben Seite und der nächsten Seite unterstützen beim Aktivieren von Zielgruppen für Adobe Target- oder benutzerdefinierte Personalization-Ziele maximal 30 Attribute pro Sandbox. Weitere Informationen zu Aktivierungsleitplanken finden Sie in der [Dokumentation zu Leitplanken](guardrails.md#edge-destinations-activation).
+++

### Welche Arten von Attributen werden für die Aktivierung unterstützt (z. B. Arrays, Zuordnungen usw.)?

+++Antwort
Derzeit werden nur statische Attribute mit einem Wert unterstützt, z. B. `person.name.firstName`. Array-Attribute werden derzeit nicht unterstützt.
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### Wie lange dauert es nach der Erstellung einer Zielgruppe in Experience Platform, bis diese Zielgruppe für Anwendungsfälle der Edge-Segmentierung verfügbar ist?

+++Antwort
Zielgruppendefinitionen werden in bis zu einer Stunde an die Edge Network weitergegeben. Wenn jedoch innerhalb dieser ersten Stunde eine Zielgruppe aktiviert wird, könnten einige Besucher fehlen, die sich für die Zielgruppe qualifiziert hätten.
+++

### Wo kann ich die aktivierten Attribute in Adobe Target sehen?

+++Antwort
Attribute stehen zur Verwendung in Target in {[} JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html?lang=de) und [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html?lang=de) Angeboten zur Verfügung.
+++

### Kann ich ein Ziel ohne Datenstrom erstellen und dann zu einem späteren Zeitpunkt einen Datenstrom zum selben Ziel hinzufügen?

+++Antwort
Dies wird derzeit nicht über die Benutzeroberfläche „Ziele“ unterstützt. Wenn Sie in diesem Fall Hilfe benötigen, wenden Sie sich bitte an den Adobe-Support.
+++

### Was passiert, wenn ich ein Adobe Target-Ziel lösche?

+++Antwort
Wenn Sie ein Ziel löschen, werden alle unter dem Ziel zugeordneten Zielgruppen und Attribute aus Adobe Target gelöscht und auch aus Edge Network entfernt.
+++

### Funktioniert die Integration mit der Edge Network-API?

+++Antwort
Ja, die Edge Network-API funktioniert mit dem benutzerdefinierten Personalization-Ziel. Da Profilattribute vertrauliche Daten enthalten können, müssen Sie zum Schutz dieser Daten beim benutzerdefinierten Personalization-Ziel die Edge Network-API für die Datenerfassung verwenden. Darüber hinaus müssen alle API-Aufrufe in einem [authentifizierten Kontext](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication/) erfolgen.
+++

### Ich kann nur eine einzige Zusammenführungsrichtlinie haben, die im Randbereich aktiv ist. Kann ich Zielgruppen erstellen, die eine andere Zusammenführungsrichtlinie verwenden, und sie dennoch als Streaming-Zielgruppen an Adobe Target senden?

+++Antwort
Nein. Alle Zielgruppen, die Sie für Adobe Target aktivieren möchten, müssen eine Active-On-Edge-[&#x200B; (Zusammenführungsrichtlinie) &#x200B;](../profile/merge-policies/ui-guide.md).
+++

### Werden Datennutzungskennzeichnungen und -durchsetzung (Data Usage Labeling and Enforcement, DULE) und Einverständnisrichtlinien durchgesetzt?

+++Antwort
Ja. Die [Data Governance- und Einverständnisrichtlinien](../data-governance/home.md), die erstellt und mit den ausgewählten Marketing-Aktionen verknüpft sind, steuern die Aktivierung der ausgewählten Attribute.
+++

### Sind die [!DNL Adobe Target]- und [!DNL Custom Personalization]-Ziele [!DNL HIPAA]?

+++Antwort
[!DNL Adobe Target] ist nicht [!DNL HIPPA] konform mit [[!DNL Adobe Healthcare Shield]](https://business.adobe.com/de/solutions/industries/healthcare.html). Kunden sollten sich bei ihren eigenen Rechtsabteilungen erkundigen, ob [!DNL HIPPA] für benutzerdefinierte Optimierungskanäle bereit sind, bevor sie die Edge-Personalisierung über [!DNL Adobe Target] oder die [!DNL Custom Personalization] Ziele verwenden.

Für Anwendungsfälle, bei denen die Verwaltung von Einverständnisrichtlinien skaliert werden muss, müssen Kunden [!DNL Adobe Privacy & Security Shield] kaufen. [!DNL Adobe Privacy & Security Shield] Funktionen werden als erweiterte Funktionssuite angeboten und können nicht separat erworben werden.

Dieser Service umfasst vom Kunden verwaltete Schlüssel und erhöhte Schwellenwerte für die Verwaltung des Kundendatenlebenszyklus.

Die [!DNL Adobe Target]- und [!DNL Custom Personalization] sind in die [Experience Platform-Datennutzungskennzeichnungen](../data-governance/labels/overview.md) und den [Service zur Durchsetzung von Einverständnisrichtlinien](../data-governance/enforcement/overview.md) integriert. Diese Funktionen stehen allen Kunden zur Verfügung.




+++

