---
keywords: Anzeigen von Profilen rtcdp;rtcdp-Profilansicht;rtcdp-Profile
title: Profile in Real-time Customer Data Platform durchsuchen
description: Mit Real-time Customer Data Platform können Sie Echtzeit-Kundenprofildaten über die Adobe Experience Platform-Benutzeroberfläche durchsuchen.
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: c15f59de49c60f55b432a39f30fb5f1865fd4671
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 24%

---


# Profile in Real-time Customer Data Platform durchsuchen

Das Echtzeit-Kundenprofil erstellt eine ganzheitliche Sicht Ihrer einzelnen Kunden und fasst Daten aus mehreren Kanälen (einschließlich Online-, Offline-, CRM- und Drittanbieter-Daten) zusammen. Da einzelne Profile auf Grundlage von Daten aggregiert werden, die aus unterschiedlichen Quellen in das System eingespeist werden, wird jedes Profil zu einem umsetzbaren Konto mit Zeitstempel für jede Interaktion, die ein Kunde mit Ihrer Marke hat.

In der Adobe Experience Platform-Benutzeroberfläche können Sie diese schreibgeschützten Profile anzeigen und wichtige Informationen zu jedem Ihrer Kunden anzeigen, einschließlich der Voreinstellungen, vergangener Ereignisse, Interaktionen und der Segmente, zu denen der Kontakt gehört.

Real-time Customer Data Platform basiert auf Adobe Experience Platform und kann so die Funktionen zur Profilanzeige in der Experience Platform-Benutzeroberfläche nutzen. Eine ausführliche Anleitung zum Anzeigen von Kundenprofilen in der Benutzeroberfläche von Platform finden Sie im Abschnitt [Benutzerhandbuch zum Echtzeit-Kundenprofil](../../profile/ui/user-guide.md).

## Profilverbesserungen für die Echtzeit-Kundendatenplattform, B2B Edition (Beta)

>[!IMPORTANT]
>
>Real-time Customer Data Platform B2B Edition befindet sich derzeit in der Beta-Phase. Dokumentation und Funktionalität können sich ändern.

Zusätzlich zu den von Adobe Experience Platform unterstützten Funktionen zum Durchsuchen von Profilen können Benutzer der Echtzeit-Kundendatenplattform und B2B Edition auf B2B-Attribute und -Ereignisse im Kundenprofil im [!UICONTROL Attribute] und [!UICONTROL Veranstaltungen] Registerkarten. B2B-Daten können auch für die Segmentierung verwendet werden, wobei diese Segmente unter dem [!UICONTROL Segmentmitgliedschaft] neben Nicht-B2B-Segmenten.

Die Echtzeit-Kundendatenplattform B2B Edition ermöglicht Ihnen auch das Durchsuchen von [!UICONTROL Konten], [!UICONTROL Chancen]und [!UICONTROL Quelldatensätze] aus allen Quellen Ihres Unternehmens, die mit einem einzelnen Kunden verknüpft sind.

Um diese Verbesserungen zu untersuchen, führen Sie zunächst die Schritte aus, die im Abschnitt [Benutzerhandbuch zum Echtzeit-Kundenprofil](../../profile/ui/user-guide.md) um ein Profil nach Zusammenführungsrichtlinie oder Identitäts-Namespace zu durchsuchen.

![](images/b2b-browse-profile.png)

Zu den Profildetails gehört der Zugriff auf [!UICONTROL Konten], [!UICONTROL Chancen]und [!UICONTROL Quelldatensätze] Registerkarten zusätzlich zu den im Kundenprofil bereitgestellten Standardinformationen, die auch mit B2B-Ereignissen und -Attributen erweitert wurden.

![](images/b2b-profile-detail.png)

### Registerkarte „Konten“

Auswählen **[!UICONTROL Konten]** um eine Liste der mit dem Profil verbundenen Konten anzuzeigen. Diese Liste enthält grundlegende Informationen aus dem Kontoprofil wie den Namen, die Website und die Branche des Kontos sowie einen Link zum Kontoprofil.

Weitere Informationen zum Anzeigen und Erkunden von Kontoprofilen erhalten Sie im Abschnitt [Übersicht über Kontoprofile](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Registerkarte „Opportunitys“

Die **[!UICONTROL Chancen]** -Tab enthält Details zu den mit dem Konto verbundenen Öffnungs- und Schließungsmöglichkeiten. Diese Opportunitys können aus verschiedenen Quellen in Experience Platform aufgenommen werden. Real-Time Customer Data Platform B2B Edition erleichtert es Marketing-Experten jedoch, all diese Opportunitys an einem Ort zu sehen.

Jede Opportunity umfasst Informationen wie den Namen der Opportunity, ihren Umfang, die Phase und ob die Opportunity offen, geschlossen, gewonnen oder verloren ist.

![](images/b2b-profile-opportunities.png)

### Registerkarte &quot;Quelldatensätze&quot;

Die **[!UICONTROL Quelldatensätze]** -Tab können Sie mühelos die verschiedenen Quelldatensätze anzeigen, die aus Ihren Unternehmensquellen stammen und zum einzelnen Kundenprofil beitragen. Zusätzlich zu den [!UICONTROL Person source key] und der E-Mail-Adresse, enthält jeder Quelldatensatz auch den Typ des Datensatzes (z. B. einen &quot;Kontakt&quot;- oder &quot;Lead&quot;-Datensatz) sowie die Quelle.

![](images/b2b-profile-source-records.png)
