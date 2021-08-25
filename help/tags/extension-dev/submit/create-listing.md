---
title: Erstellen eines Exchange-Listeneintrags für eine Erweiterung
description: Erfahren Sie, wie Sie Ihre Erweiterung dem öffentlichen Katalog in Adobe Experience Platform hinzufügen.
source-git-commit: c8705cfa65cb1d3a738610821ece827c2af33615
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 96%

---

# Erstellen eines Exchange-Listeneintrags für eine Erweiterung

>[!NOTE]
>
>Adobe Experience Platform Launch wurde als eine Suite von Datenerfassungstechnologien in Adobe Experience Platform umbenannt. Infolgedessen wurden in der gesamten Produktdokumentation mehrere Terminologieänderungen eingeführt. Eine konsolidierte Übersicht der terminologischen Änderungen finden Sie im folgenden [Dokument](../../term-updates.md).

Adobe Experience Platform verfügt über einen zentralen Katalog, in dem Anwender Tag-Erweiterungen anzeigen können, die zur Installation verfügbar sind. Dieser Katalog ist innerhalb des Produkts verfügbar und enthält Erweiterungen von drei Typen:

1. **Öffentliche Erweiterungen**: Hierbei handelt es sich um fertige Erweiterungen, die für die Verwendung durch beliebige Benutzer in der Produktion ausgelegt sind.
1. **Private Erweiterungen**: Hierbei handelt es sich um fertige Erweiterungen, die für die Produktion entwickelt wurden, aber von anderen Anwendern in Ihrer Firma entwickelt wurden und nur für Benutzer in Ihrer Firma verfügbar sind.
1. **Entwicklungserweiterungen**: Diese Erweiterungen befinden sich in der aktiven Entwicklung und sind nur in Ihrer Firma und nur für eine Eigenschaft verfügbar, die speziell als Entwicklungseigenschaft gekennzeichnet ist.

Neben den Erweiterungen im Produktkatalog sind im [Experience Cloud Exchange Marketplace](https://exchange.adobe.com/experiencecloud.experience-platform-launch.html#product) auch einige Erweiterungen aufgeführt.

Diese Einträge ermöglichen es Entwicklern von Erweiterungen, Beschreibungen über Funktionen zu posten, Links zu zusätzlichem Support- und Dokumentationsmaterial bereitzustellen sowie Ihre Erweiterungen für potenzielle Anwender zu vermarkten, welche Ihre Firma oder die Funktionen Ihrer Erweiterung möglicherweise noch nicht kennen. Auf diesem Marktplatz verfügt Ihre Erweiterung über eine öffentliche Eintragung, die angezeigt werden kann, ohne dass sich der Benutzer für Platform authentifizieren muss.  Viele Entwickler finden es nützlich, einen Exchange-Eintrag zu erstellen, dies ist jedoch kein erforderlicher Schritt.

Wenn Sie keine Firma haben, um Ihr Erweiterungspaket hochzuladen und zu testen, sollten Sie sich für das Exchange-Programm registrieren und einen Eintrag erstellen.  Dadurch wird die Erstellung eines Firmenkontos ausgelöst (es dauert einige Zeit, bis dies abgeschlossen ist, Sie erhalten daraufhin eine E-Mail), mit dem Sie Ihre Erweiterung hochladen und testen können.  Sie müssen den Eintrag zu keinem Zeitpunkt öffentlich machen.

Wenn Sie bereits über ein Firmenkonto verfügen oder noch nicht planen, Ihren Eintrag abzuschließen, können Sie den Rest dieses Schritts überspringen und mit [Hochladen und Testen Ihrer Erweiterung](./upload-and-test.md) fortfahren.

## Erstellen eines Listeneintrags

>[!NOTE]
>
>Im folgenden Prozess wird die Erstellung eines Listeneintrags im Adobe Exchange-Programm beschrieben. Dieser Begriff wird für die verschiedenen Integrationen und Erweiterungen in Adobe Experience Platform verwendet.

![Link-Speicherort in Experience Cloud App Manager](../images/getting-started/app-mgr-link.png)

1. Melden Sie sich bei der [Exchange Partner-Site](https://partners.adobe.com/exchangeprogram/experiencecloud) an. Klicken Sie nach der Anmeldung auf den Link **App Manager** neben Ihrem Namen.
1. Wählen Sie die Registerkarte **Neue Anwendung erstellen** und dann die Option **Neue App erstellen** für eine benutzerdefinierte Lösung, oder wählen Sie eine entsprechende Vorlage aus.
1. Geben Sie die Informationen für Ihren Eintrag ein. Ausführliche Informationen zum App Manager finden Sie im vollständigen [Artikel](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931). Die Informationen für den Eintrag sollten sehr klar beschreiben, was die Erweiterung tut und warum sie nützlich ist. Der Listeneintrag dient als Marketing-Bereich für Ihre Mobile App. Werben Sie hier mit klaren Beschreibungen, Links zu Landingpages auf Ihrer Site, Links zu Hilfedokumenten oder Support-E-Mail-Adressen usw. für Ihre Erweiterung. Auch wenn der Platz in den Erweiterungsansichten begrenzt ist, bietet der Exchange-Listeneintrag eine Möglichkeit, sowohl Ihre Erweiterung als auch Ihr Unternehmen zu bewerben. Im Folgenden finden Sie Vorschläge zur Verbesserung der Bewerbung Ihrer Erweiterung:
   - **App-Symbol**: Stellen Sie sicher, dass das Symbol für den Exchange-Listeneintrag die entsprechenden Abmessungen (512 x 512 für PNG oder 1:1-Seitenverhältnis für JPG) hat.

      >[!NOTE]
      >
      >Dies ist ein anderes Dateiformat als das in Ihrem Erweiterungs-Code verwendete. Die Erweiterung selbst enthält eine SVG-Datei als [Symbol](../manifest.md).

   - **Angezeigtes Bild** – Ziehen Sie Aufmerksamkeit auf sich, indem Sie ein Bild verwenden, dass aussagekräftig ist, Ihre Marke zeigt und Ihr Programm hervorhebt. Das angezeigte Bild ist zu sehen, wenn ein Benutzer einen Link zu Ihrem Exchange-Listeneintrag oder zu Social-Media-Beiträgen darüber teilt. Es muss daher eine ideale Präsentation Ihrer Marke sein.
   - **Logo des App-Herausgebers**: Dies ist Ihr Firmenlogo. Vergewissern Sie sich, dass das Symbol die entsprechenden Abmessungen von 1280 x 720 oder 2560 x 1440 (16:9) im PNG- oder JPG-Format aufweist.
   - **Konfigurationsanweisungen** – Informieren Sie Kunden darüber, wie Ihre Adobe Experience Platform-Erweiterung konfiguriert werden kann. Vergewissern Sie sich, dass sie alle erforderlichen Einstellungen und die nächsten Schritte verstehen, wenn die [Konfigurationsansicht](../configuration.md) unmittelbar nach der Installation Ihrer Erweiterung in einer Eigenschaft angezeigt wird. 
   - **Tags**: Auf der ersten Seite der Bearbeitung Ihres Listeneintrags sollten Sie unbedingt das Wort „Launch“ in das Feld „Benutzerdefinierte Tags“ aufnehmen. Dadurch erscheint Ihr Listeneintrag bei der Suche nach Tags im Exchange-Marktplatz:
      ![](../images/getting-started/custom-tags.jpg)
   - **Sandboxes** – Ihr Zugriff auf Adobe-Lösungen erfolgt über ein Sandbox-Konto, über das Sie Zugriff auf eine voll funktionsfähige Version von Adobe Experience Platform haben. Diese Sandbox-Accounts werden angefordert, wenn Sie den Listeneintrag für Ihr Programm erstellen. Wählen Sie im Abschnitt **Verbindungen** die spezifischen Verbindungen aus, die für das von Ihnen erstellte Programm (Ihre Tag-Erweiterung) gelten. Wenn Sie auf **Speichern** klicken, wird bei Bedarf die Sandbox-Anfrage generiert.
1. Reichen Sie Ihren Listeneintrag ein. Das Adobe Exchange-Team prüft Ihre Applikation und gibt Ihnen Feedback, wenn Updates erforderlich sind. Wenn Sie das Kontrollkästchen **Sofort veröffentlichen** aktivieren, wenn Sie Ihren Listeneintrag übermitteln, wird dieser sofort nach der Genehmigung veröffentlicht. Wenn Sie Ihr Programm erst zu einem späteren Zeitpunkt veröffentlichen möchten, lassen Sie das Kontrollkästchen deaktiviert. Sobald der Listeneintrag für Ihre Erweiterung genehmigt ist, wird auf der Seite mit den Listeneinträgen für Ihre Programme (Erweiterungen) neben dem entsprechenden Programm eine blaue Schaltfläche **Veröffentlichen** angezeigt.

### Erstellen eines effektiven Listeneintrags

Sehen Sie sich unseren [Leitfaden für die Einreichung von Mobile Apps](https://partners.adobe.com/exchangeprogram/experiencecloud/build/ec-exchange.html) an, um detaillierte Informationen dazu zu erhalten, wie Sie den ansprechendsten Eintrag erstellen.

#### Nach dem Einreichen Ihres Exchange-Listeneintrags

Nach der Einreichung prüft das Adobe Exchange-Team die Applikation und genehmigt sie oder reagiert mit Kommentaren zu erforderlichen Änderungen. Dieser Vorgang wird im Leitfaden für die Einreichung von Applikationen beschrieben.

Wenn Sie nicht über Anmeldedaten für die Exchange-Website verfügen, stellen Sie sicher, dass Ihre E-Mail für das Exchange-Programm registriert ist, indem Sie die Anweisungen im [Leitfaden zur Programmregistrierung](https://partners.adobe.com/content/mcp/us/en/home/reg-guide.html) befolgen. Jeder Benutzer muss seine E-Mail-Adressse mit dem Partnerkonto für sein Unternehmen verknüpfen. Fragen zu diesem Vorgang können per E-Mail an <ExchangeHelpEC@adobe.com> gerichtet werden.

#### Aktualisieren Ihres Exchange-Listeneintrags nach der ersten Genehmigung

Wenn Sie Ihre Erweiterung oder auch lediglich Ihren Exchange-Listeneintrag aktualisieren möchten, melden Sie sich beim [Partner-Portal](https://partners.adobe.com/exchangeprogram/experiencecloud) an und klicken Sie auf den Button „App Manager“ neben Ihrem Namen. Wählen Sie dann Ihr Programm aus und folgen Sie dem obigen Fluss, der ursprünglich zum Erstellen des Listeneintrags verwendet wurde. Nach der erneuten Einreichung prüft das Adobe Exchange-Team die Änderungen und genehmigt entweder die Änderungen oder reagiert mit Kommentaren.

## Verknüpfen Sie Ihr Erweiterungspaket mit Ihrem Eintrag.

Nachdem Ihr Eintrag genehmigt wurde und öffentlich verfügbar ist, empfehlen wir, im Feld `exchange_url` der Datei `extension.json` innerhalb Ihres Erweiterungspakets einen Link zum öffentlichen Eintrag anzugeben.  Dadurch wird ein &quot;Mehr Infos&quot;-Link im Tag-Erweiterungskatalog erstellt, über den Benutzer innerhalb des Produkts Ihre Liste finden und zusätzliche Informationen erhalten können.
