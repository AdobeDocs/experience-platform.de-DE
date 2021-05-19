---
keywords: Bestimmungsorte; Fragen; häufig gestellte Fragen; faq; Ziel-FAQ
title: Häufig gestellte Fragen zu Zielen
seo-title: Häufig gestellte Fragen zu Zielen
description: Antworten auf die am häufigsten gestellten Fragen zu Adobe Experience Platform Destinationen
seo-description: Antworten auf die am häufigsten gestellten Fragen zu Adobe Experience Platform Destinationen
source-git-commit: 61678c5a62980cdb81714420016b7c4b2093f5c6
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 12%

---


# Häufig gestellte Fragen zu Zielen {#faq}

## [!DNL Facebook Custom Audiences] {#facebook-faq}

**Was muss ich tun, bevor ich Audiencen aktivieren kann  [!DNL Facebook Custom Audiences]?**

Bevor Sie Zielgruppensegmente an [!DNL Facebook] senden können, müssen Sie sicherstellen, dass Sie die folgenden Voraussetzungen erfüllen:

* Für Ihr [!DNL Facebook]-Benutzerkonto muss die **[!DNL Manage campaigns]**-Berechtigung für das Anzeigenkonto aktiviert sein, das Sie verwenden möchten.
* Das Geschäftskonto **Adobe Experience Cloud** muss als Werbepartner in Ihrem [!DNL Facebook Ad Account] hinzugefügt werden. Verwenden Sie `business ID=206617933627973`. Weitere Informationen finden Sie unter [Hinzufügen Partner für Ihren Business Manager](https://www.facebook.com/business/help/1717412048538897) in der Facebook-Dokumentation.
   >[!IMPORTANT]
   >
   > Beim Konfigurieren der Berechtigungen für Adobe Experience Cloud müssen Sie die Berechtigung **Kampagnen verwalten** aktivieren. Dies ist für die [!DNL Adobe Experience Platform]-Integration erforderlich.
* Lesen und unterschreiben Sie die [!DNL Facebook Custom Audiences]-Nutzungsbedingungen. Rufen Sie dazu `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]` auf, wobei `accountID` Ihre [!DNL Facebook Ad Account ID] ist.

**Muss ich meinem  [!DNL Facebook] Advertiser-Konto Apps oder Pixel hinzufügen?**

Nein. Da es sich hierbei nicht um eine pixelbasierte Integration handelt, müssen Sie Ihrem Advertiser-Konto keine Pixel hinzufügen.

**Wie lange dauert die Verarbeitung von Informationen aus Adobe Experience Platform durch Facebook?**

Ab März 2021 benötigt [!DNL Facebook Custom Audiences] bis zu einer Stunde, um die von [!DNL Platform] erhaltenen Informationen zu verarbeiten.

**Kann ich das Targeting  [!DNL Facebook Custom Audiences] für Audiencen in anderen  [!DNL Facebook] Apps verwenden, z. B.  [!DNL Instagram]?**

Sie können das [!DNL Facebook Custom Audiences]-Ziel für Audience-Targeting in Facebooks Anwendungsfamilie verwenden, die von [!DNL Facebook Custom Audiences] unterstützt wird, einschließlich [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] und [!DNL Messenger]. Die Auswahl der App, auf der Werbetreibende Kampagnen ausführen möchten, wird auf Platzierungsebene in [!DNL Facebook Ads Manager] angezeigt.

**Was ist der Unterschied zwischen  [!DNL Facebook Custom Audiences] Verbindung und  [!DNL Facebook Pixel] Erweiterung?**

Die [!DNL Facebook Custom Audiences]-Verbindung verwendet beim Senden von Audiencen an [!DNL Facebook] die [[!DNL Facebook Pixel] connection](../destinations/catalog/advertising/facebook-pixel.md)-ID, während [!DNL Facebook] das in eine Website integrierte [!DNL Platform]-Pixel verwendet.

Diese beiden Integrationen ergänzen sich. Sie können beide verwenden, um eine bessere Zielgruppenabdeckung sicherzustellen. Beispielsweise können Sie die Erweiterung [!DNL Facebook Pixel] zum Aufsuchen von Website-Besuchern verwenden, die noch kein Konto erstellt haben, während [!DNL Facebook Custom Audiences] Ihnen dabei helfen kann, bestehende Kunden anhand von [!DNL Platform]-Identitäten Zielgruppe.

**Ist die Adobe Experience Platform-Integration mit  [!DNL Facebook Custom Audiences] Support geeignet, Benutzer von einer Audience zu disqualifizieren, wenn sie sich nicht mehr dafür qualifizieren?**

Ja, die Integration unterstützt das Entfernen von Benutzern aus [!DNL Facebook Custom Audiences], wenn sie sich nicht mehr qualifizieren.

**Wie sollte ich die Daten der Audience vor dem Senden an  [!DNL Facebook]ein Hash senden?**

[!DNL Facebook] verlangt, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher können die für [!DNL Facebook] aktivierten Audiencen anhand von *Hash*-IDs wie E-Mail-Adressen oder Telefonnummern ausgewertet werden.

Ausführliche Erläuterungen zu den Anforderungen für die ID-Übereinstimmung finden Sie unter [Anforderungen für die ID-Übereinstimmung](catalog/social/facebook.md#id-matching-requirements).

**In welcher Art von Identitäten kann ich aktivieren  [!DNL Facebook Custom Audiences]?**

[!DNL Facebook Custom Audiences] unterstützt die Aktivierung der folgenden Identitäten: Hash-E-Mails, Hash-Telefonnummern,  [!DNL GAID] [!DNL IDFA]und benutzerdefinierte externe IDs.

## linkedIn-übereinstimmende Audiencen {#linkedin}

**Muss ich meinem  [!DNL LinkedIn] Advertiser-Konto Apps oder Pixel hinzufügen?**

Nein. Da es sich hierbei nicht um eine pixelbasierte Integration handelt, müssen Sie Ihrem Advertiser-Konto keine Pixel hinzufügen.

**Was muss ich tun, bevor ich Audiencen aktivieren kann  [!DNL LinkedIn Matched Audiences]?**

Bevor Sie das [!UICONTROL LinkedIn Matched Audience]-Ziel verwenden können, stellen Sie sicher, dass Ihr [!DNL LinkedIn Campaign Manager]-Konto das Berechtigungsniveau [!DNL Creative Manager] oder höher aufweist.

Informationen zum Bearbeiten Ihrer [!DNL LinkedIn Campaign Manager]-Benutzerberechtigungen finden Sie unter [Hinzufügen, Bearbeiten und Entfernen von Benutzerberechtigungen für Werbekonten](https://www.linkedin.com/help/lms/answer/5753) in der LinkedIn-Dokumentation.

**Wie sollte ich die Daten der Audience vor dem Senden an  [!DNL LinkedIn]ein Hash senden?**

[!DNL LinkedIn] verlangt, dass keine personenbezogenen Daten (PII) klar übermittelt werden. Daher können die für [!DNL LinkedIn] aktivierten Audiencen anhand von *Hash*-IDs wie E-Mail-Adressen oder Telefonnummern ausgewertet werden.

Ausführliche Erläuterungen zu den Anforderungen für die ID-Übereinstimmung finden Sie unter [Anforderungen für die ID-Übereinstimmung](catalog/social/linkedin.md#id-matching-requirements).

**In welcher Art von Identitäten kann ich aktivieren  [!DNL LinkedIn]?**

[!DNL LinkedIn Matched Audiences] unterstützt die Aktivierung der folgenden Identitäten: E-Mails mit Hashing  [!DNL GAID]und  [!DNL IDFA].
