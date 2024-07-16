---
keywords: Ziele; Fragen; häufig gestellte Fragen; FAQ; Ziele FAQ
title: Häufig gestellte Fragen
description: Antworten auf die am häufigsten gestellten Fragen zu Adobe Experience Platform-Zielen
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 5b37b51308dc2097c05b0e763293467eb12a2f21
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 3%

---

# Häufig gestellte Fragen {#faq}

## Übersicht {#overview}

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Adobe Experience Platform-Zielen. Fragen und Informationen zur Fehlerbehebung bei anderen [!DNL Platform]-Diensten, einschließlich der in allen [!DNL Platform]-APIs aufgetretenen Probleme, finden Sie im [Handbuch zur Fehlerbehebung bei Experience Platform](../landing/troubleshooting.md).

## Allgemeine Fragen zu Zielen {#general}

### Warum werden in der Experience Platform-Benutzeroberfläche und in den exportierten CSV-Dateien unterschiedliche Profilzahlen angezeigt?

+++Antwort
Dies ist ein normales Verhalten aufgrund der Art, wie Experience Platform die Segmentierung durchführt.

Streaming-Segmentierung aktualisiert die Profilanzahl für Streaming-Zielgruppen über den ganzen Tag, während die Batch-Segmentierung die Profilanzahl für Batch-Zielgruppen einmal alle 24 Stunden aktualisiert.

Wenn sich der Zeitplan für den Zielgruppenexport von dem der Segmentierungsplanung unterscheidet, unterscheidet sich die Profilanzahl zwischen der Benutzeroberfläche und der exportierten [!DNL CSV] -Datei, insbesondere im Hinblick auf Streaming-Zielgruppen.

Weitere Informationen finden Sie in der Dokumentation zum [Segmentation Service](../segmentation/home.md) .
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

### Wenn eine Zielgruppe aus einem Ziel entfernt wird: Gibt es ein Signal, das an das Ziel gesendet wird, um anzugeben, dass die Zielgruppe entfernt wurde?

+++Antwort

Nein, es gibt keine Abhängigkeit zwischen dem Experience Platform-Ziel und der Kundeninstanz des Zielsystems. Auf der Empfangsseite ist der einzige Hinweis, den das Zielsystem sehen würde, dass es diese Zielgruppendaten nicht mehr erhält.

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
Bevor Sie Ihre Zielgruppen an [!DNL Facebook] senden können, stellen Sie sicher, dass Sie die folgenden Voraussetzungen erfüllen:

* Für Ihr [!DNL Facebook] -Benutzerkonto muss die Berechtigung **[!DNL Manage campaigns]** für das Werbekonto aktiviert sein, das Sie verwenden möchten.
* Das Geschäftskonto **Adobe Experience Cloud** muss als Werbepartner in Ihrem [!DNL Facebook Ad Account] hinzugefügt werden. Verwenden Sie `business ID=206617933627973`. Weitere Informationen finden Sie unter [Partner zu Ihrem Business Manager hinzufügen](https://www.facebook.com/business/help/1717412048538897) in der Facebook-Dokumentation.

  >[!IMPORTANT]
  >
  > Beim Konfigurieren der Berechtigungen für Adobe Experience Cloud müssen Sie die Berechtigung **Kampagnen verwalten** aktivieren. Dies ist für die [!DNL Adobe Experience Platform]-Integration erforderlich.
* Lesen und unterschreiben Sie die [!DNL Facebook Custom Audiences]-Nutzungsbedingungen. Rufen Sie dazu `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]` auf, wobei `accountID` Ihre [!DNL Facebook Ad Account ID] ist.
+++

### Muss ich meinem [!DNL Facebook] -Advertiser-Konto Apps oder Pixel hinzufügen?

+++Antwort 
Nr. Da es sich hierbei nicht um eine pixelbasierte Integration handelt, müssen Sie Ihrem Advertiser-Konto keine Pixel hinzufügen.
+++

### Wie lange dauert die Verarbeitung von Informationen aus Adobe Experience Platform in Facebook?

+++Antwort
Ab März 2021 benötigt [!DNL Facebook Custom Audiences] bis zu eine Stunde, um die von [!DNL Platform] erhaltenen Informationen zu verarbeiten.
+++

### Kann ich [!DNL Facebook Custom Audiences] für Zielgruppen-Targeting in anderen [!DNL Facebook] -Apps verwenden, z. B. [!DNL Instagram]?

++ + Amswer
Sie können das Ziel [!DNL Facebook Custom Audiences] für Zielgruppen-Targeting in der Facebook-Familie von Apps verwenden, die von [!DNL Facebook Custom Audiences] unterstützt werden, einschließlich [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] und [!DNL Messenger]. Die Auswahl der App, für die Advertiser Kampagnen ausführen möchten, wird auf der Platzierungsebene in [!DNL Facebook Ads Manager] angezeigt.
+++

### Was ist der Unterschied zwischen der Verbindung [!DNL Facebook Custom Audiences] und der Erweiterung [!DNL Facebook Pixel]?

+++Antwort
Die [!DNL Facebook Custom Audiences]-Verbindung verwendet beim Senden von Zielgruppen an [!DNL Facebook] [!DNL Platform] Identitäten, während die [[!DNL Facebook Pixel] Verbindung](../destinations/catalog/advertising/facebook-pixel.md) das in eine Website integrierte [!DNL Facebook]-Pixel verwendet.

Diese beiden Integrationen ergänzen sich. Sie können beide verwenden, um eine bessere Zielgruppenabdeckung sicherzustellen. Beispielsweise können Sie die Erweiterung [!DNL Facebook Pixel] für die Suche nach Website-Besuchern verwenden, die kein Konto erstellt haben, während [!DNL Facebook Custom Audiences] Ihnen dabei helfen kann, bestehende Kunden anhand von [!DNL Platform] -Identitäten anzusprechen.
+++

### Unterstützt die Adobe Experience Platform-Integration mit [!DNL Facebook Custom Audiences] das Deaktivieren von Benutzern aus einer Zielgruppe, wenn sie sich nicht mehr dafür qualifizieren?**

+++Antwort
Ja, die Integration unterstützt das Entfernen von Benutzern aus [!DNL Facebook Custom Audiences], wenn sie sich nicht mehr qualifizieren.
+++

### Wie sollten die Zielgruppendaten gehasht werden, bevor sie an [!DNL Facebook] gesendet werden?

+++Antwort
[!DNL Facebook] erfordert, dass keine personenbezogenen Daten (PII) klar gesendet werden. Daher können die für [!DNL Facebook] aktivierten Zielgruppen aus *Hash*-Identifikatoren wie E-Mail-Adressen oder Telefonnummern abgeleitet werden.

Ausführliche Erklärungen zu den Anforderungen für die ID-Übereinstimmung finden Sie unter [Anforderungen für die ID-Übereinstimmung](catalog/social/facebook.md#id-matching-requirements).
+++

### Welche Identitäten kann ich in [!DNL Facebook Custom Audiences] aktivieren?

+++Antwort
[!DNL Facebook Custom Audiences] unterstützt die Aktivierung der folgenden Identitäten: Hash-E-Mails, Hash-Telefonnummern, [!DNL GAID], [!DNL IDFA] und benutzerdefinierte externe IDs.
+++

### Kann ich mehrere Facebook-Ziele in der Platform-Benutzeroberfläche für separate Facebook-Konten erstellen?

+++Antwort
Ja. Ein Facebook-Ziel in Experience Platform ist 1:1 für ein Anzeigenkonto in Facebook. Sie können für jedes Facebook-Anzeigenkonto in Ihrem Unternehmen ein eigenes Facebook-Ziel erstellen. Folgen Sie dem Tutorial [ zur Zielverbindung](/help/destinations/ui/connect-destination.md) und stellen Sie für jedes neue Facebook-Ziel in der Platform-Benutzeroberfläche eine Verbindung zu einem separaten Facebook-Konto her. Die Anzahl der Facebook-Anzeigenkonten, mit denen Sie eine Verbindung herstellen können, ist unbegrenzt.
+++

## Google Customer Match {#google-customer-match}

### Warum werden beim Exportieren von Zielgruppen in Google-Kundenabgleich am Ende der Zielgruppennamen in der Google-Benutzeroberfläche zusätzliche Zahlen angehängt?

+++Antwort
Google erfordert, dass Zielgruppennamen eindeutig sind. Die angezeigten Zahlen sind [UNIX-Zeitstempel](https://www.unixtimestamp.com/) und werden angehängt, um die eindeutigen Zielgruppennamen beizubehalten, wenn Sie dieselbe Zielgruppe mehreren Google-Zielen zugeordnet haben.
+++

## LinkedIn Matched Audiences {#linkedin}

### Muss ich meinem [!DNL LinkedIn] -Advertiser-Konto Apps oder Pixel hinzufügen?

+++Antwort 
Nr. Da es sich hierbei nicht um eine pixelbasierte Integration handelt, müssen Sie Ihrem Advertiser-Konto keine Pixel hinzufügen.
+++

### Was muss ich tun, bevor ich Zielgruppen in [!DNL LinkedIn Matched Audiences] aktivieren kann?

+++Antwort
Bevor Sie das Ziel [!UICONTROL LinkedIn Matched Audience] verwenden können, stellen Sie sicher, dass Ihr [!DNL LinkedIn Campaign Manager]-Konto über die Berechtigungsebene [!DNL Creative Manager] oder höher verfügt.

Informationen zum Bearbeiten Ihrer [!DNL LinkedIn Campaign Manager] -Benutzerberechtigungen finden Sie unter [Hinzufügen, Bearbeiten und Entfernen von Benutzerberechtigungen für Advertising-Konten](https://www.linkedin.com/help/lms/answer/5753) in der LinkedIn-Dokumentation.
+++

### Wie sollten die Zielgruppendaten gehasht werden, bevor sie an [!DNL LinkedIn] gesendet werden?

+++Antwort
[!DNL LinkedIn] erfordert, dass keine personenbezogenen Daten (PII) klar gesendet werden. Daher können die für [!DNL LinkedIn] aktivierten Zielgruppen aus *Hash*-Identifikatoren wie E-Mail-Adressen oder Telefonnummern abgeleitet werden.

Ausführliche Erklärungen zu den Anforderungen für die ID-Übereinstimmung finden Sie unter [Anforderungen für die ID-Übereinstimmung](catalog/social/linkedin.md#id-matching-requirements).
+++

### Welche Identitäten kann ich in [!DNL LinkedIn] aktivieren?

+++Antwort
[!DNL LinkedIn Matched Audiences] unterstützt die Aktivierung der folgenden Identitäten: gehashte E-Mails, [!DNL GAID] und [!DNL IDFA].

+++

## Personalisierung auf derselben Seite und auf der nächsten Seite über die Adobe Target- und benutzerdefinierten Personalization-Ziele {#same-next-page-personalization}

### Muss ich das Experience Platform Web SDK verwenden, um Zielgruppen und Attribute an Adobe Target zu senden?

+++Antwort
Nein, das [Web SDK](../web-sdk/home.md) ist nicht erforderlich, um Zielgruppen für [Adobe Target](catalog/personalization/adobe-target-connection.md) zu aktivieren.

Wenn jedoch [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html) anstelle des Web SDK verwendet wird, wird nur die Personalisierung der nächsten Sitzung unterstützt.

Für die [ Personalisierung der gleichen Seite und der nächsten Seite](ui/activate-edge-personalization-destinations.md) müssen Sie entweder das [Web SDK](../web-sdk/home.md) oder die [Edge Network Server API](../server-api/overview.md) verwenden. Weitere Informationen zur Implementierung finden Sie in der Dokumentation zum Aktivieren von Zielgruppen für Edge-Ziele ](ui/activate-edge-personalization-destinations.md).[
+++

### Gibt es eine Begrenzung für die Anzahl der Attribute, die ich von Real-time Customer Data Platform an Adobe Target oder ein benutzerspezifisches Personalization-Ziel senden kann?

+++Antwort
Ja, Personalisierungsfälle für die gleiche Seite und die nächste Seite unterstützen maximal 30 Attribute pro Sandbox, wenn Zielgruppen für Adobe Target- oder benutzerdefinierte Personalization-Ziele aktiviert werden. Weitere Informationen zu AktivierungsLimits finden Sie in der [Limits-Dokumentation](guardrails.md#edge-destinations-activation).
+++

### Welche Attributtypen werden für die Aktivierung unterstützt (z. B. Arrays, Maps usw.)?

+++Antwort
Derzeit werden nur statische Attribute mit einem Wert unterstützt, z. B. `person.name.firstName`. Array-Attribute werden derzeit nicht unterstützt.
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### Wie lange dauert es, bis diese Zielgruppe für Anwendungsfälle der Kantensegmentierung verfügbar ist, nachdem ich eine Zielgruppe in Experience Platform erstellt habe?

+++Antwort
Zielgruppendefinitionen werden bis zu einer Stunde an das [Edge Network](../web-sdk/home.md) übertragen. Wenn jedoch innerhalb dieser ersten Stunde eine Zielgruppe aktiviert wird, können einige Besucher verpasst werden, die sich für die Zielgruppe qualifiziert hätten.
+++

### Wo kann ich die aktivierten Attribute in Adobe Target sehen?

+++Antwort
Attribute stehen in Target in [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) - und [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html) -Angeboten zur Verfügung.
+++

### Kann ich ein Ziel ohne Datastream erstellen und dann zu einem späteren Zeitpunkt demselben Ziel einen Datastream hinzufügen?

+++Antwort
Dies wird derzeit nicht über die Benutzeroberfläche &quot;Ziele&quot;unterstützt. Wenn Sie in diesem Fall Hilfe benötigen, wenden Sie sich bitte an Ihren Adobe-Support-Mitarbeiter.
+++

### Was passiert, wenn ich ein Adobe Target-Ziel lösche?

+++Antwort
Wenn Sie ein Ziel löschen, werden alle unter dem Ziel zugeordneten Zielgruppen und Attribute aus Adobe Target gelöscht und auch aus dem Edge Network entfernt.
+++

### Funktioniert die Integration mit der Edge Network Server-API?

+++Antwort
Ja, die Edge Network Server-API funktioniert mit dem benutzerdefinierten Personalization-Ziel. Da Profilattribute möglicherweise vertrauliche Daten enthalten, müssen Sie zum Schutz dieser Daten für das benutzerdefinierte Personalization-Ziel die Edge Network Server-API für die Datenerfassung verwenden. Darüber hinaus müssen alle API-Aufrufe in einem [authentifizierten Kontext](../server-api/authentication.md) erfolgen.
+++

### Ich kann nur eine Zusammenführungsrichtlinie haben, die aktiv ist. Kann ich Zielgruppen erstellen, die eine andere Zusammenführungsrichtlinie verwenden und diese dennoch als Streaming-Zielgruppen an Adobe Target senden?

+++Antwort 
Nr. Alle Zielgruppen, die Sie für Adobe Target aktivieren möchten, müssen eine aktive [Zusammenführungsrichtlinie](../profile/merge-policies/ui-guide.md) verwenden.
+++

### Werden DULE (Data Usage Labeling and Enforcement) und Einverständnisrichtlinien durchgesetzt?

+++Antwort
Ja. Die Aktivierung der ausgewählten Attribute wird von den [Richtlinien für Data Governance und Einverständniserklärung](../data-governance/home.md) gesteuert, die erstellt und mit den ausgewählten Marketing-Aktionen verknüpft wurden.
+++

### Sind die Ziele [!DNL Adobe Target] und [!DNL Custom Personalization] [!DNL HIPAA] kompatibel?

+++Antwort
[!DNL Adobe Target] entspricht nicht [!DNL HIPPA] [[!DNL Adobe Healthcare Shield]](https://business.adobe.com/solutions/industries/healthcare.html). Kunden sollten sich mit ihren eigenen Rechtsabteilungen bezüglich der [!DNL HIPPA]-Bereitschaft für benutzerdefinierte Optimierungskanäle erkundigen, bevor sie die Edge-Personalisierung über [!DNL Adobe Target] oder die [!DNL Custom Personalization] -Ziele verwenden.

Für Anwendungsfälle, in denen die Verwaltung von Einwilligungsrichtlinien skaliert angewendet werden muss, müssen Kunden [!DNL Adobe Privacy & Security Shield] kaufen. [!DNL Adobe Privacy & Security Shield] -Funktionen werden als erweiterte Suite von Funktionen verkauft und möglicherweise nicht separat erworben.

Dieser Dienst umfasst kundenverwaltete Schlüssel und erhöhte Schwellenwerte zur Verwaltung des Lebenszyklus von Kundendaten.

Die Ziele [!DNL Adobe Target] und [!DNL Custom Personalization] sind in die [Experience Platform-Datennutzungsbezeichnungen](../data-governance/labels/overview.md) und den Dienst [Durchsetzung der Einwilligungsrichtlinie](../data-governance/enforcement/overview.md) integriert. Diese Funktionen stehen allen Kunden zur Verfügung.




+++

