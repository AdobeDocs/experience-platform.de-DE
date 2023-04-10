---
title: Häufig gestellte Fragen zum Adobe Experience Platform Web SDK
description: Erhalten Sie Antworten auf häufig gestellte Fragen zum Adobe Experience Platform Web SDK.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: a8f6bb8c3e35f4c17812ef944440210b7fe3f87b
workflow-type: tm+mt
source-wordcount: '2104'
ht-degree: 3%

---

# Häufig gestellte Fragen

Dieses Handbuch enthält Antworten auf häufig zum Adobe Experience Platform Web SDK gestellte Fragen.

## Was ist das Adobe Experience Platform Web SDK?

Das Adobe Experience Platform Web SDK ist eine Client-seitige JavaScript-Bibliothek, die es Kunden von Adobe Experience Cloud ermöglicht, mit den verschiedenen Diensten im Experience Cloud zu interagieren.

Es sendet Daten auf lösungsunabhängige Weise (XDM) an das Adobe Experience Platform Edge Network, das die Daten dann lösungsspezifischen Formaten und Zielen zuordnet und in Echtzeit sendet.

**Weitere Informationen**
[Präsentation der Adobe Summit](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Inwiefern unterscheidet sich das Adobe Experience Platform Web SDK von früheren Lösungen?

### Vor Adobe Experience Platform SDK

Derzeit müssen Sie je nach Lösung unterschiedliche JavaScript-Bibliotheken bereitstellen.

* Jede Lösung verfügt über eine eigene JavaScript-Bibliothek, ein eigenes Schema und eine eigene Domäne.
* Keine dieser Bibliotheken wurde für die Zusammenarbeit erstellt.
* Bei lösungsübergreifenden und Adobe Experience Platform-Anwendungsfällen müssen diese unterschiedlichen Bibliotheken voneinander abhängig sein, was zu Problemen bei der Implementierung führt.

Obwohl Tags in Platform die Bereitstellung und Verwaltung dieser Bibliotheken so einfach wie möglich machen, gibt es nach wie vor Probleme mit:

* Bibliotheksgröße (zu viel Adobe-Code auf einer Seite)
* Leistung (das Laden von Sites dauert zu lange.)
* Mehrere Aufrufe für einen einzelnen Anwendungsfall
* Warten auf ECID-Rückgabe vor Personalisierungsaufrufen (Gründe: Verzögerung)
* Fragmentierte Datenerfassung (was ist eine eVar?)
* Schema-Verwirrung zwischen Lösungen (A4T)
* Viele andere weniger optimale Dinge

Außerdem gibt es derzeit keine JavaScript-Bibliothek, die Daten direkt an Adobe Experience Platform sendet.

### Mit Adobe Experience Platform Web SDK

Das neue Web SDK sendet Daten für die folgenden Lösungen an ein einzelnes Ziel (Adobe Experience Platform Edge Network) und löst die häufigsten oben genannten Anwendungsfälle für Lösungen.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Besucher-ID
* Adobe Experience Platform

Weitere Lösungen werden im Laufe dieses Jahres folgen.

Adobe Experience Platform Web SDK kann auch Daten direkt an Adobe Experience Platform senden. Diese Daten befinden sich in XDM und werden dem serverseitigen Lösungsschema zugeordnet.

## Welchen Wert hat dieses neue Web SDK?

**Leistung:** Das Web-SDK ist kleiner als die Verwendung aller aktuellen Adobe-Bibliotheken und bietet deutlich schnellere Seitenladevorgänge.

**Einfachheit:** Die Kombination aus XDM, Web SDK, Tags, Experience Edge, Adobe Experience Cloud-Lösungen und Adobe Experience Platform bietet eine einfach zu verständliche und zu befolgende Datenerfassung.

* **XDM:** Das lösungsunabhängige Schema, mit dem Sie Daten an Adobe senden. Kein Tagging für eVars oder Mboxes mehr.
* **Adobe Experience Platform Web SDK:** Erleichtert das Senden und Empfangen von Daten an Adobe Experience Platform Edge Network.
* **Tags:** Vereinfacht die Bereitstellung und Konfiguration des Web SDK (und anderer JavaScript-Tags) auf einer Site.
* **Experience Edge:** Die Daten können einfach in dem gewünschten Format an Adobe Experience Platform und Lösungen weitergeleitet werden.
* **Adobe Experience Platform- und Adobe-Lösungen:** Aktivieren Sie deren Wertvorschlag.

**Kontrolle:** Da alle Daten einen einzigen und verbundenen Datenstrom verwenden, können Sie logisch verfolgen und steuern, wie die Daten bei jeder Millisekunde ihrer Journey aussehen, von und zu den Anwendungen.

**Modernste und zukunftsbereite Lösungen:** Das Web SDK und seine Verbindung zum Experience Edge Network haben es der Adobe ermöglicht, die Art und Weise, in der Adobe mit der Datenerfassung, Personalisierung, Zustimmung und Zukunft von Drittanbieter-Cookies umgeht, erheblich zu modernisieren. (Dadurch wird eine Erstanbieterdomäne aktiviert, die von Adobe verwaltet wird.)

**Time-to-Value:** Adobe hat hart gearbeitet (und wird dies auch weiterhin tun), um die Bereitstellung des Web SDK über Tags und die Zuordnung von clientseitigen Daten zu XDM so einfach wie möglich zu gestalten. Nach Abschluss dieser Arbeit können alle anderen Adobe-Lösungen und Adobe Experience Platform-Dienste serverseitig aktiviert oder deaktiviert werden. Wenn Sie dies beispielsweise für Adobe Analytics verwenden und Target oder Experience Platform aktivieren möchten, können Sie einfach einen Umschalter in der Datastream-Konfiguration aktivieren und diese Anwendungsfälle aufleuchten.

## Was ist Alloy?

Alloy ist der Codename für das Adobe Experience Platform Web SDK. Sie wird im Quellcode und Dateinamen des SDK verwendet, obwohl das Adobe Experience Platform Web SDK der offizielle Name ist.

## Müssen Kunden Adobe Experience Platform kaufen, um die [!DNL Web SDK]?

Nein. Jeder Adobe Digital Experience-Kunde kann das Adobe Experience Platform Web SDK kostenlos nutzen. Kunden, die die [!DNL Web SDK] müssen die richtigen Berechtigungen zum Erstellen von Schemas, Datensätzen, Identitäts-Namespaces und Datensätzen in der Datenerfassungs-Benutzeroberfläche oder der Benutzeroberfläche von Experience Platform konfigurieren.

Weitere Informationen zum Konfigurieren dieser Berechtigungen finden Sie in unserer Dokumentation unter [Verwaltung von Datenerfassungsberechtigungen](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).

## Wer sollte das Web SDK verwenden?

Das Adobe Experience Platform Web SDK wurde für folgende Personen entwickelt:

* Adobe Experience Platform-Benutzer
   * Wenn Sie Daten direkt von einem Gerät an Adobe Experience Platform senden müssen, wird dies offiziell empfohlen.
   * Adobe ist sich bewusst, dass die Verwendung des Adobe Analytics-Connectors schneller ist, wenn der Kunde bereits über Adobe Analytics verfügt. Dies ist jedoch nicht die langfristige Strategie für die Datenerfassung.

* Adobe Experience Cloud-Lösungskunden
   * Neue Kunden von Adobe Analytics, Adobe Audience Manager und Adobe Target sollten mit dem neuen Web SDK beginnen und keine älteren Bibliotheken verwenden.
   * Bestehende Kunden, die die bestmögliche Implementierung erhalten möchten, sollten das neue Web SDK verwenden.


## Wie erhalte ich Zugriff auf die Verwendung des Adobe Experience Platform Web SDK?

Das Web SDK ist derzeit für die allgemeine Öffentlichkeit verfügbar und kann zum Senden von Daten an Adobe Experience Cloud-Produkte verwendet werden. Die Möglichkeit, Daten an Drittanbieterlösungen zu senden, wird in naher Zukunft eingeführt. Das SDK ist gebührenfrei und wird von Adobe kostenlos gehostet. Bei Bedarf können Sie es herunterladen und kostenlos auf Ihren eigenen Servern hosten. Das Platform Web SDK benötigt Zugriff auf Datastream-Konfigurationen und den Adobe Experience Platform XDM-Schema-Builder, damit die Server der Adobe eingehende Daten aus dem SDK ordnungsgemäß verarbeiten können. Wenn Sie Zugriff erhalten möchten, wenden Sie sich an Ihr Adobe-Kundenbetreuungsteam, um den Anforderungsprozess zu starten.

## Welche Anwendungsfälle werden derzeit vom Web SDK unterstützt?

Das Web SDK entwickelt sich schnell. An weiteren Anwendungsfällen wird gearbeitet. Sie finden die [Liste der derzeit unterstützten Anwendungsfälle.](https://github.com/adobe/alloy/projects/5)

## Müssen aktuelle Kunden ihre Sites neu taggen?

Das hängt von Ihrer aktuellen Situation ab. Das Adobe Experience Platform Web SDK kann in zwei verschiedenen Stilen bereitgestellt werden. Ein zukünftiges Migrationsdokument enthält zusätzliche Details.

* **Nur ein weiteres Tag:** Wenn die Site bereits für Lösungen getaggt wurde und Sie keine neuen Tags erstellen können, Sie aber Daten für Anwendungsfälle der Experience Platform an Adobe Experience Platform Edge Network senden möchten oder die nächsten Funktionen für die Ereignisweiterleitung nutzen möchten (siehe unten), können Sie die `alloy.js` -Tag auf der Site, wo es als &quot;nur ein weiteres Tag&quot;funktioniert.

* **Das Tag &quot;Eins&quot;und &quot;Einziger&quot;:** Wenn Sie das Web SDK für eine Experience Cloud-Lösung verwenden möchten, müssen Sie es für _all_ der Lösungen auf dieser Seite. Wenn Ihre Site beispielsweise bereits für Adobe Analytics getaggt ist und Sie sie für Target verwenden möchten, müssen Sie sie sowohl für beide als auch für alle anderen künftig verwenden.

Wenn Sie sich also für die Verwendung des Adobe Experience Platform Web SDK für Anwendungsfälle ohne Lösung entscheiden, können Sie die Website mit `alloy.js` und gehen Sie weiter, als wäre es eine neue Lösung. Wenn Sie ihn für Adobe Analytics, Target, Audience Manager oder Anwendungsfälle verwenden möchten, müssen Sie möglicherweise den alten Code auf Ihrer Seite entfernen.

## Kann ich die ECIDs migrieren, wenn ich Alloy verwende, damit meine Website-Besucher nicht als neue Besucher angezeigt werden?

Ja, das Adobe Experience Platform Web SDK bietet eine Funktion zur Identitätsmigration. Befolgen Sie die Anweisungen zur ID-Migration im Abschnitt [Identitätsdokumentation für Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) für weitere Details.

## Inwiefern unterscheidet sich das Web SDK von Tags?

* **Tags in Experience Platform** den Gerätecode verwalten. Verwenden Sie sie, um den Code einfacher bereitzustellen. Sie sind frei und mächtig.

* **Adobe Experience Platform Web SDK** ist der offizielle Name des neuen Codes, der von Tags für Anwendungsfälle der Adobe bereitgestellt wird. Es ist auch frei und mächtig.

* **`alloy.js`** ist der Dateiname des Adobe Experience Platform Web SDK-Codes.

## Muss ich Tags verwenden, um das Web SDK bereitzustellen?

Nein. Sie können die `alloy.js` Datei selbst.

Beachten Sie jedoch Folgendes:

* Das Adobe Experience Platform Web SDK erfordert eine so genannte Datastream-ID, damit das Edge-Netzwerk den Stream identifizieren und bestimmen kann, was mit den Daten zu tun ist. Diese ID wird innerhalb von Experience Platform erstellt. Dies bedeutet nicht, dass Sie die Benutzeroberfläche verwenden müssen, um Eigenschaften zu erstellen oder den JavaScript-Code bereitzustellen. Sie müssen jedoch Tags verwenden, um eine Konfigurations-ID zu erstellen.

* Tags sind nicht nur der beste verfügbare Tag- und SDK-Manager, sondern machen es auch sehr einfach, `alloy.js` und ordnen Daten XDM-Schemas zu. Wenn Sie sich gegen die Verwendung von Tags entscheiden, müssen Sie die Bereitstellung von `alloy.js`, Ereignissen und Zuordnen Ihrer Daten zu XDM vor dem Senden. Dies ist ein _viel_ ist schwieriger als die Verwendung von Tags.

* Es wird empfohlen, zum Bereitstellen von Tags `alloy.js`, auch wenn es das einzige Tag ist, für das Sie es verwenden.

## Was ist die Ereignisweiterleitung?

Wenn Sie unsere SDKs verwenden und XDM an Experience Edge senden, können Sie mit dieser neuen Funktionen-Ereignisweiterleitung neue Server-seitige Erweiterungen installieren und diese Daten auf beliebige Elemente aus unserem Edge-Netzwerk zuordnen - und an beliebige Stellen senden. Stellen Sie sich dies als &quot;Datenerfassung als Dienst&quot;vor. Dies ist kostenpflichtig und wird als Teil von Adobe Experience Platform gebündelt.

## Was ist ein CNAME oder eine Erstanbieterdomäne und warum ist dies wichtig?

Weitere Informationen zu einem CNAME finden Sie im [Dokumentation zur Adobe](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html?lang=de)

## Verwendet das Adobe Experience Platform Web SDK Cookies? Wenn ja, welche Cookies werden verwendet?

Ja, das Web SDK verwendet derzeit je nach Implementierung zwischen einem und sieben Cookies. Im Folgenden finden Sie eine Liste der Cookies, die mit dem Web SDK angezeigt werden, sowie ihre Verwendung:

| **Name** | **maxAge** | **Freundliches Alter** | **Beschreibung** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 Tage | Das Identitäts-Cookie speichert die ECID sowie andere Informationen zur ECID. |
| **kndctr_orgid_consent_check** | 7200 | 2 Stunden | Dieses Cookie speichert die Zustimmungsvoreinstellung des Benutzers für die Website. |
| **kndctr_orgid_consent** | 15552000 | 180 Tage | Dieses sitzungsbasierte Cookie signalisiert dem Server, die Zustimmungsvoreinstellungen serverseitig zu suchen. |
| **kndctr_orgid_cluster** | 1800 | 30 Minuten | Dieses Cookie speichert den Experience Edge-Bereich, der die Anforderungen des aktuellen Benutzers erfüllt. Der Bereich wird im URL-Pfad verwendet, damit Experience Edge die Anforderung an den richtigen Bereich weiterleiten kann. Dieses Cookie hat eine Lebensdauer von 30 Minuten. Wenn ein Benutzer eine Verbindung mit einer anderen IP-Adresse herstellt, kann die Anforderung an den nächsten Bereich weitergeleitet werden. |
| **mbox** | 63072000 | 2 Jahre | Dieses Cookie wird angezeigt, wenn die Target-Migrationseinstellung auf &quot;true&quot;gesetzt ist. Dadurch kann Target [Mbox-Cookie](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) vom Web SDK festgelegt werden. |
| **mboxEdgeCluster** | 1800 | 30 Minuten | Dieses Cookie wird angezeigt, wenn die Target-Migrationseinstellung auf &quot;true&quot;gesetzt ist. Mit diesem Cookie kann das Web SDK den richtigen Edge-Cluster mit at.js kommunizieren, damit Target-Profile synchronisiert bleiben können, wenn Benutzer auf einer Site navigieren. |
| **AMCV_###@AdobeOrg** | 34128000 | 395 Tage | Dieses Cookie wird nur angezeigt, wenn die ID-Migration im Adobe Experience Platform Web SDK aktiviert ist. Dieses Cookie hilft beim Übergang zum Web SDK, während einige Teile der Site weiterhin visitor.js verwenden. Siehe [idMigrationEnabled-Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/configuring-the-sdk.html?lang=en#identity-options) um mehr über diese Einstellung zu erfahren. |

Bei Verwendung des Web SDK setzt das Edge Network mindestens eines der oben genannten Cookies. Das Edge-Netzwerk setzt alle Cookies mit dem `secure` und `sameSite="none"` -Attribute.

Wenn Ihre Website derzeit sowohl sichere als auch nicht sichere Abschnitte enthält, kann dies die Benutzeridentifizierung beeinträchtigen. Wenn ein Benutzer von einem sicheren Bereich der Site zu einem nicht sicheren Bereich navigiert, generiert das Edge-Netzwerk eine neue `ECID` mit der Anfrage.

## Welche Browser unterstützt das Adobe Experience Platform Web SDK?

Das Adobe Experience Platform Web SDK wurde für die optimale Verwendung in den neuesten Versionen von Google Chrome, Safari, Firefox, Internet Explorer 11 und Microsoft Edge Chromium entwickelt. Möglicherweise haben Sie bei der Verwendung bestimmter Funktionen in älteren Versionen von Browsern Probleme.

## Wo erhalte ich weitere Informationen zum Adobe Experience Platform Web SDK?

* [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=de)
* [Quell-Code](https://github.com/adobe/alloy)
