---
title: Registerkarte "Zusammenfassung"
description: Erfahren Sie, wie Sie die Registerkarte "Zusammenfassung"im Adobe Experience Platform Debugger verwenden.
keywords: Debugger;Experience Platform Debugger-Erweiterung;Chrome;Erweiterung;Zusammenfassung;clear;Anfragen;Zusammenfassungsbildschirm;Lösung;Informationen;Analytics;Target;DTM;Audience Manager;Launch;ID-Dienst
seo-description: Experience Platform Debugger Summary Screen
seo-title: Summary Tab
uuid: 46b17eaa-b611-43cf-8c6a-67b2e9b9d940
exl-id: 91234125-15c4-4111-9ee4-f3af093a3c4d
source-git-commit: f94bba7eb4763230dae6794eb70a75f53a853c53
workflow-type: tm+mt
source-wordcount: '909'
ht-degree: 74%

---

# Registerkarte &quot;Zusammenfassung&quot;

Um Adobe Experience Platform Debugger auszuführen, öffnen Sie die Seite, die Sie im Browser untersuchen möchten, und wählen Sie dann das Symbol (![](images/start-icon.jpg)) in Ihrer Browser-Leiste. Die Erweiterung wird im **Zusammenfassung** Registerkarte.

![](images/summary.jpg)

Auf diesem Bildschirm werden Informationen zu den verschiedenen Adobe Experience Cloud-Lösungen angezeigt. Die angezeigten Informationen unterscheiden sich je nach Lösung. In der Regel sind jedoch Details wie Lösungsbibliothek und -version (z. B. „AppMeasurement v2.9“) sowie Konto-IDs (wie z. B. die Analytics Report Suite ID, der Target-Kundencode, die Audience Manager-Partner-ID usw.) enthalten.

## In Experience Platform Debugger angezeigte Informationen

Experience Platform Debugger zeigt die folgenden Informationen zu den verschiedenen Lösungen an:

**Adobe Analytics**

<table id="table_BEB9CC58E59D4D86BC895A8A51D84A2C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Report Suite(s) </p> </td> 
   <td colname="col2"> <p>Eine <a href="https://experiencecloud.adobe.com/resources/help/de_DE/reference/report_suites_admin.html" format="html" scope="external">Report Suite</a> definiert die vollständige, unabhängige Berichterstellung über eine bestimmte Website, eine Gruppe von Websites oder eine Untergruppe von Seiten einer Webseite. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Version </p> </td> 
   <td colname="col2"> <p>Die für die Seite definierte <a href="https://experienceleague.adobe.com/docs/analytics/implementation/js/overview.html?lang=de" format="html" scope="external"> AppMeasurement</a>-Version. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Besucherversion </p> </td> 
   <td colname="col2"> <p>Die Version der <a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html?lang=de" format="html" scope="external">Besucher-ID</a>-Bibliothek. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Webseitenname </p> </td> 
   <td colname="col2"> <p>Die Variable <a href="https://experiencecloud.adobe.com/resources/help/de_DE/sc/implement/pageName.html" format="html" scope="external">pageName</a>, die an Analytics gesendet wird und einen benutzerfreundlichen Namen der Seite enthält. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Module </p> </td> 
   <td colname="col2"> <p>Die von Adobe Analytics geladenen Module. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Audience Manager**

<table id="table_784AEABADBDA4D14BB9A7A9CB9EF07C3"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Partner </p> </td> 
   <td colname="col2"> <p>Der <a href="https://experiencecloud.adobe.com/resources/help/de_DE/aam/r_dil_get_partner.html" format="html" scope="external">Partnername</a> für die DIL-Instanz. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Version </p> </td> 
   <td colname="col2"> <p>Die <a href="https://experiencecloud.adobe.com/resources/help/de_DE/aam/r_api_return_versions_dil.html" format="html" scope="external">Versionsnummer</a> für die DIL-Instanz. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>UUID </p> </td> 
   <td colname="col2"> <p>Die <a href="https://experiencecloud.adobe.com/resources/help/de_DE/aam/ids-in-aam.html" format="html" scope="external">eindeutige Benutzer-ID</a>, die der DIL-Instanz zugeordnet ist. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Experience Platform Tags**

<table id="table_E9574975444A407887E26514D1BB1601"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Name </p> </td> 
   <td colname="col2"> <p>Der Name des Tags <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/admin/companies-and-properties.html" format="https" scope="external"> property</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Version </p> </td> 
   <td colname="col2"> <p>Die Turbine-Version.</a> </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Build-Datum </p> </td> 
   <td colname="col2"> <p>Das Tag <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/libraries.html" format="https" scope="external"> Bibliothek</a> Build-Datum </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Umgebung </p> </td> 
   <td colname="col2"> <p>Die <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/publish/environments/environments.html" format="https" scope="external"> Umgebung</a> von der Tag-Bibliothek verwendet </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Erweiterungen </p> </td> 
   <td colname="col2"> <p>Die auf der Seite verwendeten Erweiterungen. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Experience Platform Web SDK**

<table id="table_DC76D63FA6EF4891906B9E1D3E4A8A6C"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Bibliotheksversion </p> </td> 
   <td colname="col2"> <p>Die Nummer der Adobe Experience Platform Web SDK-<a href="https://experienceleague.adobe.com/docs/experience-platform/edge/extension/web-sdk-ext-release-notes.html" format="html" scope="external">Bibliotheksversion</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Namespace</p> </td> 
   <td colname="col2"> <p>Der in der Erweiterung angegebene Name.</p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Property-ID </p> </td> 
   <td colname="col2"> <p>Der Name der in der Erweiterung angegebenen Tag-Eigenschaft. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Edge-Domäne </p> </td> 
   <td colname="col2"> <p>Die Domain, von der die Adobe Experience Platform-Erweiterung Daten sendet und empfängt. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>IMS-Organisations-ID </p> </td> 
   <td colname="col2"> <p>Die Organisation, an die Adobe die Daten entsprechend der Angabe in der Erweiterung senden soll. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Protokollierung aktiviert </p> </td> 
   <td colname="col2"> <p>Gibt an, ob die Protokollierung für diese Property aktiviert wurde.</p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Experience Cloud ID-Dienst**

<table id="table_274CFCEFA8F34D16BB546B4669EC0209"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Experience Cloud Org ID </p> </td> 
   <td colname="col2"> <p>Ihre <a href="https://experiencecloud.adobe.com/resources/help/de_DE/mcvid/" format="https" scope="external"> Organisations-ID</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Version </p> </td> 
   <td colname="col2"> <p>Die Version der <a href="https://experienceleague.adobe.com/docs/analytics/import/data-sources/data-types-and-categories/datasrc-visitorid.html" format="html" scope="external">Besucher-ID</a>-Bibliothek. </p> </td> 
  </tr> 
 </tbody> 
</table>

**Adobe Target**

<table id="table_D30E0CD20FB04E41862B22655136E043"> 
 <tbody> 
  <tr> 
   <td colname="col1"> <p>Clientcode </p> </td> 
   <td colname="col2"> <p>Ihr Target-<a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/deploy-at-js/implementing-target-without-a-tag-manager.html" format="html" scope="external"> Kundencode</a>. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Version </p> </td> 
   <td colname="col2"> <p>Ihre aktuelle <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/at-js-implementation/target-atjs-versions.html" format="html" scope="external"> at.js</a>- oder mbox.js-Version. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Globaler Anforderungsname </p> </td> 
   <td colname="col2"> <p>Die<a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html" format="html" scope="external"> globale Mbox</a> bezieht sich auf den einzelnen Server-Aufruf, der oben auf jeder Webseite in Ihrer Target-Implementierung durchgeführt wird. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Ereignis zum Laden der Seite </p> </td> 
   <td colname="col2"> <p>Der Typ des <a href="https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/adobe/target/overview.html?lang=de" format="html" scope="external">Ereignisses</a>, das beim Laden der Seite ausgelöst wird. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Name einer Anfrage </p> </td> 
   <td colname="col2"> <p>Der Name einer Anfrage zu einer <a href="https://experienceleague.adobe.com/docs/target/using/implement-target/client-side/global-mbox/understanding-global-mbox.html" format="html" scope="external"> Position</a> auf der Seite. Ist nur dann ohne Authentifizierung verfügbar, wenn Sie den Debugging-Ereignis-Listener in Ihren Code oder Tag-Manager implementieren und die erforderlichen <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> Antwort-Tokens</a> in der Target-Benutzeroberfläche aktivieren. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Aktivitätsname </p> </td> 
   <td colname="col2"> <p>Name der Target-<a href="https://experienceleague.adobe.com/docs/target/using/activities/activities.html" format="html" scope="external"> Kampagne oder -Aktivität</a>. Ist nur dann ohne Authentifizierung verfügbar, wenn Sie den Debugging-Ereignis-Listener in Ihren Code oder Tag-Manager implementieren und die erforderlichen <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> Antwort-Tokens</a> in der Target-Benutzeroberfläche aktivieren. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Activity ID </p> </td> 
   <td colname="col2"> <p>Die ID der Target-Aktivität. Ist nur dann ohne Authentifizierung verfügbar, wenn Sie den Debugging-Ereignis-Listener in Ihren Code oder Tag-Manager implementieren und die erforderlichen <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> Antwort-Tokens</a> in der Target-Benutzeroberfläche aktivieren. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Name des Erlebnisses </p> </td> 
   <td colname="col2"> <p>Name des Target-<a href="https://experienceleague.adobe.com/docs/target/using/experiences/experiences.html" format="html" scope="external"> Erlebnisses</a>. Ist nur dann ohne Authentifizierung verfügbar, wenn Sie den Debugging-Ereignis-Listener in Ihren Code oder Tag-Manager implementieren und die erforderlichen <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> Antwort-Tokens</a> in der Target-Benutzeroberfläche aktivieren. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Erlebnis-ID </p> </td> 
   <td colname="col2"> <p>Die ID des Target-Erlebnisses. Ist nur dann ohne Authentifizierung verfügbar, wenn Sie den Debugging-Ereignis-Listener in Ihren Code oder Tag-Manager implementieren und die erforderlichen <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> Antwort-Tokens</a> in der Target-Benutzeroberfläche aktivieren. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Angebot Name</p> </td> 
   <td colname="col2"> <p>Name des Target-<a href="https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html" format="html" scope="external"> Angebots</a>. Ist nur dann ohne Authentifizierung verfügbar, wenn Sie den Debugging-Ereignis-Listener in Ihren Code oder Tag-Manager implementieren und die erforderlichen <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> Antwort-Tokens</a> in der Target-Benutzeroberfläche aktivieren. </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <p>Offer ID </p> </td> 
   <td colname="col2"> <p>Die ID des Target-Angebots. Ist nur dann ohne Authentifizierung verfügbar, wenn Sie den Debugging-Ereignis-Listener in Ihren Code oder Tag-Manager implementieren und die erforderlichen <a href="https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html" format="html" scope="external"> Antwort-Tokens</a> in der Target-Benutzeroberfläche aktivieren. </p> </td> 
  </tr> 
 </tbody> 
</table>
