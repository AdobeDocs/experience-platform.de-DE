---
keywords: Experience Platform;Home;Data Science Workspace;beliebte Themen;Date Science Workspace;Data Science
solution: Experience Platform
title: Data Science Workspace – Übersicht
description: Dieser Leitfaden bietet eine Übersicht über die wichtigsten Konzepte im Zusammenhang mit Data Science Workspace in Adobe Experience Platform.
exl-id: bef25073-0dfb-453d-8c32-7f44d917d62d
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: ht
source-wordcount: '2388'
ht-degree: 100%

---

# Data Science Workspace – Übersicht

Adobe Experience Platform [!DNL Data Science Workspace] nutzt maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. [!DNL Data Science Workspace] ist in Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen auf der Basis Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen.

Datenwissenschaftler aller Qualifikationsstufen verfügen hier über ausgereifte, benutzerfreundliche Tools, die eine schnelle Entwicklung, Schulung und Abstimmung von Rezepten für maschinelles Lernen unterstützen – all die Vorteile der KI-Technologie, aber ohne deren Komplexität.

Mit [!DNL Data Science Workspace] können Datenwissenschaftler auf einfache Weise APIs für Intelligent Services erstellen – angetrieben durch maschinelles Lernen. Diese Services können mit anderen Adobe-Services wie Adobe Target und Adobe Analytics Cloud kombiniert werden, um Ihnen bei der Automatisierung personalisierter, gezielter digitaler Erlebnisse in Web-, Desktop- und Mobile Apps zu helfen.

Dieses Handbuch bietet einen Überblick über die wichtigsten Konzepte im Zusammenhang mit [!DNL Data Science Workspace].

## Einführung

Heute legt ein Unternehmen großen Wert auf die Erfassung von Big Data für Prognosen und Einblicke, die es ihm ermöglichen, Kundenerlebnisse zu personalisieren und den Kunden – sowie dem Unternehmen – einen Mehrwert zu liefern.
So wichtig dies auch ist, der Weg von den Daten zu den Erkenntnissen kann mit hohen Kosten verbunden sein. Es erfordert in der Regel qualifizierte Datenwissenschaftler, die intensive und zeitaufwendige Datenforschung betreiben, um Modelle für maschinelles Lernen oder Rezepte zu entwickeln, die Intelligent Services unterstützen. Der Prozess ist langwierig, die Technologie komplex, und qualifizierte Datenwissenschaftler sind möglicherweise schwer zu finden.

Mit [!DNL Data Science Workspace] ermöglicht Ihnen Adobe Experience Platform, erlebnisorientierte KI im gesamten Unternehmen zu implementieren, indem die Prozesse von Daten zu Erkenntnissen zu Code optimiert und beschleunigt werden mit:
- Ein Framework für maschinelles Lernen und Laufzeit
- Integrierter Zugriff auf Ihre in Adobe Experience Platform gespeicherten Daten
- Ein auf [!DNL Experience Data Model] (XDM) erstelltes einheitliches Schema für Daten
- Die notwendige Rechenleistung für maschinelles Lernen/KI und die Verwaltung großer Datensätze
- Vorgefertigte Rezepte für maschinelles Lernen, um den Einstieg in KI-gesteuerte Erlebnisse zu beschleunigen
- Vereinfachtes Authoring, Wiederverwendung und Modifizierung von Rezepten für Datenwissenschaftler mit unterschiedlichem Kenntnisstand
- Intelligente Veröffentlichung und Freigabe von Services in nur wenigen Klicks – ohne Entwickler – sowie Überwachung und Nachschulung zur kontinuierlichen Optimierung personalisierter Kundenerlebnisse

Datenwissenschaftler aller Qualifikationsstufen werden so schneller und effektiver digitale Erfahrungen erzielen.

## Erste Schritte

Bevor wir in die Details von [!DNL Data Science Workspace] eintauchen, hier eine kurze Zusammenfassung der Schlüsselbegriffe:

| Begriff | Definition |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] innerhalb von [!DNL Experience Platform] ermöglicht Kunden, maschinelle Lernmodelle zu erstellen, die Daten aus verschiedenen Lösungen von [!DNL Experience Platform] und Adobe verwenden, um intelligente Einblicke und Prognosen zu generieren und ansprechende digitale Erlebnisse für Endbenutzer zu entwickeln. |
| Künstliche Intelligenz | Künstliche Intelligenz befasst sich mit der Theorie und Entwicklung von Computersystemen, die in der Lage sind, Aufgaben auszuführen, die normalerweise menschliche Intelligenz erfordern, wie visuelle Wahrnehmung, Spracherkennung, Entscheidungsfindung und Übersetzung zwischen Sprachen. |
| Maschinelles Lernen | Maschinelles Lernen ist der Studienbereich, der es Computern ermöglicht zu lernen, ohne explizit programmiert zu werden. |
| [!DNL Sensei] ML Framework | [!DNL Sensei] ML Framework ist ein einheitlicher Rahmen für maschinelles Lernen überall bei Adobe, das Daten auf [!DNL Experience Platform] nutzt, um Datenwissenschaftler bei der Entwicklung maschinenlerngestützter Intelligenz-Services schneller, skalierbar und wiederverwendbar zu unterstützen. |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM) von Adobe führt zur Definition von Standardschemas wie [!DNL Profile] und [!DNL ExperienceEvent] für Customer Experience Management. |
| [!DNL JupyterLab] | [!DNL JupyterLab] ist eine Web-basierte Open-Source-Schnittstelle für Project Jupyter und ist eng in [!DNL Experience Platform] integriert. |
| Rezepte | Ein „Rezept“ ist ein von Adobe verwendeter Begriff für eine Modellspezifikation. Es handelt sich dabei um einen Container auf oberster Ebene, der einen bestimmten Algorithmus für maschinelles Lernen, einen KI-Algorithmus oder eine Gruppe von Algorithmen, eine Verarbeitungslogik und eine Konfiguration darstellt, die für die Einrichtung und Ausführung eines trainierten Modells und somit zur Lösung spezifischer geschäftlicher Herausforderungen erforderlich sind. |
| Modell | Ein Modell ist eine Instanz eines Rezepts für maschinelles Lernen, das mithilfe von historischen Daten und Konfigurationen dazu trainiert wird, eine geschäftliche Fragestellung zu lösen. |
| Training | Ein Training besteht aus dem Erlernen von Mustern und Insights auf Grundlage gekennzeichneter Daten. |
| Schulungsmodell | Ein trainiertes Modell stellt die ausführbare Ausgabe eines Modellschulungsprozesses dar, bei dem eine Reihe von Trainings-Daten auf die Modellinstanz angewendet wurde. Ein trainiertes Modell behält einen Verweis auf jeden intelligenten Web-Service bei, der daraus erstellt wird. Das trainierte Modell eignet sich für die Bewertung und Erstellung eines intelligenten Web-Services. Änderungen an einem trainierten Modell können als neue Version nachverfolgt werden. |
| Scoring | Beim Scoring werden mithilfe eines trainierten Modells Insights aus Daten generiert. |
| Service | Ein bereitgestellter Service stellt Funktionen einer künstlichen Intelligenz, eines maschinellen Lernmodells oder eines erweiterten Algorithmus über eine API zur Verfügung, sodass sie von anderen Services oder Programmen genutzt werden können, um intelligente Apps zu erstellen. |

Das folgende Diagramm zeigt die hierarchische Beziehung zwischen Rezepten, Modellen, Schulungsübungen und Bewertungsläufen.

![](./images/home/recipe_hiearchy_ui.png)

## Grundlagen zu [!DNL Data Science Workspace]

Mit [!DNL Data Science Workspace] können Ihre Datenwissenschaftler den umständlichen Prozess des Ziehens von Erkenntnissen aus großen Datensätzen optimieren. Die auf einem gemeinsamen maschinellen Lern-Framework und der Laufzeitumgebung aufbauende Funktion [!DNL Data Science Workspace] bietet erweiterte Workflow-Verwaltung, Modellverwaltung und Skalierbarkeit. Intelligent Services unterstützt die Wiederverwendung von maschinellen Lernrezepten, was einer Vielzahl von Programmen zugutekommt, die mithilfe von Adobe-Produkten und -Lösungen erstellt werden.

### Datenzugriff aus einer Hand

Daten sind der Eckpfeiler von KI und maschinellem Lernen.

[!DNL Data Science Workspace] ist vollständig in Adobe Experience Platform integriert, einschließlich Data Lake, [!DNL Real-Time Customer Profile] und [!DNL Unified Edge]. Entdecken Sie alle in Adobe Experience Platform gespeicherten Organisationsdaten zusammen mit gemeinsamen Big Data- und Deep Learning-Bibliotheken wie [!DNL Spark] ML und [!DNL TensorFlow]. Wenn Sie nicht finden, was Sie benötigen, nehmen Sie Ihre eigenen Datensätze mit dem XDM-standardisierten Schema auf.

### Vorgefertigte Rezepte für maschinelles Lernen

[!DNL Data Science Workspace] umfasst vorgefertigte Rezepte für maschinelles Lernen für gängige Geschäftsanforderungen, z. B. Prognosen zum Einzelhandel und Anomalieerkennung, sodass Datenwissenschaftler und Entwickler nicht bei Null anfangen müssen. Derzeit werden drei Rezepte angeboten: [Produktkaufprognosen](./pre-built-recipes/product-purchase-prediction.md), [Produktempfehlungen](./pre-built-recipes/product-recommendations.md) und [Einzelhandelsverkäufe](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

Wenn Sie es bevorzugen, können Sie ein vorgefertigtes Rezept an Ihre Anforderungen anpassen, ein Rezept importieren oder ein benutzerdefiniertes Rezept von Grund auf neu erstellen. Wie auch immer Sie beginnen, sobald Sie ein Rezept trainiert und überarbeitet haben, ist für die Erstellung eines benutzerdefinierten intelligenten Service kein Entwickler erforderlich – nur ein paar Klicks und Sie sind bereit, ein zielgerichtetes, personalisiertes digitales Erlebnis zu erstellen.

### Workflow, der auf den Datenwissenschaftler ausgerichtet ist

[!DNL Data Science Workspace] hilft Ihnen unabhängig von Ihrem Kenntnisstand in der Datenwissenschaft, den Prozess der Suche nach Einblicken in Daten zu vereinfachen und zu beschleunigen und diese Einblicke auf digitale Erlebnisse anzuwenden.

### Datenforschung

Die richtigen Daten zu finden und sie vorzubereiten, ist der arbeitsintensivste Teil des Aufbaus eines effektiven Rezeptes. [!DNL Data Science Workspace] und Adobe Experience Platform helfen Ihnen, schneller von Daten zu Einblicken zu gelangen.

Unter Adobe Experience Platform werden Ihre Daten über verschiedene Kanäle hinweg zentralisiert und im standardisierten XDM-Schema gespeichert, sodass sie leichter zu finden, zu verstehen und zu bereinigen sind. Ein einziger Datenspeicher auf der Grundlage eines gemeinsamen Schemas kann Ihnen unzählige Stunden an Datenforschung und -vorbereitung ersparen.

Verwenden Sie beim Durchsuchen R, [!DNL Python] oder Scala mit dem integrierten gehosteten [!DNL Jupyter Notebook], um den Datenkatalog in [!DNL Platform] zu durchsuchen. Mit einer dieser Sprachen können Sie auch die Vorteile von [!DNL Spark] ML und TensorFlow nutzen. Beginnen Sie von Grund auf oder verwenden Sie eine der bereitgestellten Notebook-Vorlagen für spezifische geschäftliche Herausforderungen.

Im Rahmen des Workflows für die Datenforschung können Sie auch neue Daten aufnehmen oder vorhandene Funktionen zur Hilfe bei der Datenvorbereitung verwenden.

### Authoring

Mit [!DNL Data Science Workspace] entscheiden Sie, wie Sie Rezepte erstellen möchten.

- Sparen Sie Zeit, indem Sie nach einem vorgefertigten Rezept suchen, das Ihren geschäftlichen Anforderungen entspricht und das Sie nach Bedarf verwenden oder konfigurieren können, damit es Ihre spezifischen Anforderungen erfüllt.
- Erstellen Sie ein Rezept von Grund auf neu, indem Sie die Authoring-Runtime in Jupyter Notebook verwenden, um das Rezept zu entwickeln und zu registrieren.
- Laden Sie ein außerhalb von Adobe Experience Platform erstelltes Rezept in [!DNL Data Science Workspace] hoch oder importieren Sie Rezept-Code aus einem Repository, z. B. [!DNL Git], mit der zwischen [!DNL Git] und [!DNL Data Science Workspace] verfügbaren Authentifizierung und Integration.

### Experimentieren

Data Science Workspace bietet eine enorme Flexibilität beim Experimentieren. Beginnen Sie mit Ihrem Rezept. Erstellen Sie dann eine separate Instanz, indem Sie denselben Kernalgorithmus zusammen mit eindeutigen Merkmalen wie etwa Hypertuning-Parametern verwenden. Sie können so viele Instanzen erstellen, wie Sie benötigen, und jede Instanz so oft trainieren und bewerten, wie Sie möchten. Auf der Basis des Trainings verfolgt [!DNL Data Science Workspace] Rezepte, Rezeptinstanzen und trainierte Instanzen zusammen mit Auswertungsmetriken, sodass Sie es nicht selbst tun müssen.

### Operationalisierung

Wenn Sie mit Ihrem Rezept zufrieden sind, brauchen Sie nur ein paar Klicks, um einen intelligenten Service zu erstellen. Keine Codierung erforderlich – Sie können es selbst machen, ohne einen Entwickler oder Ingenieur hinzuzuziehen. Veröffentlichen Sie den intelligenten Service schließlich auf Adobe IO. Er ist für Ihr Team für digitale Erlebnisse nutzbar.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Kontinuierliche Verbesserung

[!DNL Data Science Workspace] verfolgt, wo intelligente Services aufgerufen werden und wie sie funktionieren. Wenn Daten eingehen, können Sie die Genauigkeit intelligenter Services bewerten, um den Kreis zu schließen, und die Rezepte bei Bedarf neu trainieren, um die Leistung zu verbessern. Das Ergebnis ist eine kontinuierliche Verfeinerung der Präzision der Kundenpersonalisierung.

### Zugriff auf neue Funktionen und Datensätze

Datenwissenschaftler können neue Technologien und Datensätze nutzen, sobald sie über Adobe-Services verfügbar sind. Durch häufige Aktualisierungen integrieren wir Datensätze und Technologien in die Plattform, sodass nicht Sie es müssen.

### Sicherheit und Sorgenfreiheit

Die Sicherung Ihrer Daten ist eine der obersten Prioritäten für Adobe. Adobe schützt Ihre Daten mit Sicherheitsprozessen und -kontrollen, die zur Einhaltung branchenüblicher Normen, Vorschriften und Zertifizierungen entwickelt wurden.

Die Sicherheit ist in Software und Services als Teil des Adobe Secure Product Lifecycle integriert.
Weitere Informationen zur Daten- und Software-Sicherheit bei Adobe, zu Compliance und mehr finden Sie auf der Sicherheitsseite unter https://www.adobe.com/de/security.html.

## [!DNL Data Science Workspace] in Aktion

Prognosen und Einblicke liefern die Informationen, die Sie benötigen, um jedem Kunden, der Ihre Website besucht, Ihr Callcenter kontaktiert oder andere digitale Erlebnisse nutzt, ein hoch personalisiertes Erlebnis zu bieten. So funktioniert Ihre tägliche Arbeit mit [!DNL Data Science Workspace].

### Problem definieren

Alles fängt mit einer geschäftlichen Herausforderung an. Ein Online-Callcenter benötigt beispielsweise Kontext, um ein negatives Kundengefühl in ein positives umwandeln zu können.

Es gibt viele Daten über den Kunden. Er hat z. B. die Site durchsucht, Artikel in seinen Warenkorb gelegt und sogar Bestellungen aufgegeben. Möglicherweise hat er E-Mails erhalten, Coupons verwendet oder das Callcenter schon zuvor kontaktiert. Das Rezept muss dann die verfügbaren Daten über den Kunden und seine Aktivitäten verwenden, um dessen Kaufneigung zu bestimmen und ihm ein Angebot zu unterbreiten, das der Kunde mit hoher Wahrscheinlichkeit schätzen und wahrnehmen wird.

![](./images/home/example_problem.png)

Zum Zeitpunkt des Kontakts mit dem Callcenter hat der Kunde noch zwei Paar Schuhe im Warenkorb, aber ein Hemd wieder entfernt. Mit diesen Informationen kann der Intelligent Service dem Callcenter-Agenten empfehlen, während des Anrufs einen Coupon für 20 % Rabatt auf Schuhe anzubieten. Wenn der Kunde den Coupon verwendet, werden diese Informationen dem Datensatz hinzugefügt und die Prognosen werden beim nächsten Anruf des Kunden sogar noch besser.

### Daten untersuchen und vorbereiten

Basierend auf der definierten geschäftlichen Herausforderung wissen Sie, dass das Rezept alle Web-Transaktionen des Kunden berücksichtigen sollte, einschließlich Site-Besuche, Suchvorgänge, Seitenaufrufe, angeklickte Links, Warenkorbaktionen, erhaltene Angebote, erhaltene E-Mails, Interaktionen mit dem Callcenter usw.

Ein Datenwissenschaftler verbringt in der Regel bis zu 75 % der Zeit, die für die Erstellung eines Rezepts benötigt wird, damit, die Daten zu erforschen und zu transformieren. Daten stammen oft aus mehreren Repositorys und werden in verschiedenen Schemas gespeichert – so müssen sie kombiniert und zugeordnet werden, bevor sie zur Erstellung eines Rezepts verwendet werden können.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

Wenn Sie von Grund auf neu beginnen oder ein vorhandenes Rezept konfigurieren, beginnen Sie mit der Datensuche in einem zentralisierten und standardisierten Datenkatalog für Ihr Unternehmen, was die Jagd erheblich vereinfacht. Möglicherweise stellen Sie sogar fest, dass ein anderer Datenwissenschaftler in Ihrer Organisation bereits einen ähnlichen Datensatz identifiziert hat, und entscheiden sich für eine Feinabstimmung dieses Datensatzes, anstatt von Grund auf neu zu beginnen.
Sämtliche Daten in Adobe Experience Platform entsprechen einem standardisierten XDM-Schema, sodass kein komplexes Modell für die Datenzusammenführung erstellt werden muss oder die Hilfe eines Dateningenieurs benötigt wird.

Wenn Sie die benötigten Daten nicht sofort finden, sie aber außerhalb von Adobe Experience Platform schon existieren, ist es eine relativ einfache Aufgabe, zusätzliche Datensätze aufzunehmen, die sich auch in das standardisierte XDM-Schema umwandeln lassen.\
Sie können [!DNL Jupyter Notebook] verwenden, um die Vorverarbeitung von Daten zu vereinfachen – möglicherweise beginnend mit einer Notebook-Vorlage oder einem Notebook, das Sie zuvor zur Ermittlung der Kauftendenz verwendet haben.

![](./images/home/notebook_templates-new.png)

### Rezept erstellen

Wenn Sie bereits ein Rezept gefunden haben, das allen Ihren Anforderungen entspricht, können Sie mit dem Experimentieren fortfahren. Oder Sie können das Rezept ein wenig ändern oder eines von Grund auf neu erstellen – unter Nutzung der Authoring-Laufzeit von [!DNL Data Science Workspace] in [!DNL Jupyter Notebook]. Die Verwendung der Authoring-Laufzeit stellt sicher, dass Sie sowohl den Schulungs- und Bewertungs-Workflow von [!DNL Data Science Workspace] verwenden als auch das Rezept später konvertieren können, damit es von anderen Mitgliedern Ihres Unternehmens gespeichert und wiederverwendet werden kann.

Sie können auch ein Rezept in [!DNL Data Science Workspace] importieren und die Experimentier-Workflows nutzen, um Ihren Intelligent Service zu erstellen.

### Mit dem Rezept experimentieren

Mit einem Rezept, das Ihre wichtigsten Algorithmen für maschinelles Lernen enthält, können viele Rezeptinstanzen mit einem einzigen Rezept erstellt werden. Diese Rezeptinstanzen werden als Modelle bezeichnet. Ein Modell erfordert Training und Auswertung, um seine Effizienz und Wirksamkeit zu optimieren, ein Prozess, der in der Regel aus Versuch und Irrtum besteht.

![](./images/home/recipe_hiearchy_ui.png)

Während Sie Ihre Modelle trainieren, werden Trainings-Läufe und Auswertungen generiert. [!DNL Data Science Workspace] erfasst die Evaluierungsmetriken für jedes einzelne Modell und dessen Trainings-Läufe. Mithilfe von Testmetriken, die durch Experimente generiert wurden, können Sie den Trainings-Lauf ermitteln, der am effektivsten ist.

![](./images/home/evaluation_metrics.png)

Sehen Sie sich das Tutorial zu [API](./models-recipes/train-evaluate-model-api.md) oder [UI](./models-recipes/train-evaluate-model-ui.md) an, um zu erfahren, wie Sie Modelle in [!DNL Data Science Workspace] trainieren und auswerten können.

### Operationalisieren des Modells

Wenn Sie das am besten trainierte Rezept für Ihre geschäftlichen Anforderungen ausgewählt haben, können Sie einen Intelligent Service in [!DNL Data Science Workspace] ohne Unterstützung durch einen Entwickler erstellen. Sie brauchen dazu nur ein paar Klicks – keine Codierung erforderlich. Ein veröffentlichter Intelligent Service steht anderen Mitgliedern Ihrer Organisation zur Verfügung, ohne dass das Modell neu erstellt werden muss.

Ein veröffentlichter Intelligent Service ist so konfigurierbar, dass er sich von Zeit zu Zeit selbst mit neuen Daten trainiert, sobald diese verfügbar werden. Dadurch wird sichergestellt, dass Ihr Service im Laufe der Zeit seine Effizienz und Wirksamkeit beibehält.

## Nächste Schritte

[!DNL Data Science Workspace] hilft bei der Straffung und Vereinfachung des Workflows in der Datenwissenschaft, von der Datenerfassung über Algorithmen bis hin zu Intelligent Services für Datenwissenschaftler aller Qualifikationsstufen. Mit den ausgereiften Tools, die [!DNL Data Science Workspace] bietet, können Sie die Zeit von den puren Daten bis hin zu Erkenntnissen erheblich verkürzen.

Noch wichtiger ist, dass [!DNL Data Science Workspace] die Datenwissenschaft und die algorithmische Optimierung der führenden Marketing-Plattform von Adobe in die Hände von Unternehmensdatenwissenschaftlern legt. Zum ersten Mal können Unternehmen eigene Algorithmen in die Plattform einbringen und so die leistungsstarken Adobe-Funktionen für maschinelles Lernen und KI nutzen, um hochgradig personalisierte Kundenerlebnisse in großem Umfang bereitzustellen.

Durch die Verbindung von Markenwissen mit dem maschinellen Lernen und den KI-Fähigkeiten von Adobe können Unternehmen den Geschäftswert und die Markentreue steigern, indem sie ihren Kunden das geben, was sie wollen, schon bevor sie danach fragen.

Weitere Informationen, z. B. einen kompletten täglichen Workflow, finden Sie in der Dokumentation [Übersicht über den Data Science Workspace](./walkthrough.md).

## Zusätzliche Ressourcen

Das folgende Video wurde entwickelt, um Ihr Verständnis von [!DNL Data Science Workspace] zu unterstützen.

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)