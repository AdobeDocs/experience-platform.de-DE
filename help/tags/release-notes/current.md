---
title: Versionshinweise für Tags und Ereignisweiterleitung
description: Die neuesten Versionshinweise für Tags und Ereignisweiterleitung in Adobe Experience Platform.
exl-id: 2ebeaa1e-64b8-48fd-b4e8-419663271a87
source-git-commit: 12648469a1e06e316597fa46fb877f947c8ddb92
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 20%

---

# Versionshinweise für Tags und Ereignisweiterleitung

## 26. Oktober 2022

* **Umgang mit sensiblen Daten für Datastreams**: Datastreams nutzt jetzt verschiedene Platform-Technologien, um sensible Daten, wie sie durch Vorschriften wie den Health Insurance Portability and Accounability Act (HIPAA) durchgesetzt werden, angemessen zu handhaben. Siehe Abschnitt zu [Umgang mit sensiblen Daten in Datenströmen](../../edge/datastreams/overview.md#sensitive) für weitere Informationen.
* **[!DNL Splunk]Erweiterung für die Ereignisweiterleitung**: Sie können jetzt Daten an senden [!DNL Splunk] mit [Ereignisweiterleitung](../ui/event-forwarding/overview.md) -Erweiterung. Siehe [[!DNL Splunk] Erweiterungsübersicht](../extensions/web/splunk/overview.md) für weitere Informationen.
* **[!DNL Zendesk]Erweiterung für die Ereignisweiterleitung**: Sie können jetzt Daten an senden [!DNL Zendesk] mit [Ereignisweiterleitung](../ui/event-forwarding/overview.md) -Erweiterung. Siehe [[!DNL Zendesk] Erweiterungsübersicht](../extensions/web/zendesk/overview.md) für weitere Informationen.

## 28. September 2022

* **Adobe Experience Platform - linke Navigationsintegration**: Alle Funktionen, die zuvor ausschließlich für die Datenerfassungs-Benutzeroberfläche galten (einschließlich Tags und Ereignisweiterleitung), sind jetzt auch über die linke Navigation in der Experience Platform-Benutzeroberfläche unter der Kategorie verfügbar. **[!UICONTROL Datenerfassung]**. Dadurch entfällt die Notwendigkeit, beim Arbeiten mit Datenerfassungsfunktionen in Platform zwischen Benutzeroberflächen zu wechseln.
* **Benutzerzuordnung in Tags und Ereignisweiterleitung**: Bei der Auflistung der verfügbaren Eigenschaften in Tags und der Ereignisweiterleitung zeigt jede aufgelistete Eigenschaft jetzt an, wann sie zuletzt aktualisiert wurde und von wem.
* **[[!DNL Snap Conversions API] Erweiterung](https://exchange.adobe.com/apps/ec/108550) für die Ereignisweiterleitung**: Sie können jetzt Daten an die [!DNL Snapchat Conversions API] mit [Ereignisweiterleitung](../../tags/ui/event-forwarding/overview.md) -Erweiterung. Weitere Informationen zur Authentifizierung und Verwendung der API finden Sie in der [[!DNL Snapchat Marketing API] Dokumentation](https://marketingapi.snapchat.com/docs/conversion.html).

## 27. Juli 2022

* Der Zugriff auf Tags und die Ereignisweiterleitungsfunktionen wird jetzt über Adobe Admin Console unter der Karte für die Adobe Experience Platform-Datenerfassung verwaltet. Weitere Informationen finden Sie im Handbuch zu [Datenerfassungsberechtigungen](../../collection/permissions.md).
* Unterstützung für Internet Explorer 10 und 11 wurde [veraltet](../ie-deprecation.md).

## 22. Juni 2022

Es wurden neue Erweiterungen veröffentlicht:

* [Google Data Layer Tag-Erweiterung](../extensions/web/google-data-layer/overview.md): Ermöglicht die Verwendung einer Google-Datenschicht in Ihrer Tags-Implementierung.
* [Google Ads Enhanced Conversions-Ereignisweiterleitungs-Erweiterung](https://partners.adobe.com/exchangeprogram/experiencecloud/exchange.details.108630.html): Ermöglicht Ihnen, Ihre Google Ads-Konversionen in Echtzeit zu verbessern.
* [Mailchimp-Ereignisweiterleitungserweiterung](../extensions/web/mailchimp/overview.md): Sendet Ereignisse an die Mailchimp Marketing-API, die E-Mails für Mailchimp-Marketingkampagnen, Journey oder Transaktionen an Trigger weiterleiten kann.
