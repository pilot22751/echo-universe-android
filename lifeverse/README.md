# VIDAVERSO 3.0 — Simulador de vida original para Android

VIDAVERSO é um jogo independente, 100% offline e gratuito, com visual e conteúdo originais. Não possui compras internas nem anúncios, não é afiliado ao BitLife e não desbloqueia ou redistribui recursos de aplicativos de terceiros.

## O que mudou nesta versão

A versão **3.0 expande o projeto 2.0 existente**. O motor principal continua em JavaScript, a interface é empacotada por uma aplicação Android WebView nativa, e os slots e backups do projeto anterior são lidos com migração de dados. O jogo não foi reconstruído do zero.

- **Limites anuais persistentes:** uma mesma interação positiva com o mesmo NPC rende benefício somente uma vez por ano. Limites por ação, pessoa, emprego e projeto são mantidos no salvamento, inclusive ao fechar o aplicativo. Outras atividades exigem energia, dinheiro, idade e recursos.
- **Personagens persistentes:** familiares, amigos e filhos têm atributos e memórias; envelhecem, mudam de profissão, podem enfrentar perdas, casar, se afastar e morrer. A vida social produz efeitos atrasados, preservados no save.
- **Trabalho mais criterioso:** 291 títulos profissionais distintos no catálogo, com idade, salário, qualificação, experiência, habilidades, entrevistas limitadas, contratação probabilística, histórico de empresas, demissões, desempenho e promoções condicionadas a tempo e mérito. **A maior parte das ocupações compartilha o motor de carreiras setoriais:** 291 nomes não significam 291 campanhas profissionais exclusivas.
- **Educação:** 90 cursos/especialidades catalogados, necessidade de ensino básico, qualificações específicas para profissões reguladas, desempenho acadêmico e possibilidade de reprovação.
- **Economia e imóveis:** despesas por país, conservação, reparos e locações, vacância e inadimplência de imóveis; despesas de veículos; monitoramento do desempenho empresarial e dívidas corrigidas. Os valores econômicos são fictícios.
- **Saúde e animais:** 32 condições de saúde com evolução, gravidade, tratamento e recuperação não garantida; saúde, vínculo e custos para animais de estimação.
- **Eventos condicionais:** 49 eventos 3.0 originais com pré-requisitos e escolhas, incluindo consequências em anos futuros. A biblioteca combinada tem **263 eventos roteirizados**, além de 25 sagas preexistentes de 3 capítulos.
- **Carreiras especiais interativas adicionais:** oficinas de cinema, música, esporte, ciência, criadores, gastronomia e estúdio de jogos, com progressão, custos, contratos/projetos, resultados, limitações anuais e produção ao longo dos anos. **São sete módulos jogáveis, não sete simulações de carreira completas**.
- **123 conquistas verificáveis** no catálogo, 55 tipos de negócios, 34 propriedades e 29 países da base atual.
- **Auditoria dentro do jogo:** apresenta números realmente carregados e indica objetivos ainda incompletos.

## Onde encontrar

Abra o jogo e navegue para **Universo**. Selecione as novas subáreas **Motor 3.0**, **Emprego real**, **Formações**, **Vidas dos NPCs**, **Imóveis+**, **Saúde & pets**, **Especiais** e **Auditoria**. As demais abas do VIDAVERSO 2.0 continuam acessíveis.

## Testes

Na raiz do projeto Android:

```bash
node tests/smoke.js
node tests/v3-regression.js
for f in app/src/main/assets/*.js; do node --check "$f"; done
```

`v3-regression.js` mede o conteúdo real e verifica anti-farm por personagem/ano e após reiniciar; personagens mortos; diploma específico; contratação; promoção; evolução anual de NPCs; reforma de imóvel; tratamento; consequências e backup; migração de saves; carreiras especiais (protótipos, lançamentos, royalties); mais de 200 anos simulados em múltiplas vidas. Inclui verificações de dinheiro, dívidas, patrimônio e idades válidas. **Passar nos testes não garante ausência de todos os bugs.**

## Compilação Android

Requisitos: Java 17, Android SDK 35, Gradle 8.11.1.

```bash
gradle --no-daemon assembleDebug
```

APK: `app/build/outputs/apk/debug/app-debug.apk`.

No GitHub: **Actions → Compilar VIDAVERSO APK → Artifacts → VIDAVERSO-Android-APK**. A automação executa a regressão 2.0 e 3.0 antes de compilar o Android.

### Diagnóstico de execução no GitHub Actions

Se uma execução aparecer como **Queued** (na fila), isso não é um erro de compilação: o GitHub ainda não iniciou o job. Verifique em **Actions** se o repositório pode utilizar runners hospedados pelo GitHub e se não há bloqueios de plano, permissões ou cobrança. Uma nova execução por alteração da pasta `lifeverse/` pode ser solicitada sem modificar o código do jogo. Se o job iniciar, os testes automatizados são executados antes da compilação do APK.

## Limitações transparentes

O prompt de expansão define metas, não quantidade de funcionalidades já prontas. **Não estão completos**: 1.000 eventos realmente únicos, 100 países com legislações próprias, 60 doenças, 200 conquistas, 15 sistemas de carreira especial completos, 400 cargos de progressão distinta, políticas eleitorais detalhadas, tribunal, exército, imigração, geração procedural rica por país, todos os mecanismos financeiros e a mesma profundidade exclusiva em cada uma das 291 ocupações. Os módulos criados são funcionais nas regras que exibem, mas não substituem uma simulação integral de cada profissão ou área.

A simulação médica, judicial, econômica e política é fictícia; não serve como fonte de aconselhamento profissional. O APK debug depende da assinatura utilizada no build. **Antes de remover uma instalação antiga para instalar um APK com assinatura diferente, exporte o backup JSON; desinstalar apaga os dados locais.** A migração 1.0/2.0 foi testada no motor, mas uma instalação no celular ainda precisa de teste real.

## Próximos passos recomendados

Completar carreiras especiais individualmente, melhorar o sistema de cidades e imigração, aprofundar escola, saúde e justiça, adicionar mais eventos contextuais sem repetições artificiais, aperfeiçoar balanceamento da economia e realizar testes de aparelho físico.