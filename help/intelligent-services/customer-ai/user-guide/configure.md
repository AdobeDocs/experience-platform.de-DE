---
keywords: Experience Platform;Benutzerhandbuch;Kunden-KI;beliebte Themen;Instanz konfigurieren;Instanz erstellen;
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Konfigurieren einer Kunden-KI-Instanz
description: KI-/ML-Services bieten Kunden-KI als benutzerfreundlichen Adobe Sensei-Service, der für verschiedene Anwendungsfälle konfiguriert werden kann. Die folgenden Abschnitte enthalten Schritte zum Konfigurieren einer Instanz von Customer AI.
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
source-git-commit: 73dea391f8fcb1d2d491c814b453afb4e538459d
workflow-type: tm+mt
source-wordcount: '3092'
ht-degree: 7%

---


# Konfigurieren einer Customer AI-Instanz

Kunden-KI als Teil von KI-/ML-Services ermöglicht es Ihnen, benutzerdefinierte Tendenzwerte zu generieren, ohne sich über maschinelles Lernen Gedanken machen zu müssen.

KI-/ML-Services bieten Kunden-KI als benutzerfreundlichen Adobe Sensei-Service, der für verschiedene Anwendungsfälle konfiguriert werden kann. Die folgenden Abschnitte enthalten Schritte zum Konfigurieren einer Instanz von Customer AI.

## Instanz erstellen {#set-up-your-instance}

Wählen Sie in der Benutzeroberfläche von Experience Platform **[!UICONTROL Services]** im linken Navigationsbereich aus. Der Browser für **[!UICONTROL Dienste]** erscheint und zeigt alle Dienste an, die Ihnen zur Verfügung stehen. Wählen Sie im Container für Kunden-KI **[!UICONTROL Öffnen]** aus.

![Navigieren Sie in der Experience Platform-Benutzeroberfläche zum Kunden-KI-Service.](../images/user-guide/navigate-to-service.png)

Die **Kunden-KI**-Benutzeroberfläche wird angezeigt und zeigt alle Ihre Service-Instanzen an.

- Die Metrik **[!UICONTROL Gesamtzahl der bewerteten Profile]** befindet sich unten rechts im Container **[!UICONTROL Instanz erstellen]**. Diese Metrik verfolgt die Gesamtzahl der von Kunden-KI im aktuellen Kalenderjahr bewerteten Profile, einschließlich aller Sandbox-Umgebungen und gelöschter Service-Instanzen.

![Metrik für insgesamt bewertete Profile in Kunden-KI.](../images/user-guide/total-profiles.png)

Dienstinstanzen können mithilfe der Steuerelemente auf der rechten Seite der Benutzeroberfläche bearbeitet, geklont und gelöscht werden. Um diese Steuerelemente anzuzeigen, wählen Sie eine Instanz aus Ihren vorhandenen **[!UICONTROL Service-Instanzen]** aus. Die Steuerelemente enthalten Folgendes:

- **[!UICONTROL Bearbeiten]**: Wenn Sie **[!UICONTROL Bearbeiten]** auswählen, können Sie eine vorhandene Service-Instanz ändern. Sie können den Namen, die Beschreibung und die Bewertungsfrequenz der Instanz bearbeiten.
- **[!UICONTROL Klonen]**: Wenn Sie **[!UICONTROL Klonen]** auswählen, wird die aktuell ausgewählte Dienstinstanz-Einrichtung kopiert. Anschließend können Sie den Workflow ändern, um kleinere Anpassungen vorzunehmen, und ihn in eine neue Instanz umbenennen.
- **[!UICONTROL Löschen]**: Sie können eine Service-Instanz einschließlich aller historischen Ausführungen löschen. Der entsprechende Ausgabedatensatz wird aus Experience Platform gelöscht. Scores, die mit dem Echtzeit-Kundenprofil synchronisiert wurden, werden jedoch nicht gelöscht.
- **[!UICONTROL Datenquelle]**: Ein Link zu dem von dieser Instanz verwendeten Datensatz. Wenn mehrere Datensätze verwendet werden, wird durch Auswahl des Hyperlink-Texts das Popover für die Datensatzvorschau geöffnet.
- **[!UICONTROL Details des letzten Durchgangs]**: Wird nur angezeigt, wenn ein Durchgang fehlschlägt. Hier werden Informationen darüber angezeigt, warum der Durchlauf fehlgeschlagen ist, z. B. Fehlercodes.
- **[!UICONTROL Score-Definition]**: Ein kurzer Überblick über das Ziel, das Sie für diese Instanz konfiguriert haben.

![Bedienfeld „Service-Instanz“ in Kunden-KI.](../images/user-guide/service-instance-panel.png)

Um eine neue Instanz zu erstellen, wählen Sie **[!UICONTROL Instanz erstellen]** aus.

![Dashboard der Kunden-KI mit einer Übersicht über Service-Instanzen und ihre Status.](../images/user-guide/dashboard.png)

## Einrichten

Der Workflow zur Instanzerstellung wird angezeigt, beginnend mit dem Schritt **[!UICONTROL Einrichten]**.

Im Folgenden finden Sie wichtige Informationen zu Werten, die Sie für die Instanz angeben müssen:

-**[!UICONTROL Name]:** Der Name der Instanz wird überall dort verwendet, wo Kunden-KI-Bewertungen angezeigt werden. Daher sollten Namen beschreiben, was die Prognosewerte darstellen. Beispiel: „Wahrscheinlichkeit, ein Zeitschriftenabo zu stornieren“.

-**[!UICONTROL description]:** Eine Beschreibung, die angibt, was vorhergesagt werden soll.

-**[!UICONTROL Neigungstyp]:** Der Neigungstyp bestimmt die Absicht des Scores und die Metrikpolarität. Sie können entweder **[!UICONTROL Abwanderung]** oder **[!UICONTROL Konversion]** wählen. Weitere Informationen darüber, wie sich der Tendenztyp auf Ihre Instanz auswirkt, finden Sie in der [Auswertungszusammenfassung](./discover-insights.md#scoring-summary) im Discover Insight-Dokument.

![Setup-Bildschirm mit dem Workflow zur Instanzerstellung in Kunden-KI.](../images/user-guide/create-instance.png)

Geben Sie die erforderlichen Werte ein und wählen Sie dann **[!UICONTROL Weiter]**, um fortzufahren.

## Daten auswählen {#select-data}

Standardmäßig verwendet Kunden-KI Adobe Analytics, Adobe Audience Manager, Erlebnisereignisse im Allgemeinen und Kundenerlebnisereignisdaten, um Tendenzwerte zu berechnen. Bei der Auswahl eines Datensatzes werden nur diejenigen aufgelistet, die mit Kunden-KI kompatibel sind. Um einen Datensatz auszuwählen, klicken Sie auf das Symbol (**+**) neben dem Datensatznamen oder aktivieren Sie das Kontrollkästchen, um mehrere Datensätze gleichzeitig hinzuzufügen. Verwenden Sie die Suchoption, um die Datensätze, die Sie interessieren, schnell zu finden.

![Bildschirm zur Datensatzauswahl mit Suchleiste und hervorgehobenen Speicheroptionen.](../images/user-guide/configure-dataset-page-save-and-exit-cai.png)

Nachdem Sie die gewünschten Datensätze ausgewählt haben, klicken Sie auf die Schaltfläche **[!UICONTROL Hinzufügen]**, um die Datensätze zum Bereich für die Datensatzvorschau hinzuzufügen.

![Bildschirm zur Datensatzauswahl mit ausgewählten Datensätzen im Vorschaubereich.](../images/user-guide/select-datasets.png)

Wenn Sie das Informationssymbol ![Informationssymbol](/help/images/icons/info.png) neben dem Datensatz auswählen, wird das Popover für die Datensatzvorschau geöffnet.

![Bildschirm zur Datensatzauswahl mit Suchleiste und Datensatzinformationen.](../images/user-guide/dataset-info.png)

Die Datensatzvorschau enthält Daten wie die Zeit der letzten Aktualisierung, das Quellschema und eine Vorschau der ersten zehn Spalten.

Wählen Sie **[!UICONTROL Speichern]**, um Ihre Entwürfe zu speichern, während Sie den Workflow durchlaufen. Sie können auch Modellkonfigurationen von Entwürfen speichern und zum nächsten Schritt im Workflow wechseln. Verwenden Sie **[!UICONTROL Speichern und fortfahren]** um Entwürfe während der Modellkonfigurationen zu erstellen und zu speichern. Mit der Funktion können Sie Entwürfe der Modellkonfiguration erstellen und speichern. Dies ist besonders nützlich, wenn Sie viele Felder im Konfigurations-Workflow definieren müssen.

![Der Workflow „Erstellen“ auf der Registerkarte „Kunden-KI von Data Science Services“ mit den hervorgehobenen Optionen „Speichern und speichern und fortfahren“.](../images/user-guide/cai-save-and-exit.png)

### Datensatz-Vollständigkeit {#dataset-completeness}

In der Datensatzvorschau gibt es einen Prozentwert für die Vollständigkeit des Datensatzes . Dieser Wert bietet einen schnellen Schnappschuss davon, wie viele Spalten in Ihrem Datensatz leer/null sind. Wenn ein Datensatz viele fehlende Werte enthält und diese Werte an anderer Stelle erfasst werden, wird dringend empfohlen, den Datensatz mit den fehlenden Werten einzubeziehen. In diesem Beispiel ist die Personen-ID leer. Die Personen-ID wird jedoch in einem separaten Datensatz erfasst, der einbezogen werden kann.

>[!NOTE]
>
>Die Vollständigkeit des Datensatzes wird anhand des maximalen Trainings-Fensters für Kunden-KI (ein Jahr) berechnet. Das bedeutet, dass Daten, die älter als ein Jahr sind, beim Anzeigen Ihres Datensatzvollständigkeitswerts nicht berücksichtigt werden.

![Vollständigkeit des Datensatzes mit hervorgehobener Datensatzvorschau mit Prozentwert der Vollständigkeit.](../images/user-guide/dataset-info-2.png)

### Identität auswählen {#identity}

Sie können jetzt mehrere Datensätze anhand der Identitätszuordnung (Feld) miteinander verbinden. Sie müssen einen Identitätstyp (auch als „Identity-Namespace“ bezeichnet) und einen Identitätswert innerhalb dieses Namespace auswählen. Wenn Sie innerhalb Ihres Schemas unter demselben Namespace mehr als ein Feld als Identität zugewiesen haben, werden alle zugewiesenen Identitätswerte in der Dropdown-Liste Identität mit vorangestelltem Namespace angezeigt, z. B. `EMAIL (personalEmail.address)` oder `EMAIL (workEmail.address)`.

![Auswahlbildschirm der Identitätszuordnung mit demselben Namespace, der für mehrere Datensätze ausgewählt wird.](../images/user-guide/cai-identity-map.png)

>[!IMPORTANT]
>
>Für jeden ausgewählten Datensatz muss derselbe Identitätstyp (Namespace) verwendet werden. Neben dem Identitätstyp wird in der Identitätsspalte ein grünes Häkchen angezeigt, das angibt, dass Datensätze kompatibel sind. Wenn Sie beispielsweise den Namespace Telefon und `mobilePhone.number` als Kennung verwenden, müssen alle Kennungen für die übrigen Datensätze den Namespace Telefon enthalten und verwenden.

Um eine Identität auszuwählen, wählen Sie den unterstrichenen Wert in der Spalte Identität aus. Das Pop-up Identität auswählen wird angezeigt.

![Auswahlbildschirm der Identitätszuordnung mit demselben Namespace, der für mehrere Datensätze ausgewählt wird.](../images/user-guide/cai-identity-namespace.png)

Falls in einem Namespace mehr als eine Identität verfügbar ist, stellen Sie sicher, dass Sie das richtige Identitätsfeld für Ihren Anwendungsfall auswählen. Im E-Mail-Namespace sind beispielsweise zwei E-Mail-Identitäten verfügbar: eine geschäftliche und eine persönliche E-Mail. Je nach Anwendungsfall ist eine persönliche E-Mail mit größerer Wahrscheinlichkeit ausgefüllt und kann für individuelle Prognosen nützlicher sein. Dies bedeutet, dass `EMAIL (personalEmail.address)` als Identität ausgewählt wird.

![Beispiel mit einem nicht ausgewählten Datensatz-Schlüssel im Auswahlbildschirm der Identitätszuordnung.](../images/user-guide/select-identity.png)

>[!NOTE]
>
> Wenn für einen Datensatz kein gültiger Identitätstyp (Namespace) vorhanden ist, müssen Sie eine primäre Identität festlegen und sie mithilfe des [-Editors einem Identity-Namespace ](../../../xdm/schema/composition.md#identity). Weitere Informationen zu Namespaces und Identitäten finden Sie in der Dokumentation [Identity Service-Namespaces](../../../identity-service/features/namespaces.md) .

## Ziel definieren {#define-a-goal}

Der **[!UICONTROL Ziel definieren]** wird angezeigt und bietet eine interaktive Umgebung, in der Sie ein Prognoseziel visuell definieren können. Ein Ziel besteht aus einem oder mehreren Ereignissen, bei denen das Auftreten eines jeden Ereignisses auf der Bedingung basiert, die es enthält. Ziel einer Customer AI-Instanz ist es, die Wahrscheinlichkeit zu bestimmen, mit der ihr Ziel innerhalb eines bestimmten Zeitraums erreicht wird.

Um ein Ziel zu erstellen, wählen **[!UICONTROL Feldnamen eingeben]** und dann ein Feld aus der Dropdown-Liste aus. Wählen Sie die zweite Eingabe aus, eine -Klausel für die Bedingung des Ereignisses, und geben Sie dann optional den Zielwert an, um das Ereignis abzuschließen. Weitere Ereignisse können durch Auswahl von „Ereignis hinzufügen **[!UICONTROL konfiguriert]**. Schließen Sie abschließend das Ziel ab, indem Sie einen Prognosezeitrahmen in der Anzahl der Tage anwenden, und wählen Sie dann **[!UICONTROL Weiter]** aus.

![Definieren des Zielschritts in Kunden-KI, die die interaktive Umgebung zur Definition eines Prognoseziels anzeigt.](../images/user-guide/cai-define-a-goal.png)

### Passiert und findet nicht statt

Bei der Definition Ihres Ziels haben Sie die Möglichkeit, **[!UICONTROL Wird auftreten]** oder **[!UICONTROL Wird nicht auftreten]** auszuwählen. Wenn Sie **[!UICONTROL Wird auftreten]** auswählen, müssen die von Ihnen definierten Ereignisbedingungen erfüllt sein, damit die Ereignisdaten eines Kunden in die Insights-Benutzeroberfläche aufgenommen werden.

Wenn Sie beispielsweise eine App einrichten möchten, um vorherzusagen, ob eine Kundin oder ein Kunde einen Kauf tätigt, können Sie **[!UICONTROL Wird eintreten]** gefolgt von **[!UICONTROL Alle von]** auswählen und dann **commerce.purchases.id** (oder ein ähnliches Feld) und **[!UICONTROL exists]** als Operator eingeben.

<!-- ![will occur](../images/user-guide/occur.png) -->
![Ein Beispiel, das die Konfiguration eines Ziels zeigt, bei dem ein Ereignis eintritt.](../images/user-guide/cai-will-occur.png)

Es kann jedoch Fälle geben, in denen Sie vorhersagen möchten, ob ein Ereignis in einem bestimmten Zeitraum nicht eintreten wird. Um ein Ziel mit dieser Option zu konfigurieren, wählen Sie **[!UICONTROL Wird nicht auftreten]** aus der Dropdown-Liste der obersten Ebene aus.

Wenn Sie beispielsweise vorhersagen möchten, welche Kundinnen und Kunden weniger interagieren und Ihre Konto-Anmeldeseite im nächsten Monat nicht besuchen werden, Wählen Sie **[!UICONTROL Wird nicht auftreten]** gefolgt von **[!UICONTROL Alle von]** und geben Sie dann **web.webInteraction.URL** (oder ein ähnliches Feld) und **[!UICONTROL gleich]** als Operator mit **account-login** als Wert ein.

![Ein Beispiel, das die Konfiguration eines Ziels zeigt, bei dem kein Ereignis eintritt.](../images/user-guide/not-occur.png)

### Alle und alle von

In einigen Fällen möchten Sie möglicherweise vorhersagen, ob eine Kombination von Ereignissen eintritt, in anderen Fällen möchten Sie das Auftreten eines beliebigen Ereignisses aus einem vordefinierten Satz vorhersagen. Um vorherzusagen, ob eine Kundin oder ein Kunde über eine Kombination von Ereignissen verfügt, wählen Sie die Option **[!UICONTROL Alle von]** aus der Dropdown-Liste der zweiten Ebene auf der Seite **[!UICONTROL Ziel definieren]** aus.

Beispielsweise können Sie vorhersagen, ob eine Kundin oder ein Kunde ein bestimmtes Produkt kauft. Dieses Prognoseziel wird durch zwei Bedingungen definiert: einen `commerce.order.purchaseID` **vorhanden** und den `productListItems.SKU` **gleich** bestimmten Wert.

![Ein Beispiel, das die Konfiguration eines Ziels zeigt, bei dem alle Bedingungen erfüllt sein müssen.](../images/user-guide/all-of.png)

Um vorherzusagen, ob ein Kunde ein Ereignis aus einem bestimmten Satz haben wird, können Sie die Option **[!UICONTROL Beliebig von]** verwenden.

Beispielsweise können Sie vorhersagen, ob eine Kundin oder ein Kunde eine bestimmte URL oder eine Webseite mit einem bestimmten Namen besucht. Dieses Prognoseziel wird durch zwei Bedingungen definiert: `web.webPageDetails.URL` **beginnt mit** einem bestimmten Wert und `web.webPageDetails.name` **beginnt mit** einem bestimmten Wert.

![Ein Beispiel, das die Konfiguration eines Ziels zeigt, bei dem eine beliebige Bedingung erfüllt werden kann.](../images/user-guide/any-of.png)

### Geeignete Population *(optional)*

Standardmäßig werden Tendenzwerte für alle Profile generiert, es sei denn, es wurde eine qualifizierte Zielgruppe angegeben. Sie können eine qualifizierte Zielgruppe angeben, indem Sie Bedingungen festlegen, um Profile auf Grundlage von Ereignissen ein- oder auszuschließen.

![Ein Beispiel für die Konfiguration einer auswählbaren Population in Kunden-KI.](../images/user-guide/eligible-population.png)

### Benutzerspezifische Ereignisse (*optional*) {#custom-events}

Wenn Sie zusätzlich zu den [Standardereignisfeldern“, die von Kunden-KI ](../data-requirements.md#standard-events) Generieren von Tendenz-Scores verwendet werden, über zusätzliche Informationen verfügen, wird eine Option für benutzerdefinierte Ereignisse bereitgestellt. Mit dieser Option können Sie zusätzliche Ereignisse hinzufügen, die Sie als einflussreich erachten, was die Qualität Ihres Modells verbessern und zu genaueren Ergebnissen führen kann. Wenn der ausgewählte Datensatz benutzerdefinierte Ereignisse enthält, die in Ihrem Schema definiert sind, können Sie sie zu Ihrer Instanz hinzufügen.

>[!NOTE]
>
> Eine ausführliche Erläuterung der Auswirkungen benutzerdefinierter Ereignisse auf die Ergebnisse der Kunden-KI-Bewertung finden Sie [ Abschnitt „Beispiel für benutzerdefiniertes ](#custom-event)&quot;.

![Ein Beispiel für die Konfiguration einer Ereignisfunktion in Kunden-KI.](../images/user-guide/event-feature.png)

Um ein benutzerdefiniertes Ereignis hinzuzufügen, wählen Sie **[!UICONTROL Benutzerdefiniertes Ereignis hinzufügen]** aus. Geben Sie als Nächstes einen benutzerdefinierten Ereignisnamen ein und ordnen Sie ihn dann dem Ereignisfeld in Ihrem Schema zu. Bei der Betrachtung von Einflussfaktoren und anderen Einblicken werden benutzerdefinierte Ereignisnamen anstelle der Feldwerte angezeigt. Das bedeutet, dass der benutzerdefinierte Ereignisname anstelle der ID/des Werts des Ereignisses verwendet wird. Weitere Informationen zur Anzeige benutzerdefinierter Ereignisse finden Sie [ Abschnitt „Beispiel für benutzerdefiniertes Ereignis](#custom-event). Diese zusätzlichen benutzerspezifischen Ereignisse werden von Kunden-KI verwendet, um die Qualität Ihres Modells zu verbessern und genauere Ergebnisse zu liefern.

![Ein Beispiel für die Konfiguration eines benutzerdefinierten Ereignisfelds in Kunden-KI.](../images/user-guide/custom-event.png)

Wählen Sie anschließend den gewünschten Operator aus der Dropdown-Liste Verfügbare Operatoren aus. Es werden nur mit dem Ereignis kompatible Operatoren aufgelistet.

![Ein Beispiel mit den verfügbaren Operatoren zum Konfigurieren eines benutzerdefinierten Ereignisses in Kunden-KI.](../images/user-guide/custom-operator.png)

Geben Sie abschließend die Feldwerte ein, sofern der ausgewählte Operator einen benötigt. In diesem Beispiel müssen wir nur sehen, ob eine Hotel- oder Restaurantreservierung vorhanden ist. Wenn wir jedoch genauer sein wollten, konnten wir den Operator Gleich verwenden und einen exakten Wert in die Eingabeaufforderung eingeben.

![Ein Beispiel für die Konfiguration eines benutzerdefinierten Ereignisfeldwerts in Kunden-KI.](../images/user-guide/custom-value.png)

Klicken Sie nach Abschluss **[!UICONTROL oben rechts]** „Weiter“, um fortzufahren.

### Benutzerdefinierte Profilattribute (*optional*)

Zusätzlich zu den [Standardereignisfeldern“, die von Kunden-KI zum Generieren von Tendenz-Scores verwendet werden, können Sie wichtige Profildatensatzfelder (mit Zeitstempeln](../data-requirements.md#standard-events) in Ihren Daten definieren. Mit dieser Option können Sie zusätzliche, von Ihnen als einflussreich erachtete Profilattribute hinzufügen, was die Qualität Ihres Modells verbessern und genauere Ergebnisse liefern kann. Darüber hinaus können Kunden-KI durch das Hinzufügen benutzerdefinierter Profilattribute besser darstellen, wie bestimmte Profile in einem Neigungs-Bucket endeten.

>[!NOTE]
>
>Das Hinzufügen eines benutzerdefinierten Profilattributs folgt demselben Workflow wie das Hinzufügen eines benutzerdefinierten Ereignisses. Ähnlich wie benutzerdefinierte Ereignisse wirken sich benutzerdefinierte Profilattribute auf die gleiche Weise auf die Bewertung Ihres Modells aus. Eine ausführliche Erläuterung finden Sie im Abschnitt [Beispiel für ein benutzerdefiniertes ](#custom-event)).

![Ein Beispiel für die Konfiguration eines benutzerdefinierten Profilattributs in Kunden-KI.](../images/user-guide/profile-attributes.png)

#### Wählen Sie Profilattribute aus dem Export von Profilschnappschüssen aus

Sie können auch wählen, Profilattribute aus dem täglichen Profil-Schnappschuss-Export einzubeziehen. Diese Attribute werden mit dem Profil-Schnappschuss-Export synchronisiert und zeigen den zuletzt verfügbaren Wert an. Sie werden automatisch angezeigt und erfordern nicht, dass im Konfigurationsschritt ein Datensatz ausgewählt wird.

>[!WARNING]
>
> Wählen Sie kein Profilattribut aus, das infolge des Prognoseziels aktualisiert wurde oder stark mit dem Prognoseziel korreliert. Dies führt zu Datenlecks und Überanpassung des Modells. Beispielsweise ist `total_purchases_in_the_last_3_months` ein Attribut, das eine Kaufkonvertierung vorhersagt.

### Beispiel für ein benutzerdefiniertes Ereignis hinzufügen {#custom-event}

Im folgenden Beispiel werden ein benutzerdefiniertes Ereignis und Profilattribut zu einer Kunden-KI-Instanz hinzugefügt. Das Ziel der Customer AI-Instanz ist es, die Wahrscheinlichkeit vorherzusagen, mit der ein Kunde in den nächsten 60 Tagen ein anderes Luma-Produkt kaufen wird. Normalerweise sind Produktdaten mit einer Produkt-SKU verknüpft. In diesem Fall ist die SKU `prd1013`. Nachdem das Kunden-KI-Modell trainiert/bewertet wurde, kann diese SKU mit einem Ereignis verknüpft und als Einflussfaktor für einen Neigungs-Bucket angezeigt werden.

Kunden-KI wendet die Funktionsgenerierung wie „Tage seit“ oder „Anzahl der Tage“ automatisch auf benutzerdefinierte Ereignisse wie **Kauf ansehen** an. Wenn dieses Ereignis als einflussreicher Faktor dafür angesehen wurde, warum Kunden eine hohe, mittlere oder niedrige Neigung haben, zeigt Kunden-KI es als `Days since prd1013 purchase` oder `Count of prd1013 purchase` an. Durch Erstellen dieses Ereignisses als benutzerdefiniertes Ereignis können Sie dem Ereignis einen neuen Namen geben, der die Lesbarkeit der Ergebnisse erheblich erleichtert. Beispiel: `Days since Watch purchase`. Darüber hinaus nutzt Kunden-KI dieses Ereignis für die Schulung und Bewertung, auch wenn das Ereignis kein Standardereignis ist. Dies bedeutet, dass Sie mehrere Ereignisse hinzufügen können, von denen Sie glauben, dass sie Einfluss auf Ihr Modell haben, und Ihr Modell weiter anpassen können, indem Sie Daten wie Reservierungen, Besucherprotokolle und andere Ereignisse einbeziehen. Durch das Hinzufügen dieser Datenpunkte wird die Genauigkeit und Genauigkeit Ihres Kunden-KI-Modells weiter erhöht.

![Ein Beispiel für die Konfiguration eines benutzerdefinierten Ereignisses mit einem benutzerdefinierten Namen in Kunden-KI.](../images/user-guide/custom-event-name.png)

## Optionen festlegen

Mit dem Schritt „Optionen festlegen“ können Sie einen Zeitplan konfigurieren, um Prognoseausführungen zu automatisieren, Prognoseausschlüsse zu definieren, um bestimmte Ereignisse zu filtern, und **[!UICONTROL Profil]** ein-/auszuschalten.

### Zeitplan konfigurieren *(optional)* {#configure-a-schedule}

Um einen Scoring-Zeitplan einzurichten, konfigurieren Sie zunächst die **[!UICONTROL Scoring-Häufigkeit]**. Die Ausführung automatisierter Prognosen kann entweder wöchentlich oder monatlich geplant werden.

![Ein Beispiel für die Konfigurationsoptionen für den Scoring-Zeitplan in Kunden-KI.](../images/user-guide/schedule.png)

### Prognoseausschlüsse *(optional)*

Wenn Ihr Datensatz Spalten enthält, die als Testdaten hinzugefügt wurden, können Sie diese Spalte oder dieses Ereignis zu einer Ausschlussliste hinzufügen, indem Sie **[!UICONTROL Ausschluss hinzufügen]** auswählen und dann das Feld eingeben, das Sie ausschließen möchten. Dadurch wird verhindert, dass Ereignisse, die bestimmte Bedingungen erfüllen, beim Generieren von Scores ausgewertet werden. Diese Funktion kann verwendet werden, um irrelevante Dateneingaben oder Promotions herauszufiltern.

Um ein Ereignis auszuschließen, wählen Sie **[!UICONTROL Ausschluss hinzufügen]** aus und definieren Sie das Ereignis. Um einen Ausschluss zu entfernen, klicken Sie auf die Auslassungszeichen (**[!UICONTROL …]**) oben rechts im Ereignis-Container und wählen Sie dann **[!UICONTROL Container entfernen]**.

![Ein Beispiel für die Konfiguration von Prognoseausschlüssen in Kunden-KI.](../images/user-guide/exclusion.png)

### Profil-Umschalter

Mit dem Umschalter Profil kann Kunden-KI die Bewertungsergebnisse in das Echtzeit-Kundenprofil exportieren. Wenn Sie diesen Umschalter deaktivieren, werden die Scoring-Ergebnisse der Modelle nicht zum Profil hinzugefügt. Kunden-KI-Bewertungsergebnisse sind weiterhin verfügbar, wobei diese Funktion deaktiviert ist.

Bei der ersten Verwendung von Kunden-KI können Sie diese Funktion deaktivieren, bis Sie mit den Modellausgabeergebnissen zufrieden sind. Dadurch wird verhindert, dass beim Optimieren Ihres Modells mehrere Scoring-Datensätze in Ihre Kundenprofile hochgeladen werden. Nachdem Sie Ihr Modell fertig kalibriert haben, können Sie das Modell mithilfe der Option [Klonen](#set-up-your-instance) auf der Seite **Service-Instanzen** klonen. Auf diese Weise können Sie eine Kopie Ihres Modells erstellen und das Profil aktivieren.

![Ein Beispiel für die Umschaltoption „Profil“ im erweiterten Workflow von Kunden-KI.](../images/user-guide/advanced-workflow-save.png)

Nachdem Sie Ihren Scoring-Zeitplan, Prognoseausschlüsse und den Profilumschalter, in dem Sie ihn haben möchten, festgelegt haben, wählen Sie oben rechts **[!UICONTROL Beenden]** aus, um Ihre Kunden-KI-Instanz zu erstellen.

Wenn die Instanz erfolgreich erstellt wurde, wird sofort eine Prognose ausgeführt; nachfolgende Ausführungen erfolgen dann gemäß Ihrem definierten Zeitplan.

>[!NOTE]
>
>Je nach Größe der Eingabedaten kann es bis zu 24 Stunden dauern, bis die Prognoseausführungen abgeschlossen sind.

In diesem Abschnitt haben Sie eine Instanz der Kunden-KI konfiguriert und einen Prognosedurchgang ausgeführt. Nach erfolgreichem Abschluss des Durchgangs werden bewertete Insights automatisch mit prognostizierten Werten ausgefüllt, wenn der Umschalter Profil aktiviert ist. Warten Sie bis zu 24 Stunden, bevor Sie mit dem nächsten Abschnitt dieses Tutorials fortfahren.

## Nächste Schritte {#next-steps}

In diesem Tutorial haben Sie erfolgreich eine Instanz von Kunden-KI konfiguriert und Tendenz-Scores generiert. Sie können jetzt Segment Builder verwenden, um [Kundensegmente mit prognostizierten Werten zu erstellen](./create-segment.md) oder [Einblicke mit Kunden-KI zu ](./discover-insights.md).

## Zusätzliche Ressourcen

Das folgende Video soll Ihnen dabei helfen, den Konfigurations-Workflow für Kunden-KI besser zu verstehen. Darüber hinaus werden Best Practices und Anwendungsbeispiele bereitgestellt.

>[!IMPORTANT]
>
> Das folgende Video ist veraltet. Die aktuellsten Informationen finden Sie in der Dokumentation.

>[!VIDEO](https://video.tv.adobe.com/v/36559?learn=on&quality=12&captions=ger)
