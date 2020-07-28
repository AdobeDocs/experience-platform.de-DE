---
keywords: Experience Platform;attribution ai;overview;popular topics
solution: Experience Platform
title: Übersicht über Attribution AIS
topic: Attribution AI
translation-type: tm+mt
source-git-commit: 83e74ad93bdef056c8aef07c9d56313af6f4ddfd
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 9%

---


# Übersicht über Attribution AIS

Attribution AI als Teil von Intelligent Services ist ein algorithmischer Zuordnungsdienst mit mehreren Kanälen, der den Einfluss und die inkrementelle Auswirkung von Kundeninteraktionen auf bestimmte Ergebnisse berechnet. Mit Attribution AI können Marketing-Experten die Ausgaben für Marketing und Werbung messen und optimieren, indem sie die Auswirkungen einzelner Kundeninteraktionen in einzelnen Phasen der Customer Journey untersuchen.

## Attribution AIS verstehen

Attribution AI wird verwendet, um Gutschriften Touchpoints zuzuordnen, die zu Konversions-Ereignissen führen. Dies kann von Marketingexperten genutzt werden, um die Marketingauswirkungen jedes einzelnen Marketing-Touchpoints über Kundenreisen hinweg zu quantifizieren. Beispiele für Touchpoints sind Display-Anzeigenimpressionen, E-Mail-Senden, E-Mail-Öffnen und Klicks auf gebührenpflichtige Suchen.

Attribution AI-Ausgaben können über verschiedene Dimensionen getrennt werden und können über verschiedene Phasen der Customer Journey hinweg genutzt werden. Dies erfolgt, ohne dass geschäftliche Anforderungen in maschinelle Lernprobleme, die Auswahl von Algorithmen, Schulungen oder die Bereitstellung von Modellen übersetzt werden müssen.

Attribution AI Daten können aus der Adobe stammen (z. [!DNL Analytics]) oder Datenquellen, die keine Adobe sind.

Attribution AI unterstützt zwei Kategorien von Ergebnissen, algorithmisch und regelbasiert. Algorithmische Ergebnisse beinhalten inkrementelle und beeinflusste Werte. Regelbasierte Ergebnisse sind First Touch, Last Touch, Linear, U-förmig und Time-Decay.

Das folgende Video hilft Ihnen, Attribution AIS besser zu verstehen.

>[!VIDEO](https://video.tv.adobe.com/v/32667?learn=on&quality=12)

## Algorithmische Attribution AIS

Attribution AI unterstützt zwei Kategorien von Zuordnungswerten, algorithmische und regelbasierte Werte.

Attribution AI produziert zwei verschiedene Arten von algorithmischen Ergebnissen, inkrementell und beeinflusst. Ein beeinflusster Wert ist der Anteil der Konversion, für die jeder Marketing-Touchpoint verantwortlich ist. Ein inkrementelles Ergebnis ist der Betrag der direkt durch den Marketing-Touchpoint verursachten marginalen Auswirkungen. Der Hauptunterschied zwischen dem inkrementellen Ergebnis und dem beeinflussten Ergebnis besteht darin, dass das inkrementelle Ergebnis den Basiseffekt berücksichtigt. Es wird nicht davon ausgegangen, dass eine Konversion ausschließlich durch die vorherigen Marketing-Touchpoints verursacht wird.

Die nachstehende Tabelle enthält weitere Details zu den einzelnen Zuordnungswerten:

| Zuordnungswerte | Beschreibung |
| ----- | ----------- |
| Erstkontakt | Regelbasiertes Zuordnungsergebnis, das dem ursprünglichen Touchpoint auf einem Konversionspfad alle Gutschriften zuweist. |
| Letztkontakt | Regelbasierter Zuordnungswert, der dem Touchpoint die Gutschrift zuweist, der der Konversion am nächsten kommt. |
| Linear | Regelbasiertes Zuordnungsergebnis, das jedem Touchpoint auf einem Konversionspfad die gleiche Gutschrift zuweist. |
| U-förmig | Regelbasiertes Zuordnungsergebnis, bei dem 40 % der Gutschrift dem ersten Touchpoint und 40 % der Gutschrift dem letzten Touchpoint zugeordnet werden, während die übrigen 20 % gleichmäßig auf die anderen Touchpoints aufgeteilt werden. |
| Zeitverfall | Regelbasierter Zuordnungswert, bei dem Touchpoints, die näher an der Konversion liegen, mehr gutgeschrieben werden als Touchpoints, die zeitlich weiter von der Konversion entfernt sind. |
| Beeinflusst (algorithmisch) | Einflussreiches Ergebnis ist der Anteil der Konversion, für den jeder Marketing-Touchpoint verantwortlich ist. |
| Inkrementell (algorithmisch) | Inkrementelles Ergebnis ist die Höhe des Grenzeffekts, der direkt durch einen Marketing-Touchpoint verursacht wird. |

## Beispiele für Geschäftsverwendungsfälle

Attribution AI kann zur Unterstützung der folgenden Anwendungsbeispiele verwendet werden:

- **Berichte**: Ermöglichen Sie es Führungskräften, die wahren inkrementellen Auswirkungen des Marketing zu verstehen, sowohl als Ganzes als auch nach Kanal, Region, SKU usw.
- **Mittelzuweisung**: Informieren Sie die Budgetzuweisungsentscheidungen über den Marketing Kanal.
- **Optimierung** der Kampagne: Verstehen Sie in jedem Kanal, welche Kampagnen, kreativen Elemente und Suchbegriffe für welche SKUs oder Geos besser funktionieren. Auf diese Weise können Sie sich jeden Kanal ansehen, damit das Marketingteam seine Taktik optimieren kann.
- **Vollständige Trichterzuordnung**: Verstehen Sie die Auswirkungen von Marketing auf die gesamte Customer Journey. Beispielsweise kostenlose Kontoanmeldung zur gebührenpflichtigen Konversion und darüber hinaus.
- **Partnerbewertungen**: Bewerten Sie die Effektivität von Agenturen und Partnern anhand der Zuordnungsergebnisse.

### Zusätzliche Funktionen

Attribution AI Angebote integrieren sich auch in andere Adoben wie [!DNL Adobe Analytics]. Auf diese Weise können Sie mithilfe dieser Lösungen das anpassbare Algorithmusmodell zur Bewertung der Medienleistung und zur Bereitstellung analytischer Einblicke einsetzen.

## Nächste Schritte

Beginnen Sie mit den [Ersten Schritten](./getting-started.md). Dieser Leitfaden führt Sie durch die Einrichtung aller erforderlichen Voranforderungen für Attribution AI. If you already have your credentials and data ready, visit the [Attribution AI user guide](./user-guide.md). Dieses Handbuch führt Sie durch das Erstellen einer Instanz sowie das Übermitteln der Instanz zum Trainieren und Bewerten.