---
solution: Experience Platform
title: Erfahren Sie, wie Sie mit dem KI-Assistenten Ihre eigenen Playbooks erstellen und freigeben können.
description: So erstellen Sie eigene Playbooks für Anwendungsfälle und geben diese frei.
role: User
exl-id: 0bc49710-ad9e-4509-b7e6-55f9b9037aa9
source-git-commit: aa1e155fb8d71497958d0de1f6c10cf47e58dbf0
workflow-type: tm+mt
source-wordcount: '1113'
ht-degree: 1%

---


# Erstellen und Freigeben eigener Playbooks (Beta)

Mit dem [!DNL Playbook Authoring Framework], der von AI Assistant in Adobe Experience Platform unterstützt wird, können Sie Playbooks in Adobe Experience Platform effizient erstellen, verwalten und freigeben.

Das Framework folgt einem dreistufigen Prozess:

1. **Metadatenerfassung**: Verwenden Sie den KI-Assistenten oder das [Webformular] um Playbook-Metadaten zu erfassen.

2. **Technische Verknüpfung**: Dem Playbook werden spezifische technische Assets wie Journey oder Zielgruppen hinzugefügt. Sie behalten die volle Kontrolle über den Prozess der Playbook-Erstellung in Ihrer Entwicklungs-Sandbox, um sicherzustellen, dass er mit Ihren Schemata und anderen eindeutigen Datenstrukturen übereinstimmt.

3. **Playbook-Verteilung**: Freigeben von Playbooks über verschiedene Organisationen hinweg. So kann beispielsweise das deutsche Martech Center of Excellence von ACME ein „goldenes“ Playbook erstellen und es an regionale Organisationen in Thailand, Australien usw. verteilen. um den Marketing-Anwendungsfall zu standardisieren.

## Playbook erstellen

Sie können ein Playbook auf zwei Arten erstellen: entweder mithilfe des KI-Assistenten oder manuell. In den folgenden Abschnitten erfahren Sie mehr darüber.

### Playbook - Übersicht

Führen Sie die folgenden Schritte aus, um ein Playbook mit dem KI-Assistenten zu erstellen:

Wählen Sie im linken Navigationsbereich die Option **[!UICONTROL Playbooks]**.

![ „Playbooks“ im linken Navigationsbereich der Benutzeroberfläche hervorgehoben.](/help/use-case-playbooks/assets/playbooks/authoring/playbooks.png)

Wählen Sie **[!UICONTROL Neues Playbook]** und dann **Playbook mit KI-Assistenten erstellen** aus.

![Die Playbook-Oberfläche mit der Auswahl „Playbook mit KI-Assistenten generieren“.](/help/use-case-playbooks/assets/playbooks/authoring/generate-playbook.png)

Beschreiben Sie im Feld Eingabeaufforderung den Anwendungsfall.

**Beispiel**: „Wenden Sie sich an ACME-Kunden, die Laufschuhe durchsucht, den Kauf jedoch nicht abgeschlossen haben.“

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

![Beispiel 1-Eingabeaufforderung](/help/use-case-playbooks/assets/playbooks/authoring/example-prompt.png)

**Beispiel 2:**

„Projektname: Fashion Newsletter
Hintergrund: (Proaktiv oder Problemlösung): Eine Journey, die dazu dient, Mode-Newsletter an ACME-Kunden zu senden, die sich für die Newsletter-Kommunikation angemeldet haben.
Ziel: Versand von Newsletter-E-Mails an Kunden von ACME, die sich für die Kommunikation angemeldet haben.
Werbedetails: Der Kunde erhält wöchentlich Modenachrichten im E-Mail-Kanal. Die E-Mail sollte personalisiert sein und Inhaltsvarianten basierend auf Geschlecht, Sprache und Markt aufweisen.
Projektkanäle/Touchpoints: E-Mail
Zielgruppe: Kunden, die sich für Newsletter-Nachrichten von ACME Fashion angemeldet haben.
Ziel-KPIs/Interaktionsmetriken/ROI: 1. Steigern Sie den Umsatz durch Produkte. 2. Fördern Sie die Kundentreue.“

![Beispiel 2-Eingabeaufforderung](/help/use-case-playbooks/assets/playbooks/authoring/example-2-prompt.png)

**Beispiel 3:**

„Ermutigen Sie Kunden, während einer laufenden Produktwerbekampagne Produkte zu kaufen.
Interagieren Sie mit Käufern während einer laufenden Promotion, indem Sie geeignete Kommunikation per E-Mail, SMS oder Push-Benachrichtigungen senden, um Produkte zu kaufen. Senden Sie ihnen nach 24 Stunden, in denen sie nicht an der Promotion teilnehmen, eine Erinnerungs-E-Mail.“

![Beispiel 3-Eingabeaufforderung](/help/use-case-playbooks/assets/playbooks/authoring/example-3-prompt.png)

**Beispiel 4:**

„Verkaufe Schuhe an High School-Spieler.“

![Beispiel 4-Eingabeaufforderung](/help/use-case-playbooks/assets/playbooks/authoring/example-4-prompt.png)

Der KI-Assistent entfernt alle unnötigen Details wie „Projektname“ oder „Hintergrund“. Es extrahiert die Schlüsselelemente wie „Zielgruppe“, „Kampagnenziel“ und „Marketing-Kanal“ und funktioniert mit jedem Eingabestil.

Diese Beispiele zeigen, wie KI wichtige Details aus Benutzeraufforderungen verfeinern und extrahieren kann.

>[!NOTE]
>
> Vermeiden Sie beim Schreiben Ihrer Eingabeaufforderungen personenbezogene Daten oder explizite Wörter.

## Inhaltsrichtlinien und Moderation

Achten Sie beim Erstellen von Playbooks auf die Sprache und die Inhalte, die Sie einbeziehen. Playbooks sind in Ihrer gesamten Organisation sichtbar, und Benutzer können beleidigende oder unangemessene Inhalte markieren.

### Kennzeichnungs- und Überprüfungsprozess

Wenn ein Playbook für unangemessene oder anstößige Inhalte markiert wird, wird es automatisch zur Überprüfung an Adobe gemeldet. Adobe überprüft dann den gekennzeichneten Inhalt, und wenn er als unangemessen betrachtet wird, wird der Kunde benachrichtigt und das Playbook entfernt.

## Nächste Schritte

Nachdem Sie nun wissen, wie Sie mit dem KI-Assistenten Playbooks erstellen und veröffentlichen, erfahren Sie, wie Sie mit den verfügbaren Playbooks beginnen und das richtige für Ihren Anwendungsfall aus der [Playbooks-Liste](/help/use-case-playbooks/playbooks/choose.md) auswählen.
