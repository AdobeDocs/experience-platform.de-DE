---
title: Integration der Adobe TikTok Web Events API
description: Mit dieser Adobe Experience Platform-Web-Events-API können Sie Website-Interaktionen direkt mit TikTok teilen.
last-substantial-update: 2023-09-26T00:00:00Z
exl-id: 14b8e498-8ed5-4330-b1fa-43fd1687c201
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 4%

---

# Übersicht über die Web-Events-API-Erweiterung [!DNL TikTok]

Die API [!DNL TikTok] events ist eine sichere Benutzeroberfläche der [Edge Network-Server-API](/help/server-api/overview.md), über die Sie Informationen über Benutzeraktionen auf Ihren Websites direkt an [!DNL TikTok] weitergeben können. Sie können die Ereignisweiterleitungsregeln nutzen, um Daten von [!DNL Adobe Experience Platform Edge Network] an [!DNL TikTok] zu senden, indem Sie die [!DNL TikTok] Web Events API-Erweiterung verwenden.

## Voraussetzungen für [!DNL TikTok] {#prerequisites}

Um die [!DNL TikTok] Web-Events-API für die Verwendung der [!DNL TikTok]-Ereignis-API zu konfigurieren, müssen Sie einen [!DNL TikTok]-Pixelcode und ein Zugriffstoken generieren.

Sie müssen über einen gültigen [!DNL TikTok] -Wert für Ihr Geschäftskonto verfügen, um ein [!DNL TikTok]-Pixel mit der Partnereinrichtung zu erstellen. Rufen Sie die Seite [[!DNL TikTok] für die Registrierung von Unternehmen](https://www.tiktok.com/business/en-US/solutions/business-account) auf, um sich zu registrieren und ein Konto zu erstellen, falls noch keines vorhanden ist.

Sie müssen bei Ihrem Geschäftskonto angemeldet sein, um [!DNL TikTok] Pixel mithilfe der Partnereinrichtung einzurichten. Gehen Sie dazu wie folgt vor:

1. Navigieren Sie zur Registerkarte **[!UICONTROL Assets]** und wählen Sie **[!UICONTROL Ereignis]** aus.
2. Wählen Sie unter &quot;Web Events&quot;die Option **[!UICONTROL Verwalten]**.
3. Wählen Sie **[!UICONTROL Web-Ereignisse einrichten]**.
4. Wählen Sie **[!UICONTROL Partner-Setup]** als Verbindungsmethode aus.

Weitere Informationen zum Einrichten des [!DNL TikTok]-Pixels finden Sie im Handbuch [Erste Schritte mit Pixel](https://ads.tiktok.com/help/article/get-started-pixel) .

Sie können ein Zugriffstoken generieren, sobald das Pixel erfolgreich erstellt wurde. Navigieren Sie dazu zum Pixel und wählen Sie die Registerkarte **[!UICONTROL Einstellungen]** aus. Wählen Sie unter &quot;Events API&quot;die Option **[!UICONTROL Zugriffs-Token generieren]**.

Weitere Informationen zum Einrichten des Pixel-Codes und Zugriffs-Tokens finden Sie in der Anleitung [[!DNL TikTok] Erste Schritte](https://business-api.tiktok.com/portal/docs?id=1739584855420929) .

## Installieren und Konfigurieren der Web-Events-API-Erweiterung [!DNL TikTok] {#install}

Um die Erweiterung zu installieren, wählen Sie im linken Navigationsbereich **[!UICONTROL Erweiterungen]** aus. Wählen Sie auf der Registerkarte **[!UICONTROL Katalog]** die Erweiterung der TikTok-Web-Events-API ]**und dann**[!UICONTROL  Installieren ]**.**[!UICONTROL 

![Der Erweiterungskatalog, der die Installation der Erweiterungskarte [!DNL TikTok] hervorhebt.](../../../images/extensions/server/tiktok/install-extension.png)

Geben Sie im nächsten Bildschirm die folgenden Konfigurationswerte ein, die Sie zuvor über den Anzeigen-Manager von [!DNL TikTok] generiert haben:

* **[!UICONTROL Pixel-Code]**
* **[!UICONTROL Zugriffs-Token]**

Klicken Sie abschließend auf **[!UICONTROL Speichern]**.

![[!DNL TikTok] Konfigurationsbildschirm für die [!DNL TikTok] Web-Events-API-Erweiterung.](../../../images/extensions/server/tiktok/configure.png)

## Konfigurieren einer Ereignisweiterleitungsregel {#config-rule}

Sobald alle Ihre Datenelemente eingerichtet sind, können Sie mit der Erstellung von Ereignisweiterleitungsregeln beginnen, die bestimmen, wann und wie Ihre Ereignisse an [!DNL TikTok] gesendet werden.

Erstellen Sie eine neue [Regel](../../../ui/managing-resources/rules.md) in Ihrer Ereignisweiterleitungseigenschaft. Fügen Sie unter **[!UICONTROL Aktionen]** eine neue Aktion hinzu und legen Sie die Erweiterung auf **[!UICONTROL TikTok Web Events API Extension]** fest. Um Edge Network-Ereignisse an [!DNL TikTok] zu senden, setzen Sie den **[!UICONTROL Aktionstyp]** auf **[!UICONTROL TikTok Web Events API Event senden]**.

![Der Aktionstyp [!UICONTROL TikTok Web Events API Event senden] wurde für eine [!DNL TikTok] -Regel in der Datenerfassungs-Benutzeroberfläche ausgewählt.](../../../images/extensions/server/tiktok/select-action.png)

Nach der Auswahl scheinen zusätzliche Steuerelemente das Ereignis weiter zu konfigurieren, wie unten beschrieben. Wählen Sie nach dem Abschluss **[!UICONTROL Änderungen beibehalten]** aus, um die Regel zu speichern.

**[!UICONTROL Web-Ereignisse und -Parameter]**

Web-Ereignisse und -Parameter enthalten allgemeine Informationen zum Ereignis. Standardereignisse werden über die [!DNL TikTok] -Integrations-Tools hinweg unterstützt und können für die Berichterstellung , die Optimierung für Konversionen und die Erstellung von Zielgruppen verwendet werden.

| Eingabe | Beschreibung |
| --- | --- |
| Ereignisname | Der Name des Ereignisses. Hierbei handelt es sich um Aktionen mit vordefinierten Namen, die von [!DNL TikTok] erstellt werden und ein erforderliches Feld sind. Weitere Informationen zu unterstützten Ereignissen finden Sie in der Dokumentation zur [[!DNL TikTok] Marketing-API](https://business-api.tiktok.com/portal/docs?id=1741601162187777) . |
| Ereigniszeit | Datum/Uhrzeit als Zeichenfolge im ISO 8601- oder im `yyyy-MM-dd'T'HH:mm:ss:SSSZ`-Format. Dies ist ein erforderliches Feld. |
| Ereignis-ID | Die eindeutige ID, die von Advertisern zur Angabe jedes Ereignisses generiert wurde. Dies ist ein optionales Feld, das zur Deduplizierung verwendet wird. |

{style="table-layout:auto"}

![Der Abschnitt [!DNL Web Events and Parameters], der Beispieldaten in die Felder eingibt.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL Benutzerkontextparameter]**

Benutzerkontextparameter enthalten Kundeninformationen, mit denen Webbesucherereignisse mit [!DNL TikTok] Benutzern abgeglichen werden. Durch die Einbeziehung mehrerer Typen von übereinstimmenden Daten können Sie die Genauigkeit von Targeting- und Optimierungsmodellen erhöhen.

| Eingabe | Beschreibung |
| --- | --- |
| IP-Adresse | Öffentliche IP-Adresse des Browsers ohne Hash. IPv4- und IPv6-Adressen werden unterstützt. Sowohl die vollständige als auch die komprimierte Form von IPv6-Adressen werden erkannt. |
| Benutzeragent | Der Benutzeragent ohne Hash vom Gerät des Benutzers. |
| E-Mail | E-Mail-Adresse des Kontakts, der mit dem Konversionsereignis verbunden ist. |
| Telefon | Die Telefonnummer muss im E164-Format [+][Ländercode][Bereichscode][local phone number] vorliegen, bevor ein Hashing erfolgt. |
| Cookie-ID | Wenn Sie das Pixel SDK verwenden, wird automatisch eine eindeutige Kennung im `_ttp` -Cookie gespeichert, wenn Cookies aktiviert sind. Der Wert `_ttp` kann extrahiert und für dieses Feld verwendet werden. |
| Externe ID | Jede eindeutige Kennung wie Benutzer-IDs, externe Cookie-IDs usw. muss mit SHA256 gehasht werden. |
| TikTok-Klick-ID | Die `ttclid` , die der URL der Landingpage bei jeder Auswahl einer Anzeige auf [!DNL TikTok] hinzugefügt wird. |
| „Seiten-URL“ | Die Seiten-URL zum Zeitpunkt des Ereignisses. |
| Seiten-Referrer-URL | Die URL der verweisenden Seite. |

{style="table-layout:auto"}

![Der Abschnitt [!DNL User Context Parameters], der Beispieldaten in die Felder eingibt.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL Eigenschaftsparameter]**

Verwenden Sie die Eigenschaftenparameter, um zusätzliche unterstützte Eigenschaften zu konfigurieren.

| Eingabe | Beschreibung |
| --- | --- |
| Price | Die Kosten eines einzelnen Artikels. |
| Menge | Die Anzahl der Artikel, die im Ereignis gekauft werden. Hierbei muss es sich um eine positive Zahl größer als 0 handeln. |
| Content-Typ | Der Objekteigenschaft content_type muss entweder `product` oder `product_group` ein Wert zugewiesen werden, je nachdem, wie Sie Ihren Daten-Feed bei der Einrichtung Ihres Produktkatalogs konfigurieren. |
| Inhalts-ID | Eine eindeutige Kennung des Produktelements. |
| Inhaltskategorie | Kategorie der Seite/des Produkts. |
| Inhaltsname | Name der Seite/des Produkts. |
| Währung | Die Währung der Artikel, die im Ereignis gekauft werden. Dies wird in ISO-4217 ausgedrückt. |
| Wert | Der Gesamtpreis der Bestellung. Dieser Wert entspricht dem Preis * der Menge. |
| Beschreibung | Eine Beschreibung des Elements oder der Seite. |
| Abfrage | Die Textzeichenfolge, die zum Nachschlagen eines Produkts verwendet wurde. |
| Status | Der Status einer Bestellung, eines Artikels oder eines Dienstes. Beispiel: &quot;gesendet&quot;. |

{style="table-layout:auto"}

![Der Abschnitt [!DNL Properties Parameters], der Beispieldaten in die Felder eingibt.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## Ereignisdeduplizierung {#deduplication}

Das Pixel [!DNL TikTok] muss zur Deduplizierung eingerichtet werden, wenn Sie sowohl das [!DNL TikTok] Pixel SDK als auch die [!DNL TikTok] Web-Events-API-Erweiterung verwenden, um dieselben Ereignisse an [!DNL TikTok] zu senden.

Eine Deduplizierung ist nicht erforderlich, wenn vom Client und vom Server unterschiedliche Ereignistypen gesendet werden, die sich nicht überschneiden. Um sicherzustellen, dass Ihre Berichterstellung keine negativen Auswirkungen hat, müssen Sie sicherstellen, dass jedes einzelne Ereignis, das vom [!DNL TikTok] Pixel SDK und der [!DNL TikTok] Web-Events-API-Erweiterung freigegeben wird, dedupliziert wird.

Stellen Sie beim Senden freigegebener Ereignisse sicher, dass jedes Ereignis eine Pixel-ID, Ereignis-ID und einen Namen enthält. Duplizierte Ereignisse, die innerhalb von fünf Minuten aufeinander folgen, werden zusammengeführt. Wenn das Datenfeld beim ersten Ereignis fehlte, wird es mit dem nachfolgenden Ereignis kombiniert. Alle doppelten Ereignisse, die innerhalb von 48 Stunden empfangen wurden, werden entfernt.

Weitere Informationen zu diesem Prozess finden Sie in der Dokumentation zu [!DNL TikTok] unter [Ereignisdeduplizierung](https://ads.tiktok.com/help/article/event-deduplication) .

## Nächste Schritte

In diesem Handbuch wurde beschrieben, wie serverseitige Ereignisdaten mit der Web-Events-API-Erweiterung [!DNL TikTok] an [!DNL TikTok] gesendet werden. Weiterführende Informationen zu Ereignisweiterleitungsfunktionen in [!DNL Adobe Experience Platform] finden Sie in der Übersicht über die [Ereignisweiterleitung](../../../ui/event-forwarding/overview.md).
