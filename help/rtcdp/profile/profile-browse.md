---
keywords: Profile anzeigen rtcdp;rtcdp-Profilansicht;rtcdp-Profile
title: Profile in Real-time Customer Data Platform durchsuchen
description: Mit Adobe Real-time Customer Data Platform können Sie Echtzeit-Kundenprofildaten über die Adobe Experience Platform-Benutzeroberfläche durchsuchen.
feature: Get Started, Profiles
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: ea785ffa1dfa0f7c684fe536796a4b7409882159
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 11%

---


# Profile in Real-time Customer Data Platform durchsuchen

Das Echtzeit-Kundenprofil erstellt eine ganzheitliche Ansicht Ihrer einzelnen Kunden und kombiniert Daten aus verschiedenen Kanälen, einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten. Da einzelne Profile auf Grundlage von Daten aggregiert werden, die aus unterschiedlichen Quellen in das System eingespeist werden, wird jedes Profil zu einem umsetzbaren Konto mit Zeitstempel für jede Interaktion, die ein Kunde mit Ihrer Marke hat.

In der Adobe Experience Platform-Benutzeroberfläche können Sie diese schreibgeschützten Profile anzeigen und wichtige Informationen zu jedem Ihrer Kunden anzeigen, einschließlich der Voreinstellungen, vergangener Ereignisse, Interaktionen und der Zielgruppen, zu denen der Kontakt gehört.

Adobe Real-time Customer Data Platform basiert auf Adobe Experience Platform und kann so die Funktionen zur Profilanzeige in der Experience Platform-Benutzeroberfläche nutzen. Eine ausführliche Anleitung zum Anzeigen von Kundenprofilen in der Benutzeroberfläche von Platform finden Sie im [Benutzerhandbuch zum Echtzeit-Kundenprofil](../../profile/ui/user-guide.md).

## Profilverbesserungen für Real-Time CDP, B2B Edition

Zusätzlich zu den von Adobe Experience Platform, Real-Time CDP und B2B Edition unterstützten Profilbrowserfunktionen können Benutzer auf B2B-Attribute und -Ereignisse innerhalb des Kundenprofils auf den Registerkarten [!UICONTROL Attribute] und [!UICONTROL Ereignisse] zugreifen. B2B-Daten können auch für die Segmentierung verwendet werden, wobei diese Zielgruppen neben Nicht-B2B-Zielgruppen auf der Registerkarte [!UICONTROL Zielgruppenmitgliedschaft] des Kunden angezeigt werden.

Mit Real-Time CDP, B2B Edition können Sie auch [!UICONTROL Konten], [!UICONTROL Chancen] und [!UICONTROL Source-Datensätze] aus allen Unternehmensquellen durchsuchen, die mit einem einzelnen Kunden verknüpft sind.

Um diese Verbesserungen zu untersuchen, führen Sie zunächst die im Benutzerhandbuch für das Echtzeit-Kundenprofil](../../profile/ui/user-guide.md) beschriebenen Schritte aus, um ein Profil nach Zusammenführungsrichtlinie oder Identitäts-Namespace zu durchsuchen.[

![](images/b2b-browse-profile.png)

Die Profildetails enthalten Zugriff auf die Registerkarten [!UICONTROL Konten], [!UICONTROL Chancen] und [!UICONTROL Source-Einträge] sowie auf die Standardinformationen im Kundenprofil, die auch durch B2B-Ereignisse und -Attribute erweitert wurden.

![](images/b2b-profile-detail.png)

Weitere Informationen zu den Profildetails, die in der Platform-Benutzeroberfläche bereitgestellt werden, finden Sie im Abschnitt [Details der Dashboard-Dokumentation &quot;Profile&quot;](../../dashboards/guides/profiles.md#browse-profiles).

### Registerkarte &quot;Konten&quot;

Wählen Sie **[!UICONTROL Konten]** aus, um eine Liste der mit dem Profil verbundenen Konten anzuzeigen. Diese Liste enthält grundlegende Informationen aus dem Kontoprofil wie den Namen, die Website und die Branche des Kontos sowie einen Link zum Kontoprofil.

Weitere Informationen zum Anzeigen und Erkunden von Kontoprofilen finden Sie in der [Übersicht über Kontoprofile](../accounts/account-profile-overview.md) .

![](images/b2b-profile-accounts.png)

### Registerkarte „Opportunitys“

Die Registerkarte **[!UICONTROL Chancen]** enthält Details zu den Öffnungs- und Schließungsmöglichkeiten für das Konto. Diese Möglichkeiten können aus verschiedenen Quellen in Experience Platform eingebunden werden, aber Real-Time CDP, B2B Edition macht es für Marketingexperten einfach, all diese Möglichkeiten an einem Ort zu sehen.

Jede Opportunity umfasst Informationen wie den Namen der Opportunity, ihren Umfang, die Phase und ob die Opportunity offen, geschlossen, gewonnen oder verloren ist.

![](images/b2b-profile-opportunities.png)

### Registerkarte &quot;Source-Datensätze&quot;

Mit dem Tab **[!UICONTROL Source-Datensätze]** können Sie mühelos die verschiedenen Quelldatensätze aus Ihren Unternehmensquellen anzeigen, die zum einheitlichen Kundenprofil beitragen. Zusätzlich zum [!UICONTROL Personen-Quellschlüssel] und der E-Mail-Adresse stellt jeder Quelldatensatz auch den Typ des Datensatzes (z. B. einen &quot;Kontakt&quot;- oder &quot;Lead&quot;-Datensatz) sowie die Quelle bereit.

![](images/b2b-profile-source-records.png)
