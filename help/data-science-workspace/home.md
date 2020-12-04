---
keywords: Experience Platform;home;Data Science Workspace;popular topics;data science workspace;data science
solution: Experience Platform
title: Übersicht über den Data Science Workspace
topic: overview
description: Dieser Leitfaden bietet einen Überblick über die wichtigsten Konzepte im Zusammenhang mit Data Science Workspace.
translation-type: tm+mt
source-git-commit: 581d11bdb934f46c53a6703829b4dc470076e195
workflow-type: tm+mt
source-wordcount: '2578'
ht-degree: 4%

---


# Übersicht über den Data Science Workspace

Adobe Experience Platform [!DNL Data Science Workspace] uses machine learning and artificial intelligence to unleash insights from your data. Integrated into Adobe Experience Platform, [!DNL Data Science Workspace] helps you make predictions using your content and data assets across Adobe solutions.

Datenwissenschaftler aller Qualifikationsstufen finden ausgereifte, einfach zu bedienende Werkzeuge, die eine schnelle Entwicklung, Ausbildung und Abstimmung von maschinellen Lernrezepten unterstützen - all die Vorteile der AI-Technologie, ohne die Komplexität.

Mithilfe [!DNL Data Science Workspace]von Daten können Wissenschaftler auf einfache Weise intelligente Services-APIs erstellen - basierend auf maschinellem Lernen. Diese Dienste können mit anderen Adoben-Diensten wie Adobe Target und Adobe Analytics Cloud kombiniert werden, um Ihnen bei der Automatisierung personalisierter, gezielter digitaler Erlebnisse in Web-, Desktop- und mobilen Apps zu helfen.

Dieser Leitfaden bietet einen Überblick über die wichtigsten Konzepte in Bezug auf [!DNL Data Science Workspace].

## Einführung

Das heutige Unternehmen legt großen Wert auf die Erfassung von Big Data für Prognosen und Einblicke, die es ihnen ermöglichen, Kundenerlebnisse zu personalisieren und Kunden - und Unternehmen - mehr Wert zu verschaffen.
So wichtig es auch ist, dass es zu hohen Kosten kommen kann, von Daten zu Erkenntnissen zu gelangen. Es erfordert in der Regel qualifizierte Datenwissenschaftler, die intensive und zeitaufwendige Datenforschung betreiben, um Modelle für maschinelles Lernen oder Rezepte zu entwickeln, die intelligente Dienste unterstützen. Der Prozess ist langwierig, die Technologie ist komplex und qualifizierte Datenwissenschaftler können schwer zu finden sein.

Mit [!DNL Data Science Workspace]Adobe Experience Platform können Sie unternehmensweit erlebnisorientierte KI einführen, Daten optimieren und schneller in die Programmierung einarbeiten mit:
- Ein Framework für maschinelles Lernen und Laufzeit
- Integrierter Zugriff auf Ihre in Adobe Experience Platform gespeicherten Daten
- Ein auf [!DNL Experience Data Model] (XDM) basierendes einheitliches Data Schema
- Die Rechenleistung ist unverzichtbar für maschinelles Lernen/AI und die Verwaltung von Big DataSets
- Vorgefertigte maschinelle Lernrezepte zur Beschleunigung des Abstiegs in AI-basierte Erlebnisse
- Vereinfachtes Authoring, Wiederverwendung und Modifizierung von Rezepten für Datenwissenschaftler mit unterschiedlichem Kenntnisstand
- Intelligente Veröffentlichung und Freigabe von Diensten in nur wenigen Klicks - ohne Entwickler - sowie Überwachung und Umschulung zur kontinuierlichen Optimierung personalisierter Kundenerlebnisse

Datenwissenschaftler aller Qualifikationsstufen werden schneller und effektivere digitale Erfahrungen erzielen.

## Erste Schritte

Bevor Sie in die Details zu [!DNL Data Science Workspace]den Themen eintauchen, hier eine kurze Zusammenfassung der wichtigsten Begriffe:

| Begriff | Definition |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [!DNL Data Science Workspace] | [!DNL Data Science Workspace] Innerhalb von [!DNL Experience Platform] ermöglicht es Kunden, maschinelle Lernmodelle zu erstellen, die Daten aus verschiedenen Lösungen [!DNL Experience Platform] und Adoben verwenden, um intelligente Einblicke und Prognosen zu generieren, um ansprechende digitale Erlebnisse für Endbenutzer zu entwickeln. |
| Künstliche Intelligenz | Künstliche Intelligenz ist eine Theorie und Entwicklung von Computersystemen, die in der Lage sind, Aufgaben auszuführen, die normalerweise menschliche Intelligenz erfordern, wie visuelle Wahrnehmung, Spracherkennung, Entscheidungsfindung und Übersetzung zwischen Sprachen. |
| Maschinelles Lernen | Maschinelles Lernen ist der Studienbereich, der es Computern ermöglicht, zu lernen, ohne explizit programmiert zu werden. |
| [!DNL Sensei] ML Framework | [!DNL Sensei] ML Framework ist ein einheitliches maschinelles Lernumfeld für die gesamte Adobe, das Daten nutzt, [!DNL Experience Platform] um Datenwissenschaftler bei der Entwicklung maschinenlerngestützter Intelligenzdienste auf schnellere, skalierbare und wiederverwendbare Weise zu unterstützen. |
| [!DNL Experience Data Model] | [!DNL Experience Data Model] (XDM) ist der Standardisierungsaufwand, der von der Adobe zur Definition von Standard-Schemas wie [!DNL Profile] und [!DNL ExperienceEvent]für Customer Experience Management führt. |
| [!DNL JupyterLab] | [!DNL JupyterLab] ist eine Open-Source Web-basierte Schnittstelle für Project Jupyter und ist eng in [!DNL Experience Platform]integriert. |
| Rezepte | Ein Rezept ist der Begriff der Adobe für eine Modellspezifikation. Es handelt sich dabei um einen Container auf oberster Ebene, der ein bestimmtes maschinelles Lernen, einen AI-Algorithmus oder ein Ensemble von Algorithmen, Verarbeitungslogik und Konfiguration darstellt, die zum Aufbau und Ausführen eines geschulten Modells erforderlich sind und somit zur Lösung spezifischer Geschäftsprobleme beitragen. |
| Modell | Ein Modell ist eine Instanz eines Rezepts für maschinelles Lernen, das mithilfe von historischen Daten und Konfigurationen dazu trainiert wird, eine geschäftliche Fragestellung zu lösen. |
| Training | Ein Training besteht aus dem Erlernen von Mustern und Insights auf Grundlage gekennzeichneter Daten. |
| Schulungsmodell | Ein trainiertes Modell stellt die ausführbare Ausgabe eines Modellschulungsprozesses dar, bei dem eine Reihe von Schulungsdaten auf die Modellinstanz angewendet wurde. Ein ausgebildetes Modell behält einen Verweis auf jeden intelligenten Webdienst bei, der daraus erstellt wird. Das geschulte Modell eignet sich für die Bewertung und Erstellung eines intelligenten Webdiensts. Änderungen an einem geschulten Modell können als neue Version nachverfolgt werden. |
| Scoring | Beim Scoring werden mithilfe eines trainierten Modells Insights aus Daten generiert. |
| Dienst | Ein bereitgestellter Dienst stellt Funktionen einer künstlichen Intelligenz, eines maschinellen Lernmodells oder eines erweiterten Algorithmus über eine API zur Verfügung, sodass sie von anderen Diensten oder Anwendungen genutzt werden können, um intelligente Apps zu erstellen. |

Das folgende Diagramm zeigt die hierarchische Beziehung zwischen Rezepten, Modellen, Schulungsübungen und Bewertungsläufen.

![](./images/home/recipe_hiearchy_ui.png)

## Erläuterungen [!DNL Data Science Workspace]

Mit [!DNL Data Science Workspace]diesen Daten können Ihre Wissenschaftler den umständlichen Prozess der Ermittlung von Erkenntnissen in großen Datensätzen optimieren. Basierend auf einem gemeinsamen Framework für maschinelles Lernen und Laufzeitumgebung [!DNL Data Science Workspace] bietet es ein erweitertes Workflow-Management, eine Modellverwaltung und Skalierbarkeit. Intelligente Dienste unterstützen die Wiederverwendung von maschinellen Lernrezepten, um eine Vielzahl von Anwendungen zu ermöglichen, die mithilfe von Adobe-Produkten und -Lösungen erstellt wurden.

### Datenzugriff aus einer Hand

Daten sind der Eckpfeiler von KI und maschinellem Lernen.

[!DNL Data Science Workspace] ist vollständig in Adobe Experience Platform integriert, einschließlich Data Lake, [!DNL Real-time Customer Profile]und [!DNL Unified Edge]. Entdecken Sie alle in Adobe Experience Platform gespeicherten Organisationsdaten zusammen mit gemeinsamen Big Data und Deep-Learning-Bibliotheken wie [!DNL Spark] ML und [!DNL TensorFlow]. Wenn Sie nicht finden, was Sie benötigen, erfassen Sie Ihre eigenen Datensätze mit dem XDM-standardisierten Schema.

### Vorgefertigte maschinelle Lernrezepte

[!DNL Data Science Workspace] umfasst vorgefertigte maschinelle Lernrezepte für gängige Geschäftsanforderungen, z. B. Prognosen zum Einzelhandel und Anomalieerkennung, sodass Datenwissenschaftler und Entwickler nicht von Grund auf Beginn benötigen. Derzeit werden drei Rezepte angeboten: [Produktkaufprognosen](./pre-built-recipes/product-purchase-prediction.md), [Produktempfehlungen](./pre-built-recipes/product-recommendations.md)und [Einzelhandelsverkäufe](./pre-built-recipes/retail-sales.md).

[//]: # (The built-in recipe gallery offers recommendations for prebuilt recipes based on your business needs.)

Wenn Sie es bevorzugen, können Sie ein vorgefertigtes Rezept an Ihre Anforderungen anpassen, ein Rezept importieren oder einen Beginn von Grund auf neu erstellen, um ein benutzerdefiniertes Rezept zu erstellen. Sobald Sie jedoch ein Rezept trainieren und überarbeiten, ist für die Erstellung eines benutzerdefinierten intelligenten Dienstes kein Entwickler erforderlich - nur wenige Klicks und Sie sind bereit, ein zielgerichtetes, personalisiertes digitales Erlebnis zu entwickeln.

### Arbeitsablauf, der auf den Datenwissenschaftler ausgerichtet ist

Unabhängig vom Grad Ihrer fachlichen Erfahrung in der Datenwissenschaft [!DNL Data Science Workspace] können Sie den Prozess der Suche nach Einblicken in Daten und deren Anwendung auf digitale Erfahrungen vereinfachen und beschleunigen.

### Datenforschung

Die richtigen Daten zu finden und sie vorzubereiten, ist der arbeitsintensivste Teil des Aufbaus eines effektiven Rezeptes. [!DNL Data Science Workspace] und Adobe Experience Platform hilft Ihnen, schneller von Daten zu Einblicken zu gelangen.

Unter Adobe Experience Platform werden Ihre Daten über den Kanal hinweg zentralisiert und im XDM-standardisierten Schema gespeichert, sodass sie leichter zu finden, zu verstehen und zu reinigen sind. Ein Datenspeicher auf der Grundlage eines gemeinsamen Schemas kann Ihnen unzählige Stunden an Datenforschung und -vorbereitung ersparen.

Verwenden Sie während des Browsens R, [!DNL Python]oder Scala mit integriertem Hosting, [!DNL Jupyter Notebook] um den Datenkatalog zu durchsuchen [!DNL Platform]. Mit einer dieser Sprachen können Sie auch die Vorteile von [!DNL Spark] ML und TensorFlow nutzen. Beginn von Grund auf, oder verwenden Sie eine der Notebook-Vorlagen für spezifische Geschäftsprobleme.

Im Rahmen des Arbeitsablaufs für die Datenforschung können Sie auch neue Daten erfassen oder vorhandene Funktionen zur Datenvorbereitung verwenden.

### Authoring

Mit [!DNL Data Science Workspace]dieser Option entscheiden Sie, wie Sie Rezepte erstellen möchten.

- Sparen Sie Zeit, indem Sie nach einem vorgefertigten Rezept suchen, das Ihren geschäftlichen Anforderungen entspricht und das Sie nach Bedarf verwenden oder konfigurieren können, um Ihre spezifischen Anforderungen zu erfüllen.
- Erstellen Sie ein Rezept von Grund auf neu, indem Sie die Authoring-Laufzeit in Jupyter Notebook verwenden, um das Rezept zu entwickeln und zu registrieren.
- Laden Sie ein außerhalb von Adobe Experience Platform erstelltes Rezept in ein [!DNL Data Science Workspace] oder importieren Sie Rezeptcode aus einem Repository, z. B. [!DNL Git]mit der zwischen- [!DNL Git] und [!DNL Data Science Workspace]verfügbaren Authentifizierung und Integration.

### Experimentieren

Data Science Workspace bietet eine enorme Flexibilität beim Experimentieren. Beginn mit Ihrem Rezept. Erstellen Sie dann eine separate Instanz, indem Sie denselben Core-Algorithmus mit eindeutigen Merkmalen wie Hypertuning-Parameter verwenden. Sie können so viele Instanzen erstellen, wie Sie benötigen, und jede Instanz so oft trainieren und bewerten, wie Sie möchten. Wenn Sie sie trainieren, werden Rezepte, Rezeptorinstanzen und geschulte Instanzen sowie Evaluierungsmetriken [!DNL Data Science Workspace] verfolgt, sodass Sie dies nicht benötigen.

### Operationalisierung

Wenn Sie mit Ihrem Rezept zufrieden sind, ist es nur ein paar Klicks, einen intelligenten Dienst zu schaffen. Keine Kodierung erforderlich - Sie können es selbst machen, ohne einen Entwickler oder Ingenieur zu benennen. Veröffentlichen Sie den intelligenten Dienst schließlich auf Adobe IO und es ist für Ihr digitales Erlebnis-Team nutzbar.

<!--You can also publish your intelligent service to the Service Gallery, where it's available to specific people, specific organizations, or everyone who develops data solutions on Adobe Experience Platform. You can even share it with your external partners, and they can share their intelligent service with you. And the next time you're starting a new recipe, you can check the Service Gallery to see if there's a similar intelligent service you can use to get started. -->

### Kontinuierliche Verbesserung

[!DNL Data Science Workspace] verfolgt, wo intelligente Dienste aufgerufen werden und wie sie funktionieren. Wenn Daten eingehen, können Sie die Genauigkeit intelligenter Dienste bewerten, um die Schleife zu schließen, und die Rezepte nach Bedarf neu ausbilden, um die Leistung zu verbessern. Das Ergebnis ist eine kontinuierliche Verfeinerung der Präzision der Kundenpersonalisierung.

### Zugriff auf neue Funktionen und Datensätze

Datenwissenschaftler können neue Technologien und Datensätze nutzen, sobald sie über Adoben verfügbar sind. Durch häufige Aktualisierungen machen wir die Arbeit, Datasets und Technologien in die Plattform zu integrieren, sodass Sie nicht müssen.

### Zugriffskontrolle in [!DNL Data Science Workspace]

Access control for [!DNL Experience Platform] is administered through the [Adobe Admin Console](https://adminconsole.adobe.com). Diese Funktion nutzt Produktprofile in Admin Console, um Anwender mit Berechtigungen und Sandboxes zu verknüpfen. Weiterführende Informationen dazu finden Sie unter [Zugriffskontrolle – Übersicht](../access-control/home.md).

>[!IMPORTANT]
>
>Zur Verwendung [!DNL Data Science Workspace]muss die Berechtigung [!UICONTROL &quot;Data Science Workspace verwalten&quot;] aktiviert sein.

Die folgende Tabelle zeigt die Auswirkungen, die eine Aktivierung oder Deaktivierung dieser Berechtigung hat:

| Berechtigung | Aktiviert | Deaktiviert |
|---|---|---|
| [!DNL Manage Data Science Workspace] | Bietet Zugriff auf alle Dienste in [!DNL Data Science Workspace]. | API- und UI-Zugriff auf alle Dienste innerhalb [!DNL Data Science Workspace] sind deaktiviert. Bei Deaktivierung wird das Routing zu den [!DNL Data Science Workspace] Modellen **[!UICONTROL - und]** Dienstseiten **** verhindert. |

### Sicherheit und Seelenfrieden

Die Sicherung Ihrer Daten ist eine der obersten Prioritäten für die Adobe. Adobe schützt Ihre Daten mit Sicherheitsvorgängen und -kontrollen, die zur Einhaltung branchenüblicher Normen, Vorschriften und Zertifizierungen entwickelt wurden.

Security ist Teil der Adobe Secure Product Lifecycle in Software und Services integriert.
Weitere Informationen zu Adoben- und Softwaresicherheit, Compliance und mehr finden Sie auf der Seite &quot;Sicherheit&quot;unter https://www.adobe.com/security.html.

### Sandbox-Unterstützung

Sandboxes sind virtuelle Partitionen innerhalb einer einzelnen Instanz von [!DNL Experience Platform]. Jede [!DNL Platform] Instanz unterstützt eine Produktions-Sandbox und mehrere Nicht-Produktions-Sandboxen, wobei jede einzelne eine eigene Bibliothek mit [!DNL Platform] Ressourcen unterhält. Mit Nicht-Produktions-Sandboxes können Sie Funktionen testen, Experimente ausführen und benutzerdefinierte Konfigurationen vornehmen, ohne die Produktions-Sandbox zu beeinträchtigen. For more information on sandboxes, see the [sandboxes overview](../sandboxes/home.md).

Zurzeit [!DNL Data Science Workspace] gelten einige Sandbox-Beschränkungen:

- Compute-Ressourcen werden über die Produktions-Sandbox und Nicht-Produktions-Sandboxen freigegeben. Die Isolation für Produktionssandboxes soll in Zukunft bereitgestellt werden.
- Scala/[!DNL Spark] und PySpark-Arbeitslasten für Notebooks und Rezepte werden derzeit nur in der Produktions-Sandbox unterstützt. Die Unterstützung für Sandboxen, die keine Produktion sind, soll in Zukunft bereitgestellt werden.

## [!DNL Data Science Workspace] in Aktion

Prognosen und Einblicke liefern die Informationen, die Sie benötigen, um jedem Kunden, der Ihre Website besucht, Ihr Call-Center kontaktiert oder andere digitale Erlebnisse nutzt, ein hoch personalisiertes Erlebnis zu bieten. Hier sehen Sie, wie Ihre tägliche Arbeit abläuft [!DNL Data Science Workspace].

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
Sämtliche Daten in Adobe Experience Platform entsprechen einem standardisierten XDM-Schema, sodass kein komplexes Modell für die Datenzusammenführung oder Hilfe eines Dateningenieurs erstellt werden muss.

Wenn Sie die benötigten Daten nicht sofort finden, sie aber außerhalb von Adobe Experience Platform existieren, ist es eine relativ einfache Aufgabe, zusätzliche Datensätze zu erfassen, die sich auch in das standardisierte XDM-Schema umwandeln.\
Sie können [!DNL Jupyter Notebook] die Vorverarbeitung von Daten vereinfachen - möglicherweise beginnend mit einer Notebook-Vorlage oder einem Notebook, das Sie zuvor für die Kaufneigung verwendet haben.

![](./images/home/notebook_templates.png)

### Rezept erstellen

Wenn Sie bereits ein Rezept gefunden haben, das Ihren Anforderungen entspricht, können Sie mit dem Experimentieren fortfahren. Oder Sie können das Rezept ein wenig ändern oder von Grund auf neu erstellen - unter Nutzung der [!DNL Data Science Workspace] Authoring-Laufzeit in [!DNL Jupyter Notebook]. Die Verwendung der Authoring-Laufzeit stellt sicher, dass Sie sowohl den [!DNL Data Science Workspace] Schulungs- als auch den Bewertungsarbeitsablauf verwenden und das Rezept später konvertieren können, damit es von anderen Mitgliedern Ihres Unternehmens gespeichert und wiederverwendet werden kann.

Sie können auch ein Rezept in die Workflows importieren [!DNL Data Science Workspace] und diese nutzen, während Sie Ihren intelligenten Dienst erstellen.

### Experimentieren mit dem Rezept

Mit einem Rezept, das Ihre Kern-Computer-Lernalgorithmen enthält, können viele Rezept-Instanzen mit einem einzigen Rezept erstellt werden. Diese Rezeptinstanzen werden als Modelle bezeichnet. Ein Modell erfordert Schulung und Auswertung, um seine Effizienz und Wirksamkeit zu optimieren, ein Prozess, der in der Regel aus Test und Fehler besteht.

![](./images/home/recipe_hiearchy_ui.png)

Während Sie Ihre Modelle trainieren, werden Schulungen und Bewertungen generiert. [!DNL Data Science Workspace] erfasst die Evaluierungsmetriken für jedes einzelne Modell und deren Schulungslaufzeiten. Mithilfe von Testmetriken, die durch Experimente generiert wurden, können Sie den Schulungsablauf ermitteln, der am besten funktioniert.

![](./images/home/evaluation_metrics.png)

Besuchen Sie entweder das [API](./models-recipes/train-evaluate-model-api.md) - oder [UI](./models-recipes/train-evaluate-model-ui.md) -Lernprogramm, um zu erfahren, wie Sie Modelle trainieren und auswerten können [!DNL Data Science Workspace].

### Modell operationalisieren

Wenn Sie das am besten geschulte Rezept für Ihre geschäftlichen Anforderungen ausgewählt haben, können Sie einen intelligenten Dienst [!DNL Data Science Workspace] ohne Hilfe von Entwicklern erstellen. Es sind nur ein paar Klicks - keine Kodierung erforderlich. Ein veröffentlichter intelligenter Dienst steht anderen Mitgliedern Ihrer Organisation zur Verfügung, ohne dass das Modell neu erstellt werden muss.

Ein veröffentlichter intelligenter Dienst ist konfigurierbar, um sich von Zeit zu Zeit mit neuen Daten zu trainieren, sobald diese verfügbar werden. Dadurch wird sichergestellt, dass Ihr Service seine Effizienz und Wirksamkeit im Laufe der Zeit erhält.

## Nächste Schritte

[!DNL Data Science Workspace] hilft bei der Straffung und Vereinfachung des Arbeitsablaufs in der Datenwissenschaft, von der Datenerfassung über Algorithmen bis hin zu intelligenten Diensten für Datenwissenschaftler aller Qualifikationsstufen. Mit den ausgereiften Tools [!DNL Data Science Workspace] können Sie die Zeit von Daten bis zu Erkenntnissen erheblich verkürzen.

Wichtiger noch ist, dass [!DNL Data Science Workspace] die Datenwissenschaft und die algorithmische Optimierung der führenden Marketingplattform der Adobe in die Hände von Unternehmensdatenwissenschaftlern gelegt werden. Zum ersten Mal können Unternehmen proprietäre Algorithmen auf die Plattform übertragen, indem sie die leistungsstarken maschinellen Lernfunktionen und KI-Funktionen der Adobe nutzen, um hochpersonalisierte Kundenerlebnisse in großem Maßstab zu bieten.

Durch die Verbindung von Markenwissen und maschinellem Lernen und KI-Fähigkeiten der Adobe können Unternehmen den Geschäftswert und die Markentreue steigern, indem sie ihren Kunden das geben, was sie wollen, bevor sie danach fragen.

Weitere Informationen, z. B. einen kompletten täglichen Arbeitsablauf, finden Sie in der [Data Science Workspace-Dokumentation](./walkthrough.md) .

## Zusätzliche Ressourcen

Das folgende Video unterstützt Sie dabei, [!DNL Data Science Workspace]die

>[!VIDEO](https://video.tv.adobe.com/v/30567?quality=12&amp;enable10seconds=on&amp;speedcontrol=on)

