---
title: Versionshinweise für Tags und Ereignisweiterleitung
description: Die neuesten Versionshinweise für Tags und Ereignisweiterleitung in Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: 3ebf8df16f88660eab481bd0a0ba88816b470255
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 70%

---

# Versionshinweise für Tags und Ereignisweiterleitung

## 29. März 2023

**Schnellstartarbeitsabläufe (Beta)**

Greifen Sie über den Startseite der Datenerfassung auf neue Schnellstartarbeitsabläufe unter &quot;Erste Schritte&quot;zu! Die folgenden Workflows stehen Kunden jetzt als öffentliche Betaversion zur Verfügung.
* **[Meta Conversions-API](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/meta/overview.html?lang=en#quick-start)**: Kunden mit Ereignisweiterleitung können Ereignisdaten schnell erfassen und serverseitig an Meta weiterleiten, um Anzeigenkonversionen in nur wenigen einfachen Schritten zu ermöglichen.
* **[Mobile SDK](https://developer.adobe.com/client-sdks/documentation/)**: Kunden können das Mobile SDK schnell implementieren und einfache mobile Ereignisse in nur wenigen einfachen Schritten validieren.

Es wurden neue Erweiterungen veröffentlicht:

* **[!DNL Braze]Ereignisweiterleitungs-Erweiterung**: Die [[!DNL Braze Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) Mit der Ereignisweiterleitungs-Erweiterung können Sie die im Adobe Experience Platform Edge Network erfassten Daten nutzen und an senden. [!DNL Braze] in Form von serverseitigen Ereignissen, bei denen die [!DNL Braze] APIs für die Benutzerverfolgung.
* **[Epsilon Events API] Ereignisweiterleitungs-Erweiterung**: Die [[!DNL Epsilon Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) Mit der -Erweiterung können Sie die Ereignisweiterleitung nutzen, um Ereignisinformationen im Adobe Experience Platform Edge Network zu erfassen und an zu senden. [!DNL Epsilon] mithilfe der [!DNL Epsilon] Ereignis-API.
* **[!DNL Mixpanel]Ereignisweiterleitungs-Erweiterung**: Die [[!DNL Mixpanel Track Events API]](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/server/braze/overview.html) Mit der -Erweiterung können Sie die Ereignisweiterleitung nutzen, um Ereignisinformationen im Adobe Experience Platform Edge Network zu erfassen und an zu senden. [!DNL Mixpanel] Verwendung der Tracking-Events-API.

## 25. Januar 2023

* **Neuer Startbildschirm**: Die Startseite der Datenerfassungs-Benutzeroberfläche wurde aktualisiert und enthält jetzt hilfreiche Onboarding-Informationen und Links zur Optimierung der Produktivität. Dazu gehören:
   1. Dokumentation und empfohlene Workflows für die ersten Schritte
   1. Aktuelle Eigenschaften, Regeln und Datenelemente
   1. Beliebte Erweiterungen
   1. Neue Erweiterungsaktualisierungen mit Schnellinstallationsfunktion
* **Datenversand an [!DNL Google Ads] mittels Ereignisweiterleitung**: Sie können jetzt die [[!DNL Google Ads Enhanced Conversions] API-Erweiterung](../extensions/server/google-ads-enhanced-conversions/overview.md) für die Ereignisweiterleitung in Kombination mit [Google Oauth 2-Geheimnissen](../ui/event-forwarding/secrets.md#google-oauth2) verwenden, um Server-seitige Daten sicher und in Echtzeit an [!DNL Google Ads] zu senden.

## 23. November 2022

* **[!DNL AWS]-Erweiterung für die Ereignisweiterleitung**: Sie können jetzt Daten an [!DNL Amazon Web Services] ([!DNL AWS]) senden, indem Sie eine Erweiterung für die [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) verwenden. Weiterführende Informationen dazu finden Sie in der [[!DNL AWS] Übersicht der Erweiterungen](../../tags/extensions/server/aws/overview.md).
* **[!DNL Google Ads Enhanced Conversions]-Erweiterung für die Ereignisweiterleitung**: Sie können jetzt Konversionsdaten an [!DNL Google Ads] senden, indem Sie eine Erweiterung für die [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) verwenden. Weiterführende Informationen dazu finden Sie in der [[!DNL Google Ads Enhanced Conversions] Übersicht der Erweiterungen](../../tags/extensions/server/google-ads-enhanced-conversions/overview.md).
* **[!DNL Microsoft Azure]-Erweiterung für die Ereignisweiterleitung**: Sie können jetzt Daten an [!DNL Microsoft Azure] senden, indem Sie eine Erweiterung für die [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) verwenden. Weiterführende Informationen dazu finden Sie in der [[!DNL Microsoft Azure] Übersicht der Erweiterungen](../../tags/extensions/server/azure/overview.md).

## 26. Oktober 2022

* **Behandlung sensibler Daten für Datenströme**: Datenströme nutzen jetzt mehrere Platform-Technologien, um sensible Daten entsprechend den Vorschriften wie dem Health Insurance Portability and Accountability Act (HIPAA) zu behandeln. Weitere Informationen finden Sie im Abschnitt [Umgang mit sensiblen Daten in Datenströmen](../../edge/datastreams/overview.md#sensitive).
* **[!DNL Splunk]-Erweiterung für die Ereignisweiterleitung**: Sie können jetzt Daten an [!DNL Splunk] senden, indem Sie eine Erweiterung für die [Ereignisweiterleitung](../ui/event-forwarding/overview.md) verwenden. Weiterführende Informationen dazu finden Sie in der [[!DNL Splunk] Übersicht der Erweiterungen](../extensions/server/splunk/overview.md).
* **[!DNL Zendesk]-Erweiterung für die Ereignisweiterleitung**: Sie können jetzt Daten an [!DNL Zendesk] senden, indem Sie eine Erweiterung für die [Ereignisweiterleitung](../ui/event-forwarding/overview.md) verwenden. Weiterführende Informationen dazu finden Sie in der [[!DNL Zendesk] Übersicht der Erweiterungen](../extensions/server/zendesk/overview.md).

## 28. September 2022

* **Integration der linken Navigationsleiste von Adobe Experience Platform**: Alle Funktionen, die bisher ausschließlich in der Datenerfassungs-Benutzeroberfläche verfügbar waren (einschließlich Tags und Ereignisweiterleitung), sind jetzt auch über die linke Navigation in der Benutzeroberfläche von Experience Platform verfügbar, und zwar unter der Kategorie **[!UICONTROL Datensammlung]**. Dadurch entfällt die Notwendigkeit, beim Arbeiten mit Datenerfassungsfunktionen in Platform zwischen Benutzeroberflächen zu wechseln.
* **Benutzerzuordnung in Tags und Ereignisweiterleitung**: Bei der Auflistung der verfügbaren Eigenschaften in Tags und Ereignisweiterleitung wird jetzt für jede aufgeführte Eigenschaft angezeigt, wann und von wem sie zuletzt aktualisiert wurde.
* **[[!DNL Snap Conversions API] Erweiterung](https://exchange.adobe.com/apps/ec/108550) für die Ereignisweiterleitung**: Sie können jetzt mit einer Erweiterung für die [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) Daten an [!DNL Snapchat Conversions API] senden. Weitere Informationen zur Authentifizierung und Verwendung der API finden Sie in der [[!DNL Snapchat Marketing API] Dokumentation](https://marketingapi.snapchat.com/docs/conversion.html).

## 27. Juli 2022

* Der Zugriff auf Tags und Ereignisweiterleitungsfunktionen wird jetzt über die Adobe Admin Console unter der Karte für Adobe Experience Platform Datenerfassung verwaltet. Weitere Informationen finden Sie im Handbuch zu [Datenerfassungsberechtigungen](../../collection/permissions.md).
* Die Unterstützung für Internet Explorer 10 und 11 wurde [eingestellt](../ie-deprecation.md).

## 22. Juni 2022

Es wurden neue Erweiterungen veröffentlicht:

* [Google-Datenschicht-Tag-Erweiterung](../extensions/client/google-data-layer/overview.md): Ermöglicht es Ihnen, eine Google-Datenschicht in Ihrer Tag-Implementierung zu verwenden.
* [Erweiterung für Ereignisweiterleitung mit Google Ads Enhanced Conversions](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): Ermöglicht es Ihnen, Ihre Google Ads Conversions in Echtzeit zu verbessern.
* [Mailchimp-Ereignisweiterleitung](../extensions/server/mailchimp/overview.md): Sendet Ereignisse an die Mailchimp Marketing-API, die E-Mails für Mailchimp-Marketingkampagnen, Journeys oder Transaktionen auslösen können.