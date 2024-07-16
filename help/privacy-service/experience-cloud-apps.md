---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Privacy Service- und Experience Cloud-Anwendungen
description: Dieses Dokument enthält eine Referenz zum Konfigurieren verschiedener Experience Cloud-Anwendungen für datenschutzbezogene Vorgänge.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: 46ca46460de9211c3e876454c986d030b964646e
workflow-type: tm+mt
source-wordcount: '822'
ht-degree: 14%

---

# [!DNL Privacy Service] - und [!DNL Experience Cloud] -Anwendungen

Adobe Experience Platform [!DNL Privacy Service] wurde entwickelt, um Datenschutzanfragen für mehrere Adobe Experience Cloud-Anwendungen zu unterstützen. Jede Anwendung unterstützt unterschiedliche Produktwerte und IDs zur Identifizierung von Datensubjekten.

Dieses Dokument dient als Referenz für die Dokumentation zur [!DNL Experience Cloud]-Anwendung, in der beschrieben wird, wie Sie diese Anwendung für datenschutzbezogene Vorgänge konfigurieren. Dazu gehört auch die Formatierung und Beschriftung Ihrer Daten. Es werden zwei Kategorien von Anträgen behandelt:

* [In Privacy Service integrierte Anwendungen](#integrated): Anwendungen, die Zugriffs-, Lösch- oder Opt-out-Anfragen an [!DNL Privacy Service] senden können.
* [Self-Service-Anwendungen](#self-serve): Anwendungen, die ihre Datenschutzanfragen intern verwalten und nicht direkt mit [!DNL Privacy Service] kommunizieren können.

In der Dokumentation zu Ihren [!DNL Experience Cloud] -Anwendungen erfahren Sie, wie Sie Ihre Datenschutzanfragen formatieren und welche Werte für diese Anfragen unterstützt werden.

## In [!DNL Privacy Service] integrierte Anwendungen {#integrated}

Im Folgenden finden Sie eine Liste der [!DNL Experience Cloud] Anwendungen, die in [!DNL Privacy Service] integriert sind, einschließlich der [!DNL Privacy Service] Funktionen, mit denen sie kompatibel sind, ihrer Protokolle zur Verarbeitung von Löschanfragen und Links zur Dokumentation für weitere Informationen.

>[!NOTE]
>
>Alle integrierten Produkte reagieren auf Datenschutzanfragen innerhalb von 30 Tagen oder weniger.

| Anwendung | Zugriff/Löschen | Abmeldung vom Verkauf | Löschverhalten | Dokumentation und andere Aspekte |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising Cloud | ✓ | ✓ | Die Cookie-ID oder Geräte-ID des Datensubjekts wird zusammen mit allen mit dem Cookie verbundenen Kosten-, Klick- und Umsatzdaten aus dem System gelöscht. | <ul><li>[Zugriff/Löschen der Dokumentation für die DSGVO](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-gdpr.html)</li><li>[Zugriff/Löschen der Dokumentation für CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-access-delete.html)</li><li>[Dokumentation zum Opt-out-of-Sale für CCPA](https://experienceleague.adobe.com/docs/advertising-cloud/privacy/ad-cloud-ccpa-opt-out-of-sale.html)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Adobe Analytics bietet Tools zur Kennzeichnung von Daten entsprechend ihrer Vertraulichkeit und vertraglichen Beschränkungen. Beschriftungen sind ein wichtiger Schritt für:<ol><li>Identifizieren von Datensubjekten.</li><li>Bestimmen, welche Daten im Rahmen einer Zugriffsanfrage zurückgegeben werden sollen.</li><li>Identifizieren von Datenfeldern, die im Rahmen einer Löschanfrage gelöscht werden müssen.</li></ol> | <ul><li>[Datenschutz-Workflow](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/an-gdpr-workflow.html)</li><li>[Analytics-Beschriftung](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/data-governance/data-labels/gdpr-labels.html)</li><li>[Analytics-Opt-out](https://experienceleague.adobe.com/docs/analytics/components/dimensions/cm-opt-out.html)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | Alle Eigenschaften und Segmente, die mit der in der Anfrage enthaltenen Audience Manager-ID verknüpft sind, werden gelöscht. Darüber hinaus werden die jeweiligen Kennungen für die Person von der weiteren Datenerfassung ausgeschlossen und die entsprechenden ID-Zuordnungen entfernt. | <ul><li>Dokumentation zu [Zugriff](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#access-data) / [Löschen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#delete-data)</li><li>[Dokumentation zum Opt-out](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/declared-ids.html#opt-out-calls)</li><li>[Opt-out-Anfragen](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests.html#opt-out-requests)</li></ul> |
| Adobe Campaign Classic | ✓ | ✓ | Die gespeicherten Daten der betroffenen Person werden aus dem System gelöscht. | <ul><li>[Datenschutzverwaltung](https://experienceleague.adobe.com/docs/campaign-classic/using/getting-started/privacy/privacy-management.html?lang=de).</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | Die gespeicherten Daten der betroffenen Person werden aus dem System gelöscht. | <ul><li>[Dokumentation aufrufen/löschen](https://docs.campaign.adobe.com/doc/standard/getting_started/de/ACS_GDPR.html)</li><li>[Dokumentation zum Opt-out](../segmentation/consents.md)</li></ul> |
| Adobe Kundenattribute (CRS) | ✓ | K. A. | Die Attribute der betroffenen Person werden aus dem System gelöscht. | <ul><li>[Zugriff/Löschen der Dokumentation für die DSGVO](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/gdpr.html?lang=de)</li><li>[Zugriff/Löschen der Dokumentation für CCPA](https://experienceleague.adobe.com/docs/core-services/interface/customer-attributes/ccpa.html?lang=de)</li><li>Kundenattribute können keine Daten übertragen. Daher sind Opt-out-Anfragen für den Verkauf nicht möglich.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | Wenn Experience Platform von Privacy Service eine Löschanfrage erhält, sendet Platform eine Bestätigung an Privacy Service, dass die Anfrage empfangen wurde und die betroffenen Daten zum Löschen markiert wurden. Die Datensätze werden dann aus dem Data Lake oder Profilspeicher entfernt, sobald der Datenschutzauftrag abgeschlossen ist. Bevor der Auftrag abgeschlossen ist, werden die Daten weich gelöscht und stehen daher keinem Platform-Dienst zur Verfügung. | <ul><li>[Zugriff/Löschen der Dokumentation für den Data Lake](../catalog/privacy.md)</li><li>[Zugriff/Löschen der Dokumentation für Identity Service](../identity-service/privacy.md)</li><li>[Zugriff/Löschen der Dokumentation für das Echtzeit-Kundenprofil](../profile/privacy.md)</li><li>[!DNL Experience Platform] berücksichtigt [Opt-out-Anfragen für Zielgruppensegmente](../segmentation/consents.md).</li></ul> |
| Adobe Journey Optimizer | ✓ | K. A. | Die gespeicherten Daten der betroffenen Person werden aus dem System gelöscht. | <ul><li>[Dokumentation aufrufen/löschen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/requests)</li></ul> |
| Adobe Pass-Authentifizierung | ✓ | K. A. | Die gespeicherten Daten der betroffenen Person werden aus dem System gelöscht. | <ul><li>[Dokumentation aufrufen/löschen](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Der Pass verfügt nicht über die Fähigkeit, Daten zu übertragen. Daher sind Opt-out-Kaufanfragen nicht möglich.</li></ul> |
| Adobe Target | ✓ | K. A. | Alle Daten, die mit der ID der betroffenen Person verknüpft sind, werden aus ihrem Besucherprofil gelöscht. Aggregierte oder anonymisierte Daten, die die Person nicht identifizieren oder anderweitig nicht verwandt sind (z. B. Inhaltsdaten), gelten nicht für Löschanfragen. | <ul><li>[Dokumentation aufrufen/löschen](https://experienceleague.adobe.com/docs/target/using/implement-target/before-implement/privacy/cmp-privacy-and-general-data-protection-regulation.html?lang=de)</li><li>[!DNL Target] verfügt nicht über die Fähigkeit, Daten zu übertragen. Daher sind Opt-out-Kaufanfragen nicht möglich.</li></ul> |
| Marketo Engage | ✓ | K. A. | Die gespeicherten Daten der betroffenen Person werden aus dem System gelöscht. | <ul><li>[Dokumentation aufrufen/löschen](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests.html)</li><li>[!DNL Marketo] verfügt nicht über die Fähigkeit, Daten zu übertragen. Daher sind Opt-out-Kaufanfragen nicht möglich.</li></ul> |

{style="table-layout:auto"}

## Self-Service-Anwendungen {#self-serve}

Im Folgenden finden Sie eine Liste von [!DNL Experience Cloud] -Anwendungen, die nicht in [!DNL Privacy Service] integriert sind und ihre Datenschutzanfragen intern verwalten müssen. Es werden Links zur Dokumentation der einzelnen Anwendungen sowie Beschreibungen der Dokumentationsinhalte bereitgestellt.

| Anwendung | Dokumentationsbeschreibung |
| ------- | ----------- |
| [Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy.html) | Ein Überblick darüber, wie ein Datenschutzadministrator oder AEM Administrator DSGVO-Anfragen verarbeiten kann. |
| [Adobe Experience Manager Livefyre](https://experienceleague.adobe.com/docs/livefyre/using/settings-other/privacy-requests/c-gdpr-compliance.html) | Schritte zum Ausführen von DSGVO-Zugriffs- und -Löschanfragen mit Livefyre. |
| [Magento](https://devdocs.magento.com/compliance/industry-compliance.html) | Stellen Sie sicher, dass Ihre Magento Commerce-Installationen den Anforderungen der jeweiligen Datenschutzgesetze entsprechen. |
| [Tags in Adobe Experience Platform](../tags/ui/client-side/consent.md) | Anleitung für Entwickler zur Verwendung von Erweiterungen und Rule Builder zum Definieren von Opt-in- und Opt-out-Lösungen. |
| [Workfront](https://www.workfront.com/privacy-notice) | Erfahren Sie, wie Workfront personenbezogene Daten erfasst und wie ein Datensubjekt über ein Formular eine Datenschutzanfrage senden kann. |

{style="table-layout:auto"}
