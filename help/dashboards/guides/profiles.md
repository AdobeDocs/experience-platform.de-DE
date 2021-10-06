---
keywords: Experience Platform; Profil; Echtzeit-Kundenprofil; Benutzeroberfläche; Benutzeroberfläche; Anpassung; Profil-Dashboard; Dashboard
title: Profil-Dashboard
description: Adobe Experience Platform bietet ein Dashboard, über das Sie wichtige Informationen zu den Echtzeit-Kundenprofildaten Ihres Unternehmens anzeigen können.
type: Documentation
exl-id: 7b9752b2-460e-440b-a6f7-a1f1b9d22eeb
source-git-commit: 05f2ba2e8e7abadeef18a908ba8b0e9a02d4c3f8
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 6%

---

#  Profilesdashboard

Die Adobe Experience Platform-Benutzeroberfläche bietet ein Dashboard, über das Sie wichtige Informationen zu Ihren [!DNL Real-time Customer Profile]-Daten anzeigen können, die in einem täglichen Schnappschuss erfasst werden. In diesem Handbuch wird beschrieben, wie Sie auf das Dashboard [!UICONTROL Profile] in der Benutzeroberfläche zugreifen und mit ihm arbeiten können. Außerdem erhalten Sie Informationen zu den im Dashboard angezeigten Metriken.

Einen Überblick über alle Profilfunktionen in der Experience Platform-Benutzeroberfläche finden Sie im Handbuch [Benutzeroberfläche des Echtzeit-Kundenprofils](../../profile/ui/user-guide.md).

## Profil-Dashboard-Daten

Das Dashboard [!UICONTROL Profile] zeigt eine Momentaufnahme der Attributdaten (Datensatzdaten), die Ihr Unternehmen im Profilspeicher in der Experience Platform hat. Der Schnappschuss enthält keine Ereignisdaten (Zeitreihendaten).

Die Attributdaten im Snapshot zeigen die Daten exakt so an, wie sie zu dem Zeitpunkt angezeigt werden, zu dem die Momentaufnahme erstellt wurde. Mit anderen Worten, der Schnappschuss ist keine Annäherung oder Stichprobe der Daten, und das Profil-Dashboard wird nicht in Echtzeit aktualisiert.

>[!NOTE]
>
>Änderungen oder Aktualisierungen, die seit der Aufnahme des Schnappschusses an den Daten vorgenommen wurden, werden erst dann im Dashboard angezeigt, wenn der nächste Schnappschuss erstellt wurde.

## Analyse des Dashboards [!UICONTROL Profile]

Um in der Platform-Benutzeroberfläche zum Dashboard [!UICONTROL Profile] zu navigieren, wählen Sie in der linken Leiste **[!UICONTROL Profile]** und dann die Registerkarte **[!UICONTROL Übersicht]** aus, um das Dashboard anzuzeigen.

>[!NOTE]
>
>Wenn Ihr Unternehmen neu bei Platform ist und noch keine aktiven Profildatensätze oder Zusammenführungsrichtlinien erstellt wurden, ist das Dashboard [!UICONTROL Profile] nicht sichtbar. Stattdessen werden auf der Registerkarte [!UICONTROL Übersicht] Links und Dokumentation angezeigt, die Ihnen bei den ersten Schritten mit dem Echtzeit-Kundenprofil helfen.

![](../images/profiles/dashboard-overview.png)

### Ändern des Dashboards [!UICONTROL Profile]

Sie können das Erscheinungsbild des Dashboards [!UICONTROL Profile] ändern, indem Sie **[!UICONTROL Dashboard ändern]** auswählen. Dadurch können Sie Widgets aus dem Dashboard verschieben, hinzufügen und entfernen sowie auf die **[!UICONTROL Widget-Bibliothek]** zugreifen, um verfügbare Widgets zu untersuchen und benutzerdefinierte Widgets für Ihre Organisation zu erstellen.

Weitere Informationen finden Sie in der Dokumentation [Dashboards ändern](../customize/modify.md) und [Widget-Bibliothek - Übersicht](../customize/widget-library.md) .

## Zusammenführungsrichtlinien {#merge-policies}

Die im Dashboard [!UICONTROL Profile] angezeigten Metriken basieren auf Zusammenführungsrichtlinien, die auf Ihre Echtzeit-Kundenprofildaten angewendet werden. Wenn Daten aus mehreren Quellen zusammengeführt werden, um das Kundenprofil zu erstellen, können die Daten widersprüchliche Werte enthalten (z. B. kann ein Datensatz einen Kunden als &quot;einzeln&quot;auflisten, während ein anderer Datensatz den Kunden als &quot;verheiratet&quot;auflisten kann). Es ist der Auftrag der Zusammenführungsrichtlinie, zu bestimmen, welche Daten als Teil des Profils priorisiert und angezeigt werden sollen.

Weitere Informationen zu Zusammenführungsrichtlinien, einschließlich der Erstellung, Bearbeitung und Deklarierung einer standardmäßigen Zusammenführungsrichtlinie für Ihre Organisation, finden Sie in der [Übersicht über Zusammenführungsrichtlinien](../../profile/merge-policies/overview.md).

Das Dashboard wählt automatisch eine anzuzeigende Zusammenführungsrichtlinie aus, Sie können jedoch die ausgewählte Zusammenführungsrichtlinie über das Dropdown-Menü ändern. Um eine andere Zusammenführungsrichtlinie auszuwählen, wählen Sie das Dropdown-Menü neben dem Namen der Zusammenführungsrichtlinie und dann die Zusammenführungsrichtlinie aus, die Sie anzeigen möchten.

>[!NOTE]
>
>Im Dropdown-Menü werden nur Zusammenführungsrichtlinien angezeigt, die sich auf die Klasse &quot;XDM Individual Profile&quot;beziehen. Wenn Ihr Unternehmen jedoch mehrere Zusammenführungsrichtlinien erstellt hat, müssen Sie möglicherweise einen Bildlauf durchführen, um die vollständige Liste der verfügbaren Zusammenführungsrichtlinien anzuzeigen.

![](../images/profiles/select-merge-policy.png)

## Widgets und Metriken

Das Dashboard besteht aus Widgets, die schreibgeschützte Metriken sind und wichtige Informationen zu Ihren Profildaten enthalten.

Das Datum und die Uhrzeit der letzten Aktualisierung eines Widgets zeigen an, wann die letzte Momentaufnahme der Daten erstellt wurde. Datum und Uhrzeit der Momentaufnahme werden in UTC angegeben. Es befindet sich nicht in der Zeitzone des einzelnen Benutzers oder der IMS-Organisation.

## Standard-Widgets

Adobe bietet mehrere Standard-Widgets, mit denen Sie verschiedene Metriken im Zusammenhang mit Ihren Profildaten visualisieren können. Sie können auch benutzerdefinierte Widgets erstellen, die für Ihre Organisation freigegeben werden, indem Sie die [!UICONTROL Widget-Bibliothek] verwenden. Um mehr über das Erstellen benutzerdefinierter Widgets zu erfahren, lesen Sie zunächst die [Übersicht über die Widget-Bibliothek](../customize/widget-library.md).

Um mehr über die einzelnen verfügbaren Standard-Widgets zu erfahren, wählen Sie den Namen eines Widgets aus der folgenden Liste aus:

* [[!UICONTROL Anzahl der Profile]](#profile-count)
* [[!UICONTROL Hinzugefügte Profile]](#profiles-added)
* [[!UICONTROL Trend der Profilanzahl]](#profiles-count-trend)
* [[!UICONTROL Profile nach Identität]](#profiles-by-identity)
* [[!UICONTROL Identitätsüberschneidung]](#identity-overlap)

### [!UICONTROL Anzahl der Profile] {#profile-count}

Das Widget **[!UICONTROL Profilanzahl]** zeigt die Gesamtzahl der zusammengeführten Profile im Profilspeicher zum Zeitpunkt der Momentaufnahme an. Diese Zahl ist das Ergebnis der ausgewählten Zusammenführungsrichtlinie, die auf Ihre Profildaten angewendet wird, um Profilfragmente zu einem einzelnen Profil für jede Person zusammenzuführen.

Weitere Informationen finden Sie im Abschnitt [zu Zusammenführungsrichtlinien weiter oben in diesem Dokument](#merge-policies) .

>[!NOTE]
>
>Das Widget [!UICONTROL Profilanzahl] kann aus mehreren Gründen eine andere Zahl anzeigen als die Profilanzahl, die auf der Registerkarte [!UICONTROL Durchsuchen] im Abschnitt [!UICONTROL Profile] der Benutzeroberfläche angezeigt wird. Der häufigste Grund ist, dass der Tab [!UICONTROL Durchsuchen] die Gesamtzahl der zusammengeführten Profile basierend auf der standardmäßigen Zusammenführungsrichtlinie Ihres Unternehmens referenziert, während das Widget [!UICONTROL Profilanzahl] die Gesamtanzahl der zusammengeführten Profile basierend auf der Zusammenführungsrichtlinie referenziert, die Sie im Dashboard anzeigen möchten.
>
>Ein weiterer häufiger Grund sind die Unterschiede zwischen der Zeit, zu der der Dashboard-Schnappschuss erstellt wird, und der Zeit, zu der der Beispielauftrag für die Registerkarte [!UICONTROL Durchsuchen] ausgeführt wird. Sie können sehen, wann das Widget [!UICONTROL Profilanzahl] zuletzt aktualisiert wurde, indem Sie sich den Zeitstempel im Widget ansehen. Weitere Informationen dazu, wie der Beispielauftrag auf der Registerkarte [!UICONTROL Durchsuchen] ausgelöst wird, finden Sie im Abschnitt [Profilanzahl im Handbuch zur Benutzeroberfläche des Echtzeit-Kundenprofils](https://experienceleague.adobe.com/docs/experience-platform/profile/ui/user-guide.html?lang=en#profile-count).

![](../images/profiles/profile-count.png)

### [!UICONTROL Hinzugefügte Profile] {#profiles-added}

Das Widget **[!UICONTROL hinzugefügte Profile]** zeigt die Gesamtzahl der zusammengeführten Profile an, die zum Profilspeicher hinzugefügt wurden, nachdem der letzte Schnappschuss erstellt wurde. Diese Zahl ist das Ergebnis der ausgewählten Zusammenführungsrichtlinie, die auf Ihre Profildaten angewendet wird, um Profilfragmente zu einem einzelnen Profil für jede Person zusammenzuführen. Mit der Dropdown-Auswahl können Sie die Profile anzeigen, die in den letzten 30 Tagen, 90 Tagen oder 12 Monaten hinzugefügt wurden.

>[!NOTE]
>
>Das Widget [!UICONTROL Hinzugefügte Profile] gibt die Anzahl der Profile an, die hinzugefügt wurden, nachdem der Profilspeicher eingerichtet wurde und Profile erfasst wurden. Mit anderen Worten: Wenn Ihr Unternehmen den Profilspeicher eingerichtet und 4.000.000 an Tag 1 aufgenommen hat, wäre das Dashboard innerhalb von 24 Stunden verfügbar, das Widget [!UICONTROL hinzugefügte Profile] würde jedoch auf 0 gesetzt. Dies geschieht, um eine Spitze zu vermeiden, die mit der anfänglichen Aufnahme von Profilen in das System verbunden ist. In den nächsten 30 Tagen nimmt Ihr Unternehmen weitere 1.000.000 Profile in den Profilspeicher auf. Nach der nächsten Momentaufnahme würde das Widget [!UICONTROL hinzugefügte Profile] insgesamt 1.000.000 hinzugefügte Profile anzeigen, während das Widget [!UICONTROL Profilanzahl] insgesamt 5.000.000 Profile anzeigen würde.

![](../images/profiles/profiles-added.png)

### [!UICONTROL Trend der Profilanzahl] {#profiles-count-trend}

Das Widget **[!UICONTROL Trend der Profilanzahl]** zeigt die Gesamtanzahl der zusammengeführten Profile an, die in den letzten 30 Tagen, 90 Tagen oder 12 Monaten täglich zum Profilspeicher hinzugefügt wurden. Diese Zahl wird jeden Tag aktualisiert, wenn die Momentaufnahme erstellt wird. Wenn Sie also Profile in Platform aufnehmen möchten, wird die Anzahl der Profile erst angezeigt, wenn die nächste Momentaufnahme erfolgt. Die Anzahl der hinzugefügten Profile ist das Ergebnis der ausgewählten Zusammenführungsrichtlinie, die auf Ihre Profildaten angewendet wird, um Profilfragmente zusammenzuführen und so für jede Person ein Profil zu erstellen.

Weitere Informationen finden Sie im Abschnitt [zu Zusammenführungsrichtlinien weiter oben in diesem Dokument](#merge-policies) .

![](../images/profiles/profile-count-trend.png)

### [!UICONTROL Profile nach Identität] {#profiles-by-identity}

Das Widget **[!UICONTROL Profile nach Identität]** zeigt die Aufschlüsselung der Identitäten für alle zusammengeführten Profile in Ihrem Profilspeicher an. Die Gesamtzahl der Profile nach Identität (d. h. das Addieren der für jeden Namespace angezeigten Werte) kann höher sein als die Gesamtzahl der zusammengeführten Profile, da einem Profil mehrere Namespaces zugeordnet sein können. Wenn beispielsweise ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Namespaces zugeordnet.

Weitere Informationen finden Sie im Abschnitt [zu Zusammenführungsrichtlinien weiter oben in diesem Dokument](#merge-policies) .

Weitere Informationen zu Identitäten finden Sie in der Dokumentation zum Adobe Experience Platform Identity Service](../../identity-service/home.md).[

![](../images/profiles/profiles-by-identity.png)

### [!UICONTROL Identitätsüberschneidung] {#identity-overlap}

Das Widget **[!UICONTROL Identitätsüberschneidung]** zeigt ein Venn-Diagramm oder Set-Diagramm an, das die Überschneidung von Profilen in Ihrem Profilspeicher mit mehreren Identitäten anzeigt.

Nachdem Sie die zu vergleichenden Identitäten mithilfe der Dropdown-Menüs im Widget ausgewählt haben, werden Kreise angezeigt, die die relative Größe jeder Identität anzeigen. Die Anzahl der Profile, die beide Namespaces enthalten, wird durch die Größe der Überschneidung zwischen den Kreisen dargestellt. Wenn ein Kunde mit Ihrer Marke auf mehr als einem Kanal interagiert, werden diesem einzelnen Kunden mehrere Identitäten zugeordnet. Daher ist es wahrscheinlich, dass Ihr Unternehmen über mehrere Profile verfügt, die Fragmente aus mehr als einer Identität enthalten.

Weitere Informationen zu Profilfragmenten finden Sie im Abschnitt [Profilfragmente im Vergleich zu zusammengeführten Profilfragmenten](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html?lang=en#profile-fragments-vs-merged-profiles) in der Übersicht zum Echtzeit-Kundenprofil.

Weitere Informationen zu Identitäten finden Sie in der Dokumentation zum Adobe Experience Platform Identity Service](../../identity-service/home.md).[

![](../images/profiles/identity-overlap.png)

## Nächste Schritte

Durch Befolgen dieses Dokuments sollten Sie jetzt in der Lage sein, das Profil-Dashboard zu finden und die in den verfügbaren Widgets angezeigten Metriken zu verstehen. Weitere Informationen zum Arbeiten mit [!DNL Profile]-Daten in der Experience Platform-Benutzeroberfläche finden Sie im [Handbuch zur Benutzeroberfläche des Echtzeit-Kundenprofils](../../profile/ui/user-guide.md).
