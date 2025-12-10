---
keywords: Experience Platform;Startseite;beliebte Themen
solution: Experience Platform
title: Privacy Service- und Experience Cloud-Programme
description: Dieses Dokument enthält eine Referenz zum Konfigurieren verschiedener Experience Cloud-Programme für datenschutzbezogene Vorgänge.
exl-id: da21c15f-0b99-4eb7-ac9a-f0fe5e3ba842
source-git-commit: b8b862a2134d4901e45f5dce82ac4de457ed6db6
workflow-type: tm+mt
source-wordcount: '869'
ht-degree: 7%

---

# [!DNL Privacy Service] und [!DNL Experience Cloud]

Adobe Experience Platform [!DNL Privacy Service] wurde entwickelt, um Datenschutzanfragen für mehrere Adobe Experience Cloud-Programme zu unterstützen. Jede Anwendung unterstützt verschiedene Produktwerte und IDs zur Identifizierung von betroffenen Personen.

Dieses Dokument dient als Referenz für [!DNL Experience Cloud] Anwendungsdokumentation, in der beschrieben wird, wie Sie diese Anwendung für datenschutzbezogene Vorgänge konfigurieren. Dazu gehört auch die Formatierung und Beschriftung Ihrer Daten. Es werden zwei Arten von Anträgen behandelt:

* [In Privacy Service integrierte Anwendungen](#integrated): Anwendungen, die Zugriffs-, Lösch- oder Opt-out-Anfragen an [!DNL Privacy Service] senden können.
* [Selbstbedienungsanwendungen](#self-serve): Anwendungen, die ihre Datenschutzanfragen intern verwalten müssen und nicht direkt mit [!DNL Privacy Service] kommunizieren können.

Lesen Sie die Dokumentation für Ihre [!DNL Experience Cloud]-Programme, um zu erfahren, wie Sie Ihre Datenschutzanfragen formatieren und welche Werte für diese Anfragen unterstützt werden.

## In [!DNL Privacy Service] integrierte Anwendungen {#integrated}

Im Folgenden finden Sie eine Liste [!DNL Experience Cloud] Anwendungen, die in [!DNL Privacy Service] integriert sind, einschließlich der [!DNL Privacy Service] Funktionen, mit denen sie kompatibel sind, ihrer Protokolle zur Verarbeitung von Löschanfragen und Links zur Dokumentation für weitere Informationen.

>[!NOTE]
>
>Alle integrierten Produkte reagieren auf Datenschutzanfragen in 30 Tagen oder weniger.

| Anwendung | Zugriff/Löschung | Opt-out vom Verkauf | Löschverhalten | Dokumentation und andere Überlegungen |
| --- | :---: | :---: | --- | --- |
| Adobe Advertising | ✓ | ✓ | Die Cookie-ID oder Geräte-ID der betroffenen Person wird zusammen mit allen mit dem Cookie verbundenen Kosten-, Klick- und Umsatzdaten aus dem System gelöscht. | <ul><li>[Zugriff/Löschung der Dokumentation zur DSGVO](https://experienceleague.adobe.com/en/docs/advertising/privacy/gdpr)</li><li>[Zugriff auf/Löschen der Dokumentation für CCPA](https://experienceleague.adobe.com/en/docs/advertising/privacy/ccpa/ccpa-access-delete)</li><li>[Dokumentation zum Opt-out vom Verkauf für CCPA](https://experienceleague.adobe.com/en/docs/advertising/privacy/ccpa/ccpa-opt-out-of-sale)</li></ul> |
| Adobe Analytics | ✓ | ✓ | Adobe Analytics bietet Tools zur Kennzeichnung von Daten entsprechend ihrer Sensibilität und ihren vertraglichen Einschränkungen. Kennzeichnungen sind ein wichtiger Schritt für:<ol><li>Identifizieren von betroffenen Personen.</li><li>Bestimmen, welche Daten im Rahmen einer Zugriffsanfrage zurückgegeben werden sollen.</li><li>Identifizieren von Datenfeldern, die im Rahmen einer Löschanfrage gelöscht werden müssen.</li></ol> | <ul><li>[Datenschutz-Workflow](https://experienceleague.adobe.com/en/docs/analytics/technotes/privacy/gdpr)</li><li>[Analytics-Beschriftung](https://experienceleague.adobe.com/en/docs/analytics/admin/admin-tools/privacy-labeling/labels)</li><li>[Analytics-Opt-out](https://experienceleague.adobe.com/en/docs/analytics/components/dimensions/cm-opt-out)</li></ul> |
| Adobe Audience Manager | ✓ | ✓ | Alle in der Anfrage enthaltenen Eigenschaften und Segmente, die mit der Audience Manager-Kennung verknüpft sind, werden gelöscht. Darüber hinaus werden die jeweiligen Kennungen für die Person von der weiteren Datenerfassung ausgeschlossen und die jeweiligen ID-Zuordnungen entfernt. | <ul><li>Dokumentation [Zugriff](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests#access-data)/[Löschen](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests#delete-data)</li><li>[Opt-out-Dokumentation](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/features/declared-ids#opt-out-calls)</li><li>[Opt-out-Anfragen](https://experienceleague.adobe.com/en/docs/audience-manager/user-guide/overview/data-privacy/data-privacy-requests#opt-out-requests)</li></ul> |
| Adobe Campaign Classic | ✓ | ✓ | Die gespeicherten Daten der betroffenen Person werden aus dem System gelöscht. | <ul><li>[Datenschutzverwaltung](https://experienceleague.adobe.com/en/docs/campaign-classic/using/getting-started/privacy/privacy-management)</li></ul> |
| Adobe Campaign Standard | ✓ | ✓ | Die gespeicherten Daten der betroffenen Person werden aus dem System gelöscht. | <ul><li>[Auf Dokumentation zugreifen/sie löschen](https://experienceleague.adobe.com/en/docs/campaign-standard/using/getting-started/privacy/privacy-management#right-access-forgotten)</li><li>[Opt-out-Dokumentation](https://experienceleague.adobe.com/en/docs/campaign-standard/using/profiles-and-audiences/understanding-opt-in-and-opt-out-processes/about-opt-in-and-opt-out-in-campaign)</li></ul> |
| Adobe-Kundenattribute (CRS) | ✓ | k. A. | Die Attribute der betroffenen Person werden aus dem System gelöscht. | <ul><li>[Zugriff/Löschung der Dokumentation zur DSGVO](https://experienceleague.adobe.com/en/docs/core-services/interface/services/customer-attributes/gdpr)</li><li>[Zugriff auf/Löschen der Dokumentation für CCPA](https://experienceleague.adobe.com/en/docs/core-services/interface/services/customer-attributes/ccpa)</li><li>Kundenattribute sind nicht in der Lage, Daten zu übertragen, daher können Opt-out-Anfragen nicht angewendet werden.</li></ul> |
| Adobe Experience Platform | ✓ | ✓ | Wenn Experience Platform eine DELETE-Anfrage von Privacy Service erhält, sendet Experience Platform eine Bestätigung an Privacy Service, dass die Anfrage empfangen wurde und die betroffenen Daten zum Löschen markiert wurden. Die Datensätze werden dann aus dem Data Lake oder Profilspeicher entfernt, sobald der Datenschutzvorgang abgeschlossen ist. Vor Abschluss des Auftrags werden die Daten vorläufig gelöscht und stehen somit keinem Experience Platform-Service mehr zur Verfügung. | <ul><li>[Zugriff auf/Löschen der Dokumentation für den Data Lake](../catalog/privacy.md)</li><li>[Zugriff auf/Löschen der Dokumentation für Identity Service](../identity-service/privacy.md)</li><li>[Zugriff auf/Löschen der Dokumentation für das Echtzeit-Kundenprofil](../profile/privacy.md)</li><li>[!DNL Experience Platform] berücksichtigt [Opt-out-Anfragen für Zielgruppensegmente](../segmentation/tutorials/consents.md).</li></ul> |
| Adobe Journey Optimizer | ✓ | k. A. | Die gespeicherten Daten der betroffenen Person werden aus dem System gelöscht. | <ul><li>[Auf Dokumentation zugreifen/sie löschen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/privacy/requests)</li></ul> |
| Adobe Pass-Authentifizierung | ✓ | k. A. | Die gespeicherten Daten der betroffenen Person werden aus dem System gelöscht. | <ul><li>[Auf Dokumentation zugreifen/sie löschen](https://tve.helpdocsonline.com/how-to-make-a-privacy-request)</li><li>Pass ist nicht in der Lage, Daten zu übertragen, weshalb Opt-out-Kaufanfragen nicht anwendbar sind.</li></ul> |
| Adobe Target | ✓ | k. A. | Alle mit der ID der betroffenen Person verknüpften Daten werden aus ihrem Besucherprofil gelöscht. Aggregierte oder anonymisierte Daten, die die Person nicht identifizieren oder anderweitig nicht miteinander in Verbindung stehen (z. B. Inhaltsdaten), gelten nicht für Löschanfragen. | <ul><li>[Auf Dokumentation zugreifen/sie löschen](https://experienceleague.adobe.com/en/docs/target-dev/developer/implementation/privacy/cmp-privacy-and-general-data-protection-regulation)</li><li>[!DNL Target] ist nicht in der Lage, Daten zu übertragen, daher können Opt-out-Anfragen nicht angewendet werden.</li></ul> |
| Commerce (Personalization) | ✓ | k. A. | Privacy Service löscht [!DNL Commerce] in Commerce SaaS-Services gespeicherten Daten zu Marketing-Zwecken, d. h. die Profile und Bestellungen der betroffenen Personen werden nicht mehr zur Verwendung in Kampagnen und Kunden-Journey an Adobe-Marketing-Anwendungen gesendet. Privacy Service löscht jedoch keine Daten in der [!DNL Commerce]-Anwendung, da sie möglicherweise weiterhin für die Abwicklung von Transaktionen durch Händler erforderlich sind. Händler sind für alle Datenlöschungs-/-zugriffsanfragen im [!DNL Commerce] verantwortlich. | <ul><li>[Zugriff/Löschen der Dokumentation für Commerce](https://experienceleague.adobe.com/en/docs/commerce-merchant-services/data-connection/handle-privacy-request)</li></ul> |
| Marketo Engage | ✓ | k. A. | Die gespeicherten Daten der betroffenen Person werden aus dem System gelöscht. | <ul><li>[Auf Dokumentation zugreifen/sie löschen](https://experienceleague.adobe.com/en/docs/marketo/using/product-docs/core-marketo-concepts/miscellaneous/privacy-requests)</li><li>[!DNL Marketo] ist nicht in der Lage, Daten zu übertragen, daher können Opt-out-Anfragen nicht angewendet werden.</li></ul> |

## Self-Service-Anwendungen {#self-serve}

Im Folgenden finden Sie eine Liste [!DNL Experience Cloud] Anwendungen, die nicht in [!DNL Privacy Service] integriert sind und deren Datenschutzanliegen intern verwalten müssen. Links zur Dokumentation der einzelnen Programme werden zusammen mit Beschreibungen des Inhalts der Dokumentation bereitgestellt.

| Anwendung | Dokumentationsbeschreibung |
| ------- | ----------- |
| [Adobe Experience Manager](https://experienceleague.adobe.com/en/docs/experience-manager-64/managing/data-protection/data-protection-and-privacy) | Ein Überblick darüber, wie Datenschutzadministratoren oder AEM-Administratoren DSGVO-Anfragen bearbeiten können. |
| [Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/security-and-compliance/overview) | Stellen Sie sicher, dass Ihre Adobe Commerce-Installationen die Anforderungen bestimmter Datenschutzgesetze erfüllen. |
| [Tags in Adobe Experience Platform](../tags/ui/client-side/consent.md) | Anleitung für Entwickler zur Verwendung von Erweiterungen und Rule Builder zum Definieren von Opt-in- und Opt-out-Lösungen. |
| [Workfront](https://www.workfront.com/privacy-notice) | Erfahren Sie, wie Workfront personenbezogene Daten erfasst und wie eine betroffene Person eine Datenschutzanfrage über ein Formular senden kann. |
