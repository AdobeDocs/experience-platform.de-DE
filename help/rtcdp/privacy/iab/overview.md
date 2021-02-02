---
keywords: Experience Platform;Home;IAB;IAB 2.0;Zustimmung;Zustimmung
solution: Experience Platform
title: Unterstützung von IAB TCF 2.0 in der Echtzeit-Plattform für Kundendaten
topic: privacy events
description: Erfahren Sie, wie Sie Ihre Datenvorgänge und Schema so konfigurieren, dass beim Exportieren von Segmenten in die Echtzeit-Kundendatenplattform Entscheidungen zur Benutzereinwilligung übertragen werden.
translation-type: tm+mt
source-git-commit: 1e37e8b3d540bcb503773e7c99e6e83d75980a24
workflow-type: tm+mt
source-wordcount: '2414'
ht-degree: 1%

---


# IAB TCF 2.0-Unterstützung in [!DNL Real-time Customer Data Platform]

Der nach dem IAB (a1/>) umrissene (TCF) ist ein offener technischer Rahmen, der Organisationen die Erlangung, Aufzeichnung und Aktualisierung der Zustimmung des Verbrauchers zur Verarbeitung ihrer personenbezogenen Daten gemäß den Vorgaben der Europäischen Vereinigung (GDPR) ermöglichen soll. [!DNL Transparency & Consent Framework][!DNL Interactive Advertising Bureau][!DNL General Data Protection Regulation] Die zweite Iteration des Rahmens, TCF 2.0, bietet mehr Flexibilität bei der Bereitstellung oder Zurückhaltung der Zustimmung durch die Verbraucher, einschließlich der Frage, ob und wie Anbieter bestimmte Merkmale der Datenverarbeitung, wie z. B. eine genaue Geolokation, nutzen können.

>[!NOTE]
>
>Weitere Informationen zu TCF 2.0 finden Sie auf der [IAB Europe Website](https://iabeurope.eu/tcf-2-0/), einschließlich Unterstützungsmaterialien und technischer Spezifikationen.

[!DNL Real-time Customer Data Platform (Real-time CDP)] ist Teil der registrierten  [IAB TCF 2.0 Händlerversion Liste](https://iabeurope.eu/vendor-list-tcf-v2-0/), unter der ID  **565**. [!DNL Real-time CDP] ermöglicht Ihnen gemäß den Anforderungen von TCF 2.0 die Erfassung von Daten zur Kundengenehmigung und deren Integration in Ihre gespeicherten Profil. Diese Daten zur Einwilligung können dann je nach Anwendungsfall in die Segmente der exportierten Audience einbezogen werden.

>[!IMPORTANT]
>
>[!DNL Real-time CDP] kann nur mit Version 2.0 des TCF (oder höher) übereinstimmen. Frühere Versionen von TCF werden nicht unterstützt.

Dieses Dokument bietet einen Überblick darüber, wie Sie Ihre Datenvorgänge konfigurieren und Profil-Schema zum Akzeptieren von durch Ihren CMP generierten Daten zur Kundeneinwilligung verwenden können und wie [!DNL Real-time CDP] Auswahlmöglichkeiten für die Benutzereinwilligung beim Exportieren von Segmenten vermittelt.

## Voraussetzungen

Um diesem Leitfaden zu folgen, müssen Sie entweder eine kommerzielle oder eigene Consent Management Platform (CMP) verwenden, die mit dem IAB TCF integriert und kompatibel ist. Weitere Informationen finden Sie unter [Liste der konformen CMPs](https://iabeurope.eu/cmp-list/).

>[!IMPORTANT]
>
>Wenn die ID Ihres CMP ungültig ist, verarbeitet [!DNL Real-time CDP] Ihre Daten unverändert. Um TCF 2.0 durchzusetzen, müssen Sie vor dem Senden von Daten an [!DNL Experience Platform] bestätigen, dass Ihr CMP über eine gültige ID verfügt, die bei IAB TCF 2.0 registriert wurde.

Dieser Leitfaden erfordert auch ein Verständnis der folgenden Adobe Experience Platform-Dienste:

* [Experience-Datenmodell (XDM)](../../../xdm/home.md)[!DNL Experience Platform]: Das standardisierte Framework, mit dem Kundenerlebnisdaten organisiert.
* [Adobe Experience Platform-Identitätsdienst](../../../identity-service/home.md): Löst die grundlegende Herausforderung, die sich aus der Fragmentierung von Kundenerlebnisdaten ergibt, indem Identitäten zwischen Geräten und Systemen überbrückt werden.
* [Echtzeit-Profil](../../../profile/home.md): Ermöglicht  [!DNL Identity Service] die Erstellung detaillierter Kundendaten aus Ihren Datensätzen in Echtzeit. [!DNL Real-time Customer Profile] ruft Daten aus dem Data Lake ab und behält die Profil der Kunden in einem eigenen separaten Datenspeicher bei.
* [Adobe Experience Platform Web SDK](../../../edge/home.md): Eine clientseitige JavaScript-Bibliothek, mit der Sie verschiedene  [!DNL Platform] Dienste in Ihre kundenorientierte Website integrieren können.
   * [SDK-Zustimmungsbefehle](../../../edge/consent/supporting-consent.md): Eine Gebrauchsanweisung zu den einwilligungsbezogenen SDK-Befehlen, die in diesem Handbuch gezeigt werden.
* [Adobe Experience Platform-Segmentierungsdienst](../../../segmentation/home.md): Ermöglicht es Ihnen,  [!DNL Real-time Customer Profile] Daten in Gruppen von Einzelpersonen zu unterteilen, die ähnliche Eigenschaften aufweisen und ähnlich wie Marketingstrategien reagieren.

Zusätzlich zu den oben aufgeführten [!DNL Platform]-Diensten sollten Sie auch mit [Zielen](../../destinations/overview.md) und deren Verwendung in [!DNL Real-time CDP] vertraut sein.

## Zusammenfassung zum Ablauf der Kundengenehmigung {#summary}

In den folgenden Abschnitten wird beschrieben, wie Daten zur Einwilligung erfasst und erzwungen werden, nachdem das System ordnungsgemäß konfiguriert wurde.

### Datenerfassung mit Zustimmung

[!DNL Real-time CDP] ermöglicht Ihnen die Erfassung von Daten zur Kundeneinwilligung durch den folgenden Prozess:

1. Ein Kunde gibt seine Einwilligung in die Datenerfassung durch einen Dialog auf Ihrer Website.
1. Ihr CMP erkennt die Änderung der Einwilligungsvoreinstellung und generiert die IAB-Einwilligungsdaten entsprechend.
1. Mit dem [!DNL Experience Platform Web SDK] werden die (vom CMP zurückgesendeten) Daten der generierten Zustimmung an Adobe Experience Platform gesendet.
1. Die erfassten Daten zur Einwilligung werden in einen [!DNL Profile]-aktivierten Datensatz aufgenommen, dessen Schema die IAB-Einwilligungsfelder enthält.

Zusätzlich zu den SDK-Befehlen, die durch CMP-Zugriffs-Change-Haken ausgelöst werden, können Genehmigungsdaten auch über kundengenerierte XDM-Daten in [!DNL Experience Platform] fließen, die direkt in ein [!DNL Profile]-aktiviertes Dataset hochgeladen werden.

Alle Segmente, die mit [!DNL Platform] von Adobe Audience Manager (über den [!DNL Audience Manager]-Quellanschluss oder anderweitig) freigegeben werden, können auch Genehmigungsdaten enthalten, sofern die entsprechenden Felder über [!DNL Experience Cloud Identity Service] auf diese Segmente angewendet wurden. Weitere Informationen zum Sammeln von Genehmigungsdaten in [!DNL Audience Manager] finden Sie im Dokument zum [Adobe Audience Manager-Plugin für IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Durchsetzung von Genehmigungen

Nachdem die IAB-Genehmigungsdaten erfolgreich erfasst wurden, finden die folgenden Prozesse in nachgelagerten [!DNL Real-time CDP]-Diensten statt:

1. [!DNL Real-time Customer Profile] aktualisiert die gespeicherten Einwilligungsdaten für das Profil des Kunden.
1. [!DNL Real-time CDP] verarbeitet Kunden-IDs nur, wenn die Herstellerberechtigung für  [!DNL Real-time CDP] (565) für jede ID in einem Cluster bereitgestellt wird.
1. Beim Exportieren von Segmenten in Ziele, die zu Mitgliedern der TCF 2.0-Anbieter-Liste gehören, enthält [!DNL Real-time CDP] nur Profil, wenn die Händlerberechtigungen für [!DNL Real-time CDP] (565) *und* für jede ID in einem Cluster bereitgestellt werden.

Die übrigen Abschnitte in diesem Dokument enthalten Anleitungen zur Konfiguration von [!DNL Real-time CDP] und Ihren Datenvorgängen zur Erfüllung der oben beschriebenen Anforderungen an die Erfassung und Durchsetzung.

## Ermitteln Sie, wie Daten zur Kundengenehmigung in Ihrem CMP generiert werden.{#consent-data}

Da jedes CMP-System einzigartig ist, müssen Sie die beste Methode festlegen, um Ihren Kunden die Zustimmung zu geben, während sie mit Ihrem Service interagieren. Eine gängige Möglichkeit hierfür ist die Verwendung eines Cookie-Einwilligungsdialogs, ähnlich dem folgenden Beispiel:

![](../assets/iab/cmp-dialog.png)

Dieser Dialog muss es dem Kunden ermöglichen, Folgendes zu Opt-in oder auszuschließen:

| Option &quot;Zustimmung&quot; | Beschreibung |
| --- | --- |
| **Zweck** | Zweck definiert, für welche Ad-Tech-Zwecke eine Marke die Daten eines Kunden verwenden kann. Für die Verarbeitung von Kunden-IDs müssen die folgenden Zwecke gewählt werden:[!DNL Real-time CDP] <ul><li>**Zweck 1**: Store- und/oder Zugriffsinformationen auf einem Gerät</li><li>**Zweck 10**: Entwicklung und Verbesserung von Produkten</li></ul> |
| **Herstellerberechtigungen** | Zusätzlich zu den Anzeigentechnologien muss der Dialog es dem Kunden ermöglichen, seine Daten von bestimmten Anbietern, einschließlich [!DNL  Real-time CDP] (565), Opt-in oder zu verwenden. |

### Zustimmungszeichenfolgen {#consent-strings}

Unabhängig von der Methode, die Sie zur Datenerfassung verwenden, besteht das Ziel darin, einen Zeichenfolgenwert zu generieren, der auf den vom Kunden gewählten Zustimmungsoptionen basiert, die so genannte Einwilligungszeichenfolge.

In der TCF-Spezifikation werden Zustimmungszeichenfolgen verwendet, um relevante Details über die Einstellungen für die Zustimmung eines Kunden zu kodieren, in Bezug auf spezifische Marketingzwecke, die von Richtlinien und Anbietern definiert werden. [!DNL Real-time CDP] nutzt diese Zeichenfolgen, um die Einstellungen für die Einwilligung für jeden Kunden zu speichern. Daher muss bei jeder Änderung dieser Einstellungen eine neue Zeichenfolge für die Einwilligung generiert werden.

Zustimmungszeichenfolgen können nur von einem CMP erstellt werden, der bei der IAB-TCF registriert ist. Weitere Informationen zum Generieren von Zustimmungszeichenfolgen mit Ihrem jeweiligen CMP finden Sie im Handbuch [zur Formatierung der Einwilligungszeichenfolge](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) im IAB TCF GitHub-Repo.

## Erstellen von Datensätzen mit IAB-Genehmigungsfeldern {#datasets}

Die Daten zur Kundengenehmigung müssen an Datensätze gesendet werden, deren Schemas die IAB-Einwilligungsfelder enthalten. Lesen Sie das Lernprogramm zum Erstellen von Datensätzen zum Erfassen von TCF 2.0-Einwilligungen](./dataset-preparation.md), um zu erfahren, wie die beiden erforderlichen Datensätze erstellt werden, bevor Sie mit diesem Handbuch fortfahren.[

## [!DNL Profile]-Zusammenführungsrichtlinien aktualisieren, um Einwilligungsdaten einzuschließen {#merge-policies}

Nachdem Sie einen [!DNL Profile]-aktivierten Datensatz für die Erfassung von Genehmigungsdaten erstellt haben, müssen Sie sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert wurden, dass sie stets IAB-Einwilligungsfelder in Ihre Profil aufnehmen. Hierzu gehört die Festlegung der Priorität von Datasets, sodass Ihr Dataset für die Einwilligung Vorrang vor anderen möglicherweise widersprüchlichen Datensätzen hat.

Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien finden Sie im Benutzerhandbuch [Richtlinien zusammenführen](../../../profile/ui/merge-policies.md). Beim Einrichten der Zusammenführungsrichtlinien müssen Sie sicherstellen, dass Ihre Segmente alle erforderlichen Zustimmungsattribute enthalten, die vom [XDM Privacy mixin](./dataset-preparation.md#privacy-mixin) bereitgestellt werden, wie im Handbuch zur Vorbereitung des Datensatzes beschrieben.

## Integrieren Sie das [!DNL Experience Platform] Web SDK, um Daten zur Kundeneinwilligung zu erfassen. {#sdk}

>[!NOTE]
>
>Die Verwendung des [!DNL Experience Platform] Web SDK ist erforderlich, um die Einwilligungsdaten direkt in Adobe Experience Platform zu verarbeiten. [!DNL Experience Cloud Identity Service] wird derzeit nicht unterstützt.
>
>[!DNL Experience Cloud Identity Service] wird jedoch weiterhin für die Verarbeitung der Zustimmung in Adobe Audience Manager unterstützt, und die Einhaltung von TCF 2.0 erfordert nur, dass die Bibliothek auf  [Version 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases) aktualisiert wird.

Nachdem Sie Ihre CMP zur Generierung von Zustimmungszeichenfolgen konfiguriert haben, müssen Sie das [!DNL Experience Platform] Web SDK integrieren, um diese Zeichenfolgen zu erfassen und sie an [!DNL Platform] zu senden. Das [!DNL Platform]-SDK stellt zwei Befehle bereit, die zum Senden von IAB-Genehmigungsdaten an Platform verwendet werden können (wie in den unten stehenden Unterabschnitten erläutert), und sollten verwendet werden, wenn ein Kunde zum ersten Mal Informationen zur Einwilligung bereitstellt, und jedes Mal, wenn sich die Zustimmung danach ändert.

**Das SDK kann nicht standardmäßig mit CMPs verknüpft werden**. Es liegt an Ihnen, zu bestimmen, wie das SDK in Ihre Website integriert werden soll, auf Änderungen der Zustimmung im CMP zu hören und den entsprechenden Befehl aufzurufen.

### Neue Edge-Konfiguration erstellen

Damit das SDK Daten an [!DNL Experience Platform] senden kann, müssen Sie zunächst eine neue Edge-Konfiguration für [!DNL Platform] in [!DNL Adobe Experience Platform Launch] erstellen. Spezifische Schritte zum Erstellen einer neuen Konfiguration finden Sie in der [SDK-Dokumentation](../../../edge/fundamentals/edge-configuration.md).

Nachdem Sie einen eindeutigen Namen für die Konfiguration angegeben haben, klicken Sie auf die Schaltfläche zum Umschalten neben **[!UICONTROL Adobe Experience Platform]**. Verwenden Sie anschließend die folgenden Werte, um den Rest des Formulars auszufüllen:

| Edge-Konfigurationsfeld | Wert |
| --- | --- |
| [!UICONTROL Sandbox] | Der Name der [!DNL Platform] [Sandbox](../../../sandboxes/home.md), die die erforderliche Streaming-Verbindung und die für die Einrichtung der Edge-Konfiguration erforderlichen Datensätze enthält. |
| [!UICONTROL Streaming-Inlet] | Eine gültige Streaming-Verbindung für [!DNL Experience Platform]. Sehen Sie sich das Lernprogramm unter [Erstellen einer Streaming-Verbindung](../../../ingestion/tutorials/create-streaming-connection-ui.md) an, wenn Sie keinen vorhandenen Streaming-Einlass haben. |
| [!UICONTROL Ereignis DataSet] | Wählen Sie den Datensatz [!DNL XDM ExperienceEvent] aus, der im [vorherigen Schritt](#datasets) erstellt wurde. |
| [!UICONTROL Profil DataSet] | Wählen Sie den Datensatz [!DNL XDM Individual Profile] aus, der im [vorherigen Schritt](#datasets) erstellt wurde. |

![](../assets/iab/edge-config.png)

Wenn Sie fertig sind, wählen Sie unten im Bildschirm **[!UICONTROL Speichern]** und folgen Sie den weiteren Eingabeaufforderungen, um die Konfiguration abzuschließen.

### Befehle zum Ändern der Zustimmung

Nachdem Sie die im vorherigen Abschnitt beschriebene Edge-Konfiguration erstellt haben, können Sie mit SDK-Befehlen Beginn ausführen, um Genehmigungsdaten an [!DNL Platform] zu senden. Die folgenden Abschnitte enthalten Beispiele dafür, wie jeder SDK-Befehl in verschiedenen Szenarien verwendet werden kann.

>[!NOTE]
>
>Eine Einführung in die allgemeine Syntax für alle SDK-Befehle finden Sie im Dokument [Ausführungsbefehle](../../../edge/fundamentals/executing-commands.md).[!DNL Platform]

#### Verwenden von CMP-Haken zum Ändern der Zustimmung

Viele CMPs bieten vordefinierte Haken, die auf Ereignisse zur Änderung der Zustimmung hören. Wenn diese Ereignis auftreten, können Sie mit dem Befehl `setConsent` die Daten für die Zustimmung des Kunden aktualisieren.

Der Befehl `setConsent` erwartet zwei Argumente: (1) eine Zeichenfolge, die den Befehlstyp angibt (in diesem Fall &quot;setConsent&quot;), und (2) eine Nutzlast, die ein `consent`-Array enthält, das mindestens ein Objekt enthalten muss, das die erforderlichen Felder für die Zustimmung bereitstellt, wie unten dargestellt:

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
| `version` | Die Versionsnummer des Zustimmungsstandards, die unter `standard` angegeben ist. Dieser Wert muss für die Verarbeitung der TCF 2.0-Zustimmung auf &quot;2.0&quot;gesetzt werden. |
| `value` | Die Base-64-kodierte Zustimmungszeichenfolge, die vom CMP generiert wurde. |
| `gdprApplies` | Ein boolescher Wert, der angibt, ob der GDPR für den derzeit angemeldeten Kunden gilt. Damit TCF 2.0 für diesen Kunden erzwungen wird, muss der Wert auf &quot;true&quot;gesetzt werden. |

Der Befehl `setConsent` sollte als Teil eines CMP-Hook verwendet werden, der Änderungen in den Einstellungen für die Zustimmung erkennt. Das folgende JavaScript bietet ein Beispiel dafür, wie der Befehl `setConsent` für den `OnConsentChanged`-Haken von OneTrust verwendet werden kann:

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

Sie können auch mit dem Befehl `sendEvent` TCF 2.0-Einwilligungsdaten für jedes in [!DNL Platform] ausgelöste Ereignis erfassen.

>[!NOTE]
>
>Um diese Methode verwenden zu können, müssen Sie dem [!DNL Profile]-aktivierten [!DNL XDM ExperienceEvent]-Schema [!DNL Experience Event Privacy mixin] den Wert  hinzugefügt haben. Anweisungen zum Konfigurieren finden Sie im Abschnitt zum Aktualisieren des ExperienceEvent-Schemas](./dataset-preparation.md#event-schema) im DataSet-Vorbereitungshandbuch.[

Der Befehl `sendEvent` sollte als Rückruf in entsprechenden Ereignis-Listenern auf Ihrer Website verwendet werden. Der Befehl erwartet zwei Argumente: (1) eine Zeichenfolge, die den Befehlstyp angibt (in diesem Fall &quot;sendEvent&quot;), und (2) eine Payload, die ein `xdm`-Objekt enthält, das die erforderlichen Felder für die Zustimmung als JSON bereitstellt:

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
| `consentStandardVersion` | Die Versionsnummer des Zustimmungsstandards, die unter `standard` angegeben ist. Dieser Wert muss für die Verarbeitung der TCF 2.0-Zustimmung auf &quot;2.0&quot;gesetzt werden. |
| `consentStringValue` | Die Base-64-kodierte Zustimmungszeichenfolge, die vom CMP generiert wurde. |
| `gdprApplies` | Ein boolescher Wert, der angibt, ob der GDPR für den derzeit angemeldeten Kunden gilt. Damit TCF 2.0 für diesen Kunden erzwungen wird, muss der Wert auf &quot;true&quot;gesetzt werden. |

### Umgang mit SDK-Antworten

Alle [!DNL Platform SDK]-Befehle geben Versprechungen zurück, die angeben, ob der Aufruf erfolgreich war oder fehlgeschlagen ist. Sie können diese Antworten dann für zusätzliche Logik verwenden, z. B. für die Anzeige von Bestätigungsmeldungen an den Kunden. Genaue Beispiele finden Sie im Abschnitt [Handhabung von Erfolg oder Fehler](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) im Handbuch zum Ausführen von SDK-Befehlen.

## Segmente {#export} exportieren

>[!NOTE]
>
>Bevor Sie Beginn exportieren, müssen Sie sicherstellen, dass Ihre Segmente alle erforderlichen Felder für die Zustimmung enthalten. Weitere Informationen finden Sie im Abschnitt [Konfigurieren von Zusammenführungsrichtlinien](#merge-policies).

Nachdem Sie Daten zur Kundengenehmigung gesammelt und Segmente mit den erforderlichen Genehmigungsattributen erstellt haben, können Sie die TCF 2.0-Konformität erzwingen, wenn Sie diese Audiencen an nachgelagerte Ziele exportieren.

Sofern die Einstellung für die Zustimmung `gdprApplies` für eine Reihe von Profilen auf `true` eingestellt ist, werden alle Daten aus den Profilen, die in nachgelagerte Ziele exportiert werden, basierend auf den Voreinstellungen für die Zustimmung für jedes Profil gefiltert. Jedes Profil, das die erforderlichen Voreinstellungen für die Zustimmung nicht erfüllt, wird während des Exportvorgangs übersprungen.

Die Kunden müssen den folgenden Zwecken zustimmen (wie in den Richtlinien [TCF 2.0 ](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions) beschrieben), damit ihre Profil in Segmente aufgenommen werden, die in Ziele exportiert werden:

* **Zweck 1**: Store- und/oder Zugriffsinformationen auf einem Gerät
* **Zweck 10**: Entwicklung und Verbesserung von Produkten

Für TCF 2.0 ist außerdem erforderlich, dass die Datenquelle vor dem Senden der Daten an dieses Ziel die Herstellerberechtigung des Ziels überprüfen muss. [!DNL Real-time CDP] überprüft daher, ob die Herstellerberechtigung des Ziels für alle IDs im Cluster aktiviert ist, bevor Daten mit diesem Ziel verknüpft werden.

>[!NOTE]
>
>Alle Segmente, die für Adobe Audience Manager freigegeben werden, enthalten dieselben TCF 2.0-Zustimmungswerte wie ihre [!DNL Platform]-Entsprechungen. Da [!DNL Audience Manager] dieselbe Anbieter-ID wie [!DNL Real-time CDP] (565) verwendet, sind dieselben Zwecke und die gleiche Herstellerberechtigung erforderlich. Weitere Informationen finden Sie im Dokument zum [Adobe Audience Manager-Plugin für IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

## Testen Sie Ihre Implementierung {#test-implementation}

Nachdem Sie Ihre TCF 2.0-Implementierung konfiguriert und Segmente an Ziele exportiert haben, werden Daten, die die Anforderungen für die Zustimmung nicht erfüllen, nicht exportiert. Um jedoch festzustellen, ob die richtigen Kundendaten während des Exports gefiltert wurden, müssen Sie die Datenspeicher Ihrer Profil manuell überprüfen, um festzustellen, ob die Zustimmung ordnungsgemäß durchgesetzt wurde.

Beachten Sie, dass bei mehreren IDs, aus denen ein Cluster besteht und bei denen TCF 2.0 angewendet wird, der gesamte Cluster ausgeschlossen wird, wenn selbst eine einzelne ID nicht die richtigen Zwecke und die richtige(n) Herstellerberechtigung(en) enthält.

## Nächste Schritte

Dieses Dokument behandelte den Prozess der Konfiguration Ihrer Datenvorgänge in [!DNL Real-time CDP], um mit TCF 2.0 konform zu sein. Weitere Informationen zu den anderen Datenschutzfunktionen von [!DNL Real-time CDP] finden Sie in der folgenden Dokumentation:

* [Datenschutz in der Echtzeit-Kundendatenplattform](../privacy-overview.md)
* [Data Governance in der Echtzeit-Kundendatenplattform](../data-governance-overview.md)