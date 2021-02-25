---
keywords: Experience Platform;Profil;Echtzeit-Profil von Kunden;Fehlerbehebung;API
title: Einführung in berechnete Attribute
topic: guide
type: Dokumentation
description: Berechnete Attribute sind Funktionen zum Aggregat von Daten auf Ereignis-Ebene in Attribute auf Profil-Ebene. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können.
translation-type: tm+mt
source-git-commit: 4ed2b80ebfd87f8920462ae0a918b01bb13d4210
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 41%

---


# (Alpha) Überblick über berechnete Attribute

>[!IMPORTANT]
>
>Die Funktion für berechnete Attribute ist derzeit alphanumerisch und steht nicht allen Benutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.

Berechnete Attribute sind Funktionen, mit denen Daten auf Ereignis-Ebene in Attribute auf Profil-Ebene Aggregat werden. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können.

Jedes berechnete Attribut enthält einen Ausdruck, oder &quot;Regel&quot;, der eingehende Daten auswertet und den sich ergebenden Wert in einem Profil-Attribut speichert. Mit diesen Berechnungen können Sie Fragen im Zusammenhang mit dem Kaufwert über die gesamte Lebensdauer, der Zeit zwischen Käufen oder der Anzahl der Anwendungsöffnungen leicht beantworten, ohne für jede benötigte Information manuell komplexe Berechnungen ausführen zu müssen. Diese berechneten Attributwerte können dann in einem Profil angezeigt, zum Erstellen eines Segments verwendet oder über verschiedene Zugriffsmuster aufgerufen werden.

Dieser Leitfaden hilft Ihnen, die Rolle von berechneten Attributen in Adobe Experience Platform besser zu verstehen.

## Berechnete Attribute

Mit Adobe Experience Platform können Sie einfach Daten aus mehreren Quellen importieren und zusammenführen, um [!DNL Real-time Customer Profiles] zu generieren. Jedes Profil enthält wichtige Daten zu einer Person, wie z. B. ihre Kontaktdaten, Präferenzen und den Kaufverlauf, sodass eine 360-Grad-Ansicht des Kunden entsteht.

Manche der im Profil erfassten Daten sind beim direkten Lesen der Datenfelder leicht verständlich (z. B. „Vorname“), während bei anderen Daten mehrere Berechnungen oder andere Felder und Werte erforderlich sind, um die Daten zu generieren (z. B. „Lebenszeitkaufsumme“). Damit diese Daten auf einen Blick leichter zu verstehen sind, können Sie mit [!DNL Platform] berechnete Attribute erstellen, die automatisch diese Verweise und Berechnungen durchführen und den Wert im entsprechenden Feld zurückgeben.

Berechnete Attribute umfassen das Erstellen eines Ausdrucks oder einer &quot;Regel&quot;, der für eingehende Daten arbeitet und den sich ergebenden Wert in einem Profil-Attribut speichert. Ausdrücke können auf unterschiedliche Weise definiert werden. So können Sie festlegen, dass eine Regel nur eingehende Ereignisse, ein eingehendes Ereignis und Profildaten oder ein eingehendes Ereignis, Profildaten und historische Ereignisse auswertet.

### Anwendungsbeispiele

Anwendungsbeispiele für berechnete Attribute können von einfachen Berechnungen hin zu sehr komplexen Verweisen reichen. Im Folgenden finden Sie einige Anwendungsbeispiele für berechnete Attribute:

1. **[!UICONTROL Prozentwerte]:** Ein einfaches, berechnetes Attribut kann die Entnahme zweier numerischer Felder in einem Datensatz und deren Aufteilung zur Erstellung eines Prozentsatzes sein. Sie könnten beispielsweise die Gesamtzahl der an eine Person gesendeten E-Mails durch die Zahl der von der Person geöffneten E-Mails teilen. Wenn Sie das sich ergebende Feld für berechnete Attribute ansehen, erkennen Sie schnell den Prozentsatz der Gesamt-E-Mails, die von der Person geöffnet wurden.
1. **[!UICONTROL Anwendungsnutzung]:** Ein weiteres Beispiel ist die Möglichkeit, die Anzahl der Anwendungsstarts durch einen Benutzer Aggregat. Wenn Sie die Gesamtzahl der Anwendungsöffnungen anhand einzelner Öffnungsereignisse verfolgen, können Sie Anwendern bei der 100. Öffnung besondere Angebote oder Nachrichten zukommen lassen, um die Interaktion mit Ihrer Marke zu stärken.
1. **[!UICONTROL Lebenszeitwerte]: Das** Sammeln von Gesamtwerten, wie z. B. einem Kaufwert für einen Kunden, kann sehr schwierig sein. Dafür muss die historische Gesamtsumme bei jedem Auftreten eines neuen Kaufereignisses aktualisiert werden. Mit einem berechneten Attribut können Sie dies wesentlich einfacher tun, indem Sie den Lebenszeitwert in einem einzelnen Feld pflegen, das nach jedem erfolgreichen Kaufereignis, das mit dem Kunden verbunden ist, automatisch aktualisiert wird.

## Bekannte Einschränkungen

### Verzögerte Verfügbarkeit neuer berechneter Attribute

Die Verfügbarkeit neuer berechneter Attribute kann bis zu 2 Stunden nach dem Hinzufügen des entsprechenden Schema-Attributs zum Schema Vereinigung verzögert werden.

Diese Verzögerung ist auf die aktuelle Cache-Konfiguration zurückzuführen. Nach der Alpha-Methode kann die Cache-Aktualisierungshäufigkeit erhöht werden.

### Abhängigkeitsverfolgung in Segmenten

Schema-Attribute, die bereits in einem Segmentdefinitionssegment verwendet, später jedoch in ein berechnetes Attribut umgewandelt wurden, werden nicht als Abhängigkeit dieses Ausdrucks verfolgt.

Da keine Abhängigkeit erkannt wurde, wird das zugehörige berechnete Attribut von der Experience Platform nicht automatisch bei jeder Bewertung der Segmentdefinition ausgewertet.

Alternativ kann die Erstellung berechneter Attribute über eine bestimmte Mischung verwaltet werden, die neue berechnete Attribute hinzufügt, die nicht mit vorhandenen Attributen in Konflikt stehen. Eine andere Möglichkeit besteht darin, das Segment einfach mit der richtigen Abhängigkeitsverfolgung für die neuen berechneten Attribute neu zu erstellen.