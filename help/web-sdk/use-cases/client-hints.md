---
title: User Agent Client-Hinweise
description: Erfahren Sie, wie User Agent Client-Hinweise in Web SDK funktionieren. Mit Client-Hinweisen können Website-Besitzer auf viele der Informationen zugreifen, die auch in der Benutzeragenten-Zeichenfolge enthalten sind, allerdings auf eine Weise, die die Privatsphäre besser schützt.
keywords: user-agent;Client hints;String;user-agent string;niedrige Entropie;hohe Entropie
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: 89dfe037e28bae51e335dc67185afa42b2c418e3
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 4%

---

# User Agent Client-Hinweise

## Übersicht {#overview}

Jedes Mal, wenn ein Webbrowser eine Anfrage an einen Webserver sendet, enthält der Header der Anfrage Informationen über den Browser und die Umgebung, in der der Browser ausgeführt wird. Alle diese Daten werden in einer Zeichenfolge zusammengefasst, der so genannten Benutzeragenten-Zeichenfolge.

Im Folgenden finden Sie ein Beispiel dafür, wie eine Benutzeragenten-Zeichenfolge auf einer Anfrage aussieht, die von einem Chrome-Browser stammt, der auf einem [!DNL Mac OS] ausgeführt wird.

>[!NOTE]
>
>Im Laufe der Jahre ist die Menge der Browser- und Geräteinformationen, die in der Benutzeragenten-Zeichenfolge enthalten sind, mehrfach gestiegen und geändert worden. Das folgende Beispiel zeigt eine Auswahl der häufigsten Benutzeragenten-Informationen.

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| Feld | Wert |
|---|---|
| Software-Name | Chrome |
| Software-Version | 105 |
| Vollständige Software-Version | 105.0.0.0 |
| Name der Layout-Engine | AppleWebKit |
| Layout-Engine-Version | 537,36 |
| Betriebssystem | MAC OS X |
| Betriebssystemversion | 10,15,7 |
| Gerät | Intel Mac OS X 10_15_7 |

## Anwendungsfälle {#use-cases}

Benutzeragenten-Zeichenfolgen werden seit langem verwendet, um Marketing- und Entwicklungs-Teams wichtige Einblicke in die Anzeige von Website-Inhalten durch Browser, Betriebssysteme und Geräte sowie in die Interaktion zwischen Benutzern und Websites zu bieten.

Benutzeragenten-Zeichenfolgen werden auch verwendet, um Spam zu blockieren und Bots zu filtern, die Websites für eine Vielzahl von zusätzlichen Zwecken durchsuchen.

## Benutzeragenten-Zeichenfolgen in Adobe Experience Cloud {#user-agent-in-adobe}

Adobe Experience Cloud-Lösungen nutzen die Zeichenfolgen der Benutzeragenten auf verschiedene Weise.

* Adobe Analytics verwendet die Benutzeragenten-Zeichenfolge, um zusätzliche Informationen zu Betriebssystemen, Browsern und Geräten, die für den Besuch einer Website verwendet werden, zu ergänzen und abzuleiten.
* Adobe Audience Manager und Adobe Target qualifizieren Endbenutzende für Segmentierungs- und Personalisierungskampagnen, basierend auf den Informationen, die von der Benutzeragenten-Zeichenfolge bereitgestellt werden.

## Einführung in User Agent Client-Hinweise {#ua-ch}

In den letzten Jahren haben Site-Eigentümer und Marketing-Anbieter Benutzeragenten-Zeichenfolgen zusammen mit anderen in Anfrage-Headern enthaltenen Informationen verwendet, um digitale Fingerabdrücke zu erstellen. Diese Fingerabdrücke können zur Identifizierung von Benutzern ohne deren Wissen verwendet werden.

Trotz des wichtigen Zwecks, den Benutzeragenten-Zeichenfolgen für Site-Eigentümer erfüllen, haben Browser-Entwickler beschlossen, die Funktionsweise von Benutzeragenten-Zeichenfolgen zu ändern, um potenzielle Datenschutzprobleme für Endbenutzer zu vermeiden.

Die von ihnen entwickelte Lösung heißt [User Agent Client Hints](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Mit Client-Hinweisen können Websites weiterhin die erforderlichen Browser-, Betriebssystem- und Geräteinformationen erfassen und gleichzeitig einen besseren Schutz vor verdeckten Tracking-Methoden wie dem Fingerabdruck bieten.

Mit Client-Hinweisen können Website-Besitzer auf viele der Informationen zugreifen, die auch in der Benutzeragenten-Zeichenfolge enthalten sind, allerdings auf eine Weise, die die Privatsphäre besser schützt.

Wenn moderne Browser einen Benutzer an einen Webserver senden, wird bei jeder Anfrage die gesamte Benutzeragenten-Zeichenfolge gesendet, unabhängig davon, ob sie erforderlich ist. Client Hints hingegen erzwingen ein Modell, bei dem der Server den Browser nach den zusätzlichen Informationen über den Client fragen muss. Nach Erhalt dieser Anfrage kann der Browser seine eigenen Richtlinien oder Benutzerkonfigurationen anwenden, um zu bestimmen, welche Daten zurückgegeben werden. Anstatt die gesamte Benutzeragenten-Zeichenfolge standardmäßig für alle Anfragen verfügbar zu machen, wird der Zugriff jetzt explizit und überprüfbar verwaltet.

## Browser-Unterstützung {#browser-support}

[User Agent Client-Hinweise](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) wurden mit Version [!DNL Google Chrome] eingeführt.

Zusätzliche Chromium-basierte Browser unterstützen die Client Hints-API, z. B.:

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## Kategorien {#categories}

Es gibt zwei Kategorien von User Agent Client Hints:

* [Client-Hinweise mit niedriger Entropie](#low-entropy)
* [Client-Hinweise mit hoher Entropie](#high-entropy)

### Client-Hinweise mit niedriger Entropie {#low-entropy}

Client-Hinweise mit niedriger Entropie enthalten grundlegende Informationen, die nicht für Fingerabdruckbenutzer verwendet werden können. Informationen wie Browser-Marke, Plattform und ob die Anfrage von einem Mobilgerät kommt.

Client-Hinweise mit niedriger Entropie sind in Web SDK standardmäßig aktiviert und werden bei jeder Anfrage übergeben.

| HTTP-Kopfzeile | JavaScript | Standardmäßig im Benutzeragenten enthalten | Standardmäßig in Client-Hinweisen enthalten |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | Ja | Ja |
| `Sec-CH-UA-Platform` | `platform` | Ja | Ja |
| `Sec-CH-UA-Mobile` | `mobile` | Ja | Ja |

### Client-Hinweise mit hoher Entropie {#high-entropy}

Client-Hinweise mit hoher Entropie sind detailliertere Informationen über das Client-Gerät, z. B. Plattformversion, Architektur, Modell, Bit-Größe (64-Bit- oder 32-Bit-Plattformen) oder vollständige Betriebssystemversion. Diese Informationen könnten bei der Abnahme von Fingerabdrücken verwendet werden.

| Eigenschaft | Beschreibung | HTTP-Kopfzeile | XDM-Pfad | Beispiel | Standardmäßig im Benutzeragenten enthalten | Standardmäßig in Client-Hinweisen enthalten |
| --- | --- | --- | --- | --- |---|---|
| Betriebssystemversion | Die Version des Betriebssystems | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` | Ja | Nein |
| Architektur | Die zugrunde liegende CPU-Architektur. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` | Ja | Nein |
| Gerätemodell | Der Name des verwendeten Geräts. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` | Ja | Nein |
| Bitness | Die Anzahl der Bits, die von der zugrunde liegenden CPU-Architektur unterstützt werden. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` | Ja | Nein |
| Browser-Anbieter | Das Unternehmen, das den Browser erstellt hat. Der Hinweis `Sec-CH-UA` niedrige Entropie erfasst auch dieses Element. | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` | Ja | Nein |
| Browser-Name | Der verwendete Browser. Der Hinweis `Sec-CH-UA` niedrige Entropie erfasst auch dieses Element. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` | Ja | Nein |
| Browser-Version | Die Hauptversion des Browsers. Der Hinweis `Sec-CH-UA` niedrige Entropie erfasst auch dieses Element. Die genaue Browser-Version wird nicht automatisch erfasst. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` | Ja | Nein |


Client-Hinweise mit hoher Entropie sind in Web SDK standardmäßig deaktiviert. Um sie zu aktivieren, müssen Sie die Web-SDK manuell so konfigurieren, dass Client-Hinweise mit hoher Entropie angefordert werden.

## Auswirkungen von Client-Hinweisen mit hoher Entropie auf Experience Cloud-Lösungen {#impact-in-experience-cloud-solutions}

Einige Adobe Experience Cloud-Lösungen stützen sich bei der Berichterstellung auf Informationen in Client-Hinweisen mit hoher Entropie.

Wenn Sie in Ihrer Umgebung keine Client-Hinweise mit hoher Entropie aktivieren, funktionieren die unten beschriebenen Adobe Analytics- und Audience Manager-Berichte und -Eigenschaften nicht.

### Adobe Analytics-Berichte, die auf Client-Hinweisen mit hoher Entropie basieren {#analytics}

Die Dimension [Betriebssystem](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html) enthält die Betriebssystemversion, die als Client-Hinweis mit hoher Entropie gespeichert wird. Wenn Client-Hinweise mit hoher Entropie nicht aktiviert sind, kann die Betriebssystemversion für Treffer, die von Chromium-Browsern erfasst werden, ungenau sein.

### Audience Manager-Eigenschaften, die auf Client-Hinweisen mit hoher Entropie basieren {#aam}

[!DNL Google] hat die Funktion „Browser [!DNL Chrome]&quot; aktualisiert, um die über den `User-Agent`-Header erfassten Informationen zu minimieren. Daher erhalten Audience Manager-Kunden, die [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=de) verwenden, keine verlässlichen Informationen mehr über Eigenschaften, die auf [Plattformschlüsseln“ basieren](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html).

Audience Manager-Kunden, die Schlüssel auf Plattformebene für das Targeting verwenden, müssen zu [Experience Platform Web SDK](/help/web-sdk/home.md) anstelle von [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=de) wechseln und [Client Hints mit hoher Entropie](#enabling-high-entropy-client-hints) aktivieren, um weiterhin zuverlässige Eigenschaftsdaten zu erhalten.

## Aktivieren von Client-Hinweisen mit hoher Entropie {#enabling-high-entropy-client-hints}

Um Client-Hinweise mit hoher Entropie in Ihrer Web-SDK-Bereitstellung zu aktivieren, müssen Sie die zusätzliche Option `highEntropyUserAgentHints`-Kontext in das Feld [`context`](/help/web-sdk/commands/configure/context.md) einfügen.

Um beispielsweise Client-Hinweise mit hoher Entropie aus Web-Eigenschaften abzurufen, würde Ihre Konfiguration wie folgt aussehen:

`context: ["highEntropyUserAgentHints", "web"]`

## Beispiel {#example}

Client Hints in den Kopfzeilen der ersten vom Browser an einen Webserver gerichteten Anfrage enthalten die Browser-Marke, die Hauptversion des Browsers und einen Hinweis darauf, ob es sich bei dem Client um ein Mobilgerät handelt. Jedes Datenelement verfügt über einen eigenen Kopfzeilenwert, anstatt wie unten dargestellt in einer einzelnen Benutzeragenten-Zeichenfolge gruppiert zu werden:

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

Die entsprechende [!DNL User-Agent]-Kopfzeile für denselben Browser würde wie folgt aussehen:

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Obwohl die Informationen ähnlich sind, enthält die erste an den Server gerichtete Anfrage Client-Hinweise. Diese enthalten nur eine Teilmenge dessen, was in der Benutzeragenten-Zeichenfolge verfügbar ist. In der Anfrage fehlen die Betriebssystemarchitektur, die vollständige Betriebssystemversion, der Name der Layout-Engine, die Version der Layout-Engine und die vollständige Browser-Version.

Bei nachfolgenden Anfragen ermöglicht der [!DNL Client Hints API] Webservern jedoch, zusätzliche Details zum Gerät anzufordern. Wenn diese Werte angefordert werden, kann die Browser-Antwort je nach Browser-Richtlinie oder Benutzereinstellungen diese Informationen enthalten.

Nachfolgend finden Sie ein Beispiel für das JSON-Objekt, das von der [!DNL Client Hints API] zurückgegeben wird, wenn Werte mit hoher Entropie angefordert werden:


```json
{
   "architecture":"x86",
   "bitness":"64",
   "brands":[
      {
         "brand":" Not A;Brand",
         "version":"99"
      },
      {
         "brand":"Chromium",
         "version":"100"
      },
      {
         "brand":"Google Chrome",
         "version":"100"
      }
   ],
   "fullVersionList":[
      {
         "brand":" Not A;Brand",
         "version":"99.0.0.0"
      },
      {
         "brand":"Chromium",
         "version":"100.0.4896.127"
      },
      {
         "brand":"Google Chrome",
         "version":"100.0.4896.127"
      }
   ],
   "mobile":false,
   "model":"",
   "platformVersion":"12.2.1"
}
```
