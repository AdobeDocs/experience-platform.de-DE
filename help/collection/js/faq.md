---
title: Häufig gestellte Fragen zu Adobe Experience Platform Web SDK
description: Erhalten Sie Antworten auf häufig gestellte Fragen zur Adobe Experience Platform Web SDK.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 66105ca19ff1c75f1185b08b70634b7d4a6fd639
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 1%

---

# Häufig gestellte Fragen

Dieses Handbuch enthält Antworten auf Fragen, die häufig zum Adobe Experience Platform Web SDK gestellt werden.

## Wie unterscheidet sich Adobe Experience Platform Web SDK von früheren Lösungen?

### Vor Experience Platform Web SDK

Derzeit müssen Sie basierend auf jeder einzelnen Lösung verschiedene JavaScript-Bibliotheken bereitstellen.

* Jede Lösung verfügt über eine eigene JavaScript-Bibliothek, ein eigenes Schema und eine eigene Domain.
* Keine dieser Bibliotheken wurde für die Zusammenarbeit errichtet.
* In lösungsübergreifenden und Adobe Experience Platform-Anwendungsfällen müssen diese unterschiedlichen Bibliotheken voneinander abhängig sein, was zu Reibungen bei der Bereitstellung führt.

Obwohl Tags in Experience Platform die Bereitstellung und Verwaltung dieser Bibliotheken so einfach wie möglich machen, bestehen weiterhin Probleme mit:

* Bibliotheksgröße (zu viel Adobe-Code auf einer Seite)
* Leistung (Websites benötigen zu lange, um geladen zu werden)
* Mehrere Aufrufe für einen einzigen Anwendungsfall
* Warten auf die ECID-Rückgabe vor Personalisierungsaufrufen (verursacht Verzögerung)
* Gebrochene Datenerfassung (was ist eine eVar?)
* Schemaverwechslung zwischen Lösungen (A4T)
* Viele andere, weniger optimale Dinge

Außerdem gibt es derzeit keine JavaScript-Bibliothek, die Daten direkt an Adobe Experience Platform sendet.

### Mit Experience Platform Web SDK

Das neue Web-SDK sendet Daten für die folgenden Lösungen an ein einzelnes Ziel (Experience Platform Edge Network) und löst die oben genannten häufigsten Lösungsanwendungsfälle.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* Besucher-ID
* Adobe Experience Platform

Weitere Lösungen werden folgen.

Adobe Experience Platform Web SDK kann auch Daten direkt an Adobe Experience Platform senden. Diese Daten liegen im XDM-Format vor und werden dem Server-seitigen Lösungsschema zugeordnet.

## Was ist der Wert dieser neuen Web-SDK?

**Leistung:** Die Web-SDK ist kleiner als alle aktuellen Adobe-Bibliotheken und bietet deutlich schnellere Seitenladevorgänge.

**Einfachheit:** Die Kombination aus XDM, Web SDK, Tags, Edge Network, Adobe Experience Cloud-Lösungen und Adobe Experience Platform schafft eine leicht verständliche und leicht nachvollziehbare Datenerfassungsgeschichte.

* **XDM:** Das lösungsunabhängige Schema, das Sie zum Senden von Daten an Adobe verwenden. Keine weiteren Tags für eVars oder Mboxes.
* **Web SDK:** Erleichtert das Senden und Empfangen von Daten an Adobe Experience Platform Edge Network.
* **Tags:** Vereinfacht die Bereitstellung und Konfiguration der Web-SDK (und aller anderen JavaScript-Tags) auf einer Site.
* **Edge Network:** Leiten Sie die Daten einfach in dem benötigten Format an Adobe Experience Platform und die Lösungen weiter.
* **Adobe Experience Platform- und Adobe-Lösungen:** Ihr Wertversprechen aktivieren.

**Kontrolle** Da alle Daten einen einzigen und verbundenen Datenstrom verwenden, können Sie logisch verfolgen und steuern, wie die Daten bei jeder Millisekunde ihres Journey, zu und von Anwendungen aussehen.

**Modern und zukunftsbereit:** Die Web-SDK und ihre Verbindung zur Edge Network haben Adobe in die Lage versetzt, den Umgang von Adobe mit der Datenerfassung, Personalisierung, Einverständniserklärung und der Zukunft von Drittanbieter-Cookies erheblich zu modernisieren. (Erstanbieter-Domain wird von Adobe verwaltet.)

**Time-to-Value:** Adobe hat hart daran gearbeitet (und wird es auch weiterhin tun), die Bereitstellung des Web-SDK über Tags und die Zuordnung Client-seitiger Daten zu XDM so einfach wie möglich zu gestalten. Danach können alle anderen Adobe-Lösungen und Adobe Experience Platform-Services Server-seitig aktiviert oder deaktiviert werden. Wenn Sie dies beispielsweise für Adobe Analytics verwenden und Target oder Experience Platform aktivieren möchten, können Sie einfach einen Umschalter in der Datenstromkonfiguration umschalten und diese Anwendungsfälle aufleuchten lassen.

## Was ist `alloy.js`?

`alloy.js` ist der Name der Web SDK JavaScript-Bibliothek. Es wird innerhalb des Quell-Codes und Dateinamens von SDK referenziert.

## Müssen Kunden Adobe Experience Platform kaufen, um die [!DNL Web SDK] nutzen zu können?

Nein. Jeder Kunde von Adobe Digital Experience kann die Adobe Experience Platform Web SDK kostenlos nutzen.

* Kunden, die *nicht* Zugriff auf Experience Platform oder Real-Time CDP haben und die [!DNL Web SDK] verwenden möchten, müssen die richtigen Berechtigungen konfigurieren, um Schemas und Datenströme in der Datenerfassungs-Benutzeroberfläche oder der Experience Platform-Benutzeroberfläche zu erstellen.
* Kunden, die Zugriff auf Experience Platform oder Real-Time CDP haben und die [!DNL Web SDK] verwenden möchten, müssen die richtigen Berechtigungen konfigurieren, um Schemas, Datensätze, Identitäts-Namespaces und Datenströme in der Datenerfassungs-Benutzeroberfläche oder der Experience Platform-Benutzeroberfläche zu erstellen.

Weitere Informationen zum Konfigurieren dieser Berechtigungen finden Sie in der Dokumentation unter [Verwaltung von Datenerfassungsberechtigungen](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=de).

## Wer sollte die Web-SDK verwenden?

Adobe Experience Platform Web SDK wurde für die folgenden Kunden entwickelt:

* Adobe Experience Platform-Benutzer
   * Wenn Sie Daten direkt von einem Gerät an Adobe Experience Platform senden müssen, ist dies die offiziell empfohlene Methode.
   * Adobe ist sich bewusst, dass die Verwendung des Adobe Analytics-Connectors schneller ist, wenn Sie bereits über Adobe Analytics verfügen. Dies ist jedoch keine langfristige Strategie für die Datenerfassung.

* Adobe Experience Cloud-Lösungskunden
   * Neue Kunden von Adobe Analytics, Adobe Audience Manager und Adobe Target sollten mit der neuen Web-SDK beginnen und keine Legacy-Bibliotheken verwenden.
   * Bestehende Kunden, die die bestmögliche Implementierung erhalten möchten, sollten den neuen Web SDK verwenden.

## Wie erhalte ich Zugriff auf Web SDK?

Web SDK ist derzeit öffentlich verfügbar und kann zum Senden von Daten an Adobe Experience Cloud-Produkte verwendet werden. Die Möglichkeit, Daten an Lösungen von Drittanbietern zu senden, wird in naher Zukunft verfügbar sein.

Die SDK ist kostenlos und wird von Adobe kostenlos gehostet. Bei Bedarf können Sie es kostenlos herunterladen und auf Ihren eigenen Servern hosten.

Web SDK erfordert Zugriff auf [Datenstromkonfigurationen](/help/datastreams/overview.md) und den Experience Platform [XDM Schema Builder](/help/xdm/tutorials/create-schema-ui.md), damit die Adobe-Server eingehende Daten aus SDK ordnungsgemäß verarbeiten können. Wenn Sie Zugriff erhalten möchten, wenden Sie sich an Ihr Adobe-Accountteam, um den Anfrageprozess zu starten.

## Welche Anwendungsfälle werden derzeit vom Web SDK unterstützt?

Web SDK entwickelt sich schnell weiter. Weitere Anwendungsfälle werden derzeit bearbeitet. Die [Liste der derzeit unterstützten Anwendungsfälle finden Sie hier.](https://github.com/orgs/adobe/projects/18/views/1?filterQuery=)

## Müssen aktuelle Kunden ihre Sites neu taggen?

Es kommt darauf an. Adobe Experience Platform Web SDK kann in zwei verschiedenen Stilen bereitgestellt werden. Weitere Einzelheiten werden in einem künftigen Migrationsdokument aufgeführt.

* **Nur ein weiteres Tag:** Wenn die Website bereits für Lösungen getaggt ist und Sie sie nicht erneut taggen können, aber Daten für Experience Platform-Anwendungsfälle oder die bevorstehenden Funktionen zur Ereignisweiterleitung (siehe unten) an Adobe Experience Platform Edge Network senden möchten, können Sie das `alloy.js` Tag zur Website hinzufügen, wo es als „nur ein weiteres Tag“ funktioniert.

* **Einziges Tag:** Wenn Sie die Web-SDK für eine Experience Cloud-Lösung verwenden möchten, müssen Sie sie für _alle_ Lösungen auf dieser Seite verwenden. Wenn Ihre Site beispielsweise bereits für Adobe Analytics getaggt ist und Sie sie für Target verwenden möchten, müssen Sie sie sowohl für beide als auch für alle anderen in der Zukunft verwenden.

Anders ausgedrückt: Wenn Sie sich entscheiden, Adobe Experience Platform Web SDK für Anwendungsfälle zu verwenden, bei denen es sich nicht um eine Lösung handelt, können Sie die Site mit `alloy.js` taggen und so weitermachen, als wäre es eine neue Lösung. Wenn Sie ihn für Adobe Analytics, Target oder Audience Manager oder für Anwendungsfälle verwenden möchten, müssen Sie möglicherweise einen der Legacy-Codes auf Ihrer Seite entfernen.

## Kann ich die ECIDs migrieren, wenn ich mit der Verwendung von Web SDK beginne, damit meine Website-Besucher nicht als neue Besucher angezeigt werden?

Ja, Adobe Experience Platform Web SDK bietet eine Funktion zur Identitätsmigration. Weitere Informationen finden Sie in der Dokumentation zu Experience Platform Web SDK Identity [&#x200B; der Anleitung zur ID-Migration.](/help/collection/use-cases/identity/id-overview.md#migrating-visitor-api-ecid)

## Worin unterscheidet sich Web SDK von Tags?

* **Tags in Experience Platform** verwalten den Geräte-Code. Verwenden Sie sie, um den Code einfacher bereitzustellen. Sie sind frei und mächtig.

* **Adobe Experience Platform Web SDK** ist der offizielle Name des neuen Codes, der von Tags für Adobe-Anwendungsfälle bereitgestellt wird. Es ist auch frei und mächtig.

* **`alloy.js`** ist der Dateiname des Adobe Experience Platform Web SDK-Codes.

## Muss ich Tags verwenden, um die Web-SDK bereitzustellen?

Nein. Sie können die `alloy.js` selbst herunterladen.

Allerdings:

* Adobe Experience Platform Web SDK erfordert eine so genannte Datenstrom-ID, damit das Edge-Netzwerk den Datenstrom identifizieren und bestimmen kann, was mit den Daten geschehen soll. Diese ID wird in Experience Platform erstellt. Dies bedeutet nicht, dass Sie die Benutzeroberfläche verwenden müssen, um Eigenschaften zu erstellen oder den JavaScript-Code bereitzustellen. Sie müssen jedoch Tags verwenden, um eine Konfigurations-ID zu erstellen.

* Tags sind nicht nur das beste verfügbare Tag und SDK Manager, sondern auch eine sehr einfache Bereitstellung von `alloy.js` und Zuordnung von Daten zu XDM-Schemata. Wenn Sie sich entscheiden, keine Tags zu verwenden, müssen Sie die Bereitstellung von `alloy.js`, Ereignissen und die Zuordnung Ihrer Daten zu XDM verwalten, bevor Sie sie senden. Dies ist ein _viel_ schwierigerer Prozess als die Verwendung von Tags.

* Es wird empfohlen, Tags zur Bereitstellung von `alloy.js` zu verwenden, auch wenn es das einzige Tag ist, für das Sie es verwenden.

## Was ist Ereignisweiterleitung?

Wenn Sie unsere SDKs verwenden und XDM an die Edge Network senden, können Sie mit diesen neuen Funktionen für die Ereignisweiterleitung neue Server-seitige Erweiterungen installieren und diese Daten allen Elementen über unser Edge-Netzwerk zuordnen und an beliebige Stellen senden. Betrachten Sie dies als „Datenerfassung als Service“. Diese ist gegen Aufpreis verfügbar und wird als Teil von Adobe Experience Platform gebündelt.

## Was ist eine CNAME- oder Erstanbieter-Domain und warum ist sie wichtig?

Weitere Informationen finden Sie im Handbuch zu [&#x200B; Services im &#x200B;](https://experienceleague.adobe.com/de/docs/core-services/interface/data-collection/adobe-managed-cert)Adobe-Managed Certificate Program.

## Verwendet Adobe Experience Platform Web SDK Cookies? Wenn ja, welche Cookies werden verwendet?

Siehe [Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/de/docs/core-services/interface/data-collection/cookies/web-sdk)Cookies im Core Services-Handbuch.

## Welche Browser unterstützt Adobe Experience Platform Web SDK?

Adobe Experience Platform Web SDK wurde für eine optimale Funktionsweise in den neuesten Versionen von Google Chrome, Safari, Firefox und Microsoft Edge Chromium entwickelt. Bei der Verwendung bestimmter Funktionen in älteren Versionen von Browsern oder veralteten Browsern wie Internet Explorer können Probleme auftreten.

## Wo erhalte ich den Quell-Code für die Web-SDK?

Siehe das [Alloy](https://github.com/adobe/alloy)-Repository auf GitHub.
