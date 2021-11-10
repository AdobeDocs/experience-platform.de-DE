---
keywords: Experience Platform;Home;beliebte Themen
solution: Experience Platform
title: Privacy Service- und Experience Cloud-Anwendungen
topic-legacy: overview
description: Dieses Dokument bietet eine Referenz zum Konfigurieren verschiedener Experience Cloud-Anwendungen für datenschutzbezogene Vorgänge.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: b430b9741beb2f8d41bcbe8168cb20a73d13c750
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 15%

---

# [!DNL Privacy Service] und [!DNL Experience Cloud] Anwendungen

Adobe Experience Platform [!DNL Privacy Service] wurde entwickelt, um Datenschutzanfragen für mehrere Adobe Experience Cloud-Anwendungen zu unterstützen. Jede Anwendung unterstützt unterschiedliche Produktwerte und IDs zur Identifizierung von Datensubjekten.

Dieses Dokument dient als Referenz für [!DNL Experience Cloud] Anwendungsdokumentation, in der die Konfiguration dieser Anwendung für datenschutzbezogene Vorgänge beschrieben wird. Dazu gehört auch die Formatierung und Beschriftung Ihrer Daten. Es werden zwei Kategorien von Anträgen behandelt:

* [In Privacy Service integrierte Anwendungen](#integrated): Anwendungen, die Zugriffs-, Lösch- oder Opt-out-Anfragen an senden können [!DNL Privacy Service].
* [Self-Service-Anwendungen](#self-serve): Anwendungen, die ihre Datenschutzanfragen intern verwalten und nicht mit [!DNL Privacy Service] direkt.

Lesen Sie die Dokumentation für Ihre [!DNL Experience Cloud] Anwendungen , um zu erfahren, wie Sie Ihre Datenschutzanfragen formatieren und welche Werte für diese Anfragen unterstützt werden.

## In integrierte Anwendungen [!DNL Privacy Service] {#integrated}

Im Folgenden finden Sie eine Liste von [!DNL Experience Cloud] Anwendungen, die mit [!DNL Privacy Service], einschließlich der [!DNL Privacy Service] Funktionen, mit denen sie kompatibel sind, deren Protokolle zur Verarbeitung von Löschanfragen und Links zur Dokumentation für weitere Informationen.

>[!NOTE]
>
>Alle integrierten Produkte reagieren auf Datenschutzanfragen innerhalb von 30 Tagen oder weniger.

| Anwendung | Zugriff/Löschen | Abmeldung vom Verkauf | Löschverhalten | Dokumentation und andere Aspekte |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | verwalten | Die Cookie-ID oder Geräte-ID des Datensubjekts wird zusammen mit allen mit dem Cookie verbundenen Kosten-, Klick- und Umsatzdaten aus dem System gelöscht. | <ul><li>[Dokumentation zur DSGVO aufrufen/löschen](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Dokumentation für CCPA aufrufen/löschen](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Dokumentation zum Opt-out-of-Sale für CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | verwalten | verwalten | Wenn `analyticsDeleteMethod` ausgelassen oder auf `anonymize` bei der Erstellung der Datenschutzanfrage werden alle Daten, auf die bei der angegebenen Sammlung von Benutzer-IDs verwiesen wird, anonym gemacht. Wenn `analyticsDeleteMethod` auf `purge`, werden alle Daten vollständig entfernt. | <ul><li>[Dokumentation aufrufen/löschen](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/an-gdpr-overview.html?lang=de)</li><li>[!DNL Analytics] verarbeitet Opt-out-Anfragen mithilfe von [Variablen für Datenschutzberichte](https://experienceleague.adobe.com/docs/analytics/admin/data-governance/consent-variables.html?lang=de)</li></ul> |
| Adobe Audience Manager | verwalten | verwalten | Alle Eigenschaften und Segmente, die mit der in der Anfrage enthaltenen Audience Manager-ID verknüpft sind, werden gelöscht. Darüber hinaus werden die jeweiligen Kennungen für die Person von der weiteren Datenerfassung ausgeschlossen und die entsprechenden ID-Zuordnungen entfernt. | <ul><li>[Dokumentation aufrufen/löschen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html)</li><li>[Opt-out-Dokumentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html)</li></ul> |
| Adobe Campaign Standard | verwalten | verwalten | Die gespeicherten Daten der betroffenen Person werden aus dem System gelöscht. | <ul><li>[Dokumentation aufrufen/löschen](https://docs.campaign.adobe.com/doc/standard/getting_started/de/ACS_GDPR.html)</li><li>[Opt-out-Dokumentation](../segmentation/consents.md)</li></ul> |
| Adobe-Kundenattribute (CRS) | verwalten | K. A. | Die Attribute der betroffenen Person werden aus dem System gelöscht. | <ul><li>[Dokumentation zur DSGVO aufrufen/löschen](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html)</li><li>[Dokumentation für CCPA aufrufen/löschen](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html)</li><li>Kundenattribute können keine Daten übertragen. Daher sind Opt-out-Anfragen für den Verkauf nicht möglich.</li></ul> |
| Adobe Experience Platform | verwalten | verwalten | Wenn Experience Platform von Privacy Service eine Löschanfrage erhält, sendet Platform eine Bestätigung an Privacy Service, dass die Anfrage empfangen wurde und die betroffenen Daten zum Löschen markiert wurden. Die Datensätze werden dann aus dem Data Lake oder Profilspeicher entfernt, sobald der Datenschutzauftrag abgeschlossen ist. Bevor der Auftrag abgeschlossen ist, werden die Daten weich gelöscht und stehen daher keinem Platform-Dienst zur Verfügung. | <ul><li>[Zugriff/Löschung der Dokumentation für den Data Lake](../catalog/privacy.md)</li><li>[Dokumentation für Identity Service aufrufen/löschen](../identity-service/privacy.md)</li><li>[Dokumentation für Echtzeit-Kundenprofil aufrufen/löschen](../profile/privacy.md)</li><li>[!DNL Experience Platform] honors [Opt-out-Anfragen für Zielgruppensegmente](../segmentation/consents.md).</li></ul> |
| Adobe Primetime-Authentifizierung | verwalten | K. A. | Die gespeicherten Daten der betroffenen Person werden aus dem System gelöscht. | <ul><li>[Dokumentation aufrufen/löschen](http://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>[!DNL Primetime] verfügt nicht über die Möglichkeit, Daten zu übertragen. Daher sind Opt-out-Anfragen für den Verkauf nicht möglich.</li></ul> |
| Adobe Target | verwalten | K. A. | Alle mit der ID der betroffenen Person verknüpften Daten werden aus ihrem Besucherprofil gelöscht. Aggregierte oder anonymisierte Daten, die die Person nicht identifizieren oder anderweitig nicht verwandt sind (z. B. Inhaltsdaten), gelten nicht für Löschanfragen. | <ul><li>[Dokumentation aufrufen/löschen](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=de)</li><li>[!DNL Target] verfügt nicht über die Möglichkeit, Daten zu übertragen. Daher sind Opt-out-Anfragen für den Verkauf nicht möglich.</li></ul> |
| Marketo Engage | verwalten | K. A. | Die gespeicherten Daten der betroffenen Person werden aus dem System gelöscht. | <ul><li>[Dokumentation aufrufen/löschen](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html)</li><li>[!DNL Marketo] verfügt nicht über die Möglichkeit, Daten zu übertragen. Daher sind Opt-out-Anfragen für den Verkauf nicht möglich.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Self-Service-Anwendungen {#self-serve}

Im Folgenden finden Sie eine Liste von [!DNL Experience Cloud] Anwendungen, die nicht in [!DNL Privacy Service] und müssen ihre Datenschutzanliegen intern verwalten. Es werden Links zur Dokumentation der einzelnen Anwendungen sowie Beschreibungen der Dokumentationsinhalte bereitgestellt.

| Anwendung | Dokumentationsbeschreibung |
| ------- | ----------- |
| [Adobe Campaign Classic](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=de) | Eine Übersicht über die DSGVO-Funktionen für Adobe Campaign Classic. |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | Ein Überblick darüber, wie ein Datenschutzadministrator oder AEM Administrator DSGVO-Anfragen verarbeiten kann. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Schritte zum Ausführen von DSGVO-Zugriffs- und -Löschanfragen mit Livefyre. |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | Stellen Sie sicher, dass Ihre Magento Commerce-Installationen den Anforderungen der jeweiligen Datenschutzgesetze entsprechen. |
| [Marketo](https://www.marketo.com/company/trust/gdpr/) | Erfahren Sie, wie die Datenschutzbestimmungen für Marketo gelten. |
| [Tags in Adobe Experience Platform](../tags/ui/client-side/consent.md) | Anleitung für Entwickler zur Verwendung von Erweiterungen und Rule Builder zum Definieren von Opt-in- und Opt-out-Lösungen. |
| [Workfront](https://www.workfront.com/privacy-notice) | Erfahren Sie, wie Workfront personenbezogene Daten erfasst und wie ein Datensubjekt über ein Formular eine Datenschutzanfrage senden kann. |

{style=&quot;table-layout:auto&quot;}
