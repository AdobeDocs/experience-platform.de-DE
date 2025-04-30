---
solution: Experience Platform
title: Erfahren Sie, wie Sie mit dem KI-Assistenten Ihre eigenen Playbooks erstellen und freigeben können.
description: So erstellen Sie eigene Playbooks für Anwendungsfälle und geben diese frei.
role: User
exl-id: 0bc49710-ad9e-4509-b7e6-55f9b9037aa9
source-git-commit: 401062fbea8845f16803edb72ccb14b75c3f8409
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 0%

---


# Erstellen und Freigeben eigener Playbooks (Beta)

Mit dem [!DNL Playbook Authoring Framework], der von AI Assistant in Adobe Experience Platform unterstützt wird, können Sie Playbooks in Adobe Experience Platform effizient erstellen, verwalten und freigeben.

Das Framework folgt einem dreistufigen Prozess:

1. **Metadatenerfassung**: Verwenden Sie den KI-Assistenten oder das Webformular, um Playbook-Metadaten zu erfassen.

2. **Technische Verknüpfung**: Dem Playbook werden spezifische technische Assets wie Journey oder Zielgruppen hinzugefügt. Sie behalten die volle Kontrolle über den Prozess der Playbook-Erstellung in Ihrer Entwicklungs-Sandbox, um sicherzustellen, dass er mit Ihren Schemata und anderen eindeutigen Datenstrukturen übereinstimmt.

3. **Playbook-Verteilung**: Freigeben von Playbooks über verschiedene Organisationen hinweg. So kann beispielsweise das deutsche Martech Center of Excellence von ACME ein „goldenes“ Playbook erstellen und es an regionale Organisationen in Thailand, Australien usw. verteilen. um den Marketing-Anwendungsfall zu standardisieren.

## Playbook erstellen

Sie können ein Playbook auf zwei Arten erstellen: entweder mithilfe des KI-Assistenten oder manuell. Lesen Sie die folgenden Abschnitte, um zu erfahren, wie Sie mit dem KI-Assistenten ein Playbook erstellen.

### Playbook - Übersicht

Führen Sie die folgenden Schritte aus, um ein Playbook mit dem KI-Assistenten zu erstellen:

Wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Playbooks]**.

![ „Playbooks“ im linken Navigationsbereich der Benutzeroberfläche hervorgehoben.](/help/use-case-playbooks/assets/playbooks/authoring/playbooks.png)

Wählen Sie **[!UICONTROL Neues Playbook]** und dann **Playbook mit KI-Assistenten erstellen** aus.

![Die Playbook-Oberfläche mit der Auswahl „Playbook mit KI-Assistenten generieren“.](/help/use-case-playbooks/assets/playbooks/authoring/generate-playbook.png)

Beschreiben Sie den Anwendungsfall mithilfe des Eingabeaufforderungsfelds. z. B.:

„Wenden Sie sich an ACME-Kunden, die Laufschuhe durchsucht, den Kauf jedoch nicht abgeschlossen haben.“

![Die Playbook-Oberfläche mit hervorgehobenem Webformularbereich.](/help/use-case-playbooks/assets/playbooks/authoring/prompt.png)

Wählen Sie **[!UICONTROL Generieren]** aus, um die Playbook-Metadaten zu erstellen.

![Der Eingabeaufforderungsbereich mit der hervorgehobenen Schaltfläche „Playbook generieren“.](/help/use-case-playbooks/assets/playbooks/authoring/generate.png)

Klicken Sie nach der Generierung **[!UICONTROL Bearbeiten]**, um den generierten Titel, die Beschreibung und die Metadaten nach Bedarf zu ändern.

![Das generierte Playbook mit der hervorgehobenen Schaltfläche „Bearbeiten“.](/help/use-case-playbooks/assets/playbooks/authoring/edit.png)

Um sicherzustellen, dass die Dateningenieure über alle erforderlichen Details zum Einrichten des Anwendungsfalls verfügen, füllen Sie den Abschnitt **[!UICONTROL Playbook-]**&quot; aus. Diese Felder sind optional, helfen jedoch bei der Erfassung wichtiger Informationen und erleichtern die Verbindung der richtigen technischen Komponenten. Wählen Sie **[!UICONTROL Bearbeiten]** aus, um den folgenden Feldern Werte hinzuzufügen:

* **Branche**
* **Zielgruppe**
* **Marketing-Kanal**

![Der Abschnitt mit den Playbook-Details mit der hervorgehobenen Schaltfläche „Bearbeiten“.](/help/use-case-playbooks/assets/playbooks/authoring/edit-details.png)

Nachdem die Metadaten generiert wurden, wählen Sie **[!UICONTROL Journey-Map bearbeiten]** aus, um die Schritte in der Journey-Map nach Bedarf anzupassen.

![Bearbeiten der Journey-Zuordnungs-Schaltfläche.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map-button.png)

![Bearbeiten Sie die Journey-Zuordnung, sobald Sie die Playbook-Metadaten erfasst haben.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map.png)

Verknüpfen Sie dann das Playbook mit technischen Assets. Um ein Playbook manuell zu erstellen, wählen Sie **[!UICONTROL Playbook manuell erstellen]**.

![Playbook manuell erstellen](/help/use-case-playbooks/assets/playbooks/authoring/create-manually.png)

Eine leere Playbook-Vorlage wird angezeigt. Füllen Sie Details wie &quot;**&quot;** &quot;**&quot;**. Sie können auch die Journey-Zuordnung bearbeiten, um nach Bedarf Ereignisse und Touchpoints hinzuzufügen.

## Playbook mit technischen Assets verknüpfen

Unabhängig davon, ob Sie ein Playbook manuell oder mit dem KI-Assistenten erstellen, müssen Sie es mit den erforderlichen technischen Assets verknüpfen. Navigieren Sie zur Registerkarte **[!UICONTROL Technische Assets]** und wählen Sie das gewünschte Produkt aus. Wählen Sie für dieses Beispiel **[!UICONTROL Journey Optimizer]**.

>[!NOTE]
>
> Die Unterstützung für Real-Time CDP wird in einer zukünftigen Version hinzugefügt.

![Die Registerkarte „Technische Assets“ und die Schaltfläche „Erforderliches Produkt hinzufügen“ sind hervorgehoben.](/help/use-case-playbooks/assets/playbooks/authoring/technical-assets-add-required-product.png)

Wählen Sie **[!UICONTROL Asset auswählen]**, um dieses Playbook mit einer Journey zu verknüpfen, wie in der Abbildung unten dargestellt. Wählen Sie dann **Playbook veröffentlichen**, um das Playbook abzuschließen.

![ Schaltfläche „Assets auswählen“ auf der Registerkarte „Technische Assets“ hervorgehoben](/help/use-case-playbooks/assets/playbooks/authoring/select-assets.png)

![Journey auswählen](/help/use-case-playbooks/assets/playbooks/authoring/journey.png)

Nach der Veröffentlichung extrahiert das Playbook automatisch das Journey-Schema und die Zielgruppendetails und verknüpft sie.

![Veröffentlichtes Playbook](/help/use-case-playbooks/assets/playbooks/authoring/publish-playbook.png)

Alle erstellten Playbooks sind auf der Registerkarte &quot;**Playbooks“**.

![ Registerkarte „Ihre Playbooks“](/help/use-case-playbooks/assets/playbooks/authoring/your-playbooks-tab.png)

Sie können jedes Playbook aus dem Katalog auswählen, um Instanzen zur Wiederverwendung zu erstellen. Weitere Informationen finden Sie in der Dokumentation [Erstellen von Instanzen](/help/use-case-playbooks/playbooks/create-share-reuse.md).

![ Option „Instanz erstellen“ auf der Registerkarte „Playbook-Übersicht“ hervorgehoben, sobald Sie ein Playbook auswählen.](/help/use-case-playbooks/assets/playbooks/authoring/create-instance.png)

>[!NOTE]
>
> Nachdem ein Playbook veröffentlicht wurde, kann es nicht mehr bearbeitet werden. Um Änderungen vorzunehmen, löschen Sie das Playbook und beginnen Sie von vorne.

## Beispiel-Eingabeaufforderungen

Der KI-Assistent kann verschiedene Aufforderungsstrukturen verarbeiten und wichtige Details extrahieren, während er unnötige Informationen herausfiltert. Im Folgenden finden Sie einige Beispiele für Benutzeraufforderungen und deren Interpretation durch das System:

**Beispiel 1:**

„Erstellen Sie eine Kampagne mit dem Titel „Vervollständigen Sie den Look“, um den Umsatz und den CLV zu steigern. Die Kampagne ermutigt Kundinnen und Kunden, die Küchenartikel oder Möbel gekauft haben, einen ergänzenden Kauf über personalisierte Empfehlungen und Angebote im Zusammenhang mit ihrem Kauf abzuschließen. Erste Nachricht an die Kunden mit Produktempfehlungen. Wenn er innerhalb von 7 Tagen keine Käufe tätigt, erhält er eine zweite Nachricht mit Produktempfehlungen und Angeboten. Verwenden Sie Push-Benachrichtigungen und E-Mail, um die Kunden zu kontaktieren. Targeting von Kunden, die in den letzten 7 Tagen einen Kauf in der Kategorie Küchenartikel oder Möbel getätigt haben und in den letzten 30 Tagen nicht kontaktiert wurden. Im Rahmen der Kampagne möchten wir KPIs wie Klicks (E-Mail, Mobile App, SMS, Push), CTR, E-Wallet, CTR, AOV Conversion.CLV-Umsatz, Kaufereignisse insgesamt (im Geschäft, digital, Callcenter) messen.“

![Beispiel mit einer langen Eingabeaufforderung im Texteingabefeld](/help/use-case-playbooks/assets/playbooks/authoring/long-prompt.png)

**Beispiel 2:**

„Projektname: Fashion Newsletter
Hintergrund: (Proaktiv oder Problemlösung): Eine Journey, die dazu dient, Mode-Newsletter an ACME-Kunden zu senden, die sich für die Newsletter-Kommunikation angemeldet haben.
Ziel: Versand von Newsletter-E-Mails an Kunden von ACME, die sich für die Kommunikation angemeldet haben.
Werbedetails: Der Kunde erhält wöchentlich Modenachrichten im E-Mail-Kanal. Die E-Mail sollte personalisiert sein und Inhaltsvarianten basierend auf Geschlecht, Sprache und Markt aufweisen.
Projektkanäle/Touchpoints: E-Mail
Zielgruppe: Kunden, die sich für Newsletter-Nachrichten von ACME Fashion angemeldet haben.
Ziel-KPIs/Interaktionsmetriken/ROI: 1. Steigern Sie den Umsatz durch Produkte. 2. Fördern Sie die Kundentreue.“

![Beispiel für eine organisierte Eingabeaufforderung im Texteingabefeld](/help/use-case-playbooks/assets/playbooks/authoring/organized-list-prompt.png)

**Beispiel 3:**

„Ermutigen Sie Kunden, während einer laufenden Produktwerbekampagne Produkte zu kaufen.
Interagieren Sie mit Käufern während einer laufenden Promotion, indem Sie geeignete Kommunikation per E-Mail, SMS oder Push-Benachrichtigungen senden, um Produkte zu kaufen. Senden Sie ihnen nach 24 Stunden, in denen sie nicht an der Promotion teilnehmen, eine Erinnerungs-E-Mail.“

![Beispiel mit einer knappen Eingabeaufforderung im Texteingabefeld](/help/use-case-playbooks/assets/playbooks/authoring/concise-prompt.png)

**Beispiel 4:**

„Verkaufe Schuhe an High School-Spieler.“

![Beispiel für eine Einzeiler-Eingabeaufforderung](/help/use-case-playbooks/assets/playbooks/authoring/one-liner-prompt.png)

Der KI-Assistent entfernt alle unnötigen Details wie „Projektname“ oder „Hintergrund“. Es extrahiert die Schlüsselelemente wie „Zielgruppe“, „Kampagnenziel“ und „Marketing-Kanal“ und funktioniert mit jedem Eingabestil.

Diese Beispiele zeigen, wie KI wichtige Details aus Benutzeraufforderungen verfeinern und extrahieren kann.

>[!NOTE]
>
> Vermeiden Sie beim Schreiben Ihrer Eingabeaufforderungen personenbezogene Daten oder explizite Wörter.

## Inhaltsrichtlinien und Moderation

Achten Sie beim Erstellen von Playbooks auf die Sprache und die Inhalte, die Sie einbeziehen. Playbooks sind in Ihrer gesamten Organisation sichtbar, und Benutzer können beleidigende oder unangemessene Inhalte markieren.

### Kennzeichnungs- und Überprüfungsprozess

Wenn ein Playbook für unangemessene oder anstößige Inhalte markiert wird, wird es automatisch zur Überprüfung an Adobe gemeldet. Adobe überprüft dann den gekennzeichneten Inhalt, und wenn er als unangemessen betrachtet wird, wird der Kunde benachrichtigt und das Playbook entfernt.

## Freigeben von Playbooks über Sandboxes hinweg {#sharing-playbooks-sandboxes}

Wenn Ihre Organisation mehrere Sandboxes enthält, müssen Sie Playbooks nicht manuell über sie hinweg freigeben. Nachdem Sie ein Playbook in einer Sandbox erstellt und veröffentlicht haben, wird es für alle Sandboxes in dieser Organisation verfügbar. Sie können dann Instanzen dieses Playbooks in jeder der anderen Sandboxes erstellen.

Wenn das Playbook auf Felder verweist, die nicht im Vereinigungsschema der Ziel-Sandbox verfügbar sind oder denen die erforderlichen Berechtigungen fehlen, wird beim Erstellen der Instanz möglicherweise eine Fehlermeldung angezeigt. Diese Meldung ruft die fehlenden Felder und/oder fehlenden Berechtigungen auf.

Wenn im Vereinigungsschema Felder fehlen, werden diese beim Import in einem Dialogfeld hervorgehoben.

![Felder fehlen im Vereinigungsschema, das während des Importvorgangs aufgelistet wird](/help/use-case-playbooks/assets/playbooks/authoring/missing-fields.png)

## Freigeben von Playbooks in Organisationen {#sharing-playbooks-organizations}

Gehen Sie wie folgt vor, um ein Playbook von einer Organisation für eine andere freizugeben:

* **Bei der Quellorganisation anmelden**: Navigieren Sie zu der Organisation, die das von Ihnen erstellte Playbook enthält und über die Registerkarte &quot;**[!UICONTROL Playbooks“]** werden soll.
* **Playbook veröffentlichen**: Wenn das Playbook noch nicht veröffentlicht ist, müssen Sie es vor der Freigabe veröffentlichen.

>[!NOTE]
>
>Es muss eine Partnerschaft zwischen den Quell- und Zielorganisationen eingerichtet werden, um die Freigabe von Playbooks zu ermöglichen. Erfahren Sie, wie [eine Organisations-Partnerschaftsanfrage erstellen](https://experienceleague.adobe.com/en/docs/experience-platform/sandbox/ui/sharing-packages-across-orgs).

* **Freigabe initiieren**: Nachdem das Playbook veröffentlicht und eine Partnerschaft eingerichtet wurde, wählen Sie **[!UICONTROL Playbook freigeben]**.
* **Zielorganisation auswählen**: Wählen Sie die Organisation aus, für die Sie das Playbook freigeben möchten, wenn Sie dazu aufgefordert werden.
* **Bestätigen und freigeben**: Bestätigen Sie Ihre Auswahl. Sie erhalten Bestätigungsnachrichten, die eine erfolgreiche Freigabe anzeigen.
* **Zielorganisation überprüfen**: Melden Sie sich bei der Zielorganisation an, um sicherzustellen, dass das Playbook verfügbar ist.
* **Playbook importieren**: Wählen Sie **[!UICONTROL Importieren]**, um das Playbook in die Zielorganisation zu importieren. Sie können sie auf der Registerkarte **Playbooks** anzeigen.

Wenn das Playbook nicht angezeigt wird, stellen Sie sicher, dass es veröffentlicht ist und die Organisationspartnerschaft aktiv ist.

>[!IMPORTANT]
>
>Die transitive Playbook-Freigabe wird nicht unterstützt. Wenn Sie ein Playbook von einer Organisation für eine andere freigeben und dann importieren, kann es nicht erneut von der empfangenden Organisation für eine dritte Organisation freigegeben werden.

## Erforderliche Berechtigungen

Um auf die Sandbox zuzugreifen und diese Funktion zu verwenden, benötigen Sie die folgenden Berechtigungen:

* **Sandbox-**:

Diese sind erforderlich, um auf die Sandbox-Umgebung zuzugreifen, in der die Funktion vorhanden ist:

* **Verwalten einer Sandbox**
* **Sandbox anzeigen**

* **Berechtigungen zur Paketfreigabe**:

Diese Berechtigungen sind für die interne Freigabefunktion erforderlich:

* [**Paket verwalten**](/help/sandboxes/ui/sandbox-tooling.md)
* [**Paket freigeben**](/help/sandboxes/ui/sharing-packages-across-orgs.md)

Diese Berechtigungen ermöglichen Ihnen Folgendes:

* Sandbox-Umgebung aufrufen
* Zugriff auf die Funktion in der Sandbox
* Verwalten und Freigeben von Paketen nach Bedarf

Diese Berechtigungen befinden sich im Abschnitt **[!UICONTROL Sandboxes]** der Liste Berechtigungen .

![Die Liste der Berechtigungen mit den hervorgehobenen entsprechenden Berechtigungen.](/help/use-case-playbooks/assets/playbooks/authoring/permissions.png)

### Journey und zugehörige Objekte - Berechtigungen

Beim Erstellen von Journeys, die Playbooks verwenden, verweisen Sie wahrscheinlich auf andere Objekte wie **Kanäle**, **Zielgruppen** und andere Entitäten. Jede dieser Berechtigungen verfügt über einen eigenen Berechtigungssatz.

Dies sind die wichtigsten Berechtigungen für Journey-bezogene Aktionen, z. B.:

* **Journey anzeigen**
* **Journey verwalten**
* Berechtigungen in Bezug auf Objekte wie Zielgruppen und Kanäle

Sie benötigen außerdem die folgenden Zielgruppenberechtigungen:

* **Segment lesen**
* **Profil lesen**
* **Datensatz lesen**

Da Journey sehr flexibel sind und viele miteinander verbundene Objekte umfassen können, werden [vollständige Berechtigungen](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/access-control/privacy/high-low-permissions) separat dokumentiert und können je nach Anwendungsfall variieren.

## Nächste Schritte

Nachdem Sie nun wissen, wie Sie mit dem KI-Assistenten Playbooks erstellen, veröffentlichen und freigeben können, erfahren Sie, wie Sie mit den verfügbaren Playbooks beginnen und das richtige für Ihren Anwendungsfall aus der [Playbooks-Liste](/help/use-case-playbooks/playbooks/choose.md) auswählen.