# VIDAVERSO 5.0 — Simulador de Vida para Android

**Jogo independente, 100% offline, gratuito, sem compras reais nem anúncios obrigatórios.** Não é afiliado a BitLife e não redistribui recursos premium, arquivos, textos ou código de aplicativos de terceiros.

## Situação real da entrega

Esta é uma **expansão jogável e incremental da versão 4.0**; não representa a conclusão dos 400 requisitos. O documento original da especificação está em `docs/ESPECIFICACAO_400_REQUISITOS.md`. A auditoria conservadora item a item está disponível em `docs/COBERTURA_400.csv` e na aba **Universo → Auditoria 5.0** dentro do jogo.

**Resultado da matriz:** 400 itens; **27 implementados**, **260 parciais**, **113 pendentes**. A matriz não é certificação de completude; itens marcados como implementados indicam comportamentos verificáveis por testes de regressão, mas não garantem ausência de bugs em aparelhos físicos. A classificação foi conservadora e pode mudar conforme os testes.

## Recursos efetivamente acrescentados na versão 5.0

### Bancos e crédito
- Três instituições fictícias com tarifas, juros e requisitos diferentes.
- Conta corrente e poupança próprias, depósitos e saques entre carteira e banco que **não criam riqueza**.
- Rendimentos anuais de poupança, lançados no extrato.
- Empréstimos com taxas, parcelas, amortização, inadimplência, juros e pontuação de crédito.
- Cartão de crédito com limite, compras fictícias, pagamento de fatura, juros quando não quitada e impacto no score.
- Ativos e passivos novos passam a compor o patrimônio líquido; valores históricos das versões anteriores continuam em créditos de referência BRL.

### Passaporte, autorizações e viagens
- Passaporte com custos e vencimento.
- Solicitações de autorização migratória com avaliação probabilística de recursos e reputação; a solicitação tem tarifa e pode ser recusada.
- Viagens internacionais com custos, permissões fictícias e registro de destinos.
- Nova rota guiada de imigração que exige cidadania ou permissão; a função antiga de mudança livre foi preservada para compatibilidade técnica e modo legado.
- Naturalização fictícia após residência mínima. **Não representa exigências legais atuais.**

### Escola, carreira e relações
- Clubes escolares com idade mínima, custos, habilidades específicas e limite por ano.
- Exame de ingresso com nota condicionada por atributos e bolsa de estudo de 35% ou 65%, que reduz realmente o custo da próxima graduação compatível.
- Processos seletivos novos: busca por profissão, três estratégias de entrevista, avaliação de requisitos e contratação/rejeição com histórico, limite anual e salários regionalizados.
- Empréstimos pessoais a NPCs: dinheiro transferido vira recebível, NPC pode atrasar ou pagar com recursos próprios; registros afetam confiança e memória.
- Reuniões familiares com convidados e custos, recusas conforme personalidade e memórias persistentes.

### Empresas, justiça e carreira digital
- Linha adicional de produção nas empresas existentes, com compras de insumos, estoque, preço, vendas anuais, receita e histórico. A simulação é separada da receita base da empresa para não duplicar o mesmo faturamento.
- Processos civis e criminais **inteiramente fictícios**, com abertura, defesa jurídica custosa, audiências no ano seguinte, absolvição, condenação, multas ou pena. Não há instruções operacionais de crimes.
- Quatro canais fictícios de conteúdo (vídeo, lives, música e textos) com custos de criação, habilidades, duas publicações por canal ao ano, crescimento orgânico/viral condicionado, engajamento, desinteresse do público e patrocínios.
- Matriz completa dos 400 requisitos visível no jogo e em CSV, separando implementado/parcial/pendente.

## Compatibilidade com os saves 1.0–4.0

A estrutura `S.v5` é acrescentada de forma não destrutiva após `v4Init`; saves antigos são migrados ao abrir. As funções básicas da 2.0–4.0 continuam carregadas. Os valores de banco e empréstimos V5 são rastreados separadamente e agregados na função de patrimônio líquido.

**Faça sempre backup JSON dentro da versão anterior antes de instalar outra APK.** APKs debug do GitHub podem usar assinaturas diferentes, e desinstalar apaga dados locais. A migração foi testada no motor, mas não há garantia de compatibilidade de assinatura entre APKs debug.

## Testes

Na raiz do projeto:

```bash
node tests/smoke.js
node tests/v3-regression.js
node tests/v4-regression.js
node tests/v5-regression.js
for file in app/src/main/assets/*.js; do node --check "$file"; done
```

A regressão V5 verifica 400 IDs únicos na auditoria, preservação de patrimônio entre transferências, juros anuais sem duplicidade, empréstimos, cartão de crédito, passaporte, autorizações, migração, bolsas, entrevistas, limites sociais, empréstimos familiares, estoques e vendas, processos judiciais, canais e seguidores, persistência e 210 anos de simulações distribuídas em cinco países. As regressões 2.0/3.0/4.0 também passaram. A interface foi testada em Chromium em dimensões de celular, incluindo nove seções novas sem erros JavaScript. **Não substitui testes de APK em celulares físicos.**

## Estrutura técnica

- `app/src/main/assets/game.js`, `expansion.js`, `v3-*.js`, `v4-*.js` preservam os mecanismos anteriores.
- `v5-engine.js` contém a lógica de banco, escola, documentação, entrevistas, família e estoque.
- `v5-extras.js` contém processo judicial fictício e canais digitais.
- `v5-ui.js` e `v5-extras-ui.js` fornecem interfaces de ações reais.
- `v5-hooks.js` integra com salvamento, ano de vida, botões e patrimônio.
- `v5-coverage.js` contém o resumo do CSV para acesso offline.
- `tests/v5-regression.js` testa novas regras e compatibilidade.
- `docs/COBERTURA_400.csv` contém a matriz auditada dos requisitos.

## Como gerar o APK no GitHub

Acesse **Actions → Compilar VIDAVERSO APK → Artifacts → VIDAVERSO-Android-APK**. Dentro do ZIP estará `app-debug.apk`. Para compilar localmente requer Java 17, Android SDK 35 e Gradle 8.11.1:

```bash
gradle --no-daemon assembleDebug
```

## O que ainda está incompleto

Ainda **não** estão concluídos os 400 requisitos. Entre os pontos pendentes ou parciais mais importantes: grande diversidade de carreiras especiais exclusivas; processos judiciários e códigos legais por país; centenas de cursos com universidades reais e calendários nacionais; saúde pública e dezenas de tratamentos específicos; dezenas de modalidades esportivas com campeonatos; companhias com múltiplos produtos, sociedade, contabilidade e falência avançadas; herança empresarial e cadeia de gerações complexa; política e eleições nacionais completas; GPS/bairros e imóveis com licenças reais; imigração integral com cidadania por ascendência; minijogos extras e interações profundas de pets; acessibilidade e tradução integral; balanceamento econômico entre todos os países. A simulação não deve ser usada para decisões financeiras, médicas ou legais reais.

Consulte `docs/COBERTURA_400.csv` e `docs/PLANO_DE_CONTINUIDADE.md` para detalhes. A prioridade continua sendo corrigir estados incoerentes e aprofundar sistemas interligados antes de multiplicar catálogos sem consequências.