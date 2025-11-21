---
keywords: RTCDP;CDP;Real-Time Customer Data Platform;Real-time Customer Data Platform;Real-time CDP;cdp;rtcdp
title: Erste Schritte mit Real-Time Customer Data Platform
description: Verwenden Sie dieses Szenario als Beispiel, wenn Sie Ihre Implementierung von Adobe Real-Time Customer Data Platform einrichten.
feature: Get Started, Use Cases
exl-id: 9f775d33-27a1-4a49-a4c5-6300726a531b
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2321'
ht-degree: 62%

---

# Erste Schritte mit Real-Time Customer Data Platform

Diese Anleitung führt Sie durch eine Beispielimplementierung von Real-Time Customer Data Platform (Real-Time CDP). Sie können sie bei der Einrichtung einer eigenen Implementierung als Muster verwenden. Zwar enthält das vorliegende Handbuch spezifische Beispiele, doch gibt es auch Links zu weiteren Informationen, die Sie bei der Einrichtung nutzen können.

Dieses Beispiel zeigt die Leistungsfähigkeit von Real-Time Customer Data Platform, powered by Adobe Experience Platform, für:

* Daten aus verschiedenen Quellen erfassen
* Zusammenführen zu einer einzigen [!DNL real-time customer profile]
* Ein konsistentes, relevantes und personalisiertes Erlebnis auf allen Geräten ermöglichen

## Anwendungsfall

Luma, ein Sportbekleidungsunternehmen, arbeitet kontinuierlich daran, sein Kundenerlebnis zu verbessern. Das Unternehmen verfügt über eine neue Initiative zur Steigerung der Geschenkumsätze. Außerdem soll übermäßige Kommunikation verringert werden (z. B. aufdringliche Anzeigen, die Kunden überall hin folgen).

Derzeit geben sie zu viel für Medien aus, die Elemente erneut ansprechen, die der Besucher in Zukunft nicht kaufen wird. Luma möchte beispielsweise niemanden erneut mit einem Artikel ansprechen, der als einmaliger Kauf für eine andere Person gedacht war.

Momentan sind die Daten von Luma auf verschiedene Quellen verteilt. Daher steht das Unternehmen vor großen Herausforderungen:

* Die Marketing-Abteilung muss mit verschiedenen Teams zusammenarbeiten, die jeweils für eine eigene Datenquelle verantwortlich sind (z. B. Website, App, Treuesysteme, CRM usw.).
* Wenn das Marketing-Team endlich Zugriff auf die Daten erhält, sind diese oft schon veraltet und für zeitsensible Kampagnen nicht mehr relevant.
* Es muss die Daten vereinheitlichen, damit diese auf Personen abzielen und nicht auf Kanäle.

Daher verfolgt Luma folgende Geschäftsziele:

* Erstellen einer einheitlichen Echtzeitansicht von Kunden auf Basis unterschiedlicher Datenquellen.
* Personalisieren von Marketing-Kampagnen mit relevanten Botschaften über verschiedene Kanäle und Geräte hinweg.

Um diese Ziele erreichen zu können, muss das Marketing-Team dazu in der Lage sein, Kundendaten in großem Umfang zu verwalten.

Mit Real-Time CDP, unterstützt durch Adobe Experience Platform, kann die Marketing-Organisation von Luma:

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

Beim Navigieren werden Daten in Echtzeit erfasst und nicht nur an eine Report Suite in Adobe Analytics, sondern auch direkt an Adobe Experience Platform gesendet. Beim Erfassen von Daten beginnen Sie, auf der Grundlage von Verhaltensdaten in [!DNL Experience Platform's real-time customer profile] eine einzige Ansicht des Verbrauchers zu erstellen.

Bei vielen Besuchern der Website handelt es sich wahrscheinlich um wiederkehrende Kunden, die zuvor bereits bei Luma gekauft haben.  Es ist wichtig, dass Luma Botschaften und Angebote personalisieren kann, um sowohl neue und wiederkehrende Besucher als auch bekannte Kunden anzusprechen.

### Erstbesuch eines neuen Kunden

Beispielsweise navigiert ein nicht identifizierter Besucher zum Bereich „Herren“ auf der Website von Luma und sieht sich einige laufende Sweatshirts an.

![Bild](assets/luma-sweatshirts.png)

Wenn der Kunde mehr über diese Produkte erfahren möchte, werden diese Produktansichten in Adobe Analytics erfasst und an [!DNL Experience Platform] gesendet.

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

Wenn man das Browsing-Verhalten des anonymen Besuchers im Herrenbereich der Site betrachtet, hätte man erwarten können, dass der Kunde männlich ist. Jetzt, da sie eingeloggt ist, erkennt Luma Sarah Rose. Luma nutzt die Leistungsfähigkeit der [!DNL Real-Time Customer Profile], um die Nachrichten, die ihr über verschiedene Kanäle zugestellt werden, zu verfeinern.

## Personalisierung des Kundenerlebnisses

Sarah wird mit einer Treuebotschaft begrüßt und ihr wird dafür gedankt, dass sie Bronze-Mitglied ist. Zudem erhält sie weitere Informationen zu Vorteilen und dazu, wie sie ihren Status und Punktestand verbessern kann.

Sie navigiert zur Startseite, um weitere Informationen zu erhalten.

![Bild](assets/luma-personal.png)

Sarah erhält ein personalisiertes Startseitenerlebnis, das dynamisch bereitgestellt wird und auf ihrer [!DNL Real-Time Customer Profile] in Adobe Experience Platform basiert.

Dank der Adobe Sensei-basierten Personalisierung in Adobe Target, bei der ihre bisherigen Käufe sowie ihre Affinität für Laufbekleidung und -ausrüstung berücksichtigt werden, werden ihr relevante Inhalte angezeigt. Luma schneidet den Katalog für Herren auch auf der Grundlage ihres letzten Browsers auf Laufausrüstung für Männer an.

Weiter unten auf der Seite werden Sarah vorgestellte Produkte sowie eine Ablage mit neuen Empfehlungen angezeigt, die auf ihren zuletzt angezeigten Artikeln basieren.

Diese personalisierten Inhalte helfen Sarah dabei, rasch passende Artikel zu finden. Dadurch wird die Konversionsrate verbessert und ein angenehmeres Kundenerlebnis entsteht.

### Den Kunden zurückholen

Sarah wird abgelenkt und verlässt die Site, wodurch ihre Sitzung beendet wird. Luma kann ihre Daten in Adobe Experience Platform verwenden, um sie zurück auf die Site zu holen.

Real-Time Customer Data Platform basiert auf Adobe Experience Platform und wurde für das Customer Experience Management entwickelt. Mit ihrer Hilfe können Unternehmen folgende Aufgaben erledigen:

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

Verwenden Sie [!DNL Real-Time Customer Data Platform], um neue Datenquellen in Experience Platform zu importieren. Real-Time CDP enthält einen Katalog von Datenquellen, die schnell und einfach zum Profil hinzugefügt werden können.

![Bild](assets/luma-source-cat.png)

Um beispielsweise die CRM-Daten von Luma aufzunehmen, filtern Sie den Katalog nach *CRM* und alle nativen Connectoren, die *CRM* enthalten, werden aufgelistet. So fügen Sie [!DNL Microsoft Dynamics CRM] hinzu:

1. Lassen Sie die Verbindung zu.

   ![Bild](assets/luma-source-auth.png)

1. Wählen Sie aus einer Empfehlungsliste mit vorab zugeordneten XDM-Tabellen aus, um zu entscheiden, was Sie importieren möchten.

   <!--    ![image](assets/luma-source-import.png) -->

   Wählen Sie beispielsweise **[!UICONTROL Contacts]** aus. Eine Vorschau der Kontaktdaten wird automatisch geladen, damit Sie überprüfen können, ob alles wie erwartet aussieht.

   Real-Time CDP übernimmt einen Großteil der manuellen Arbeit bei diesem Prozess, indem Standardfelder automatisch dem [!DNL Experience Data Model] (XDM)-Profilschema zugeordnet werden.

1. Überprüfen Sie die Feldzuweisungen.

   <!--    ![image](assets/luma-source-mapping.png) -->

   Prüfen Sie beispielsweise, ob das E-Mail-Feld für Kontakte richtig zugeordnet ist.\
   Sie haben die Möglichkeit, eine Vorschau der Daten anzuzeigen und eine erweiterte Zuordnung vorzunehmen.

1. Legen Sie einen Zeitplan fest.

   ![Bild](assets/luma-source-sched.png)

Damit ist der Vorgang abgeschlossen. Sie haben soeben [!DNL Microsoft CRM] als Datenquelle zu [!DNL Experience Platform] hinzugefügt.

### Bezeichnen von erfassten Daten für Nutzungsrichtlinien

Luma hat viele interne Richtlinien, die die Nutzung bestimmter Arten von erfassten Informationen einschränken und auch rechtlichen und datenschutzrechtlichen Vorgaben bezüglich der Nutzung von Daten entsprechen müssen. Mit Data Governance in Adobe Experience Platform können vordefinierte Datennutzungsbezeichnungen auf Datensätze (und bestimmte Felder in diesen Datensätzen) angewendet werden, sodass Luma die Daten nach bestimmten Nutzungsbeschränkungen kategorisieren kann.

![](assets/governance-labels.png)

Sobald die Datennutzungs-Labels angewendet wurden, kann Luma dann Data Governance verwenden, um Datennutzungsrichtlinien zu erstellen. Datennutzungsrichtlinien sind Regeln, die beschreiben, welche Arten von Aktionen Sie für Daten ausführen dürfen, die bestimmte Labels enthalten. Beim Versuch, eine Aktion in Real-Time CDP durchzuführen, die einen Richtlinienverstoß darstellt, wird die Aktion verhindert und ein Warnhinweis ausgegeben, der angibt, welche Richtlinie verletzt wurde und warum.

Darüber hinaus Real-Time CDP

## Zusammenführen der Daten für einen bestimmten Kunden

Durchsuchen Sie in diesem Szenario Profile nach Sarah Rose. Ihr Profil erscheint mit der E-Mail-Adresse, die sie zum Anmelden verwendet hat.

<!-- ![image](assets/luma-find-profile.png) -->

Alle Profilinformationen, die Luma zu Sarah hat, werden angezeigt. Dazu gehören ihre persönlichen Informationen wie Adresse und Telefonnummer, Kommunikationsvoreinstellungen und die Zielgruppen, für die sie qualifiziert ist.

| Kategorie | Beschreibung |
|---|---|
| Identitäten | Zeigt die Identitäten, die in [!DNL Experience Platform] aus Sarahs Interaktionen mit Luma über Kanäle und Geräte hinweg miteinander verknüpft wurden. Ihre ECID von der Website wird angezeigt. Zu ihrer Identität gehören auch die ECID aus ihrer Mobile App, ihre E-Mail-ID, eine CRM-ID aus dem kürzlich hinzugefügten [!DNL Microsoft Dynamics]-Datensatz und eine Treueprogramm-ID, die vom Luma-Treuesystem an Adobe Experience Platform übergeben wurde. |
| Ereignisse | Zeigt alle Interaktionsdaten von Sarah mit der Marke Luma an. Dazu gehören der Artikel, den sie gerade angesehen hat, alles, was Sarah in der Vergangenheit angesehen hat, die E-Mails, die sie erhalten hat, ihre Interaktionen mit dem Callcenter sowie Daten darüber, auf welchem Kanal und welchem Gerät die einzelnen Interaktionen stattgefunden haben. |

Das Real-Time CDP-Profil reduziert den Workflow des Marketing-Teams von Luma von Wochen auf Minuten und erschließt Personalisierungsmöglichkeiten, die auf dieser 360-Grad-Kundenansicht basieren. Das Profil führt die Verhaltensdaten, die erfasst wurden, als sie die Site vor dem Anmelden durchsucht hat, mit ihrem bestehenden Kundenprofil zusammen und erlaubt so einen genauen Überblick über Sarah.

Das Marketing-Team kann diese erweiterte [!DNL Real-Time Customer Profile] nutzen, um Sarahs Erfahrung besser zu personalisieren und ihre Markentreue mit Luma zu steigern.

## Zielgruppen

Die leistungsstarken Segmentierungsfunktionen von Adobe Experience Platform ermöglichen es Marketing-Experten, Attribute, Ereignisse und bestehende Zielgruppen basierend auf den im [!DNL Real-Time Customer Profile] erfassten Daten zu kombinieren.

<!-- ![image](assets/luma-segments.png) -->

In diesem Szenario weisen Sarahs letzte Interaktionen auf der Site auf ein anderes Verhalten als bei ihren vergangenen Aktionen hin. Sarah kauft normalerweise Damenkleidung. Der Artikel in ihrem Warenkorb ist jedoch ein großes Herren-Sweatshirt.

Das Data-Science-Team von Luma hat Modelle zur Kauftendenz entwickelt. Ein Modell identifiziert eine plötzliche Änderung bei der Bekleidungskategorie (z. B. Herren/Damen) oder der Größe für den bestehenden Kunden. Sarahs verändertes Kaufverhalten legt nahe, dass sie nicht für sich selbst einkauft.

<!-- ![image](assets/luma-gift.png) -->

### Definieren einer Audience

Verwenden Sie die verschiedenen Optionen für die visuelle Komposition oder den Code-basierten Ausdruckseditor im Zielgruppen-Arbeitsbereich, um eine Zielgruppe zu ändern oder zu erstellen, die Warenkorbabgänger darstellt, die anscheinend gerade dabei sind, ein Geschenk zu kaufen:

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

Wenn Sie die Zielgruppe „Geschenk-Warenkorbabgänger“ hinzugefügt haben, können Sie ungefähr sehen, wie viele Personen zu dieser Zielgruppe gehören. Sie können aktiv werden und es für Personalisierungszwecke kanalübergreifend bereitstellen.

Wählen Sie **[!UICONTROL Send to destinations]** aus.

In Real-Time CDP kann Luma Personalisierungen an seinen Zielgruppen nahtlos durchführen.\
Hier sehen Sie alle Ziele, an die Luma dieses Ziel senden kann, sowohl Adobe- als auch Nicht-Adobe-Lösungen:

![Bild](assets/luma-dest.png)

### Auswählen von Zielen

In diesem Szenario möchte Luma die Zielgruppe mit Personalisierung über folgende Ziele hinweg erneut ansprechen:

* Google, für Anzeige
  <!--* Facebook -->
* Adobe Campaign, für E-Mail

<!-- ![image](assets/luma-sched-dest.png) -->

### Planen von Zielen

Sie können auch festlegen, dass der Zielgruppenexport zu einem bestimmten Zeitpunkt gestartet oder beendet wird. Die Zielgruppe wird veröffentlicht und zu den geplanten Terminen automatisch auf den konfigurierten Plattformen aktualisiert.

>[!NOTE]
>
>Wenn Sie das Datumsfeld auswählen, wird optional automatisch ein 90-tägiges Timeout geplant.

Wählen Sie **[!UICONTROL Save]** aus, um zur nächsten Seite zu wechseln.

Wenn ein Kunde in dieser Zielgruppe einen Kauf tätigt, wird seine Zugehörigkeit zu dieser Zielgruppe in Echtzeit unterdrückt. Sie qualifizieren sich nicht mehr, weil sich ihr Status geändert hat.

Das spart dem Direktor des Medien-Teams von Luma Hunderttausende von Dollar, da er Inventar nicht für eine Zielgruppe verwenden muss, die gar nicht qualifiziert ist.

### Durchsetzung von Datennutzungsrichtlinien für Ziele

Adobe Experience Platform umfasst Datenschutz- und Sicherheitskontrollen, mit denen festgestellt wird, ob eine Zielgruppe für ein bestimmtes Ziel aktiviert werden kann. Die Aktivierung ist je nach Marketing-Zweck, der dem Ziel beim Erstellen zugewiesen wurde, sowie den von Ihrem Unternehmen festgelegten Datennutzungsrichtlinien aktiviert oder eingeschränkt.

Wenn Ihre Aktivität gegen eine Richtlinie verstößt, wird eine Warnmeldung angezeigt. Diese Warnmeldung enthält Informationen zur Datenherkunft, mit denen Sie erkennen können, wie gegen die Richtlinie verstoßen wurde und was Sie tun können, um den Verstoß zu beheben.

Mit diesen Kontrollen unterstützt [!DNL Experience Platform] Luma bei der Einhaltung von Vorschriften und bei der verantwortungsvollen Vermarktung. Diese Steuerelemente sind flexibel und können an die Anforderungen der Sicherheits- und Governance-Teams von Luma angepasst werden, sodass sie zuverlässig die regionalen und organisatorischen Anforderungen für die Verwaltung bekannter und unbekannter Kundendaten erfüllen können.

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
* Sie sieht die „Geschenk-Nachricht“.
* Sie sieht auch die „Free Gift Wrap“-Nachricht, die Teil ihrer Bronze-Mitgliedsvorteile ist.
* Aufgrund ihrer Laufaffinität gehört sie im Hero Image weiterhin zur Zielgruppe.

Sie kauft das Shirt, fügt die Geschenkpackung hinzu und verfasst eine Karte zu dem Geschenk. Außerdem hat sie die Möglichkeit, dieses Ereignis zu speichern und im nächsten Jahr eine Erinnerung an das Besorgen eines neuen Geschenks zu erhalten. Sarah stimmt zu und ist für eine E-Mail-Kampagne im folgenden Jahr angemeldet, bei der sie daran erinnert wird, wieder ein Geschenk zu kaufen.

Dank der Funktionen für Zielgruppenunterdrückung wird Sarah nicht mehr in die Zielgruppe für dieses Herren-Shirt aufgenommen.

## Analysieren des Profils

Luma-Marketing-Experten verwenden Adobe Experience Platform, um die Zielgruppe der Geschenkgeber im Real-Time CDP-Dashboard anzuzeigen. Sie sehen die Ergebnisse dieser Initiative im Laufe der Zeit und erkennen, dass sie erfolgreich ist. Kunden reagieren auf Angebote und geben mehr Geld aus.

Diese Einblicke ermöglichen es den Marketing-Experten, auf dieses Signal zu reagieren, das dadurch angeheizt wurde, dass diese Daten in CDP verfügbar waren und Kunden wie Sarah an die Zielgruppe angehängt wurden.

Mithilfe dieser Daten gelingt es Luma, die Treue und Kundenzufriedenheit zu steigern.
