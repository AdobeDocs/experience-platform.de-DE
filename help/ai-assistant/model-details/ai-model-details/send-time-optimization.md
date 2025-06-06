---
title: Details zum Sendezeit-Optimierungsmodell
description: Erfahren Sie mehr über das KI-Modell, das für die Sendezeitoptimierung in Adobe Journey Optimizer verwendet wird.
hide: true
hidefromtoc: true
exl-id: 95e1fc8f-1817-40d7-aa55-93daa50f43c0
source-git-commit: 481108135ee6ed5b90547e4e95799ab99edb210e
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 10%

---

# Details zum Sendezeit-Optimierungsmodell

## Modellübersicht {#model-overview}

* **Modellname und -version**: Sendezeitoptimierung
* **Modellveröffentlichungsdatum:** 2024
* **Modellzweck**: Das Adobe Journey Optimizer-Modell zur Optimierung des Versandzeitpunkts wählt den optimalen Versandzeitpunkt für E-Mail- und Push-Nachrichten aus, um die Kundeninteraktion auf der Grundlage des historischen Öffnungs- und Klickverhaltens Ihrer Kunden zu maximieren.
* **Vorgesehene Benutzer**: Die primären Benutzer dieses Modells sind Marketing-Experten, Produkt-Manager und Kundeninteraktions-Teams, die Adobe Journey Optimizer zur Förderung datengesteuerter Marketing-Strategien nutzen.
* **Anwendungsfälle**: Die Sendezeitoptimierung eignet sich am besten für weniger dringende Marketing-Nachrichten, z. B. eine wöchentliche Anzeige, Werbeinformationen über ein neues Produkt oder Informationen über einen einmonatigen Verkauf. Die Sendezeitoptimierung ist nur für die integrierten Aktionstypen E-Mail und Push von Journey Optimizer verfügbar und derzeit nicht für Nachrichten, die über benutzerdefinierte Aktionen oder für andere Aktionstypen gesendet werden.
* **Potenzieller Missbrauch**: Die Sendezeitoptimierung sollte nicht für dringende, zeitkritische Betriebsnachrichten verwendet werden - z. B. eine Bestellbestätigung, eine Benachrichtigung zum Zurücksetzen des Kennworts oder eine Benachrichtigung über eine Änderung des Fluggatters.

## Modelldetails {#model-details}

* **Modelltyp**: Das Modell „Sendezeitoptimierung“ nimmt die Adobe Journey Optimizer-Kundenverhaltensdaten Ihres Unternehmens auf und untersucht Öffnungs- und Klickereignisse auf Benutzerebene, um vorherzusagen, wann Ihre Kunden mit der größten Wahrscheinlichkeit mit Ihrer Nachricht interagieren. Das Öffnungs- und Klickverhalten auf Benutzerebene für jede Wochenstunde wird gewichtet und mit dem Lookalike- und dem Gesamtbenutzerverhalten mithilfe einer [!DNL Bayesian] kombiniert. Die [!DNL Bayesian] Prognosen für jede Stunde der Woche werden dann nach Rang geordnet, was zu einer „Heatmap“ für jede Metrik (E-Mail-Öffnungen, E-Mail-Klicks und Push-Öffnungen) für jeden Kunden führt, um die Wochenstunden vorherzusagen, zu denen die Kontaktaufnahme mit jedem Benutzer am wahrscheinlichsten und am wenigsten zum gewünschten Interaktionsergebnis führt.
* **Eingabe**: Die Sendezeitoptimierung verwendet Benutzerzeitzonendaten im Feld &quot;`timeZone`&quot; innerhalb der Feldergruppe [!UICONTROL Voreinstellungsdetails], falls angegeben, um die Zeitzone eines Benutzers zu bestimmen. Wenn die Zeitzone eines Benutzers im Feld `timeZone` nicht verfügbar ist, versucht die Sendezeitoptimierung, auf die Zeitzone des Benutzers zu schließen, basierend auf der häufigsten Zeitzonenübereinstimmung mit der ersten im Profil des Benutzers gespeicherten Postanschrift unter Verwendung des Datentyps [Postanschrift](../../../xdm/data-types/postal-address.md). Die Sendezeitoptimierung trifft Prognosen für jede Benutzerin und jeden Benutzer basierend auf drei Arten von Verhaltensdaten:
   * Das Öffnungs- und Klickverhalten Ihrer Benutzer insgesamt.
   * Das Öffnungs- und Klickverhalten von Lookalike-Benutzern in derselben Zeitzone.
   * Das Öffnungs- und Klickverhalten dieses einzelnen Benutzers.
* **Ausgabe**: Diese Prognosen werden gewichtet und mithilfe eines [!DNL Bayesian] Ansatzes kombiniert, was zu einer „Heatmap“ für jede Metrik (E-Mail-Öffnungen, E-Mail-Klicks und Push-Öffnungen) für jeden Kunden führt. Dies gibt die Stunden der Woche an, zu der die Kontaktaufnahme mit diesem Benutzer am wahrscheinlichsten und am wenigsten zum gewünschten Interaktionsergebnis führt (Öffnen/Klicken), wie in der folgenden Beispiel-Heatmap dargestellt:

![Die Heatmap zur Sendezeitoptimierung.](../../images/models/send-time-optimization.png)

* **Beispiel-Eingabe und -**: Um die Auswirkungen des Modells auf die Profilreichhaltigkeit zu minimieren, werden Modellbewertungen in drei in `_experience.intelligentServices.journeyAI.sendTimeOptimization` gespeicherten Profilattributen gespeichert und komprimiert und sind nicht für die menschliche Lesbarkeit konzipiert.

## Modellschulung {#model-training}

* **Schulungsdaten und Vorverarbeitung**: Der Schulungsdatensatz für jede Organisation wird nur aus den eigenen Daten in Adobe Experience Platform bezogen.
   * Sobald die Funktion zur Optimierung des Versandzeitpunkts für Ihr Unternehmen aktiviert ist, wird das Modell für die letzten 16 Wochen für E-Mail-, Push-, Sende-, Öffnungs- und Klickereignisse in allen Journey und Aktionen Ihres Unternehmens trainiert - unabhängig davon, ob bei diesen Aktionen die Optimierung des Versandzeitpunkts verwendet wird. Dadurch kann die Optimierung des Versandzeitpunkts von allen Daten profitieren, die durch Ihre Kundschaft generiert wurden.
   * Die Modelle werden zunächst wöchentlich trainiert und ausgewertet. Nach 16 Wochen werden die Modelle dann monatlich neu trainiert und ausgewertet. Die Modellbewertung umfasst alle Kundenprofile - sowohl vorhandene als auch neue - seit dem letzten Scoring-Durchgang.
   * Nachrichten, die von der Sendezeitoptimierung gesendet werden, erhalten eine der folgenden Optionen:
      * Versandzeit einer „Exploration“-Nachricht, ausgewählt zum Testen verschiedener Versandzeiten und zum Beobachten der Reaktion von Kunden
      * Eine „optimierte“ Versandzeit für Nachrichten, ausgewählt zur Maximierung der Klick-/Öffnungsraten. 5 % der Versandereignisse erhalten eine Versandzeit zum „Ausprobieren“ und 95 % der Versandereignisse sind „optimiert“.
   * Die Versandzeiten zum Ausprobieren werden zufällig aus den Versandzeiten ausgewählt, die durch die konfigurierte maximale Wartezeit zur Verfügung gestellt werden. Wenn beispielsweise eine Nachricht um 9 Uhr Mittwoch mit aktivierter Sendezeitoptimierung und einer maximalen Wartezeit von 3 Stunden ausgewählt wird, werden die Explorations-Sendezeiten für die Nachricht gleichmäßig zwischen 9 Uhr, 10 Uhr, 11 Uhr und 12 Uhr aufgeteilt.

## Modellauswertung {#model-evaluation}

* **Modellauswertung**: Die Sendezeitoptimierung kann die E-Mail-Klickrate und die Push-Öffnungsrate in allen von einem Unternehmen optimierten Nachrichten im Bereich von etwa 2 % bis 10 % erhöhen.
   * Wenn beispielsweise ein Unternehmen, das E-Mails ohne Sendezeitoptimierung sendet, eine durchschnittliche Klickrate von 5,0 % aufweist, kann derselbe Satz von E-Mails mit Sendezeitoptimierung zu einer durchschnittlichen Klickrate von 5,5 % führen (5,0 % * (1 + 10 %) = 5,5 %).
   * Aufgrund von Variabilität innerhalb kleiner Stichprobengrößen lässt sich ein Vorteil der Versandzeitoptimierung bei einzelnen Nachrichtensendungen möglicherweise nicht feststellen.
   * Organisationen profitieren in den folgenden Fällen mit höherer Wahrscheinlichkeit von den Vorteilen der Versandzeitoptimierung:
      * Bestehende Journey verwenden feste und nicht gut optimierte Versandzeiten.
      * Variables Kundenverhalten (Klicks und Öffnungen) entspricht dem Kundenstandort und den Kundenpräferenzen;
      * Unternehmen verwenden die Sendezeitoptimierung für einen größeren Anteil von E-Mail- und Push-Nachrichten.
      * Unternehmen wählen maximale Wartezeiten innerhalb des empfohlenen Bereichs von 6 bis 12 Stunden.

## Modellbereitstellung {#model-deployment}

* **Modellaktualisierung**: Modelle werden zunächst einmal wöchentlich trainiert und bewertet. Nach 16 Wochen werden die Modelle dann monatlich neu trainiert und ausgewertet. Die Modellauswertung umfasst alle Kundenprofile – sowohl vorhandene als auch neue seit der letzten Auswertung.

## Fairness und Voreingenommenheit {#fairness-and-bias}

* **Modellfairness**: Falsche Rückschlüsse auf die Zeitzone eines Benutzers können dazu führen, dass eine Nachricht für einen bestimmten Benutzer früher als optimal oder für einen bestimmten Benutzer später als optimal gesendet wird. Alle Benutzer in einer Kommunikation, die die Sendezeitoptimierung verwendet, erhalten jedoch letztendlich eine Nachricht und haben die Möglichkeit, mit einer Nachricht zu interagieren. Darüber hinaus verwendet dieses Modell keine demografischen Benutzerdaten oder Proxys für demografische Daten, sondern nur Daten zum Benutzerverhalten und zur Zeitzone. Die Bedenken im Hinblick auf die Fairness sind daher begrenzt und werden abgeschwächt.
* **Datenverzerrungen**: Falsche Rückschlüsse auf die Zeitzone eines Benutzers können dazu führen, dass eine Nachricht für einen bestimmten Benutzer früher als optimal oder für einen bestimmten Benutzer später als optimal gesendet wird. Alle Benutzer in einer Kommunikation, die die Sendezeitoptimierung verwendet, erhalten jedoch letztendlich eine Nachricht und haben die Möglichkeit, mit einer Nachricht zu interagieren. Darüber hinaus verwendet dieses Modell keine demografischen Benutzerdaten oder Proxys für demografische Daten, sondern nur Daten zum Benutzerverhalten und zur Zeitzone. Daher werden Bedenken in Bezug auf Verzerrungen begrenzt und ausgeräumt.

## Stärke {#robustness}

* **Modellstabilität**: Profile ohne ausreichende Interaktions-Ereignisdaten (häufig der Fall bei neuen Profilen) erhalten entweder eine sofortige Sendezeit, eine Explorations-Sendezeit innerhalb des ausgewählten Fensters oder eine Sendezeit, die auf der leistungsstärksten Sendezeit für alle Kunden basiert.

## Ethische Überlegungen {#ethical-considerations}

* **Ethische Überlegungen im Zusammenhang mit dem Modell**: Falsche Rückschlüsse auf die Zeitzone eines Benutzers können dazu führen, dass eine Nachricht für einen bestimmten Benutzer früher als optimal oder für einen bestimmten Benutzer später als optimal gesendet wird. Alle Benutzer in einer Kommunikation, die die Sendezeitoptimierung verwendet, erhalten jedoch letztendlich eine Nachricht und haben die Möglichkeit, mit einer Nachricht zu interagieren. Darüber hinaus verwendet dieses Modell keine demografischen Benutzerdaten oder Proxys für demografische Daten, sondern nur Daten zum Benutzerverhalten und zur Zeitzone. Daher sind ethische Bedenken begrenzt und werden abgeschwächt.
