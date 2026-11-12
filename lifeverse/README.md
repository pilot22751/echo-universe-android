# VIDAVERSO 4.0 — Imersão geográfica e cotidiana

Jogo independente e original de simulação de vida para Android. Offline, sem compras internas ou anúncios. Não é afiliado a BitLife nem altera outro aplicativo.

## O que foi efetivamente implementado

A versão 4.0 expande o mesmo motor e os mesmos saves da 3.0, em vez de recriar o jogo. A arquitetura é Android nativo com WebView offline e JavaScript de motor, conteúdos e interface.

- **68 países jogáveis** e **290 localidades** (nomes reais de cidades e alguns bairros, como Complexo do Alemão). Há ao menos 4 localidades na maioria dos países. Registros de migração, seleção de destino e encerramento de emprego/locação ao mudar.
- **Moedas por país** (BRL, USD, EUR, GBP, JPY etc.), exibidas em todas as quantias da interface: salário, saldo, patrimônio, anúncios, custos e apostas. Conversões da unidade interna para a moeda local são registradas ao imigrar. Os valores do motor continuam armazenados numa **unidade de referência BRL** para preservar os saves; a tabela cambial é fixa e **simulada**, não traz cotações financeiras reais. Salários de novos empregos e custos de vida são influenciados por país e localidade.
- **Mercado imobiliário geográfico:** 14 tipos de imóveis com 5 variantes por tipo em cada localidade, ou 70 ofertas por localidade; 490 ofertas geradas para o Brasil em 7 localidades. Os imóveis têm preços simulados determinísticos, área, conservação, aluguel potencial, compra com taxas e opção de financiamento com entrada, dívida e pagamentos periódicos. Os imóveis do jogador preservam localidade e histórico, com manutenção, vacância e venda com comissão e quitação do empréstimo. É possível **morar de aluguel**, com caução, cobrança anual, rescisão e dívida por atraso.
- **23 veículos/modelos** com nomes reais (ex.: Toyota Corolla, Honda Civic, Tesla Model 3, Jeep Compass), taxas, conservação e custos. Os preços são **inventados para o jogo**, não tabelas reais, ofertas de concessionárias ou publicidade.
- **Cassino fictício para maiores de 18 anos**: roleta europeia (37 casas), caça-níqueis e blackjack interativo com pedir carta/parar; saldo, lucro/prejuízo, histórico e limite persistente de 5 rodadas por ano. Usa somente dinheiro virtual do jogo.
- **Vida noturna e cinema:** seis opções de lazer com custos, limites anuais, chances de resultados diferentes, registros na linha do tempo, interação com amigos/companheiros e referências nominais a filmes existentes (ex.: *Megamente*, *A Viagem de Chihiro*) sem copiar cenas, arte ou roteiro.
- **Vida afetiva adulta:** escolha da orientação sexual, início de namoro compatível, encontros, flertes e intimidade consensual narrada de forma não explícita. Relações, confiança, personalidade e memórias afetam o resultado. O conteúdo íntimo exige personagens adultos.
- **Realeza realista:** nascer ou casar na realeza só se o país tiver uma monarquia; o Brasil e outras repúblicas não oferecem esse caminho. Sair de uma monarquia encerra o status real. Funções reais anteriores permanecem acessíveis nos países aptos.
- **27 ocupações locais**, incluindo mangaká e animador de anime no Japão, roteirista de Hollywood nos EUA, produtor de K-pop na Coreia do Sul, carnaval e música popular no Brasil. Empregos locais bloqueiam candidaturas fora do país. **14 formações ligadas à localidade** também exigem o país correspondente. Total integrado: **318 títulos profissionais** e **104 cursos**. Isso não significa 318 histórias profissionais exclusivas.
- **Eventos culturais por país** ligados ao tempo e à localidade, sem replicar integralmente falas/obras de terceiros.
- **Auditoria 4.0 no jogo** mostrando os números reais: países, cidades, ofertas, modelos, profissões locais e monarquias.

## Testes

```bash
node tests/smoke.js
node tests/v3-regression.js
node tests/v4-regression.js
for f in app/src/main/assets/*.js; do node --check "$f"; done
```

Foram executados: legado 2.0, regressão 3.0 e 4.0; proteção contra repetir atividades, compra financiada e venda, locação anual, imigração e moeda, profissões exclusivas, cassino, cinema, romance adulto e simulações de 225 anos em vários países. Testes não substituem execução num celular real.

## Compilação Android

No GitHub, acesse `Actions → Compilar VIDAVERSO APK`. Baixe o artefato `VIDAVERSO-Android-APK` e extraia `app-debug.apk`.

```bash
gradle --no-daemon assembleDebug
```

**Atenção:** antes de substituir o APK da 3.0, exporte um backup JSON dos seus saves. Builds de depuração podem ser assinados com chaves diferentes, exigindo desinstalação e apagando dados locais.

## Limitações honestas

Os preços imobiliários e dos veículos são fictícios; não representam anúncios ou avaliações. As taxas de câmbio usadas na simulação não são taxas de mercado. O patrimônio é representado internamente em unidades BRL de referência e convertido apenas para exibição, preservando coerência e compatibilidade. A jogabilidade ainda não possui políticas completas para todos os países, nem carreiras exclusivas e história individual para cada um dos 318 títulos. Eventos culturais regionais são um primeiro sistema de profundidade, não uma réplica das experiências reais de cada país. O cassino é ficcional, sem dinheiro real. A interface gráfica da 4.0 ainda precisa ser validada em um Android físico, pois o navegador de captura de tela não inicializou neste ambiente.

## Licença e direitos

Código e conteúdo originais. Referências a nomes de filmes, marcas de automóveis e localidades são usadas nominativamente para contextualização; não são redistribuídas imagens, códigos ou outros materiais protegidos desses aplicativos e obras.