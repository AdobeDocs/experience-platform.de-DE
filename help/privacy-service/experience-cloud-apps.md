---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Privacy Service und Experience Cloud-Anwendungen
topic: overview
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 25%

---


# [!DNL Privacy Service] und [!DNL Experience Cloud] Anwendungen

Adobe Experience Platform [!DNL Privacy Service] unterstützt Datenschutzanforderungen für mehrere Adobe Experience Cloud-Anwendungen. Jede Anwendung unterstützt verschiedene Produktwerte und IDs zur Identifizierung von Datensubjekten.

Dieses Dokument dient als Referenz für die [!DNL Experience Cloud] Anwendungsdokumentation, in der beschrieben wird, wie Sie diese Anwendung für datenschutzbezogene Vorgänge konfigurieren. Dazu gehört auch die Formatierung und Beschriftung Ihrer Daten. Es werden zwei Kategorien von Anträgen behandelt:

* [In Privacy Service](#integrated)integrierte Anwendungen: Anwendungen, an die Zugriffsanfragen gesendet, gelöscht oder Abmeldeanfragen gesendet werden können [!DNL Privacy Service].
* [Selbstbedienungsanwendungen](#self-serve): Anwendungen, die ihre Datenschutzanforderungen intern verwalten müssen und nicht mit [!DNL Privacy Service] direkt kommunizieren können.

Lesen Sie die Dokumentation für Ihre [!DNL Experience Cloud] Anwendungen, um zu erfahren, wie Sie Ihre Datenschutzanforderungen formatieren und welche Werte für diese Anforderungen unterstützt werden.

## In [!DNL Privacy Service] {#integrated}

Im Folgenden finden Sie eine Liste von [!DNL Experience Cloud] Anwendungen, mit denen [!DNL Privacy Service]die [!DNL Privacy Service] Funktionen, mit denen sie kompatibel sind, integriert sind, sowie Links zur Dokumentation für weitere Informationen.

| Anwendung | Zugriff/Löschen | Ausschluss vom Verkauf | Dokumentation und Überlegungen |
--- | :---: | :---: | ---
| Adobe Advertising Cloud | ✓ | ✓ | <ul><li>[Dokumentation aufrufen/löschen](https://docs.adobe.com/content/help/en/advertising-cloud/all/privacy/ad-cloud-gdpr.html) </li><li>[!DNL Advertising Cloud] nutzt vorhandene globale Ausschluss-Funktionen des Adobe Datenschutzzentrums. Weitere Informationen finden Sie im Handbuch zum [Erstellen von Datenschutzanforderungen](https://docs.adobe.com/content/help/de-DE/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests) .</li></ul> |
| Adobe Analytics | ✓ | ✓ | <ul><li>[Dokumentation aufrufen/löschen](https://docs.adobe.com/content/help/en/analytics/admin/data-governance/an-gdpr-overview.html)</li><li>[!DNL Analytics] verarbeitet Abmeldeanfragen mithilfe von [Privacy Berichte-Variablen](https://docs.adobe.com/content/help/de-DE/analytics/admin/data-governance/consent-variables.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | <ul><li>[Dokumentation aufrufen/löschen](https://docs.adobe.com/content/help/de-DE/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Dokumentation zur Abmeldung](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | <ul><li>[Dokumentation aufrufen/löschen](https://docs.campaign.adobe.com/doc/standard/getting_started/de/ACS_GDPR.html)</li><li>[Dokumentation zur Abmeldung](../segmentation/honoring-opt-outs.md)</li></ul> |
| Adobe-Kundenattribute (CRS) | ✓ | K. A. | <ul><li>[Dokumentation für GDPR aufrufen/löschen](https://docs.adobe.com/content/help/de-DE/core-services/interface/customer-attributes/gdpr.html)</li><li>[Dokumentation für CCPA aufrufen/löschen](https://docs.adobe.com/content/help/de-DE/core-services/interface/customer-attributes/ccpa.html)</li><li>Kundenattribute sind nicht in der Lage, Daten zu übertragen. Daher sind Ausschlussanfragen nicht möglich.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | <ul><li>[Dokumentation zum Data Lake aufrufen/löschen](../catalog/privacy.md)</li><li>[Dokumentation für Echtzeit-Kundendaten aufrufen/löschen](../profile/privacy.md)</li><li>[!DNL Experience Platform] berücksichtigt [Abmeldeanforderungen für Audiencen-Segmente](../segmentation/honoring-opt-outs.md).</li></ul> |
| Adobe Primetime-Authentifizierung | ✓ | K. A. | <ul><li>[Dokumentation aufrufen/löschen](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] nicht in der Lage ist, Daten zu übertragen, daher sind Ausschlussanträge nicht anwendbar.</li></ul> |
| Adobe Target | ✓ | K. A. | <ul><li>[Dokumentation aufrufen/löschen](https://docs.adobe.com/content/help/de-DE/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html)</li><li>[!DNL Target] nicht in der Lage ist, Daten zu übertragen, daher sind Ausschlussanträge nicht anwendbar.</li></ul> |


## Selbstbedienungsanwendungen {#self-serve}

Im Folgenden finden Sie eine Liste von [!DNL Experience Cloud] Anwendungen, die nicht in die Datenschutzbestimmungen integriert sind [!DNL Privacy Service] und intern verwaltet werden müssen. Links zur Dokumentation der einzelnen Anwendungen sowie Beschreibungen des Inhalts der Dokumentation werden bereitgestellt.

| Anwendung | Beschreibung der Dokumentation |
| ------- | ----------- |
| [Adobe Campaign Classic](https://docs.campaign.adobe.com/doc/AC/getting_started/DE/ACC_GDPR.html) | Eine Übersicht über die GDPR-Funktionen von Adobe Campaign Classic. |
| [Adobe Dynamischer Tag-Manager](https://docs.adobe.com/content/help/de-DE/dtm/using/tools/opt-in.html) | Schritte, die verhindern, dass Adobe-Tags ausgelöst werden, bis die Zustimmung erteilt wurde. |
| [Adobe Experience Manager](https://helpx.adobe.com/experience-manager/6-4/managing/using/gdpr-compliance.html) | Eine Übersicht darüber, wie ein Datenschutzadministrator oder AEM-Administrator GDPR-Anforderungen bearbeiten kann. |
| [Adobe Experience Manager Livefyre](https://docs.adobe.com/content/help/en/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Schritte zum Erstellen des Zugriffs auf GDPR und Löschen von Anforderungen mit Livefyre. |
| [Adobe Experience Platform Launch](https://docs.adobelaunch.com/client-side-information/deploy-javascript-tags-to-opt-in-to-launch) | Anleitung für Entwickler zur Verwendung von Erweiterungen und Rule Builder zum Definieren von Opt-in- und Opt-out-Lösungen. |
