---
keywords: Experience Platform;Benutzerhandbuch;Kundenhilfe;beliebte Themen;Instanz konfigurieren;Instanz erstellen;
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Konfigurieren einer Customer AI-Instanz
topic-legacy: Instance creation
description: Intelligent Services stellen Customer AI als einfach zu verwendenden Adobe Sensei-Dienst bereit, der für verschiedene Anwendungsfälle konfiguriert werden kann. Die folgenden Abschnitte enthalten Schritte zum Konfigurieren einer Instanz von Customer AI.
exl-id: 78353dab-ccb5-4692-81f6-3fb3f6eca886
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1302'
ht-degree: 34%

---

# Konfigurieren einer Customer AI-Instanz

Die Customer AI als Teil von Intelligent Services ermöglicht es Ihnen, benutzerspezifische Tendenzwerte zu generieren, ohne sich um Machine Learning kümmern zu müssen.

Intelligent Services stellen Customer AI als einfach zu verwendenden Adobe Sensei-Dienst bereit, der für verschiedene Anwendungsfälle konfiguriert werden kann. Die folgenden Abschnitte enthalten Schritte zum Konfigurieren einer Instanz von Customer AI.

## Einrichten Ihrer Instanz {#set-up-your-instance}

Wählen Sie in der Benutzeroberfläche &quot;Plattform&quot;in der linken Navigation **[!UICONTROL Dienste]**. Der Browser für **[!UICONTROL Dienste]** erscheint und zeigt alle Dienste an, die Ihnen zur Verfügung stehen. Wählen Sie im Container für Customer AI **[!UICONTROL Open]**.

![](../images/user-guide/navigate-to-service.png)

Die Benutzeroberfläche **Kunden-AI** wird angezeigt und zeigt alle Ihre Dienstinstanzen an.

- Sie finden die Metrik **[!UICONTROL Gespeicherte Profil insgesamt]** unten rechts im Container **[!UICONTROL Instanz erstellen]**. Diese Metrik verfolgt die Gesamtanzahl der von der Kunden-API für das aktuelle Kalenderjahr bewerteten Profil einschließlich aller Sandbox-Umgebung und aller gelöschten Dienstinstanzen.

![](../images/user-guide/total-profiles.png)

Dienstinstanzen können mithilfe der Steuerelemente auf der rechten Seite der Benutzeroberfläche bearbeitet, geklont und gelöscht werden. Um diese Steuerelemente anzuzeigen, wählen Sie eine Instanz aus den vorhandenen **[!UICONTROL Dienstinstanzen]** aus. Die Steuerelemente enthalten Folgendes:

- **[!UICONTROL Bearbeiten]**: Durch Auswahl von  **** Bearbeiten können Sie eine vorhandene Dienstinstanz ändern. Sie können den Namen, die Beschreibung und die Bewertungsfrequenz der Instanz bearbeiten.
- **[!UICONTROL Klonen]**: Durch Auswahl von  **** Clonecopies wird die derzeit ausgewählte Dienstinstanz-Einrichtung kopiert. Anschließend können Sie den Workflow ändern, um kleinere Änderungen vorzunehmen und ihn als neue Instanz umzubenennen.
- **[!UICONTROL Löschen]**: Sie können eine Dienstinstanz einschließlich aller historischen Ausführung löschen.
- **[!UICONTROL Datenquelle]**: Ein Link zum Datensatz, der von dieser Instanz verwendet wird.
- **[!UICONTROL Details]** der letzten Ausführung: Dies wird nur angezeigt, wenn eine Ausführung fehlschlägt. Informationen darüber, warum die Ausführung fehlgeschlagen ist, wie Fehlercodes werden hier angezeigt.
- **[!UICONTROL Score-Definition]**: Eine schnelle Übersicht über das Ziel, das Sie für diese Instanz konfiguriert haben.

![](../images/user-guide/service-instance-panel.png)

Um eine neue Instanz zu erstellen, wählen Sie **[!UICONTROL Instanz erstellen]**.

![](../images/user-guide/dashboard.png)

Der Workflow für die Instanzerstellung wird angezeigt, beginnend mit dem Schritt **[!UICONTROL Einrichtung]**.

Im Folgenden finden Sie wichtige Informationen zu Werten, die Sie für die Instanz angeben müssen:

- Der Name der Instanz wird an allen Stellen verwendet, an denen Kunden-AI-Werte angezeigt werden. Daher sollten Namen beschreiben, was die Prognosewerte darstellen, z. B. „Wahrscheinlichkeit einer Kündigung eines Zeitschriftenabonnements“.

- Der Tendenztyp bestimmt den Zweck des Wertes und die Metrikpolarität. Sie können entweder **[!UICONTROL Abwanderung]** oder **[!UICONTROL Konversion]** wählen. Weitere Informationen darüber, wie sich der Tendenztyp auf Ihre Instanz auswirkt, finden Sie in der [Auswertungszusammenfassung](./discover-insights.md#scoring-summary) im Discover Insight-Dokument.

- Die Datenquelle befindet sich an der Stelle, an der sich die Daten befinden. Der Datensatz ist der Eingabedatensatz, mit dem Ergebnisse vorhergesagt werden. Standardmäßig verwendet die Kundenunterstützung Consumer Experience Ereignis-, Adobe Analytics- und Adobe Audience Manager-Daten, um Tendenzwerte zu berechnen. Wenn Sie einen Datensatz in der Dropdown-Auswahl wählen, werden nur Datensätze aufgelistet, die mit Customer KI kompatibel sind.

- Standardmäßig werden Tendenzwerte für alle Profile generiert, es sei denn, es wurde eine qualifizierte Zielgruppe angegeben. Sie können eine qualifizierte Zielgruppe angeben, indem Sie Bedingungen festlegen, um Profile auf Grundlage von Ereignissen ein- oder auszuschließen.

Geben Sie die erforderlichen Werte ein und wählen Sie dann **[!UICONTROL Weiter]**.

![](../images/user-guide/setup.png)

### Ziel definieren {#define-a-goal}

Der Schritt **[!UICONTROL Ziel definieren]** wird angezeigt und bietet eine interaktive Umgebung, um ein Prognoseziel visuell zu definieren. Ein Ziel besteht aus einem oder mehreren Ereignissen, bei denen das Auftreten eines jeden Ereignisses auf der Bedingung basiert, die es enthält. Ziel einer Customer AI-Instanz ist es, die Wahrscheinlichkeit zu bestimmen, mit der ihr Ziel innerhalb eines bestimmten Zeitraums erreicht wird.

Um ein Ziel zu erstellen, wählen Sie **[!UICONTROL Feldnamen eingeben]** und wählen Sie ein Feld aus der Dropdown-Liste aus. Wählen Sie die zweite Eingabe aus und wählen Sie eine Klausel für die Bedingung des Ereignisses. Geben Sie dann die Zielgruppe ein, um das Ereignis abzuschließen. Zusätzliche Ereignis können durch Auswahl von **[!UICONTROL Hinzufügen Ereignis]** konfiguriert werden. Schließen Sie schließlich das Ziel ab, indem Sie einen Prognosezeitrahmen in der Anzahl der Tage anwenden und dann **[!UICONTROL Weiter]** wählen.

![](../images/user-guide/goal.png)

#### Wird ausgeführt und wird nicht ausgeführt

Beim Definieren Ihres Ziels haben Sie die Möglichkeit, **[!UICONTROL Wird auftreten]** oder **[!UICONTROL Wird nicht ausgeführt]**. Wenn Sie **[!UICONTROL Wird auftreten]** wählen, müssen die von Ihnen definierten Ereignis-Bedingungen erfüllt sein, damit die Ereignis-Daten eines Kunden in die Einblicke-Benutzeroberfläche aufgenommen werden.

Wenn Sie z. B. eine App einrichten möchten, um vorherzusagen, ob ein Kunde einen Kauf tätigt, können Sie **[!UICONTROL Folgendes auswählen:]**, dann **[!UICONTROL All von]** und **commerce.purchase.id** und **exists** als Operator eingeben.

![wird](../images/user-guide/occur.png)

Es kann jedoch vorkommen, dass Sie sich für eine Vorhersage interessieren, ob ein Ereignis in einem bestimmten Zeitraum nicht eintritt. Um ein Ziel mit dieser Option zu konfigurieren, wählen Sie **[!UICONTROL Wird nicht ausgeführt]** aus der Dropdownliste auf der obersten Ebene.

Wenn Sie z. B. vorhersagen möchten, welche Kunden sich weniger engagieren und Ihre Kontoanmeldung im nächsten Monat nicht besuchen. Wählen Sie **[!UICONTROL Wird nicht vorkommen]** gefolgt von **[!UICONTROL All of]** und geben Sie **web.webInteraction.URL** und **[!UICONTROL entspricht]** als Operator mit **account-login** als Wert ein.

![wird nicht](../images/user-guide/not-occur.png)

#### Alle und beliebige

In einigen Fällen können Sie vorhersagen, ob eine Kombination von Ereignissen eintritt, und in anderen Fällen können Sie das Auftreten eines beliebigen Ereignisses aus einem vordefinierten Satz vorhersagen. Um vorherzusagen, ob ein Kunde eine Kombination von Ereignissen hat, wählen Sie die Option **[!UICONTROL Alle von]** aus der Dropdown-Liste der zweiten Ebene auf der Seite **[!UICONTROL Ziel definieren]**.

Sie können beispielsweise vorhersagen, ob ein Kunde ein bestimmtes Produkt kauft. Dieses Prognoseziel ist durch zwei Bedingungen definiert: a `commerce.order.purchaseID` **exists** und `productListItems.SKU` **entspricht** einem bestimmten Wert.

![Alle Beispiele](../images/user-guide/all-of.png)

Um vorherzusagen, ob ein Kunde ein Ereignis aus einem bestimmten Satz hat, können Sie die Option **[!UICONTROL Beliebig von]** verwenden.

Sie können beispielsweise vorhersagen, ob ein Kunde eine bestimmte URL oder eine Webseite mit einem bestimmten Namen besucht. Dieses Prognoseziel ist durch zwei Bedingungen definiert: `web.webPageDetails.URL` **Beginn mit** einem bestimmten Wert und `web.webPageDetails.name` **Beginn mit** einem bestimmten Wert.

![Beispiel](../images/user-guide/any-of.png)

### Zeitplan konfigurieren *(optional)* {#configure-a-schedule}

Der Schritt **[!UICONTROL Erweitert]** wird angezeigt. Mit diesem optionalen Schritt können Sie einen Zeitplan konfigurieren, um die Ausführung von Prognosen zu automatisieren, Prognoseausschlüsse zum Filtern bestimmter Ereignis zu definieren oder **[!UICONTROL Fertigstellen]** wählen, wenn nichts erforderlich ist.

Richten Sie einen Auswertungszeitplan ein, indem Sie die **[!UICONTROL Auswertungshäufigkeit]** festlegen. Die Ausführung automatisierter Prognosen kann entweder wöchentlich oder monatlich geplant werden.

![](../images/user-guide/schedule.png)

Unter der Zeitplankonfiguration können Sie Prognoseausschlüsse definieren, um zu verhindern, dass bei der Generierung von Werten Ereignisse ausgewertet werden, die bestimmte Bedingungen erfüllen. Mit dieser Funktion können irrelevante Dateneingaben herausgefiltert werden.

Um bestimmte Ereignis auszuschließen, wählen Sie **[!UICONTROL Hinzufügen aus und definieren Sie das Ereignis auf dieselbe Weise wie das Ziel.]** Um einen Ausschluss zu entfernen, wählen Sie die Auslassungspunkte (**[!UICONTROL ...]**) oben rechts im Ereignis-Container und wählen Sie **[!UICONTROL Container entfernen]**.

![](../images/user-guide/exclusion.png)

Schließen Sie die Ereignis nach Bedarf aus und wählen Sie dann **[!UICONTROL Fertig]**, um die Instanz zu erstellen.

![](../images/user-guide/advanced.png)

Wenn die Instanz erfolgreich erstellt wurde, wird sofort eine Prognose ausgeführt; nachfolgende Ausführungen erfolgen dann gemäß Ihrem definierten Zeitplan.

>[!NOTE]
>
>Je nach Umfang der Eingabedaten kann die Ausführung von Prognosen bis zu 24 Stunden dauern.

In diesem Abschnitt haben Sie eine Instanz von Customer AI konfiguriert und eine Prognose durchgeführt. Nach erfolgreicher Ausführung sorgen Auswertungsdaten für ein automatisches Ausfüllen von Profilen mit Prognosewerten. Warten Sie bis zu 24 Stunden, bevor Sie mit dem nächsten Abschnitt dieses Tutorials fortfahren.

## Nächste Schritte {#next-steps}

In diesem Lernprogramm haben Sie erfolgreich eine Instanz der Kunden-API konfiguriert und Tendenzwerte generiert. Sie können nun den Segmentaufbau verwenden, um Kundensegmente mit prognostizierten Ergebnissen](./create-segment.md) oder [zu erstellen, um Erkenntnisse mit der Kunden-KI](./discover-insights.md) zu ermitteln.[

## Zusätzliche Ressourcen

Das folgende Video unterstützt Sie dabei, den Konfigurationsarbeitsablauf für Kunden-API zu verstehen. Darüber hinaus werden Best Practices und Verwendungsfallbeispiele bereitgestellt.

>[!VIDEO](https://video.tv.adobe.com/v/32665?learn=on&quality=12)
