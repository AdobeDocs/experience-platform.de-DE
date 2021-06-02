---
keywords: Bestimmungsländer; Fragen; häufig gestellte Fragen; faq; Ziele-FAQ
title: Häufig gestellte Fragen
seo-title: Häufig gestellte Fragen
description: Antworten auf die am häufigsten gestellten Fragen zu Adobe Experience Platform-Zielen
seo-description: Antworten auf die am häufigsten gestellten Fragen zu Adobe Experience Platform-Zielen
source-git-commit: a01b53758f4ad42272c39f71a08021d30900e7af
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 11%

---


# Häufig gestellte Fragen {#faq}

## Übersicht {#overview}

Dieses Dokument enthält Antworten auf häufig gestellte Fragen zu Adobe Experience Platform-Zielen. Fragen und Antworten zur Fehlerbehebung bei anderen [!DNL Platform]-Diensten, einschließlich der bei allen [!DNL Platform]-APIs aufgetretenen Probleme, finden Sie im [Handbuch zur Fehlerbehebung bei Experience Platformen](../landing/troubleshooting.md).

## Allgemeine Fragen zu Zielen {#general}

**Warum werden in der Experience Platform-Benutzeroberfläche und in den exportierten CSV-Dateien unterschiedliche Profilzahlen angezeigt?**

Dies ist ein normales Verhalten aufgrund der Art und Weise, wie Experience Platform die Segmentierung durchführt.

Streaming-Segmentierung aktualisiert die Profilanzahl für Streaming-Segmente über den ganzen Tag, während die Batch-Segmentierung die Profilanzahl für Batch-Segmente einmal alle 24 Stunden aktualisiert.

Wenn sich der Zeitplan für den Segmentexport von dem der Segmentierungsplanung unterscheidet, unterscheiden sich die Profilzahlen zwischen der Benutzeroberfläche und der exportierten [!DNL CSV]-Datei, insbesondere bei Streaming-Segmenten.

Weitere Informationen finden Sie in der [Dokumentation zum Segmentation Service](../segmentation/home.md).

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**Was muss ich tun, bevor ich Zielgruppen in aktivieren kann  [!DNL Facebook Custom Audiences]?**

Bevor Sie Zielgruppensegmente an [!DNL Facebook] senden können, müssen Sie sicherstellen, dass Sie die folgenden Voraussetzungen erfüllen:

* Für Ihr [!DNL Facebook]-Benutzerkonto muss die **[!DNL Manage campaigns]**-Berechtigung für das Werbekonto aktiviert sein, das Sie verwenden möchten.
* Das Geschäftskonto **Adobe Experience Cloud** muss in Ihrem [!DNL Facebook Ad Account] als Werbepartner hinzugefügt werden. Verwenden Sie `business ID=206617933627973`. Weitere Informationen finden Sie unter [Partner zu Ihrem Business Manager hinzufügen](https://www.facebook.com/business/help/1717412048538897) in der Facebook-Dokumentation.
   >[!IMPORTANT]
   >
   > Beim Konfigurieren der Berechtigungen für Adobe Experience Cloud müssen Sie die Berechtigung **Kampagnen verwalten** aktivieren. Dies ist für die [!DNL Adobe Experience Platform]-Integration erforderlich.
* Lesen und unterschreiben Sie die [!DNL Facebook Custom Audiences]-Nutzungsbedingungen. Rufen Sie dazu `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]` auf, wobei `accountID` Ihre [!DNL Facebook Ad Account ID] ist.

**Muss ich meinem  [!DNL Facebook] Advertiser-Konto Apps oder Pixel hinzufügen?**

Nein. Da es sich hierbei nicht um eine pixelbasierte Integration handelt, müssen Sie Ihrem Advertiser-Konto keine Pixel hinzufügen.

**Wie lange dauert die Verarbeitung von Informationen aus Adobe Experience Platform in Facebook?**

Ab März 2021 benötigt [!DNL Facebook Custom Audiences] bis zu eine Stunde, um Informationen zu verarbeiten, die von [!DNL Platform] empfangen wurden.

**Kann ich  [!DNL Facebook Custom Audiences] für Zielgruppen-Targeting in anderen  [!DNL Facebook] Apps verwenden, z. B.  [!DNL Instagram]?**

Sie können das [!DNL Facebook Custom Audiences]-Ziel für Zielgruppen-Targeting in der Facebook-Familie von Apps verwenden, die von [!DNL Facebook Custom Audiences] unterstützt werden, einschließlich [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] und [!DNL Messenger]. Die Auswahl der App, für die Advertiser Kampagnen ausführen möchten, wird auf der Platzierungsebene in [!DNL Facebook Ads Manager] angezeigt.

**Was ist der Unterschied zwischen der  [!DNL Facebook Custom Audiences] Verbindung und der  [!DNL Facebook Pixel] Erweiterung?**

Die Verbindung [!DNL Facebook Custom Audiences] verwendet beim Senden von Zielgruppen an [!DNL Facebook] [!DNL Platform] Identitäten, während die [[!DNL Facebook Pixel] Verbindung](../destinations/catalog/advertising/facebook-pixel.md) das in eine Website integrierte [!DNL Facebook]-Pixel verwendet.

Diese beiden Integrationen ergänzen sich. Sie können beide verwenden, um eine bessere Zielgruppenabdeckung sicherzustellen. Beispielsweise können Sie die [!DNL Facebook Pixel]-Erweiterung zum Anzeigen von Website-Besuchern verwenden, die kein Konto erstellt haben, während [!DNL Facebook Custom Audiences] Ihnen dabei helfen kann, bestehende Kunden anhand von [!DNL Platform]-Identitäten anzusprechen.

**Unterstützt die Adobe Experience Platform-Integration die  [!DNL Facebook Custom Audiences] Deaktivierung von Benutzern aus einer Zielgruppe, wenn diese sich nicht mehr dafür qualifizieren?**

Ja, die Integration unterstützt das Entfernen von Benutzern aus [!DNL Facebook Custom Audiences], wenn sie sich nicht mehr qualifizieren.

**Wie sollten die Zielgruppendaten gehasht werden, bevor sie an  [!DNL Facebook]gesendet werden?**

[!DNL Facebook] erfordert, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher können die für [!DNL Facebook] aktivierten Zielgruppen von *Hash*-Identifikatoren wie E-Mail-Adressen oder Telefonnummern abgeleitet werden.

Ausführliche Erklärungen zu den Anforderungen für die ID-Zuordnung finden Sie unter [Anforderungen für die ID-Zuordnung](catalog/social/facebook.md#id-matching-requirements).

**In welcher Art von Identitäten kann ich  [!DNL Facebook Custom Audiences]aktivieren?**

[!DNL Facebook Custom Audiences] unterstützt die Aktivierung der folgenden Identitäten: Hash-E-Mails, Hash-Telefonnummern  [!DNL GAID],  [!DNL IDFA]und benutzerdefinierte externe IDs.

## linkedIn Matched Audiences {#linkedin}

**Muss ich meinem  [!DNL LinkedIn] Advertiser-Konto Apps oder Pixel hinzufügen?**

Nein. Da es sich hierbei nicht um eine pixelbasierte Integration handelt, müssen Sie Ihrem Advertiser-Konto keine Pixel hinzufügen.

**Was muss ich tun, bevor ich Zielgruppen in aktivieren kann  [!DNL LinkedIn Matched Audiences]?**

Bevor Sie das Ziel [!UICONTROL LinkedIn Matched Audience] verwenden können, stellen Sie sicher, dass Ihr [!DNL LinkedIn Campaign Manager]-Konto über die Berechtigungsebene [!DNL Creative Manager] oder höher verfügt.

Informationen zum Bearbeiten Ihrer [!DNL LinkedIn Campaign Manager]-Benutzerberechtigungen finden Sie unter [Hinzufügen, Bearbeiten und Entfernen von Benutzerberechtigungen für Werbekonten](https://www.linkedin.com/help/lms/answer/5753) in der LinkedIn-Dokumentation.

**Wie sollten die Zielgruppendaten gehasht werden, bevor sie an  [!DNL LinkedIn]gesendet werden?**

[!DNL LinkedIn] erfordert, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher können die für [!DNL LinkedIn] aktivierten Zielgruppen von *Hash*-Identifikatoren wie E-Mail-Adressen oder Telefonnummern abgeleitet werden.

Ausführliche Erklärungen zu den Anforderungen für die ID-Zuordnung finden Sie unter [Anforderungen für die ID-Zuordnung](catalog/social/linkedin.md#id-matching-requirements).

**In welcher Art von Identitäten kann ich  [!DNL LinkedIn]aktivieren?**

[!DNL LinkedIn Matched Audiences] unterstützt die Aktivierung der folgenden Identitäten: gehashte E-Mails,  [!DNL GAID]und  [!DNL IDFA].
