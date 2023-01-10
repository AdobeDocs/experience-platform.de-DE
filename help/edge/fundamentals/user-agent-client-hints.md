---
title: Benutzeragenten-Client-Hinweise
description: Erfahren Sie, wie Benutzeragenten-Client-Hinweise im Web SDK funktionieren.
keywords: user-agent;client hints; Zeichenfolge; user-agent string; niedrige Entropie; hohe Entropie
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: 4a2ae40fc64c4340ddb05db881c2176bb2aedc46
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 8%

---

# Benutzeragenten-Client-Hinweise

## Übersicht {#overview}

Jedes Mal, wenn ein Webbrowser eine Anforderung an einen Webserver sendet, enthält der Header der Anfrage Informationen über den Browser und die Umgebung, in der der Browser ausgeführt wird. Alle diese Daten werden in einer Zeichenfolge zusammengefasst, die als [!DNL User-Agent] Zeichenfolge.

Im Folgenden finden Sie ein Beispiel für eine [!DNL User-Agent] -Zeichenfolge ähnelt einer Anforderung, die von einem Chrome-Browser stammt, der auf einem [!DNL Mac OS] Gerät.

>[!NOTE]
>
>Im Laufe der Jahre die Menge der Browser- und Geräteinformationen, die in der [!DNL User-Agent] -Zeichenfolge wurde mehrmals erweitert und geändert. Das folgende Beispiel zeigt eine Auswahl der häufigsten [!DNL User-Agent] Informationen.

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| Feld | Wert |
|---|---|
| Software-Name | Chrome |
| Software-Version | 105 |
| Vollständige Software-Version | 105.0.0.0 |
| Name der Layout-Engine | AppleWebKit |
| Version der Layout-Engine | 537.36 |
| Betriebssystem | Mac OS X |
| Betriebssystemversion | 10.15.7 |
| Gerät | Intel Mac OS X 10_15_7 |

## Anwendungsbeispiele {#use-cases}

[!DNL User-Agent] -Zeichenfolgen werden seit langem verwendet, um Marketing- und Entwicklungsteams wichtige Einblicke in die Anzeige von Site-Inhalten in Browsern, Betriebssystemen und Geräten sowie in die Interaktion der Benutzer mit Websites zu bieten.

[!DNL User-Agent] -Zeichenfolgen werden auch verwendet, um Spam zu blockieren und Bots zu filtern, die Sites für eine Vielzahl zusätzlicher Zwecke durchsuchen.

## [!DNL User-Agent] Zeichenfolgen in Adobe Experience Cloud {#user-agent-in-adobe}

Adobe Experience Cloud-Lösungen verwenden die [!DNL User-Agent] Zeichenfolgen auf verschiedene Arten.

* Adobe Analytics verwendet die [!DNL User-Agent] -Zeichenfolge, um zusätzliche Informationen zu Betriebssystemen, Browsern und Geräten, die zum Besuch einer Website verwendet werden, zu ergänzen und abzuleiten.
* Adobe Audience Manager und Adobe Target qualifizieren Endbenutzer anhand der von der [!DNL User-Agent] Zeichenfolge.

## Einführung von Benutzeragenten-Client-Hinweisen {#ua-ch}

In den letzten Jahren haben Site-Eigentümer und Marketing-Anbieter [!DNL User-Agent] -Zeichenfolgen zusammen mit anderen Informationen, die in Anfragekopfzeilen enthalten sind, um digitale Fingerabdrücke zu erstellen. Diese Fingerabdrücke können als Mittel zur Identifizierung von Benutzern ohne deren Wissen verwendet werden.

Trotz des wichtigen Zwecks [!DNL User-Agent] Zeichenfolgen dienen Site-Eigentümern, Browser-Entwickler haben beschlossen, die Art und Weise zu ändern, in der [!DNL User-Agent] -Zeichenfolgen verwenden, um potenzielle Datenschutzprobleme für Endbenutzer zu begrenzen.

Die von ihnen entwickelte Lösung heißt [Benutzeragenten-Client-Hinweise](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). Client-Hinweise ermöglichen es Websites weiterhin, die erforderlichen Browser-, Betriebssystem- und Geräteinformationen zu erfassen und bieten gleichzeitig einen besseren Schutz vor verdeckten Tracking-Methoden wie dem Fingerabdruck.

Mit Client-Hinweisen können Website-Besitzer auf viele der Informationen zugreifen, die auch in der [!DNL User-Agent]-Zeichenfolge enthalten sind, allerdings auf eine Weise, die die Privatsphäre besser schützt.

Wenn moderne Browser einen Benutzer an einen Webserver senden, wird die gesamte [!DNL User-Agent] -Zeichenfolge wird bei jeder Anfrage gesendet, unabhängig davon, ob sie erforderlich ist. Client-Hinweise erzwingen dagegen ein Modell, bei dem der Server den Browser um die zusätzlichen Informationen bitten muss, die er über den Client wissen möchte. Nach Erhalt dieser Anfrage kann der Browser seine eigenen Richtlinien oder Benutzerkonfigurationen anwenden, um zu bestimmen, welche Daten zurückgegeben werden. Anstatt das gesamte [!DNL User-Agent] -Zeichenfolge standardmäßig bei allen Anforderungen, wird der Zugriff jetzt explizit und überprüfbar verwaltet.

## Browserunterstützung {#browser-support}

[Benutzeragenten-Client-Hinweise](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) wurden mit [!DNL Google Chrome ]Version 89.

Zusätzliche Chromium-basierte Browser unterstützen die Client Hints-API, z. B.:

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## Kategorien {#categories}

Es gibt zwei Kategorien von Benutzeragenten-Client-Hints:

* [Clienthinweise mit geringer Entropie](#low-entropy)
* [Hohe Entropie-Client-Hinweise](#high-entropy)

### Clienthinweise mit geringer Entropie {#low-entropy}

Clienthinweise mit geringer Entropie enthalten grundlegende Informationen, die nicht zum Abnehmen von Fingerabdrücken von Benutzern verwendet werden können. Informationen wie Browsermarke, -plattform und darüber, ob die Anfrage von einem Mobilgerät stammt.

Clienthinweise mit geringer Entropie sind im Web SDK standardmäßig aktiviert und werden bei jeder Anfrage übergeben.

| HTTP-Header | JavaScript | Standardmäßig in User-Agent enthalten | Standardmäßig in Client-Hinweisen enthalten |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | Ja | Ja |
| `Sec-CH-UA-Platform` | `platform` | Ja | Ja |
| `Sec-CH-UA-Mobile` | `mobile` | Ja | Ja |

### Hohe Entropie-Client-Hinweise {#high-entropy}

Hohe Entropie-Client-Hinweise sind detailliertere Informationen über das Client-Gerät, wie Plattformversion, Architektur, Modell, Bitness (64-Bit- oder 32-Bit-Plattformen) oder vollständige Betriebssystemversion. Diese Informationen können potenziell beim Fingerabdruck verwendet werden.

| HTTP-Header | JavaScript | Standardmäßig in User-Agent enthalten | Standardmäßig in Client Hints eingeschlossen |
|---|---|---|---|
| `Sec-CH-UA-Platform-Version` | `platformVersion` | Ja | Nein |
| `Sec-CH-UA-Arc` | `architecture` | Ja | Nein |
| `Sec-CH-UA-Model` | `model` | Ja | Nein |
| `Sec-CH-UA-Bitness` | `Bitness` | Ja | Nein |
| `Sec-CH-UA-Full-Version-List` | `fullVersionList` | Ja | Nein |

Clienthinweise mit hoher Entropie sind im Web SDK standardmäßig deaktiviert. Um sie zu aktivieren, müssen Sie das Web SDK manuell so konfigurieren, dass Clienthinweise mit hoher Entropie angefordert werden.

## Hohe Entropie-Client-Hinweise wirken sich auf Experience Cloud-Lösungen aus {#impact-in-experience-cloud-solutions}

Einige Adobe Experience Cloud-Lösungen basieren beim Generieren von Berichten auf Informationen, die in Client-Hinweisen zur hohen Entropie enthalten sind.

Wenn Sie in Ihrer Umgebung keine Client-Hinweise mit hoher Entropie aktivieren, funktionieren die im Folgenden beschriebenen Adobe Analytics- und Audience Manager-Berichte und -Eigenschaften nicht.

### Adobe Analytics-Berichte, die auf Client-Hinweisen mit hoher Entropie basieren {#analytics}

Die [Betriebssystem](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html) -Dimension umfasst die Betriebssystemversion, die als Client-Hinweis mit hoher Entropie gespeichert wird. Wenn Client-Hinweise mit hoher Entropie nicht aktiviert sind, kann die Betriebssystemversion für Treffer, die von Chromium-Browsern erfasst werden, ungenau sein.

### Audience Manager-Eigenschaften, die auf Client-Hinweisen mit hoher Entropie basieren {#aam}

Wenn Ihre Audience Manager-Eigenschaften eine der folgenden Eigenschaften verwenden, müssen Sie Clienthinweise mit hoher Entropie aktivieren. Andernfalls funktionieren die Eigenschaften nicht mehr.

* Betriebssystemversion
* Gerätemodell
* Gerätehersteller
* Geräteanbieter

## Aktivieren von Client-Hinweisen mit hoher Entropie {#enabling-high-entropy-client-hints}

Um Client-Hinweise mit hoher Entropie in Ihrer Web SDK-Bereitstellung zu aktivieren, müssen Sie die zusätzlichen `highEntropyUserAgentHints` -Kontextoption, wie im Abschnitt [Konfigurationsdokumentation](configuring-the-sdk.md#context), neben Ihrer vorhandenen Konfiguration.

Um beispielsweise Hinweise zu hochentropy-Clients aus Web-Eigenschaften abzurufen, würde Ihre Konfiguration wie folgt aussehen:

`context: ["highEntropyUserAgentHints", "web"]`

## Beispiel {#example}

Client-Hinweise, die in den Kopfzeilen der ersten vom Browser an einen Webserver gerichteten Anforderung enthalten sind, enthalten die Browsermarke, die Hauptversion des Browsers und einen Hinweis darauf, ob es sich bei dem Client um ein Mobilgerät handelt. Jedes Datenelement hat einen eigenen Header-Wert, anstatt in ein einzelnes [!DNL User-Agent] Zeichenfolge, wie unten dargestellt:

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

Die Entsprechung [!DNL User-Agent] -Kopfzeile für denselben Browser würde wie folgt aussehen:

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Während die Informationen ähnlich sind, enthält die erste Anfrage an den Server Client-Hinweise. Diese enthalten nur eine Untergruppe der verfügbaren Elemente im [!DNL User-Agent] Zeichenfolge. Fehlt in der Anfrage sind die Betriebssystemarchitektur, die vollständige Betriebssystemversion, der Name der Layout-Engine, die Version der Layout-Engine und die vollständige Browser-Version.

Bei nachfolgenden Anfragen muss die Variable [!DNL Client Hints API] ermöglicht es Webservern, zusätzliche Details zum Gerät anzufordern. Wenn diese Werte angefordert werden, kann die Browserantwort abhängig von der Browserrichtlinie oder den Benutzereinstellungen diese Informationen enthalten.

Nachfolgend finden Sie ein Beispiel für das JSON-Objekt, das vom [!DNL Client Hints API] wenn hohe Entropiewerte angefordert werden:


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
