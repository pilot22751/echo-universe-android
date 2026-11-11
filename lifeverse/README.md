# VIDAVERSO 2.0 — Simulador de vida original

Jogo Android offline, em português, sem anúncios, assinaturas ou compras internas. Código e identidade próprios; **não afiliado, não compatível nem derivado do aplicativo BitLife**. Nenhuma função paga de terceiros é desbloqueada ou distribuída.

## O que está incluído e jogável

- 172 profissões, em diversos setores, com requisitos por idade, formação e habilidades; promoção e projetos, mentoria, certificações, renda extra e currículo persistente.
- 214 eventos narrativos que oferecem escolhas, condições de elegibilidade e efeitos sobre atributos, dinheiro, relações e reputação.
- 25 sagas próprias com três capítulos (75 cenas), três decisões por capítulo e consequências que persistem de um ano a outro.
- 100 conquistas com condições verificáveis e pontos de legado; 29 países ficticiamente modelados, novos cursos, imóveis, veículos, hobbies e empresas.
- Economia simulada com inflação, desemprego, juros, fases de expansão e recessão; orçamento pessoal e evolução patrimonial por ano.
- Empresas com qualidade, marca, satisfação de equipe, inovação, marketing, pesquisa, preços, resultados anuais e gráficos.
- Familiares, amigos, filhos e cônjuges com traços pessoais, confiança, humor e lembranças de interações.
- Oito propósitos de vida que influenciam atributos iniciais e recompensam escolhas coerentes.
- Saúde, sono, atividade física, aprendizado, convivência, relacionamento, histórias, memória anual e diário pessoal.
- Sistemas anteriores preservados: nascimentos, envelhecimento, estudo, emprego, política fictícia, realeza, arte, esportes, crime fictício, negócios, propriedades, investimentos, aposentadoria, morte e dinastias.
- Salvamento automático local, até oito slots, backup JSON e importação de saves da versão 1.0.
- Tema claro/escuro, jogo offline e interface responsiva para Android.

## Construir APK

Requisitos: JDK 17, Android SDK 35 e Gradle 8.11.1.

```bash
node tests/smoke.js
gradle --no-daemon assembleDebug
```

APK: `app/build/outputs/apk/debug/app-debug.apk`.

No GitHub: `Actions → Compilar VIDAVERSO APK → Artifacts → VIDAVERSO-Android-APK`.

## Limitações importantes

- Uma aprovação de build ou testes de navegador **não substitui testes num aparelho físico**. APK gerado é debug e não uma versão lançada na Play Store.
- A economia e a política são **ficcionais**. Valores e probabilidades não são dados econômicos reais.
- Existem centenas de escolhas, mas não são todas as funcionalidades de simuladores comerciais; campanhas, política, profissões e outras áreas podem ganhar mais profundidade em futuras versões.
- O jogo armazena dados no próprio aplicativo. Reinstalar APKs de depuração assinados com chaves diferentes pode exigir remover a instalação anterior, o que apaga dados locais. **Exporte um backup antes de desinstalar**. Não há sincronização automática ou recuperação por conta.
- O programa não envia dados pessoais a servidores externos e não precisa de internet.

## Testes

`tests/smoke.js`: roteiro reproduzível que verifica a contagem de conteúdo, criação de personagem, interface das subáreas, saga de três capítulos, simulação econômica, negócios, relações e migração de dados antigos.

Na sessão de desenvolvimento, também foram executados testes de navegador com Playwright em viewport Android e desktop, incluindo simulações com mais de 40 anos e conclusão de saga.

## Licença

Veja `LICENSE`. O jogo é uma obra independente. Sem coleta de dados.