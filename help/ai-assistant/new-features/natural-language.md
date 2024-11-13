---
title: Kostenlose Sprachschätzung mit AI Assistant
description: Erfahren Sie, wie Sie die Funktionen zur Schätzung der natürlichen Sprache von AI Assistant verwenden.
badge: Alpha
source-git-commit: aef3be05ca23abe9ed8275aa562fdd3313a7e2d0
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 0%

---

# Natürliche Sprachschätzung mit AI Assistant

>[!AVAILABILITY]
>
>Diese Funktion ist in Alpha verfügbar und steht Ihrem Unternehmen möglicherweise nicht zur Verfügung. Wenden Sie sich an Ihr Adobe-Account-Team, um am Alpha-Programm teilzunehmen und auf diese Funktion zuzugreifen.

Sie können die Funktionen zur Schätzung natürlicher Sprachen des AI-Assistenten für Adobe Experience Platform verwenden, um die Größe von Zielgruppen zu schätzen und die Neigung von Zielgruppen auf der Grundlage einfacher, kommunikativer Fragen vorherzusagen. Mit dieser Funktion können Sie Einblicke aus Zielgruppen leichter zugänglich und intuitiver machen. Dies kann besonders für Ihre geschäftlichen und Marketing-Vorgänge nützlich sein, insbesondere wenn Sie Ihre Zielgruppen täglich verwalten und sich bei der Gestaltung effektiver Marketing-Strategien auf diese Einblicke verlassen.

Mit den Funktionen der automatischen Sprachverarbeitung des KI-Assistenten können Sie Fragen stellen wie: &quot;Wie viele Profile habe ich in Kalifornien zwischen 25 und 35 Jahren&quot;oder &quot;Wie viele hochwertige Kunden haben wir?&quot; oder sogar &quot;Welcher Prozentsatz meiner Zielgruppe wird wahrscheinlich innerhalb des nächsten Monats kaufen?&quot; Der AI-Assistent interpretiert diese Fragen und gibt Schätzungen oder Tendenzwerte zurück, die Sie für datenbasierte Entscheidungen verwenden können.

In diesem Dokument erfahren Sie, wie Sie die Funktionen zur Schätzung der natürlichen Sprache von AI Assistant verwenden können.

## Wichtige Begriffe und Definitionen {#key-terminology-and-definitions}

In der folgenden Tabelle finden Sie eine Liste wichtiger Begriffe und der zugehörigen Definitionen.

| Terminologie | Definition |
| --- | --- |
| Schätzung der Zielgruppengröße | Der Prozess der Berechnung der Anzahl der Mitglieder innerhalb einer bestimmten Zielgruppe anhand eines definierten Kriteriums. Sie können Ihre Größenschätzungen auf Profildaten basieren, einschließlich Profilen, die nicht in einer Zielgruppe enthalten sind. Darüber hinaus können Sie Schätzungen der Zielgruppengröße abrufen, ohne zuvor eine Zielgruppe erstellen zu müssen. Verwenden Sie diese Einblicke, um den Umfang Ihrer Reichweite für zielgerichtete Kampagnen zu verstehen. |
| Tendenzschätzung | Eine Vorhersage der Wahrscheinlichkeit, dass Mitglieder in einer Zielgruppe innerhalb eines bestimmten Zeitraums bestimmte Verhaltensweisen zeigen (z. B. Einkäufe tätigen, kursieren). Die Tendenzschätzung ist für Zielgruppen in Real-time Customer Data Platform spezifisch, kann aber Profildaten enthalten, einschließlich Profilen in allen Zielgruppen. Sie können diese Einblicke bei der Optimierung Ihrer Kampagnen und der Verwaltung von Strategien zur Zielgruppenbeibehaltung referenzieren. |
| Natürliche Sprachverarbeitung | Die Fähigkeit der KI-Assistenzkraft, alltägliche Fragen zu interpretieren und zu beantworten, sodass Sie ohne technische Abfragen kommunikativ interagieren und relevante Einblicke erhalten können. |
| Vordefinierte Zeitrahmen | Standardzeitbereiche ( &quot;Letzter Monat&quot;, &quot;Nächste 30 Tage&quot;), die vom AI-Assistenten zur Schätzung der Zielgruppengröße und -neigung unterstützt werden. **Hinweis**: Benutzerdefinierte Zeitrahmen werden während der Alpha-Phase möglicherweise nicht vollständig unterstützt. |
| Momentaufnahmen-Daten | Der Datensatz, der von AI Assistant zur Bereitstellung von Schätzungen verwendet wird. Diese Daten werden alle 24-48 Stunden von Real-time Customer Data Platform aktualisiert. Daher spiegeln Einblicke möglicherweise keine Änderungen der Zielgruppe in Echtzeit wider. |

{style="table-layout:auto"}

## Anwendungsbeispiele {#use-case-examples}

Die Funktionen zur Schätzung der natürlichen Sprache des KI-Assistenten können in den folgenden Anwendungsfällen besonders hilfreich sein:

### Marketing-Vorgänge

Als professioneller Marketing-Experte können Sie Zielgruppendaten verwalten und überwachen, um sicherzustellen, dass sie mit Ihren Geschäftszielen in Einklang stehen. Mit der Funktion zur Schätzung der natürlichen Sprache des KI-Assistenten können Sie schnell Einblicke in die Größe und Neigung von Zielgruppen gewinnen, ohne dass Sie zuerst eine Audience erstellen müssen oder umfangreiche Kenntnisse zur Datenanalyse benötigen.

Unterstützung bei der Aufrechterhaltung eines konsistenten, datengesteuerten Ansatzes in ihren Workflows.

### Geschäftsbenutzer und Marketing-Experten

Als Business-Anwender und Marketing-Experte kann der schnelle Zugriff auf Zielgruppendaten entscheidend für den Erfolg Ihrer Kampagnenplanung, -zielgruppenbestimmung und -bewertung sein. Mit der Funktion zur Schätzung der natürlichen Sprache des KI-Assistenten können Sie Ihren Zugriff auf Zielgruppendaten vereinfachen, unkomplizierte Fragen stellen und praktische Einblicke erhalten, die Sie bei der Erstellung und Optimierung von Zielgruppen unterstützen.

## Wichtigste Funktionen

>[!IMPORTANT]
>
>Die folgenden Funktionen sind in Alpha verfügbar und konzentrieren sich auf grundlegende Fähigkeiten der Schätzung natürlicher Sprachen. Da sich diese Funktion im Alpha befindet, müssen Sie sicherstellen, dass Sie die Antworten, die Sie von AI Assistant erhalten, auf ihre Richtigkeit doppelprüfen.

### Schätzung der Zielgruppengröße

Sie können kostenlose Sprachabfragen verwenden, um AI Assistant zu bitten, die Größe bestimmter Zielgruppen zu schätzen. Diese Funktion kann besonders für die Messung der Reichweite und Auswirkung von Zielgruppen nützlich sein. Als Marketingstratege können Sie beispielsweise Fragen stellen wie:

* &quot;Wie viele Profile leben in New York?&quot;
* &quot;Wie viele Profile habe ich mit einer E-Mail und habe zugestimmt?&quot;

Verwenden Sie diese Funktion, um die Schätzung der Zielgruppengrößen zu vereinfachen und sofort Antworten zu erhalten, ohne komplexe Datenfilter oder Segmentdefinitionen durchsuchen zu müssen.

### Schätzung der Audience-Neigung

>[!TIP]
>
>Ihr Experience Platform-Konto muss über [Customer AI](../../intelligent-services/customer-ai/overview.md) verfügen, um die Tendenzschätzungsfunktionen des KI-Assistenten nutzen zu können.

Sie können die Tendenzschätzung der Zielgruppe verwenden, um die Wahrscheinlichkeit bestimmter Verhaltensweisen oder Aktionen innerhalb einer Zielgruppe zu ermitteln. Sie können beispielsweise Fragen stellen wie:

* &quot;Welcher Prozentsatz meiner aktuellen Zielgruppe wird voraussichtlich im nächsten Monat gekauft?&quot;
* &quot;Wie viele Profile habe ich mit einer hohen Konversionsneigung?&quot;

Indem Sie Fragen zur natürlichen Sprache stellen, können Sie Tendenzwerte abrufen, die den Prozentsatz oder die Wahrscheinlichkeit von Zielgruppenmitgliedern angeben, die bestimmte Verhaltensweisen zeigen, und Sie dabei unterstützen, proaktive Anpassungen an Ihren Kampagnen oder Aufbewahrungsstrategien vorzunehmen.

## Beispielfragen zur Zielgruppengröße und Tendenzschätzung

Im Folgenden finden Sie Beispielfragen, die Sie an den KI-Assistenten richten können, um Ihr Verständnis der Zielgruppengröße und Verhaltensanfälligkeit zu erhalten:

### Schätzung der Zielgruppengröße

* &quot;Wie viele Profile habe ich mit einer E-Mail- oder Mobiltelefonnummer?&quot;
* &quot;Wie viele Profile habe ich in New York?&quot;
* &quot;Was sind die fünf wichtigsten Staaten, in denen meine Kunden leben?&quot;

### Schätzung der Zielgruppen-Propensity

* &quot;Welcher Prozentsatz meiner Zielgruppe wird wahrscheinlich innerhalb des nächsten Monats kaufen?&quot;
* &quot;Wie viele Kunden werden voraussichtlich im nächsten Quartal konvertieren?&quot;

Sie können die Flexibilität natürlicher Sprachabfragen nutzen, um schnelle Einblicke in die Zielgruppendynamik zu erhalten, ohne technische Kenntnisse zu benötigen.

## Häufig gestellte Fragen

In diesem Abschnitt finden Sie Antworten auf häufig gestellte Fragen zur Schätzung natürlicher Sprachen mit dem KI-Assistenten.

### Wie oft aktualisiert der KI-Assistent Zielgruppendaten?

Die Daten der KI-Assistenzkraft werden alle 24-48 Stunden aktualisiert. Daher können Schätzungen geringfügige Verzögerungen widerspiegeln. Wenn Sie nach &quot;aktuellen&quot;Daten fragen, spiegelt die Antwort die neueste Momentaufnahme wider, die bis zu 48 Stunden alt sein kann.

### Kann ich nach Zielgruppengrößen oder Eigenschaften mit benutzerdefinierten Datumsbereichen fragen?

Derzeit unterstützt der AI-Assistent vordefinierte Datumsbereiche, z. B. &quot;Letzter Monat&quot;oder &quot;Nächste 30 Tage&quot;. Benutzerdefinierte Datumsbereiche, die über diese vordefinierten Optionen hinausgehen, werden in der Phase &quot;Alpha&quot;nicht vollständig unterstützt. Wenn ein benutzerdefinierter Zeitrahmen angefordert wird, bietet der KI-Assistent Einblicke basierend auf dem nächstverfügbaren Zeitrahmen.

### Wie berechnet der KI-Assistent Tendenzwerte?

Tendenzwerte werden mit [Customer AI](../../intelligent-services/customer-ai/overview.md) berechnet. Der KI-Assistent verwendet Modelle für maschinelles Lernen, um die Wahrscheinlichkeit bestimmter Verhaltensweisen von Zielgruppen wie Käufen und Abwanderungen innerhalb des angeforderten Zeitraums vorherzusagen. Während des Alphas verwendet die Tendenzwertberechnung im AI-Assistenten keine Erlebnisereignisse oder Verhaltensdaten.

### Wird der AI-Assistent Zielgruppengrößen oder -neigungen auf der Grundlage von Echtzeitdaten schätzen?

Nein, Echtzeitdaten sind derzeit nicht verfügbar. Die Schätzungen basieren auf aktuellen Datenmomentaufnahmen, die alle 24-48 Stunden aktualisiert werden. Echtzeit-Updates werden während des Alphas nicht berücksichtigt.

### Wie werden Eigenschaften berechnet?

Der KI-Assistent nutzt Customer AI-Modelle zur Beantwortung aller Wahrscheinlichkeits- oder Tendenzwerte.

## Out-of-Scope-Funktionen

Die folgenden Funktionen werden derzeit nicht unterstützt:

### Zielgruppengrößenschätzungen basierend auf dem Ereignis von Verhaltensdaten

Der KI-Assistent kann derzeit keine Fragen beantworten, die auf Verhaltensdaten wie &quot;**&quot;Wie viele Benutzer in den letzten 30 Tagen ein Produkt zum Warenkorb hinzugefügt haben&quot;**. Sie können jedoch ein berechnetes Attribut in Real-Time CDP erstellen, das diese Werte vorab berechnen kann. Diese berechneten Attribute sind dann im AI-Assistenten verfügbar. Weitere Informationen finden Sie in der Dokumentation zu [berechneten Attributen](../../profile/computed-attributes/overview.md).

### Echtzeit-Datenaktualisierungen

Die von AI Assistant bereitgestellten Schätzungen basieren auf aktuellen, aber nicht Echtzeit-Datenmomentaufnahmen. Die Daten werden alle 24 bis 48 Stunden aktualisiert, sodass Einblicke diese Verzögerung widerspiegeln. Diese Einschränkung bedeutet, dass Benutzer keine sofortigen Aktualisierungen erhalten können, wenn sich ein Segment oder ein Datensatz innerhalb kurzer Zeit signifikant ändert.