---
keywords: Bestimmungsländer; Fragen; häufig gestellte Fragen; faq; Ziele-FAQ
title: Häufig gestellte Fragen
seo-title: Frequently asked questions
description: Antworten auf die am häufigsten gestellten Fragen zu Adobe Experience Platform-Zielen
seo-description: Answers to the most frequently asked questions about Adobe Experience Platform destinations
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: b2636377eda6740dceb9bc07fbcc082b85ff3c94
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 9%

---

# Häufig gestellte Fragen {#faq}

## Übersicht {#overview}

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Adobe Experience Platform-Zielen. Für Fragen und Fehlerbehebung im Zusammenhang mit anderen [!DNL Platform] Dienste, einschließlich der in allen [!DNL Platform] APIs, siehe [Handbuch zur Fehlerbehebung bei Experience Platformen](../landing/troubleshooting.md).

## Allgemeine Fragen zu Zielen {#general}

**Warum werden in der Experience Platform-Benutzeroberfläche und in den exportierten CSV-Dateien unterschiedliche Profilzahlen angezeigt?**

Dies ist ein normales Verhalten aufgrund der Art und Weise, wie Experience Platform die Segmentierung durchführt.

Streaming-Segmentierung aktualisiert die Profilanzahl für Streaming-Segmente über den ganzen Tag, während die Batch-Segmentierung die Profilanzahl für Batch-Segmente einmal alle 24 Stunden aktualisiert.

Wenn der Segmentexportzeitplan vom Segmentierungsplan abweicht, zählt das Profil zwischen der Benutzeroberfläche und dem exportierten [!DNL CSV] -Datei anders aussehen, insbesondere wenn es um Streaming-Segmente geht.

Siehe [Dokumentation zum Segmentierungsdienst](../segmentation/home.md) für weitere Details.

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**Was muss ich tun, bevor ich Zielgruppen in aktivieren kann? [!DNL Facebook Custom Audiences]?**

Bevor Sie Zielgruppensegmente an [!DNL Facebook] senden können, müssen Sie sicherstellen, dass Sie die folgenden Voraussetzungen erfüllen:

* Ihre [!DNL Facebook] Das Benutzerkonto muss über Folgendes verfügen: **[!DNL Manage campaigns]** -Berechtigung für das Werbekonto aktiviert wurde, das Sie verwenden möchten.
* Die **Adobe Experience Cloud** Geschäftskonto muss als Werbepartner in Ihrem [!DNL Facebook Ad Account]. Verwenden Sie `business ID=206617933627973`. Siehe [Partner zu Ihrem Business Manager hinzufügen](https://www.facebook.com/business/help/1717412048538897) in der Dokumentation zu Facebook .
   >[!IMPORTANT]
   >
   > Beim Konfigurieren der Berechtigungen für Adobe Experience Cloud müssen Sie die Berechtigung **Kampagnen verwalten** aktivieren. Dies ist für die [!DNL Adobe Experience Platform]-Integration erforderlich.
* Lesen und unterschreiben Sie die [!DNL Facebook Custom Audiences]-Nutzungsbedingungen. Rufen Sie dazu `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]` auf, wobei `accountID` Ihre [!DNL Facebook Ad Account ID] ist.

**Muss ich irgendwelche Apps oder Pixel zu meiner [!DNL Facebook] Advertiser-Konto?**

Nein. Da es sich hierbei nicht um eine pixelbasierte Integration handelt, müssen Sie Ihrem Advertiser-Konto keine Pixel hinzufügen.

**Wie lange dauert die Verarbeitung von Informationen aus Adobe Experience Platform in Facebook?**

Seit März 2021 [!DNL Facebook Custom Audiences] benötigt bis zu eine Stunde, um die von erhaltenen Informationen zu verarbeiten [!DNL Platform].

**Kann ich [!DNL Facebook Custom Audiences] für Zielgruppen-Targeting in anderen [!DNL Facebook] Apps, wie [!DNL Instagram]?**

Sie können die [!DNL Facebook Custom Audiences] Ziel für Zielgruppen-Targeting in der Facebook-Familie von Apps, die von [!DNL Facebook Custom Audiences], einschließlich [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network]und [!DNL Messenger]. Die Auswahl der App, für die Advertiser Kampagnen ausführen möchten, wird auf der Platzierungsebene in [!DNL Facebook Ads Manager].

**Was ist der Unterschied zwischen dem [!DNL Facebook Custom Audiences] Verbindung und [!DNL Facebook Pixel] Erweiterung?**

Die [!DNL Facebook Custom Audiences] Verbindungsnutzungen [!DNL Platform] Identitäten beim Senden von Zielgruppen an [!DNL Facebook], während die [[!DNL Facebook Pixel] connection](../destinations/catalog/advertising/facebook-pixel.md) verwendet die [!DNL Facebook] in eine Website integriert ist.

Diese beiden Integrationen ergänzen sich. Sie können beide verwenden, um eine bessere Zielgruppenabdeckung sicherzustellen. Als Beispiel können Sie die [!DNL Facebook Pixel] Erweiterung für die Suche nach Website-Besuchern, die kein Konto erstellt haben, während [!DNL Facebook Custom Audiences] können Ihnen dabei helfen, bestehende Kunden auf Basis von [!DNL Platform] Identitäten.

**Ist die Adobe Experience Platform-Integration mit [!DNL Facebook Custom Audiences] Unterstützung der Nichtqualifizierung von Benutzern von einer Zielgruppe, wenn sie sich nicht mehr dafür qualifizieren?**

Ja, die Integration unterstützt das Entfernen von Benutzern aus [!DNL Facebook Custom Audiences] wenn sie sich nicht mehr qualifizieren.

**Wie sollen die Zielgruppendaten gehasht werden, bevor sie an gesendet werden? [!DNL Facebook]?**

[!DNL Facebook] erfordert, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher werden die Zielgruppen für [!DNL Facebook] kann deaktiviert werden *Hash* Kennungen wie E-Mail-Adressen oder Telefonnummern.

Detaillierte Erläuterungen zu den Anforderungen an die ID-Zuordnung finden Sie unter [Anforderungen an die ID-Übereinstimmung](catalog/social/facebook.md#id-matching-requirements).

**Welche Identitäten kann ich aktivieren? [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] unterstützt die Aktivierung der folgenden Identitäten: Hash-E-Mails, Hash-Telefonnummern, [!DNL GAID], [!DNL IDFA]und benutzerdefinierte externe IDs.

**Kann ich mehrere Facebook-Ziele in der Platform-Benutzeroberfläche für separate Facebook-Konten erstellen?**

Ja. Ein Facebook-Ziel in Experience Platform ist 1:1 für ein Anzeigenkonto in Facebook. Sie können für jedes Facebook-Anzeigenkonto in Ihrem Unternehmen ein eigenes Facebook-Ziel erstellen. Befolgen Sie die [Tutorial zur Zielverbindung](/help/destinations/ui/connect-destination.md) und eine Verbindung zu einem separaten Facebook-Konto für jedes neue Facebook-Ziel in der Platform-Benutzeroberfläche herstellen. Die Anzahl der Facebook-Anzeigenkonten, mit denen Sie eine Verbindung herstellen können, ist unbegrenzt.

## Google-Kundenabgleich {#google-customer-match}

**Warum werden beim Exportieren von Segmenten in Google-Kundenabgleich am Ende der Segmentnamen in der Google-Benutzeroberfläche zusätzliche Zahlen angehängt?**

Google erfordert, dass Segmentnamen eindeutig sind. Die Zahlen, die Sie sehen, sind [UNIX-Zeitstempel](https://www.unixtimestamp.com/) und sie werden angehängt, um die Segmentnamen eindeutig zu halten, wenn Sie dasselbe Segment mehreren Google-Zielen zugeordnet haben.

## linkedIn Matched Audiences {#linkedin}

**Muss ich irgendwelche Apps oder Pixel zu meiner [!DNL LinkedIn] Advertiser-Konto?**

Nein. Da es sich hierbei nicht um eine pixelbasierte Integration handelt, müssen Sie Ihrem Advertiser-Konto keine Pixel hinzufügen.

**Was muss ich tun, bevor ich Zielgruppen in aktivieren kann? [!DNL LinkedIn Matched Audiences]?**

Bevor Sie die [!UICONTROL linkedIn Match Audience] Ziel, stellen Sie sicher, dass Ihre [!DNL LinkedIn Campaign Manager] -Konto hat [!DNL Creative Manager] Berechtigungsebene oder höher.

Informationen zum Bearbeiten Ihrer [!DNL LinkedIn Campaign Manager] Benutzerberechtigungen, siehe [Hinzufügen, Bearbeiten und Entfernen von Benutzerberechtigungen für Werbekonten](https://www.linkedin.com/help/lms/answer/5753) in der LinkedIn-Dokumentation.

**Wie sollen die Zielgruppendaten gehasht werden, bevor sie an gesendet werden? [!DNL LinkedIn]?**

[!DNL LinkedIn] erfordert, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher werden die Zielgruppen für [!DNL LinkedIn] kann deaktiviert werden *Hash* Kennungen wie E-Mail-Adressen oder Telefonnummern.

Detaillierte Erläuterungen zu den Anforderungen an die ID-Zuordnung finden Sie unter [Anforderungen an die ID-Übereinstimmung](catalog/social/linkedin.md#id-matching-requirements).

**Welche Identitäten kann ich aktivieren? [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] unterstützt die Aktivierung der folgenden Identitäten: gehashte E-Mails, [!DNL GAID]und [!DNL IDFA].
