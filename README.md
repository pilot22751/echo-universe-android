# ECHO UNIVERSE 3.0 — ECHO LIFE (Letterboxd, Steam e YouTube)

Versão 3.0 do aplicativo Android. Mantém as estatísticas, missões, quizzes, coleções, diário, Spotify e histórico importado da 2.0 e adiciona três áreas de fontes externas.

## Conexões implementadas

### 🎬 Letterboxd
1. Abra **ECHO LIFE → Letterboxd** e salve seu nome de usuário.
2. Toque **Sincronizar RSS** para carregar os registros recentes do seu feed público (`https://letterboxd.com/usuario/rss/`). Não é necessário senha ou chave.
3. Para histórico antigo, no Letterboxd (site em desktop) vá em **Settings → Data → Export** e baixe o ZIP.
4. No Android, toque **Importar ZIP / CSV** para trazer as entradas de `diary.csv`, `watched.csv`, `ratings.csv` e `watchlist.csv` (quando presentes no arquivo); aceita também um CSV individual.
5. Veja filmes, avaliações, watchlist, pesquisa e nota média. O RSS mostra apenas as atividades recentes, não todo o acervo.

### 🎮 Steam
1. Localize seu **SteamID64** (17 dígitos). Em geral: endereço do perfil público `steamcommunity.com/profiles/7656...`.
2. Solicite sua **Steam Web API Key** em `https://steamcommunity.com/dev/apikey`, caso sua conta seja elegível.
3. Abra **ECHO LIFE → Steam**, informe SteamID64 e Key, salve e toque **Atualizar Steam**.
4. Biblioteca visível, horas acumuladas, jogos recentes, ranking por tempo jogado, filtros e atalhos.

A Steam só devolve jogos expostos pelas configurações de privacidade da sua biblioteca. A API não retorna um diário completo de sessões por dia.

### ▶ YouTube
1. Entre em **Google Cloud Console**, crie um projeto e habilite a **YouTube Data API v3**.
2. Gere uma **API Key** para requisições de leitura de dados públicos e aplique as restrições de chave adequadas, se possível.
3. Abra **ECHO LIFE → YouTube**, informe o ID do seu canal (`UC...`) ou `@handle` e a chave, salve e toque **Atualizar YouTube**.
4. O ECHO lista playlists públicas, contagens e vídeos de até quatro playlists públicas. Oferece busca e atalhos para abrir as listas e vídeos no YouTube.

**Privacidade e limites do YouTube:** esta versão não acessa playlists privadas, histórico de vídeos assistidos, minutos vistos nem vídeos curtidos privados. Esses dados exigem OAuth Google com permissões adicionais e configuração específica de credenciais Android, que ainda não foi implementado. Não considere esse recurso uma conexão com o histórico privado da conta Google.

## Segurança e privacidade
- Cada fonte é opcional e possui **Desconectar** para apagar seus dados e credenciais locais.
- A Steam Key e YouTube API Key são cifradas com AES-GCM e chave em `AndroidKeyStore` antes de salvar nas preferências privadas do Android. Não aparecem nos arquivos do repositório ou no HTML.
- A senha dos serviços nunca é solicitada pelo ECHO.
- Histórico importado e dados consultados são gravados em arquivos privados do próprio app. Não há servidor próprio ECHO nem transferência entre usuários.
- Os dados são lidos por HTTPS, com limites de tamanho, e o XML RSS bloqueia entidades externas.
- Dependências: Android SDK padrão (sem bibliotecas de terceiros em tempo de execução).

## Compilação e instalação
1. No GitHub, abra `Actions → Gerar APK do ECHO → Run workflow`.
2. Na execução concluída com sucesso, baixe o artefato `ECHO-Android-APK`.
3. Extraia o `app-debug.apk` e instale em Android 8.0 ou superior.
4. Este é um APK **debug**, não uma versão publicada na Play Store. É preciso teste real em um celular.

**Importante sobre atualizações:** o GitHub Actions usa um certificado de depuração gerado pelo executor. Se você já instalou o APK 2.0 compilado por outro executor, o Android pode recusar a instalação da 3.0 por assinatura diferente. Faça backup/exportação de tudo que puder (inclusive notas do diário) antes de desinstalar a versão anterior; ao desinstalar, os dados locais do ECHO são apagados. A instalação precisa de uma estratégia de assinatura estável para upgrades futuros.

## Por que há arquivos `.tar.xz` no repositório?
O GitHub Actions extrai `source/echo-universe-source.tar.xz` na raiz antes da compilação. É o código completo em Java 17 com Android WebView. A pasta `app/src/main/assets/` contém as telas HTML, CSS e JavaScript; a pasta `app/src/main/java/com/echomusic/stats/` contém a integração nativa.

ECHO é independente do Spotify, Letterboxd, Steam/Valve e Google/YouTube. Os dados continuam sob os termos de cada serviço.

---

## Recursos da versão 2.0 preservados

Projeto Android nativo (Java 17 + Android WebView) com interface offline em HTML/CSS/JS,
conexão oficial com Spotify (OAuth 2.0 Authorization Code + PKCE), banco SQLite e
importação do histórico real do Spotify em JSON ou ZIP.

**Status:** expansão interativa v2.0 implementada e testada em navegador desktop e móvel, incluindo navegação, quiz, batalha ELO, memória, bingo, favorito, mix, diário e histórico de exemplo. A versão 2.0 foi compilada via GitHub Actions. A versão 3.0 exige sua própria compilação e validação.

## Novidades da versão 2 — ECHO Universe

Esta versão adiciona **9 áreas interativas** à experiência original:

1. **Universo ECHO (hub)**: 8 portais, painel de nível, XP, estatísticas rápidas e pontos de entrada para as experiências.
2. **Laboratório**: 24 indicadores de escuta, gráficos por horário e dia da semana, plataformas e meses, relatórios compartilháveis e temporizador de foco independente.
3. **Meu acervo**: pesquisa por músicas/artistas/álbuns, filtros e ordenação, favoritos, sorteio de músicas e descoberta de pérolas do ranking.
4. **Arcade musical**: 6 quizzes gerados a partir dos dados do usuário (quem canta, maiores favoritos, artistas, hora, mês e verdadeiro/mito); batalha ELO para comparar músicas, memória de faixas e artistas, bingo 5×5 e roleta musical.
5. **Missões e conquistas**: 12 missões que se renovam pela data local, 52 medalhas por progresso e atividades, XP/níveis e metas personalizadas.
6. **Coleção**: favoritos salvos manualmente, estante pessoal e biblioteca de mixes.
7. **Mix Lab**: gerador por temas, mix aleatório, top, pérolas, favoritos e lembranças mensais. O modo por horário funciona **somente na prévia do navegador com eventos históricos detalhados**. Edição da ordem e remoção de faixas; compartilhamento da lista.
8. **Diário musical**: adicionar memórias, escolher humor manualmente, associar uma música, tags, filtros, exclusão e exportação em JSON no navegador.
9. **Cápsulas do tempo**: escolher mês/ano, reprodução e minutos registrados, favorita do mês (quando identificada), dia marcante, comparação entre meses e compartilhamento.

As atividades funcionam offline após abrir o app. O progresso das novas atividades
fica em armazenamento local do WebView/navegador. Não há backend nem rede social.

**Limites intencionais:** quizzes e rankings usam somente faixas/artistas conhecidos;
alguns desafios exigem diversidade mínima no histórico. O modo bingo e as missões
não afirmam verificar o que você ouviu fora do ECHO. Misturas são **listas pessoais**,
não criam playlists no Spotify nem reproduzem música dentro do ECHO.

**Para experimentar:** abra `ECHO_UNIVERSE_PREVIA.html` no navegador ou entre no
app e toque **Universo ECHO**. A prévia começa com dados fictícios identificados.
Com histórico JSON real, substitui os dados da demonstração pelas suas escutas.
A prévia aceita JSON; a importação de ZIP é suportada **no Android**.

## Recursos originais que continuam na versão 2

- Login seguro com sua própria conta Spotify via API oficial, sem informar senha ao ECHO.
- Top 50 músicas e artistas do Spotify para 4 semanas, 6 meses e 12 meses (afinidade,
  **não** número de plays).
- Últimas reproduções disponíveis pela API e faixa tocando agora (quando disponível).
- Recontagem de reproduções por faixa, artista, álbum, dia, hora e mês, a partir do histórico.
- Minutos reais de escuta a partir de `msPlayed` / `ms_played` nos arquivos exportados.
- Rankings por minutos e número de reproduções, gráficos horários, mapa de calor 7×24,
  dias mais musicais, recordes de sequência, evolução mensal, retrospectiva anual.
- Curiosidades: coruja musical, fã de carteirinha, música mais repetida, dia favorito,
  sequência de escuta e outras.
- Gêneros musicais **quando** o Spotify devolver esse campo (pode estar ausente/depreciado).
- Importação de `StreamingHistory*.json`, `endsong_*.json`,
  `Streaming_History_Audio_*.json` e ZIP do Spotify.
- Importações repetidas são deduplicadas por data, música, artista e origem.
- Dados locais SQLite, exportação CSV, apagar histórico e desconectar a conta.
- Prévia em navegador com dados fictícios marcados como demonstração. No navegador
  também é possível carregar arquivos JSON, sem acesso direto à API Spotify.

## Como gerar o APK (opção 1: GitHub Actions)

1. Descompacte o `ECHO_UNIVERSE_ANDROID.zip` e envie **o conteúdo da pasta** (incluindo `.github`)
   a um repositório GitHub.
2. Abra a aba **Actions** do repositório → **Gerar APK do ECHO** → **Run workflow**.
3. Ao terminar, na execução em **Artifacts**, baixe `ECHO-Android-APK`.
4. Descompacte o artefato; o arquivo `app-debug.apk` é o instalador Android.
5. Transfira o APK para seu Android e permita a instalação de apps dessa origem,
   se o sistema solicitar.

Para compartilhar o app com outras pessoas além das permitidas pelo modo de desenvolvimento
seria necessário adequar o projeto aos termos e ao processo de aprovação do Spotify.

## Como gerar o APK (opção 2: Android Studio)

1. Instale o [Android Studio](https://developer.android.com/studio), com SDK Android 35,
   JDK 17 e Gradle 8.11.1 (ou deixe o Studio configurar as versões necessárias).
2. Abra a pasta `ECHO_Android` no Android Studio e aguarde a sincronização do projeto.
3. Caso o Android Studio peça o Gradle, configure a versão 8.11.1.
4. Clique **Build → Build Bundle(s) / APK(s) → Build APK(s)**.
5. O arquivo estará em `app/build/outputs/apk/debug/app-debug.apk`.

O projeto usa somente o Android SDK padrão, sem SDKs de terceiros em tempo de execução.
A integração Spotify é opcional para explorar os jogos com dados históricos importados.

## Conectar com o Spotify

**IMPORTANTE (regras atuais de 2026):** apps em modo Development exigem que o
proprietário da aplicação tenha **Spotify Premium**, e a lista de usuários permitidos é
limitada a **cinco contas**. Essas são condições da plataforma Spotify, não do ECHO.

1. Entre em <https://developer.spotify.com/dashboard> com uma conta Premium.
2. Crie um app, escolha **Web API**, obtenha o **Client ID** (32 caracteres).
3. Nas configurações desse app, adicione exatamente esta Redirect URI:

   `echomusicapp://auth/callback`

4. Salve as configurações. Se for acessar de uma conta diferente da conta dona do app,
   adicione-a à lista de usuários permitidos no dashboard do Spotify.
5. Instale e abra o ECHO → **Ajustes & conexão**, cole o Client ID e toque **Conectar**.
6. Autorize os escopos solicitados diretamente no site do Spotify, após o redirecionamento.
7. Toque **Atualizar dados** se quiser fazer uma nova sincronização manual.
   O app também consulta os dados novamente ao abrir se a sincronização anterior tiver
   mais de 30 minutos.

**Escopos solicitados:** `user-top-read`, `user-read-recently-played`,
`user-read-currently-playing`, `user-read-private`.

O OAuth usa PKCE/SHA-256 com verificador aleatório e validação do parâmetro `state`.
Não existe `client_secret` embutido no aplicativo.

## Como mostrar os minutos reais

A API Web do Spotify **não** fornece os minutos efetivamente escutados ou a quantidade
exata de vezes que cada música tocou ao longo de toda a sua conta.
O endpoint de reprodução recente retorna no máximo 50 itens por pedido e cobre apenas
parte do histórico acessível. O aplicativo não finge que a duração total da faixa é
igual ao tempo ouvido.

1. Solicite o **histórico estendido de escuta** nas configurações de privacidade da
   sua conta Spotify: <https://www.spotify.com/account/privacy/>.
2. Quando o Spotify disponibilizar o arquivo, baixe o ZIP com o histórico.
3. No ECHO, acesse **Ajustes & conexão** → **Importar histórico JSON / ZIP**.
4. Selecione o ZIP ou múltiplos JSON e aguarde a conclusão.
5. As estatísticas por minutos aparecerão usando o campo `ms_played` (histórico
   estendido) ou `msPlayed` (histórico básico).

Os minutos são definidos como a soma dos milissegundos que o arquivo registra.
O app considera 30 segundos de escuta como limiar de uma reprodução contada
no ranking histórico; intervalos menores ainda contribuem para os minutos.
Os dados da API com duração desconhecida são identificados separadamente.

## Limitações intencionais

- **Tunesimo:** não há integração no projeto porque não há API pública e permissão
  verificadas para ler o histórico desse serviço; não utiliza scraping nem credenciais.
- **Gêneros:** o campo `genres` de artistas pode estar ausente nos novos apps da API
  Spotify. Se vier, as barras refletem um índice relativo da lista de artistas, não
  percentual exato de tempo de escuta em um gênero.
- **Minutos / sessões em tempo real:** não são fornecidos diretamente pela Web API.
- **Sincronização:** atualiza em abertura do app (se cache tiver >30 min) ou quando
  tocado Atualizar; não fica rodando continuamente em background.
- **Histórico exportado:** fica no dispositivo. Importação não manda o arquivo para
  servidores do ECHO. Cuidado ao compartilhar o CSV que contém informações pessoais.
- **Privacidade:** credenciais OAuth ficam em preferências privadas do Android e
  o histórico em banco SQLite privado do app. Um aplicativo de produção poderia
  fortalecer isso com armazenamento de tokens via Android Keystore e testes adicionais.
- **Duplicatas entre fontes:** casos em que API e exportação registram a mesma reprodução
  com precisão de horário diferente podem exigir reconciliação adicional.
- **Pacote:** `com.echomusic.stats`, Android mínimo 8.0 (API 26), target Android 14 (API 34).

## Estrutura

```
app/src/main/java/com/echomusic/stats/
  MainActivity.java     # tela WebView + ponte nativa + atividades de arquivos
  SpotifyClient.java    # OAuth PKCE + Spotify Web API
  StatsDatabase.java    # SQLite + agregações dos rankings
  HistoryImporter.java  # importação streaming JSON e ZIP
app/src/main/assets/
  index.html            # interface responsiva
  app.css               # identidade visual ECHO
  app.js                # dashboards, rankings, gráficos, dados e prévia JSON
  echo_universe.js      # 9 novas áreas, atividades, jogos e persistência local
  echo_universe.css     # visual responsivo ECHO Universe
.github/workflows/build-apk.yml # geração de APK pelo GitHub
```

## Fontes oficiais para implementar os dados

- <https://developer.spotify.com/documentation/web-api/tutorials/code-pkce-flow>
- <https://developer.spotify.com/documentation/web-api/reference/get-users-top-artists-and-tracks>
- <https://developer.spotify.com/documentation/web-api/reference/get-recently-played>
- <https://developer.spotify.com/documentation/web-api/tutorials/february-2026-migration-guide>
- <https://support.spotify.com/article/understanding-your-data/>

**Aviso:** ECHO é um projeto independente e não tem afiliação ou patrocínio do Spotify.