---
keywords: RTCDP; CDP; Real-time Customer Data Platform; Echtzeit-Kundendatenplattform; Echtzeit-CDP; cdp; rtcdp
title: Erste Schritte mit Real-time Customer Data Platform
description: Verwenden Sie dieses Szenario als Beispiel, wenn Sie Ihre Implementierung von Adobe Real-Time Customer Data Platform einrichten.
feature: Get Started, Use Cases
exl-id: 9f775d33-27a1-4a49-a4c5-6300726a531b
source-git-commit: 82535ec3ac2dd27e685bb591fdf661d3ab5dd2c9
workflow-type: tm+mt
source-wordcount: '2325'
ht-degree: 62%

---

# Erste Schritte mit Real-time Customer Data Platform

Diese ersten Schritte führen Sie durch eine Beispielimplementierung von Real-time Customer Data Platform (Real-Time CDP). Sie können sie bei der Einrichtung einer eigenen Implementierung als Muster verwenden. Zwar enthält das vorliegende Handbuch spezifische Beispiele, doch gibt es auch Links zu weiteren Informationen, die Sie bei der Einrichtung nutzen können.

Dieses Beispiel zeigt die Leistungsfähigkeit von Real-time Customer Data Platform mit Adobe Experience Platform:

* Daten aus verschiedenen Quellen erfassen
* Zusammenführen in einer einzelnen [!DNL real-time customer profile]
* Ein konsistentes, relevantes und personalisiertes Erlebnis auf allen Geräten ermöglichen

## Anwendungsfall

Luma, ein Sportbekleidungsunternehmen, arbeitet kontinuierlich daran, sein Kundenerlebnis zu verbessern. Das Unternehmen verfügt über eine neue Initiative zur Steigerung der Geschenkumsätze. Außerdem soll übermäßige Kommunikation verringert werden (z. B. aufdringliche Anzeigen, die Kunden überall hin folgen).

Derzeit geben sie zu viel für Medien aus, die sich erneut auf Artikel beziehen, die der Besucher in Zukunft nicht kaufen wird. Beispielsweise möchte Luma niemanden erneut mit einem Artikel ansprechen, der als einmaliger Kauf für eine andere Person gedacht war.

Momentan sind die Daten von Luma auf verschiedene Quellen verteilt. Daher steht das Unternehmen vor großen Herausforderungen:

* Die Marketing-Abteilung muss mit verschiedenen Teams zusammenarbeiten, die jeweils für eine eigene Datenquelle verantwortlich sind (z. B. Website, App, Treuesysteme, CRM usw.).
* Wenn das Marketing-Team endlich Zugriff auf die Daten erhält, sind diese oft schon veraltet und für zeitsensible Kampagnen nicht mehr relevant.
* Es muss die Daten vereinheitlichen, damit diese auf Personen abzielen und nicht auf Kanäle.

Daher verfolgt Luma folgende Geschäftsziele:

* Erstellen einer einheitlichen Echtzeitansicht von Kunden auf Basis unterschiedlicher Datenquellen.
* Personalisieren von Marketing-Kampagnen mit relevanten Botschaften über verschiedene Kanäle und Geräte hinweg.

Um diese Ziele erreichen zu können, muss das Marketing-Team dazu in der Lage sein, Kundendaten in großem Umfang zu verwalten.

Mit Real-Time CDP auf Basis von Adobe Experience Platform kann die Marketing-Organisation von Luma:

1. Erfassen von Daten aus unterschiedlichen Plattformen und Sicherstellen, dass diese später für andere Marketing-Aktivitäten verfügbar sind.
1. Einrichten einer zentralen Echtzeitansicht von Kunden, unabhängig davon, woher die Daten stammen.
1. Bereitstellen eines konsistenten, relevanten und personalisierten Erlebnisses an jedem Touchpoint.

## Schritte

Dieses Tutorial umfasst folgende Schritte:

1. [Kundenprofil](#customer-profile) erstellen.
1. Anwendererlebnis [personalisieren](#personalizing-the-user-experience).
1. [Verschiedene Datenquellen](#using-multiple-data-sources) verwenden.
1. [Datenquelle konfigurieren](#configuring-a-data-source).
1. [Daten erfassen](#bringing-the-data-together-for-a-specific-customer) für einen bestimmten Kunden.
1. Einrichten von [Zielgruppen](#audiences).
1. [Ziele](#destinations) einrichten.
1. [Profil geräteübergreifend zusammenführen](#cross-device-identity-stitching).
1. [Profil analysieren](#analyzing-the-profile).

## Kundenprofil

Wenn Kunden Ihre Site zum ersten Mal besuchen, wissen Sie gar nichts über sie.

![Bild](assets/luma-site.png)

Während der Navigation werden Daten in Echtzeit erfasst und nicht nur an eine Report Suite in Adobe Analytics gesendet, sondern auch direkt an Adobe Experience Platform. Bei der Erfassung von Daten beginnen Sie, anhand von Verhaltensdaten in [!DNL Experience Platform's real-time customer profile] eine einzelne Ansicht des Verbrauchers zu erstellen.

Bei vielen Besuchern der Website handelt es sich wahrscheinlich um wiederkehrende Kunden, die zuvor bereits bei Luma gekauft haben.  Es ist wichtig, dass Luma Botschaften und Angebote personalisieren kann, um sowohl neue und wiederkehrende Besucher als auch bekannte Kunden anzusprechen.

### Erstbesuch eines neuen Kunden

Beispielsweise navigiert ein nicht identifizierter Besucher auf der Site &quot;Luma&quot;zum Abschnitt &quot;Herren&quot;und sieht sich einige laufende Pullover an.

![Bild](assets/luma-sweatshirts.png)

Wenn der Kunde navigiert, um mehr über diese Produkte zu erfahren, werden diese Produktansichten in Adobe Analytics erfasst und an [!DNL Experience Platform] gesendet.

<!--![image](assets/luma-shirt-detail.png)-->

Luma kann das Verhalten des Besuchers einem Nutzerprofil in Adobe Experience Platform zuordnen und damit beginnen, sich einen genaueren Überblick über das Verhalten des Kunden zu verschaffen.

### Detailliertere Ansicht des Kunden

Wenn der Kunde weiter mit der Website interagiert, ergibt sich nach und nach ein klareres Bild. Angenommen, der Besucher fügt dem Warenkorb ein Produkt hinzu und meldet sich an.

Bei der Anmeldung identifiziert sich der Kunde als Sarah Rose.

![Bild](assets/luma-login.png)

Zwei Identitäten werden zusammengeführt:

* die anonymen Browsing-Daten
* die vorhandenen Daten, die mit dem Konto von Sarah Rose verknüpft sind.

Beide Identitäten werden in [!DNL Experience Platform] zu einem einzigen Profil zusammengefasst. Luma verfügt nun über eine zentrale Ansicht dieses Kunden.

Wenn man das Browsing-Verhalten des anonymen Besuchers im Herrenbereich der Site betrachtet, hätte man erwarten können, dass der Kunde männlich ist. Nachdem sie angemeldet ist, erkennt Luma Sarah Rose. Luma nutzt die Stärke von [!DNL Real-Time Customer Profile], um die Nachrichten, die ihr über verschiedene Kanäle hinweg zugestellt werden, zu verfeinern.

## Personalisierung des Kundenerlebnisses

Sarah wird mit einer Treuebotschaft begrüßt und ihr wird dafür gedankt, dass sie Bronze-Mitglied ist. Zudem erhält sie weitere Informationen zu Vorteilen und dazu, wie sie ihren Status und Punktestand verbessern kann.

Sie navigiert zur Startseite, um weitere zu durchsuchen.

![Bild](assets/luma-personal.png)

Sarah erhält ein personalisiertes Startseitenerlebnis, das dynamisch bereitgestellt wird und auf ihrem &quot;[!DNL Real-Time Customer Profile]&quot;-Wert in Adobe Experience Platform basiert.

Dank der Adobe Sensei-basierten Personalisierung in Adobe Target, bei der ihre bisherigen Käufe sowie ihre Affinität für Laufbekleidung und -ausrüstung berücksichtigt werden, werden ihr relevante Inhalte angezeigt. Außerdem passt Luma den Inhalt des Herrenkatalogs basierend auf ihrem letzten Durchsuchen an Laufausrüstung für Männer an.

Weiter unten auf der Seite werden Sarah vorgestellte Produkte sowie eine Ablage mit neuen Empfehlungen angezeigt, die auf ihren zuletzt angezeigten Artikeln basieren.

Diese personalisierten Inhalte helfen Sarah dabei, rasch passende Artikel zu finden. Dadurch wird die Konversionsrate verbessert und ein angenehmeres Kundenerlebnis entsteht.

### Den Kunden zurückholen

Sarah wird abgelenkt und verlässt die Site, wodurch ihre Sitzung beendet wird. Luma kann ihre Daten in Adobe Experience Platform verwenden, um sie zurück auf die Site zu holen.

Real-time Customer Data Platform wurde mit Adobe Experience Platform für das Customer Experience Management entwickelt. Mit ihrer Hilfe können Unternehmen folgende Aufgaben erledigen:

* Datenintegration und -aktivierung vereinfachen
* Nutzung bekannter und unbekannter Daten steuern
* Marketing-Anwendungsfälle skaliert beschleunigen

## Verwenden verschiedener Datenquellen

Das Team von Luma verfügt über alle Verhaltens- und Kundendaten an einem Ort.

![Bild](assets/luma-dash.png)

Es kann Daten aus allen der folgenden Quellen erfassen:

* Vorhandene Daten aus Adobe Experience Cloud-Lösungen
* Daten aus Nicht-Adobe-Quellen, wie z. B. dem Treueprogramm von Luma, dem Callcenter und Point-of-Sale-Systemdaten
* Echtzeit-Streaming-Daten aus Luma-Datenquellen
* Echtzeit-Daten aus Adobe-Lösungen (keine neuen Tags erforderlich)

Alle diese Daten aus unterschiedlichen Quellen werden in einem einheitlichen Kundenprofil zusammengeführt.

## Konfigurieren einer Datenquelle

Verwenden Sie [!DNL Real-Time Customer Data Platform] , um neue Datenquellen in Platform zu importieren. Real-Time CDP enthält einen Datenquellenkatalog, der schnell und einfach zum Profil hinzugefügt werden kann.

![Bild](assets/luma-source-cat.png)

Um beispielsweise die CRM-Daten von Luma zu erfassen, filtern Sie den Katalog nach *CRM* und alle nativen Connectoren mit *CRM* werden aufgelistet. Hinzufügen von [!DNL Microsoft Dynamics CRM] -Daten:

1. Lassen Sie die Verbindung zu.

   ![Bild](assets/luma-source-auth.png)

1. Wählen Sie aus einer Empfehlungsliste mit vorab zugeordneten XDM-Tabellen aus, um zu entscheiden, was Sie importieren möchten.

   <!--    ![image](assets/luma-source-import.png) -->

   Wählen Sie beispielsweise **[!UICONTROL Kontakte]**. Eine Vorschau der Kontaktdaten wird automatisch geladen, damit Sie überprüfen können, ob alles wie erwartet aussieht.

   Real-Time CDP übernimmt einen Großteil der manuellen Arbeit aus diesem Prozess, indem Standardfelder automatisch dem Profilschema [!DNL Experience Data Model] (XDM) zugeordnet werden.

1. Überprüfen Sie die Feldzuweisungen.

   <!--    ![image](assets/luma-source-mapping.png) -->

   Prüfen Sie beispielsweise, ob das E-Mail-Feld für Kontakte richtig zugeordnet ist.\
   Sie haben die Möglichkeit, eine Vorschau der Daten anzuzeigen und eine erweiterte Zuordnung vorzunehmen.

1. Legen Sie einen Zeitplan fest.

   ![Bild](assets/luma-source-sched.png)

Damit ist der Vorgang abgeschlossen. Sie haben gerade [!DNL Microsoft CRM] als Datenquelle zu [!DNL Experience Platform] hinzugefügt.

### Bezeichnen von erfassten Daten für Nutzungsrichtlinien

Luma hat viele interne Richtlinien, die die Nutzung bestimmter Arten von erfassten Informationen einschränken und auch rechtlichen und datenschutzrechtlichen Vorgaben bezüglich der Nutzung von Daten entsprechen müssen. Mit Data Governance in Adobe Experience Platform können vordefinierte Datennutzungsbezeichnungen auf Datensätze (und bestimmte Felder in diesen Datensätzen) angewendet werden, sodass Luma die Daten nach bestimmten Nutzungsbeschränkungen kategorisieren kann.

![](assets/governance-labels.png)

Sobald die Datennutzungsbezeichnungen angewendet wurden, kann Luma dann Data Governance verwenden, um Datennutzungsrichtlinien zu erstellen. Datennutzungsrichtlinien sind Regeln, die beschreiben, welche Arten von Aktionen Sie für Daten ausführen dürfen, die bestimmte Bezeichnungen enthalten. Beim Versuch, eine Aktion in Real-Time CDP durchzuführen, die eine Richtlinienverletzung darstellt, wird die Aktion verhindert und ein Warnhinweis angezeigt, der angibt, welche Richtlinie verletzt wurde und warum.

Zusätzlich zu Real-Time CDP

## Zusammenführen der Daten für einen bestimmten Kunden

Durchsuchen Sie in diesem Szenario Profile nach Sarah Rose. Ihr Profil erscheint mit der E-Mail-Adresse, die sie zum Anmelden verwendet hat.

<!-- ![image](assets/luma-find-profile.png) -->

Alle Profilinformationen, die Luma zu Sarah hat, werden angezeigt. Dazu gehören ihre persönlichen Informationen wie Adresse und Telefonnummer, die Voreinstellungen für die Kommunikation und die Zielgruppen, für die sie qualifiziert ist.

| Kategorie | Beschreibung |
|---|---|
| Identitäten | Zeigt die Identitäten an, die in [!DNL Platform] aus Sarahs Interaktionen mit Luma über Kanäle und Geräte hinweg verknüpft wurden. Ihre ECID von der Website wird angezeigt. Zu ihrer Identität gehören auch die ECID aus ihrer mobilen App, ihre E-Mail-ID, eine CRM-ID aus dem kürzlich hinzugefügten [!DNL Microsoft Dynamics] -Datensatz und eine Treueprogramm-ID, die vom Treuesystem Luma an Adobe Experience Platform übergeben wird. |
| Ereignisse | Zeigt alle Interaktionsdaten von Sarah mit der Marke Luma an. Dazu gehören der Artikel, den sie gerade angesehen hat, alles, was Sarah in der Vergangenheit angesehen hat, die E-Mails, die sie erhalten hat, ihre Interaktionen mit dem Callcenter sowie Daten darüber, auf welchem Kanal und welchem Gerät die einzelnen Interaktionen stattgefunden haben. |

Das Real-Time CDP-Profil reduziert den Arbeitsablauf des Luma-Marketingteams von Wochen auf Minuten und bietet auf Grundlage dieser 360-Grad-Kundenansicht Möglichkeiten zur Personalisierung. Das Profil fasst die Verhaltensdaten, die erfasst wurden, als sie die Site vor dem Anmelden durchsucht hat, mit ihrem bestehenden Kundenprofil zusammen und erlaubt so einen genauen Überblick über Sarah.

Das Marketing-Team kann diese verbesserte [!DNL Real-Time Customer Profile] verwenden, um Sarahs Erlebnis besser zu personalisieren und die Markentreue zu Luma zu erhöhen.

## Zielgruppen

Die leistungsstarken Segmentierungsfunktionen von Adobe Experience Platform ermöglichen es Marketing-Experten, Attribute, Ereignisse und vorhandene Zielgruppen basierend auf den in [!DNL Real-Time Customer Profile] erfassten Daten zu kombinieren.

<!-- ![image](assets/luma-segments.png) -->

In diesem Szenario weisen Sarahs letzte Interaktionen auf der Site auf ein anderes Verhalten als bei ihren vergangenen Aktionen hin. Sarah kauft normalerweise Damenkleidung. Der Artikel in ihrem Warenkorb ist jedoch ein großes Pullover für Männer.

Das Data-Science-Team von Luma hat Modelle zur Kauftendenz entwickelt. Ein Modell identifiziert eine plötzliche Änderung bei der Bekleidungskategorie (z. B. Herren/Damen) oder der Größe für den bestehenden Kunden. Sarahs verändertes Kaufverhalten deutet darauf hin, dass sie nicht für sich selbst einkauft.

<!-- ![image](assets/luma-gift.png) -->

### Audience definieren

Verwenden Sie die verschiedenen Optionen für die visuelle Komposition oder den code-basierten Ausdruckseditor im Arbeitsbereich für Zielgruppen, um eine Zielgruppe zu ändern oder zu erstellen, die Warenkorbabbrecher darstellt, die offenbar gerade ein Geschenk kaufen:

```sql
Profile: Category != Preferred Category 
AND 
Product Size != Preferred Size 
in last 7 days.  
AND 
Abandoned Cart 
AND 
Loyalty member 
```

<!-- ![image](assets/luma-abandon.png)-->

Da Sarah wahrscheinlich einen Geschenkartikel in den Warenkorb gelegt und den Vorgang dann abgebrochen hat, kann Luma sie mit einem Angebot zum kostenlosen Einpacken des Geschenks locken.

## Ziele

Wenn Sie die Zielgruppe &quot;Warenkorbabbrecher für Geschenkgutscheine&quot;hinzugefügt haben, können Sie ungefähr sehen, wie viele Personen Teil dieser Zielgruppe sind. Sie können aktiv werden und es für Personalisierungszwecke kanalübergreifend bereitstellen.

Wählen Sie **[!UICONTROL An Ziele senden]** aus.

In Real-Time CDP kann Luma zur Personalisierung nahtlos auf ihre Zielgruppen reagieren.\
Hier sehen Sie alle Ziele, an die Luma dieses Ziel senden kann, sowohl Adobe- als auch Nicht-Adobe-Lösungen:

![Bild](assets/luma-dest.png)

### Auswählen von Zielen

In diesem Szenario möchte Luma die Zielgruppe mit Personalisierung über folgende Ziele hinweg erneut ansprechen:

* Google, für Anzeige
  <!--* Facebook -->
* Adobe Campaign, für E-Mail

<!-- ![image](assets/luma-sched-dest.png) -->

### Planen von Zielen

Sie können auch planen, dass der Zielgruppenexport zu einem bestimmten Zeitpunkt gestartet oder beendet wird. Die Zielgruppe wird veröffentlicht und in den konfigurierten Plattformen am geplanten Datum automatisch aktualisiert.

>[!NOTE]
>
>Wenn Sie optional das Datumsfeld auswählen, wird automatisch eine Zeitdauer von 90 Tagen festgelegt.

Wählen Sie **[!UICONTROL Speichern]** aus, um zur nächsten Seite zu wechseln.

Wenn ein Kunde in dieser Zielgruppe einen Kauf tätigt, wird seine Mitgliedschaft in dieser Zielgruppe in Echtzeit unterdrückt. Sie qualifizieren sich nicht mehr, weil sich ihr Status geändert hat.

Das spart dem Direktor des Medien-Teams von Luma Hunderttausende von Dollar, da er Inventar nicht für eine Zielgruppe verwenden muss, die gar nicht qualifiziert ist.

### Durchsetzung von Datennutzungsrichtlinien für Ziele

Adobe Experience Platform enthält Datenschutz- und Sicherheitskontrollen, mit denen festgestellt werden kann, ob eine Zielgruppe für ein bestimmtes Ziel aktiviert werden kann. Die Aktivierung ist je nach Marketing-Zweck, der dem Ziel beim Erstellen zugewiesen wurde, sowie den von Ihrem Unternehmen festgelegten Datennutzungsrichtlinien aktiviert oder eingeschränkt.

Wenn Ihre Aktivität gegen eine Richtlinie verstößt, wird eine Warnmeldung angezeigt. Diese Warnmeldung enthält Informationen zur Datenherkunft, mit denen Sie erkennen können, wie gegen die Richtlinie verstoßen wurde und was Sie tun können, um den Verstoß zu beheben.

Mit diesen Steuerelementen hilft [!DNL Experience Platform] Luma bei der Einhaltung von Vorschriften und beim verantwortungsvollen Marketing. Diese Steuerelemente sind flexibel und können an die Anforderungen der Sicherheits- und Governance-Teams von Luma angepasst werden, sodass sie sich auf regionale und organisatorische Anforderungen für die Verwaltung bekannter und unbekannter Kundendaten einstellen können.

<!--

### Data flow canvas

When you save, a visual data flow canvas shows the segment mapped from the unified profile to the three destinations you selected.

![image](assets/luma-flow.png)

-->

## Geräteübergreifende Identitätszuordnung

Sarah durchsucht eine Social-Media-Site auf ihrem Mobilgerät und sieht eine Anzeige von Luma. Diese erinnert sie an den Artikel, den sie im Warenkorb gelassen hat.

Später öffnet sie ihre E-Mail und sieht die Retargeting-Nachrichten. Sie wählt einen Link zu Luma aus einer E-Mail aus.

Über den Link gelangt Sarah zur mobilen Startseite von Luma, auf der ihr auf Grundlage von Adobe Target ein voll personalisiertes Erlebnis geboten wird.

* Sie wird als Bronze-Mitglied begrüßt.
* Sie sieht die &quot;Geschenk&quot;-Nachricht.
* Sie sieht auch die Meldung &quot;Kostenlose Geschenkverpackung&quot;, die Teil ihrer Bronze-Mitgliedschaft ist.
* Aufgrund ihrer Laufaffinität gehört sie im Hero Image weiterhin zur Zielgruppe.

Sie kauft das Shirt, fügt die Geschenkpackung hinzu und verfasst eine Karte zu dem Geschenk. Außerdem hat sie die Möglichkeit, dieses Ereignis zu speichern und im nächsten Jahr eine Erinnerung an das Besorgen eines neuen Geschenks zu erhalten. Sarah stimmt zu und ist für eine E-Mail-Kampagne im folgenden Jahr angemeldet, bei der sie daran erinnert wird, wieder ein Geschenk zu kaufen.

Dank der Funktionen für Zielgruppenunterdrückung wird Sarah nicht mehr in die Zielgruppe für dieses Herren-Shirt aufgenommen.

## Analysieren des Profils

Luma-Marketer verwenden Adobe Experience Platform, um sich die Geschenkgutachter-Zielgruppe im Real-Time CDP Dashboard anzusehen. Sie sehen die Ergebnisse dieser Initiative im Laufe der Zeit und erkennen, dass sie erfolgreich ist. Kunden reagieren auf Angebote und geben mehr Geld aus.

Diese Einblicke ermöglichen es Marketingexperten, auf dieses Signal zu reagieren, das durch die Verfügbarkeit dieser Daten in der Kundendatenplattform und die Anbindung von Kunden wie Sarah an die Zielgruppe ausgelöst wurde.

Mithilfe dieser Daten gelingt es Luma, die Loyalität und Kundenzufriedenheit zu steigern.
