---
keywords: Experience Platform;home;IAB;IAB 2.0;consent;Consensus
solution: Experience Platform
title: IAB TCF 2.0-Unterstützung für Experience Platform
topic-legacy: privacy events
description: Erfahren Sie, wie Sie Ihre Datenvorgänge und Schemata konfigurieren, um bei der Aktivierung von Segmenten für Ziele in Adobe Experience Platform Auswahlmöglichkeiten für die Kundenzustimmung zu vermitteln.
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: da7696d288543abd21ff8a1402e81dcea32efbc2
workflow-type: tm+mt
source-wordcount: '2559'
ht-degree: 0%

---

# IAB TCF 2.0-Unterstützung für Experience Platform

Das [!DNL Transparency & Consent Framework] (TCF), wie im [!DNL Interactive Advertising Bureau] (IAB) beschrieben, ist ein offener technischer Rahmen, der Organisationen die Erlangung, Aufzeichnung und Aktualisierung der Einwilligung der Verbraucher zur Verarbeitung ihrer personenbezogenen Daten gemäß der [!DNL General Data Protection Regulation] (DSGVO) der Europäischen Union ermöglichen soll. Die zweite Iteration des Frameworks, TCF 2.0, bietet mehr Flexibilität dafür, wie Verbraucher ihre Zustimmung erteilen oder verweigern können, einschließlich der Frage, ob und wie Anbieter bestimmte Funktionen der Datenverarbeitung, wie z. B. die genaue Geolokation, nutzen können.

>[!NOTE]
>
>Weitere Informationen zu TCF 2.0 finden Sie auf der [IAB Europe-Website](https://iabeurope.eu/tcf-2-0/), einschließlich Unterstützungsmaterialien und technischer Spezifikationen.

Adobe Experience Platform ist Teil der registrierten [IAB TCF 2.0-Anbieterliste](https://iabeurope.eu/vendor-list-tcf-v2-0/) unter der ID **565**. In Übereinstimmung mit den TCF 2.0-Anforderungen können Sie mit Platform Daten zur Kundenzustimmung erfassen und in Ihre gespeicherten Kundenprofile integrieren. Diese Einwilligungsdaten können dann je nach Anwendungsfall in exportierte Zielgruppensegmente einbezogen werden.

>[!IMPORTANT]
>
>Platform kann nur Version 2.0 des TCF (oder höher) erfüllen. Frühere Versionen von TCF werden nicht unterstützt.

Dieses Dokument bietet einen Überblick darüber, wie Sie Ihre Datenvorgänge und Profilschemata so konfigurieren können, dass von Ihrem CMP generierte Kundenzustimmungsdaten akzeptiert werden, und wie Platform beim Exportieren von Segmenten Auswahlmöglichkeiten bezüglich der Benutzerzustimmung nutzt.

## Voraussetzungen

Um diesem Handbuch zu folgen, müssen Sie eine kommerzielle oder eigene Consent Management Platform (CMP) verwenden, die mit dem IAB TCF integriert und kompatibel ist. Weitere Informationen finden Sie in der [Liste der kompatiblen CMPs](https://iabeurope.eu/cmp-list/).

>[!IMPORTANT]
>
>Wenn die ID Ihres CMP ungültig ist, verarbeitet Platform Ihre Daten unverändert. Um TCF 2.0 zu erzwingen, müssen Sie sicherstellen, dass Ihre CMP über eine gültige ID verfügt, die beim IAB TCF 2.0 registriert wurde, bevor Daten an Platform gesendet werden.

Dieses Handbuch setzt außerdem ein Verständnis der folgenden Platform-Dienste voraus:

* [Experience-Datenmodell (XDM)](../../../../xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Adobe Experience Platform Identity-Dienst](../../../../identity-service/home.md): Löst die grundlegende Herausforderung, die sich aus der Fragmentierung von Kundenerlebnisdaten ergibt, indem Identitäten zwischen Geräten und Systemen überbrückt werden.
* [Echtzeit-Kundenprofil](../../../../profile/home.md): Ermöglicht  [!DNL Identity Service] die Erstellung detaillierter Kundenprofile aus Ihren Datensätzen in Echtzeit. [!DNL Real-time Customer Profile] ruft Daten aus dem Data Lake ab und behält Kundenprofile in einem eigenen separaten Datenspeicher bei.
* [Adobe Experience Platform Web SDK](../../../../edge/home.md): Eine Client-seitige JavaScript-Bibliothek, mit der Sie verschiedene Platform-Dienste in Ihre kundenorientierte Website integrieren können.
   * [SDK-Zustimmungsbefehle](../../../../edge/consent/supporting-consent.md): Eine Anwendungsfallübersicht der einwilligungsbezogenen SDK-Befehle, die in diesem Handbuch gezeigt werden.
* [Adobe Experience Platform Segmentation Service](../../../../segmentation/home.md): Ermöglicht die Unterteilung von  [!DNL Real-time Customer Profile] Daten in Gruppen von Einzelanwendern, die ähnliche Eigenschaften aufweisen und ähnlich auf Marketing-Strategien reagieren.

Zusätzlich zu den oben aufgeführten Platform-Diensten sollten Sie auch mit [Zielen](../../../../data-governance/home.md) und ihrer Rolle im Platform-Ökosystem vertraut sein.

## Übersicht über die Kundenzustimmungen {#summary}

In den folgenden Abschnitten wird beschrieben, wie Einwilligungsdaten erfasst und durchgesetzt werden, nachdem das System ordnungsgemäß konfiguriert wurde.

### Einverständnisdatenerfassung

Platform ermöglicht die Erfassung von Daten zur Einwilligung von Kunden mithilfe des folgenden Prozesses:

1. Ein Kunde gibt seine Zustimmungsvoreinstellungen für die Datenerfassung über ein Dialogfeld auf Ihrer Website an.
1. Ihr CMP erkennt die Änderung der Zustimmungsvoreinstellung und generiert dementsprechend TCF-Zustimmungsdaten.
1. Mithilfe des Platform Web SDK werden die (vom CMP zurückgegebenen) generierten Zustimmungsdaten an Adobe Experience Platform gesendet.
1. Die erfassten Zustimmungsdaten werden in einen [!DNL Profile]-aktivierten Datensatz aufgenommen, dessen Schema TCF-Zustimmungsfelder enthält.

Zusätzlich zu den SDK-Befehlen, die von CMP-Zustimmungs-Change-Hooks ausgelöst werden, können Zustimmungsdaten auch über alle kundengenerierten XDM-Daten in Experience Platform fließen, die direkt in einen [!DNL Profile]-aktivierten Datensatz hochgeladen werden.

Alle Segmente, die von Adobe Audience Manager (über den Quell-Connector [!DNL Audience Manager] oder anderweitig) für Platform freigegeben werden, können auch Einwilligungsdaten enthalten, sofern die entsprechenden Felder über [!DNL Experience Cloud Identity Service] auf diese Segmente angewendet wurden. Weitere Informationen zum Erfassen von Einwilligungsdaten in [!DNL Audience Manager] finden Sie im Dokument zum [Adobe Audience Manager-Plug-in für IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html).

### Durchsetzung der nachgelagerten Zustimmung

Sobald die TCF-Zustimmungsdaten erfolgreich erfasst wurden, finden die folgenden Prozesse in nachgelagerten Platform-Diensten statt:

1. [!DNL Real-time Customer Profile] aktualisiert die gespeicherten Zustimmungsdaten für das Profil dieses Kunden.
1. Platform verarbeitet Kunden-IDs nur, wenn die Anbieterberechtigung für Platform (565) für jede ID in einem Cluster bereitgestellt wird.
1. Beim Exportieren von Segmenten in Ziele, die zu Mitgliedern der TCF 2.0-Anbieterliste gehören, enthält Platform nur Profile, wenn die Anbieterberechtigungen für beide Platform (565) *und* für die einzelnen Ziele für jede ID in einem Cluster bereitgestellt werden.

Die übrigen Abschnitte in diesem Dokument enthalten Anleitungen dazu, wie Sie Platform und Ihre Datenvorgänge so konfigurieren, dass die oben beschriebenen Anforderungen an die Erfassung und Durchsetzung erfüllt werden.

## Ermitteln, wie Sie in Ihrem CMP Kundenzustimmungsdaten generieren {#consent-data}

Da jedes CMP-System einzigartig ist, müssen Sie festlegen, wie Ihre Kunden bei der Interaktion mit Ihrem Dienst am besten ihre Zustimmung erteilen können. Eine gängige Methode, dies zu erreichen, ist die Verwendung eines Cookie-Einverständnisdialogfelds, ähnlich dem folgenden Beispiel:

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Dieser Dialog muss es dem Kunden ermöglichen, sich an Folgendem zu beteiligen oder abzuwählen:

| Zustimmungsoption | Beschreibung |
| --- | --- |
| **Zweck** | Zweck definiert, für welche Werbetechnologiezwecke eine Marke die Daten eines Kunden verwenden kann. Damit Platform Kunden-IDs verarbeiten kann, müssen die folgenden Zwecke aktiviert werden: <ul><li>**Zweck 1**: Informationen auf einem Gerät speichern und/oder aufrufen</li><li>**Zweck 10**: Produkte entwickeln und verbessern</li></ul> |
| **Berechtigungen von Anbietern** | Zusätzlich zu den Werbetechnologiezwecken muss das Dialogfeld auch dem Kunden die Möglichkeit bieten, seine Daten von bestimmten Anbietern, einschließlich Adobe Experience Platform (565), zu verwenden oder abzulehnen. |

### Zustimmungszeichenfolgen {#consent-strings}

Unabhängig von der Methode, mit der Sie die Daten erfassen, besteht das Ziel darin, einen Zeichenfolgenwert zu generieren, der auf den vom Kunden gewählten Zustimmungsoptionen basiert, die Zustimmungszeichenfolge genannt.

In der TCF-Spezifikation werden Zustimmungszeichenfolgen verwendet, um relevante Details zu den Zustimmungseinstellungen eines Kunden im Hinblick auf spezifische Marketing-Zwecke zu kodieren, die von Richtlinien und Anbietern definiert werden. Platform nutzt diese Zeichenfolgen zum Speichern der Zustimmungseinstellungen für jeden Kunden. Daher muss bei jeder Änderung dieser Einstellungen eine neue Zustimmungszeichenfolge generiert werden.

Zustimmungszeichenfolgen dürfen nur von einer CMP erstellt werden, die beim IAB TCF registriert ist. Weitere Informationen zum Generieren von Zustimmungszeichenfolgen mit Ihrer jeweiligen CMP finden Sie im [Handbuch zur Formatierung von Zustimmungszeichenfolgen](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) im IAB TCF GitHub-Repository.

## Erstellen von Datensätzen mit TCF-Einwilligungsfeldern {#datasets}

Die Daten zur Kundenzustimmung müssen an Datensätze gesendet werden, deren Schemas TCF-Einwilligungsfelder enthalten. Informationen zum Erstellen des erforderlichen Profildatensatzes (und eines optionalen Experience Event-Datensatzes) finden Sie im Tutorial zu [Erstellen von Datensätzen zur Erfassung der TCF 2.0-Zustimmung](./dataset.md) , bevor Sie mit diesem Handbuch fortfahren.

## Aktualisieren Sie die [!DNL Profile]-Zusammenführungsrichtlinien, um Einwilligungsdaten einzuschließen. {#merge-policies}

Nachdem Sie einen [!DNL Profile]-aktivierten Datensatz für die Erfassung von Zustimmungsdaten erstellt haben, müssen Sie sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert wurden, dass immer TCF-Einwilligungsfelder in Ihre Kundenprofile aufgenommen werden. Dazu gehört das Festlegen der Datensatzpriorität, sodass Ihr Einwilligungsdatensatz Vorrang vor anderen möglicherweise in Konflikt stehenden Datensätzen erhält.

Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien finden Sie unter [Übersicht über Zusammenführungsrichtlinien](../../../../profile/merge-policies/overview.md). Beim Einrichten Ihrer Zusammenführungsrichtlinien müssen Sie sicherstellen, dass Ihre Segmente alle erforderlichen Zustimmungsattribute enthalten, die von der Feldergruppe [XDM-Datenschutzschema](./dataset.md#privacy-field-group) bereitgestellt werden, wie im Handbuch zur Vorbereitung von Datensätzen beschrieben.

## Integrieren des Experience Platform Web SDK zur Erfassung von Daten zur Kundenzustimmung {#sdk}

>[!NOTE]
>
>Die Verwendung des Experience Platform Web SDK ist erforderlich, um Einwilligungsdaten direkt in Adobe Experience Platform zu verarbeiten. [!DNL Experience Cloud Identity Service] wird derzeit nicht unterstützt.
>
>[!DNL Experience Cloud Identity Service] wird weiterhin für die Zustimmungsverarbeitung in Adobe Audience Manager unterstützt. Für die Einhaltung von TCF 2.0 ist jedoch nur eine Aktualisierung der Bibliothek auf  [Version 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases) erforderlich.

Nachdem Sie Ihre CMP zur Generierung von Zustimmungszeichenfolgen konfiguriert haben, müssen Sie das Experience Platform Web SDK integrieren, um diese Zeichenfolgen zu erfassen und an Platform zu senden. Das Platform SDK stellt zwei Befehle bereit, mit denen TCF-Zustimmungsdaten an Platform gesendet werden können (wie in den folgenden Unterabschnitten erläutert). Diese Befehle sollten verwendet werden, wenn ein Kunde zum ersten Mal Einwilligungsinformationen bereitstellt, und sobald sich die Einwilligung anschließend ändert.

**Das SDK verfügt nicht standardmäßig** über eine Schnittstelle mit CMPs. Sie müssen bestimmen, wie das SDK in Ihre Website integriert werden kann, auf Zustimmungsänderungen in der CMP warten und den entsprechenden Befehl aufrufen.

### Neuen Datastream erstellen

Damit das SDK Daten an Experience Platform senden kann, müssen Sie zunächst einen neuen Datastream für Platform in [!DNL Adobe Experience Platform Launch] erstellen. Spezifische Schritte zum Erstellen einer neuen Konfiguration finden Sie in der [SDK-Dokumentation](../../../../edge/fundamentals/datastreams.md).

Nachdem Sie einen eindeutigen Namen für die Konfiguration angegeben haben, wählen Sie die Umschalter-Schaltfläche neben **[!UICONTROL Adobe Experience Platform]** aus. Verwenden Sie als Nächstes die folgenden Werte, um den Rest des Formulars auszufüllen:

| Datenspeicherfeld | Wert |
| --- | --- |
| [!UICONTROL Sandbox] | Der Name der Plattform [Sandbox](../../../../sandboxes/home.md), die die erforderliche Streaming-Verbindung und Datensätze zum Einrichten des Datastreams enthält. |
| [!UICONTROL Streaming-Inlet] | Eine gültige Streaming-Verbindung für die Experience Platform. Lesen Sie das Tutorial zu [Erstellen einer Streaming-Verbindung](../../../../ingestion/tutorials/create-streaming-connection-ui.md) , wenn Sie keinen vorhandenen Streaming-Inlet haben. |
| [!UICONTROL Ereignis-Datensatz] | Wählen Sie den Datensatz [!DNL XDM ExperienceEvent] aus, der im [vorherigen Schritt](#datasets) erstellt wurde. Wenn Sie die Feldergruppe [[!UICONTROL IAB TCF 2.0 Consent] ](../../../../xdm/field-groups/event/iab.md) im Schema dieses Datensatzes eingeschlossen haben, können Sie Einwilligungsänderungsereignisse im Laufe der Zeit mithilfe des Befehls [`sendEvent`](#sendEvent) verfolgen und diese Daten in diesem Datensatz speichern. Beachten Sie, dass die in diesem Datensatz gespeicherten Zustimmungswerte **nicht** in automatischen Durchsetzungs-Workflows verwendet werden. |
| [!UICONTROL Profildatensatz] | Wählen Sie den Datensatz [!DNL XDM Individual Profile] aus, der im [vorherigen Schritt](#datasets) erstellt wurde. Wenn Sie mit dem Befehl [`setConsent`](#setConsent) auf CMP-Zustimmungs-Change-Hooks reagieren, werden die erfassten Daten in diesem Datensatz gespeichert. Da dieser Datensatz profilaktiviert ist, werden die in diesem Datensatz gespeicherten Zustimmungswerte bei automatischen Durchsetzungs-Workflows berücksichtigt. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Wählen Sie nach Abschluss des Vorgangs **[!UICONTROL Speichern]** am unteren Bildschirmrand aus und folgen Sie den weiteren Anweisungen, um die Konfiguration abzuschließen.

### Festlegen von Befehlen zur Änderung der Zustimmung

Nachdem Sie den im vorherigen Abschnitt beschriebenen Datastream erstellt haben, können Sie mit der Verwendung von SDK-Befehlen beginnen, um Zustimmungsdaten an Platform zu senden. Die folgenden Abschnitte enthalten Beispiele dafür, wie die einzelnen SDK-Befehle in verschiedenen Szenarien verwendet werden können.

>[!NOTE]
>
>Eine Einführung in die allgemeine Syntax für alle Platform SDK-Befehle finden Sie im Dokument zu [Ausführen von Befehlen](../../../../edge/fundamentals/executing-commands.md).

#### Verwenden von CMP-Zustimmungs-Change-Hooks {#setConsent}

Viele CMPs bieten vordefinierte Hooks, die Zustimmungsänderungs-Ereignisse überwachen. Wenn diese Ereignisse eintreten, können Sie den Befehl `setConsent` verwenden, um die Einwilligungsdaten dieses Kunden zu aktualisieren.

Der Befehl `setConsent` erwartet zwei Argumente: (1) eine Zeichenfolge, die den Befehlstyp angibt (in diesem Fall &quot;setConsent&quot;), und (2) eine Payload, die ein `consent` -Array enthält, das mindestens ein Objekt enthalten muss, das die erforderlichen Zustimmungsfelder bereitstellt, wie unten dargestellt:

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
| `gdprApplies` | Ein boolescher Wert, der anzeigt, ob die DSGVO für den aktuell angemeldeten Kunden gilt. Damit TCF 2.0 für diesen Kunden erzwungen werden kann, muss der Wert auf `true` gesetzt werden. Die Standardeinstellung ist `true`, falls nicht definiert. |

Der Befehl `setConsent` sollte als Teil eines CMP-Hooks verwendet werden, der Änderungen in den Zustimmungseinstellungen erkennt. Das folgende JavaScript zeigt ein Beispiel dafür, wie der Befehl `setConsent` für den `OnConsentChanged`-Hook von OneTrust verwendet werden kann:

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

Sie können auch mithilfe des Befehls `sendEvent` TCF 2.0-Zustimmungsdaten für jedes in Platform ausgelöste Ereignis erfassen.

>[!NOTE]
>
>Um diese Methode verwenden zu können, müssen Sie die Feldergruppe Erlebnisereignis-Datenschutz zu Ihrem [!DNL Profile]-aktivierten [!DNL XDM ExperienceEvent]-Schema hinzugefügt haben. Anweisungen zur Konfiguration finden Sie im Abschnitt zum Aktualisieren des ExperienceEvent-Schemas](./dataset.md#event-schema) im Handbuch zur Datensatzvorbereitung .[

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
| `gdprApplies` | Ein boolescher Wert, der anzeigt, ob die DSGVO für den aktuell angemeldeten Kunden gilt. Damit TCF 2.0 für diesen Kunden erzwungen werden kann, muss der Wert auf `true` gesetzt werden. Die Standardeinstellung ist `true`, falls nicht definiert. |

### Umgang mit SDK-Antworten

Alle [!DNL Platform SDK]-Befehle geben Zusagen zurück, die angeben, ob der Aufruf erfolgreich war oder fehlgeschlagen ist. Sie können diese Antworten dann für zusätzliche Logik verwenden, z. B. für die Anzeige von Bestätigungsnachrichten an den Kunden. Spezifische Beispiele finden Sie im Abschnitt [Umgang mit Erfolg oder Fehler](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) im Handbuch zum Ausführen von SDK-Befehlen .

## Segmente exportieren {#export}

>[!NOTE]
>
>Bevor Sie mit dem Exportieren von Segmenten beginnen, müssen Sie sicherstellen, dass Ihre Segmente alle erforderlichen Einwilligungsfelder enthalten. Weitere Informationen finden Sie im Abschnitt [Konfigurieren von Zusammenführungsrichtlinien](#merge-policies) .

Nachdem Sie Daten zur Kundenzustimmung erfasst und Zielgruppensegmente erstellt haben, die die erforderlichen Zustimmungsattribute enthalten, können Sie die TCF 2.0-Compliance erzwingen, wenn Sie diese Segmente an nachgelagerte Ziele exportieren.

Sofern die Zustimmungseinstellung `gdprApplies` für eine Reihe von Kundenprofilen auf `true` gesetzt ist, werden alle Daten aus diesen Profilen, die an nachgelagerte Ziele exportiert werden, anhand der TCF-Zustimmungsvoreinstellungen für jedes Profil gefiltert. Jedes Profil, das nicht die erforderlichen Zustimmungseinstellungen erfüllt, wird während des Exportvorgangs übersprungen.

Kunden müssen den folgenden Zwecken zustimmen (wie in [TCF 2.0-Richtlinien](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions) beschrieben), damit ihre Profile in Segmente aufgenommen werden, die nach Zielen exportiert werden:

* **Zweck 1**: Informationen auf einem Gerät speichern und/oder aufrufen
* **Zweck 10**: Produkte entwickeln und verbessern

Für TCF 2.0 muss außerdem die Datenquelle die Berechtigung des Zielanbieters überprüfen, bevor Daten an dieses Ziel gesendet werden. Daher prüft Platform, ob die Berechtigung des Anbieters des Ziels für alle IDs im Cluster angemeldet ist, bevor Daten an dieses Ziel gebunden werden.

>[!NOTE]
>
>Alle Segmente, die für Adobe Audience Manager freigegeben werden, enthalten dieselben TCF 2.0-Zustimmungswerte wie ihre Platform-Gegenstücke. Da [!DNL Audience Manager] dieselbe Anbieter-ID wie Platform (565) verwendet, sind dieselben Zwecke und die Berechtigung des Anbieters erforderlich. Weitere Informationen finden Sie im Dokument zum [Adobe Audience Manager-Plug-in für IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) .

## Implementierung testen {#test-implementation}

Nachdem Sie Ihre TCF 2.0-Implementierung konfiguriert und Segmente an Ziele exportiert haben, werden keine Daten exportiert, die nicht den Zustimmungsanforderungen entsprechen. Um jedoch zu sehen, ob die richtigen Kundenprofile während des Exports gefiltert wurden, müssen Sie die Datenspeicher Ihrer Ziele manuell überprüfen, um festzustellen, ob die Zustimmung ordnungsgemäß durchgesetzt wurde.

Beachten Sie, dass bei mehreren IDs, aus denen ein Cluster besteht und TCF 2.0 angewendet wird, der gesamte Cluster ausgeschlossen wird, wenn selbst eine einzelne ID nicht die richtigen Zwecke und Berechtigungen des Anbieters enthält.

## Nächste Schritte

In diesem Dokument wurde der Prozess der Konfiguration Ihrer Platform-Datenvorgänge zur Erfüllung Ihrer geschäftlichen Verpflichtungen gemäß TCF 2.0 beschrieben. Weiterführende Informationen zu den datenschutzbezogenen Funktionen der Plattform finden Sie in der Übersicht zu [Governance, Datenschutz und Sicherheit](../../overview.md).
