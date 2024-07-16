---
title: Stripe
description: Erfahren Sie, wie Sie Zahlungsdaten von Ihrem Stripe-Konto in Adobe Experience Platform erfassen.
badge: Beta
exl-id: 191d217e-036d-491a-b7dd-abcad74625ba
source-git-commit: 62bcaa532cdec68a2f4f62e5784c35b91b7d5743
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 9%

---

# [!DNL Stripe]

>[!NOTE]
>
>Die [!DNL Stripe]-Quelle befindet sich in der Beta-Phase. Weitere Informationen zur Verwendung von Beta-beschrifteten Quellen finden Sie in der [Quellenübersicht](../../home.md#terms-and-conditions) .

Tausende von Unternehmen aller Größenordnungen verwenden [!DNL Stripe] sowohl online als auch persönlich, um Zahlungen zu akzeptieren, neue Umsatzquellen zu erschließen und mithilfe von Adobe Experience Platform, Adobe Commerce und [!DNL Magento Open Source] global zu expandieren.

Verwenden Sie die [!DNL Stripe]-Quelle in Experience Platform, um Daten zu erfassen, die während des Kaufvorgangs von Ihren Kunden erfasst wurden. Verwenden Sie nach der Erfassung diese Daten, um personalisierte Angebote zu erstellen und umfassendere geschäftliche Einblicke zu gewinnen.

>[!TIP]
>
>Wenden Sie sich bei Fragen zur [!DNL Stripe] Quelle auf Experience Platform an [!DNL Stripe] unter adobe-Partnership<span>@stripe.com.

>[!BEGINSHADEBOX]

**Beispielanwendungsfall für die [!DNL Stripe] Quelle**

Ihr Unternehmen ermöglicht es Kunden, Artikel in Ihrem Onlineshop mit der Option **Jetzt kaufen** und **später bezahlen** (mit [!DNL Klarna], [!DNL Afterpay], [!DNL Affirm] oder [!DNL Zip]) zu erwerben.

Verwenden Sie die [!DNL Stripe] -Datenquelle, um die Verwendung der Optionen **Jetzt kaufen** und **später bezahlen** zu analysieren und mit personalisierten Angeboten für diese Kunden zu experimentieren. Erwägen Sie beispielsweise die Empfehlung von Zusatzartikeln, um die Anzahl der Artikel in ihrem Warenkorb vor dem Checkout zu erhöhen.

>[!ENDSHADEBOX]

Im folgenden Dokument erfahren Sie, wie Sie Ihr [!DNL Stripe] -Quellkonto einrichten, die erforderlichen Anmeldeinformationen abrufen und Ihre Schemas erstellen können.

## Voraussetzungen {#prerequisites}

In den folgenden Abschnitten finden Sie Informationen zur erforderlichen Einrichtung, die Sie vor dem Herstellen einer Verbindung Ihres [!DNL Stripe]-Kontos mit Experience Platform durchführen müssen.

### Zugriffstoken abrufen

* Melden Sie sich mit Ihrer [!DNL Stripe] E-Mail-Adresse und Ihrem Kennwort beim [[!DNL Stripe] Dashboard](https://dashboard.stripe.com/login) an.
* Wählen Sie im Dashboard [!DNL Developers] die Option **[!DNL API keys for developers]** aus.
* Wählen Sie auf der Registerkarte **API-Schlüssel** die Option **[!DNL Reveal test key]** aus, um Ihr Zugriffstoken anzuzeigen.
* Sie können dieses Token jetzt als Zugriffstoken verwenden, wenn Sie Ihr [!DNL Stripe]-Konto mit der Experience Platform verbinden, indem Sie entweder die [!DNL Flow Service] -API oder die Experience Platform-Benutzeroberfläche verwenden.

### Sammeln erforderlicher Anmeldeinformationen

Um Ihr [!DNL Stripe]-Konto mit Experience Platform zu verbinden, müssen Sie Werte für die folgenden Authentifizierungsberechtigungen angeben:

>[!BEGINTABS]

>[!TAB API]

Sie müssen beim Verbinden Ihres [!DNL Stripe]-Kontos mit der [!DNL Flow Service] -API die folgenden Anmeldedaten angeben.

| Anmeldedaten | Beschreibung |
| --- | --- |
| `accessToken` | Ihr [!DNL Stripe] OAuth 2-Authentifizierungstoken für Code aktualisieren. |
| `connectionSpec.id` | Die Verbindungsspezifikations-ID der [!DNL Stripe]-Quelle. Diese ID wird als `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3` festgelegt. |

>[!TAB UI]

Sie müssen die folgenden Anmeldedaten angeben, wenn Sie Ihr [!DNL Stripe]-Konto über die Experience Platform-Benutzeroberfläche verbinden.

| Anmeldedaten | Beschreibung |
| --- | --- |
| Zugriffs-Token | Ihr [!DNL Stripe] OAuth 2-Authentifizierungstoken für Code aktualisieren. |

>[!ENDTABS]

Weitere Informationen zur Verwendung von [!DNL Stripe] -APIs finden Sie in der [[!DNL Stripe] Dokumentation zu API-Schlüsseln](https://docs.stripe.com/keys).

### Erstellen eines Experience-Datenmodell (XDM)-Schemas

Die Quelle [!DNL Stripe] unterstützt die Aufnahme von Daten aus den folgenden Ressourcenpfaden:

* Gebühren
* Abonnements
* Erstattungen
* Bilanztransaktionen
* Kundinnen und Kunden
* Preise

Sie müssen ein XDM-Schema erstellen, um einen Datensatz zu beschreiben, in dem die von [!DNL Stripe] an Experience Platform gesendeten Felder und Datentypen gespeichert werden können.

>[!BEGINTABS]

>[!TAB Gebühren]

In [!DNL Stripe] stellen **charges** die Versuche dar, Geld in Ihre [!DNL Stripe] zu verschieben. Weitere Informationen zu bestimmten Ladungsattributen finden Sie im [[!DNL Stripe] API-Handbuch zu Gebühren](https://docs.stripe.com/api/charges) .

+++Auswählen zum Anzeigen des Stripe Charge-Objekts

```json
{
  "id": "ch_3MmlLrLkdIwHu7ix0snN0B15",
  "object": "charge",
  "amount": 1099,
  "amount_captured": 1099,
  "amount_refunded": 0,
  "application": null,
  "application_fee": null,
  "application_fee_amount": null,
  "balance_transaction": "txn_3MmlLrLkdIwHu7ix0uke3Ezy",
  "billing_details": {
    "address": {
      "city": null,
      "country": null,
      "line1": null,
      "line2": null,
      "postal_code": null,
      "state": null
    },
    "email": null,
    "name": null,
    "phone": null
  },
  "calculated_statement_descriptor": "Stripe",
  "captured": true,
  "created": 1679090539,
  "currency": "usd",
  "customer": null,
  "description": null,
  "disputed": false,
  "failure_balance_transaction": null,
  "failure_code": null,
  "failure_message": null,
  "fraud_details": {},
  "invoice": null,
  "livemode": false,
  "metadata": {},
  "on_behalf_of": null,
  "outcome": {
    "network_status": "approved_by_network",
    "reason": null,
    "risk_level": "normal",
    "risk_score": 32,
    "seller_message": "Payment complete.",
    "type": "authorized"
  },
  "paid": true,
  "payment_intent": null,
  "payment_method": "card_1MmlLrLkdIwHu7ixIJwEWSNR",
  "payment_method_details": {
    "card": {
      "brand": "visa",
      "checks": {
        "address_line1_check": null,
        "address_postal_code_check": null,
        "cvc_check": null
      },
      "country": "US",
      "exp_month": 3,
      "exp_year": 2024,
      "fingerprint": "mToisGZ01V71BCos",
      "funding": "credit",
      "installments": null,
      "last4": "4242",
      "mandate": null,
      "network": "visa",
      "three_d_secure": null,
      "wallet": null
    },
    "type": "card"
  },
  "receipt_email": null,
  "receipt_number": null,
  "receipt_url": "https://pay.stripe.com/receipts/payment/CAcaFwoVYWNjdF8xTTJKVGtMa2RJd0h1N2l4KOvG06AGMgZfBXyr1aw6LBa9vaaSRWU96d8qBwz9z2J_CObiV_H2-e8RezSK_sw0KISesp4czsOUlVKY",
  "refunded": false,
  "review": null,
  "shipping": null,
  "source_transfer": null,
  "statement_descriptor": null,
  "statement_descriptor_suffix": null,
  "status": "succeeded",
  "transfer_data": null,
  "transfer_group": null
}
```

+++

>[!TAB Abonnements]

In [!DNL Stripe] können Sie **Abonnements** verwenden, um einen Kunden wiederkehrend zu berechnen. Weitere Informationen zu bestimmten Abonnementattributen finden Sie im [[!DNL Stripe] API-Handbuch zu Abonnements](https://docs.stripe.com/api/subscriptions) .

+++Auswählen zum Anzeigen des Stripe-Abonnementobjekts

```json
{
  "id": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
  "object": "subscription",
  "application": null,
  "application_fee_percent": null,
  "automatic_tax": {
    "enabled": false,
    "liability": null
  },
  "billing_cycle_anchor": 1679609767,
  "billing_thresholds": null,
  "cancel_at": null,
  "cancel_at_period_end": false,
  "canceled_at": null,
  "cancellation_details": {
    "comment": null,
    "feedback": null,
    "reason": null
  },
  "collection_method": "charge_automatically",
  "created": 1679609767,
  "currency": "usd",
  "current_period_end": 1682288167,
  "current_period_start": 1679609767,
  "customer": "cus_Na6dX7aXxi11N4",
  "days_until_due": null,
  "default_payment_method": null,
  "default_source": null,
  "default_tax_rates": [],
  "description": null,
  "discount": null,
  "ended_at": null,
  "invoice_settings": {
    "issuer": {
      "type": "self"
    }
  },
  "items": {
    "object": "list",
    "data": [
      {
        "id": "si_Na6dzxczY5fwHx",
        "object": "subscription_item",
        "billing_thresholds": null,
        "created": 1679609768,
        "metadata": {},
        "plan": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "plan",
          "active": true,
          "aggregate_usage": null,
          "amount": 1000,
          "amount_decimal": "1000",
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "interval": "month",
          "interval_count": 1,
          "livemode": false,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "tiers_mode": null,
          "transform_usage": null,
          "trial_period_days": null,
          "usage_type": "licensed"
        },
        "price": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "price",
          "active": true,
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "custom_unit_amount": null,
          "livemode": false,
          "lookup_key": null,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "recurring": {
            "aggregate_usage": null,
            "interval": "month",
            "interval_count": 1,
            "trial_period_days": null,
            "usage_type": "licensed"
          },
          "tax_behavior": "unspecified",
          "tiers_mode": null,
          "transform_quantity": null,
          "type": "recurring",
          "unit_amount": 1000,
          "unit_amount_decimal": "1000"
        },
        "quantity": 1,
        "subscription": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
        "tax_rates": []
      }
    ],
    "has_more": false,
    "total_count": 1,
    "url": "/v1/subscription_items?subscription=sub_1MowQVLkdIwHu7ixeRlqHVzs"
  },
  "latest_invoice": "in_1MowQWLkdIwHu7ixuzkSPfKd",
  "livemode": false,
  "metadata": {},
  "next_pending_invoice_item_invoice": null,
  "on_behalf_of": null,
  "pause_collection": null,
  "payment_settings": {
    "payment_method_options": null,
    "payment_method_types": null,
    "save_default_payment_method": "off"
  },
  "pending_invoice_item_interval": null,
  "pending_setup_intent": null,
  "pending_update": null,
  "quantity": 1,
  "schedule": null,
  "start_date": 1679609767,
  "status": "active",
  "test_clock": null,
  "transfer_data": null,
  "trial_end": null,
  "trial_settings": {
    "end_behavior": {
      "missing_payment_method": "create_invoice"
    }
  },
  "trial_start": null
}
```

+++

>[!TAB Rückerstattungen]

In [!DNL Stripe] können Sie **erstattungen** verwenden, um eine zuvor erstellte Gebühr zurückzuerstatten. Weitere Informationen zu bestimmten Erstattungsattributen finden Sie im [[!DNL Stripe] API-Handbuch zu Erstattungen](https://docs.stripe.com/api/refunds) .

+++Auswählen zum Anzeigen des Stripe-Rückerstattungsobjekts

```json
{
  "id": "re_1Nispe2eZvKYlo2Cd31jOCgZ",
  "object": "refund",
  "amount": 1000,
  "balance_transaction": "txn_1Nispe2eZvKYlo2CYezqFhEx",
  "charge": "ch_1NirD82eZvKYlo2CIvbtLWuY",
  "created": 1692942318,
  "currency": "usd",
  "destination_details": {
    "card": {
      "reference": "123456789012",
      "reference_status": "available",
      "reference_type": "acquirer_reference_number",
      "type": "refund"
    },
    "type": "card"
  },
  "metadata": {},
  "payment_intent": "pi_1GszsK2eZvKYlo2CfhZyoZLp",
  "reason": null,
  "receipt_number": null,
  "source_transfer_reversal": null,
  "status": "succeeded",
  "transfer_reversal": null
}
```

+++

>[!TAB Bilanztransaktionen]

In [!DNL Stripe] stellen die **Bilanztransaktionen** die Bewegungen der Mittel zwischen Ihren [!DNL Stripe]-Konten dar. Weitere Informationen zu bestimmten Bilanztransaktionsattributen finden Sie im [[!DNL Stripe] API-Handbuch zu Bilanztransaktionen](https://docs.stripe.com/api/balance_transactions) .

+++Auswählen, um das Stripe Balance-Transaktionsobjekt anzuzeigen

```json
{
  "id": "txn_1MiN3gLkdIwHu7ixxapQrznl",
  "object": "balance_transaction",
  "amount": -400,
  "available_on": 1678043844,
  "created": 1678043844,
  "currency": "usd",
  "description": null,
  "exchange_rate": null,
  "fee": 0,
  "fee_details": [],
  "net": -400,
  "reporting_category": "transfer",
  "source": "tr_1MiN3gLkdIwHu7ixNCZvFdgA",
  "status": "available",
  "type": "transfer"
}
```

+++

>[!TAB Customers]

In [!DNL Stripe] stellen **Kunden** einen bestimmten Kunden Ihres Unternehmens dar. Weitere Informationen zu bestimmten Kundenattributen finden Sie im [[!DNL Stripe] API-Handbuch zu Kunden](https://docs.stripe.com/api/customers) , wo Sie weitere Informationen zu bestimmten Kundenattributen erhalten.

+++Auswählen zum Anzeigen des Stripe-Kundenobjekts

```json
{
  "id": "cus_NffrFeUfNV2Hib",
  "object": "customer",
  "address": null,
  "balance": 0,
  "created": 1680893993,
  "currency": null,
  "default_source": null,
  "delinquent": false,
  "description": null,
  "discount": null,
  "email": "jennyrosen@example.com",
  "invoice_prefix": "0759376C",
  "invoice_settings": {
    "custom_fields": null,
    "default_payment_method": null,
    "footer": null,
    "rendering_options": null
  },
  "livemode": false,
  "metadata": {},
  "name": "Jenny Rosen",
  "next_invoice_sequence": 1,
  "phone": null,
  "preferred_locales": [],
  "shipping": null,
  "tax_exempt": "none",
  "test_clock": null
}
```

+++

>[!TAB Preise]

In [!DNL Stripe] stellen die **preise** die Stückkosten, die Währung und den optionalen Abrechnungszyklus für den wiederkehrenden und einmaligen Kauf von Produkten dar. Weitere Informationen zu bestimmten Preisattributen finden Sie im [[!DNL Stripe] API-Handbuch zu Preisen](https://docs.stripe.com/api/prices) .

+++Auswählen zum Anzeigen des Stripe Price-Objekts

```json
{
  "id": "price_1MoBy5LkdIwHu7ixZhnattbh",
  "object": "price",
  "active": true,
  "billing_scheme": "per_unit",
  "created": 1679431181,
  "currency": "usd",
  "custom_unit_amount": null,
  "livemode": false,
  "lookup_key": null,
  "metadata": {},
  "nickname": null,
  "product": "prod_NZKdYqrwEYx6iK",
  "recurring": {
    "aggregate_usage": null,
    "interval": "month",
    "interval_count": 1,
    "trial_period_days": null,
    "usage_type": "licensed"
  },
  "tax_behavior": "unspecified",
  "tiers_mode": null,
  "transform_quantity": null,
  "type": "recurring",
  "unit_amount": 1000,
  "unit_amount_decimal": "1000"
}
```

+++

>[!ENDTABS]


### IP-Adressen-Zulassungsliste

Vor der Arbeit mit Quell-Connectoren muss einer Zulassungsliste eine Liste von IP-Adressen hinzugefügt werden. Wenn Sie Ihre regionsspezifischen IP-Adressen nicht zu Ihrer Zulassungsliste hinzufügen, kann dies bei der Verwendung von Quellen zu Fehlern oder Performance-Einbußen führen. Weitere Information finden Sie unter [IP-Adressen-Zulassungsliste](../../ip-address-allow-list.md).

### Berechtigungen auf Experience Platform konfigurieren

Sie müssen sowohl über die Berechtigung **[!UICONTROL Quellen anzeigen]** als auch über die Berechtigung **[!UICONTROL Quellen verwalten]** für Ihr Konto verfügen, um Ihr [!DNL Stripe]-Konto mit Experience Platform zu verbinden. Wenden Sie sich an Ihren Produktadministrator, um die erforderlichen Berechtigungen zu erhalten. Weitere Informationen finden Sie im Benutzerhandbuch zur Zugriffskontrolle [.](../../../access-control/ui/overview.md)

## Nächste Schritte

Nachdem Sie die erforderliche Einrichtung abgeschlossen haben, können Sie mit der Herstellung der Verbindung und Aufnahme Ihrer [!DNL Stripe]-Daten zu Experience Platform fortfahren. In den folgenden Handbüchern erfahren Sie, wie Sie mit APIs oder der Benutzeroberfläche [!DNL Stripe] Zahlungsdaten an Experience Platform erfassen:

* [Erfassen Sie Zahlungsdaten von Ihrem Stripe-Konto an Experience Platform mithilfe der Flow Service-API](../../tutorials/api/create/payments/stripe.md).
* [Erfassen Sie Zahlungsdaten von Ihrem Stripe-Konto an Experience Platform mithilfe der Benutzeroberfläche](../../tutorials/ui/create/payments/stripe.md).
