---
title: Schnellstartanleitung
description: Erfahren Sie, wie Sie in Adobe Experience Platform schnell mit Tags arbeiten können.
source-git-commit: 5f810ada57eeb12a56de603d974a091b888dc9d2
workflow-type: tm+mt
source-wordcount: '1562'
ht-degree: 45%

---

# Schnellstartanleitung

>[!NOTE]
>
>Adobe Experience Platform Launch wird als eine Suite von Datenerfassungstechnologien in Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere terminologische Änderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../term-updates.md).

Tags sind die nächste Generation der Tag-Management-Technologie von Adobe Experience Platform. Es wurde von Grund auf neu erstellt, um ein offenes und nachhaltiges Ökosystem zu unterstützen, in dem jeder seine eigenen Integrationen erstellen kann, die Adobe-Kunden auf ihren Sites bereitstellen können. Es handelt sich um eine API-First-Anwendung, sodass alle möglichen Aktionen auf der Benutzeroberfläche auch programmgesteuert über eine API erfolgen können.

Der grundlegende Tags-Workflow:

1. Einrichten von Gruppen und Benutzern.
2. Anmelden.
3. Erstellen einer Eigenschaft.
4. Installieren von Erweiterungen.
5. Erstellen von Datenelementen und Regeln.
6. Testen in Ihrer Entwicklungsumgebung.
7. Weiterleiten an Produktion.

Ein Einführungsvideo finden Sie in der [Einführungsvideos](videos.md) -Dokumentation.

## 1. Einrichten von Gruppen und Benutzern

Tags sind vollständig in Ihre Adobe ID integriert. Benutzerberechtigungen werden über die Admin Console mit anderen Adobe-Produkten und -Lösungen aus dem Experience Cloud [!DNL Creative Cloud], [!DNL Document Cloud] und verwaltet.

Tags verfügen über ein berechtigungsbasiertes Benutzerverwaltungssystem. Das bedeutet, dass individuelle Rechte explizit gewährt werden müssen. Diese Rechte werden Gruppen zugewiesen, dann werden Benutzer den entsprechenden Gruppen hinzugefügt, um Zugriff zu erhalten. Selbst wenn Ihr Unternehmen Zugriff auf die Datenerfassungs-Benutzeroberfläche hat, können einzelne Benutzer nichts tun, bis ihnen ein Org-Administrator ausdrücklich einige Rechte erteilt.

Detaillierte Anweisungen zum Erstellen von Gruppen und Hinzufügen von Benutzern für Tags finden Sie im Dokument [Benutzerberechtigungen](../ui/administration/user-permissions.md) .

## 2. Anmelden

Nachdem Sie Ihrer Adobe ID Tag-Rechte hinzugefügt haben, müssen Sie sich bei der Datenerfassungs-Benutzeroberfläche anmelden. Navigieren Sie dazu direkt zum Bildschirm [Experience Cloud login](https://experiencecloud.adobe.com) und wählen Sie **[!UICONTROL Launch/Data Collection]** auf der Registerkarte Schnellzugriff .

>[!NOTE]
>
>Wenn Sie über ein einzelnes Konto mit Berechtigungen für mehrere Organisationen verfügen, kann die Organisation geändert werden, indem Sie den Organisationsnamen in der Symbolleiste am oberen Bildschirmrand auswählen und in der Dropdown-Liste eine andere Organisation auswählen.

## 3. Erstellen einer Eigenschaft

Nachdem Sie sich bei der Datenerfassungs-Benutzeroberfläche angemeldet haben, erstellen Sie zunächst eine Eigenschaft. Eine Eigenschaft ist im Wesentlichen ein Container, den Sie bei der Bereitstellung von Tags auf Ihrer Site mit Erweiterungen, Regeln, Datenelementen und Bibliotheken füllen. Viele Personen erstellen für jede Website (oder Gruppe eng miteinander verbundener Sites) eine Eigenschaft, in der sie denselben Tag-Satz bereitstellen möchten.

Weitere Informationen zum Erstellen von Eigenschaften finden Sie unter [Erstellen einer Eigenschaft](../ui/administration/companies-and-properties.md).

## 4. Installieren von Erweiterungen

Eine Erweiterung ist eine Integration, die von Adobe oder einem Adobe-Partner erstellt wurde und neue und endlose Optionen für die Tags bietet, die Sie auf Ihren Sites bereitstellen können. Wenn Sie sich ein Tag als Betriebssystem vorstellen, sind Erweiterungen die Apps, die Sie installieren, um die spezifischen Aufgaben auszuführen, die Sie benötigen.

Für alle neuen Eigenschaften ist die [Core-Erweiterung](../extensions/web/core/overview.md) installiert. Mobile Eigenschaften enthalten zusätzliche Erweiterungen. Die Haupterweiterung wird von Adobe erstellt, um einen robusten Standardsatz von Datenelementtypen für Ihre Datenschicht und Ereignistypen für Ihre Regeln bereitzustellen. Die meisten Aktionen, die Sie durchführen (Abrufen einer ECID, Senden von [!DNL Adobe Analytics]-Signalen, Laden der globalen [!DNL Target] Mbox usw.), stammen aus Erweiterungen, die Sie über den Katalog installieren.

Was Tags in Platform wirklich einzigartig macht, ist, dass diese Erweiterungen von jedem erstellt werden können. Sie müssen ein Facebook-Remarketing-Pixel auf Ihrer Site ablegen? Sehen Sie sich die von Facebook erstellte Erweiterung an. Hätten Sie gerne dasselbe für Twitter oder Linked In? Verwenden Sie diese Erweiterungen. Sie müssen eine Umfrage ausführen? Sehen Sie sich Question Pro oder Foresee an. Müssen Sie den Datenschutz und die Einwilligung Ihrer Endbenutzer verwalten, um mit [!DNL GDPR] zu helfen? Sehen Sie sich Evidon und Trust Arc genau an. Möchten Sie detaillierte Einblicke in das Verhalten einzelner Benutzer auf Ihrer Site erhalten? Sehen Sie sich doch einmal Clicktale an. Weitere Informationen finden Sie unter [Hinzufügen neuer Erweiterungen](../ui/managing-resources/extensions/overview.md#add-a-new-extension).

## 5. Erstellen von Datenelementen und Regeln

**Datenelemente** zeigen auf die Informationen, die Sie erfassen und an verschiedene Stellen auf Ihrer Seite senden möchten:

* Eine definierte Datenschicht in JSON
* DOM-Elemente
* Cookies
* Sitzung und lokaler Speicher
* Alles andere

Nachdem das Datenelement definiert wurde, können Sie es überall in der Datenerfassungs-Benutzeroberfläche für jede beliebige Erweiterung verwenden. Weitere Informationen finden Sie in der Dokumentation zu [Datenelemente](../ui/managing-resources/data-elements.md) .

**Regeln** befinden sich im logischen Kern Ihrer Implementierung und legen das Was, Wann, Wo und Wie und wo für alle Tags auf Ihrer Site fest. Definieren Sie ein Ereignis, legen Sie Bedingungen und Ausnahmen fest und definieren Sie dann die Aktionen und die Reihenfolge. Schlussendlich veröffentlichen Sie Ihre Änderungen, um die Ergebnisse zu sehen. Weitere Informationen finden Sie unter [Regeln](../ui/managing-resources/rules.md).

## 6. Testen in Ihrer Entwicklungsumgebung

### Bibliotheken und Builds

Tag-Builds werden nie automatisch veröffentlicht. Alle Änderungen, die Sie vornehmen, werden in eine [Bibliothek](../ui/publishing/libraries.md) eingeschlossen. Alle erstellten Bibliotheken übernehmen automatisch alle vorgelagerten Elemente (veröffentlichte, genehmigte oder gesendete Elemente) als Basis, sodass Sie lediglich die Änderungen definieren müssen, die Sie vornehmen möchten. Diese Bibliothek dient als Entwurf für einen [Build](../ui/publishing/builds.md). Ein Build ist der eigentliche Satz von JavaScript-Dateien, die bereitgestellt und verwendet werden.

Es ist wichtig, die Beziehung zwischen Ihrer Web-Seite, Ihrem Hosting-Standort und Tags zu verstehen.

1. Ihr Hostserver stellt einen Speicherort zum Veröffentlichen des Builds bereit. Der Build selbst enthält die für die Bibliothek erforderlichen JavaScript-Dateien.

   Jede Umgebung weist eine Beziehung zu einem Host auf und der Host stellt einen Endpunkt bereit, der angibt, wo der Build bereitgestellt werden soll. Der Host kann nur zu einer Eigenschaft gehören, obwohl eine Eigenschaft über viele Hosts verfügen kann.

2. Im Formular `<script>` -Tag wird ein Einbettungscode bereitgestellt, der in die `<head>` -Abschnitte Ihrer Website-HTML eingefügt wird.

   Wenn Sie eine Umgebung erstellen und einen Host anhängen, generiert die Umgebung automatisch einen eindeutigen Einbettungscode, mit dem Sie den zugewiesenen Build in Ihre Site integrieren können. Der `<script>`-Code wird verwendet, um den Bibliotheks-Build zur Laufzeit bereitzustellen.

3. Wenn ein Benutzer Ihre Site durchsucht, ruft das Tag `<script>` -Einbettungscode den Build von Ihrem Hostserver ab und führt die definierten Aktionen im Browser aus.

### Hosts

Ein Host ist eine Verbindung zwischen einer Tag-Eigenschaft und Ihrem Hosting-Standort. Tags unterstützen derzeit entweder das von Adobe verwaltete Hosting über einen [!DNL Akamai]-Host oder das selbstständige Hosting über einen SFTP-Host. Wenn Sie einen Build erstellen, stellen Tags eine Verbindung zu dem Server her, der vom Host definiert wurde, und stellen den Build bereit.

Wenn Sie selbst hosten, kann ein Tag-Build direkt über SFTP an Ihre Server übertragen werden. Alternativ können Sie ihn per Push an [!DNL Akamai] übertragen und mithilfe der Archivierungsoption Ihrer Umgebung herunterladen.

Weitere Informationen finden Sie unter [Hosts](../ui/publishing/hosts/hosts-overview.md).

### Umgebungen

Jede Bibliothek wird in einer Umgebung erstellt. Mit einer Umgebung wird definiert, wie der Build aussehen soll, wenn er veröffentlicht wird. Sie können Folgendes angeben:

* **Host:** Jede Umgebung benötigt einen Host, der den Endpunkt bestimmt, an den alle in dieser Umgebung erstellten Builds weitergeleitet werden.
* **Archivieren:** Die Standardeinstellung besteht darin, Ihren Build als minimierte JS-Datei bereitzustellen. Wenn Sie benutzerdefinierten Code verwenden, können mehrere Dateien vorliegen, die sich gegenseitig referenzieren. Diese können zu einer einzelnen ZIP-Datei kombiniert und verschlüsselt werden.

Nachdem Sie Ihre Umgebung gespeichert haben, generiert sie den eingebetteten Code, den Sie kopieren und in Ihre Website einfügen können. Beachten Sie, dass der Einbettungscode erst funktioniert, nachdem Sie eine Bibliothek erstellt und einen Build erstellt haben. Weitere Informationen finden Sie unter [Umgebungen](../ui/publishing/environments.md).

### Veröffentlichen eines Builds in der Entwicklung

Der Veröffentlichungsprozess wird in den folgenden Schritten beschrieben.

1. Erstellen Sie einen Host.
1. Erstellen Sie eine Entwicklungsumgebung mit dem von Ihnen erstellten Host.
1. Stellen Sie den eingebetteten Code aus Ihrer Entwicklungsumgebung auf Ihrer Entwicklungstest-Site bereit.
1. Erstellen Sie eine Bibliothek und weisen Sie sie der von Ihnen erstellten Entwicklungsumgebung zu.
1. Erstellen Sie Ihre Bibliothek.

## 7. Weiterleiten an Produktion

Nachdem Sie Ihren Build in Ihrer Entwicklungsumgebung getestet haben, stellen Sie sicher, dass Sie Ihre Staging- und Produktionsumgebungen erstellen und die eingebetteten Codes an den erforderlichen Stellen platzieren. Sie können zu diesem Zweck vorhandene Hosts wiederverwenden.

Wenn Sie eine Bibliothek vollständig bis zur Produktion weiterleiten, müssen Sie in der Regel die Koordination verschiedener Personen mit den entsprechenden Rechten gewährleisten.

* Ein Entwickler (ein Benutzer mit Entwicklungsrechten) sendet die Bibliothek, wodurch die Bibliothek in den Status „Gesendet“ wechselt.
* Ein Genehmiger (ein Benutzer mit Genehmigungsrechten) kann die Bibliothek in der Phasenumgebung erstellen und sie nach dem Testen genehmigen. Dadurch wird die Bibliothek in den Status „Genehmigt“ versetzt. Es kann jeweils nur eine Bibliothek gesendet und genehmigt werden.
* Ein Herausgeber (ein Benutzer mit Veröffentlichungsrechten) kann die Bibliothek in der Produktionsumgebung erstellen.

Sie können alle diese Rechte einer einzelnen Person zuweisen.

Weitere Informationen zu den verschiedenen Status und Optionen, die während des Veröffentlichungsvorgangs verfügbar sind, finden Sie unter [Genehmigungs-Workflow](../ui/publishing/publishing-flow.md).

## Zusätzliche Ressourcen

Weitere Informationen zu Tags finden Sie in diesen Ressourcen:

[https://forums.adobe.com/community/experience-cloud/platform/launchAsk](https://forums.adobe.com/community/experience-cloud/platform/launchAsk), wo Sie auch Fragen beantworten, Ideen einreichen und über die Ideen anderer Benutzer abstimmen können. Melden Sie sich mit Ihrer Adobe ID an.

* **[Datenerfassungs-Community](https://forums.adobe.com/community/experience-cloud/platform/launch)**: Stellen und beantworten Sie Fragen, reichen Sie Ideen ein, stimmen Sie über die Ideen anderer Benutzer ab. Melden Sie sich mit Ihrer Adobe ID an.
* **[Entwicklerdokumente](https://developer.adobelaunch.com/)**: Einbindung in die -Tag-Entwickler-Community, um Erweiterungen zu erstellen oder die -Tags-APIs zu verwenden
* **[Tutorials - Überblick](https://experienceleague.adobe.com/docs/core-services-learn/tutorials/overview.html?lang=de)**: Diese Dokumente enthalten eine Einführung in Tag-Konzepte, einschließlich Ereignisweiterleitung und Mobile SDK in Android-Apps.
