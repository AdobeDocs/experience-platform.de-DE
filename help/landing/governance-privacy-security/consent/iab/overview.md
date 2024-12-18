---
keywords: Experience Platform;home;IAB;IAB 2.0;consent;Consensus
solution: Experience Platform
title: IAB TCF 2.0-Unterstützung für Experience Platform
description: Erfahren Sie, wie Sie Ihre Datenvorgänge und Schemata konfigurieren, um bei der Aktivierung von Segmenten für Ziele in Adobe Experience Platform Auswahlmöglichkeiten für die Kundenzustimmung zu vermitteln.
role: Developer
feature: Consent
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '2492'
ht-degree: 1%

---

# IAB TCF 2.0-Unterstützung für Experience Platform

Der im [!DNL Interactive Advertising Bureau] (IAB) beschriebene [!DNL Transparency & Consent Framework] (TCF) ist ein offener technischer Rahmen, der Organisationen die Erlangung, Aufzeichnung und Aktualisierung der Einwilligung der Verbraucher zur Verarbeitung ihrer personenbezogenen Daten gemäß der DSGVO (2) der Europäischen Union ermöglichen soll. [!DNL General Data Protection Regulation] Die zweite Iteration des Frameworks, TCF 2.0, bietet mehr Flexibilität dafür, wie Verbraucher ihre Zustimmung erteilen oder verweigern können, einschließlich der Frage, ob und wie Anbieter bestimmte Funktionen der Datenverarbeitung, wie z. B. die genaue Geolokation, nutzen können.

>[!NOTE]
>
>Weitere Informationen zu TCF 2.0 finden Sie auf der [IAB Europe-Website](https://iabeurope.eu/), einschließlich Unterstützungsmaterialien und technischer Spezifikationen.

Adobe Experience Platform ist Teil der registrierten Lieferantenliste [IAB TCF 2.0 ](https://iabeurope.eu/vendor-list-tcf/) unter der ID **565**. In Übereinstimmung mit den TCF 2.0-Anforderungen können Sie mit Platform Daten zur Kundenzustimmung erfassen und in Ihre gespeicherten Kundenprofile integrieren. Diese Einwilligungsdaten können dann je nach Anwendungsfall in exportierte Zielgruppensegmente einbezogen werden.

>[!IMPORTANT]
>
>Platform kann nur Version 2.0 des TCF (oder höher) erfüllen. Frühere Versionen von TCF werden nicht unterstützt.

Dieses Dokument bietet einen Überblick darüber, wie Sie Ihre Datenvorgänge und Profilschemata so konfigurieren können, dass von Ihrer Consent Management Platform (CMP) generierte Kundenzustimmungsdaten akzeptiert werden. Außerdem wird behandelt, wie Platform beim Exportieren von Segmenten Entscheidungen bezüglich der Benutzerzustimmung vermittelt.

## Voraussetzungen

Um diesem Handbuch zu folgen, müssen Sie eine kommerzielle oder eigene CMP verwenden, die mit dem IAB TCF integriert und konform ist. Weitere Informationen finden Sie in der [Liste der kompatiblen CMPs](https://iabeurope.eu/cmp-list/) .

>[!IMPORTANT]
>
>Wenn die ID Ihres CMP ungültig ist, verarbeitet Platform Ihre Daten unverändert. Um TCF 2.0 zu erzwingen, müssen Sie sicherstellen, dass Ihre CMP über eine gültige ID verfügt, die beim IAB TCF 2.0 registriert wurde, bevor Daten an Platform gesendet werden.

Dieses Handbuch setzt außerdem ein Verständnis der folgenden Platform-Dienste voraus:

* [Experience-Datenmodell (XDM)](/help/xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Adobe Experience Platform Identity Service](/help/identity-service/home.md): Löst die grundlegende Herausforderung, die sich aus der Fragmentierung von Kundenerlebnisdaten ergibt, indem Identitäten zwischen Geräten und Systemen überbrückt werden.
* [Echtzeit-Kundenprofil](/help/profile/home.md): Mit [!DNL Identity Service] können Sie aus Ihren Datensätzen detaillierte Kundenprofile in Echtzeit erstellen. [!DNL Real-Time Customer Profile] ruft Daten aus dem Data Lake ab und behält Kundenprofile in seinem eigenen separaten Datenspeicher bei.
* [Adobe Experience Platform Web SDK](/help/web-sdk/home.md): Eine Client-seitige JavaScript-Bibliothek, mit der Sie verschiedene Platform-Dienste in Ihre kundenorientierte Website integrieren können.
   * [SDK-Zustimmungsbefehle](../../../../web-sdk/commands/setconsent.md): Eine Anwendungsfallübersicht der einwilligungsbezogenen SDK-Befehle, die in diesem Handbuch gezeigt werden.
* [Adobe Experience Platform Segmentation Service](/help/segmentation/home.md): Ermöglicht die Aufteilung von [!DNL Real-Time Customer Profile] -Daten in Gruppen von Einzelanwendern, die ähnliche Eigenschaften aufweisen und ähnlich wie Marketingstrategien reagieren.

Zusätzlich zu den oben aufgeführten Platform-Diensten sollten Sie auch mit [Zielen](/help/data-governance/home.md) und ihrer Rolle im Platform-Ökosystem vertraut sein.

## Übersicht über die Kundenzustimmungen {#summary}

In den folgenden Abschnitten wird beschrieben, wie Einwilligungsdaten erfasst und durchgesetzt werden, nachdem das System ordnungsgemäß konfiguriert wurde.

### Einverständnisdatenerfassung

Platform ermöglicht die Erfassung von Daten zur Einwilligung von Kunden mithilfe des folgenden Prozesses:

1. Ein Kunde gibt seine Zustimmungseinstellungen für die Datenerfassung über ein Dialogfeld auf Ihrer Website an.
1. Ihr CMP erkennt die Änderung der Zustimmungsvoreinstellung und generiert dementsprechend TCF-Zustimmungsdaten.
1. Mithilfe des Platform Web SDK werden die (vom CMP zurückgegebenen) generierten Zustimmungsdaten an Adobe Experience Platform gesendet.
1. Die erfassten Einwilligungsdaten werden in einen [!DNL Profile]-aktivierten Datensatz aufgenommen, dessen Schema TCF-Einwilligungsfelder enthält.

Zusätzlich zu den SDK-Befehlen, die von CMP-Zustimmungs-Change-Hooks ausgelöst werden, können Zustimmungsdaten auch über alle kundengenerierten XDM-Daten in Experience Platform fließen, die direkt in einen [!DNL Profile]-aktivierten Datensatz hochgeladen werden.

Alle Segmente, die von Adobe Audience Manager (über den Quell-Connector [!DNL Audience Manager] oder anderweitig mit Platform gemeinsam verwendet werden), können auch Einwilligungsdaten enthalten, wenn die entsprechenden Felder über [!DNL Experience Cloud Identity Service] auf diese Segmente angewendet wurden. Weitere Informationen zum Erfassen von Einwilligungsdaten in [!DNL Audience Manager] finden Sie im Dokument zum [Adobe Audience Manager-Plug-in für IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=de).

### Durchsetzung der nachgelagerten Zustimmung

Sobald die TCF-Zustimmungsdaten erfolgreich erfasst wurden, finden die folgenden Prozesse in nachgelagerten Platform-Diensten statt:

1. [!DNL Real-Time Customer Profile] aktualisiert die gespeicherten Zustimmungsdaten für das Profil dieses Kunden.
1. Platform verarbeitet Kunden-IDs nur, wenn die Anbieterberechtigung für Platform (565) für jede ID in einem Cluster bereitgestellt wird.
1. Beim Exportieren von Segmenten in Ziele, die zu Mitgliedern der TCF 2.0-Anbieterliste gehören, enthält Platform nur Profile, wenn die Anbieterberechtigungen für beide Platform (565) *und* für das jeweilige Ziel für jede ID in einem Cluster bereitgestellt werden.

Die übrigen Abschnitte in diesem Dokument enthalten Anleitungen dazu, wie Sie Platform und Ihre Datenvorgänge so konfigurieren, dass die oben beschriebenen Anforderungen an die Erfassung und Durchsetzung erfüllt werden.

## Ermitteln, wie Sie in Ihrem CMP Kundenzustimmungsdaten generieren {#consent-data}

Da jedes CMP-System einzigartig ist, müssen Sie festlegen, wie Ihre Kunden bei der Interaktion mit Ihrem Dienst am besten ihre Zustimmung erteilen können. Ein Dialogfeld für die Cookie-Zustimmung ist eine gängige Methode, um die Zustimmung des Kunden zu erhalten. Unten finden Sie ein Beispiel-CMP-Dialogfeld.

![Ein Beispiel für ein Dialogfeld für die Verwaltung von Einwilligungen.](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Dieser Dialog muss es dem Kunden ermöglichen, sich an Folgendem zu beteiligen oder abzuwählen:

| Zustimmungsoption | Beschreibung |
| --- | --- |
| **Zweck** | Zweck definiert, für welche Werbetechnologiezwecke eine Marke die Daten eines Kunden verwenden kann. Die folgenden Zwecke müssen in aktiviert werden, damit Platform Kunden-IDs verarbeiten kann: <ul><li>**Zweck 1**: Informationen auf einem Gerät speichern und/oder darauf zugreifen</li><li>**Zweck 10**: Entwicklung und Verbesserung von Produkten</li></ul> |
| **Berechtigungen des Anbieters** | Zusätzlich zu den Werbetechnologiezwecken muss das Dialogfeld auch dem Kunden die Möglichkeit bieten, seine Daten von bestimmten Anbietern, einschließlich Adobe Experience Platform (565), zu verwenden oder abzulehnen. |

### Zustimmungszeichenfolgen {#consent-strings}

Unabhängig von der Methode, mit der Sie die Daten erfassen, besteht das Ziel darin, einen Zeichenfolgenwert zu generieren, der auf den Zustimmungsoptionen basiert, die vom Kunden ausgewählt werden und als Zustimmungszeichenfolge bezeichnet werden.

In der TCF-Spezifikation werden Zustimmungszeichenfolgen verwendet, um relevante Details zu den Zustimmungseinstellungen eines Kunden im Hinblick auf spezifische Marketing-Zwecke zu kodieren, die von Richtlinien und Anbietern definiert werden. Platform verwendet diese Zeichenfolgen, um die Zustimmungseinstellungen für jeden Kunden zu speichern. Daher muss bei jeder Änderung dieser Einstellungen eine neue Zustimmungszeichenfolge generiert werden.

Zustimmungszeichenfolgen dürfen nur von einer CMP erstellt werden, die beim IAB TCF registriert ist. Weitere Informationen zum Generieren von Zustimmungszeichenfolgen mit Ihrer jeweiligen CMP finden Sie im [Handbuch zur Formatierung von Zustimmungszeichenfolgen](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) im IAB TCF GitHub-Repository.

## Erstellen von Datensätzen mit TCF-Einwilligungsfeldern {#datasets}

Die Daten zur Kundenzustimmung müssen an Datensätze gesendet werden, deren Schemas TCF-Einwilligungsfelder enthalten. Informationen zum Erstellen des erforderlichen Profildatensatzes (und eines optionalen Experience Event-Datensatzes) finden Sie im Tutorial zum Erstellen von Datensätzen zur Erfassung der TCF-2.0-Zustimmung](./dataset.md) , bevor Sie mit diesem Handbuch fortfahren.[

## Aktualisieren von [!DNL Profile] Zusammenführungsrichtlinien zum Einschließen von Einwilligungsdaten {#merge-policies}

Nachdem Sie einen [!DNL Profile]-aktivierten Datensatz für die Erfassung von Zustimmungsdaten erstellt haben, müssen Sie sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert wurden, dass immer TCF-Einwilligungsfelder in Ihre Kundenprofile aufgenommen werden. Dazu gehört das Festlegen der Datensatzpriorität, sodass Ihr Einwilligungsdatensatz Vorrang vor anderen möglicherweise in Konflikt stehenden Datensätzen erhält.

Weiterführende Informationen zum Arbeiten mit Zusammenführungsrichtlinien finden Sie in der [Übersicht über Zusammenführungsrichtlinien](/help/profile/merge-policies/overview.md). Beim Einrichten Ihrer Zusammenführungsrichtlinien müssen Sie sicherstellen, dass Ihre Segmente alle erforderlichen Zustimmungsattribute enthalten, die von der [XDM-Datenschutzschema-Feldergruppe](./dataset.md#privacy-field-group) bereitgestellt werden, wie im Handbuch zur Vorbereitung von Datensätzen beschrieben.

## Integrieren des Experience Platform Web SDK zur Erfassung von Kundenzustimmungsdaten {#sdk}

>[!NOTE]
>
>Die Verwendung des Experience Platform Web SDK ist erforderlich, um Einwilligungsdaten direkt in Adobe Experience Platform zu verarbeiten. [!DNL Experience Cloud Identity Service] wird nicht unterstützt.
>
>[!DNL Experience Cloud Identity Service] wird weiterhin für die Zustimmungsverarbeitung in Adobe Audience Manager unterstützt. Für die Einhaltung von TCF 2.0 ist jedoch nur eine Aktualisierung der Bibliothek auf [Version 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases) erforderlich.

Nachdem Sie Ihre CMP zur Generierung von Zustimmungszeichenfolgen konfiguriert haben, müssen Sie das Experience Platform Web SDK integrieren, um diese Zeichenfolgen zu erfassen und an Platform zu senden. Das Platform SDK stellt zwei Befehle bereit, mit denen TCF-Zustimmungsdaten an Platform gesendet werden können (siehe Unterabschnitte unten). Diese Befehle sollten verwendet werden, wenn ein Kunde zum ersten Mal Einwilligungsinformationen bereitstellt, und immer dann, wenn sich die Einwilligung ändert.

**Das SDK verfügt nicht standardmäßig über eine Schnittstelle mit CMPs**. Sie müssen bestimmen, wie das SDK in Ihre Website integriert werden kann, auf Zustimmungsänderungen in der CMP warten und den entsprechenden Befehl aufrufen.

### Erstellen eines Datenspeichers

Damit das SDK Daten an Experience Platform senden kann, müssen Sie zunächst einen Datastream für Platform erstellen. Spezifische Schritte zum Erstellen eines Datastreams finden Sie in der [SDK-Dokumentation](/help/datastreams/overview.md).

Nachdem Sie einen eindeutigen Namen für den Datastream angegeben haben, wählen Sie die Umschalter-Schaltfläche neben **[!UICONTROL Adobe Experience Platform]** aus. Verwenden Sie als Nächstes die folgenden Werte, um den Rest des Formulars auszufüllen:

| Datenspeicherfeld | Wert |
| --- | --- |
| [!UICONTROL Sandbox] | Der Name der Platform [Sandbox](/help/sandboxes/home.md), die die erforderliche Streaming-Verbindung und Datensätze zum Einrichten des Datastreams enthält. |
| [!UICONTROL Streaming-Inlet] | Eine gültige Streaming-Verbindung für Experience Platform. Lesen Sie das Tutorial zum [Erstellen einer Streaming-Verbindung](/help/ingestion/tutorials/create-streaming-connection-ui.md) , wenn Sie keinen Streaming-Inlet haben. |
| [!UICONTROL Ereignis-Datensatz] | Wählen Sie den Datensatz [!DNL XDM ExperienceEvent] aus, der im vorherigen Schritt [2} erstellt wurde. ](#datasets) Wenn Sie die Feldergruppe [[!UICONTROL IAB TCF 2.0 Consent] ](/help/xdm/field-groups/event/iab.md) im Schema dieses Datensatzes eingeschlossen haben, können Sie mithilfe des Befehls [`sendEvent`](#sendEvent) Einwilligungsänderungsereignisse im Laufe der Zeit verfolgen und diese Daten in diesem Datensatz speichern. Beachten Sie, dass die in diesem Datensatz gespeicherten Zustimmungswerte **nicht** in automatischen Durchsetzungs-Workflows verwendet werden. |
| [!UICONTROL Profildatensatz] | Wählen Sie den Datensatz [!DNL XDM Individual Profile] aus, der im vorherigen Schritt [2} erstellt wurde. ](#datasets) Bei der Reaktion auf CMP-Zustimmungs-Change-Hooks mit dem Befehl [`setConsent`](#setConsent) werden die erfassten Daten in diesem Datensatz gespeichert. Da dieser Datensatz profilaktiviert ist, werden die in diesem Datensatz gespeicherten Zustimmungswerte bei automatischen Durchsetzungs-Workflows berücksichtigt. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Wenn Sie fertig sind, wählen Sie am unteren Bildschirmrand **[!UICONTROL Speichern]** und fahren Sie mit den weiteren Anweisungen fort, um die Konfiguration abzuschließen.

### Festlegen von Befehlen zur Änderung der Zustimmung

Nachdem Sie den im vorherigen Abschnitt beschriebenen Datastream erstellt haben, können Sie mit der Verwendung von SDK-Befehlen beginnen, um Zustimmungsdaten an Platform zu senden. Die folgenden Abschnitte enthalten Beispiele dafür, wie die einzelnen SDK-Befehle in verschiedenen Szenarien verwendet werden können.

#### Verwenden von CMP-Zustimmungs-Change-Hooks {#setConsent}

Viele CMPs bieten vordefinierte Hooks, die Zustimmungsänderungs-Ereignisse überwachen. Wenn diese Ereignisse eintreten, können Sie den Befehl [`setConsent`](/help/web-sdk/commands/setconsent.md) verwenden, um die Einwilligungsdaten des Kunden zu aktualisieren.

Der Befehl `setConsent` erwartet zwei Argumente:

1. Eine Zeichenfolge, die den Befehlstyp angibt (in diesem Fall &quot;setConsent&quot;).
1. Eine Payload, die ein `consent` -Array enthält. Das Array muss mindestens ein Objekt enthalten, das die erforderlichen Einwilligungsfelder bereitstellt.

Der Befehl `setConsent` wird unten angezeigt:

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
| `standard` | Der verwendete Zustimmungsstandard. Dieser Wert muss für die Verarbeitung der TCF-Zustimmung 2.0 auf `IAB` gesetzt werden. |
| `version` | Die Versionsnummer des Zustimmungsstandards, angegeben unter `standard`. Dieser Wert muss für die Verarbeitung der TCF-Zustimmung 2.0 auf `2.0` gesetzt werden. |
| `value` | Die base-64-kodierte Zustimmungszeichenfolge, die vom CMP generiert wurde. |
| `gdprApplies` | Ein boolescher Wert, der anzeigt, ob die DSGVO für den aktuell angemeldeten Kunden gilt. Damit TCF 2.0 für diesen Kunden erzwungen wird, muss der Wert auf `true` gesetzt werden. Wenn nicht definiert, wird standardmäßig `true` verwendet. |

Der Befehl `setConsent` sollte als Teil eines CMP-Hooks verwendet werden, der Änderungen in den Zustimmungseinstellungen erkennt. Im folgenden JavaScript finden Sie ein Beispiel dafür, wie der Befehl `setConsent` für den `OnConsentChanged`-Hook von OneTrust verwendet werden kann:

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

#### Ereignisse verwenden {#sendEvent}

Sie können auch TCF 2.0-Zustimmungsdaten für jedes Ereignis erfassen, das in Platform ausgelöst wird, indem Sie den Befehl `sendEvent` verwenden.

>[!NOTE]
>
>Um diese Methode verwenden zu können, müssen Sie die Feldergruppe Erlebnisereignis-Datenschutz zu Ihrem [!DNL Profile]-aktivierten [!DNL XDM ExperienceEvent] -Schema hinzugefügt haben. Anweisungen zum Konfigurieren finden Sie im Abschnitt zum Aktualisieren des ExperienceEvent-Schemas ](./dataset.md#event-schema) im Handbuch zur Datensatzvorbereitung.[

Der Befehl `sendEvent` sollte als Callback in entsprechenden Ereignis-Listenern auf Ihrer Website verwendet werden. Der Befehl erwartet zwei Argumente: (1) eine Zeichenfolge, die den Befehlstyp angibt (in diesem Fall `sendEvent`), und (2) eine Payload, die ein `xdm` -Objekt enthält, das die erforderlichen Zustimmungsfelder als JSON bereitstellt:

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
| `xdm.consentStrings` | Ein Array, das mindestens ein Objekt enthalten muss, das die erforderlichen Zustimmungsfelder bereitstellt. |
| `consentStandard` | Der verwendete Zustimmungsstandard. Dieser Wert muss für die Verarbeitung der TCF-Zustimmung 2.0 auf `IAB` gesetzt werden. |
| `consentStandardVersion` | Die Versionsnummer des Zustimmungsstandards, angegeben unter `standard`. Dieser Wert muss für die Verarbeitung der TCF-Zustimmung 2.0 auf `2.0` gesetzt werden. |
| `consentStringValue` | Die base-64-kodierte Zustimmungszeichenfolge, die vom CMP generiert wurde. |
| `gdprApplies` | Ein boolescher Wert, der anzeigt, ob die DSGVO für den aktuell angemeldeten Kunden gilt. Damit TCF 2.0 für diesen Kunden erzwungen wird, muss der Wert auf `true` gesetzt werden. Wenn nicht definiert, wird standardmäßig `true` verwendet. |

### Umgang mit SDK-Antworten

Viele Web SDK-Befehle geben Promises zurück, die angeben, ob der Aufruf erfolgreich war oder fehlgeschlagen ist. Sie können diese Antworten dann für zusätzliche Logik verwenden, z. B. für die Anzeige von Bestätigungsnachrichten an den Kunden. Weitere Informationen finden Sie unter [Befehlsantworten](/help/web-sdk/commands/command-responses.md) .

## Segmente exportieren {#export}

>[!NOTE]
>
>Bevor Sie mit dem Exportieren von Segmenten beginnen, müssen Sie sicherstellen, dass Ihre Segmente alle erforderlichen Einwilligungsfelder enthalten. Weitere Informationen finden Sie im Abschnitt [Konfigurieren von Zusammenführungsrichtlinien](#merge-policies) .

Nachdem Sie Daten zur Kundenzustimmung erfasst und Zielgruppensegmente erstellt haben, die die erforderlichen Zustimmungsattribute enthalten, können Sie die TCF 2.0-Compliance erzwingen, wenn Sie diese Segmente an nachgelagerte Ziele exportieren.

Wenn die Zustimmungseinstellung `gdprApplies` für eine Reihe von Kundenprofilen auf `true` gesetzt ist, werden alle Daten aus diesen Profilen, die an nachgelagerte Ziele exportiert werden, anhand der TCF-Zustimmungsvoreinstellungen für jedes Profil gefiltert. Jedes Profil, das nicht die erforderlichen Zustimmungseinstellungen erfüllt, wird während des Exportvorgangs übersprungen.

Kunden müssen die folgenden Zwecke (wie in den [TCF 2.0-Richtlinien](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions) beschrieben) akzeptieren, damit ihre Profile in Segmente aufgenommen werden, die nach Zielen exportiert werden:

* **Zweck 1**: Informationen auf einem Gerät speichern und/oder darauf zugreifen
* **Zweck 10**: Entwicklung und Verbesserung von Produkten

Für TCF 2.0 muss außerdem die Datenquelle die Berechtigung des Zielanbieters überprüfen, bevor Daten an dieses Ziel gesendet werden. Daher prüft Platform, ob die Berechtigung des Anbieters des Ziels für alle IDs im Cluster angemeldet ist, bevor Daten an dieses Ziel gebunden werden.

>[!NOTE]
>
>Alle Segmente, die für Adobe Audience Manager freigegeben werden, enthalten dieselben TCF 2.0-Zustimmungswerte wie ihre Platform-Gegenstücke. Da [!DNL Audience Manager] dieselbe Anbieter-ID wie Platform (565) verwendet, sind dieselben Zwecke und die Berechtigung des Anbieters erforderlich. Weitere Informationen finden Sie im Dokument zum [Adobe Audience Manager-Plug-in für IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=de) .

## Implementierung testen {#test-implementation}

Nachdem Sie Ihre TCF 2.0-Implementierung konfiguriert und Segmente an Ziele exportiert haben, werden keine Daten exportiert, die nicht den Zustimmungsanforderungen entsprechen. Um festzustellen, ob die richtigen Kundenprofile während des Exports gefiltert wurden, müssen Sie die Datenspeicher Ihrer Ziele manuell überprüfen, um festzustellen, ob die Zustimmung ordnungsgemäß durchgesetzt wurde.

>[!IMPORTANT]
>
>Wenn ein Cluster mehrere IDs umfasst und TCF 2.0 angewendet wird, wird der gesamte Cluster ausgeschlossen, wenn selbst eine einzelne ID nicht die richtigen Zwecke und Berechtigungen des Anbieters enthält.

## Nächste Schritte

In diesem Dokument wurde der Prozess der Konfiguration Ihrer Platform-Datenvorgänge zur Erfüllung Ihrer geschäftlichen Verpflichtungen gemäß TCF 2.0 beschrieben. Weitere Informationen zu den datenschutzbezogenen Funktionen von Platform finden Sie in der Übersicht zu [Governance, Datenschutz und Sicherheit](../../overview.md) .
