---
keywords: Experience Platform;home;IAB;IAB 2.0;
solution: Experience Platform
title: Unterstützung von IAB TCF 2.0 in der Echtzeit-Plattform für Kundendaten
topic: privacy events
translation-type: tm+mt
source-git-commit: 67c598000cec36a170e7324877d4d9f2db9453a4
workflow-type: tm+mt
source-wordcount: '2373'
ht-degree: 2%

---


# IAB TCF 2.0-Unterstützung in [!DNL Real-time Customer Data Platform]

Der [!DNL Transparency & Consent Framework] (TCF), wie im [!DNL Interactive Advertising Bureau] (IAB) dargelegt, ist ein offener technischer Rahmen, der es Organisationen ermöglichen soll, die Zustimmung der Verbraucher zur Verarbeitung ihrer personenbezogenen Daten gemäß dem GDPR der Europäischen Vereinigung einzuholen, zu erfassen und zu aktualisieren [!DNL General Data Protection Regulation] . Die zweite Iteration des Rahmens, TCF 2.0, bietet mehr Flexibilität bei der Bereitstellung oder Zurückhaltung der Zustimmung durch die Verbraucher, einschließlich der Frage, ob und wie Anbieter bestimmte Merkmale der Datenverarbeitung, wie z. B. eine genaue Geolokation, nutzen können.

>[!NOTE]
>
>Weitere Informationen zu TCF 2.0 finden Sie auf der [IAB Europe-Website](https://iabeurope.eu/tcf-2-0/), einschließlich Unterstützungsmaterial und technischer Spezifikationen.

[!DNL Real-time Customer Data Platform (Real-time CDP)] ist Teil der registrierten [IAB TCF 2.0 Händlerversion Liste](https://iabeurope.eu/vendor-list-tcf-v2-0/), unter der ID **565**. In Übereinstimmung mit den Anforderungen von TCF 2.0 [!DNL Real-time CDP] können Sie Daten zur Kundengenehmigung erfassen und in Ihre gespeicherten Profil integrieren. Diese Daten zur Einwilligung können dann je nach Anwendungsfall in die Segmente der exportierten Audience einbezogen werden.

>[!IMPORTANT]
>
>[!DNL Real-time CDP] kann nur mit Version 2.0 des TCF (oder höher) übereinstimmen. Frühere Versionen von TCF werden nicht unterstützt.

Dieses Dokument bietet einen Überblick darüber, wie Sie Ihre Datenvorgänge konfigurieren und Profil-Schema zur Annahme von durch Ihren CMP generierten Daten zur Kundeneinwilligung nutzen können und wie Sie beim Exportieren von Segmenten Entscheidungen zur Benutzereinwilligung treffen [!DNL Real-time CDP] können.

## Voraussetzungen 

Um diesem Leitfaden zu folgen, müssen Sie entweder eine kommerzielle oder eigene Consent Management Platform (CMP) verwenden, die mit dem IAB TCF integriert und kompatibel ist. Weitere Informationen finden Sie in der [Liste der konformen CMPs](https://iabeurope.eu/cmp-list/) .

>[!IMPORTANT]
>
>Wenn die ID Ihres CMP ungültig ist, [!DNL Real-time CDP] werden Ihre Daten unverändert verarbeitet. Um TCF 2.0 durchzusetzen, müssen Sie vor dem Senden von Daten an [!DNL Experience Platform]eine gültige ID für Ihren CMP bestätigen, die bei IAB TCF 2.0 registriert wurde.

Dieser Leitfaden erfordert auch ein Verständnis der folgenden Adobe Experience Platform-Dienste:

* [Experience-Datenmodell (XDM)](../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
* [Adobe Experience Platform-Identitätsdienst](../../../identity-service/home.md): Löst die grundlegende Herausforderung, die sich aus der Fragmentierung von Kundenerlebnisdaten ergibt, indem Identitäten zwischen Geräten und Systemen überbrückt werden.
* [Echtzeit-Profil](../../../profile/home.md): Ermöglicht [!DNL Identity Service] die Erstellung detaillierter Kundendaten aus Ihren Datensätzen in Echtzeit. [!DNL Real-time Customer Profile] ruft Daten aus dem Data Lake ab und behält die Profil der Kunden in einem eigenen separaten Datenspeicher bei.
* [Adobe Experience Platform Web SDK](../../../edge/home.md): Eine clientseitige JavaScript-Bibliothek, mit der Sie verschiedene [!DNL Platform] Dienste in Ihre kundenorientierte Website integrieren können.
* [Adobe Experience Platform-Segmentierungsdienst](../../../segmentation/home.md): Ermöglicht es Ihnen, [!DNL Real-time Customer Profile] Daten in Gruppen von Einzelpersonen zu unterteilen, die ähnliche Eigenschaften aufweisen und ähnlich wie Marketingstrategien reagieren.

Neben den oben aufgeführten [!DNL Platform] Diensten sollten Sie auch mit [Zielen](../../destinations/destinations-overview.md) und deren Verwendung in vertraut sein [!DNL Real-time CDP].

## Übersicht zum Ablauf der Kundengenehmigung {#summary}

In den folgenden Abschnitten wird beschrieben, wie Daten zur Einwilligung erfasst und erzwungen werden, nachdem das System ordnungsgemäß konfiguriert wurde.

### Consent data collection

[!DNL Real-time CDP] allows you to collect customer consent data through the following process:

1. A customer provides their consent preferences for data collection through a dialog on your website.
1. Your CMP detects the consent preference change, and generates IAB consent data accordingly.
1. Using the [!DNL Experience Platform Web SDK], the generated consent data (returned by the CMP) is sent to Adobe Experience Platform.
1. The collected consent data is ingested into a [!DNL Profile]-enabled dataset whose schema contains IAB consent fields.

In addition to SDK commands triggered by CMP consent-change hooks, consent data can also flow into [!DNL Experience Platform] through any customer-generated XDM data that is uploaded directly to a [!DNL Profile]-enabled dataset.

Any segments shared with [!DNL Platform] by Adobe Audience Manager (through the [!DNL Audience Manager] source connector or otherwise) may also contain consent data, provided that the appropriate fields have been applied to those segments through [!DNL Experience Cloud Identity Service]. For more information on collecting consent data in [!DNL Audience Manager], see the document on the [Adobe Audience Manager plug-in for IAB TCF](https://docs.adobe.com/help/de-DE/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Downstream consent enforcement

Once IAB consent data has successfully been ingested, the following processes take place in downstream [!DNL Real-time CDP] services:

1. [!DNL Real-time Customer Profile] updates the stored consent data for that customer&#39;s profile.
1. [!DNL Real-time CDP] processes customer IDs only if the vendor permission for [!DNL Real-time CDP] (565) is provided for every ID in a cluster.
1. When exporting segments to destinations belonging to members of the TCF 2.0 vendor list, [!DNL Real-time CDP] only includes profiles if the vendor permissions for both [!DNL Real-time CDP] (565) *and* the destination is provided for every ID in a cluster.

The rest of the sections in this document provide guidance on how to configure [!DNL Real-time CDP] and your data operations to fulfill the collection and enforcement requirements described above.

## Ermitteln Sie, wie Daten zur Kundengenehmigung in Ihrem CMP generiert werden. {#consent-data}

Da jedes CMP-System einzigartig ist, müssen Sie die beste Methode festlegen, um Ihren Kunden die Zustimmung zu geben, während sie mit Ihrem Service interagieren. Eine gängige Möglichkeit hierfür ist die Verwendung eines Cookie-Einwilligungsdialogs, ähnlich dem folgenden Beispiel:

![](../assets/iab/cmp-dialog.png)

Dieser Dialog muss es dem Kunden ermöglichen, Folgendes zu Opt-in oder auszuschließen:

| Option &quot;Zustimmung&quot; | Beschreibung |
| --- | --- |
| **Zweck** | Zweck definiert, für welche Ad-Tech-Zwecke eine Marke die Daten eines Kunden verwenden kann. Für die Verarbeitung von Kunden-IDs müssen die folgenden Zwecke gewählt [!DNL Real-time CDP] werden: <ul><li>**Zweck 1**: Store- und/oder Zugriffsinformationen auf einem Gerät</li><li>**Zweck 10**: Entwicklung und Verbesserung von Produkten</li></ul> |
| **Herstellerberechtigungen** | Zusätzlich zu den Zwecken der Anzeigentechnologie muss der Dialog dem Kunden auch ermöglichen, seine Daten von bestimmten Anbietern, einschließlich [!DNL  Real-time CDP] (565), Opt-in zu verwenden oder zu verlieren. |

### Zustimmungszeichenfolgen {#consent-strings}

Unabhängig von der Methode, die Sie zur Datenerfassung verwenden, besteht das Ziel darin, einen Zeichenfolgenwert zu generieren, der auf den vom Kunden gewählten Zustimmungsoptionen basiert, die als **Zustimmungszeichenfolge** bezeichnet werden.

In der TCF-Spezifikation werden Zustimmungszeichenfolgen verwendet, um relevante Details über die Einstellungen für die Zustimmung eines Kunden zu kodieren, in Bezug auf spezifische Marketingzwecke, die von Richtlinien und Anbietern definiert werden. [!DNL Real-time CDP] nutzt diese Zeichenfolgen, um die Einstellungen für die Einwilligung für jeden Kunden zu speichern. Daher muss bei jeder Änderung dieser Einstellungen eine neue Zeichenfolge für die Einwilligung generiert werden.

Zustimmungszeichenfolgen können nur von einem CMP erstellt werden, der bei der IAB-TCF registriert ist. Weitere Informationen zum Generieren von Zustimmungszeichenfolgen mit Ihrem jeweiligen CMP finden Sie im [Dokument zur Formatierung](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) der Zustimmungszeichenfolge im IAB TCF GitHub-Repo.

## Erstellen von Datensätzen mit IAB-Genehmigungsfeldern {#datasets}

Die Daten zur Kundengenehmigung müssen an Datasets gesendet werden, deren Schema die IAB-Einwilligungsfelder enthält. Lesen Sie das Lernprogramm zum [Erstellen von Datensätzen zur Erfassung der TCF 2.0-Zustimmung](./dataset-preparation.md) , um zu erfahren, wie die beiden erforderlichen Datensätze erstellt werden, bevor Sie mit diesem Handbuch fortfahren.

## Aktualisieren Sie [!DNL Profile] die Zusammenführungsrichtlinien, um die Einwilligungsdaten einzuschließen. {#merge-policies}

Nachdem Sie einen [!DNL Profile]aktivierten Datensatz für die Erfassung von Genehmigungsdaten erstellt haben, müssen Sie sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert wurden, dass stets die IAB-Einwilligungsfelder in Ihre Profil aufgenommen werden. Hierzu gehört die Festlegung der Priorität von Datasets, sodass Ihr Dataset für die Einwilligung Vorrang vor anderen möglicherweise widersprüchlichen Datensätzen hat.

Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien finden Sie im [Benutzerhandbuch](../../../profile/ui/merge-policies.md)zu Zusammenführungsrichtlinien. Beim Einrichten der Zusammenführungsrichtlinien müssen Sie sicherstellen, dass Ihre Segmente alle erforderlichen Zustimmungsattribute enthalten, die vom [XDM-Mixin für den Datenschutz](./dataset-preparation.md#privacy-mixin)bereitgestellt werden, wie im Handbuch zur Vorbereitung des Datensatzes beschrieben.

## Integrieren Sie das [!DNL Experience Platform] Web SDK, um Daten zur Kundeneinwilligung zu erfassen. {#sdk}

>[!NOTE]
>
>The use of the [!DNL Experience Platform] Web SDK is required in order to process consent data directly in Adobe Experience Platform. [!DNL Experience Cloud Identity Service] is currently not supported.
>
>[!DNL Experience Cloud Identity Service] is still supported for consent processing in Adobe Audience Manager, however, and compliance with TCF 2.0 only requires that the library is updated to [version 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Once you have configured your CMP to generate consent strings, you must integrate the [!DNL Experience Platform] Web SDK to collect those strings and send them to [!DNL Platform]. The [!DNL Platform] SDK provides two commands that can be used to send IAB consent data to Platform (explained in the subsections below), and should be used when a customer provides consent information for the first time, and anytime that consent changes thereafter.

**The SDK does not interface with any CMPs out of the box**. It is up to you to determine how to integrate the SDK into your website, listen for consent changes in the CMP, and call the appropriate command.

### Create a new edge configuration

In order for the SDK to send data to [!DNL Experience Platform], you must first create a new edge configuration for [!DNL Platform] in [!DNL Adobe Experience Platform Launch]. Specific steps for how to create a new configuration are provided in the [SDK documentation](../../../edge/fundamentals/edge-configuration.md).

After providing a unique name for the configuration, select the toggle button next to *[!UICONTROL Adobe Experience Platform]*. Next, use the following values to complete the rest of the form:

| Edge configuration field | Wert |
| --- | --- |
| [!UICONTROL Sandbox] | The name of the [!DNL Platform] [sandbox](../../../sandboxes/home.md) that contains the required streaming connection and datasets to set up the edge configuration. |
| [!UICONTROL Streaming-Inlet] | A valid streaming connection for [!DNL Experience Platform]. Informationen zum [Erstellen einer Streaming-Verbindung](../../../ingestion/tutorials/create-streaming-connection-ui.md) finden Sie im Lernprogramm, wenn Sie keinen vorhandenen Streaming-Eingang haben. |
| [!UICONTROL Ereignis DataSet] | Wählen Sie den [!DNL XDM ExperienceEvent] Datensatz aus, der im [vorherigen Schritt](#datasets)erstellt wurde. |
| [!UICONTROL Profile Dataset] | Wählen Sie den [!DNL XDM Individual Profile] Datensatz aus, der im [vorherigen Schritt](#datasets)erstellt wurde. |

![](../assets/iab/edge-config.png)

Wenn Sie fertig sind, klicken Sie unten auf dem Bildschirm auf **[!UICONTROL Speichern]** und befolgen Sie weitere Anweisungen, um die Konfiguration abzuschließen.

### Befehle zum Ändern der Zustimmung

Once you have created the edge configuration described in the previous section, you can start using SDK commands to send consent data to [!DNL Platform]. The sections below provide examples of how each SDK command can be used in different scenarios.

>[!NOTE]
>
>For an introduction to the common syntax for all [!DNL Platform] SDK commands, see the document on [executing commands](../../../edge/fundamentals/executing-commands.md).

#### Using CMP consent-change hooks

Viele CMPs bieten vordefinierte Haken, die auf Ereignisse zur Änderung der Zustimmung hören. When these events occur, you can use the `setConsent` command to update that customer&#39;s consent data.

The `setConsent` command expects two arguments: (1) a string that indicates the command type (in this case, &quot;setConsent&quot;), and (2) a payload that contains a `consent` array, which must contain at least one object that provides the required consent fields, as shown below:

```js
alloy("setConsent", {
  consent: [{
    standard: "IAB",
    version: "2.0",
    value: "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
    gdprApplies: "true"
  }]
});
```

| Payload property | Beschreibung |
| --- | --- |
| `standard` | The consent standard being used. This value must be set to &quot;IAB&quot; for TCF 2.0 consent processing. |
| `version` | The version number of the consent standard indicated under `standard`. This value must be set to &quot;2.0&quot; for TCF 2.0 consent processing. |
| `value` | The base-64-encoded consent string generated by the CMP. |
| `gdprApplies` | A Boolean value that indicates whether the GDPR applies to the currently logged-in customer. In order for TCF 2.0 to be enforced for this customer, the value must be set to &quot;true&quot;. |

The `setConsent` command should be used as part of a CMP hook that detects changes in consent settings. The following JavaScript provides an example of how the `setConsent` command can be used for OneTrust&#39;s `OnConsentChanged` hook:

```js
OneTrust.OnConsentChanged(function () {
  // Retrieve the TCF 2.0 consent data generated by the CMP, and pass it to Alloy. 
  __tcfapi("getTCData", 2, (data, success) => {
    if (success) {
      const { tcString, gdprApplies } = data;

      alloy("setConsent", {
        consent: [{
          standard: "IAB TCF",
          version: "2.0",
          value: tcString,
          gdprApplies
        }]
      });
    }
  });
});
```

#### Using events

You can also collect TCF 2.0 consent data on every event triggered in [!DNL Platform] by using the `sendEvent` command.

>[!NOTE]
>
>In order to use this method, you must have added the [!DNL Experience Event Privacy mixin] to your [!DNL Profile]-enabled [!DNL XDM ExperienceEvent] schema. See the section on [updating the ExperienceEvent schema](./dataset-preparation.md#event-schema) in the dataset preparation guide for steps on how to configure this.

The `sendEvent` command should be used as a callback in appropriate event listeners on your website. The command expects two arguments: (1) a string that indicates the command type (in this case, &quot;sendEvent&quot;), and (2) a payload containing an `xdm` object that provides the required consent fields as JSON:

```js
alloy("sendEvent", {
  xdm: {
    "consentStrings": [{
      "consentStandard": "IAB TCF",
      "consentStandardVersion": "2.0",
      "consentStringValue": "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
      "gdprApplies": true
    }]
  }
});
```

| Payload property | Beschreibung |
| --- | --- |
| `xdm.consentStrings` | An array that must contain at least one object that provides the required consent fields. |
| `consentStandard` | The consent standard being used. This value must be set to &quot;IAB&quot; for TCF 2.0 consent processing. |
| `consentStandardVersion` | The version number of the consent standard indicated under `standard`. This value must be set to &quot;2.0&quot; for TCF 2.0 consent processing. |
| `consentStringValue` | The base-64-encoded consent string generated by the CMP. |
| `gdprApplies` | A Boolean value that indicates whether the GDPR applies to the currently logged-in customer. In order for TCF 2.0 to be enforced for this customer, the value must be set to &quot;true&quot;. |

### Handling SDK responses

All [!DNL Platform SDK] commands return promises that indicate whether the call succeeded or failed. You can then use these responses for additional logic such as displaying confirmation messages to the customer. See the section on [handling success or failure](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) in the guide on executing SDK commands for specific examples.

## Export segments {#export}

>[!NOTE]
>
>Before you start exporting segments, you must ensure that your segments include all required consent fields. See the section on [configuring merge policies](#merge-policies) for more information.

Once you have collected customer consent data and have created audience segments containing the required consent attributes, you can then enforce TCF 2.0 compliance when exporting those segments to downstream destinations.

Sofern die Einstellung für die Zustimmung für eine Reihe von Profilen festgelegt `gdprApplies` `true` ist, werden alle Daten von Profilen, die in nachgelagerte Bestimmungsorte ausgeführt werden, auf der Grundlage der Voreinstellungen für die Zustimmung für jedes Profil gefiltert. Any profile that does not meet the required consent preferences is skipped during the export process.

Customers must consent to the following purposes (as outlined by [TCF 2.0 policies](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) in order for their profiles to be included in segments that are exported to destinations:

* **Purpose 1**: Store and/or access information on a device
* **Purpose 10**: Develop and improve products

TCF 2.0 also requires that the source of data must check the destination&#39;s vendor permission before sending data to that destination. As such, [!DNL Real-time CDP] checks if the destination&#39;s vendor permission is opted in to for all IDs in the cluster before including data bound to that destination.

>[!NOTE]
>
>Any segments that are shared with Adobe Audience Manager will contain the same TCF 2.0 consent values as their [!DNL Platform] counterparts. Since [!DNL Audience Manager] shares the same vendor ID as [!DNL Real-time CDP] (565), the same purposes and vendor permission are required. See the document on the [Adobe Audience Manager plug-in for IAB TCF](https://docs.adobe.com/help/de-DE/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) for more information.

## Test your implementation {#test-implementation}

Once you have configured your TCF 2.0 implementation and have exported segments to destinations, any data that does not meet consent requirements will not be exported. However, in order to see whether the right customer profiles were filtered during the export, you must manually check the data stores on your destinations to see if consent was properly enforced.

It is important to note that if multiple IDs make up a cluster and TCF 2.0 applies, the entire cluster will be excluded if even a single ID does not contain the correct purposes and vendor permission(s).

## Nächste Schritte

This document covered the process of configuring your data operations in [!DNL Real-time CDP] to be compliant with TCF 2.0. For more information on the other privacy capabilities provided by [!DNL Real-time CDP], refer to the following documentation:

* [Datenschutz in der Echtzeit-Kundendatenplattform](../privacy-overview.md)
* [Data Governance in der Echtzeit-Kundendatenplattform](../data-governance-overview.md)