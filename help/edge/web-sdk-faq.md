---
title: Häufig gestellte Fragen zum Adobe Experience Platform Web SDK
description: Erhalten Sie Antworten auf häufig gestellte Fragen zum Adobe Experience Platform Web SDK.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 5ead9dc72b8b9fe89e0a1bc8365ceff8affd3c85
workflow-type: tm+mt
source-wordcount: '1847'
ht-degree: 2%

---

# Häufig gestellte Fragen 

Dieses Handbuch enthält Antworten auf häufig gestellte Fragen zum Adobe Experience Platform Web SDK.

## Was ist das Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK ist eine clientseitige JavaScript-Bibliothek, die es Kunden von Adobe Experience Cloud ermöglicht, mit den verschiedenen Diensten im Experience Cloud zu interagieren.

Es sendet Daten auf lösungsunabhängige Weise (XDM) an das Adobe Experience Platform Edge Network, das die Daten dann lösungsspezifischen Formaten und Zielen zuordnet und sie dann in Echtzeit sendet.

**Weitere**
[InformationenAdobe Summit-Präsentation](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Inwiefern unterscheidet sich das Adobe Experience Platform Web SDK von früheren Lösungen?

### Vor dem Adobe Experience Platform SDK

Derzeit müssen Sie je nach Lösung unterschiedliche JavaScript-Bibliotheken bereitstellen.

* Jede Lösung verfügt über eine eigene JavaScript-Bibliothek, ein eigenes Schema und eine eigene Domäne.
* Keine dieser Bibliotheken wurde für die Zusammenarbeit gebaut.
* Bei lösungsübergreifenden und Adobe Experience Platform-Anwendungsfällen müssen diese unterschiedlichen Bibliotheken voneinander abhängig sein, was zu Unterbrechungen bei der Bereitstellung führt.

Obwohl Adobe Experience Platform Launch die Bereitstellung und Verwaltung dieser Bibliotheken so einfach wie möglich macht, gibt es immer noch Probleme mit:

* Bibliotheksgröße (zu viel Adobe-Code auf einer Seite)
* Leistung (das Laden von Sites dauert zu lange.)
* Mehrere Aufrufe für einen einzelnen Anwendungsfall
* Warten auf ECID-Rückkehr vor Personalisierungsaufrufen (Ursachen: Verzögerung)
* Fragmentierte Datenerfassung (was ist eine evar?)
* Schema-Verwirrung zwischen Lösungen (A4T)
* Viele andere weniger optimale Dinge

Außerdem gibt es derzeit keine JavaScript-Bibliothek, die Daten direkt an Adobe Experience Platform sendet.

### Mit Adobe Experience Platform Web SDK

Das neue Web SDK sendet Daten für die folgenden Lösungen an ein einziges Ziel (Adobe Experience Platform Edge Network) und löst die gängigsten oben genannten Anwendungsfälle für Lösungen.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Visitor ID
* Adobe Experience Platform

Weitere Lösungen werden im Laufe dieses Jahres folgen.

Adobe Experience Platform Web SDK kann auch Daten direkt an Adobe Experience Platform senden. Diese Daten befinden sich im XDM-Format und werden dem serverseitigen Lösungs-Schema zugeordnet.

## Welchen Wert hat dieses neue Web SDK?

**Leistung:** Das Web-SDK ist kleiner als alle aktuellen Bibliotheken der Adobe und bietet deutlich schnellere Seitenladevorgänge.

**Einfachheit:** Die Kombination aus XDM-, Web-SDK-, Experience Platform Launch-, Experience Edge-, Adobe Experience Cloud-Lösungen und Adobe Experience Platform-Lösungen bietet eine leicht verständliche und einfach zu bedienende Datenkollektionsgeschichte.

* **XDM:** Das lösungsunabhängige Schema, mit dem Daten an die Adobe gesendet werden. Kein Tagging für evars oder mboxes mehr.
* **Adobe Experience Platform Web SDK:** Erleichtert das Senden und Empfangen von Daten an Adobe Experience Platform Edge Network.
* **Experience Platform Launch:** Vereinfacht die Bereitstellung und Konfiguration des Web SDK (und aller anderen JavaScript-Tags) auf einer Site.
* **Erlebnis-Edge:** Versenden Sie die Daten einfach in das gewünschte Format an Adobe Experience Platform und Lösungen.
* **Adobe Experience Platform- und Adobe-Lösungen:** Aktivieren Sie deren Wertangebot.

**Steuerung:** Da alle Daten einen einzigen und verbundenen Datenstrom verwenden, können Sie logisch verfolgen und steuern, wie die Daten in jeder Millisekunde ihrer Journey aussehen, zu und von Anwendungen.

**Modern und zukunftsfähig:** Das Web SDK und seine Verbindung zum Experience Edge Network haben die Adobe in die Lage versetzt, die Art und Weise, wie Adobe mit der Datenerfassung, Personalisierung, Zustimmung und der Zukunft von Drittanbieter-Cookies umgeht, erheblich zu modernisieren. (Dadurch wird eine Erstanbieterdomäne aktiviert, die von der Adobe verwaltet wird.)

**Time-to-Value:** Adobe hat hart gearbeitet (und wird es auch weiterhin tun), um die Bereitstellung des Web SDK so einfach wie möglich über Experience Platform Launch zu machen und clientseitige Daten XDM zuzuordnen.  Nach Abschluss dieser Arbeit können alle anderen Adoben und Adobe Experience Platform-Dienste serverseitig aktiviert oder deaktiviert werden. Wenn Sie dies beispielsweise für Adobe Analytics verwenden und die Zielgruppe oder Experience Platform aktivieren möchten, können Sie einfach einen Schalter in der Datastream-Konfiguration aktivieren und diese Anwendungsfälle aufklären.

## Was ist Alloy?

Alloy ist der Codename für das Adobe Experience Platform Web SDK. Es wird im Quellcode und im Dateinamen des SDK verwendet, obwohl Adobe Experience Platform Web SDK der offizielle Name ist.

## Müssen Kunden Adobe Experience Platform kaufen, um das Web SDK zu verwenden?

Nein. Jeder Digital Experience-Kunde von Adobe kann es verwenden. Ganz kostenlos. Jeder Kunde, der das Web SDK verwenden möchte, erhält Zugriff auf die Erstellung von Schemas und Datensätzen in der Adobe Experience Platform-Benutzeroberfläche.

## Wer sollte das Web SDK verwenden?

Adobe Experience Platform Web SDK wurde für folgende Personen entwickelt:

* Adobe Experience Platform-Nutzer

   Wenn Sie Daten direkt von einem Gerät an Adobe Experience Platform senden müssen, wird dies offiziell empfohlen.

   Die Adobe ist sich bewusst, dass die Verwendung des Adobe Analytics Connectors schneller ist, wenn der Kunde bereits über Adobe Analytics verfügt, dies jedoch nicht die langfristige Strategie für die Datenerfassung ist.

* Adobe Experience Cloud-Lösungskunden

   Neue Adobe Analytics-, Adobe Audience Manager- und Adobe Target-Kunden sollten mit dem neuen Web SDK Beginn haben und keine alten Bibliotheken verwenden.

   Bestehende Kunden, die die bestmögliche Implementierung erhalten möchten, sollten das neue Web SDK verwenden.


## Wie erhalte ich Zugriff auf Beginn mit dem Adobe Experience Platform Web SDK?

Das Web SDK steht derzeit der Öffentlichkeit zur Verfügung und kann zum Senden von Daten an Adobe Experience Cloud-Produkte verwendet werden. Die Möglichkeit, Daten an Lösungen von Drittanbietern zu senden, wird demnächst verfügbar sein. Das SDK ist kostenlos, wird kostenlos von der Adobe gehostet und kann heruntergeladen werden, damit Sie es auf Ihren eigenen Servern hosten können, falls gewünscht, kostenlos. Platform Web SDK erfordert Zugriff auf Datastream-Konfigurationen und den Adobe Experience Platform XDM Schema Builder, damit die Server der Adobe eingehende Daten, die vom SDK stammen, ordnungsgemäß verarbeiten können. Wenn Sie Zugriff erhalten möchten, wenden Sie sich an Ihren Customer Success Manager (CSM), um den Anforderungsprozess Beginn.

## Welche Anwendungsfälle werden derzeit vom Web SDK unterstützt?

Das Web SDK entwickelt sich schnell. An weiteren Anwendungsfällen wird gearbeitet. Die aktuell unterstützte [Liste der Anwendungsfälle finden Sie hier.](https://github.com/adobe/alloy/projects/5)

## Müssen aktuelle Kunden ihre Sites neu taggen?

Das hängt von Ihrer aktuellen Situation ab. Adobe Experience Platform Web SDK kann in zwei verschiedenen Stilen bereitgestellt werden. Ein zukünftiges Dokument zur Migration wird weitere Details enthalten.

* **Nur ein weiteres Tag:** Wenn die Site bereits für Lösungen getaggt ist und Sie keine neuen Tags erstellen können, Sie aber Daten zur Experience Platform an Adobe Experience Platform Edge Network senden möchten, oder zu den bevorstehenden serverseitigen Funktionen des Experience Platform Launchs (siehe unten), können Sie das  `alloy.js` Tag der Site hinzufügen, wo es als &quot;nur ein weiteres Tag&quot;funktioniert.

* **Eins und einziges Tag:** Wenn Sie das Web SDK für eine Experience Cloud-Lösung verwenden möchten, müssen Sie es für  __ alle Lösungen auf dieser Seite verwenden. Wenn Ihre Site beispielsweise bereits für Adobe Analytics getaggt ist und Sie sie für die Zielgruppe verwenden möchten, müssen Sie sie sowohl für beide als auch für andere künftig verwenden.

Wenn Sie sich also entscheiden, Adobe Experience Platform Web SDK für Anwendungsfälle ohne Lösung zu verwenden, können Sie die Site mit `alloy.js` taggen und so fortfahren, als wäre es eine neue Lösung. Wenn Sie es für Adobe Analytics, Zielgruppe oder Audience Manager oder für Anwendungszwecke verwenden möchten, müssen Sie möglicherweise den Legacy-Code auf Ihrer Seite entfernen.

## Kann ich die ECIDs migrieren, wenn ich mit Alloy Beginn verwende, damit meine Website-Besucher nicht als neue Besucher angezeigt werden?

Ja, das Adobe Experience Platform Web SDK bietet eine Funktion zur Identitätsmigration. Befolgen Sie die Anweisungen zur ID-Migration in der [Platform Web SDK-Identitätsdokumentation](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration), um weitere Informationen zu erhalten.

## Wie unterscheidet sich das Web SDK von Adobe Experience Platform Launch?

* **Experience Platform** Launchis the device code manager. Verwenden Sie ihn, um den Code einfacher bereitzustellen. Es ist frei und mächtig.

* **Adobe Experience Platform Web** SDKist der offizielle Name des neuen Codes, der von Experience Platform Launch für Anwendungsfälle der Adobe bereitgestellt wird. Es ist auch frei und mächtig.

* **`alloy.js`** ist der Dateiname des Adobe Experience Platform Web SDK-Codes.

## Muss ich Adobe Experience Platform Launch verwenden, um das Web SDK bereitzustellen?

Nein. Sie können die Datei `alloy.js` selbst herunterladen.

Beachten Sie jedoch Folgendes:

* Adobe Experience Platform Web SDK erfordert eine so genannte Datastream-ID, damit das Edge-Netzwerk den Stream identifizieren und bestimmen kann, was mit den Daten zu tun ist. Diese ID wird in Experience Platform Launch erstellt. Dies bedeutet nicht, dass Sie Experience Platform Launch zum Erstellen von Eigenschaften oder Bereitstellen des JavaScript-Codes verwenden müssen, Sie müssen jedoch Experience Platform Launch verwenden, um eine Konfigurations-ID zu erstellen.

* Adobe Experience Platform Launch ist nicht nur der beste verfügbare Tag- und SDK-Manager, es macht es sehr einfach, `alloy.js` bereitzustellen und Daten XDM-Schemas zuzuordnen. Wenn Sie sich entscheiden, Experience Platform Launch nicht zu verwenden, müssen Sie die Bereitstellung von `alloy.js`, das Ereignis und die Zuordnung Ihrer Daten zu XDM verwalten, bevor Sie sie senden. Dies ist ein _viel_ schwierigerer Prozess als die Verwendung von Experience Platform Launch.

* Es wird empfohlen, `alloy.js` mit Experience Platform Launch bereitzustellen, auch wenn es das einzige Tag ist, für das Sie es verwenden.

## Was ist &quot;Adobe Experience Platform Launch Server Side?

Später im Jahr 2020 werden von Experience Platform Launch serverseitige Weiterleitungsfunktionen veröffentlicht. Wenn Sie unsere SDKs verwenden und XDM an Experience Edge senden, ermöglichen Ihnen diese neuen Funktionen die Installation neuer serverseitiger Erweiterungen und die Zuordnung dieser Daten zu allem - und beliebigen - Teil unseres Edge-Netzwerks. Stellen Sie sich die Datenerfassung als Dienst vor.  Dies wird kostenpflichtig sein und als Teil von Adobe Experience Platform gebündelt werden.

## Was ist eine CNAME- oder Erstanbieter-Domäne und warum ist sie wichtig?

Weitere Informationen zu einem CNAME finden Sie in der [Adobe-Dokumentation](https://docs.adobe.com/content/help/de-DE/id-service/using/reference/analytics-reference/cname.html)

## Verwendet das Adobe Experience Platform Web SDK Cookies? Wenn ja, welche Cookies verwendet sie?

Ja, das Web-SDK verwendet derzeit je nach Implementierung zwischen 1 und 4 Cookies. Im Folgenden finden Sie eine Liste der 4 Cookies, die Sie mit dem Web SDK und der Art und Weise ihrer Verwendung sehen können:

**kndct_orgid_identity:** Das Identitäts-Cookie wird zur Speicherung der ECID sowie einiger anderer Informationen im Zusammenhang mit der ECID verwendet.

**kndctr_orgid_approval:** Dieses Cookie speichert die Voreinstellung des Benutzers für die Zustimmung zur Website.

**kndctr_orgid_personalization:** Dieses Cookie enthält Sitzungsinformationen, die Adobe Target zum Personalisieren von Webseiten verwendet.

**kndctr_orgid_approvalCheck:** Dieses sitzungsbasierte Cookie signalisiert dem Server, die Voreinstellungen für die Zustimmung auf der Serverseite zu suchen.

## Welche Browser unterstützt das Adobe Experience Platform Web SDK?

Das Adobe Experience Platform Web SDK ist so konzipiert, dass es in den neuesten Versionen von Google Chrome, Safari, Firefox, Internet Explorer 11 und Microsoft Edge Chromium optimal funktioniert. Bei der Verwendung bestimmter Funktionen in älteren Versionen von Browsern kann es zu Problemen kommen.

## Wo erhalte ich weitere Informationen zum Adobe Experience Platform Web SDK?

* [Dokumentation](https://docs.adobe.com/content/help/de-DE/experience-platform/edge/home.html)
* [Quellcode](https://github.com/adobe/alloy)
