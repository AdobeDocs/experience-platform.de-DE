---
keywords: Experience Platform;home;IAB;IAB 2.0;
solution: Experience Platform
title: IAB TCF 2.0 support in Real-time Customer Data Platform
topic: privacy events
translation-type: tm+mt
source-git-commit: 28106d5db179e71f47b7e071b359ffe4934a3bbe
workflow-type: tm+mt
source-wordcount: '2388'
ht-degree: 2%

---


# IAB TCF 2.0 support in [!DNL Real-time Customer Data Platform]

The [!DNL Transparency & Consent Framework] (TCF), as outlined by the [!DNL Interactive Advertising Bureau] (IAB), is an open-standard technical framework intended to enable organizations to obtain, record, and update consumer consent for the processing of their personal data, in compliance with the European Union&#39;s [!DNL General Data Protection Regulation] (GDPR). Die zweite Iteration des Rahmens, TCF 2.0, bietet mehr Flexibilität bei der Bereitstellung oder Zurückhaltung der Zustimmung durch die Verbraucher, einschließlich der Frage, ob und wie Anbieter bestimmte Merkmale der Datenverarbeitung, wie z. B. eine genaue Geolokation, nutzen können.

>[!NOTE]
>
>More information on TCF 2.0 can be found on the [IAB Europe website](https://iabeurope.eu/tcf-2-0/), including support materials and technical specifications.

[!DNL Real-time Customer Data Platform (Real-time CDP)] is part of the registered [IAB TCF 2.0 vendor list](https://iabeurope.eu/vendor-list-tcf-v2-0/), under the ID **565**. In compliance with TCF 2.0 requirements, [!DNL Real-time CDP] allows you to collect customer consent data and integrate it into your stored customer profiles. Diese Daten zur Einwilligung können dann je nach Anwendungsfall in die Segmente der exportierten Audience einbezogen werden.

>[!IMPORTANT]
>
>[!DNL Real-time CDP] kann nur mit Version 2.0 des TCF (oder höher) übereinstimmen. Previous versions of TCF are not supported.

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
   * [SDK-Zustimmungsbefehle](../../../edge/fundamentals/supporting-consent.md): Eine Gebrauchsanweisung zu den einwilligungsbezogenen SDK-Befehlen, die in diesem Handbuch gezeigt werden.
* [Adobe Experience Platform-Segmentierungsdienst](../../../segmentation/home.md): Ermöglicht es Ihnen, [!DNL Real-time Customer Profile] Daten in Gruppen von Einzelpersonen zu unterteilen, die ähnliche Eigenschaften aufweisen und ähnlich wie Marketingstrategien reagieren.

Neben den oben aufgeführten [!DNL Platform] Diensten sollten Sie auch mit [Zielen](../../destinations/destinations-overview.md) und deren Verwendung in vertraut sein [!DNL Real-time CDP].

## Übersicht zum Ablauf der Kundengenehmigung {#summary}

In den folgenden Abschnitten wird beschrieben, wie Daten zur Einwilligung erfasst und erzwungen werden, nachdem das System ordnungsgemäß konfiguriert wurde.

### Datenerfassung mit Zustimmung

[!DNL Real-time CDP] ermöglicht Ihnen die Erfassung von Daten zur Kundeneinwilligung durch den folgenden Prozess:

1. Ein Kunde gibt seine Einwilligung in die Datenerfassung durch einen Dialog auf Ihrer Website.
1. Ihr CMP erkennt die Änderung der Einwilligungsvoreinstellung und generiert die IAB-Einwilligungsdaten entsprechend.
1. Mithilfe der [!DNL Experience Platform Web SDK]werden die (vom CMP zurückgesendeten) Daten zur erteilten Zustimmung an Adobe Experience Platform gesendet.
1. Die erfassten Daten zur Einwilligung werden in einen [!DNL Profile]aktivierten Datensatz aufgenommen, dessen Schema die IAB-Einwilligungsfelder enthält.

Zusätzlich zu den SDK-Befehlen, die durch CMP-Zugriffs-Änderungs-Haken ausgelöst werden, können die Genehmigungsdaten auch [!DNL Experience Platform] durch kundengenerierte XDM-Daten fließen, die direkt in einen [!DNL Profile]aktivierten Datensatz hochgeladen werden.

Alle Segmente, die [!DNL Platform] von Adobe Audience Manager (über den [!DNL Audience Manager] Quell-Connector oder anderweitig) gemeinsam genutzt werden, können auch Zustimmungsdaten enthalten, sofern die entsprechenden Felder über [!DNL Experience Cloud Identity Service]die entsprechenden Felder auf diese Segmente angewendet wurden. Weitere Informationen zum Sammeln von Genehmigungsdaten finden Sie [!DNL Audience Manager]im Dokument zum [Adobe Audience Manager-Plug-in für IAB TCF](https://docs.adobe.com/help/de-DE/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Durchsetzung von Genehmigungen

Nach der erfolgreichen Erfassung der IAB-Genehmigungsdaten werden die folgenden Prozesse in nachgelagerten [!DNL Real-time CDP] Diensten durchgeführt:

1. [!DNL Real-time Customer Profile] aktualisiert die gespeicherten Einwilligungsdaten für das Profil des Kunden.
1. [!DNL Real-time CDP] verarbeitet Kunden-IDs nur, wenn die Herstellerberechtigung für [!DNL Real-time CDP] (565) für jede ID in einem Cluster bereitgestellt wird.
1. Beim Exportieren von Segmenten in Ziele, die zu Mitgliedern der TCF 2.0-Anbieter-Liste gehören, werden [!DNL Real-time CDP] nur Profil einbezogen, wenn die Herstellerberechtigungen für [!DNL Real-time CDP] (565) *und* das Ziel für jede ID in einem Cluster bereitgestellt werden.

Die übrigen Abschnitte in diesem Dokument enthalten Anleitungen zur Konfiguration [!DNL Real-time CDP] und Ausführung Ihrer Datenvorgänge, um die oben beschriebenen Anforderungen an die Erfassung und Durchsetzung zu erfüllen.

## Ermitteln Sie, wie Daten zur Kundengenehmigung in Ihrem CMP generiert werden. {#consent-data}

Da jedes CMP-System einzigartig ist, müssen Sie die beste Methode festlegen, um Ihren Kunden die Zustimmung zu geben, während sie mit Ihrem Service interagieren. Eine gängige Möglichkeit hierfür ist die Verwendung eines Cookie-Einwilligungsdialogs, ähnlich dem folgenden Beispiel:

![](../assets/iab/cmp-dialog.png)

Dieser Dialog muss es dem Kunden ermöglichen, Folgendes zu Opt-in oder auszuschließen:

| Option &quot;Zustimmung&quot; | Beschreibung |
| --- | --- |
| **Zweck** | Purposes define which ad tech purposes a brand can use a customer&#39;s data for. The following purposes must be opted into in order for [!DNL Real-time CDP] to process customer IDs: <ul><li>**Purpose 1**: Store and/or access information on a device</li><li>**Purpose 10**: Develop and improve products</li></ul> |
| **Herstellerberechtigungen** | Zusätzlich zu den Zwecken der Anzeigentechnologie muss der Dialog dem Kunden auch ermöglichen, seine Daten von bestimmten Anbietern, einschließlich [!DNL  Real-time CDP] (565), Opt-in zu verwenden oder zu verlieren. |

### Zustimmungszeichenfolgen {#consent-strings}

Unabhängig von der Methode, die Sie zur Datenerfassung verwenden, besteht das Ziel darin, einen Zeichenfolgenwert zu generieren, der auf den vom Kunden gewählten Zustimmungsoptionen basiert, die als **Zustimmungszeichenfolge** bezeichnet werden.

In der TCF-Spezifikation werden Zustimmungszeichenfolgen verwendet, um relevante Details über die Einstellungen für die Zustimmung eines Kunden zu kodieren, in Bezug auf spezifische Marketingzwecke, die von Richtlinien und Anbietern definiert werden. [!DNL Real-time CDP] nutzt diese Zeichenfolgen, um die Einstellungen für die Einwilligung für jeden Kunden zu speichern. Daher muss bei jeder Änderung dieser Einstellungen eine neue Zeichenfolge für die Einwilligung generiert werden.

Consent strings may only be created by a CMP that is registered with the IAB TCF. For more information on how to generate consent strings using your particular CMP, refer to the [consent string formatting guide](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) in the IAB TCF GitHub repo.

## Create datasets with IAB consent fields {#datasets}

Customer consent data must be sent to a datasets whose schema contains IAB consent fields. Refer to the tutorial on [creating datasets for capturing TCF 2.0 consent](./dataset-preparation.md) for how to create the two required datasets before continuing with this guide.

## Aktualisieren Sie [!DNL Profile] die Zusammenführungsrichtlinien, um die Einwilligungsdaten einzuschließen. {#merge-policies}

Once you have created a [!DNL Profile]-enabled dataset for collecting consent data, you must ensure that your merge policies have been configured to always include IAB consent fields in your customer profiles. This involves setting dataset precedence so that your consent dataset is prioritized over other potentially conflicting datasets.

For more information on how to work with merge policies, refer to the [merge policies user guide](../../../profile/ui/merge-policies.md). When setting up your merge policies, you must ensure that your segments include all the required consent attributes provided by the [XDM privacy mixin](./dataset-preparation.md#privacy-mixin), as outlined in the guide on dataset preparation.

## Integrieren Sie das [!DNL Experience Platform] Web SDK, um Daten zur Kundeneinwilligung zu erfassen. {#sdk}

>[!NOTE]
>
>The use of the [!DNL Experience Platform] Web SDK is required in order to process consent data directly in Adobe Experience Platform. [!DNL Experience Cloud Identity Service] is currently not supported.
>
>[!DNL Experience Cloud Identity Service] wird jedoch weiterhin für die Verarbeitung der Zustimmung in Adobe Audience Manager unterstützt, und die Einhaltung von TCF 2.0 erfordert nur, dass die Bibliothek auf [Version 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases)aktualisiert wird.

Nachdem Sie Ihre CMP zur Generierung von Zustimmungszeichenfolgen konfiguriert haben, müssen Sie das [!DNL Experience Platform] Web SDK integrieren, um diese Zeichenfolgen zu erfassen und sie an [!DNL Platform]zu senden. Das [!DNL Platform] SDK stellt zwei Befehle bereit, die zum Senden von IAB-Genehmigungsdaten an die Plattform verwendet werden können (wie in den folgenden Unterabschnitten erläutert). Sie sollten verwendet werden, wenn ein Kunde zum ersten Mal Informationen zur Einwilligung bereitstellt, und jedes Mal, wenn sich die Zustimmung danach ändert.

**Das SDK kann nicht standardmäßig mit CMPs verknüpft werden**. Es liegt an Ihnen, zu bestimmen, wie das SDK in Ihre Website integriert werden soll, auf Änderungen der Zustimmung im CMP zu hören und den entsprechenden Befehl aufzurufen.

### Neue Edge-Konfiguration erstellen

Damit das SDK Daten an senden kann, müssen Sie zunächst eine neue Edge-Konfiguration für [!DNL Experience Platform]In erstellen [!DNL Platform] [!DNL Adobe Experience Platform Launch]. Spezifische Schritte zum Erstellen einer neuen Konfiguration finden Sie in der [SDK-Dokumentation](../../../edge/fundamentals/edge-configuration.md).

Nachdem Sie einen eindeutigen Namen für die Konfiguration angegeben haben, klicken Sie auf die Umschalter neben *[!UICONTROL Adobe Experience Platform]*. Verwenden Sie anschließend die folgenden Werte, um den Rest des Formulars auszufüllen:

| Edge-Konfigurationsfeld | Wert |
| --- | --- |
| [!UICONTROL Sandbox] | Der Name der [!DNL Platform] Sandbox [](../../../sandboxes/home.md) , die die erforderliche Streaming-Verbindung und die zum Einrichten der Edge-Konfiguration erforderlichen Datensätze enthält. |
| [!UICONTROL Streaming-Inlet] | Eine gültige Streaming-Verbindung für [!DNL Experience Platform]. Informationen zum [Erstellen einer Streaming-Verbindung](../../../ingestion/tutorials/create-streaming-connection-ui.md) finden Sie im Lernprogramm, wenn Sie keinen vorhandenen Streaming-Eingang haben. |
| [!UICONTROL Ereignis DataSet] | Wählen Sie den [!DNL XDM ExperienceEvent] Datensatz aus, der im [vorherigen Schritt](#datasets)erstellt wurde. |
| [!UICONTROL Profil DataSet] | Wählen Sie den [!DNL XDM Individual Profile] Datensatz aus, der im [vorherigen Schritt](#datasets)erstellt wurde. |

![](../assets/iab/edge-config.png)

Wenn Sie fertig sind, klicken Sie unten auf dem Bildschirm auf **[!UICONTROL Speichern]** und befolgen Sie weitere Anweisungen, um die Konfiguration abzuschließen.

### Befehle zum Ändern der Zustimmung

Nachdem Sie die im vorherigen Abschnitt beschriebene Edge-Konfiguration erstellt haben, können Sie mithilfe von SDK-Befehlen Beginn zum Senden von Genehmigungsdaten an [!DNL Platform]erstellen. Die folgenden Abschnitte enthalten Beispiele dafür, wie jeder SDK-Befehl in verschiedenen Szenarien verwendet werden kann.

>[!NOTE]
>
>Eine Einführung in die allgemeine Syntax für alle [!DNL Platform] SDK-Befehle finden Sie im Dokument zum [Ausführen von Befehlen](../../../edge/fundamentals/executing-commands.md).

#### Verwenden von CMP-Haken zum Ändern der Zustimmung

Viele CMPs bieten vordefinierte Haken, die auf Ereignisse zur Änderung der Zustimmung hören. Wenn diese Ereignis auftreten, können Sie den `setConsent` Befehl verwenden, um die Einwilligungsdaten des Kunden zu aktualisieren.

Der `setConsent` Befehl erwartet zwei Argumente: (1) eine Zeichenfolge, die den Befehlstyp angibt (in diesem Fall &quot;setConsent&quot;), und (2) eine Nutzlast, die ein `consent` Array enthält, das mindestens ein Objekt enthalten muss, das die erforderlichen Felder für die Zustimmung bereitstellt, wie unten dargestellt:

```js
alloy("setConsent", {
  consent: [{
    standard: "IAB TCF",
    version: "2.0",
    value: "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
    gdprApplies: "true"
  }]
});
```

| Payload-Eigenschaft | Beschreibung |
| --- | --- |
| `standard` | Der verwendete Zustimmungsstandard. Dieser Wert muss für die Verarbeitung der TCF 2.0-Zustimmung auf &quot;IAB&quot;gesetzt werden. |
| `version` | Die Versionsnummer des Zustimmungsstandards unter `standard`. Dieser Wert muss für die Verarbeitung der TCF 2.0-Zustimmung auf &quot;2.0&quot;gesetzt werden. |
| `value` | Die Base-64-kodierte Zustimmungszeichenfolge, die vom CMP generiert wurde. |
| `gdprApplies` | Ein boolescher Wert, der angibt, ob der GDPR für den derzeit angemeldeten Kunden gilt. Damit TCF 2.0 für diesen Kunden erzwungen wird, muss der Wert auf &quot;true&quot;gesetzt werden. |

Der `setConsent` Befehl sollte als Teil eines CMP-Hakens verwendet werden, der Änderungen in den Einstellungen für die Zustimmung erkennt. Das folgende JavaScript zeigt, wie der `setConsent` Befehl für den OneTrust- `OnConsentChanged` Haken verwendet werden kann:

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
>In order to use this method, you must have added the [!DNL Experience Event Privacy mixin] to your [!DNL Profile]-enabled [!DNL XDM ExperienceEvent] schema. Anweisungen zum Konfigurieren finden Sie im Abschnitt zum [Aktualisieren des ExperienceEvent-Schemas](./dataset-preparation.md#event-schema) im Vorbereitungshandbuch für den Datensatz.

The `sendEvent` command should be used as a callback in appropriate event listeners on your website. Der Befehl erwartet zwei Argumente: (1) eine Zeichenfolge, die den Befehlstyp angibt (in diesem Fall &quot;sendEvent&quot;), und (2) eine Payload, die ein `xdm` Objekt enthält, das die erforderlichen Felder für die Zustimmung als JSON bereitstellt:

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

| Payload-Eigenschaft | Beschreibung |
| --- | --- |
| `xdm.consentStrings` | Ein Array, das mindestens ein Objekt enthalten muss, das die erforderlichen Felder für die Zustimmung bereitstellt. |
| `consentStandard` | Der verwendete Zustimmungsstandard. Dieser Wert muss für die Verarbeitung der TCF 2.0-Zustimmung auf &quot;IAB&quot;gesetzt werden. |
| `consentStandardVersion` | The version number of the consent standard indicated under `standard`. This value must be set to &quot;2.0&quot; for TCF 2.0 consent processing. |
| `consentStringValue` | The base-64-encoded consent string generated by the CMP. |
| `gdprApplies` | A Boolean value that indicates whether the GDPR applies to the currently logged-in customer. In order for TCF 2.0 to be enforced for this customer, the value must be set to &quot;true&quot;. |

### Umgang mit SDK-Antworten

All [!DNL Platform SDK] commands return promises that indicate whether the call succeeded or failed. You can then use these responses for additional logic such as displaying confirmation messages to the customer. See the section on [handling success or failure](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) in the guide on executing SDK commands for specific examples.

## Export segments {#export}

>[!NOTE]
>
>Before you start exporting segments, you must ensure that your segments include all required consent fields. Weitere Informationen finden Sie im Abschnitt zum [Konfigurieren von Zusammenführungsrichtlinien](#merge-policies) .

Once you have collected customer consent data and have created audience segments containing the required consent attributes, you can then enforce TCF 2.0 compliance when exporting those segments to downstream destinations.

Sofern die Einstellung für die Zustimmung für eine Reihe von Profilen festgelegt `gdprApplies` `true` ist, werden alle Daten von Profilen, die in nachgelagerte Bestimmungsorte ausgeführt werden, auf der Grundlage der Voreinstellungen für die Zustimmung für jedes Profil gefiltert. Jedes Profil, das die erforderlichen Voreinstellungen für die Zustimmung nicht erfüllt, wird während des Exportvorgangs übersprungen.

Die Kunden müssen den folgenden Zwecken zustimmen (wie in den [TCF 2.0-Richtlinien](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)beschrieben), damit ihre Profil in Segmente aufgenommen werden, die nach Bestimmungsorten exportiert werden:

* **Zweck 1**: Store- und/oder Zugriffsinformationen auf einem Gerät
* **Zweck 10**: Entwicklung und Verbesserung von Produkten

Für TCF 2.0 ist außerdem erforderlich, dass die Datenquelle vor dem Senden der Daten an dieses Ziel die Herstellerberechtigung des Ziels überprüfen muss. Daher wird [!DNL Real-time CDP] überprüft, ob die Herstellerberechtigung des Ziels für alle IDs im Cluster aktiviert ist, bevor Daten mit diesem Ziel verknüpft werden.

>[!NOTE]
>
>Alle Segmente, die für Adobe Audience Manager freigegeben werden, enthalten dieselben TCF 2.0-Zustimmungswerte wie ihre [!DNL Platform] Gegenstücke. Da [!DNL Audience Manager] dieselbe Anbieter-ID wie [!DNL Real-time CDP] (565) verwendet wird, sind dieselben Zwecke und die gleiche Herstellerberechtigung erforderlich. Weitere Informationen finden Sie im Dokument zum [Adobe Audience Manager-Plug-in für IAB TCF](https://docs.adobe.com/help/de-DE/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) .

## Test your implementation {#test-implementation}

Nachdem Sie Ihre TCF 2.0-Implementierung konfiguriert und Segmente an Ziele exportiert haben, werden Daten, die die Anforderungen für die Zustimmung nicht erfüllen, nicht exportiert. Um jedoch festzustellen, ob die richtigen Kundendaten während des Exports gefiltert wurden, müssen Sie die Datenspeicher Ihrer Profil manuell überprüfen, um festzustellen, ob die Zustimmung ordnungsgemäß durchgesetzt wurde.

Beachten Sie, dass bei mehreren IDs, aus denen ein Cluster besteht und bei denen TCF 2.0 angewendet wird, der gesamte Cluster ausgeschlossen wird, wenn selbst eine einzelne ID nicht die richtigen Zwecke und die richtige(n) Herstellerberechtigung(en) enthält.

## Nächste Schritte

In diesem Dokument wurde der Prozess der Konfiguration Ihrer Datenvorgänge im Hinblick auf die Kompatibilität mit TCF 2.0 behandelt. [!DNL Real-time CDP] Weitere Informationen zu den anderen Datenschutzfunktionen [!DNL Real-time CDP]finden Sie in der folgenden Dokumentation:

* [Datenschutz in der Echtzeit-Kundendatenplattform](../privacy-overview.md)
* [Data Governance in der Echtzeit-Kundendatenplattform](../data-governance-overview.md)