---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Benutzeroberfläche; Benutzeroberfläche; Anpassung; Profil-Dashboard; Dashboard
title: Profil-Dashboard
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zu den Echtzeit-Kundenprofildaten Ihres Unternehmens anzeigen können.
topic-legacy: guide
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 11e8acc3da7f7540421b5c7f3d91658c571fdb6f
workflow-type: tm+mt
source-wordcount: '1123'
ht-degree: 3%

---

# (Beta) Dashboard [!UICONTROL Profile]

>[!IMPORTANT]
>
>Die in diesem Dokument beschriebene Dashboard-Funktion befindet sich derzeit in der Beta-Phase und steht nicht allen Benutzern zur Verfügung. Die Dokumentation und Funktionalität können sich ändern.

Die Adobe Experience Platform-Benutzeroberfläche bietet ein Dashboard, über das Sie wichtige Informationen zu Ihren [!DNL Real-time Customer Profile]-Daten anzeigen können, die in einem täglichen Schnappschuss erfasst werden. In diesem Handbuch wird beschrieben, wie Sie auf das Dashboard [!UICONTROL Profile] in der Benutzeroberfläche zugreifen und mit ihm arbeiten können. Außerdem erhalten Sie Informationen zu den im Dashboard angezeigten Metriken.

Einen Überblick über alle Profilfunktionen in der Experience Platform-Benutzeroberfläche finden Sie im Handbuch [Benutzeroberfläche des Echtzeit-Kundenprofils](../../profile/ui/user-guide.md).

## Profil-Dashboard-Daten

Das Dashboard [!UICONTROL Profile] zeigt eine Momentaufnahme der Attributdaten (Datensatzdaten) an, die Ihr Unternehmen im Profilspeicher in Experience Platform hat. Der Schnappschuss enthält keine Ereignisdaten (Zeitreihendaten).

Die Attributdaten im Snapshot zeigen die Daten exakt so an, wie sie zu dem Zeitpunkt angezeigt werden, zu dem die Momentaufnahme erstellt wurde. Mit anderen Worten, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten, und das Profil-Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme des Schnappschusses an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn der nächste Schnappschuss erstellt wurde.

## Analyse des Dashboards [!UICONTROL Profile]

Um in der Platform-Benutzeroberfläche zum Dashboard [!UICONTROL Profile] zu navigieren, wählen Sie in der linken Leiste **[!UICONTROL Profile]** und dann die Registerkarte **[!UICONTROL Übersicht]** aus, um das Dashboard anzuzeigen.

![](../images/profiles/dashboard-overview.png)

### Auswählen von Zusammenführungsrichtlinien

Die im Dashboard [!UICONTROL Profile] angezeigten Metriken basieren auf Zusammenführungsrichtlinien, die auf Ihre Echtzeit-Kundenprofildaten angewendet werden. Wenn Daten aus mehreren Quellen zusammengeführt werden, können die Daten widersprüchliche Werte enthalten (z. B. kann ein Datensatz einen Kunden als &quot;einzeln&quot;auflisten, während ein anderer Datensatz den Kunden als &quot;verheiratet&quot;auflisten kann). Es ist Aufgabe der Zusammenführungsrichtlinie zu bestimmen, welche Daten priorisiert und als Teil des Profils angezeigt werden sollen.

Das Dashboard wählt automatisch eine anzuzeigende Zusammenführungsrichtlinie aus, Sie können jedoch die ausgewählte Zusammenführungsrichtlinie über das Dropdown-Menü ändern. Um eine andere Zusammenführungsrichtlinie auszuwählen, wählen Sie das Dropdown-Menü neben dem Namen der Zusammenführungsrichtlinie und dann die Zusammenführungsrichtlinie aus, die Sie anzeigen möchten.

>[!NOTE]
>
>Im Dropdown-Menü werden nur Zusammenführungsrichtlinien angezeigt, die sich auf die Klasse &quot;XDM Individual Profile&quot;beziehen. Wenn Ihr Unternehmen jedoch mehrere Zusammenführungsrichtlinien erstellt hat, müssen Sie möglicherweise einen Bildlauf durchführen, um die vollständige Liste der verfügbaren Zusammenführungsrichtlinien anzuzeigen.

Weitere Informationen zu Zusammenführungsrichtlinien, einschließlich der Erstellung, Bearbeitung und Deklarierung einer standardmäßigen Zusammenführungsrichtlinie für Ihre Organisation, finden Sie in der [Übersicht über Zusammenführungsrichtlinien](../../profile/merge-policies/overview.md).

![](../images/profiles/select-merge-policy.png)

### Widgets und Metriken

Das Dashboard besteht aus Widgets, die schreibgeschützte Metriken sind und wichtige Informationen zu Ihren Profildaten enthalten. Das Datum und die Uhrzeit der letzten Aktualisierung eines Widgets zeigen an, wann die letzte Momentaufnahme der Daten erstellt wurde.

![](../images/profiles/dashboard-timestamp.png)

## Verfügbare Widgets

Experience Platform bietet mehrere Widgets, mit denen Sie verschiedene Metriken im Zusammenhang mit Ihren Profildaten visualisieren können. Wählen Sie unten den Namen eines Widgets aus, um mehr zu erfahren:

* [[!UICONTROL Zielgruppengröße]](#audience-size)
* [[!UICONTROL Hinzugefügte Profile]](#profiles-added)
* [[!UICONTROL Im Zeitverlauf hinzugefügte Profile]](#profiles-added-over-time)
* [[!UICONTROL Profile nach Namespace]](#profiles-by-namespace)
* [[!UICONTROL Namespace-Überschneidung]](#namespace-overlap)

### [!UICONTROL Zielgruppengröße] {#audience-size}

Das Widget **[!UICONTROL Zielgruppengröße]** zeigt die Gesamtzahl der zusammengeführten Profile im Profildatenspeicher zum Zeitpunkt der Momentaufnahme an. Diese Zahl ist das Ergebnis der ausgewählten Zusammenführungsrichtlinie, die auf Ihre Profildaten angewendet wird, um Profilfragmente zu einem einzelnen Profil für jede Person zusammenzuführen.

Weitere Informationen zu Fragmenten und zusammengeführten Profilen finden Sie im Abschnitt *Profilfragmente im Vergleich zu zusammengeführten Profilen* der [Übersicht zum Echtzeit-Kundenprofil](../../profile/home.md).

>[!NOTE]
>
>Die zur Berechnung dieser Metrik verwendete Zusammenführungsrichtlinie ist nicht mit der systemgenerierten Zusammenführungsrichtlinie identisch, die zur Berechnung von [!UICONTROL Addressable audiences] im Dashboard [!UICONTROL Lizenznutzung] verwendet wird. Daher ist es unwahrscheinlich, dass die Zielgruppenanzahl in den Dashboards [!UICONTROL Profile] und [!UICONTROL Lizenznutzung] genau der gleichen ist.

![](../images/profiles/audience-size.png)

### [!UICONTROL Hinzugefügte Profile] {#profiles-added}

Das Widget **[!UICONTROL hinzugefügte Profile]** zeigt die Gesamtzahl der zusammengeführten Profile an, die seit der letzten Momentaufnahme zum Profildatenspeicher hinzugefügt wurden. Diese Zahl ist das Ergebnis der ausgewählten Zusammenführungsrichtlinie, die auf Ihre Profildaten angewendet wird, um Profilfragmente zu einem einzelnen Profil für jede Person zusammenzuführen.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Im Zeitverlauf hinzugefügte Profile] {#profiles-added-over-time}

Das Widget **[!UICONTROL Im Zeitverlauf hinzugefügte Profile]** zeigt die Gesamtzahl der zusammengeführten Profile an, die in den letzten 30 Tagen täglich zum Profildatenspeicher hinzugefügt wurden. Diese Zahl wird jeden Tag aktualisiert, wenn die Momentaufnahme erstellt wird. Wenn Sie also Profile in Platform aufnehmen möchten, wird die Anzahl der Profile erst angezeigt, wenn die nächste Momentaufnahme erfolgt.

Die Anzahl der hinzugefügten Profile ist das Ergebnis der ausgewählten Zusammenführungsrichtlinie, die auf Ihre Profildaten angewendet wird, um Profilfragmente zusammenzuführen und so für jede Person ein Profil zu erstellen.

![](../images/profiles/profiles-added-over-time.png)

### [!UICONTROL Profile nach Namespace] {#profiles-by-namespace}

Das Widget **[!UICONTROL Profile nach Namespace]** zeigt die Aufschlüsselung der Identitäts-Namespaces für alle zusammengeführten Profile in Ihrem Profilspeicher an. Die Gesamtanzahl der Profile nach [!UICONTROL ID-Namespace] (d. h. das Addieren der für jeden Namespace angezeigten Werte) kann höher sein als die Gesamtanzahl der Zusammenführungsprofile, da einem Profil mehrere Namespaces zugeordnet sein können. Wenn beispielsweise ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Namespaces zugeordnet.

Weitere Informationen zu Identitäts-Namespaces finden Sie in der [Dokumentation zum Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/profiles-by-namespace.png)

### [!UICONTROL Namespace-Überschneidung] {#namespace-overlap}

Das Widget **[!UICONTROL Namespace-Überschneidung]** zeigt ein Venn-Diagramm oder Set-Diagramm, das die Überschneidung von Profilen in Ihrem Profilspeicher mit mehreren Identitäts-Namespaces anzeigt.

Nachdem Sie die Dropdown-Menüs im Widget zur Auswahl der Identitäts-Namespaces verwendet haben, die Sie vergleichen möchten, werden Kreise angezeigt, die die relative Größe jedes Namespace anzeigen. Die Anzahl der Profile, die beide Namespaces enthalten, wird durch die Größe der Überschneidung zwischen den Kreisen dargestellt.

Wenn ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Namespaces zugeordnet. Daher ist es wahrscheinlich, dass Ihr Unternehmen über mehrere Profile verfügt, die Fragmente aus mehr als einem Identitäts-Namespace enthalten.

Weitere Informationen zu Identitäts-Namespaces finden Sie in der [Dokumentation zum Adobe Experience Platform Identity Service](../../identity-service/home.md).

![](../images/profiles/namespace-overlap.png)

## Nächste Schritte

Durch Befolgen dieses Dokuments sollten Sie jetzt in der Lage sein, das Profil-Dashboard zu finden und die in den verfügbaren Widgets angezeigten Metriken zu verstehen. Weitere Informationen zum Arbeiten mit [!DNL Profile]-Daten in der Experience Platform-Benutzeroberfläche finden Sie im [Handbuch zur Benutzeroberfläche des Echtzeit-Kundenprofils](../../profile/ui/user-guide.md).
