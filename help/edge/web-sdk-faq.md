---
title: Häufig gestellte Fragen zum Web SDK
seo-title: Häufig gestellte Fragen zum Adobe Experience Platform Web SDK
description: Häufig gestellte Fragen zum Adobe Experience Platform Web SDK
seo-description: Häufig gestellte Fragen zum Adobe Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 2e28fda40a135330054c749d73439448a55db52c
workflow-type: tm+mt
source-wordcount: '1631'
ht-degree: 4%

---


# Häufig gestellte Fragen 

Diese häufig gestellten Fragen enthalten Fragen zur Adobe Web SDK.

## Was ist das Adobe Experience Platform Web SDK?

Das Adobe Experience Platform Web SDK ist eine Client-seitige JavaScript-Bibliothek, mit der Kunden von Adobe Experience Cloud mit den verschiedenen Diensten in Experience Cloud interagieren können.

Es sendet Daten auf lösungsunabhängige Weise (XDM) an das Adobe Experience Platform Edge Network, das die Daten dann lösungsspezifischen Formaten und Zielen zuordnet und sie dann in Echtzeit sendet.

**Weitere Informationen** zur[Adobe](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

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

Das neue Web SDK sendet Daten für die folgenden Lösungen an ein einzelnes Ziel (AEP Edge Network) und löst die gängigsten oben genannten Anwendungsfälle für Lösungen.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Visitor ID
* Adobe Experience Platform

Weitere Lösungen werden im Laufe dieses Jahres folgen.

Adobe Experience Platform Web SDK kann auch Daten direkt an Adobe Experience Platform senden. Diese Daten befinden sich im XDM-Format und werden dem serverseitigen Lösungs-Schema zugeordnet.

## Welchen Wert hat dieses neue Web SDK?

**Leistung:** Das Web-SDK ist kleiner als alle aktuellen Adoben-Bibliotheken und bietet deutlich schnellere Seitenladevorgänge.

**Einfachheit:** Die Kombination aus XDM-, Web-SDK-, Experience Platform Launch-, Experience Edge-, Adobe Experience Cloud- und Adobe Experience Platform-Lösungen bietet eine leicht verständliche und einfach zu bedienende Datenerfassungsgeschichte.

* **XDM:** Das lösungsunabhängige Schema zum Senden von Daten an die Adobe. Kein Tagging für evars oder mboxes mehr.
* **Web SDK:** Erleichtert das Senden und Empfangen von Daten an das Adobe Experience Platform Edge Network.
* **Experience Platform Launch:** Vereinfacht die Bereitstellung und Konfiguration des Web SDK (und aller anderen JavaScript-Tags) auf einer Site.
* **Erlebnisrand:** Versenden Sie die Daten einfach an Adobe Experience Platform und Lösungen in dem Format, das sie benötigen.
* **Lösungen für Adobe Experience Platform und Adobe:** Aktivieren Sie ihr Wertangebot.

**Kontrolle:** Da alle Daten einen einzigen und verbundenen Datenstrom verwenden, können Sie logischerweise verfolgen und steuern, wie die Daten auf jeder Millisekunde der Reise zu und von Anwendungen aussehen.

**Modermodern und zukunftsbereit:** Das Web SDK und seine Verbindung zum Experience Edge Network haben die Adobe in die Lage versetzt, die Art und Weise, wie Adobe mit der Datenerfassung, Personalisierung, Zustimmung und der Zukunft von Drittanbieter-Cookies umgeht, erheblich zu modernisieren. (Dadurch wird eine Erstanbieterdomäne aktiviert, die von der Adobe verwaltet wird.)

**Time-to-Value:** Adobe hat hart gearbeitet (und wird dies auch weiterhin tun), um die Bereitstellung des Web SDK über Experience Platform Launch so einfach wie möglich zu machen und clientseitige Daten XDM zuzuordnen.  Nach Abschluss dieser Arbeit können alle anderen Adoben und Adobe Experience Platform-Dienste serverseitig aktiviert oder deaktiviert werden. Wenn Sie dies beispielsweise für Adobe Analytics verwenden und die Zielgruppe oder Experience Platform aktivieren möchten, können Sie einfach einen Umschalter in der Experience Edge-Konfiguration aktivieren und diese Anwendungsfälle aufklären.

## Was ist `alloy.js`?

`Alloy.js` ist der Dateiname für das Adobe Experience Platform Web SDK. Adobe Experience Platform Web SDK ist der offizielle Name, aber viele Entwickler bezeichnen es als &quot;Legierung&quot;.

## Müssen Kunden Adobe Experience Platform kaufen, um das Web SDK zu verwenden?

Nein. Jeder Digital Experience-Kunde von Adobe kann es verwenden. Ganz kostenlos. Jeder Kunde, der das Web SDK verwenden möchte, erhält Zugriff auf die Erstellung von Schemas und Datensätzen in der Adobe Experience Platform-Benutzeroberfläche.

## Wer sollte das Web SDK verwenden?

Das Adobe Experience Platform Web SDK wurde für folgende Personen entwickelt:

* Adobe Experience Platform-Nutzer

   Wenn Sie Daten direkt von einem Gerät an Adobe Experience Platform senden müssen, wird dies offiziell empfohlen.

   Die Adobe ist sich bewusst, dass die Verwendung des Adobe Analytics Connectors schneller ist, wenn der Kunde bereits über Adobe Analytics verfügt, dies jedoch nicht die langfristige Strategie für die Datenerfassung ist.

* Adobe Experience Cloud-Lösungskunden

   Neue Adobe Analytics-, Adobe Audience Manager- und Adobe Target-Kunden sollten mit dem neuen Web SDK Beginn haben und keine alten Bibliotheken verwenden.

   Bestehende Kunden, die die bestmögliche Implementierung erhalten möchten, sollten das neue Web SDK verwenden.


## Wie erhalte ich Zugriff auf Beginn mit dem Adobe Experience Platform Web SDK?

Das Web SDK steht derzeit der Öffentlichkeit zur Verfügung und kann zum Senden von Daten an Adobe Experience Cloud-Produkte verwendet werden. Die Möglichkeit, Daten an Lösungen von Drittanbietern zu senden, wird demnächst verfügbar sein. Wenn Sie Zugriff auf das Web SDK erhalten möchten, wenden Sie sich an Ihren zertifizierten Software-Manager (CSM), um den Anforderungsprozess Beginn.

## Welche Anwendungsfälle werden derzeit vom Web SDK unterstützt?

Das Web SDK entwickelt sich schnell. An weiteren Anwendungsfällen wird gearbeitet. Die aktuell unterstützte [Liste der Anwendungsfälle finden Sie hier.](https://github.com/adobe/alloy/projects/5)

## Müssen aktuelle Kunden ihre Sites neu taggen?

Das hängt von Ihrer aktuellen Situation ab. Das Adobe Experience Platform Web SDK kann in zwei verschiedenen Stilen bereitgestellt werden. Ein zukünftiges Dokument zur Migration wird weitere Details enthalten.

* **Nur ein weiteres Tag:** Wenn die Site bereits für Lösungen getaggt ist und Sie keine neuen Tags erstellen können, Sie aber Daten zur Experience Platform an das Adobe Experience Platform Edge Network senden möchten (siehe unten), können Sie das `alloy.js` Tag der Site hinzufügen, wo es als &quot;nur ein weiteres Tag&quot;funktioniert.

* **Das erste und einzige Tag:** Wenn Sie das Web SDK für eine Experience Cloud-Lösung verwenden möchten, müssen Sie es für _alle_ Lösungen auf dieser Seite verwenden. Wenn Ihre Site beispielsweise bereits für Adobe Analytics getaggt ist und Sie sie für die Zielgruppe verwenden möchten, müssen Sie sie sowohl für beide als auch für andere künftig verwenden.

Mit anderen Worten, wenn Sie sich entscheiden, das Adobe Experience Platform Web SDK für Anwendungsfälle ohne Lösung zu verwenden, können Sie die Site mit Tags versehen `alloy.js` und weitermachen, als wäre es eine neue Lösung. Wenn Sie es für Adobe Analytics, Zielgruppe oder Audience Manager oder für Anwendungszwecke verwenden möchten, müssen Sie möglicherweise den Legacy-Code auf Ihrer Seite entfernen.

## Kann ich die ECIDs migrieren, wenn ich mit Alloy Beginn verwende, damit meine Website-Besucher nicht als neue Besucher angezeigt werden?

Ja, das Adobe Experience Platform Web SDK bietet eine Funktion zur Identitätsmigration. Weitere Informationen finden Sie in den Anweisungen in [diesem Dokument](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/identity.html#id-migration) .

## Wie unterscheidet sich das Web SDK von Adobe Experience Platform Launch?

* **Experience Platform Launch** ist der Code-Manager des Geräts. Verwenden Sie ihn, um den Code einfacher bereitzustellen. Es ist frei und mächtig.

* **Adobe Experience Platform Web SDK** ist der offizielle Name des neuen Codes, der von Experience Platform Launch für Anwendungsfälle der Adobe bereitgestellt wird. Es ist auch frei und mächtig.

* **`alloy.js`** ist der Dateiname des Adobe Experience Platform Web SDK-Codes.

## Muss ich Adobe Experience Platform Launch verwenden, um das Web SDK bereitzustellen?

Nein. Sie können die `alloy.js` Datei selbst herunterladen.

Allerdings:

* Das Adobe Experience Platform Web SDK erfordert eine so genannte Experience Edge-Konfigurations-ID, damit das Edge-Netzwerk den Stream identifizieren und bestimmen kann, was mit den Daten zu tun ist. Diese ID wird in Experience Platform Launch erstellt. Dies bedeutet nicht, dass Sie Experience Platform Launch zum Erstellen von Eigenschaften oder Bereitstellen des JavaScript-Codes verwenden müssen, Sie müssen jedoch Experience Platform Launch verwenden, um eine Konfigurations-ID zu erstellen.

* Adobe Experience Platform Launch ist nicht nur der beste verfügbare Tag- und SDK-Manager, es macht es sehr einfach, Daten bereitzustellen `alloy.js` und XDM-Schemas zuzuordnen. Wenn Sie sich entschließen, Experience Platform Launch nicht zu verwenden, müssen Sie die Bereitstellung `alloy.js`, das Ereignis und die Zuordnung Ihrer Daten zu XDM verwalten, bevor Sie sie senden. Dies ist ein _viel_ schwierigerer Prozess als der Einsatz von Experience Platform Launch.

* Es wird empfohlen, Experience Platform Launch für die Bereitstellung zu verwenden, auch `alloy.js`wenn es das einzige Tag ist, für das Sie es verwenden.

## Was ist &quot;Adobe Experience Platform Launch Server Side?

Später im Jahr 2020 werden von Experience Platform Launch serverseitige Weiterleitungsfunktionen veröffentlicht. Wenn Sie unsere SDKs verwenden und XDM an Experience Edge senden, ermöglichen Ihnen diese neuen Funktionen die Installation neuer serverseitiger Erweiterungen und die Zuordnung dieser Daten zu allem - und beliebigen - Teil unseres Edge-Netzwerks. Stellen Sie sich die Datenerfassung als Dienst vor.  Dies wird kostenpflichtig sein und als Teil der Adobe Experience Platform gebündelt werden.

## Was ist eine CNAME- oder Erstanbieter-Domäne und warum ist sie wichtig?

Weitere Informationen zu einem CNAME finden Sie in der Dokumentation zur [Adobe](https://docs.adobe.com/content/help/de-DE/id-service/using/reference/analytics-reference/cname.html)

## Wo erhalte ich weitere Informationen zum Adobe Experience Platform Web SDK?

* [Dokumentation](https://docs.adobe.com/content/help/de-DE/experience-platform/edge/home.html)
* [Quellcode](https://github.com/adobe/alloy)
