---
keywords: Profile anzeigen RTCDP;RTCDP-Profilansicht;RTCDP-Profile
title: Durchsuchen von Profilen in Real-Time Customer Data Platform
description: Mit Adobe Real-Time Customer Data Platform können Sie Echtzeit-Kundenprofildaten mithilfe der Benutzeroberfläche von Adobe Experience Platform durchsuchen.
feature: Get Started, Profiles
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 11%

---


# Durchsuchen von Profilen in Real-Time Customer Data Platform

Das Echtzeit-Kundenprofil erstellt eine ganzheitliche Sicht auf Ihre einzelnen Kunden und führt Daten aus verschiedenen Kanälen (Online-, Offline-, CRM- und Drittanbieter-Daten) zusammen. Da einzelne Profile auf Grundlage von Daten aggregiert werden, die aus unterschiedlichen Quellen in das System eingespeist werden, wird jedes Profil zu einem umsetzbaren Konto mit Zeitstempel für jede Interaktion, die ein Kunde mit Ihrer Marke hat.

In der Benutzeroberfläche von Adobe Experience Platform können Sie diese schreibgeschützten Profile anzeigen und wichtige Informationen zu Ihren einzelnen Kundinnen und Kunden anzeigen, einschließlich ihrer Voreinstellungen, vergangener Ereignisse, Interaktionen und der Zielgruppen, zu denen die Person gehört.

Adobe Real-Time Customer Data Platform basiert auf Adobe Experience Platform und kann daher die Funktionen zur Profilanzeige in der Benutzeroberfläche von Experience Platform nutzen. Eine detaillierte Anleitung zum Anzeigen von Kundenprofilen in der Benutzeroberfläche von Experience Platform finden Sie [ Benutzerhandbuch zum Echtzeit-Kundenprofil](../../profile/ui/user-guide.md).

## Profilverbesserungen für Real-Time CDP, B2B Edition

Zusätzlich zu den von Adobe Experience Platform, Real-Time CDP unterstützten Funktionen zum Durchsuchen von Profilen können B2B edition-Benutzende auf den Registerkarten „Attribute[!UICONTROL &#x200B; und „Ereignisse] auf B2B-Attribute und -Ereignisse innerhalb  Kundenprofils zugreifen. B2B-Daten können auch für die Segmentierung verwendet werden, wobei diese Zielgruppen neben Nicht-B2B-Zielgruppen auf der Registerkarte [!UICONTROL Zielgruppenzugehörigkeit] des Kunden angezeigt werden.

Mit Real-Time CDP, B2B edition können Sie auch [!UICONTROL Konten], [!UICONTROL Opportunities] und [!UICONTROL Source-] aus allen Unternehmensquellen durchsuchen, die mit einem einzelnen Kunden verknüpft sind.

Um sich diese Verbesserungen anzusehen, folgen Sie zunächst den Schritten, die im [Benutzerhandbuch zum Echtzeit-Kundenprofil](../../profile/ui/user-guide.md) beschrieben sind, um ein Profil nach Zusammenführungsrichtlinie oder Identity-Namespace zu durchsuchen.

![](images/b2b-browse-profile.png)

Die Profildetails enthalten Zugriff auf die Registerkarten [!UICONTROL Konten], [!UICONTROL Opportunities] und [!UICONTROL Source-]Datensätze) zusätzlich zu den im Kundenprofil bereitgestellten Standardinformationen, die auch um B2B-Ereignisse und -Attribute erweitert wurden.

![](images/b2b-profile-detail.png)

Weitere Informationen zu den in der Benutzeroberfläche von Experience Platform bereitgestellten Profildetails finden Sie im Abschnitt [Details“ der Dokumentation zum Dashboard „Profile](../../dashboards/guides/profiles.md#browse-profiles).

### Registerkarte „Konten“

Wählen Sie **[!UICONTROL Konten]** aus, um eine Liste der mit dem Profil verbundenen Konten anzuzeigen. Diese Liste enthält grundlegende Informationen aus dem Kontoprofil, wie z. B. den Namen, die Website und die Branche des Kontos, sowie einen Link zum Kontoprofil.

Um weitere Informationen zum Anzeigen und Untersuchen von Account-Profilen zu erhalten, lesen Sie zunächst die [Übersicht über Account-Profile](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Registerkarte „Opportunitys“

Die **[!UICONTROL Opportunitys]** enthält Details zu offenen und geschlossenen Opportunitys im Zusammenhang mit dem Account. Diese Opportunitys können aus verschiedenen Quellen in Experience Platform aufgenommen werden. Real-Time CDP, B2B edition, erleichtert es Marketing-Experten jedoch, all diese Opportunitys an einem Ort zu sehen.

Jede Opportunity umfasst Informationen wie den Namen der Opportunity, ihren Umfang, die Phase und ob die Opportunity offen, geschlossen, gewonnen oder verloren ist.

![](images/b2b-profile-opportunities.png)

### Registerkarte &quot;Source-Einträge“

Auf der Registerkarte **[!UICONTROL Source]** Datensätzekönnen Sie die verschiedenen Quelldatensätze aus Ihren Unternehmensquellen, die zu dem einzelnen Kundenprofil beitragen, einfach anzeigen. Neben dem [!UICONTROL Quellschlüssel der Person] und der E-Mail-Adresse enthält jeder Quelldatensatz auch den Typ des Datensatzes (z. B. einen „Kontakt“- oder „Lead“-Datensatz) sowie die Quelle.

![](images/b2b-profile-source-records.png)
