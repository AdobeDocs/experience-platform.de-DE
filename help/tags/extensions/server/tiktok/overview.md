---
title: Integration der Adobe TikTok Web Events API-Erweiterung
description: Mit dieser Adobe Experience Platform-Web-Ereignis-API können Sie Website-Interaktionen direkt mit TikTok teilen.
last-substantial-update: 2023-09-26T00:00:00Z
exl-id: 14b8e498-8ed5-4330-b1fa-43fd1687c201
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 5%

---

# Übersicht über die [!DNL TikTok] Web Events API-Erweiterung

Die [!DNL TikTok]-Ereignis-API ist eine sichere [Edge Network-API](https://developer.adobe.com/data-collection-apis/docs/)-Schnittstelle, über die Sie Informationen direkt über Benutzeraktionen auf Ihren Websites mit [!DNL TikTok] teilen können. Sie können die Ereignisweiterleitungsregeln nutzen, um Daten vom [!DNL Adobe Experience Platform Edge Network] an [!DNL TikTok] zu senden, indem Sie die [!DNL TikTok] Web Events API-Erweiterung verwenden.

## Voraussetzungen für [!DNL TikTok] {#prerequisites}

Um die [!DNL TikTok]-Web-Ereignis-API für die Verwendung der [!DNL TikTok]-Ereignis-API zu konfigurieren, müssen Sie einen [!DNL TikTok] Pixel-Code und ein Zugriffstoken generieren.

Sie müssen über ein gültiges [!DNL TikTok] für ein Geschäftskonto verfügen, um mithilfe der Partnereinrichtung ein [!DNL TikTok] Pixel zu erstellen. Navigieren Sie zur [[!DNL TikTok] für die Geschäftsregistrierung](https://www.tiktok.com/business/en-US/solutions/business-account), um sich zu registrieren und ein Konto zu erstellen, falls Sie noch keines haben.

Sie müssen bei Ihrem Geschäftskonto angemeldet sein, um [!DNL TikTok] Pixel mithilfe der Partnereinrichtung einzurichten. Gehen Sie dazu wie folgt vor:

1. Navigieren Sie zur Registerkarte **[!UICONTROL Assets]** und wählen Sie **[!UICONTROL Event]** aus.
2. Wählen Sie unter Web-Ereignisse die Option **[!UICONTROL Manage]**.
3. Wählen Sie **[!UICONTROL Set Up Web Events]** aus.
4. Wählen Sie **[!UICONTROL Partner Setup]** als Verbindungsmethode aus.

Weitere Informationen [ Einrichten des ](https://ads.tiktok.com/help/article/get-started-pixel) Pixels finden Sie [!DNL TikTok] Handbuch „Erste Schritte mit Pixeln“.

Sie können ein Zugriffs-Token generieren, sobald das Pixel erfolgreich erstellt wurde. Navigieren Sie dazu zum Pixel und wählen Sie die Registerkarte **[!UICONTROL Settings]** aus. Wählen Sie unter Ereignis-API die Option **[!UICONTROL Generate Access Token]** aus.

Weitere Informationen [[!DNL TikTok]  Einrichten des Pixel-Codes ](https://business-api.tiktok.com/portal/docs?id=1739584855420929) Zugriffstokens finden Sie im Abschnitt Erste Schritte .

## Installieren und Konfigurieren der [!DNL TikTok] Web Events API-Erweiterung {#install}

Um die Erweiterung zu installieren, klicken Sie im linken Navigationsbereich auf **[!UICONTROL Extensions]** . Wählen Sie auf der Registerkarte **[!UICONTROL Catalog]** die **[!UICONTROL TikTok Web Events API Extension]** und dann **[!UICONTROL Install]** aus.

![Der Erweiterungskatalog mit der [!DNL TikTok] Erweiterungskarte, in der install hervorgehoben ist.](../../../images/extensions/server/tiktok/install-extension.png)

Geben Sie im nächsten Bildschirm die folgenden Konfigurationswerte ein, die Sie zuvor aus [!DNL TikTok] Ads Manager generiert haben:

* **[!UICONTROL Pixel Code]**
* **[!UICONTROL Access Token]**

Wenn Sie fertig sind, wählen Sie **[!UICONTROL Save]** aus.

![[!DNL TikTok] Konfigurationsbildschirm für die [!DNL TikTok] Web Events API-Erweiterung.](../../../images/extensions/server/tiktok/configure.png)

## Konfigurieren einer Ereignisweiterleitungsregel {#config-rule}

Nachdem alle Datenelemente eingerichtet wurden, können Sie mit der Erstellung von Ereignisweiterleitungsregeln beginnen, die bestimmen, wann und wie Ihre Ereignisse an [!DNL TikTok] gesendet werden.

Erstellen Sie eine neue [Regel](../../../ui/managing-resources/rules.md) in Ihrer Ereignisweiterleitungs-Eigenschaft. Fügen Sie unter **[!UICONTROL Actions]** eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL TikTok Web Events API Extension]** fest. Um Edge Network-Ereignisse an [!DNL TikTok] zu senden, setzen Sie den **[!UICONTROL Action Type]** auf **[!UICONTROL Send TikTok Web Events API Event].**

![Der [!UICONTROL Send TikTok Web Events API Event] Aktionstyp, der für eine [!DNL TikTok] in der Datenerfassungs-Benutzeroberfläche ausgewählt wird.](../../../images/extensions/server/tiktok/select-action.png)

Nach der Auswahl werden zusätzliche Steuerelemente angezeigt, um das Ereignis weiter zu konfigurieren, wie unten beschrieben. Klicken Sie nach Abschluss des Vorgangs auf **[!UICONTROL Keep Changes]** , um die Regel zu speichern.

**[!UICONTROL Web Events and Parameters]**

Web-Ereignisse und -Parameter enthalten allgemeine Informationen zum Ereignis. Standardereignisse werden in allen [!DNL TikTok] Integrationstools unterstützt und können für Berichte , die Optimierung von Konversionen und die Erstellung von Zielgruppen verwendet werden.

| Eingabe | Beschreibung |
| --- | --- |
| Ereignisname | Der Name des Ereignisses. Hierbei handelt es sich um Aktionen mit vordefinierten Namen, die von [!DNL TikTok] erstellt wurden und ein erforderliches Feld sind. Weitere Informationen zu unterstützten Ereignissen finden [[!DNL TikTok]  in der ](https://business-api.tiktok.com/portal/docs?id=1741601162187777) zur Marketing-API . |
| Ereigniszeit | Datum-Uhrzeit als Zeichenfolge in ISO 8601 oder im `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. Dies ist ein Pflichtfeld. |
| Ereignis-ID | Die eindeutige ID, die von Werbetreibenden generiert wird, um jedes Ereignis anzugeben. Dies ist ein optionales Feld, das für die Deduplizierung verwendet wird. |

{style="table-layout:auto"}

![Der [!DNL Web Events and Parameters] Abschnitt mit Beispieldaten, die in die Felder eingegeben werden.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL User Context Parameters]**

Benutzerkontextparameter enthalten Kundeninformationen, mit denen Web-Besucherereignisse mit [!DNL TikTok] Benutzern abgeglichen werden. Durch die Einbeziehung mehrerer Arten von übereinstimmenden Daten können Sie die Genauigkeit von Zielgruppenbestimmungs- und Optimierungsmodellen erhöhen.

| Eingabe | Beschreibung |
| --- | --- |
| IP-Adresse | Nicht gehashte öffentliche IP-Adresse des Browsers. Unterstützung wird für IPv4- und IPv6-Adressen bereitgestellt. Sowohl die vollständige als auch die komprimierte Form von IPv6-Adressen werden erkannt. |
| Benutzeragent | Der nicht gehashte Benutzeragent vom Gerät des Benutzers. |
| E-Mail | E-Mail-Adresse des Kontakts, der mit dem Konversionsereignis verknüpft ist. |
| Telefon | Die Telefonnummer muss vor dem Hashing im E164-Format `[+][country code][area code][local phone number]` sein. |
| Cookie-ID | Wenn Sie Pixel SDK verwenden, wird automatisch eine eindeutige Kennung im `_ttp` Cookie gespeichert, sofern Cookies aktiviert sind. Der `_ttp` kann extrahiert und für dieses Feld verwendet werden. |
| Externe ID | Jeder eindeutige Bezeichner wie Benutzer-IDs, externe Cookie-IDs usw. muss mit SHA256 gehasht werden. |
| TikTok-Klick-ID | Die `ttclid`, die der URL der Landingpage jedes Mal hinzugefügt wird, wenn eine Anzeige auf [!DNL TikTok] ausgewählt wird. |
| „Seiten-URL“ | Die Seiten-URL zum Zeitpunkt des Ereignisses. |
| Page Referrer URL | Die URL des Seiten-Referrers. |

{style="table-layout:auto"}

![Der [!DNL User Context Parameters] Abschnitt mit Beispieldaten, die in die Felder eingegeben werden.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL Properties Parameters]**

Verwenden Sie die Parameter „properties“, um zusätzliche unterstützte Eigenschaften zu konfigurieren.

| Eingabe | Beschreibung |
| --- | --- |
| Price | Die Kosten eines einzelnen Artikels. |
| Menge | Die Anzahl der Artikel, die im Ereignis gekauft werden. Dies muss eine positive Zahl größer als 0 sein. |
| Content-Typ | Der Objekteigenschaft content_type muss ein Wert von `product` oder `product_group` zugewiesen werden, je nachdem, wie Sie Ihren Daten-Feed konfigurieren, wenn Sie Ihren Produktkatalog einrichten. |
| Inhalts-ID | Eine eindeutige Kennung des Produktelements. |
| Inhaltskategorie | Kategorie der Seite/des Produkts. |
| Inhaltsname | Name der Seite/des Produkts. |
| Währung | Die Währung der Artikel, die im Ereignis gekauft werden. Dies wird in ISO-4217 ausgedrückt. |
| Wert | Der Gesamtpreis der Bestellung. Dieser Wert entspricht dem Preis * Menge. |
| Beschreibung | Eine Beschreibung des Elements oder der Seite. |
| Abfrage | Die Textzeichenfolge, die zum Suchen eines Produkts verwendet wurde. |
| Status | Der Status einer Bestellung, eines Artikels oder einer Dienstleistung. Beispiel: „eingereicht“. |

{style="table-layout:auto"}

![Der [!DNL Properties Parameters] Abschnitt mit Beispieldaten, die in die Felder eingegeben werden.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## Ereignis-Deduplizierung {#deduplication}

[!DNL TikTok] Pixel muss für die Deduplizierung eingerichtet werden, wenn Sie sowohl die [!DNL TikTok] Pixel SDK als auch die [!DNL TikTok] Web Events API-Erweiterung verwenden, um dieselben Ereignisse an [!DNL TikTok] zu senden.

Eine Deduplizierung ist nicht erforderlich, wenn unterschiedliche Ereignistypen vom Client und Server ohne Überschneidung gesendet werden. Um sicherzustellen, dass Ihr Reporting nicht negativ beeinflusst wird, müssen Sie sicherstellen, dass jedes einzelne Ereignis, das von der [!DNL TikTok]-Pixel-SDK und der [!DNL TikTok] Web Events API-Erweiterung freigegeben wird, dedupliziert wird.

Stellen Sie beim Senden von freigegebenen Ereignissen sicher, dass jedes Ereignis eine Pixel-ID, eine Ereignis-ID und einen Namen enthält. Duplizierte Ereignisse, die innerhalb von fünf Minuten aufeinander treffen, werden zusammengeführt. Wenn das Datenfeld im ersten Ereignis nicht vorhanden war, wird es mit dem nachfolgenden Ereignis kombiniert. Alle doppelten Ereignisse, die innerhalb von 48 Stunden empfangen wurden, werden entfernt.

Weitere Informationen zu diesem Prozess finden [!DNL TikTok] in der [-](https://ads.tiktok.com/help/article/event-deduplication) unter „Ereignisdeduplizierung“.

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie Sie Server-seitige Ereignisdaten mithilfe der [!DNL TikTok] Web Events API-Erweiterung an [!DNL TikTok] senden. Weitere Informationen zu den Funktionen der Ereignisweiterleitung in [!DNL Adobe Experience Platform] finden Sie unter [Übersicht über die Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
