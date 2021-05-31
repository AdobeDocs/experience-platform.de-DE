---
title: Häufig gestellte Fragen zum Adobe Experience Platform Web SDK
description: Erhalten Sie Antworten auf häufig gestellte Fragen zum Adobe Experience Platform Web SDK.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: c3d66e50f647c2203fcdd5ad36ad86ed223733e3
workflow-type: tm+mt
source-wordcount: '1843'
ht-degree: 2%

---

# Häufig gestellte Fragen

Dieses Handbuch enthält Antworten auf häufig zum Adobe Experience Platform Web SDK gestellte Fragen.

## Was ist das Adobe Experience Platform Web SDK?

Das Adobe Experience Platform Web SDK ist eine Client-seitige JavaScript-Bibliothek, die es Kunden von Adobe Experience Cloud ermöglicht, mit den verschiedenen Diensten im Experience Cloud zu interagieren.

Es sendet Daten auf lösungsunabhängige Weise (XDM) an das Adobe Experience Platform Edge Network, das die Daten dann lösungsspezifischen Formaten und Zielen zuordnet und in Echtzeit sendet.

**Weitere**
[InformationenAdobe Summit-Präsentation](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Inwiefern unterscheidet sich das Adobe Experience Platform Web SDK von früheren Lösungen?

### Vor Adobe Experience Platform SDK

Derzeit müssen Sie je nach Lösung unterschiedliche JavaScript-Bibliotheken bereitstellen.

* Jede Lösung verfügt über eine eigene JavaScript-Bibliothek, ein eigenes Schema und eine eigene Domäne.
* Keine dieser Bibliotheken wurde für die Zusammenarbeit erstellt.
* Bei lösungsübergreifenden und Adobe Experience Platform-Anwendungsfällen müssen diese unterschiedlichen Bibliotheken voneinander abhängig sein, was zu Problemen bei der Implementierung führt.

Obwohl Adobe Experience Platform Launch die Bereitstellung und Verwaltung dieser Bibliotheken so einfach wie möglich macht, gibt es nach wie vor Probleme mit:

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
* Visitor ID
* Adobe Experience Platform

Weitere Lösungen werden im Laufe dieses Jahres folgen.

Adobe Experience Platform Web SDK kann auch Daten direkt an Adobe Experience Platform senden. Diese Daten befinden sich in XDM und werden dem serverseitigen Lösungsschema zugeordnet.

## Welchen Wert hat dieses neue Web SDK?

**Leistung:** Das Web-SDK ist kleiner als die Verwendung aller aktuellen Adobe-Bibliotheken und bietet deutlich schnellere Seitenladevorgänge.

**Einfachheit:** Die Kombination aus XDM, Web SDK, Experience Platform Launch, Experience Edge, Adobe Experience Cloud-Lösungen und Adobe Experience Platform ermöglicht eine einfach zu verständliche und zu befolgende Datenerfassung.

* **XDM:** Das Lösungsagnostische Schema, mit dem Sie Daten an Adobe senden. Kein Tagging für eVars oder Mboxes mehr.
* **Adobe Experience Platform Web SDK:** Erleichtert das Senden und Empfangen von Daten an Adobe Experience Platform Edge Network.
* **Experience Platform Launch:** vereinfacht die Bereitstellung und Konfiguration des Web SDK (und anderer JavaScript-Tags) auf einer Site.
* **Experience Edge:** Leicht die Daten an Adobe Experience Platform und Lösungen im benötigten Format weiterleiten.
* **Adobe Experience Platform- und Adobe-Lösungen:** Aktivieren Sie deren Wertvorschlag.

**Kontrolle:** Da alle Daten einen einzigen und verbundenen Datenstrom verwenden, können Sie logisch verfolgen und steuern, wie die Daten bei jeder Millisekunde ihrer Journey aussehen, zu und von Anwendungen.

**Modern und zukunftsbereit:**  Das Web SDK und seine Verbindung zum Experience Edge Network haben es der Adobe ermöglicht, die Art und Weise, in der Adobe mit der Datenerfassung, Personalisierung, Einwilligung und Zukunft von Drittanbieter-Cookies umgeht, erheblich zu modernisieren. (Dadurch wird eine Erstanbieterdomäne aktiviert, die von Adobe verwaltet wird.)

**Time-to-Value:** Adobe hat hart gearbeitet (und wird dies auch weiterhin tun), um die Bereitstellung des Web-SDK über Experience Platform Launch und die Zuordnung clientseitiger Daten zu XDM so einfach wie möglich zu machen.  Nach Abschluss dieser Arbeit können alle anderen Adobe-Lösungen und Adobe Experience Platform-Dienste serverseitig aktiviert oder deaktiviert werden. Wenn Sie dies beispielsweise für Adobe Analytics verwenden und Target oder Experience Platform aktivieren möchten, können Sie einfach einen Umschalter in der Datastream-Konfiguration aktivieren und diese Anwendungsfälle aufleuchten.

## Was ist Alloy?

Alloy ist der Codename für das Adobe Experience Platform Web SDK. Sie wird im Quellcode und Dateinamen des SDK verwendet, obwohl das Adobe Experience Platform Web SDK der offizielle Name ist.

## Müssen Kunden Adobe Experience Platform kaufen, um das Web SDK zu verwenden?

Nein. Jeder Adobe Digital Experience-Kunde kann es verwenden. Ganz kostenlos. Kunden, die das Web SDK verwenden möchten, erhalten Zugriff auf die Erstellung von Schemas und Datensätzen in der Adobe Experience Platform-Benutzeroberfläche.

## Wer sollte das Web SDK verwenden?

Das Adobe Experience Platform Web SDK wurde für folgende Personen entwickelt:

* Adobe Experience Platform-Benutzer

   Wenn Sie Daten direkt von einem Gerät an Adobe Experience Platform senden müssen, wird dies offiziell empfohlen.

   Adobe ist sich bewusst, dass die Verwendung des Adobe Analytics-Connectors schneller ist, wenn der Kunde bereits über Adobe Analytics verfügt. Dies ist jedoch nicht die langfristige Strategie für die Datenerfassung.

* Adobe Experience Cloud-Lösungskunden

   Neue Kunden von Adobe Analytics, Adobe Audience Manager und Adobe Target sollten mit dem neuen Web SDK beginnen und keine älteren Bibliotheken verwenden.

   Bestehende Kunden, die die bestmögliche Implementierung erhalten möchten, sollten das neue Web SDK verwenden.


## Wie erhalte ich Zugriff auf die Verwendung des Adobe Experience Platform Web SDK?

Das Web SDK ist derzeit für die allgemeine Öffentlichkeit verfügbar und kann zum Senden von Daten an Adobe Experience Cloud-Produkte verwendet werden. Die Möglichkeit, Daten an Drittanbieterlösungen zu senden, wird in naher Zukunft eingeführt. Das SDK ist kostenlos, wird von Adobe kostenlos gehostet und kann heruntergeladen werden, damit Sie es auf Ihren eigenen Servern hosten können, falls gewünscht, kostenlos. Das Platform Web SDK benötigt Zugriff auf Datastream-Konfigurationen und den Adobe Experience Platform XDM-Schema-Builder, damit die Server der Adobe eingehende Daten aus dem SDK ordnungsgemäß verarbeiten können. Wenn Sie Zugriff erhalten möchten, wenden Sie sich an Ihren Customer Success Manager (CSM), um den Anforderungsprozess zu starten.

## Welche Anwendungsfälle werden derzeit vom Web SDK unterstützt?

Das Web SDK entwickelt sich schnell. An weiteren Anwendungsfällen wird gearbeitet. Die Liste der aktuell unterstützten Anwendungsfälle finden Sie hier.](https://github.com/adobe/alloy/projects/5)[

## Müssen aktuelle Kunden ihre Sites neu taggen?

Das hängt von Ihrer aktuellen Situation ab. Das Adobe Experience Platform Web SDK kann in zwei verschiedenen Stilen bereitgestellt werden. Ein zukünftiges Migrationsdokument enthält zusätzliche Details.

* **Nur ein weiteres Tag:**  Wenn die Site bereits für Lösungen getaggt ist und Sie keine neuen Tags erstellen können, aber Daten für Anwendungsfälle der Experience Platform an Adobe Experience Platform Edge Network oder die bevorstehenden serverseitigen Funktionen des Experience Platform Launchs senden möchten (siehe unten), können Sie das  `alloy.js` Tag zur Site hinzufügen, wo es als &quot;weiteres Tag&quot;funktioniert.

* **Das einzige und einzige Tag:** Wenn Sie das Web SDK für eine Experience Cloud-Lösung verwenden möchten, müssen Sie es für  __ alle Lösungen auf dieser Seite verwenden. Wenn Ihre Site beispielsweise bereits für Adobe Analytics getaggt ist und Sie sie für Target verwenden möchten, müssen Sie sie sowohl für beide als auch für alle anderen künftig verwenden.

Wenn Sie sich also dafür entscheiden, das Adobe Experience Platform Web SDK für Anwendungsfälle ohne Lösung zu verwenden, können Sie die Site mit `alloy.js` taggen und so weitermachen, als wäre dies eine neue Lösung. Wenn Sie ihn für Adobe Analytics, Target, Audience Manager oder Anwendungsfälle verwenden möchten, müssen Sie möglicherweise den alten Code auf Ihrer Seite entfernen.

## Kann ich die ECIDs migrieren, wenn ich Alloy verwende, damit meine Website-Besucher nicht als neue Besucher angezeigt werden?

Ja, das Adobe Experience Platform Web SDK bietet eine Funktion zur Identitätsmigration. Befolgen Sie die Anweisungen zur ID-Migration in der [Platform Web SDK-Identitätsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) , um weitere Details zu erhalten.

## Inwiefern unterscheidet sich das Web SDK von Adobe Experience Platform Launch?

* **Experience Platform** Launch ist der Geräte-Code-Manager. Verwenden Sie sie, um den Code einfacher bereitzustellen. Es ist frei und mächtig.

* **Adobe Experience Platform Web** SDK ist der offizielle Name des neuen Codes, der vom Experience Platform Launch für Anwendungsfälle der Adobe bereitgestellt wird. Es ist auch frei und mächtig.

* **`alloy.js`** ist der Dateiname des Adobe Experience Platform Web SDK-Codes.

## Muss ich Adobe Experience Platform Launch verwenden, um das Web SDK bereitzustellen?

Nein. Sie können die `alloy.js`-Datei selbst herunterladen.

Beachten Sie jedoch Folgendes:

* Das Adobe Experience Platform Web SDK erfordert eine so genannte Datastream-ID, damit das Edge-Netzwerk den Stream identifizieren und bestimmen kann, was mit den Daten zu tun ist. Diese ID wird in Experience Platform Launch erstellt. Dies bedeutet nicht, dass Sie Experience Platform Launch zum Erstellen von Eigenschaften oder Bereitstellen des JavaScript-Codes verwenden müssen. Sie müssen jedoch Experience Platform Launch verwenden, um eine Konfigurations-ID zu erstellen.

* Adobe Experience Platform Launch ist nicht nur der beste verfügbare Tag- und SDK-Manager, es erleichtert die Bereitstellung von `alloy.js` und die Zuordnung von Daten zu XDM-Schemas. Wenn Sie sich gegen die Verwendung von Experience Platform Launch entscheiden, müssen Sie die Bereitstellung von `alloy.js`, das Eventing und die Zuordnung Ihrer Daten zu XDM verwalten, bevor Sie sie senden. Dies ist ein _viel_ schwierigerer Prozess als die Verwendung von Experience Platform Launch.

* Es wird empfohlen, für die Bereitstellung von `alloy.js` Experience Platform Launch zu verwenden, selbst wenn es das einzige Tag ist, für das Sie es verwenden.

## Was ist &quot;Adobe Experience Platform Launch Server Side&quot;?

Später im Jahr 2020 werden Experience Platform Launch Funktionen für die serverseitige Weiterleitung veröffentlichen. Wenn Sie unsere SDKs verwenden und XDM an Experience Edge senden, können Sie mit diesen neuen Funktionen neue Server-seitige Erweiterungen installieren und diese Daten auf beliebige Elemente aus unserem Edge-Netzwerk zuordnen - und an beliebige Standorte senden. Stellen Sie sich dies als &quot;Datenerfassung als Dienst&quot;vor.  Dies ist kostenpflichtig und wird als Teil von Adobe Experience Platform gebündelt.

## Was ist ein CNAME oder eine Erstanbieterdomäne und warum ist dies wichtig?

Weitere Informationen zu einem CNAME finden Sie in der [Adobe-Dokumentation](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html) .

## Verwendet das Adobe Experience Platform Web SDK Cookies? Wenn ja, welche Cookies werden verwendet?

Ja, das Web SDK verwendet derzeit je nach Implementierung zwischen 1 und 4 Cookies. Nachstehend finden Sie eine Liste der vier Cookies, die Sie möglicherweise mit dem Web SDK und der Art ihrer Verwendung sehen:

**kndct_orgid_identity:** Das Identitäts-Cookie wird zum Speichern der ECID sowie einiger anderer Informationen im Zusammenhang mit der ECID verwendet.

**kndctr_orgid_consent:** Dieses Cookie speichert die Zustimmungsvoreinstellung des Benutzers für die Website.

**kndctr_orgid_personalization:**  Dieses Cookie enthält Sitzungsinformationen, die Adobe Target zum Personalisieren von Webseiten verwendet.

**kndctr_orgid_consentCheck:**  Dieses sitzungsbasierte Cookie signalisiert dem Server, die Voreinstellungen für die Zustimmung serverseitig zu durchsuchen.

## Welche Browser unterstützt das Adobe Experience Platform Web SDK?

Das Adobe Experience Platform Web SDK wurde für die optimale Verwendung in den neuesten Versionen von Google Chrome, Safari, Firefox, Internet Explorer 11 und Microsoft Edge Chromium entwickelt. Möglicherweise haben Sie bei der Verwendung bestimmter Funktionen in älteren Versionen von Browsern Probleme.

## Wo erhalte ich weitere Informationen zum Adobe Experience Platform Web SDK?

* [Dokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* [Quellcode](https://github.com/adobe/alloy)
