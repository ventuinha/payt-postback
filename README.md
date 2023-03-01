# Guia do Postback PayT

Atualmente o PayT V1 possui os seguintes campos

| Campo           | Tipo                                               | Descrição                                                                                                                  |
|-----------------|----------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------|
| integration_key | string                                             | Sua chave de integração, serve para você poder validar se realmente o postback se origina do PayT                          |
| transaction_id  | string                                             | ID da Compra                                                                                                               |
| seller_id       | string                                             | Código do Tenant                                                                                                           |
| test            | bool                                               | Se o tenant está em modo de homologação ou não. Caso True, a compra não é real.                                            |
| type            | Enum(order, upsell, manual_upsell, abandoned-cart) | Se é um Order, Upsell ou Carrinho abandonado                                                                               |
| status          | [Status](#status)                                  | Status do Order, também indica a razão do Postback                                                                         |
| tangible        | bool                                               | Se o produto é físico ou não                                                                                               |
| was_lost        | bool                                               | Aparece quando o carrinho já passou pelo evento de carrinho abandonado. Pode ser usado para verificar se é uma recuperação |
| cart_id         | string                                             | ID do Carrinho                                                                                                             |
| shipping        | [Shipping](#shipping-object)                       | Informações sobre a entrega. Existe apenas quando o tangible é True.                                                       |
| customer        | [Customer](#customer-object)                       | Informações do comprador                                                                                                   |
| product         | [Product](#product-object)                         | Informações do Produto vendido                                                                                             |
| order_bumps     | [Array de OrderBumps](#orderbump-object)           |                                                                                                                            |
| link            | [Link](#link-object)                               | Informações do Checkout/Upsell que originou a compra                                                                       |
| transaction     | [Transaction](#transaction-object)                 | Informações da Transação                                                                                                   |
| commission      | [Array de Commissions](#commission-object)         | Informações sobre a comissão                                                                                               |
| started_at      | Date (Y-m-d H:i:s)                                 | Quando o carrinho foi criado. Formato Y-m-d H:i:s                                                                          |
| updated_at      | Date (Y-m-d H:i:s)                                 | Última atualização do Order. Formato Y-m-d H:i:s                                                                           |

## Status

Atualmente o postback possui alguns status para o acompanhamento do pedido no geral, são guiados pelo tipo de produto(
físico ou digital).

| status          | Nome                             | Descrição                                                       |
|-----------------|----------------------------------|-----------------------------------------------------------------|
| waiting_payment | Reservado - Aguardando Pagamento | O pedido foi reservado e está aguardando pagamento.             |
| paid            | Pago                             | Já está pago e em breve entrará em separação(caso físico)       |
| billed          | Faturado                         | Pedido foi pago e possui emissão da nota                        |
| separation      | Em separação                     | Pedido está sendo separado para ser coletado                    |
| collected       | Pedido Coletado                  | Pedido coletado e poderá ser rastreado dependendo do vendedor   |
| shipping        | Em Transporte                    | Pedido está em transporte                                       |
| shipped         | Entregue                         | Pedido foi entregue com sucesso                                 |
| cancelled       | Cancelado                        | O pedido foi cancelado por algum motivo como pagamento recusado |
| lost_cart       | Carrinho Perdido                 | Carrinho abandonado                                             | Cliente abandonou o carrinho. Baseado na média de tempo de checkout, é enviado em 7 minutos. |

---

## Shipping Object
| Campo         | Tipo                                          | Descrição                                                                          |
|---------------|-----------------------------------------------|------------------------------------------------------------------------------------|
| price         | integer                                       | Preço do Frete **em centavos**                                                     |
| status        | [Enum(Shipping Status)](#shipping-status)     | Status da entrega                                                                  |
| service       | string(atualmente apenas "custom" e "manual") | Serviço Utilizado                                                                  |
| tracking_code | string                                        | Código do Rastreio, **presente apenas quando inserido no sistema**                 |
| tracking_url  | string URL                                    | URL para acompanhamento da entrega, **presente apenas quando inserido no sistema** |
| address       | [JSON Address Object](#address-object)        | Endereço ao qual o produto será entregue                                           |

### Shipping Status

| Status              | Nome                                  |
|---------------------|---------------------------------------|
| waiting             | Aguardando postagem                   |
| invalid_code        | Código de Rastreio Inválido           |
| delivery_problem    | Problema na Entrega                   |
| overdue             | Em Atraso                             |
| wrong_address       | Endereço Errado do Destinatário       |
| waiting_client      | Objeto aguardando retirada do cliente |
| recipient_not_found | Destinatário não encontrado           |
| delivered           | Entrega Realizada                     |
| posted_object       | Objeto Postado	                       |
| forwarded           | Encaminhado                           |
| delivering          | Saiu para entrega                     |
| waiting_validation  | Aguardando Validação                  |
| returning           | Devolvendo ao Remetente               |
| returned            | Devolvido                             |
| shipping            | Em transporte                         |

### Address Object

```json
{
    "zipcode": "00000000",
    "street": "Rua",
    "street_number": "Numero da casa/ Logradouro",
    "complement": "Complemento",
    "district": "Bairro",
    "city": "Cidade",
    "state": "XX",
    "country": "BR"
}
```

---

## Customer Object

| Campo           | Tipo                                   | Descrição                                                                    |
|-----------------|----------------------------------------|------------------------------------------------------------------------------|
| name            | string                                 | Nome do Comprador                                                            |
| fake_email      | bool                                   | Se o comprador marcou 'Não tenho Email'. Caso true, desconsidere o Email     |
| email           | string                                 | Email do comprador                                                           |
| doc             | string                                 | CPF ou CNPJ do comprador, **apenas números**                                 |
| phone           | string                                 | Número de Telefone, **apenas números**                                       |
| billing_address | [JSON Address Object](#address-object) | Endereço de Cobrança, ausente em caso do checkout digital                    |
| origin          | [JSON Origin Object](#origin-object)   | Presente caso este comprador tenha sido originado de alguma campanha do PayT |
| code            | string                                 | Código do comprador dentro do APP.PAYT                                       |
| url             | string                                 | URL de edição/ações no cadastro do comprador                                 |

### Origin Object

| Campo        | Tipo        | Descrição                                                                                                                                                          |
|--------------|-------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| name         | string      | Nome da Campanha                                                                                                                                                   |
| code         | string      | Código identificador da campanha                                                                                                                                   |
| query_params | JSON Object | Presente apenas quando possui algum valor. Parâmetros GET que o comprador possuía quando engajou na campanha. Utilizado especialmente para conversões de NativeAds |

Exemplo

```json5
{
    "name": "Nome da Campanha",
    "code": "XXXXXX",  // identificador da campanha
    "query_params": {
        "click_id": "1032183891" // os valores aqui podem ser qualquer coisa
    }
}
```

---

## Product Object
| Campo    | Tipo                                       | Descrição                                                                                                 |
|----------|--------------------------------------------|-----------------------------------------------------------------------------------------------------------|
| name     | string                                     | Nome do Produto                                                                                           |
| price    | integer                                    | Preço **em centavos**                                                                                     |
| code     | string                                     | Código de Identificação no PayT                                                                           |
| sku      | string                                     | Código de Identificação do Tenant                                                                         |
| type     | Enum(physical, digital, grouped)           | Tipo de Produto caso grouped                                                                              |
| quantity | integer                                    | Quantidade comprada                                                                                       |
| items    | [Array de Product Object](#product-object) | Presente apenas quando o _type_ é grouped. **Um produto agrupado não pode conter outro produto agrupado** |

---

## OrderBump Object
| Campo   | Tipo                              | Descrição                         |
|---------|-----------------------------------|-----------------------------------|
| name    | string                            | Nome do OrderBump                 |
| code    | string                            | Código Identificador do OrderBump |
| product | [Product Object](#product-object) | Produto vendido no OrderBump      |

---

## Link Object
| Campo             | Tipo                                                                                     | Descrição                                                                                                   |
|-------------------|------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------|
| title             | string                                                                                   | Nome do Checkout/Upsell  |
| url               | string URL                                                                               | Url do Checkout/Upsell. Em caso de carrinho abandonado, a url conterá o _cart_id_ para recuperação          |
| admin_url         | string URL                                                                               | Presente em caso de Carrinho Abandonado. Url para visualização do carrinho dentro da plataforma             |
| available_coupons | [Array de Coupon Object](#coupon-object)                                                 | Presente em caso de Carrinho Abandonado. Lista de cupons que podem ser utilizados para recuperação da venda |
| sources           | Object(possíveis keys: src, utm_source, utm_medium, utm_content, utm_campaign, utm_term) | key->value de GET params relacionados ao utm quando o checkout estava aberto                                |
| query_params      | Object                                                                                   | Outros GET params que estavam presentes na url do checkout                                                  |
| seller_email      | string                                                                                   | Email do vendendor/usuário em casos de venda manual ou upsell manual

### Coupon Object
| Campo      | Tipo                     | Descrição                                          |
|------------|--------------------------|----------------------------------------------------|
| code       | string                   | Código para utilizar o cupom                       |
| method     | Enum(number, percentage) | Método para calcular o valor do cupom              |
| amount     | float                    | Valor do cupom, interage diretamente o _method_    |
| min_price  | float                    | Preço mínimo da compra para poder utilizar o cupom |
| expires_at | Date (Y-m-d H:i:s)       | Validade do cupom                                  |

---


## Transaction Object
| Campo          | Tipo                                                    | Descrição                                                                                   |
|----------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|
| payment_method | Enum(credit_card, boleto, pix)                          | Método de Pagamento                                                                         |
| payment_status | [Payment Status](#payment-status)                       | Status do Pagamento                                                                         |
| total_price    | integer                                                 | Valor total da transação **em centavos**                                                    |
| quantity       | integer                                                 | Quantidade                                                                                  |
| upsell_from    | string                                                  | Presente apenas em upsell/upsell_manual, se refere ao Order que originou o upsell           |
| modifiers      | [Array de Payment Modifiers](#payment-modifiers-object) | Modificadores do valor da transação, atualmente apenas cupons utilizados serão listados ali |
| paid_at        | Date (Y-m-d H:i:s)                                      | Data de quando o Pagamento foi efetuado. Presente apenas quando pago                        |
| created_at     | Date (Y-m-d H:i:s)                                      | Data de criação da Transação                                                                |
| updated_at     | Date (Y-m-d H:i:s)                                      | Data de atualização da Transação                                                            |

### Credit Card Fields
| Campo             | Tipo    | Descrição                                                                                 |
|-------------------|---------|-------------------------------------------------------------------------------------------|
| installments      | integer | Número de parcelas                                                                        |
| installment_price | integer | Valor de cada parcela                                                                     |
| error_message     | string  | Mensagem quando há erro na transação, refund ou chargeback. Presente apenas nestes casos. |

### Boleto Fields
| Campo         | Tipo               | Descrição                                       |
|---------------|--------------------|-------------------------------------------------|
| bankslip_url  | string URL         | URL que possui o PDF do boleto para o pagamento |
| bankslip_code | string             | Código do Boleto                                |
| expires_at    | Date (Y-m-d H:i:s) | Data de expiração do boleto                     |

### Pix Fields
| Campo      | Tipo               | Descrição                                                 |
|------------|--------------------|-----------------------------------------------------------|
| pix_url    | string URL         | URL com o QRCode para efetuar o pagamento do Pix          |
| pix_code   | string             | Código do Pix                                             |
| expires_at | Date (Y-m-d H:i:s) | Data de expiração do Pix(aqui deve se atentar ao horário) |


### Payment Status
| Status                         | Nome                            | Descrição                                                                   |
|--------------------------------|---------------------------------|-----------------------------------------------------------------------------|
| waiting_payment                | Aguardando Pagamento            | Aguardando Pagamento, disponível apenas em Pix e Boleto                     |
| paid                           | Pagamento Aprovado              | Pagamento aprovado pela gateway                                             |
| refused                        | Pagamento Recusado              | Pagametno recusado pega gateway                                             |
| one_click_buy_refused          | Upsell Recusado                 | Upsell Recusado pela gateway                                                |
| canceled                       | Pagamento Cancelado             | O Pagamento falhou por alguma razão                                         |
| reprocessed                    | Reprocessada                    | A compra foi reprocessada manualmente com antifraude desabilitado           |
| chargeback_presented           | Chargeback Apresentado          | O Chargeback do pagamento foi apresentado                                   |
| chargeback                     | Chargeback                      | O Pagamento levou um chargeback                                             |
| expired                        | Expirado                        | O Pix ou Boleto expirou                                                     |
| peding_refund                  | Reembolso Pendente              | O Pagamento está aguardando ser autorizado na plataforma para ser estornado |
| one_click_buy_refunded         | Upsell Estornado                | Upsell estornado                                                            |
| refunded                       | Pagamento Estornado             | Order foi estornado                                                         |
| one_click_buy_refunded_partial | Upsell Reembolsado (Parcial)    | O Upsell foi parcialmente estornado                                         |
| refunded_partial               | Pagamento Reembolsado (Parcial) | O Order foi parcialmente estornado                                          |

### Payment Modifiers Object
Atualmente o único modificador apresentado é o de Cupom

| Campo  | Tipo                    | Descrição                                                             |
|--------|-------------------------|-----------------------------------------------------------------------|
| name   | string                  | Nome do modificador. Em caso de Cupom, será o código do cupom aplicado |
| reason | Enum(coupon)            | Razão do modificador ter sido aplicado                                |
| method | Enum(fixed, percentage) | Método do modificador aplicado                                        |
| amount | float                   | Valor do modificador aplicado                                         |

---

## Commission Object
| Campo  | Tipo                                | Descrição                                       |
|--------|-------------------------------------|-------------------------------------------------|
| name   | string                              | Nome do comissionado                            |
| email  | string                              | Email do comissionado                           |
| type   | Enum(platform, producer, affiliate) | Tipo do comissionado                            |
| amount | integer                             | Valor **em centavos** que o comissionado recebe |

