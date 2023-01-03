---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Fehlerbehebung; API
title: Einführung in berechnete Attribute
topic-legacy: guide
type: Documentation
description: Berechnete Attribute sind Funktionen zum Aggregieren von Daten auf Ereignisebene in Profilattributen. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können.
exl-id: 13878363-589d-4a3c-811c-21d014a5f3c2
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 47%

---

# (Alpha) Übersicht über berechnete Attribute

>[!IMPORTANT]
>
>Die Funktion für berechnete Attribute ist derzeit alphanumerisch und steht nicht allen Benutzern zur Verfügung. Dokumentation und Funktionalitäten können sich ändern.

Berechnete Attribute sind Funktionen, mit denen Daten auf Ereignisebene in Attribute auf Profilebene aggregiert werden. Diese Funktionen werden automatisch berechnet, sodass sie für die Segmentierung, Aktivierung und Personalisierung verwendet werden können.

Jedes berechnete Attribut enthält einen Ausdruck oder eine &quot;Regel&quot;, der/die eingehende Daten auswertet und den resultierenden Wert in einem Profilattribut speichert. Mit diesen Berechnungen können Sie Fragen im Zusammenhang mit dem Kaufwert über die gesamte Lebensdauer, der Zeit zwischen Käufen oder der Anzahl der Anwendungsöffnungen leicht beantworten, ohne für jede benötigte Information manuell komplexe Berechnungen ausführen zu müssen. Diese berechneten Attributwerte können dann in einem Profil angezeigt, zum Erstellen eines Segments verwendet oder über verschiedene Zugriffsmuster aufgerufen werden.

Dieses Handbuch hilft Ihnen, die Rolle berechneter Attribute in Adobe Experience Platform besser zu verstehen.

## Berechnete Attribute

Mit Adobe Experience Platform können Sie Daten aus mehreren Quellen einfach importieren und zusammenführen, um sie zu generieren [!DNL Real-Time Customer Profiles]. Jedes Profil enthält wichtige Daten zu einer Person, wie z. B. ihre Kontaktdaten, Präferenzen und den Kaufverlauf, sodass eine 360-Grad-Ansicht des Kunden entsteht.

Manche der im Profil erfassten Daten sind beim direkten Lesen der Datenfelder leicht verständlich (z. B. „Vorname“), während bei anderen Daten mehrere Berechnungen oder andere Felder und Werte erforderlich sind, um die Daten zu generieren (z. B. „Lebenszeitkaufsumme“). Damit diese Daten auf einen Blick leichter zu verstehen sind, [!DNL Platform] ermöglicht die Erstellung berechneter Attribute, die diese Verweise und Berechnungen automatisch ausführen und den Wert im entsprechenden Feld zurückgeben.

Berechnete Attribute umfassen das Erstellen eines Ausdrucks oder einer &quot;Regel&quot;, der für eingehende Daten verwendet wird und den resultierenden Wert in einem Profilattribut speichert. Ausdrücke können auf unterschiedliche Weise definiert werden. So können Sie festlegen, dass eine Regel nur eingehende Ereignisse, ein eingehendes Ereignis und Profildaten oder ein eingehendes Ereignis, Profildaten und historische Ereignisse auswertet.

### Anwendungsbeispiele

Anwendungsbeispiele für berechnete Attribute können von einfachen Berechnungen hin zu sehr komplexen Verweisen reichen. Im Folgenden finden Sie einige Anwendungsbeispiele für berechnete Attribute:

1. **[!UICONTROL Prozentsatz]:** Ein einfaches berechnetes Attribut könnte zwei numerische Felder in einen Datensatz aufnehmen und teilen, um einen Prozentsatz zu erstellen. Sie könnten beispielsweise die Gesamtzahl der an eine Person gesendeten E-Mails durch die Zahl der von der Person geöffneten E-Mails teilen. Wenn Sie das sich ergebende Feld für berechnete Attribute ansehen, erkennen Sie schnell den Prozentsatz der Gesamt-E-Mails, die von der Person geöffnet wurden.
1. **[!UICONTROL Anwendungsanwendung]:** Ein weiteres Beispiel ist die Möglichkeit, die Anzahl der Male zu addieren, die ein Benutzer Ihre Anwendung öffnet. Wenn Sie die Gesamtzahl der Anwendungsöffnungen anhand einzelner Öffnungsereignisse verfolgen, können Sie Anwendern bei der 100. Öffnung besondere Angebote oder Nachrichten zukommen lassen, um die Interaktion mit Ihrer Marke zu stärken.
1. **[!UICONTROL Lebenszeitwerte]:** Die Erfassung laufender Gesamtsummen, z. B. eines Kaufwerts für einen Kunden über die gesamte Lebensdauer, kann sehr schwierig sein. Dafür muss die historische Gesamtsumme bei jedem Auftreten eines neuen Kaufereignisses aktualisiert werden. Mit einem berechneten Attribut können Sie dies wesentlich einfacher tun, indem Sie den Lebenszeitwert in einem einzelnen Feld pflegen, das nach jedem erfolgreichen Kaufereignis, das mit dem Kunden verbunden ist, automatisch aktualisiert wird.

## Bekannte Einschränkungen

### Verzögerte Verfügbarkeit neuer berechneter Attribute

Die Verfügbarkeit neuer berechneter Attribute kann bis zu 2 Stunden nach dem Hinzufügen des entsprechenden Schemaattributs zum Vereinigungsschema verzögert werden.

Diese Verzögerung ist auf die aktuelle Cachekonfiguration zurückzuführen. Nach der Alpha-Methode kann die Aktualisierungshäufigkeit des Caches erhöht werden.

### Abhängigkeitsverfolgung in Segmenten

Schemaattribute, die bereits in einem Segmentdefinitionsausdruck verwendet, aber später in ein berechnetes Attribut umgewandelt wurden, werden nicht als Abhängigkeit dieses Segments verfolgt.

Da keine Abhängigkeit erkannt wurde, wertet Experience Platform das zugehörige berechnete Attribut nicht automatisch bei jeder Auswertung der Segmentdefinition aus.

Alternativ kann die Erstellung berechneter Attribute über eine bestimmte Schemafeldgruppe verwaltet werden, die neue berechnete Attribute hinzufügt, die nicht mit vorhandenen Attributen in Konflikt stehen. Eine weitere Alternative besteht darin, das Segment einfach mit der richtigen Abhängigkeitsverfolgung für die neuen berechneten Attribute neu zu erstellen.
