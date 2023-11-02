---
keywords: Ziele; Fragen; häufig gestellte Fragen; FAQ; Ziele FAQ
title: Häufig gestellte Fragen
description: Antworten auf die am häufigsten gestellten Fragen zu Adobe Experience Platform-Zielen
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1634'
ht-degree: 5%

---

# Häufig gestellte Fragen {#faq}

## Übersicht {#overview}

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Adobe Experience Platform-Zielen. Für Fragen und Fehlerbehebung im Zusammenhang mit anderen [!DNL Platform] Dienste, einschließlich der in allen [!DNL Platform] APIs, siehe [Handbuch zur Fehlerbehebung bei Experience Platform](../landing/troubleshooting.md).

## Allgemeine Fragen zu Zielen {#general}

### Warum werden in der Experience Platform-Benutzeroberfläche und in den exportierten CSV-Dateien unterschiedliche Profilzahlen angezeigt?

+++Antwort Dies ist ein normales Verhalten aufgrund der Art und Weise, wie Experience Platform die Segmentierung durchführt.

Streaming-Segmentierung aktualisiert die Profilanzahl für Streaming-Zielgruppen über den ganzen Tag, während die Batch-Segmentierung die Profilanzahl für Batch-Zielgruppen einmal alle 24 Stunden aktualisiert.

Wenn sich der Zeitplan für den Zielgruppenexport vom Segmentierungsplan unterscheidet, zählt das Profil zwischen der Benutzeroberfläche und dem exportierten [!DNL CSV] -Datei wird anders aussehen, insbesondere wenn es um Streaming-Zielgruppen geht.

Siehe [Dokumentation zum Segmentierungsdienst](../segmentation/home.md) für weitere Details.
+++

### Warum werden bei der Deaktivierung und erneuten Aktivierung einer aktualisierten Zielgruppe für dasselbe Ziel niedrige Übereinstimmungsraten angezeigt?

+++Antwort

Bei der Deaktivierung und der Aktivierung einer Zielgruppe von einem Streaming-Ziel wird bei der erneuten Aktivierung der Zielgruppe an dasselbe Streaming-Ziel keine Aufstockung Trigger.

**Beispiel**

Sie haben eine Zielgruppe aus 10 Profilen für ein Streaming-Ziel aktiviert.

Nach der Aktivierung der Zielgruppe erkennen Sie, dass Sie die Zielgruppenkonfiguration ändern möchten, sodass Sie die Zielgruppe deaktivieren und ihre Populationskriterien ändern, sodass eine Zielgruppenpopulation von 100 Profilen entsteht.

Sie aktivieren die aktualisierte Zielgruppe erneut für dasselbe Ziel, da jedoch keine Aufstockung ausgelöst wird, erhält Ihr Ziel nicht die zusätzlichen 90 Profile.

**Lösung**

Um sicherzustellen, dass alle Profile an Ihr Ziel gesendet werden, müssen Sie mit der neuen Konfiguration eine neue Zielgruppe erstellen und diese dann für Ihr Ziel aktivieren.

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

### Was muss ich tun, bevor ich Zielgruppen in aktivieren kann? [!DNL Facebook Custom Audiences]?

+++Antwort Bevor Sie Ihre Zielgruppen an senden können [!DNL Facebook]müssen Sie sicherstellen, dass Sie die folgenden Anforderungen erfüllen:

* Ihre [!DNL Facebook] Das Benutzerkonto muss über die **[!DNL Manage campaigns]** -Berechtigung für das Anzeigenkonto aktiviert wurde, das Sie verwenden möchten.
* Die **Adobe Experience Cloud** Geschäftskonto muss als Werbepartner in Ihrem [!DNL Facebook Ad Account]. Verwenden Sie `business ID=206617933627973`. Siehe [Partner zu Ihrem Business Manager hinzufügen](https://www.facebook.com/business/help/1717412048538897) in der Dokumentation zu Facebook .

  >[!IMPORTANT]
  >
  > Beim Konfigurieren der Berechtigungen für Adobe Experience Cloud müssen Sie die Berechtigung **Kampagnen verwalten** aktivieren. Dies ist für die [!DNL Adobe Experience Platform]-Integration erforderlich.
* Lesen und unterschreiben Sie die [!DNL Facebook Custom Audiences]-Nutzungsbedingungen. Rufen Sie dazu `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]` auf, wobei `accountID` Ihre [!DNL Facebook Ad Account ID] ist.
+++

### Muss ich irgendwelche Apps oder Pixel zu meiner [!DNL Facebook] Werbekonto?

+++Antwort 
Nr. Da es sich hierbei nicht um eine pixelbasierte Integration handelt, müssen Sie Ihrem Advertiser-Konto keine Pixel hinzufügen.
+++

### Wie lange dauert die Verarbeitung von Informationen aus Adobe Experience Platform in Facebook?

+++Antwort ab März 2021, [!DNL Facebook Custom Audiences] benötigt bis zu eine Stunde, um die von erhaltenen Informationen zu verarbeiten [!DNL Platform].
+++

### Kann ich [!DNL Facebook Custom Audiences] für Zielgruppen-Targeting in anderen [!DNL Facebook] Apps, wie [!DNL Instagram]?

++ + Umlauffußbereich Sie können [!DNL Facebook Custom Audiences] Ziel für Zielgruppen-Targeting in der Facebook-Familie von Apps, die von [!DNL Facebook Custom Audiences], einschließlich [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], und [!DNL Messenger]. Die Auswahl der App, für die Advertiser Kampagnen ausführen möchten, wird auf der Platzierungsebene in [!DNL Facebook Ads Manager].
+++

### Was ist der Unterschied zwischen dem [!DNL Facebook Custom Audiences] Verbindung und [!DNL Facebook Pixel] Erweiterung?

++ + Antwort auf die [!DNL Facebook Custom Audiences] Verbindungsnutzungen [!DNL Platform] Identitäten beim Senden von Zielgruppen an [!DNL Facebook], während die [[!DNL Facebook Pixel] connection](../destinations/catalog/advertising/facebook-pixel.md) verwendet die [!DNL Facebook] in eine Website integriert ist.

Diese beiden Integrationen ergänzen sich. Sie können beide verwenden, um eine bessere Zielgruppenabdeckung sicherzustellen. Als Beispiel können Sie die [!DNL Facebook Pixel] Erweiterung für die Suche nach Website-Besuchern, die kein Konto erstellt haben, [!DNL Facebook Custom Audiences] können Ihnen dabei helfen, bestehende Kunden auf Basis von [!DNL Platform] Identitäten.
+++

### Ist die Adobe Experience Platform-Integration mit [!DNL Facebook Custom Audiences] die Nichtqualifizierung von Benutzern von einer Zielgruppe zu unterstützen, wenn sie sich nicht mehr dafür qualifizieren?**

++ + Antwort Ja Die Integration unterstützt das Entfernen von Benutzern aus [!DNL Facebook Custom Audiences] wenn sie sich nicht mehr qualifizieren.
+++

### Wie sollen die Zielgruppendaten gehasht werden, bevor sie an gesendet werden? [!DNL Facebook]?

+++Antwort
[!DNL Facebook] erfordert, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher werden die Zielgruppen für [!DNL Facebook] kann deaktiviert werden *Hash* Kennungen wie E-Mail-Adressen oder Telefonnummern.

Detaillierte Erläuterungen zu den Anforderungen an die ID-Zuordnung finden Sie unter [Anforderungen an die ID-Übereinstimmung](catalog/social/facebook.md#id-matching-requirements).
+++

### Welche Identitäten kann ich aktivieren? [!DNL Facebook Custom Audiences]?

+++Antwort
[!DNL Facebook Custom Audiences] unterstützt die Aktivierung der folgenden Identitäten: Hash-E-Mails, Hash-Telefonnummern, [!DNL GAID], [!DNL IDFA]und benutzerdefinierte externe IDs.
+++

### Kann ich mehrere Facebook-Ziele in der Platform-Benutzeroberfläche für separate Facebook-Konten erstellen?

+++Antwort
Ja. Ein Facebook-Ziel in Experience Platform ist 1:1 für ein Anzeigenkonto in Facebook. Sie können für jedes Facebook-Anzeigenkonto in Ihrem Unternehmen ein eigenes Facebook-Ziel erstellen. Befolgen Sie die [Tutorial zur Zielverbindung](/help/destinations/ui/connect-destination.md) und stellen Sie für jedes neue Facebook-Ziel in der Platform-Benutzeroberfläche eine Verbindung zu einem separaten Facebook-Konto her. Die Anzahl der Facebook-Anzeigenkonten, mit denen Sie eine Verbindung herstellen können, ist unbegrenzt.
+++

## Google-Kundenabgleich {#google-customer-match}

### Warum werden beim Exportieren von Zielgruppen in Google-Kundenabgleich am Ende der Zielgruppennamen in der Google-Benutzeroberfläche zusätzliche Zahlen angehängt?

+++Antwort Google erfordert, dass Zielgruppennamen eindeutig sind. Die Zahlen, die Sie sehen, sind [UNIX-Zeitstempel](https://www.unixtimestamp.com/) und sie werden angehängt, um die Zielgruppennamen eindeutig zu halten, wenn Sie dieselbe Zielgruppe mehreren Google-Zielen zugeordnet haben.
+++

## LinkedIn Matched Audiences {#linkedin}

### Muss ich irgendwelche Apps oder Pixel zu meiner [!DNL LinkedIn] Werbekonto?

+++Antwort 
Nr. Da es sich hierbei nicht um eine pixelbasierte Integration handelt, müssen Sie Ihrem Advertiser-Konto keine Pixel hinzufügen.
+++

### Was muss ich tun, bevor ich Zielgruppen in aktivieren kann? [!DNL LinkedIn Matched Audiences]?

+++Antwort Bevor Sie die [!UICONTROL LinkedIn Match Audience] Ziel, stellen Sie sicher, dass Ihre [!DNL LinkedIn Campaign Manager] -Konto hat die [!DNL Creative Manager] Berechtigungsebene oder höher.

Informationen zum Bearbeiten Ihrer [!DNL LinkedIn Campaign Manager] Benutzerberechtigungen, siehe [Hinzufügen, Bearbeiten und Entfernen von Benutzerberechtigungen für Werbekonten](https://www.linkedin.com/help/lms/answer/5753) in der LinkedIn-Dokumentation.
+++

### Wie sollen die Zielgruppendaten gehasht werden, bevor sie an gesendet werden? [!DNL LinkedIn]?

+++Antwort
[!DNL LinkedIn] erfordert, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher werden die Zielgruppen für [!DNL LinkedIn] kann deaktiviert werden *Hash* Kennungen wie E-Mail-Adressen oder Telefonnummern.

Detaillierte Erläuterungen zu den Anforderungen an die ID-Zuordnung finden Sie unter [Anforderungen an die ID-Übereinstimmung](catalog/social/linkedin.md#id-matching-requirements).
+++

### Welche Identitäten kann ich aktivieren? [!DNL LinkedIn]?

+++Antwort
[!DNL LinkedIn Matched Audiences] unterstützt die Aktivierung der folgenden Identitäten: Hash-E-Mails, [!DNL GAID], und [!DNL IDFA].

+++

## Personalisierung auf derselben Seite und auf der nächsten Seite über die Adobe Target- und benutzerdefinierten Personalisierungsziele {#same-next-page-personalization}

### Muss ich das Experience Platform Web SDK verwenden, um Zielgruppen und Attribute an Adobe Target zu senden?

+++Antwort Nein, [Web SDK](../edge/home.md) ist nicht erforderlich, um Zielgruppen für [Adobe Target](catalog/personalization/adobe-target-connection.md).

Wenn jedoch [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html?lang=de) anstelle des Web SDK verwendet wird, wird nur die Personalisierung der nächsten Sitzung unterstützt.

Für [Personalisierung auf derselben Seite und auf der nächsten Seite](ui/activate-edge-personalization-destinations.md) Anwendungsbeispiele verwenden, müssen Sie entweder [Web SDK](../edge/home.md) oder [Edge Network Server-API](../server-api/overview.md). Siehe die Dokumentation unter [Aktivieren von Zielgruppen für Edge-Ziele](ui/activate-edge-personalization-destinations.md) für weitere Implementierungsdetails.
+++

### Gibt es eine Begrenzung für die Anzahl der Attribute, die ich von Real-time Customer Data Platform an Adobe Target oder ein benutzerspezifisches Personalisierungsziel senden kann?

++ + Antwort Ja, Personalisierungsfälle für die gleiche Seite und die nächste Seite unterstützen maximal 30 Attribute pro Sandbox, wenn Zielgruppen für Adobe Target- oder benutzerdefinierte Personalisierungsziele aktiviert werden. Weitere Informationen zu AktivierungsLimits finden Sie in der [Limits-Dokumentation](guardrails.md#edge-destinations-activation).
+++

### Welche Attributtypen werden für die Aktivierung unterstützt (z. B. Arrays, Maps usw.)?

+++Antwort Derzeit werden nur statische Attribute mit einem Wert unterstützt, z. B. `person.name.firstName`. Array-Attribute werden derzeit nicht unterstützt.
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### Wie lange dauert es, bis diese Zielgruppe für Anwendungsfälle der Kantensegmentierung verfügbar ist, nachdem ich eine Zielgruppe in Experience Platform erstellt habe?

+++ Zielgruppendefinitionen mit Antworten werden in die [Edge Network](../edge/home.md) in bis zu einer Stunde. Wenn jedoch innerhalb dieser ersten Stunde eine Zielgruppe aktiviert wird, können einige Besucher verpasst werden, die sich für die Zielgruppe qualifiziert hätten.
+++

### Wo kann ich die aktivierten Attribute in Adobe Target sehen?

+++Antwortattribute sind für die Verwendung in Target verfügbar [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) und [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html?lang=de) Angebote.
+++

### Kann ich ein Ziel ohne Datastream erstellen und dann zu einem späteren Zeitpunkt demselben Ziel einen Datastream hinzufügen?

+++Antwort Dies wird derzeit nicht über die Benutzeroberfläche &quot;Ziele&quot;unterstützt. Wenn Sie in diesem Fall Hilfe benötigen, wenden Sie sich bitte an Ihren Adobe-Support-Mitarbeiter.
+++

### Was passiert, wenn ich ein Adobe Target-Ziel lösche?

+++Antwort Wenn Sie ein Ziel löschen, werden alle Zielgruppen und Attribute, die unter dem Ziel zugeordnet sind, aus Adobe Target gelöscht und auch aus dem Edge Network entfernt.
+++

### Funktioniert die Integration mit der Edge Network Server-API?

++ + Antwort Ja, die Edge Network Server-API funktioniert mit dem benutzerdefinierten Personalisierungsziel. Da Profilattribute möglicherweise vertrauliche Daten enthalten, müssen Sie zum Schutz dieser Daten für das benutzerdefinierte Personalisierungsziel die Edge Network Server-API für die Datenerfassung verwenden. Darüber hinaus müssen alle API-Aufrufe in einer [authentifizierter Kontext](../server-api/authentication.md).
+++

### Ich kann nur eine Zusammenführungsrichtlinie haben, die aktiv ist. Kann ich Zielgruppen erstellen, die eine andere Zusammenführungsrichtlinie verwenden und diese dennoch als Streaming-Zielgruppen an Adobe Target senden?

+++Antwort 
Nr. Alle Zielgruppen, die Sie für Adobe Target aktivieren möchten, müssen eine aktive On-Edge-Funktion verwenden [Zusammenführungsrichtlinie](../profile/merge-policies/ui-guide.md).
+++

### Werden DULE (Data Usage Labeling and Enforcement) und Einverständnisrichtlinien durchgesetzt?

+++Antwort
Ja. Die [Data Governance und Einverständnisrichtlinien](../data-governance/home.md) Die Aktivierung der ausgewählten Attribute wird durch die erstellten und mit den ausgewählten Marketing-Aktionen verknüpften bestimmt.
+++

### Sind die [!DNL Adobe Target] und [!DNL Custom Personalization] Ziele [!DNL HIPAA]-kompatibel?

+++Antwort
[!DNL Adobe Target] ist nicht [!DNL HIPPA]-kompatibel mit [[!DNL Adobe Healthcare Shield]](https://business.adobe.com/solutions/industries/healthcare.html). Kunden sollten sich an ihre eigenen Rechtsabteilungen wenden, um [!DNL HIPPA]-Bereitschaft für benutzerdefinierte Optimierungskanäle vor Verwendung der Edge-Personalisierung über [!DNL Adobe Target] oder [!DNL Custom Personalization] Ziele.

Für Anwendungsfälle, in denen die Verwaltung von Zustimmungsrichtlinien skaliert angewendet werden muss, müssen Kunden [!DNL Adobe Privacy & Security Shield]. [!DNL Adobe Privacy & Security Shield] -Funktionen werden als erweiterte Suite von Funktionen verkauft und möglicherweise nicht separat erworben.

Dieser Dienst umfasst kundenverwaltete Schlüssel und erhöhte Schwellenwerte zur Verwaltung des Lebenszyklus von Kundendaten.

Die [!DNL Adobe Target] und [!DNL Custom Personalization] -Ziele in die [Experience Platform von Datennutzungsbezeichnungen](../data-governance/labels/overview.md) und [Dienst zur Durchsetzung von Einwilligungsrichtlinien](../data-governance/enforcement/overview.md). Diese Funktionen stehen allen Kunden zur Verfügung.




+++

