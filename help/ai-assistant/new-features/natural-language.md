---
title: Schätzung der natürlichen Sprache mit KI-Assistent
description: Erfahren Sie, wie Sie die Funktionen zum Schätzen der natürlichen Sprache des KI-Assistenten verwenden.
badge: Alpha
exl-id: 7997c84f-288b-4b48-9f88-8de4addbae36
source-git-commit: e2cb6dee0c255c8eaa3729cc7a09ae07a1f33dbc
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 0%

---

# Schätzung der natürlichen Sprache mit KI-Assistent

>[!AVAILABILITY]
>
>Diese Funktion befindet sich im Alpha und steht Ihrer Organisation möglicherweise nicht zur Verfügung. Um am Alpha-Programm teilzunehmen und auf diese Funktion zuzugreifen, wenden Sie sich an Ihr Adobe-Account-Team.

Sie können die Funktionen zur Schätzung natürlicher Sprachen des KI-Assistenten für Adobe Experience Platform verwenden, um Zielgruppengrößen zu schätzen und Zielgruppenneigungen auf der Grundlage einfacher, dialogorientierter Fragen vorherzusagen. Mit dieser Funktion können Sie Zielgruppeneinblicke zugänglicher und intuitiver gestalten. Dies kann besonders für Anwendungsfälle Ihres Unternehmens und Ihrer Marketing-Abläufe nützlich sein, insbesondere wenn Sie Ihre Zielgruppen täglich verwalten und sich bei der Gestaltung effektiver Marketing-Strategien auf diese Einblicke verlassen.

Mit den natürlichen Sprachverarbeitungsfunktionen von AI Assistant können Sie Fragen stellen wie: „Wie viele Profile habe ich in Kalifornien zwischen 25 und 35 Jahren“ oder „Wie viele hochwertige Kunden haben wir?“ oder sogar „Welcher Prozentsatz meiner Zuschauer wird wahrscheinlich innerhalb des nächsten Monats einkaufen?“ Der KI-Assistent interpretiert diese Fragen und gibt Schätzungen oder Tendenz-Scores zurück, die Sie verwenden können, um dateninformierte Entscheidungen zu treffen.

Lesen Sie dieses Dokument, um zu erfahren, wie Sie die Funktionen des KI-Assistenten zur Schätzung natürlicher Sprachen verwenden können.

## Wichtige Terminologie und Definitionen {#key-terminology-and-definitions}

In der folgenden Tabelle finden Sie eine Liste wichtiger Begriffe und der zugehörigen Definitionen.

| Terminologie | Definition |
| --- | --- |
| Schätzung der Zielgruppengröße | Der Prozess der Berechnung der Anzahl der Mitglieder in einer bestimmten Zielgruppe basierend auf definierten Kriterien. Sie können Ihre Größenschätzungen auf Profildaten basieren, einschließlich Profilen, die nicht in einer Zielgruppe enthalten sind. Darüber hinaus können Sie Schätzungen der Zielgruppengröße abrufen, ohne zunächst eine Zielgruppe erstellen zu müssen. Nutzen Sie diesen Einblick, um die Größenordnung Ihrer Reichweite für zielgerichtete Kampagnen zu verstehen. |
| Tendenzschätzung | Eine Prognose der Wahrscheinlichkeit, dass Mitglieder einer Zielgruppe innerhalb eines bestimmten Zeitraums bestimmte Verhaltensweisen zeigen (wie z. B.: einen Kauf tätigen, abwandern). Die Neigungsschätzung ist spezifisch für Audiences in Real-time Customer Data Platform, kann jedoch Profildaten, einschließlich Profile, in beliebigen Audiences enthalten. Sie können diese Einblicke bei der Optimierung Ihrer Kampagnen und der Verwaltung von Strategien zur Zielgruppentreue heranziehen. |
| Natürliche Sprachverarbeitung | Die Fähigkeit des KI-Assistenten, Fragen in alltäglicher Sprache zu interpretieren und zu beantworten, sodass Sie ohne Verwendung technischer Abfragen interagieren und relevante Erkenntnisse erhalten können. |
| Vordefinierte Zeitrahmen | Von AI Assistant unterstützte Standardzeitbereiche ( „letzter Monat“, „nächste 30 Tage„) zur Schätzung von Zielgruppengröße und -neigung. **Hinweis**: Benutzerdefinierte Zeitrahmen werden während des Alphas möglicherweise nicht vollständig unterstützt. |
| Momentaufnahmen-Daten | Der von KI-Assistent verwendete Datensatz, um Schätzungen bereitzustellen. Diese Daten werden von Real-time Customer Data Platform alle 24 bis 48 Stunden aktualisiert, sodass die Einblicke möglicherweise keine Echtzeit-Zielgruppenänderungen widerspiegeln. |

{style="table-layout:auto"}

## Anwendungsbeispiele {#use-case-examples}

Die Funktionen zur Schätzung der natürlichen Sprache des KI-Assistenten können besonders für die folgenden Anwendungsfälle hilfreich sein:

### Marketing-Vorgänge

Als Marketing-Experte können Sie unter anderem für die Verwaltung und Überwachung von Zielgruppendaten verantwortlich sein, um sicherzustellen, dass diese mit Ihren Geschäftszielen übereinstimmen. Mit der Funktion zur Schätzung der natürlichen Sprache des KI-Assistenten können Sie schnell Einblicke in die Größe und Neigung von Zielgruppen gewinnen, ohne zuerst eine Zielgruppe oder umfangreiches Wissen zur Datenanalyse erstellen zu müssen.

Unterstützung bei der Aufrechterhaltung eines konsistenten, datengesteuerten Ansatzes in ihren Workflows.

### Business-Anwender und Marketing-Experten

Als Business-Anwenderin bzw. -Anwender und Marketing-Expertin kann der schnelle Zugriff auf Zielgruppendaten entscheidend für den Erfolg Ihrer Kampagnenplanung, Zielgruppenbestimmung und Auswertung sein. Mit der Funktion zur Schätzung der natürlichen Sprache des KI-Assistenten können Sie den Zugriff auf Zielgruppeninformationen vereinfachen, einfache Fragen stellen und umsetzbare Einblicke erhalten, die bei der Erstellung und Optimierung von Zielgruppen helfen.

## Wichtigste Funktionen

>[!IMPORTANT]
>
>Die folgenden Funktionen befinden sich im Alpha und konzentrieren sich auf die grundlegenden Funktionen der Schätzung natürlicher Sprachen. Da sich diese Funktion im Alpha befindet, müssen Sie sicherstellen, dass Sie die Antworten, die Sie vom KI-Assistenten erhalten, auf Korrektheit überprüfen.

### Schätzung der Zielgruppengröße

Mit Abfragen in natürlicher Sprache können Sie den KI-Assistenten bitten, die Größe bestimmter Zielgruppen zu schätzen. Diese Funktion kann besonders nützlich sein, um die Reichweite und Wirkung von Zielgruppen zu messen. Als Marketing-Stratege können Sie zum Beispiel Fragen stellen wie:

* „Wie viele Profile leben in New York?“
* „Wie viele Profile habe ich mit einer E-Mail und habe zugestimmt?“

Verwenden Sie diese Funktion, um das Schätzen der Zielgruppengrößen zu vereinfachen und sofortige Antworten zu erhalten, ohne durch komplexe Datenfilter oder Segmentdefinitionen navigieren zu müssen.

### Schätzung der Zielgruppenneigung

>[!TIP]
>
>Ihr Experience Platform-Konto muss mit [Kunden-KI](../../intelligent-services/customer-ai/overview.md) bereitgestellt werden, damit die Funktionen zum Schätzen der Tendenz des KI-Assistenten verwendet werden können.

Mit einer Schätzung der Zielgruppen-Neigung können Sie die Wahrscheinlichkeit bestimmter Verhaltensweisen oder Aktionen in einer Zielgruppe identifizieren. Sie können zum Beispiel Fragen stellen wie:

* „Welcher Prozentsatz meiner aktuellen Audience wird im nächsten Monat wahrscheinlich einkaufen?“
* „Wie viele Profile habe ich mit einer hohen Konversionsneigung?“

Indem Sie Fragen zur natürlichen Sprache stellen, können Sie Tendenzwerte abrufen, die den Prozentsatz oder die Wahrscheinlichkeit angeben, mit der Zielgruppenmitglieder bestimmte Verhaltensweisen zeigen. So können Sie proaktive Anpassungen an Ihren Kampagnen oder Kundenbindungsstrategien vornehmen.

## Beispielfragen für die Schätzung der Zielgruppengröße und -neigung

Im Folgenden finden Sie Beispielfragen, die Sie dem KI-Assistenten stellen können, um die Zielgruppengrößen und Verhaltensneigungen besser zu verstehen:

### Schätzung der Zielgruppengröße

* „Wie viele Profile habe ich mit einer E-Mail- oder Mobiltelefonnummer?“
* „Wie viele Profile habe ich in New York?“
* „Was sind die fünf wichtigsten Bundesstaaten, in denen meine Kunden leben?“

### Schätzung der Zielgruppenneigung

* „Welcher Prozentsatz meiner Zielgruppe wird innerhalb des nächsten Monats wahrscheinlich einkaufen?“
* „Von wie vielen Kunden wird im nächsten Quartal eine Konversion erwartet?“

Sie können die Flexibilität nutzen, die Abfragen in natürlicher Sprache bieten, um schnelle Einblicke in die Dynamik Ihrer Zielgruppe zu erhalten, ohne dass Sie technisches Fachwissen benötigen.

## Häufig gestellte Fragen

In diesem Abschnitt finden Sie Antworten auf häufig gestellte Fragen zur Schätzung der natürlichen Sprache mit dem KI-Assistenten.

### Wie oft aktualisiert der KI-Assistent Zielgruppendaten?

Die Daten des KI-Assistenten werden alle 24-48 Stunden aktualisiert. Daher können Schätzungen geringfügige Verzögerungen widerspiegeln. Wenn Sie also nach „aktuellen“ Daten fragen, spiegelt die Antwort den letzten Schnappschuss wider, der bis zu 48 Stunden alt sein kann.

### Kann ich nach Zielgruppengrößen oder -neigungen mit benutzerdefinierten Datumsbereichen fragen?

Derzeit unterstützt der KI-Assistent vordefinierte Datumsbereiche wie „Letzter Monat“ oder „Nächste 30 Tage“. Benutzerdefinierte Datumsbereiche, die über diese vordefinierten Optionen hinausgehen, werden im Alpha-Schritt nicht vollständig unterstützt. Wenn ein benutzerdefinierter Zeitrahmen angefordert wird, liefert der KI-Assistent Einblicke basierend auf dem nächstmöglichen verfügbaren Zeitrahmen.

### Wie berechnet der KI-Assistent Tendenz-Scores?

Neigungs-Scores werden mithilfe von [Kunden-KI](../../intelligent-services/customer-ai/overview.md) berechnet. Der KI-Assistent verwendet Modelle für maschinelles Lernen, um die Wahrscheinlichkeit bestimmter Zielgruppenverhaltensweisen wie Käufe und Abwanderung innerhalb des angeforderten Zeitrahmens vorherzusagen. Während des Alphas verwendet die Berechnung des Tendenz-Scores im KI-Assistenten keine Erlebnisereignisse oder Verhaltensdaten.

### Wird der KI-Assistent Zielgruppengrößen oder -neigungen basierend auf Echtzeitdaten schätzen?

Nein, Echtzeitdaten sind derzeit nicht verfügbar. Die Schätzungen basieren auf aktuellen Daten-Snapshots, die alle 24-48 Stunden aktualisiert werden. Echtzeit-Updates liegen während des Alphas außerhalb des Geltungsbereichs.

### Wie werden Tendenzen berechnet?

Der KI-Assistent nutzt Kunden-KI-Modelle zur Beantwortung von Wahrscheinlichkeits- oder Tendenzwerten.

## Nicht im Umfang enthaltene Funktionen

Die folgenden Funktionen werden derzeit nicht unterstützt:

### Schätzungen der Zielgruppengröße basierend auf Ereignissen von Verhaltensdaten

Der KI-Assistent kann derzeit keine Fragen beantworten, die auf Verhaltensdaten wie **basieren: „Wie viele Benutzende haben in den letzten 30 Tagen ein Produkt zum Warenkorb hinzugefügt?**. Sie können jedoch ein berechnetes Attribut in Real-Time CDP erstellen, das solche Werte vorberechnen kann. Diese berechneten Attribute sind dann im KI-Assistenten verfügbar. Weitere Informationen finden Sie in der Dokumentation zu [berechneten Attributen](../../profile/computed-attributes/overview.md).

### Echtzeit-Datenaktualisierungen

Die vom KI-Assistenten bereitgestellten Schätzungen basieren auf aktuellen, jedoch nicht auf Echtzeit-Daten-Momentaufnahmen. Die Daten werden alle 24-48 Stunden aktualisiert, sodass die Einblicke diese Verzögerung widerspiegeln. Diese Einschränkung bedeutet, dass Benutzende keine sofortigen Aktualisierungen erhalten können, wenn ein Segment oder Datensatz innerhalb eines kurzen Zeitraums erheblich geändert wird.
