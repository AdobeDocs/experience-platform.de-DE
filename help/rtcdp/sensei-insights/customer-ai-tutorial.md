---
title: Prognostizieren Sie mithilfe von Customer AI (Alpha) die Tendenzwerte der Kunden.
seo-title: Prognostizieren Sie mithilfe von Customer AI (Alpha) die Tendenzwerte der Kunden.
description: Dieses Lernprogramm enthält Anleitungen zur Verwendung der Kunden-API (Alpha).
seo-description: Dieses Lernprogramm enthält Anleitungen zur Verwendung der Kunden-API (Alpha).
index: false
translation-type: tm+mt
source-git-commit: fde2bb7af91dbcb0c701397c878b63044cb27a4d

---


# Prognostizieren Sie mithilfe von Customer AI (Alpha) die Tendenzwerte der Kunden.

>[!NOTE]
>Die in diesem Dokument beschriebene Funktion für Kunden-API ist alphanumerisch. Die Dokumentation und die Funktionalität können geändert werden.

Kunden-API in Adobe Experience Platform wurde von Adobe Sensei entwickelt und unterstützt und ermöglicht es Ihnen, benutzerdefinierte Tendenzwerte zu generieren, ohne sich um die Aspekte des maschinellen Lernens kümmern zu müssen.

In diesem Lernprogramm werden die Schritte zum Arbeiten mit der Kunden-API mithilfe der Benutzeroberfläche der Experience Platform beschrieben. Schritte für die folgenden Themen:

* [Eine Instanz konfigurieren](#configure-an-instance)
* [Kundensegmente mit prognostizierten Ergebnissen erstellen](#create-customer-segments-with-predicted-scores)

## Erste Schritte

Dieser Leitfaden erfordert ein Verständnis der verschiedenen Plattformdienste, die bei der Verwendung der Kundentechnik erforderlich sind. Bevor Sie dieses Lernprogramm beginnen, lesen Sie bitte die folgenden Dokumente:

* [Übersicht über Kundenprofile in Echtzeit](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/unified_profile_architectural_overview/unified_profile_architectural_overview.md)
* [Übersicht über den Segmentdienst](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!end-user/markdown/segmentation_overview/segmentation.md)
* [Segment Builder-Benutzerhandbuch](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!end-user/markdown/segmentation_overview/segment-builder-guide.md)

## Eine Instanz konfigurieren

Experience Platform bietet Kunden-API als einfachen Adobe Sensei-Dienst, der für verschiedene Anwendungsfälle konfiguriert werden kann. Die folgenden Abschnitte enthalten Schritte zum Konfigurieren einer Instanz von Customer AI.

### Instanz einrichten

Klicken Sie in der Benutzeroberfläche &quot;Plattform&quot;in der linken Navigation auf **Dienste** . Der Browser **Services** erscheint und zeigt alle verfügbaren Dienste an, die Ihnen zur Verfügung stehen. Klicken Sie im Container für Customer AI auf **Open**.

![](./images/service.png)

Im Bildschirm &quot; *Kunden-API* &quot;werden alle vorhandenen Kunden-AI-Instanzen angezeigt. Klicken Sie auf Instanz **erstellen**.

![](./images/customer_ai.png)

Der Arbeitsablauf für die Instanzerstellung wird ab dem Schritt *Setup* angezeigt.

Im Folgenden finden Sie wichtige Informationen zu Werten, für die Sie die Instanz bereitstellen müssen:

* Der Name der Instanz wird an allen Stellen verwendet, an denen die Kunden-AI-Bewertung angezeigt wird. Daher sollten Namen beschreiben, was die Prognosewerte darstellen, z. B. &quot;Wahrscheinlichkeit der Kündigung eines Abonnements für Zeitschriften&quot;.

* Der Tendenztyp bestimmt den Zweck des Ergebnisses und der Metrikpolarität. Sie können entweder **Churn** oder **Conversion** wählen.

* Datenquelle bezieht sich auf den Eingabedataset, der zur Prognose von Ergebnissen verwendet wird. Standardmäßig verwendet die Kundentraining-API Consumer Experience-Ereignisdaten, um Tendenzwerte zu berechnen. Wenn Sie einen Datensatz aus der Dropdown-Auswahl auswählen, werden nur die Datensätze aufgelistet, die mit der Kunden-API kompatibel sind.

* Standardmäßig werden Tendenzwerte für alle Profile generiert, es sei denn, eine förderfähige Population wurde angegeben. Sie können eine berechtigte Population angeben, indem Sie Bedingungen festlegen, um Profile auf der Grundlage von Ereignissen ein- oder auszuschließen.

Geben Sie die erforderlichen Werte ein und klicken Sie auf **Weiter**.

![](./images/setup.png)

### Ziel definieren

Der Schritt *Ziel* definieren wird angezeigt und bietet eine interaktive Umgebung, in der Sie ein Ziel visuell definieren können. Ein Ziel besteht aus einem oder mehreren Ereignissen, bei denen das Auftreten jedes Ereignisses auf der Bedingung basiert, die es enthält. Ziel einer Kundentransferinstanz ist es, die Wahrscheinlichkeit zu bestimmen, dass ihr Ziel innerhalb eines bestimmten Zeitraums erreicht wird.

Klicken Sie auf Feldnamen **eingeben** und wählen Sie ein Feld aus der Dropdownliste aus. Klicken Sie auf die zweite Eingabe und wählen Sie eine Klausel für die Ereignisbedingung aus. Geben Sie dann einen Zielwert ein, um das Ereignis abzuschließen. Weitere Ereignisse können durch Klicken auf Ereignis **hinzufügen konfiguriert werden**. Schließen Sie schließlich das Ziel ab, indem Sie einen Prognosezeitrahmen in der Anzahl der Tage anwenden, und klicken Sie dann auf **Weiter**.

![](./images/goal.png)

### Zeitplan konfigurieren *(optional)*

Der *erweiterte* Schritt wird angezeigt. Mit diesem optionalen Schritt können Sie einen Zeitplan konfigurieren, um die Ausführung von Prognosen zu automatisieren, Prognoseausschlüsse zum Filtern bestimmter Ereignisse zu definieren oder auf **Fertig stellen** klicken, wenn nichts erforderlich ist.

Richten Sie einen Bewertungszeitplan ein, indem Sie die *Bewertungshäufigkeit* konfigurieren. Die Ausführung automatisierter Prognosen kann entweder wöchentlich oder monatlich geplant werden.

![](./images/schedule.png)

Unter der Plankonfiguration können Sie Prognoseausschlüsse definieren, um zu verhindern, dass Ereignisse, die bestimmte Bedingungen erfüllen, bei der Generierung von Ergebnissen ausgewertet werden. Mit dieser Funktion können irrelevante Dateneingaben herausgefiltert werden.

Um bestimmte Ereignisse auszuschließen, klicken Sie auf Ausschluss **** hinzufügen und definieren Sie das Ereignis auf dieselbe Weise wie das Ziel. Um einen Ausschluss zu entfernen, klicken Sie auf die Auslassungspunkte (**...**) oben rechts im Ereignisbehälter und klicken Sie dann auf Behälter **entfernen**.

![](./images/exclusion.png)

Schließen Sie Ereignisse nach Bedarf aus und klicken Sie dann auf **Fertig stellen** , um die Instanz zu erstellen.

![](./images/advanced.png)

Wenn die Instanz erfolgreich erstellt wurde, wird sofort eine Prognoseausführung ausgelöst, und nachfolgende wird gemäß Ihrem definierten Zeitplan ausgeführt.

>   **** Hinweis: Je nach Größe der Eingabedaten kann die Ausführung von Prognosen bis zu 24 Stunden dauern.

Durch Befolgen dieses Abschnitts haben Sie eine Instanz von Customer AI konfiguriert und eine Prognose ausgeführt. Nach erfolgreichem Abschluss des Vorgangs werden Profiles automatisch mit Ergebniswerten versehen. Bitte warten Sie 24 Stunden, bevor Sie mit dem nächsten Abschnitt dieses Tutorials fortfahren.

## Kundensegmente mit prognostizierten Ergebnissen erstellen

Nach Abschluss einer Prognoseausführung werden die prognostizierten Tendenzwerte automatisch von Profiles genutzt. Die Anreicherung von Profilen mit Kunden-AI-Bewertungen ermöglicht die Erstellung von Kundensegmenten, die auf Tendenzwerten basieren. In diesem Abschnitt werden Schritte zum Erstellen von Segmenten mit dem Segmentaufbau beschrieben. Eine solidere Anleitung zum Erstellen von Segmenten finden Sie im Benutzerhandbuch zum [Segmentaufbau](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!end-user/markdown/segmentation_overview/segment-builder-guide.md).

Klicken Sie in der Benutzeroberfläche &quot;Plattform&quot;im linken Navigationsbereich auf **Segmente** und dann auf Segment **erstellen**.

![](./images/segments.png)

Der *Segmentaufbau* wird angezeigt. Klicken Sie in der linken Spalte *Felder* und auf der Registerkarte *Attribute* auf den Ordner **XDM Individuelles Profil** und dann auf den Ordner mit dem Namespace Ihres Unternehmens. Der Ordner **Customer AI** enthält die Ergebnisse von Prognosen und wird nach der Instanz benannt, zu der die Ergebnisse gehören. Klicken Sie auf die Ergebnisse der gewünschten Instanz und greifen Sie darauf zu.

![](./images/results.png)

Ziehen Sie das **Ergebnisattribut** in die Arbeitsfläche *des* Regelaufbaus, um eine Regel zu definieren.

Wählen Sie unter der rechten Spalte *Segmenteigenschaften* eine *Merge-Richtlinie* aus und geben Sie einen Namen für das Segment ein. Klicken Sie dann auf **Speichern** , um das Segment zu erstellen.

![](./images/properties.png)

## Nächste Schritte

In diesem Lernprogramm haben Sie erfolgreich eine Instanz der Kunden-AI konfiguriert, Tendenzwerte generiert und ein Segment erstellt, das mithilfe von Tendenzwerten mithilfe des Segmentaufbaus erzwungen wurde. Ihr Kundensegment kann jetzt von aktivierten Zielen für Zielgruppen verwendet werden. Weitere Informationen finden Sie in der Übersicht über die [Ziele](../destinations/destinations-overview.md) .
