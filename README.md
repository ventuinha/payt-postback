Documentação de Postback PayT
-----------------------------

Por agora são apenas exemplos que se encontram na pasta do projeto.

  

### Status

Atualmente o postback possui alguns status para o acompanhamento do pedido no geral, são guiados pelo tipo de produto(físico ou digital).

| status | Nome | Descrição |
| --- | --- | --- |
| waiting\_payment | Reservado - Aguardando Pagamento | O pedido foi reservado e está aguardando pagamento. |
| paid | Pago | Já está pago e em breve entrará em separação(caso físico) |
| billed | Faturado | Pedido foi pago e possui emissão da nota |
| separation | Em separação | Pedido está sendo separado para ser coletado |
| collected\_order | Pedido Coletado | Pedido coletado e poderá ser rastreado dependendo do vendedor |
| shipping | Em Transporte | Pedido está em transporte |
| shipped | Entregue | Pedido foi entregue com sucesso |
| cancelled | Cancelado | O pedido foi cancelado por algum motivo como pagamento recusado |
| lost\_cart | Carrinho Perdido \| Carrinho abandonado | Cliente abandonou o carrinho. Baseado na média de tempo de checkout, é enviado em 7 minutos. |

  

### Fluxos de Atividade

é possível perceber um fluxo de atividade do cliente através do `cart_id`

resumidamente temos 4 fluxos nos exemplos, recomendo utilizar eles para ir em ordem cronológica

  

1.  Cartão de Crédito falha e sucesso
    1.  [Falha](https://github.com/ventuinha/payt-postback/blob/master/examples/cancelled.md)
    2.  [Sucesso](https://github.com/ventuinha/payt-postback/blob/master/examples/credit_card.md)
2.  [Boleto](https://github.com/ventuinha/payt-postback/blob/master/examples/bankslip.md)
3.  [Pix](https://github.com/ventuinha/payt-postback/blob/master/examples/pix.md)
4.  Compra com utm\_source e src + upsell
    1.  [Cartão de crédito com utm\_source](https://github.com/ventuinha/payt-postback/blob/master/examples/with_utm_sources.md)
    2.  [Upsell](https://github.com/ventuinha/payt-postback/blob/master/examples/upsell.md)
5.  Carrinho abandonado + compra recuperada + upsell manual
    1.  [Carrinho abandonado](https://github.com/ventuinha/payt-postback/blob/master/examples/lost_cart.md)
    2.  [Compra](https://github.com/ventuinha/payt-postback/blob/master/examples/cart_recovered.md)
    3.  [Upsell manual](https://github.com/ventuinha/payt-postback/blob/master/examples/manual_upsell.md)