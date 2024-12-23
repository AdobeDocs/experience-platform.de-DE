---
title: Benutzeragenten-Clienthinweise
description: Erfahren Sie, wie Benutzeragenten-Clienthinweise im Web SDK funktionieren. Clienthinweise ermöglichen es Website-Inhabern, auf einen Großteil der Informationen zuzugreifen, die in der Benutzeragenten-Zeichenfolge verfügbar sind, wobei die Privatsphäre jedoch gewahrt bleibt.
keywords: Benutzeragent; Clienthinweise; Zeichenfolge; user-agent-Zeichenfolge; niedrige Entropie; hohe Entropie
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: 89dfe037e28bae51e335dc67185afa42b2c418e3
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 4%

---

# Benutzeragenten-Clienthinweise

## Übersicht {#overview}

Jedes Mal, wenn ein Webbrowser eine Anforderung an einen Webserver sendet, enthält der Header der Anfrage Informationen über den Browser und die Umgebung, in der der Browser ausgeführt wird. Alle diese Daten werden in einer Zeichenfolge zusammengefasst, die als Benutzeragenten-Zeichenfolge bezeichnet wird.

Im Folgenden finden Sie ein Beispiel dafür, wie eine Benutzeragenten-Zeichenfolge bei einer Anfrage aussieht, die von einem Chrome-Browser stammt, der auf einem [!DNL Mac OS] -Gerät ausgeführt wird.

>[!NOTE]
>
>Im Laufe der Jahre ist die Menge der Browser- und Geräteinformationen, die in der Benutzeragenten-Zeichenfolge enthalten sind, mehrmals gestiegen und geändert worden. Das folgende Beispiel zeigt eine Auswahl der häufigsten Benutzeragenten-Informationen.

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| Feld | Wert |
|---|---|
| Softwarename | Chrome |
| Softwareversion | 105 |
| Vollversion der Software | 105.0.0.0 |
| Name der Layout-Engine | AppleWebKit |
| Layout-Engine-Version | 537,36 |
| Betriebssystem | MAC OS X |
| Betriebssystemversion | 10,15,7 |
| Gerät | Intel Mac OS X 10_15_7 |

## Anwendungsfälle {#use-cases}

Benutzeragenten-Zeichenfolgen werden seit langem verwendet, um Marketing- und Entwicklungsteams wichtige Einblicke in die Anzeige von Site-Inhalten in Browsern, Betriebssystemen und Geräten sowie in die Interaktion der Benutzer mit Websites zu bieten.

Benutzeragenten-Zeichenfolgen werden auch verwendet, um Spam zu blockieren und Bots zu filtern, die Sites für verschiedene zusätzliche Zwecke durchsuchen.

## Benutzeragenten-Zeichenfolgen in Adobe Experience Cloud {#user-agent-in-adobe}

Adobe Experience Cloud-Lösungen nutzen die Benutzeragenten-Zeichenfolgen auf verschiedene Weise.

* Adobe Analytics verwendet die Benutzeragenten-Zeichenfolge, um zusätzliche Informationen zu Betriebssystemen, Browsern und Geräten, die zum Besuch einer Website verwendet werden, zu erweitern und abzuleiten.
* Adobe Audience Manager und Adobe Target qualifizieren Endbenutzer für Segmentierungs- und Personalisierungskampagnen, basierend auf den Informationen, die von der Benutzeragenten-Zeichenfolge bereitgestellt werden.

## Einführung in Benutzeragenten-Clienthinweise {#ua-ch}

In den letzten Jahren haben Site-Eigentümer und Marketing-Anbieter Benutzeragenten-Zeichenfolgen zusammen mit anderen in Anfragekopfzeilen enthaltenen Informationen verwendet, um digitale Fingerabdrücke zu erstellen. Diese Fingerabdrücke können zur Identifizierung von Benutzern ohne deren Wissen verwendet werden.

Trotz des wichtigen Zwecks, den Benutzeragenten-Zeichenfolgen für Site-Eigentümer bereitstellen, haben Browser-Entwickler beschlossen, die Funktionsweise von Benutzeragenten-Zeichenfolgen zu ändern, um potenzielle Datenschutzprobleme für Endbenutzer zu begrenzen.

Die von ihnen entwickelte Lösung heißt [Benutzeragenten-Clienthinweise](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Client-Hinweise ermöglichen es Websites weiterhin, die erforderlichen Browser-, Betriebssystem- und Geräteinformationen zu erfassen und bieten gleichzeitig einen besseren Schutz vor verdeckten Tracking-Methoden wie dem Fingerabdruck.

Clienthinweise ermöglichen es Website-Inhabern, auf einen Großteil der Informationen zuzugreifen, die in der Benutzeragenten-Zeichenfolge verfügbar sind, wobei die Privatsphäre jedoch gewahrt bleibt.

Wenn moderne Browser einen Benutzer an einen Webserver senden, wird die gesamte Benutzeragenten-Zeichenfolge bei jeder Anforderung gesendet, unabhängig davon, ob sie erforderlich ist. Client-Hinweise erzwingen dagegen ein Modell, bei dem der Server den Browser um die zusätzlichen Informationen bitten muss, die er über den Client wissen möchte. Nach Erhalt dieser Anfrage kann der Browser seine eigenen Richtlinien oder Benutzerkonfigurationen anwenden, um zu bestimmen, welche Daten zurückgegeben werden. Anstatt die gesamte Benutzeragenten-Zeichenfolge standardmäßig für alle Anforderungen anzuzeigen, wird der Zugriff jetzt explizit und überprüfbar verwaltet.

## Browserunterstützung {#browser-support}

[Clienthinweise für Benutzeragenten](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) wurden mit Version 89 von [!DNL Google Chrome]eingeführt.

Zusätzliche Chromium-basierte Browser unterstützen die Client Hints-API, z. B.:

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## Kategorien {#categories}

Es gibt zwei Kategorien von Benutzeragenten-Client-Hinweisen:

* [Clienthinweise mit geringer Entropie](#low-entropy)
* [Hohe Entropie-Client-Hinweise](#high-entropy)

### Clienthinweise mit geringer Entropie {#low-entropy}

Clienthinweise mit geringer Entropie enthalten grundlegende Informationen, die nicht zum Abnehmen von Fingerabdrücken von Benutzern verwendet werden können. Informationen wie Browsermarke, -plattform und ob die Anfrage von einem Mobilgerät stammt.

Clienthinweise mit geringer Entropie sind im Web SDK standardmäßig aktiviert und werden bei jeder Anfrage übergeben.

| HTTP-Header | JavaScript | Standardmäßig in User-Agent enthalten | Standardmäßig in Client-Hinweisen enthalten |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | Ja | Ja |
| `Sec-CH-UA-Platform` | `platform` | Ja | Ja |
| `Sec-CH-UA-Mobile` | `mobile` | Ja | Ja |

### Hohe Entropie-Client-Hinweise {#high-entropy}

Hohe Entropie-Client-Hinweise sind detailliertere Informationen über das Client-Gerät, wie Plattformversion, Architektur, Modell, Bitness (64-Bit- oder 32-Bit-Plattformen) oder vollständige Betriebssystemversion. Diese Informationen können potenziell beim Fingerabdruck verwendet werden.

| Eigenschaft | Beschreibung | HTTP-Header | XDM-Pfad | Beispiel | Standardmäßig im Benutzeragent enthalten | Standardmäßig in Client-Hinweisen enthalten |
| --- | --- | --- | --- | --- |---|---|
| Betriebssystemversion | Die Betriebssystemversion. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` | Ja | Nein |
| Architektur | Die zugrunde liegende CPU-Architektur. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` | Ja | Nein |
| Gerätemodell | Der Name des verwendeten Geräts. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` | Ja | Nein |
| Bitrate | Die Anzahl der Bit, die die zugrunde liegende CPU-Architektur unterstützt. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` | Ja | Nein |
| Browser-Anbieter | Das Unternehmen, das den Browser erstellt hat. Der Hinweis für die niedrige Entropie `Sec-CH-UA` erfasst auch dieses Element. | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` | Ja | Nein |
| Browsername | Der verwendete Browser. Der Hinweis für die niedrige Entropie `Sec-CH-UA` erfasst auch dieses Element. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` | Ja | Nein |
| Browserversion | Die signifikante Version des Browsers. Der Hinweis für die niedrige Entropie `Sec-CH-UA` erfasst auch dieses Element. Die genaue Browserversion wird nicht automatisch erfasst. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` | Ja | Nein |


Clienthinweise mit hoher Entropie sind im Web SDK standardmäßig deaktiviert. Um sie zu aktivieren, müssen Sie das Web SDK manuell so konfigurieren, dass Clienthinweise mit hoher Entropie angefordert werden.

## Hohe Entropie-Client-Hinweise wirken sich auf Experience Cloud-Lösungen aus {#impact-in-experience-cloud-solutions}

Einige Adobe Experience Cloud-Lösungen basieren beim Generieren von Berichten auf Informationen, die in Client-Hinweisen zur hohen Entropie enthalten sind.

Wenn Sie in Ihrer Umgebung keine Client-Hinweise mit hoher Entropie aktivieren, funktionieren die im Folgenden beschriebenen Adobe Analytics- und Audience Manager-Berichte und -Eigenschaften nicht.

### Adobe Analytics-Berichte, die auf Client-Hinweisen mit hoher Entropie basieren {#analytics}

Die Dimension [Betriebssystem](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html) enthält die Betriebssystemversion, die als Client-Hinweis mit hoher Entropie gespeichert wird. Wenn Client-Hinweise mit hoher Entropie nicht aktiviert sind, kann die Betriebssystemversion für Treffer, die von Chromium-Browsern erfasst werden, ungenau sein.

### Audience Manager-Eigenschaften, die auf Client-Hinweisen mit hoher Entropie basieren {#aam}

[!DNL Google] hat die Browserfunktion [!DNL Chrome] aktualisiert, um die über die Kopfzeile `User-Agent` erfassten Informationen zu minimieren. Daher erhalten Audience Manager, die [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=de) verwenden, keine zuverlässigen Informationen mehr für Eigenschaften, die auf [Schlüsseln auf Plattformebene](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html) basieren.

Audience Manager, die Schlüssel auf Plattformebene für das Targeting verwenden, müssen zu [Experience Platform Web SDK](/help/web-sdk/home.md) anstelle von [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=de) wechseln und [High Entropy Client Hints](#enabling-high-entropy-client-hints) aktivieren, um weiterhin zuverlässige Eigenschaftsdaten zu erhalten.

## Aktivieren von Client-Hinweisen mit hoher Entropie {#enabling-high-entropy-client-hints}

Um Client-Hinweise mit hoher Entropie in Ihrer Web SDK-Bereitstellung zu aktivieren, müssen Sie die zusätzliche Kontextoption `highEntropyUserAgentHints` in das Feld [`context`](/help/web-sdk/commands/configure/context.md) einschließen.

Um beispielsweise Hinweise zu hochgradigen Entropy-Clients aus Web-Eigenschaften abzurufen, würde Ihre Konfiguration wie folgt aussehen:

`context: ["highEntropyUserAgentHints", "web"]`

## Beispiel {#example}

Client-Hinweise, die in den Kopfzeilen der ersten vom Browser an einen Webserver gerichteten Anforderung enthalten sind, enthalten die Browsermarke, die Hauptversion des Browsers und einen Hinweis darauf, ob es sich bei dem Client um ein Mobilgerät handelt. Jedes Datenelement verfügt über einen eigenen Header-Wert, anstatt wie unten gezeigt in eine einzelne Benutzeragenten-Zeichenfolge gruppiert zu werden:

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

Die entsprechende [!DNL User-Agent] -Kopfzeile für denselben Browser würde wie folgt aussehen:

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Während die Informationen ähnlich sind, enthält die erste Anfrage an den Server Client-Hinweise. Diese enthalten nur eine Teilmenge der in der Benutzeragenten-Zeichenfolge verfügbaren Elemente. Fehlt in der Anfrage sind die Betriebssystemarchitektur, die vollständige Betriebssystemversion, der Name der Layout-Engine, die Version der Layout-Engine und die vollständige Browser-Version.

Bei nachfolgenden Anfragen erlaubt der [!DNL Client Hints API] Webservern jedoch, zusätzliche Details zum Gerät anzufordern. Wenn diese Werte angefordert werden, kann die Browserantwort abhängig von der Browserrichtlinie oder den Benutzereinstellungen diese Informationen enthalten.

Nachfolgend finden Sie ein Beispiel für das JSON-Objekt, das von [!DNL Client Hints API] zurückgegeben wird, wenn hohe Entropiewerte angefordert werden:


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
