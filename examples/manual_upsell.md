Um Upsell Manual se trata de um caso onde o administrador após contatar o comprador e ter sua autorização, faz a compra utilizando a sessão ainda ativa do cartão.

Só troca de `upsell` para `manual_upsell` no campo type

```json
{
    "integration_key": "a74cf3440b21998dc78c8f35c72f124e",
    "cart_id": "R6VZW4",
    "started_at": "2020-07-10 13:42:11",
    "updated_at": "2020-07-10 13:45:24",
    "seller_id": "AR6D4X",
    "test": false,
    "status": "paid",
    "type": "manual_upsell",
    "tangible": true,
    "transaction_id": "LGEAN4",
    "shipping": {
        "price": 0,
        "status": "waiting_code",
        "service": "custom",
        "address": {
            "zipcode": "06763060",
            "street": "Rua Francisco Andugar Espinosa",
            "street_number": "999",
            "complement": "",
            "district": "Chácara Agrindus",
            "city": "Taboão da Serra",
            "estate": "SP",
            "country": "BR"
        }
    },
    "customer": {
        "name": "Solaire of Astora",
        "fake_email": false,
        "email": "test@payt.com",
        "doc": "67415765095",
        "phone": "+551199999999",
        "billing_address": {
            "zipcode": "06763060",
            "street": "Rua Francisco Andugar Espinosa",
            "street_number": "999",
            "complement": "",
            "district": "Chácara Agrindus",
            "city": "Taboão da Serra",
            "estate": "SP",
            "country": "BR"
        }
    },
    "product": {
        "code": "BLJOOR",
        "sku": "1002",
        "type": "physical",
        "name": "Never Deal With a Dragon: Secrets of Power #1",
        "quantity": 1,
        "price": 3999
    },
    "link": {
        "title": "Aproveite Também - Never Deal With a Dragon: Secrets of Power",
        "url": "https://checkout.payt.com.br/d82c8d1619ad8176d665453cfb2e55f0",
        "sources": []
    },
    "transaction": {
        "created_at": "2020-07-10 13:45:24",
        "updated_at": "2020-07-10 13:45:24",
        "payment_method": "credit_card",
        "payment_status": "paid",
        "total_price": 4815,
        "quantity": 1,
        "modifiers": [],
        "upsell_from": "R269DL",
        "installments": 9,
        "installment_price": 535,
        "paid_at": "2020-07-10 13:45:24"
    }
}
```
