---
keywords: Experience Platform;Startseite;IAB;IAB 2.0;Einverständnis;Einverständnis
solution: Experience Platform
title: IAB TCF 2.0-Unterstützung in Experience Platform
description: Erfahren Sie, wie Sie Ihre Datenvorgänge und Schemata konfigurieren, um beim Aktivieren von Segmenten für Ziele in Adobe Experience Platform die Einverständnisentscheidung der Kundinnen und Kunden zu vermitteln.
role: Developer
feature: Consent
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2524'
ht-degree: 1%

---

# IAB TCF 2.0-Unterstützung in Experience Platform

Der [!DNL Transparency & Consent Framework] (TCF) ist, wie vom [!DNL Interactive Advertising Bureau] (IAB) dargelegt, ein technischer Rahmen mit offenen Standards, der es Organisationen ermöglichen soll, die Zustimmung der Verbraucher zur Verarbeitung ihrer personenbezogenen Daten im Einklang mit der [!DNL General Data Protection Regulation] der Europäischen Union (DSGVO) zu erhalten, aufzuzeichnen und zu aktualisieren. Die zweite Iteration des Frameworks, TCF 2.0, bietet mehr Flexibilität bei der Frage, wie Verbraucher ihre Zustimmung erteilen oder verweigern können, einschließlich der Frage, ob und wie Anbieter bestimmte Funktionen der Datenverarbeitung nutzen können, wie z. B. die präzise Geolokalisierung.

>[!NOTE]
>
>Weitere Informationen zu TCF 2.0 finden Sie auf der [IAB Europe-Website](https://iabeurope.eu/) einschließlich Supportmaterialien und technischen Spezifikationen.

Adobe Experience Platform ist Teil der registrierten [IAB TCF 2.0-Anbieterliste](https://iabeurope.eu/vendor-list-tcf/) unter der ID **565**. In Übereinstimmung mit den TCF 2.0-Anforderungen können Sie mit Experience Platform Kundeneinverständnisdaten erfassen und in Ihre gespeicherten Kundenprofile integrieren. Diese Einverständnisdaten können dann je nach Anwendungsfall bei der Frage berücksichtigt werden, ob Profile in exportierte Zielgruppensegmente einbezogen werden.

>[!IMPORTANT]
>
>Experience Platform kann nur Version 2.0 des TCF (oder höher) einhalten. Frühere Versionen von TCF werden nicht unterstützt.

Dieses Dokument bietet einen Überblick darüber, wie Sie Ihre Datenvorgänge und Profilschemata so konfigurieren können, dass sie von Ihrer Einverständnisverwaltungsplattform (CMP) generierte Kundeneinverständnisdaten akzeptieren. Außerdem wird erläutert, wie Experience Platform beim Exportieren von Segmenten Einverständnisentscheidungen von Benutzenden vermittelt.

## Voraussetzungen

Um diesem Handbuch zu folgen, müssen Sie eine CMP verwenden, entweder kommerziell oder Ihre eigene, die integriert und mit dem IAB TCF konform ist. Weitere Informationen finden Sie [Liste der konformen ](https://iabeurope.eu/cmp-list/)).

>[!IMPORTANT]
>
>Wenn die ID Ihrer CMP ungültig ist, verarbeitet Experience Platform Ihre Daten unverändert. Um TCF 2.0 durchzusetzen, müssen Sie bestätigen, dass Ihre CMP über eine gültige ID verfügt, die bei IAB TCF 2.0 registriert wurde, bevor Sie Daten an Experience Platform senden.

Dieses Handbuch setzt außerdem Grundkenntnisse der folgenden Experience Platform-Services voraus:

* [Experience-Datenmodell (XDM)](/help/xdm/home.md): Das standardisierte Framework, mit dem Experience Platform Kundenerlebnisdaten organisiert.
* [Adobe Experience Platform Identity Service](/help/identity-service/home.md): Löst das grundlegende Problem der Fragmentierung von Kundenerlebnisdaten, indem Identitäten geräte- und systemübergreifend zusammengeführt werden.
* [Echtzeit-Kundenprofil](/help/profile/home.md): Verwendet [!DNL Identity Service], um aus Ihren Datensätzen in Echtzeit detaillierte Kundenprofile zu erstellen. [!DNL Real-Time Customer Profile] ruft Daten aus dem Data Lake ab und speichert Kundenprofile in einem eigenen separaten Datenspeicher.
* [Adobe Experience Platform Web SDK](/help/web-sdk/home.md): Eine Client-seitige JavaScript-Bibliothek, mit der Sie verschiedene Experience Platform-Services in Ihre kundenorientierte Website integrieren können.
   * [SDK-Einverständnisbefehle](../../../../web-sdk/commands/setconsent.md): Ein Überblick über den Anwendungsfall der einverständnisbezogenen SDK-Befehle, die in diesem Handbuch gezeigt werden.
* [Segmentierungs-Service von Adobe Experience Platform](/help/segmentation/home.md): Ermöglicht die Aufteilung [!DNL Real-Time Customer Profile] Daten in Personengruppen, die ähnliche Eigenschaften aufweisen und ähnlich auf Marketing-Strategien reagieren.

Zusätzlich zu den oben aufgeführten Experience Platform-Services sollten Sie auch mit [Zielen](/help/data-governance/home.md) und deren Rolle im Experience Platform-Ökosystem vertraut sein.

## Zusammenfassung des Kundeneinverständnisflusses {#summary}

In den folgenden Abschnitten wird beschrieben, wie Einverständnisdaten erfasst und durchgesetzt werden, nachdem das System ordnungsgemäß konfiguriert wurde.

### Einverständnisdatenerfassung

Mit Experience Platform können Sie Kundeneinverständnisdaten mithilfe des folgenden Prozesses erfassen:

1. Ein Kunde gibt seine Einverständnisvoreinstellungen für die Datenerfassung über ein Dialogfeld auf Ihrer Website an.
1. Ihre CMP erkennt die Änderung der Einverständnisvoreinstellung und generiert TCF-Einverständnisdaten entsprechend.
1. Mithilfe der Experience Platform Web SDK werden die generierten Einverständnisdaten (die von der CMP zurückgegeben werden) an Adobe Experience Platform gesendet.
1. Die erfassten Einverständnisdaten werden in einen [!DNL Profile] Datensatz aufgenommen, dessen Schema TCF-Einverständnisfelder enthält.

Zusätzlich zu den SDK-Befehlen, die durch CMP-Einverständnisänderungs-Hooks ausgelöst werden, können Einverständnisdaten auch über alle kundengenerierten XDM-Daten in Experience Platform fließen, die direkt in einen [!DNL Profile]-aktivierten Datensatz hochgeladen werden.

Alle Segmente, die von Adobe Audience Manager (über den [!DNL Audience Manager]-Quell-Connector oder anderweitig) für Experience Platform freigegeben werden, können auch Einverständnisdaten enthalten, wenn die entsprechenden Felder über [!DNL Experience Cloud Identity Service] auf diese Segmente angewendet wurden. Weitere Informationen zum Erfassen von Einverständnisdaten in [!DNL Audience Manager] finden Sie im Dokument zum [Adobe Audience Manager-Plug-in für IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=de).

### Nachgelagerte Durchsetzung von Einverständnissen

Sobald TCF-Einverständnisdaten erfolgreich aufgenommen wurden, finden die folgenden Prozesse in nachgelagerten Experience Platform-Services statt:

1. [!DNL Real-Time Customer Profile] aktualisiert die gespeicherten Einverständnisdaten für das Profil dieses Kunden.
1. Experience Platform verarbeitet Kunden-IDs nur, wenn für jede ID in einem Cluster die Anbieterberechtigung für Experience Platform (565) angegeben wird.
1. Beim Exportieren von Segmenten in Ziele, die zu Mitgliedern der TCF 2.0-Anbieterliste gehören, schließt Experience Platform nur Profile ein, wenn die Anbieterberechtigungen für Experience Platform (565) *und* das jeweilige Ziel für jede ID in einem Cluster bereitgestellt werden.

Die übrigen Abschnitte in diesem Dokument enthalten Anleitungen dazu, wie Sie Experience Platform und Ihre Datenvorgänge so konfigurieren, dass sie die oben beschriebenen Erfassungs- und Durchsetzungsanforderungen erfüllen.

## Bestimmen, wie Kundeneinverständnisdaten in Ihrem CMP generiert werden {#consent-data}

Da jedes CMP-System einzigartig ist, müssen Sie festlegen, wie Ihre Kunden bei der Interaktion mit Ihrem Service am besten ihr Einverständnis erteilen können. Ein Cookie-Einverständnisdialogfeld ist eine gängige Methode, um das Einverständnis des Kunden einzuholen. Nachfolgend finden Sie ein Beispiel für ein CMP-Dialogfeld.

![Ein Beispiel für ein Dialogfeld der Consent Management Platform.](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

In diesem Dialogfeld muss der Kunde Folgendes aktivieren oder deaktivieren können:

| Einverständnisoption | Beschreibung |
| --- | --- |
| **Zwecke** | Die Zwecke definieren, für welche Anzeigen-Tech-Zwecke eine Marke die Daten eines Kunden verwenden darf. Zur Verarbeitung von Kunden-IDs müssen für Experience Platform folgende Zwecke angemeldet werden: <ul><li>**Zweck 1**: Speichern und/oder Zugreifen auf Informationen auf einem Gerät</li><li>**Zweck 10**: Entwicklung und Verbesserung von Produkten</li></ul> |
| **Anbieterberechtigungen** | Zusätzlich zu Werbezwecken muss das Dialogfeld dem Kunden auch die Möglichkeit geben, sich für oder gegen die Verwendung seiner Daten durch bestimmte Anbieter, einschließlich Adobe Experience Platform (565), zu entscheiden. |

### Einverständnis-Zeichenfolgen {#consent-strings}

Unabhängig von der Methode, die Sie zum Erfassen der Daten verwenden, besteht das Ziel darin, einen Zeichenfolgenwert basierend auf den vom Kunden ausgewählten Einverständnisoptionen zu generieren, der als Einverständniszeichenfolge bezeichnet wird.

In der TCF-Spezifikation werden Einverständniszeichenfolgen verwendet, um relevante Details zu den Einverständniseinstellungen eines Kunden hinsichtlich spezifischer Marketing-Zwecke zu kodieren, wie sie von Richtlinien und Anbietern definiert werden. Experience Platform verwendet diese Zeichenfolgen, um die Einverständniseinstellungen für jeden Kunden zu speichern. Daher muss bei jeder Änderung dieser Einstellungen eine neue Einverständniszeichenfolge generiert werden.

Einverständniszeichenfolgen dürfen nur von einer CMP erstellt werden, die beim IAB TCF registriert ist. Weitere Informationen zum Generieren von Einverständniszeichenfolgen mit Ihrer bestimmten CMP finden Sie im [Handbuch zur Formatierung von Einverständniszeichenfolgen](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) im IAB TCF GitHub-Repository.

## Erstellen von Datensätzen mit TCF-Einverständnisfeldern {#datasets}

Kundeneinverständnisdaten müssen an Datensätze gesendet werden, deren Schemata TCF-Einverständnisfelder enthalten. Lesen Sie das Tutorial [Erstellen von Datensätzen zur Erfassung des TCF 2.0-Einverständnisses](./dataset.md) , um zu erfahren, wie Sie den erforderlichen Profildatensatz (und einen optionalen Erlebnisereignis-Datensatz) erstellen, bevor Sie mit diesem Handbuch fortfahren.

## Aktualisieren [!DNL Profile] Zusammenführungsrichtlinien zum Einschließen von Einverständnisdaten {#merge-policies}

Nachdem Sie einen [!DNL Profile]-aktivierten Datensatz zum Erfassen von Einverständnisdaten erstellt haben, müssen Sie sicherstellen, dass Ihre Zusammenführungsrichtlinien so konfiguriert wurden, dass sie immer TCF-Einverständnisfelder in Ihren Kundenprofilen enthalten. Dazu gehört die Festlegung der Datensatzpriorität, sodass Ihr Einverständnisdatensatz vor anderen potenziell kollidierenden Datensätzen priorisiert wird.

Weitere Informationen zum Arbeiten mit Zusammenführungsrichtlinien finden Sie unter [Zusammenführungsrichtlinien - Übersicht](/help/profile/merge-policies/overview.md). Beim Einrichten Ihrer Zusammenführungsrichtlinien müssen Sie sicherstellen, dass Ihre Segmente alle erforderlichen Einverständnisattribute enthalten, die von der [XDM-Datenschutzschemafeldgruppe](./dataset.md#privacy-field-group) bereitgestellt werden, wie im Handbuch zur Datensatzvorbereitung beschrieben.

## Integrieren von Experience Platform Web SDK zur Erfassung von Kundeneinverständnisdaten {#sdk}

>[!NOTE]
>
>Die Verwendung der Experience Platform Web SDK ist erforderlich, um Einverständnisdaten direkt in Adobe Experience Platform zu verarbeiten. [!DNL Experience Cloud Identity Service] wird nicht unterstützt.
>
>[!DNL Experience Cloud Identity Service] wird jedoch weiterhin für die Einverständnisverarbeitung in Adobe Audience Manager unterstützt, und die Einhaltung von TCF 2.0 erfordert nur, dass die Bibliothek auf Version 5[0 aktualisiert ](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Nachdem Sie Ihre CMP so konfiguriert haben, dass Einverständniszeichenfolgen generiert werden, müssen Sie die Experience Platform Web SDK integrieren, um diese Zeichenfolgen zu erfassen und an Experience Platform zu senden. Experience Platform SDK bietet zwei Befehle, mit denen TCF-Einverständnisdaten an Experience Platform gesendet werden können (siehe die folgenden Unterabschnitte). Diese Befehle sollten verwendet werden, wenn ein Kunde zum ersten Mal Einverständnisinformationen bereitstellt, und zwar immer dann, wenn sich das Einverständnis danach ändert.

**Der SDK stellt standardmäßig keine Schnittstelle zu CMPs bereit**. Es liegt an Ihnen zu bestimmen, wie Sie die SDK in Ihre Website integrieren, auf Einverständnisänderungen in der CMP zu warten und den entsprechenden Befehl aufzurufen.

### Erstellen eines Datenspeichers

Damit SDK Daten an Experience Platform senden kann, müssen Sie zunächst einen Datenstrom für Experience Platform erstellen. Spezifische Schritte zum Erstellen eines Datenstroms finden Sie in der [Dokumentation zu SDK](/help/datastreams/overview.md).

Nachdem Sie einen eindeutigen Namen für den Datenstrom angegeben haben, klicken Sie auf die Umschaltfläche neben **[!UICONTROL Adobe Experience Platform]**. Verwenden Sie als Nächstes die folgenden Werte, um den Rest des Formulars auszufüllen:

| Datenstromfeld | Wert |
| --- | --- |
| [!UICONTROL Sandbox] | Der Name der Experience Platform [Sandbox](/help/sandboxes/home.md) die die erforderliche Streaming-Verbindung und Datensätze zum Einrichten des Datenstroms enthält. |
| [!UICONTROL Streaming-Inlet] | Eine gültige Streaming-Verbindung für Experience Platform. Lesen Sie das Tutorial zum [Erstellen einer Streaming](/help/ingestion/tutorials/create-streaming-connection-ui.md)Verbindung, wenn noch kein Streaming-Inlet vorhanden ist. |
| [!UICONTROL Ereignis-Datensatz] | Wählen Sie den im [ Schritt erstellten [!DNL XDM ExperienceEvent] aus](#datasets). Wenn Sie die Feldergruppe [[!UICONTROL IAB TCF 2.0 ]Einverständnis](/help/xdm/field-groups/event/iab.md) in das Schema dieses Datensatzes aufgenommen haben, können Sie mit dem Befehl [`sendEvent`](#sendEvent) Einverständnisänderungsereignisse im Zeitverlauf verfolgen und diese Daten in diesem Datensatz speichern. Beachten Sie, dass die in diesem Datensatz gespeicherten Einverständniswerte in Workflows zur automatischen Durchsetzung **nicht** verwendet werden. |
| [!UICONTROL Profildatensatz] | Wählen Sie den im [ Schritt erstellten [!DNL XDM Individual Profile] aus](#datasets). Bei der Antwort auf CMP-Einverständnisänderungs-Hooks mit dem [`setConsent`](#setConsent)-Befehl werden erfasste Daten in diesem Datensatz gespeichert. Da dieser Datensatz profilaktiviert ist, werden die in diesem Datensatz gespeicherten Einverständniswerte bei automatischen Erzwingungs-Workflows berücksichtigt. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Wenn Sie fertig sind **[!UICONTROL wählen Sie unten]** Bildschirm „Speichern“ aus und folgen Sie weiteren Eingabeaufforderungen, um die Konfiguration abzuschließen.

### Erstellen von Befehlen zur Einverständnisänderung

Nachdem Sie den im vorherigen Abschnitt beschriebenen Datenstrom erstellt haben, können Sie mit der Verwendung von SDK-Befehlen beginnen, um Einverständnisdaten an Experience Platform zu senden. Die folgenden Abschnitte enthalten Beispiele dafür, wie die einzelnen SDK-Befehle in verschiedenen Szenarien verwendet werden können.

#### Verwenden der CMP-Erweiterungspunkte zur Einverständnisänderung {#setConsent}

Viele CMPs bieten vordefinierte Hooks, die auf Einverständnisänderungsereignisse warten. Wenn diese Ereignisse eintreten, können Sie den Befehl [`setConsent`](/help/web-sdk/commands/setconsent.md) verwenden, um die Einverständnisdaten dieses Kunden zu aktualisieren.

Der `setConsent`-Befehl erwartet zwei Argumente:

1. Eine Zeichenfolge, die den Befehlstyp angibt (in diesem Fall „setConsent„).
1. Eine Payload, die ein `consent` enthält. Das -Array muss mindestens ein Objekt enthalten, das die erforderlichen Einverständnisfelder bereitstellt.

Der `setConsent` Befehl wird unten angezeigt:

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
| `standard` | Der verwendete Einverständnisstandard. Dieser Wert muss für die Verarbeitung des Einverständnisses in TCF 2.0 auf `IAB` gesetzt werden. |
| `version` | Die Versionsnummer des Einverständnisstandards, die unter `standard` angegeben ist. Dieser Wert muss für die Verarbeitung des Einverständnisses in TCF 2.0 auf `2.0` gesetzt werden. |
| `value` | Die von der CMP generierte base-64-kodierte Einverständniszeichenfolge. |
| `gdprApplies` | Ein boolescher Wert, der angibt, ob die DSGVO für den aktuell angemeldeten Kunden gilt. Damit TCF 2.0 für diesen Kunden erzwungen werden kann, muss der Wert auf `true` gesetzt werden. Die Standardeinstellung ist `true`, wenn nicht definiert. |

Der `setConsent`-Befehl sollte als Teil eines CMP-Hooks verwendet werden, der Änderungen an den Einverständniseinstellungen erkennt. Der folgende JavaScript zeigt ein Beispiel dafür, wie der `setConsent`-Befehl für den `OnConsentChanged` Hook von OneTrust verwendet werden kann:

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

#### Verwenden von Ereignissen {#sendEvent}

Mit dem Befehl `sendEvent` können Sie auch TCF 2.0-Einverständnisdaten zu jedem in Experience Platform ausgelösten Ereignis erfassen.

>[!NOTE]
>
>Um diese Methode verwenden zu können, müssen Sie die Feldergruppe Datenschutz für Erlebnisereignisse zu Ihrem [!DNL Profile] aktivierten [!DNL XDM ExperienceEvent] hinzugefügt haben. Anweisungen zur Konfiguration finden [ im Abschnitt zum Aktualisieren ](./dataset.md#event-schema) ExperienceEvent-Schemas im Handbuch zur Datensatzvorbereitung.

Der `sendEvent`-Befehl sollte als Callback in entsprechenden Ereignis-Listenern auf Ihrer Website verwendet werden. Der Befehl erwartet zwei Argumente: (1) eine Zeichenfolge, die den Befehlstyp angibt (in diesem Fall `sendEvent`), und (2) eine Payload, die ein `xdm`-Objekt enthält, das die erforderlichen Einverständnisfelder als JSON bereitstellt:

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
| `xdm.consentStrings` | Ein Array, das mindestens ein Objekt enthalten muss, das die erforderlichen Einverständnisfelder bereitstellt. |
| `consentStandard` | Der verwendete Einverständnisstandard. Dieser Wert muss für die Verarbeitung des Einverständnisses in TCF 2.0 auf `IAB` gesetzt werden. |
| `consentStandardVersion` | Die Versionsnummer des Einverständnisstandards, die unter `standard` angegeben ist. Dieser Wert muss für die Verarbeitung des Einverständnisses in TCF 2.0 auf `2.0` gesetzt werden. |
| `consentStringValue` | Die von der CMP generierte base-64-kodierte Einverständniszeichenfolge. |
| `gdprApplies` | Ein boolescher Wert, der angibt, ob die DSGVO für den aktuell angemeldeten Kunden gilt. Damit TCF 2.0 für diesen Kunden erzwungen werden kann, muss der Wert auf `true` gesetzt werden. Die Standardeinstellung ist `true`, wenn nicht definiert. |

### Umgang mit SDK-Antworten

Viele Web-SDK-Befehle geben Zusagen zurück, die angeben, ob der Aufruf erfolgreich war oder fehlgeschlagen ist. Sie können diese Antworten dann für zusätzliche Logik verwenden, z. B. um Bestätigungsnachrichten an den Kunden anzuzeigen. Weitere Informationen finden [ unter ](/help/web-sdk/commands/command-responses.md).

## Segmente exportieren {#export}

>[!NOTE]
>
>Bevor Sie mit dem Export von Segmenten beginnen, müssen Sie sicherstellen, dass Ihre Segmente alle erforderlichen Einverständnisfelder enthalten. Weitere Informationen finden Sie [ Abschnitt „Konfigurieren von ](#merge-policies)&quot;.

Nachdem Sie Kundeneinverständnisdaten erfasst und Zielgruppensegmente erstellt haben, die die erforderlichen Einverständnisattribute enthalten, können Sie die TCF 2.0-Konformität durchsetzen, wenn Sie diese Segmente an nachgelagerte Ziele exportieren.

Wenn die Einverständniseinstellung `gdprApplies` für einen Satz von Kundenprofilen auf `true` festgelegt ist, werden alle Daten aus diesen Profilen, die an nachgelagerte Ziele exportiert werden, basierend auf den TCF-Einverständnisvoreinstellungen für jedes Profil gefiltert. Jedes Profil, das nicht den erforderlichen Einverständnisvoreinstellungen entspricht, wird während des Exportvorgangs übersprungen.

Kundinnen und Kunden müssen den folgenden Zwecken zustimmen (wie in [TCF 2.0-Richtlinien](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions) beschrieben), damit ihre Profile in Segmente aufgenommen werden, die an Ziele exportiert werden:

* **Zweck 1**: Speichern und/oder Zugreifen auf Informationen auf einem Gerät
* **Zweck 10**: Entwicklung und Verbesserung von Produkten

TCF 2.0 erfordert außerdem, dass die Datenquelle die Anbieterberechtigung des Ziels überprüft, bevor Daten an dieses Ziel gesendet werden. Daher prüft Experience Platform, ob die Anbieterberechtigung des Ziels für alle IDs im Cluster bei angemeldet ist, bevor Daten einbezogen werden, die an dieses Ziel gebunden sind.

>[!NOTE]
>
>Alle Segmente, die für Adobe Audience Manager freigegeben sind, enthalten dieselben TCF 2.0-Einverständniswerte wie ihre Experience Platform-Gegenstücke. Da [!DNL Audience Manager] dieselbe Anbieter-ID wie Experience Platform (565) verwendet, sind dieselben Zwecke und dieselben Anbieterberechtigungen erforderlich. Weitere Informationen finden Sie im Dokument zum [Adobe Audience Manager-Plug-in für IAB TCF](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=de) .

## Testen der Implementierung {#test-implementation}

Nachdem Sie Ihre TCF 2.0-Implementierung konfiguriert und Segmente an Ziele exportiert haben, werden alle Daten, die die Einverständnisanforderungen nicht erfüllen, nicht exportiert. Um festzustellen, ob die richtigen Kundenprofile beim Export gefiltert wurden, müssen Sie die Datenspeicher in Ihren Zielen manuell überprüfen, um festzustellen, ob das Einverständnis ordnungsgemäß durchgesetzt wurde.

>[!IMPORTANT]
>
>Wenn mehrere IDs einen Cluster bilden und TCF 2.0 gilt, wird der gesamte Cluster ausgeschlossen, wenn auch nur eine einzelne ID nicht die richtigen Zwecke und Anbieterberechtigungen enthält.

## Nächste Schritte

In diesem Dokument wurde der Prozess der Konfiguration Ihrer Experience Platform-Datenvorgänge beschrieben, um Ihre geschäftlichen Verpflichtungen gemäß TCF 2.0 zu erfüllen. Experience Platform Weitere Informationen zu den datenschutzbezogenen Funktionen von [ finden Sie in ](../../overview.md) Übersicht zu „Governance Datenschutz und Sicherheit“.
