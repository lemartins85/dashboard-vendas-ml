# Painel de Vendas · Mercado Livre

Site estático (sem build) — só HTML/CSS/JS puro, feito para publicar direto no Cloudflare Pages.

## Arquivos
- `index.html` — o painel inteiro (layout, gráficos e lógica de cálculo).
- `data.json` — os dados que alimentam o painel. É o único arquivo que muda com frequência.

## Como os dados são atualizados
Sempre que um novo relatório de Vendas/Faturamento do Mercado Livre for processado, o conteúdo de `data.json` é substituído por uma nova versão com os números atualizados. Basta subir o novo `data.json` no repositório (substituindo o antigo) — o Cloudflare Pages republica o site sozinho em menos de um minuto.

## Estrutura do data.json
```json
{
  "atualizado_em": "2026-09-16",
  "meses": [
    {"mes": "2026-07", "faturamento": 18450.30, "pedidos": 210, "cancelamentos": 6, "devolucoes": 3}
  ],
  "itens": [
    {"sku": "ROL-6204", "nome": "Rolamento 6204 ZZ", "quantidade_vendida": 340, "faturamento": 6800.00, "custo_unitario": null}
  ]
}
```

A classificação ABC (80/20) e a sugestão de envio ao FULL são calculadas automaticamente no navegador a partir do faturamento de cada item — não é preciso calcular isso manualmente antes de gerar o arquivo.

## Custo por item / margem líquida
Ainda não conectado. O plano é ler os custos de uma tabela no Supabase (`custos_itens`) e cruzar com `data.json` para calcular a margem líquida real (descontando taxa do Mercado Livre e frete). Isso entra em uma próxima etapa.
