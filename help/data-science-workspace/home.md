---
keywords: Experience Platform;home;Data Science Workspace;popular topics
solution: Experience Platform
title: Übersicht über den Data Science Workspace
topic: overview
translation-type: tm+mt
source-git-commit: e08460bc76d79920bbc12c7665a1416d69993f34
workflow-type: tm+mt
source-wordcount: '2736'
ht-degree: 0%

---


# Übersicht über den Data Science Workspace

Der Data Science Workspace der Adobe Experience Platform nutzt maschinelles Lernen und künstliche Intelligenz, um Erkenntnisse aus Ihren Daten zu gewinnen. Der Data Science Workspace ist in die Adobe Experience Platform integriert und hilft Ihnen bei der Erstellung von Prognosen mithilfe Ihrer Inhalts- und Datenelemente in allen Adobe-Lösungen.

Datenwissenschaftler aller Qualifikationsstufen finden ausgereifte, einfach zu bedienende Werkzeuge, die die schnelle Entwicklung, Ausbildung und Abstimmung von maschinellen Lernrezepten unterstützen - all die Vorteile der AI-Technologie, ohne die Komplexität.

Mit Data Science Workspace können Datenwissenschaftler auf einfache Weise intelligente Services-APIs erstellen - basierend auf maschinellem Lernen. Diese Dienste funktionieren mit anderen Adobe-Diensten, einschließlich Adobe Zielgruppe und Adobe Analytics Cloud, um Ihnen bei der Automatisierung personalisierter, zielgerichteter digitaler Erlebnisse in Web-, Desktop- und mobilen Apps zu helfen.

Dieser Leitfaden bietet einen Überblick über die wichtigsten Konzepte im Zusammenhang mit Data Science Workspace.

## Einführung

Das heutige Unternehmen legt großen Wert auf die Erfassung von Big Data für Prognosen und Einblicke, die es ihnen ermöglichen, Kundenerlebnisse zu personalisieren und Kunden - und Unternehmen - mehr Wert zu verschaffen.
So wichtig es auch ist, dass es zu hohen Kosten kommen kann, von Daten zu Erkenntnissen zu gelangen. Es erfordert in der Regel qualifizierte Datenwissenschaftler, die intensive und zeitaufwendige Datenforschung betreiben, um Modelle für maschinelles Lernen oder Rezepte zu entwickeln, die intelligente Dienste unterstützen. Der Prozess ist langwierig, die Technologie ist komplex und qualifizierte Datenwissenschaftler können schwer zu finden sein.

Mit dem Data Science Workspace können Sie mit der Adobe Experience Platform unternehmensweit erlebnisorientierte KI nutzen, um Daten-zu-Einblick-Codes zu optimieren und zu beschleunigen mit:
- Ein Framework für maschinelles Lernen und Laufzeit
- Integrierter Zugriff auf Ihre in Adobe Experience Platform gespeicherten Daten
- Ein auf dem Experience Data Model (XDM) basierendes einheitliches Datenmodell
- Die Rechenleistung ist unverzichtbar für maschinelles Lernen/AI und die Verwaltung von Big DataSets
- Vorgefertigte maschinelle Lernrezepte zur Beschleunigung des Abstiegs in durch AI angetriebene Erlebnisse
- Vereinfachtes Authoring, Wiederverwendung und Modifizierung von Rezepten für Datenwissenschaftler mit unterschiedlichem Kenntnisstand
- Intelligente Veröffentlichung und Freigabe von Diensten in nur wenigen Klicks - ohne Entwickler - sowie Überwachung und Umschulung zur kontinuierlichen Optimierung personalisierter Kundenerlebnisse

Datenwissenschaftler aller Qualifikationsstufen werden schneller und effektivere digitale Erfahrungen erzielen.

## Erste Schritte

Bevor Sie sich mit den Details des Data Science Workspace vertraut machen, hier eine kurze Zusammenfassung der Schlüsselbegriffe:

| Begriff | Definition |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Data Science-Arbeitsbereich | Mit Data Science Workspace innerhalb der Experience Platform können Kunden Modelle für maschinelles Lernen erstellen, die Daten über Experience Platform und Adobe-Lösungen hinweg nutzen, um intelligente Einblicke und Prognosen zu generieren, um ansprechende digitale Erfahrungen für Endbenutzer zu entwickeln. |
| Künstliche Intelligenz | Künstliche Intelligenz ist eine Theorie und Entwicklung von Computersystemen, die in der Lage sind, Aufgaben auszuführen, die normalerweise menschliche Intelligenz erfordern, wie visuelle Wahrnehmung, Spracherkennung, Entscheidungsfindung und Übersetzung zwischen Sprachen. |
| Maschinelles Lernen | Maschinelles Lernen ist der Studienbereich, der es Computern ermöglicht, zu lernen, ohne explizit programmiert zu werden. |
| Sensei-ML-Framework | Sensei ML Framework ist ein einheitliches Framework für maschinelles Lernen in Adobe, das Daten über Experience Platform nutzt, um Datenwissenschaftler bei der Entwicklung von intelligenten Diensten mit maschinellem Lernen schneller, skalierbar und wiederverwendbar zu unterstützen. |
| Erlebnisdatenmodell | Das Experience Data Model (XDM) ist der Standardisierungsaufwand, den Adobe zur Definition von Standard-Schemas wie Profil und ExperienceEvent für Customer Experience Management führt. |
| JupyterLab | JupyterLab ist eine webbasierte Open-Source-Schnittstelle für Project Jupyter und ist eng in Experience Platform integriert. |
| Rezepte | Ein Rezept ist der von Adobe verwendete Begriff für eine Modellspezifikation. Es handelt sich dabei um einen Container auf oberster Ebene, der ein bestimmtes maschinelles Lernen, einen AI-Algorithmus oder ein Ensemble von Algorithmen, eine Verarbeitungslogik und eine Konfiguration darstellt, die erforderlich sind, um ein geschultes Modell zu erstellen und auszuführen und damit zur Lösung spezifischer Geschäftsprobleme beizutragen. |
| Modell | Ein Modell ist ein Beispiel für ein maschinelles Lernrezept, das mithilfe von historischen Daten und Konfigurationen für die Lösung eines Geschäftsfalls trainiert wird. |
| Schulung | Schulung ist der Prozess des Lernens von Mustern und Erkenntnissen aus gekennzeichneten Daten. |
| Auszubildendes Modell | Ein trainiertes Modell stellt die ausführbare Ausgabe eines Modellschulungsprozesses dar, bei dem eine Reihe von Schulungsdaten auf die Modellinstanz angewendet wurde. Ein ausgebildetes Modell behält einen Verweis auf alle intelligenten Webdienste bei, die daraus erstellt werden. Das geschulte Modell eignet sich für die Bewertung und Erstellung eines intelligenten Webdiensts. Änderungen an einem geschulten Modell können als neue Version nachverfolgt werden. |
| Bewertung | Die Auswertung ist der Prozess, bei dem mithilfe eines geschulten Modells Erkenntnisse aus Daten generiert werden. |
| Service | Ein bereitgestellter Dienst stellt Funktionen einer künstlichen Intelligenz, eines maschinellen Lernmodells oder eines erweiterten Algorithmus über eine API zur Verfügung, sodass sie von anderen Diensten oder Anwendungen genutzt werden können, um intelligente Apps zu erstellen. |

Das folgende Diagramm zeigt die hierarchische Beziehung zwischen Rezepten, Modellen, Schulungsübungen und Bewertungsläufen.

![](./images/home/recipe_hiearchy_ui.png)

## Der Arbeitsbereich &quot;Datenwissenschaften&quot;

Mit Data Science Workspace können Ihre Datenwissenschaftler den umständlichen Prozess der Ermittlung von Einblicken in große Datensätze optimieren. Data Science Workspace basiert auf einem gemeinsamen Framework für maschinelles Lernen und einer Laufzeit und bietet erweiterte Workflow-Verwaltung, Modellverwaltung und Skalierbarkeit. Intelligente Dienste unterstützen die Wiederverwendung von Rezepten für maschinelles Lernen, um eine Vielzahl von Anwendungen zu entwickeln, die mit Adobe-Produkten und -Lösungen erstellt wurden.

### Datenzugriff aus einer Hand

Daten sind der Eckpfeiler von KI und maschinellem Lernen.

Data Science Workspace ist vollständig in die Adobe Experience Platform integriert, einschließlich Data Lake, Real-time Customer Profil und Unified Edge. Entdecken Sie alle Unternehmensdaten, die Sie in Adobe Experience Platform gespeichert haben, zusammen mit gemeinsamen Big Data- und Deep-Learning-Bibliotheken wie Spark ML und TensorFlow. Wenn Sie nicht finden, was Sie benötigen, erfassen Sie Ihre eigenen Datensätze mit dem XDM-standardisierten Schema.

### Vorgefertigte maschinelle Lernrezepte

Data Science Workspace umfasst vorgefertigte maschinelle Lernrezepte für gängige Geschäftsanforderungen, wie z. B. Prognosen zum Einzelhandel und Anomalieerkennung, sodass Datenwissenschaftler und Entwickler nicht von Grund auf Beginn benötigen. Derzeit werden drei Rezepte angeboten: [Produktkaufprognosen](./pre-built-recipes/product-purchase-prediction.md), [Produktempfehlungen](./pre-built-recipes/product-recommendations.md)und [Einzelhandelsverkäufe](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

Wenn Sie es bevorzugen, können Sie ein vorgefertigtes Rezept an Ihre Anforderungen anpassen, ein Rezept importieren oder einen Beginn von Grund auf neu erstellen, um ein benutzerdefiniertes Rezept zu erstellen. Sobald Sie jedoch ein Rezept trainieren und überarbeiten, ist für die Erstellung eines benutzerdefinierten intelligenten Dienstes kein Entwickler erforderlich - nur ein paar Klicks und Sie sind bereit, ein zielgerichtetes, personalisiertes digitales Erlebnis zu entwickeln.

### Arbeitsablauf, der auf den Datenwissenschaftler ausgerichtet ist

Unabhängig vom Kenntnisstand in der Datenwissenschaft hilft Data Science Workspace bei der Vereinfachung und Beschleunigung des Prozesses der Suche nach Einblicken in Daten und deren Anwendung auf digitale Erfahrungen.

### Datenforschung

Die richtigen Daten zu finden und sie vorzubereiten, ist der arbeitsintensivste Teil des Aufbaus eines effektiven Rezeptes. Data Science Workspace und Adobe Experience Platform helfen Ihnen, schneller von Daten zu Einblicken zu gelangen.

Auf der Adobe Experience Platform werden Ihre Daten über mehrere Kanal zentralisiert und im standardisierten XDM-Schema gespeichert, sodass Daten leichter zu finden, zu verstehen und zu bereinigen sind. Ein Datenspeicher auf der Grundlage eines gemeinsamen Schemas kann Ihnen unzählige Stunden an Datenforschung und -vorbereitung ersparen.

Verwenden Sie während des Browsens R, Python oder Scala mit dem integrierten, gehosteten Jupyter-Notebook, um den Datenkatalog auf der Plattform zu durchsuchen. Mit einer dieser Sprachen können Sie auch Spark ML und TensorFlow nutzen. Beginn von Grund auf, oder verwenden Sie eine der Notebook-Vorlagen für spezifische Geschäftsprobleme.

Im Rahmen des Arbeitsablaufs für die Datenforschung können Sie auch neue Daten erfassen oder vorhandene Funktionen zur Datenvorbereitung verwenden.

### Authoring – 

Mit Data Science Workspace entscheiden Sie, wie Sie Rezepte erstellen möchten.

- Sparen Sie Zeit, indem Sie nach einem vorgefertigten Rezept suchen, das Ihren geschäftlichen Anforderungen entspricht und das Sie nach Bedarf verwenden oder konfigurieren können, um Ihre spezifischen Anforderungen zu erfüllen.
- Erstellen Sie ein Rezept von Grund auf neu, indem Sie die Authoring-Laufzeit in Jupyter Notebook verwenden, um das Rezept zu entwickeln und zu registrieren.
- Laden Sie ein außerhalb von Adobe Experience Platform erstelltes Rezept in den Data Science Workspace hoch oder importieren Sie den Rezepturcode aus einem Repository, z. B. Git, mit der zwischen Git und Data Science Workspace verfügbaren Authentifizierung und Integration.

### Experimentieren

Data Science Workspace bietet eine enorme Flexibilität beim Experimentieren. Beginn mit Ihrem Rezept. Erstellen Sie dann eine separate Instanz, indem Sie denselben Core-Algorithmus mit eindeutigen Merkmalen wie Hypertuning-Parameter verwenden. Sie können so viele Instanzen erstellen, wie Sie benötigen, und jede Instanz so oft trainieren und bewerten, wie Sie möchten. Während Sie sie trainieren, verfolgt Data Science Workspace Rezepte, Rezept-Instanzen und geschulte Instanzen zusammen mit Evaluierungsmetriken, sodass Sie nicht müssen.

### Operationalisierung

Wenn Sie mit Ihrem Rezept zufrieden sind, ist es nur ein paar Klicks, einen intelligenten Dienst zu schaffen. Keine Programmierung erforderlich - Sie können es selbst machen, ohne einen Entwickler oder Ingenieur zu benennen. Veröffentlichen Sie den intelligenten Dienst schließlich bei Adobe IO, damit Ihr Digital Experience Team ihn nutzen kann.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Kontinuierliche Verbesserung

Data Science Workspace verfolgt, wo intelligente Dienste aufgerufen werden und wie sie funktionieren. Wenn Daten eingehen, können Sie die Genauigkeit intelligenter Dienste bewerten, um die Schleife zu schließen, und die Rezepte nach Bedarf neu ausbilden, um die Leistung zu verbessern. Das Ergebnis ist eine kontinuierliche Verfeinerung der Präzision der Kundenpersonalisierung.

### Zugriff auf neue Funktionen und Datensätze

Datenwissenschaftler können neue Technologien und Datensätze nutzen, sobald sie über Adobe-Dienste verfügbar sind. Durch häufige Aktualisierungen machen wir die Arbeit, Datasets und Technologien in die Plattform zu integrieren, sodass Sie nicht müssen.

### Zugriffskontrolle im Arbeitsbereich für Datenwissenschaften

Access control for Experience Platform is administered through the [Adobe Admin Console](https://adminconsole.adobe.com). Diese Funktion nutzt die Profil der Produkte in der Admin-Konsole, die Benutzer mit Berechtigungen und Sandboxen verknüpfen. See the [access control overview](../access-control/home.md) for more information.

>[!IMPORTANT] Um Data Science Workspace verwenden zu können, muss die Berechtigung &quot;Data Science Workspace verwalten&quot;aktiviert sein.

Die folgende Tabelle zeigt die Auswirkungen, die eine Aktivierung oder Deaktivierung dieser Berechtigung hat:

| Berechtigung | Aktiviert | Deaktiviert |
|---|---|---|
| Data Science Workspace | Bietet Zugriff auf alle Dienste im Data Science Workspace. | API- und UI-Zugriff auf alle Dienste in Data Science Workspace sind deaktiviert. Bei Deaktivierung wird Routing zu den Data Science Workspace- *Modellen* und - *Services* verhindert. |

### Sicherheit und Seelenfrieden

Die Sicherung Ihrer Daten ist eine der obersten Prioritäten von Adobe. Adobe schützt Ihre Daten durch Sicherheitsprozesse und Steuerelemente, die entwickelt wurden, um branchenübliche Standards, Vorschriften und Zertifizierungen einzuhalten.

Sicherheit ist Teil des sicheren Produktlebenszyklus von Adobe und ist in Software und Services integriert.
Weitere Informationen zu Adobe-Daten und -Software-Sicherheit, -Compliance und mehr finden Sie auf der Seite &quot;Sicherheit&quot;unter https://www.adobe.com/security.html.

### Sandbox-Unterstützung

Sandboxen sind virtuelle Partitionen innerhalb einer Instanz von Experience Platform. Jede Plattforminstanz unterstützt eine Produktions-Sandbox und mehrere Nicht-Produktions-Sandboxen, wobei jede eine eigene Bibliothek mit Plattformressourcen unterhält. Mit Sandboxen ohne Produktionsumfang können Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen, ohne die Produktionssandbox zu beeinträchtigen. Weitere Informationen zu Sandboxes finden Sie in der Übersicht über [Sandboxes](../sandboxes/home.md).

Derzeit unterliegt Data Science Workspace einigen Einschränkungen der Sandbox:

- Compute-Ressourcen werden über die Produktions-Sandbox und Nicht-Produktions-Sandboxen freigegeben. Die Isolation für Produktionssandboxes soll in Zukunft bereitgestellt werden.
- Scala/Spark- und PySpark-Arbeitslasten für Notebooks und Rezepte werden derzeit nur in der Produktions-Sandbox unterstützt. Die Unterstützung für Sandboxen, die keine Produktion sind, soll in Zukunft bereitgestellt werden.

## Data Science Workspace in Aktion

Prognosen und Einblicke liefern die Informationen, die Sie benötigen, um jedem Kunden, der Ihre Website besucht, Ihr Call-Center kontaktiert oder andere digitale Erlebnisse nutzt, ein hoch personalisiertes Erlebnis zu bieten. So funktioniert Ihre tägliche Arbeit mit Data Science Workspace.

### Problem definieren

Das sind alle Beginn mit einem Geschäftsproblem. Ein Online-Call-Center benötigt beispielsweise Kontext, um ein negatives Kundensentiment positiv zu gestalten.

Es gibt viele Daten über den Kunden. Sie haben die Site durchsucht, Artikel in ihren Einkaufswagen gelegt und sogar Bestellungen aufgegeben. Möglicherweise haben sie E-Mails erhalten, Coupons verwendet oder das Call-Center zuvor kontaktiert. Das Rezept muss dann die verfügbaren Daten über den Kunden und seine Aktivitäten verwenden, um die Kaufneigung zu bestimmen und ein Angebot zu empfehlen, das der Kunde wahrscheinlich schätzen und verwenden wird.

![](./images/home/example_problem.png)

Zum Zeitpunkt des Call-Center-Kontakts hat der Kunde noch zwei Paar Schuhe im Warenkorb, aber ein Hemd entfernt. Mit diesen Informationen kann der intelligente Dienst empfehlen, dass der Call-Center-Agent während des Anrufs einen Coupon für 20 % Rabatt auf Schuhe Angebot. Wenn der Kunde den Coupon verwendet, werden diese Informationen dem Datensatz hinzugefügt und die Prognosen werden beim nächsten Aufruf des Kunden sogar noch besser.

### Daten untersuchen und vorbereiten

Basierend auf dem definierten Geschäftsproblem wissen Sie, dass das Rezept alle Webtransaktionen des Kunden prüfen sollte, einschließlich Site-Besuche, Suchvorgänge, Seitenaufrufe, angeklickte Links, Warenkorbaktionen, Angebote erhalten, E-Mails empfangen, Interaktionen im Call-Center usw.

Ein Datenwissenschaftler verbringt in der Regel bis zu 75 % der Zeit, die für die Erstellung eines Rezepts benötigt wird, um die Daten zu erforschen und zu transformieren. Daten stammen oft aus mehreren Repositorys und werden in verschiedenen Schemas gespeichert - sie müssen kombiniert und zugeordnet werden, bevor sie zur Erstellung eines Rezepts verwendet werden können.

[//]: # (Your first step is to check the recipe gallery to see if an existing recipe meets your needs, or comes close. An alternative is to import a recipe you created outside of Adobe Experience Platform. Starting with an existing recipe often streamlines the data exploration phase and makes it easier for a data scientist.)

Wenn Sie von Grund auf neu beginnen oder ein vorhandenes Rezept konfigurieren, beginnen Sie mit der Datensuche in einem zentralisierten und standardisierten Datenkatalog für Ihr Unternehmen, was die Jagd erheblich vereinfacht. Möglicherweise stellen Sie sogar fest, dass ein anderer Datenwissenschaftler in Ihrer Organisation bereits einen ähnlichen Datensatz identifiziert hat, und wählen Sie die Feinabstimmung dieses Datensatzes anstelle des Beginns von Grund auf.
Alle Daten in Adobe Experience Platform entsprechen einem standardisierten XDM-Schema, sodass kein komplexes Modell für die Datenzusammenführung oder Hilfe von einem Datenentwickler erstellt werden muss.

Wenn Sie die benötigten Daten nicht sofort finden, sie aber außerhalb von Adobe Experience Platform vorhanden sind, ist es eine relativ einfache Aufgabe, zusätzliche Datensätze zu erfassen, die sich auch in das standardisierte XDM-Schema umwandeln.\
Sie können Jupyter-Notebook verwenden, um die Vorverarbeitung von Daten zu vereinfachen - möglicherweise beginnend mit einer Notebook-Vorlage oder einem Notebook, das Sie zuvor für die Kaufneigung verwendet haben.

![](./images/home/notebook_templates.png)

### Rezept erstellen

Wenn Sie bereits ein Rezept gefunden haben, das Ihren Anforderungen entspricht, können Sie mit dem Experimentieren fortfahren. Oder Sie können das Rezept ein wenig ändern oder von Grund auf neu erstellen - unter Nutzung der Authoring-Laufzeitumgebung von Data Science Workspace im Jupyter-Notebook. Die Verwendung der Authoring-Laufzeitumgebung stellt sicher, dass Sie sowohl den Arbeitsablauf für Schulungen und Bewertungen im Data Science Workspace verwenden als auch das Rezept später konvertieren können, damit es von anderen Mitgliedern Ihres Unternehmens gespeichert und wiederverwendet werden kann.

Sie können auch ein Rezept in den Data Science Workspace importieren und die Workflows nutzen, um Ihren intelligenten Dienst zu erstellen.

### Experimentieren mit dem Rezept

Mit einem Rezept, das Ihre Kern-Computer-Lernalgorithmen enthält, können viele Rezept-Instanzen mit einem einzigen Rezept erstellt werden. Diese Rezeptinstanzen werden als Modelle bezeichnet. Ein Modell erfordert Schulung und Auswertung, um seine Effizienz und Wirksamkeit zu optimieren, ein Prozess, der in der Regel aus Test und Fehler besteht.

![](./images/home/recipe_hiearchy_ui.png)

Während Sie Ihre Modelle trainieren, werden Schulungen und Bewertungen generiert. Data Science Workspace verfolgt die Bewertungsmetriken für jedes einzelne Modell und deren Schulungslaufzeiten. Mithilfe von Testmetriken, die durch Experimente generiert wurden, können Sie den Schulungsablauf ermitteln, der am besten funktioniert.

![](./images/home/evaluation_metrics.png)

In [diesem Abschnitt](https://www.adobe.io/apis/experienceplatform/home/tutorials/data-science-workspace/dsw-tutorials/trainmodel.html) finden Sie Übungen zur Schulung und Auswertung von Modellen im Data Science Workspace.

### Modell operationalisieren

Wenn Sie das am besten geschulte Rezept für Ihre geschäftlichen Anforderungen ausgewählt haben, können Sie einen intelligenten Dienst in Data Science Workspace ohne Unterstützung durch Entwickler erstellen. Es sind nur ein paar Klicks - keine Kodierung erforderlich. Ein veröffentlichter intelligenter Dienst steht anderen Mitgliedern Ihrer Organisation zur Verfügung, ohne dass das Modell neu erstellt werden muss.

Ein veröffentlichter intelligenter Dienst ist konfigurierbar, um sich von Zeit zu Zeit mit neuen Daten zu trainieren, sobald diese verfügbar werden. Dadurch wird sichergestellt, dass Ihr Service seine Effizienz und Wirksamkeit im Laufe der Zeit erhält.

## Nächste Schritte

Data Science Workspace vereinfacht und vereinfacht den Arbeitsablauf der Datenwissenschaften - von der Datenerfassung über Algorithmen bis hin zu intelligenten Diensten - für Datenwissenschaftler aller Qualifikationsstufen. Mit den ausgereiften Werkzeugen von Data Science Workspace können Sie die Zeit von Daten bis zu Erkenntnissen erheblich verkürzen.

Darüber hinaus stellt Data Science Workspace die Datenwissenschaft und die algorithmischen Optimierungsfunktionen der führenden Marketing-Plattform von Adobe in die Hände von Wissenschaftlern für Unternehmensdaten. Zum ersten Mal können Unternehmen proprietäre Algorithmen auf die Plattform übertragen, indem sie die leistungsstarken Funktionen von Adobe für maschinelles Lernen und KI nutzen, um hochgradig personalisierte Kundenerlebnisse in großem Maßstab bereitzustellen.

Durch die Verbindung von Markenkompetenz mit dem maschinellen Lernen und der KI-Kompetenz von Adobe haben Unternehmen die Möglichkeit, mehr Geschäftswert und Markentreue zu fördern, indem sie Kunden das geben, was sie möchten, bevor sie danach fragen.

Weitere Informationen, z. B. einen kompletten täglichen Arbeitsablauf, finden Sie in der [Data Science Workspace-Dokumentation](./walkthrough.md) .

## Zusätzliche Ressourcen

Das folgende Video unterstützt Sie dabei, den Data Science Workspace zu verstehen.

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)

