---
keywords: Experience Platform;home;IAB;IAB 2.0;
solution: Experience Platform
title: Unterstützung von IAB TCF 2.0 in der Echtzeit-Plattform für Kundendaten
topic: privacy events
translation-type: tm+mt
source-git-commit: 06eda1502d34da1caeebbe9b753dd437bbd9d6ab
workflow-type: tm+mt
source-wordcount: '2388'
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
* [Adobe Experience Platform Web SDK](../../../edge/home.md): A client-side JavaScript library that allows you to integrate various [!DNL Platform] services into your customer-facing website.
   * [SDK consent commands](../../../edge/fundamentals/supporting-consent.md): A use-case overview of the consent-related SDK commands shown in this guide.
* [Adobe Experience Platform Segmentation Service](../../../segmentation/home.md): Allows you to divide [!DNL Real-time Customer Profile] data into groups of individuals that share similar traits and will respond similarly to marketing strategies.

In addition to the [!DNL Platform] services listed above, you should also be familiar with [destinations](../../destinations/destinations-overview.md) and their use in [!DNL Real-time CDP].

## Übersicht zum Ablauf der Kundengenehmigung {#summary}

In den folgenden Abschnitten wird beschrieben, wie Daten zur Einwilligung erfasst und erzwungen werden, nachdem das System ordnungsgemäß konfiguriert wurde.

### Datenerfassung mit Zustimmung

[!DNL Real-time CDP] ermöglicht Ihnen die Erfassung von Daten zur Kundeneinwilligung durch den folgenden Prozess:

1. Ein Kunde gibt seine Einwilligung in die Datenerfassung durch einen Dialog auf Ihrer Website.
1. Your CMP detects the consent preference change, and generates IAB consent data accordingly.
1. Mithilfe der [!DNL Experience Platform Web SDK]werden die (vom CMP zurückgesendeten) Daten zur erteilten Zustimmung an Adobe Experience Platform gesendet.
1. The collected consent data is ingested into a [!DNL Profile]-enabled dataset whose schema contains IAB consent fields.

In addition to SDK commands triggered by CMP consent-change hooks, consent data can also flow into [!DNL Experience Platform] through any customer-generated XDM data that is uploaded directly to a [!DNL Profile]-enabled dataset.

Any segments shared with [!DNL Platform] by Adobe Audience Manager (through the [!DNL Audience Manager] source connector or otherwise) may also contain consent data, provided that the appropriate fields have been applied to those segments through [!DNL Experience Cloud Identity Service]. For more information on collecting consent data in [!DNL Audience Manager], see the document on the [Adobe Audience Manager plug-in for IAB TCF](https://docs.adobe.com/help/de-DE/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Durchsetzung von Genehmigungen

Once IAB consent data has successfully been ingested, the following processes take place in downstream [!DNL Real-time CDP] services:

1. [!DNL Real-time Customer Profile] updates the stored consent data for that customer&#39;s profile.
1. [!DNL Real-time CDP] processes customer IDs only if the vendor permission for [!DNL Real-time CDP] (565) is provided for every ID in a cluster.
1. When exporting segments to destinations belonging to members of the TCF 2.0 vendor list, [!DNL Real-time CDP] only includes profiles if the vendor permissions for both [!DNL Real-time CDP] (565) *and* the destination is provided for every ID in a cluster.

The rest of the sections in this document provide guidance on how to configure [!DNL Real-time CDP] and your data operations to fulfill the collection and enforcement requirements described above.

## Determine how to generate customer consent data within your CMP {#consent-data}

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
>Die Verwendung des [!DNL Experience Platform] Web SDK ist erforderlich, um die Daten der Zustimmung direkt in Adobe Experience Platform zu verarbeiten. [!DNL Experience Cloud Identity Service] wird derzeit nicht unterstützt.
>
>[!DNL Experience Cloud Identity Service] wird jedoch weiterhin für die Verarbeitung der Zustimmung in Adobe Audience Manager unterstützt, und die Einhaltung von TCF 2.0 erfordert nur, dass die Bibliothek auf [Version 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases)aktualisiert wird.

Nachdem Sie Ihre CMP zur Generierung von Zustimmungszeichenfolgen konfiguriert haben, müssen Sie das [!DNL Experience Platform] Web SDK integrieren, um diese Zeichenfolgen zu erfassen und sie an [!DNL Platform]zu senden. Das [!DNL Platform] SDK stellt zwei Befehle bereit, die zum Senden von IAB-Genehmigungsdaten an die Plattform verwendet werden können (wie in den folgenden Unterabschnitten erläutert). Sie sollten verwendet werden, wenn ein Kunde zum ersten Mal Informationen zur Einwilligung bereitstellt, und jedes Mal, wenn sich die Zustimmung danach ändert.

**Das SDK kann nicht standardmäßig mit CMPs verknüpft werden**. Es liegt an Ihnen, zu bestimmen, wie das SDK in Ihre Website integriert werden soll, auf Änderungen der Zustimmung im CMP zu hören und den entsprechenden Befehl aufzurufen.

### Neue Edge-Konfiguration erstellen

Damit das SDK Daten an senden kann, müssen Sie zunächst eine neue Edge-Konfiguration für [!DNL Experience Platform]In erstellen [!DNL Platform] [!DNL Adobe Experience Platform Launch]. Spezifische Schritte zum Erstellen einer neuen Konfiguration finden Sie in der [SDK-Dokumentation](../../../edge/fundamentals/edge-configuration.md).

Nachdem Sie einen eindeutigen Namen für die Konfiguration angegeben haben, klicken Sie auf die Umschalter neben *[!UICONTROL Adobe Experience Platform]*. Next, use the following values to complete the rest of the form:

| Edge-Konfigurationsfeld | Wert |
| --- | --- |
| [!UICONTROL Sandbox] | The name of the [!DNL Platform] [sandbox](../../../sandboxes/home.md) that contains the required streaming connection and datasets to set up the edge configuration. |
| [!UICONTROL Streaming Inlet] | Eine gültige Streaming-Verbindung für [!DNL Experience Platform]. See the tutorial on [creating a streaming connection](../../../ingestion/tutorials/create-streaming-connection-ui.md) if you do not have an existing streaming inlet. |
| [!UICONTROL Ereignis DataSet] | Wählen Sie den [!DNL XDM ExperienceEvent] Datensatz aus, der im [vorherigen Schritt](#datasets)erstellt wurde. |
| [!UICONTROL Profil DataSet] | Wählen Sie den [!DNL XDM Individual Profile] Datensatz aus, der im [vorherigen Schritt](#datasets)erstellt wurde. |

![](../assets/iab/edge-config.png)

Wenn Sie fertig sind, klicken Sie unten auf dem Bildschirm auf **[!UICONTROL Speichern]** und befolgen Sie weitere Anweisungen, um die Konfiguration abzuschließen.

### Befehle zum Ändern der Zustimmung

Once you have created the edge configuration described in the previous section, you can start using SDK commands to send consent data to [!DNL Platform]. The sections below provide examples of how each SDK command can be used in different scenarios.

>[!NOTE]
>
>For an introduction to the common syntax for all [!DNL Platform] SDK commands, see the document on [executing commands](../../../edge/fundamentals/executing-commands.md).

#### Using CMP consent-change hooks

Many CMPs provide out-of-the-box hooks that listen to consent-change events. Wenn diese Ereignis auftreten, können Sie den `setConsent` Befehl verwenden, um die Einwilligungsdaten des Kunden zu aktualisieren.

The `setConsent` command expects two arguments: (1) a string that indicates the command type (in this case, &quot;setConsent&quot;), and (2) a payload that contains a `consent` array, which must contain at least one object that provides the required consent fields, as shown below:

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

| Payload property | Beschreibung |
| --- | --- |
| `standard` | The consent standard being used. This value must be set to &quot;IAB&quot; for TCF 2.0 consent processing. |
| `version` | The version number of the consent standard indicated under `standard`. This value must be set to &quot;2.0&quot; for TCF 2.0 consent processing. |
| `value` | Die Base-64-kodierte Zustimmungszeichenfolge, die vom CMP generiert wurde. |
| `gdprApplies` | Ein boolescher Wert, der angibt, ob der GDPR für den derzeit angemeldeten Kunden gilt. Damit TCF 2.0 für diesen Kunden erzwungen wird, muss der Wert auf &quot;true&quot;gesetzt werden. |

Der `setConsent` Befehl sollte als Teil eines CMP-Hakens verwendet werden, der Änderungen in den Einstellungen für die Zustimmung erkennt. Das folgende JavaScript zeigt, wie der `setConsent` Befehl für den OneTrust- `OnConsentChanged` Haken verwendet werden kann:

```js
OneTrust.OnConsentChanged(function () {
  // Retrieve the TCF 2.0 consent data generated by the CMP, and pass it to Alloy. 
  __tcfapi("getTCData", 2, function (data, success) {
    if (success) {
      var tcString = data.tcString;
      var gdpr = data.gdprApplies;

      alloy("setConsent", {
        consent: [{
          standard: "IAB TCF",
          version: "2.0",
          value: tcString,
          gdprApplies: gdpr
        }]
      });
    }
  });
});
```

#### Ereignisse verwenden

Sie können auch Daten zur TCF 2.0-Einwilligung zu jedem Ereignis erfassen, das [!DNL Platform] durch den `sendEvent` Befehl ausgelöst wird.

>[!NOTE]
>
>Um diese Methode verwenden zu können, müssen Sie die [!DNL Experience Event Privacy mixin] zu Ihrem [!DNL Profile]aktivierten [!DNL XDM ExperienceEvent] Schema hinzugefügt haben. Anweisungen zum Konfigurieren finden Sie im Abschnitt zum [Aktualisieren des ExperienceEvent-Schemas](./dataset-preparation.md#event-schema) im Vorbereitungshandbuch für den Datensatz.

Der `sendEvent` Befehl sollte als Rückruf in entsprechenden Ereignis-Listenern auf Ihrer Website verwendet werden. Der Befehl erwartet zwei Argumente: (1) eine Zeichenfolge, die den Befehlstyp angibt (in diesem Fall &quot;sendEvent&quot;), und (2) eine Payload, die ein `xdm` Objekt enthält, das die erforderlichen Felder für die Zustimmung als JSON bereitstellt:

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
| `consentStandardVersion` | Die Versionsnummer des Zustimmungsstandards unter `standard`. Dieser Wert muss für die Verarbeitung der TCF 2.0-Zustimmung auf &quot;2.0&quot;gesetzt werden. |
| `consentStringValue` | Die Base-64-kodierte Zustimmungszeichenfolge, die vom CMP generiert wurde. |
| `gdprApplies` | Ein boolescher Wert, der angibt, ob der GDPR für den derzeit angemeldeten Kunden gilt. Damit TCF 2.0 für diesen Kunden erzwungen wird, muss der Wert auf &quot;true&quot;gesetzt werden. |

### Umgang mit SDK-Antworten

Alle [!DNL Platform SDK] Befehle geben Versprechungen zurück, die angeben, ob der Aufruf erfolgreich war oder fehlgeschlagen ist. Sie können diese Antworten dann für zusätzliche Logik verwenden, z. B. für die Anzeige von Bestätigungsmeldungen an den Kunden. Genaue Beispiele finden Sie im Abschnitt zum [Umgang mit Erfolg oder Fehlern](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) im Handbuch zum Ausführen von SDK-Befehlen.

## Segmente exportieren {#export}

>[!NOTE]
>
>Bevor Sie Beginn exportieren, müssen Sie sicherstellen, dass Ihre Segmente alle erforderlichen Felder für die Zustimmung enthalten. Weitere Informationen finden Sie im Abschnitt zum [Konfigurieren von Zusammenführungsrichtlinien](#merge-policies) .

Nachdem Sie Daten zur Kundengenehmigung gesammelt und Segmente mit den erforderlichen Genehmigungsattributen erstellt haben, können Sie die TCF 2.0-Konformität erzwingen, wenn Sie diese Audiencen an nachgelagerte Ziele exportieren.

Sofern die Einstellung für die Zustimmung für eine Reihe von Profilen festgelegt `gdprApplies` `true` ist, werden alle Daten von Profilen, die in nachgelagerte Bestimmungsorte ausgeführt werden, auf der Grundlage der Voreinstellungen für die Zustimmung für jedes Profil gefiltert. Jedes Profil, das die erforderlichen Voreinstellungen für die Zustimmung nicht erfüllt, wird während des Exportvorgangs übersprungen.

Die Kunden müssen den folgenden Zwecken zustimmen (wie in den [TCF 2.0-Richtlinien](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)beschrieben), damit ihre Profil in Segmente aufgenommen werden, die nach Bestimmungsorten exportiert werden:

* **Zweck 1**: Store- und/oder Zugriffsinformationen auf einem Gerät
* **Zweck 10**: Entwicklung und Verbesserung von Produkten

Für TCF 2.0 ist außerdem erforderlich, dass die Datenquelle vor dem Senden der Daten an dieses Ziel die Herstellerberechtigung des Ziels überprüfen muss. Daher wird [!DNL Real-time CDP] überprüft, ob die Herstellerberechtigung des Ziels für alle IDs im Cluster aktiviert ist, bevor Daten mit diesem Ziel verknüpft werden.

>[!NOTE]
>
>Any segments that are shared with Adobe Audience Manager will contain the same TCF 2.0 consent values as their [!DNL Platform] counterparts. Since [!DNL Audience Manager] shares the same vendor ID as [!DNL Real-time CDP] (565), the same purposes and vendor permission are required. See the document on the [Adobe Audience Manager plug-in for IAB TCF](https://docs.adobe.com/help/de-DE/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) for more information.

## Test your implementation {#test-implementation}

Once you have configured your TCF 2.0 implementation and have exported segments to destinations, any data that does not meet consent requirements will not be exported. Um jedoch festzustellen, ob die richtigen Kundendaten während des Exports gefiltert wurden, müssen Sie die Datenspeicher Ihrer Profil manuell überprüfen, um festzustellen, ob die Zustimmung ordnungsgemäß durchgesetzt wurde.

Beachten Sie, dass bei mehreren IDs, aus denen ein Cluster besteht und bei denen TCF 2.0 angewendet wird, der gesamte Cluster ausgeschlossen wird, wenn selbst eine einzelne ID nicht die richtigen Zwecke und die richtige(n) Herstellerberechtigung(en) enthält.

## Nächste Schritte

In diesem Dokument wurde der Prozess der Konfiguration Ihrer Datenvorgänge im Hinblick auf die Kompatibilität mit TCF 2.0 behandelt. [!DNL Real-time CDP] Weitere Informationen zu den anderen Datenschutzfunktionen [!DNL Real-time CDP]finden Sie in der folgenden Dokumentation:

* [Datenschutz in der Echtzeit-Kundendatenplattform](../privacy-overview.md)
* [Data Governance in der Echtzeit-Kundendatenplattform](../data-governance-overview.md)