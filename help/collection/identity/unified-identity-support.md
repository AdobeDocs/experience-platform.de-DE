---
title: Einheitliche Identitätsunterstützung in der Datenerfassung
description: Erfahren Sie, wie die Unterstützung einheitlicher Identitäten die Persistenz von Erstanbietern und die unterstützte Drittanbieteraktivierung in der Web-Datenerfassung zusammenführt.
hide: true
hidefromtoc: true
badge: Beta
source-git-commit: 32c2565d31eed4eda28195afaf82aac6f04a6f8a
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 3%

---

# Einheitliche Identitätsunterstützung in der Datenerfassung

>[!AVAILABILITY]
>
>Diese Funktion befindet sich derzeit in der Betaphase. Verfügbarkeit, Verhalten und Dokumentation können sich ändern.

Mit der Unterstützung einheitlicher Identitäten kann Edge Network sowohl für Erstanbieter- als auch für Drittanbieter-Identitätskontexte verwendet werden. Es führt eine dauerhafte First-Party-Identifizierung in Ihren eigenen Eigenschaften mit Aktivierungs-Workflows von Drittanbietern in Browsern zusammen, die Third-Party-Cookies unterstützen. Hintergrundinformationen dazu, wie Web SDK ECIDs, FPIDs und andere Identitätssignale verarbeitet, finden Sie unter [Identität in der Datenerfassung](./overview.md).

Mit der Unterstützung einheitlicher Identitäten können Sie:

* **Maximieren der Zielgruppenreichweite**: Aktivieren Sie Ihre Experience Platform-Zielgruppen für einen größeren Teil Ihres Traffics auf Zielen von Drittanbietern (DSPs, SSPs, Werbenetzwerke).
* **Messgenauigkeit beibehalten**: Halten Sie die Besucheridentifizierung über Ihre eigenen Eigenschaften und Werbeplattformen hinweg konsistent.
* **Zukunftssichere Implementierung**: Verwenden Sie Erstanbieter-Geräte-IDs als Grundlage, während die Kompatibilität mit Aktivierungs-Workflows von Drittanbietern gewahrt bleibt.

Wenn ein Besucher auf Ihre Site gelangt, wertet Edge Network verfügbare Identitätssignale aus und verknüpft Erstanbieter- und Drittanbieterkontexte automatisch, wenn die Bedingungen dies zulassen. Browser, die Drittanbieter-Cookies blockieren, funktionieren weiterhin im First-Party-Modus ohne Unterbrechung Ihrer Implementierung.

## Funktionsweise

Edge Network generiert ECIDs, indem es die verfügbaren Identitätssignale in der folgenden Prioritätsreihenfolge auswertet:

| Priorität | Quelle | Kontext | Verhalten |
| --- | --- | --- | --- |
| 1 | **demdex-ID** | Drittanbieter | Wenn eine Demdex-ID vorhanden ist, wird die ECID daraus ausgegeben. Dieser Seed erzeugt eine konsistente ECID über alle Domains hinweg, die denselben Drittanbieter-Cookie nutzen. |
| 2 | **FPID** | Erstanbieter | Wenn keine Demdex-ID vorhanden ist, aber eine FPID vorhanden ist, wird die ECID von der FPID vorgegeben und eine Demdex-ID wird davon abgeleitet. |
| 3 | **Random** | Erstanbieter | Wenn weder eine Demdex-ID noch eine FPID verfügbar ist, wird eine neue zufällige ECID generiert und eine Demdex-ID daraus abgeleitet. |

ECIDs und Demdex-IDs sind kryptografisch über einen deterministischen Algorithmus verknüpft, d. h. eine kann vom anderen abgeleitet werden. Diese Beziehung ermöglicht es der Edge Network, Identitätskontexte von Erstanbietern und Drittanbietern zu übersetzen, ohne dass eine separate Logik zur Besucherbehandlung in Ihrer Implementierung erforderlich ist.

Da die Beziehung deterministisch ist, können Zielgruppen, die auf Erstanbieter-ECIDs erstellt wurden, über die Drittanbieter-Infrastruktur aktiviert werden, wenn die entsprechende Demdex-ID verfügbar ist.

Für Besucherinnen und Besucher, die bereits über eine von FPID abgeleitete ECID verfügen, kann die Edge Network ihre Erstanbieteridentität automatisch mit dem Identitätskontext von Drittanbietern verknüpfen. Dies geschieht transparent, wenn der Browser Cookies von Drittanbietern unterstützt und keine Änderungen an Ihrer Implementierung erfordert. Wenn eine automatische Verknüpfung erfolgt:

1. Edge Network erkennt, dass die ECID des Besuchers nicht von einer Demdex-ID abgeleitet wurde.
1. Wenn der Browser des Besuchers Cookies von Drittanbietern unterstützt, wird eine schlanke Identitätssynchronisierung ausgelöst.
1. Das System erstellt eine Verknüpfung zwischen der Erstanbieter-ECID des Besuchers und seiner Drittanbieteridentität.
1. Der Link wird im Identitätsspeicher gespeichert, sodass die Zielgruppenaktivierung für Drittanbieterziele möglich ist.

Durch die automatische Verknüpfung werden vorhandene ECIDs beibehalten und Besucher-Cliffing verhindert. Im Laufe der Zeit wird ein größerer Teil Ihrer Audience nach und nach für die Aktivierung durch Drittanbieter infrage kommen, sobald Besucher zurückkehren und Verknüpfungen stattfinden.

Die Aktivierung von Drittanbieterzielgruppen beruht auf der ID-Synchronisierung (ID-Synchronisierung). Wenn Edge Network eine Drittanbieteridentität einrichtet oder aktualisiert, gibt es ID-Synchronisierungsanweisungen in der Antwort zurück. Diese Anweisungen weisen den Browser an, die Besucheridentität mit Partnerdomänen (DSPs, Werbenetzwerken und anderen Aktivierungsplattformen) zu synchronisieren, damit Ihre Experience Platform-Zielgruppen auf diesen Plattformen abgeglichen und bereitgestellt werden können.

## Voraussetzungen

Die Unterstützung einer einheitlichen Identität erfordert Folgendes:

* Ihre Site verwendet die Erstanbieter-Datenerfassung in einer Domain, die Sie kontrollieren.
* Ihre Implementierung verwendet FPIDs oder eine andere First-Party-Persistenzstrategie als Grundlage.
* In Ihrer Web-SDK-Konfiguration sind Drittanbieter-Cookies aktiviert.
* Die Synchronisierung von Drittanbieter-IDs ist für den Datenstrom aktiviert.
* Der Besucher verwendet einen Browser, der Cookies von Drittanbietern zulässt (siehe [Browserkompatibilität](#browser-compatibility) unten).

## Konfiguration

1. **Aktivieren von Drittanbieter-Cookies in Web SDK**: Aktivieren Sie die **Verwenden von Drittanbieter-**) in Ihrer Web SDK-Implementierung. Wenn Sie die Tag-Erweiterung verwenden, aktivieren Sie **[!UICONTROL Use third-party cookies]** in [Identitätskonfigurationseinstellungen](/help/tags/extensions/client/web-sdk/configure/identity.md#use-third-party-cookies). Wenn Sie die JavaScript-Bibliothek verwenden, setzen Sie [`thirdPartyCookiesEnabled`](/help/collection/js/commands/configure/thirdpartycookiesenabled.md) auf `true`.

1. **Synchronisierung der Drittanbieter-ID im Datenstrom aktivieren**: Aktivieren Sie die Option &quot;**[!UICONTROL Third-Party ID Sync]**&quot; in den erweiterten Einstellungen Ihres Datenstroms. Siehe [Erstellen und Konfigurieren von &#x200B;](/help/datastreams/configure.md#advanced-options)).

1. **Erstanbieter-Persistenz sicherstellen**: Vergewissern Sie sich, dass Ihre Erstanbieter-Persistenzstrategie (z. B. FPIDs) bereits in Ihrer eigenen Domain bereitgestellt ist. Siehe [Erstanbieter-Geräte-IDs in der Datenerfassung](fpid.md).

## Validierung

So überprüfen Sie, ob die Unterstützung der einheitlichen Identität funktioniert:

1. Öffnen Sie die Entwickler-Tools Ihres Browsers und navigieren Sie zur Registerkarte **Netzwerk** .
1. Löschen vorhandener Anfragen und Trigger eines Web SDK-Ereignisses (Seitenladevorgang oder benutzerspezifisches Ereignis) in einer neuen oder inkognito-Sitzung.
1. Suchen Sie die Edge Network-Antwort (suchen Sie nach Aufrufen an `adobedc.demdex.net` und Ihren Erstanbieter-Sammlungsendpunkt).
1. Überprüfen Sie die Antwort-Payload auf Anweisungen zur ID-Synchronisierung.

Wenn ID-Synchronisierungsanweisungen vorhanden sind, enthält die Antwort ein `identity:exchange`-Handle ähnlich dem folgenden:

```json
{
  "handle": [
    {
      "type": "identity:exchange",
      "payload": [
        {
          "type": "url",
          "id": 411,
          "spec": {
            "url": "https://example.com/...",
            "hideReferrer": false,
            "ttlMinutes": 10080
          }
        },
        {
          "type": "url",
          "id": 89,
          "spec": {
            "url": "https://example.org/...",
            "hideReferrer": true,
            "ttlMinutes": 10080
          }
        }
      ]
    }
  ]
}
```

| Element | Beschreibung |
| --- | --- |
| `type: "identity:exchange"` | Zeigt an, dass ID-Synchronisierungsanweisungen vorhanden sind. |
| `payload` | Liste der Synchronisierungs-URLs für Partner-IDs. |
| `url` Werte | URLs zur ID-Synchronisierung an Partner-Domains umleiten |
| `id` Werte | Partnerkennungen. |

>[!TIP]
>
>Wenn das `identity:exchange`-Handle in der Antwort nicht angezeigt wird:
>
>* Stellen Sie sicher, dass Sie mit einer neuen oder inkognito-Browser-Sitzung testen. Bei bestehenden Identitäten werden keine neuen Synchronisationen Trigger.
>* Stellen Sie sicher, dass sowohl der Datenstrom als auch die Web SDK-Einstellungen korrekt konfiguriert sind.
>* Vergewissern Sie sich, dass Sie einen Browser verwenden, der Cookies von Drittanbietern unterstützt (siehe Tabelle unten).

Überprüfen Sie nach Bestätigung der ID-Synchronisierungsaktivität, ob:

* Die Erstanbieter-Identität bleibt erwartungsgemäß über Seitenladevorgänge in Ihrer eigenen Domain hinweg erhalten.
* Aktivierungs- und Reporting-Flüsse verhalten sich in den von Ihnen unterstützten Umgebungen erwartungsgemäß.

## Browser-Kompatibilität {#browser-compatibility}

Die Identitätsfunktionen von Drittanbietern hängen von der Browser-Unterstützung für Drittanbieter-Cookies ab. Die folgende Tabelle fasst das erwartete Verhalten zusammen:

| Browser | Unterstützung von Drittanbieter-Cookies | Demdex verfügbar | Identitätsverhalten |
| --- | --- | --- | --- |
| Google Chrome | Unterstützt | Ja | Demdex → ECID (Domain-übergreifend konsistent) |
| Microsoft Edge | Standardmäßig unterstützt | Ja | Demdex → ECID (Domain-übergreifend konsistent) |
| Mozilla Firefox | Standardmäßig blockiert (ETP) | Nein (standardmäßig) | FPID → ECID (pro Domain) |
| Apple Safari | Blockiert (ITP) | Nein | FPID → ECID (pro Domain) |

Bei Browsern, die Drittanbieter-Cookies blockieren, funktioniert die Erstanbieter-Identifizierung weiterhin normal. Aktivierungsfunktionen von Drittanbietern sind nur verfügbar, wenn der Browser Cookies von Drittanbietern zulässt.

## Einschränkungen

* Das Identitätsverhalten von Drittanbietern hängt vollständig davon ab, ob der Browser des Besuchers Drittanbieter-Cookies zulässt. Es gibt kein Fallback für die Aktivierung durch Drittanbieter in Browsern, die diese blockieren.
* Für die automatische Verknüpfung muss der Besucher zur Website zurückkehren. Der Anteil Ihrer Zielgruppe, der für die Aktivierung durch Dritte in Frage kommt, nimmt im Laufe der Zeit allmählich zu.
