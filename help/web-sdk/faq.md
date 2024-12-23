---
title: Häufig gestellte Fragen zum Adobe Experience Platform Web SDK
description: Erhalten Sie Antworten auf häufig gestellte Fragen zum Adobe Experience Platform Web SDK.
source-git-commit: ed22c76b2805f1baab2ae3c82e1133e1fd8c9f72
workflow-type: tm+mt
source-wordcount: '2033'
ht-degree: 2%

---


# Häufig gestellte Fragen

Dieses Handbuch enthält Antworten auf häufig zum Adobe Experience Platform Web SDK gestellte Fragen.

## Was ist das Adobe Experience Platform Web SDK?

Das Adobe Experience Platform Web SDK ist eine Client-seitige JavaScript-Bibliothek, mit der Sie mit den verschiedenen Diensten in Adobe Experience Cloud interagieren können.

Das Web SDK sendet Daten auf lösungsunabhängige Weise (XDM) an das Experience Platform-Edge Network, das die Daten dann lösungsspezifischen Formaten und Zielen zuordnet und in Echtzeit sendet.

Weitere Informationen zum Web-SDK finden Sie im folgenden Video: [Erfüllen Sie Alloy.js und &quot;Niemals taggen&quot;für eine eVar oder Mbox erneut](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html).

## Inwiefern unterscheidet sich das Adobe Experience Platform Web SDK von früheren Lösungen?

### Vor Experience Platform Web SDK

Derzeit müssen Sie je nach Lösung verschiedene JavaScript-Bibliotheken bereitstellen.

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

### Mit Experience Platform Web SDK

Das neue Web SDK sendet Daten für die folgenden Lösungen an ein einzelnes Ziel (Experience Platform-Edge Network) und löst die häufigsten oben genannten Lösungsanwendungsfälle.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Besucher-ID
* Adobe Experience Platform

Andere Lösungen werden folgen.

Das Adobe Experience Platform Web SDK kann auch Daten direkt an Adobe Experience Platform senden. Diese Daten liegen im XDM-Format vor und werden dem serverseitigen Lösungsschema zugeordnet.

## Welchen Wert hat dieses neue Web SDK?

**Leistung:** Das Web-SDK ist kleiner als die Verwendung aller aktuellen Adobe-Bibliotheken und bietet deutlich schnellere Seitenladevorgänge.

**Einfachheit:** Die Kombination aus XDM, Web SDK, Tags, Edge Network, Adobe Experience Cloud-Lösungen und Adobe Experience Platform bietet eine einfach zu verständliche und zu befolgende Datenerfassung.

* **XDM:** Das lösungsagnostische Schema, mit dem Sie Daten an Adobe senden. Kein Tagging für eVars oder Mboxes mehr.
* **Web SDK:** Erleichtert das Senden und Empfangen von Daten an das Adobe Experience Platform-Edge Network.
* **Tags:** Vereinfacht die Bereitstellung und Konfiguration des Web SDK (und anderer JavaScript-Tags) auf einer Site.
* **Edge Network:** Leichte Weiterleitung der Daten an Adobe Experience Platform und Lösungen im benötigten Format.
* **Adobe Experience Platform- und Adobe-Lösungen:** Aktivieren Sie deren Wertvorschlag.

**Kontrolle:** Da alle Daten einen einzigen und verbundenen Datenstrom verwenden, können Sie logisch verfolgen und steuern, wie die Daten in jeder Millisekunde ihres Journey-Datums aussehen, zu und von Anwendungen.

**Modernst und zukunftsbereit:** Das Web SDK und seine Verbindung zum Edge Network haben es Adobe ermöglicht, die Art und Weise, in der Adobe mit der Datenerfassung, Personalisierung, Einwilligung und Zukunft von Drittanbieter-Cookies umgeht, erheblich zu modernisieren. (Dadurch wird eine Erstanbieterdomäne aktiviert, die von Adobe verwaltet wird.)

**Time-to-Value:** Adobe hat hart gearbeitet (und wird dies auch weiterhin tun), um die Bereitstellung des Web-SDK über Tags und die Zuordnung clientseitiger Daten zu XDM so einfach wie möglich zu machen. Nach Abschluss dieser Arbeit können alle anderen Adobe-Lösungen und Adobe Experience Platform-Dienste serverseitig aktiviert oder deaktiviert werden. Wenn Sie dies beispielsweise für Adobe Analytics verwenden und Target oder Experience Platform aktivieren möchten, können Sie einfach einen Umschalter in der Datastream-Konfiguration aktivieren und diese Anwendungsfälle aufleuchten lassen.

## Was ist [!DNL alloy.js]?

[!DNL alloy.js] ist der Name der Web SDK JavaScript-Bibliothek. Sie wird im SDK-Quellcode und -Dateinamen referenziert.

## Müssen Kunden Adobe Experience Platform kaufen, um die [!DNL Web SDK] zu verwenden?

Nein. Jeder Adobe Digital Experience-Kunde kann das Adobe Experience Platform Web SDK kostenlos nutzen. Kunden, die den [!DNL Web SDK] verwenden möchten, müssen die richtigen Berechtigungen zum Erstellen von Schemas, Datensätzen, Identitäts-Namespaces und Datensätzen in der Datenerfassungs-Benutzeroberfläche oder Experience Platform-Benutzeroberfläche konfigurieren.

Weitere Informationen zum Konfigurieren dieser Berechtigungen finden Sie in unserer Dokumentation zum [Berechtigungsverwaltung für die Datenerfassung](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## Wer sollte das Web SDK verwenden?

Das Adobe Experience Platform Web SDK wurde für folgende Kunden entwickelt:

* Adobe Experience Platform-Benutzer
   * Wenn Sie Daten direkt von einem Gerät an Adobe Experience Platform senden müssen, wird dies offiziell empfohlen.
   * Adobe ist sich bewusst, dass die Verwendung des Adobe Analytics-Connectors schneller ist, wenn Sie bereits über Adobe Analytics verfügen, dies jedoch nicht die langfristige Strategie für die Datenerfassung ist.

* Adobe Experience Cloud-Lösungskunden
   * Neue Kunden von Adobe Analytics, Adobe Audience Manager und Adobe Target sollten mit dem neuen Web SDK beginnen und keine älteren Bibliotheken verwenden.
   * Bestehende Kunden, die die bestmögliche Implementierung erhalten möchten, sollten das neue Web SDK verwenden.

## Wie erhalte ich Zugriff auf das Web SDK?

Das Web SDK ist derzeit für die allgemeine Öffentlichkeit verfügbar und kann zum Senden von Daten an Adobe Experience Cloud-Produkte verwendet werden. Die Möglichkeit, Daten an Drittanbieterlösungen zu senden, wird in naher Zukunft eingeführt.

Das SDK ist kostenlos und wird von Adobe kostenlos gehostet. Bei Bedarf können Sie es herunterladen und kostenlos auf Ihren eigenen Servern hosten.

Das Web SDK benötigt Zugriff auf [Datastream-Konfigurationen](../datastreams/overview.md) und den Experience Platform [XDM-Schema-Builder](../xdm/tutorials/create-schema-ui.md), damit Adobe-Server eingehende Daten, die vom SDK kommen, ordnungsgemäß verarbeiten können. Wenn Sie Zugriff erhalten möchten, wenden Sie sich an Ihr Adobe-Account-Team, um den Anforderungsprozess zu starten.

## Welche Anwendungsfälle werden derzeit vom Web SDK unterstützt?

Das Web SDK entwickelt sich schnell. An weiteren Anwendungsfällen wird gearbeitet. Die derzeit unterstützte [ Liste der Anwendungsfälle finden Sie hier.](https://github.com/orgs/adobe/projects/18/views/1?filterQuery=)

## Müssen aktuelle Kunden ihre Sites neu taggen?

Es kommt darauf an. Das Adobe Experience Platform Web SDK kann in zwei verschiedenen Stilen bereitgestellt werden. Ein zukünftiges Migrationsdokument enthält zusätzliche Details.

* **Nur ein weiteres Tag:** Wenn die Site bereits für Lösungen getaggt ist und Sie keine neuen Tags erstellen können, Sie aber Daten für Experience Platform-Anwendungsfälle oder die bevorstehenden Ereignisweiterleitungsfunktionen an das Adobe Experience Platform-Edge Network senden möchten (siehe unten), können Sie das Tag `alloy.js` zur Site hinzufügen, wo es als &quot;weiteres Tag&quot;funktioniert.

* **Das einzige und einzige Tag:** Wenn Sie das Web SDK für eine Experience Cloud-Lösung verwenden möchten, müssen Sie es für _alle_ der Lösungen auf dieser Seite verwenden. Wenn Ihre Site beispielsweise bereits für Adobe Analytics getaggt ist und Sie sie für Target verwenden möchten, müssen Sie sie sowohl für beide als auch für alle anderen künftig verwenden.

Mit anderen Worten: Wenn Sie sich dafür entscheiden, das Adobe Experience Platform Web SDK für Anwendungsfälle ohne Lösung zu verwenden, können Sie die Site mit `alloy.js` versehen und weitermachen, als wäre dies eine neue Lösung. Wenn Sie ihn für Adobe Analytics, Target, Audience Manager oder Anwendungsfälle verwenden möchten, müssen Sie möglicherweise den alten Code auf Ihrer Seite entfernen.

## Kann ich die ECIDs migrieren, wenn ich Web SDK verwende, damit meine Website-Besucher nicht als neue Besucher angezeigt werden?

Ja, das Adobe Experience Platform Web SDK bietet eine Funktion zur Identitätsmigration. Befolgen Sie die Anweisungen zur ID-Migration in der [Identitätsdokumentation für das Platform Web SDK](/help/web-sdk/identity/overview.md#id-migration) , um weitere Informationen zu erhalten.

## Inwiefern unterscheidet sich das Web SDK von Tags?

* **Tags in Experience Platform** verwalten den Gerätecode. Verwenden Sie sie, um den Code einfacher bereitzustellen. Sie sind frei und mächtig.

* **Adobe Experience Platform Web SDK** ist der offizielle Name des neuen Codes, der von Tags für Adobe-Anwendungsfälle bereitgestellt wird. Es ist auch frei und mächtig.

* **`alloy.js`** ist der Dateiname des Adobe Experience Platform Web SDK-Codes.

## Muss ich Tags verwenden, um das Web SDK bereitzustellen?

Nein. Sie können die `alloy.js`-Datei selbst herunterladen.

Allerdings:

* Das Adobe Experience Platform Web SDK erfordert eine so genannte Datastream-ID, damit das Edge-Netzwerk den Stream identifizieren und bestimmen kann, was mit den Daten zu tun ist. Diese ID wird innerhalb von Experience Platform erstellt. Dies bedeutet nicht, dass Sie die Benutzeroberfläche verwenden müssen, um Eigenschaften zu erstellen oder den JavaScript-Code bereitzustellen. Sie müssen jedoch Tags verwenden, um eine Konfigurations-ID zu erstellen.

* Tags sind nicht nur das beste verfügbare Tag- und SDK-Manager, sondern machen es auch sehr einfach, `alloy.js` bereitzustellen und Daten XDM-Schemas zuzuordnen. Wenn Sie sich gegen die Verwendung von Tags entscheiden, müssen Sie die Bereitstellung von `alloy.js`, das Eventing und die Zuordnung Ihrer Daten zu XDM verwalten, bevor Sie sie senden. Dies ist ein _viel_ schwierigerer Prozess als die Verwendung von Tags.

* Es wird empfohlen, zur Bereitstellung von `alloy.js` Tags zu verwenden, selbst wenn es das einzige Tag ist, für das Sie es verwenden.

## Was ist die Ereignisweiterleitung?

Wenn Sie unsere SDKs verwenden und XDM an das Edge Network senden, können Sie mit dieser neuen Funktion die Ereignisweiterleitung nutzen, um neue serverseitige Erweiterungen zu installieren und diese Daten auf beliebige Elemente von unserem Edge-Netzwerk zu übertragen - und an beliebige Stellen zu senden. Stellen Sie sich dies als &quot;Datenerfassung als Dienst&quot;vor. Dies ist kostenpflichtig und wird als Teil von Adobe Experience Platform gebündelt.

## Was ist ein CNAME oder eine Erstanbieterdomäne und warum ist dies wichtig?

Weitere Informationen zu einem CNAME finden Sie in der [Adobe-Dokumentation](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html?lang=de) .

## Verwendet das Adobe Experience Platform Web SDK Cookies? Wenn ja, welche Cookies werden verwendet?

Ja, das Web SDK verwendet derzeit je nach Implementierung zwischen einem und sieben Cookies. Im Folgenden finden Sie eine Liste der Cookies, die mit dem Web SDK angezeigt werden, sowie ihre Verwendung:

| **Name** | **maxAge** | **Anzeigenalter** | **Beschreibung** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 Tage | Das Identitäts-Cookie speichert die ECID sowie andere Informationen zur ECID. |
| **kndctr_orgid_consent_check** | 7200 | 2 Stunden | Dieses sitzungsbasierte Cookie signalisiert dem Server, die Zustimmungsvoreinstellungen serverseitig zu suchen. |
| **kndctr_orgid_consent** | 15552000 | 180 Tage | Dieses Cookie speichert die Zustimmungsvoreinstellung des Benutzers für die Website. |
| **kndctr_orgid_cluster** | 1800 | 30 Minuten | Dieses Cookie speichert den Edge Network-Bereich, der die Anforderungen des aktuellen Benutzers erfüllt. Der Bereich wird im URL-Pfad verwendet, damit das Edge Network die Anfrage an den richtigen Bereich weiterleiten kann. Dieses Cookie hat eine Lebensdauer von 30 Minuten. Wenn ein Benutzer eine Verbindung mit einer anderen IP-Adresse herstellt, kann die Anforderung an den nächsten Bereich weitergeleitet werden. |
| **mbox** | 63072000 | 2 Jahre | Dieses Cookie wird angezeigt, wenn die Target-Migrationseinstellung auf &quot;true&quot;gesetzt ist. Dadurch kann das Target-[mbox-Cookie](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) vom Web SDK gesetzt werden. |
| **mboxEdgeCluster** | 1800 | 30 Minuten | Dieses Cookie wird angezeigt, wenn die Target-Migrationseinstellung auf &quot;true&quot;gesetzt ist. Mit diesem Cookie kann das Web SDK den richtigen Edge-Cluster mit at.js kommunizieren, damit Target-Profile synchronisiert bleiben können, wenn Benutzer auf einer Site navigieren. |
| **AMCV_###@AdobeOrg** | 34128000 | 395 Tage | Dieses Cookie wird nur angezeigt, wenn die ID-Migration im Adobe Experience Platform Web SDK aktiviert ist. Dieses Cookie hilft beim Übergang zum Web SDK, während einige Teile der Site noch visitor.js verwenden. Weitere Informationen finden Sie unter [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md) . |

Bei Verwendung des Web SDK setzt das Edge Network eines oder mehrere der oben genannten Cookies. Das Edge Network setzt alle Cookies mit den Attributen `secure` und `sameSite="none"`.

Wenn Ihre Website derzeit sowohl sichere als auch nicht sichere Abschnitte enthält, kann dies die Benutzeridentifizierung beeinträchtigen. Wenn ein Benutzer von einem sicheren Bereich der Site zu einem nicht sicheren Bereich navigiert, generiert das Edge Network eine neue `ECID` mit der Anforderung.

## Welche Browser unterstützt das Adobe Experience Platform Web SDK?

Das Adobe Experience Platform Web SDK wurde für die optimale Verwendung in den neuesten Versionen von Google Chrome, Safari, Firefox und Microsoft Edge Chromium entwickelt. Bei der Verwendung bestimmter Funktionen in älteren Versionen von Browsern oder veralteten Browsern wie Internet Explorer kann es zu Problemen kommen.

## Wo erhalte ich weitere Informationen zum Adobe Experience Platform Web SDK?

* [Dokumentation](/help/web-sdk/home.md)
* [Source-Code](https://github.com/adobe/alloy)