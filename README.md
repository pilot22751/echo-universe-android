# ECHO LIFE 4.0 — cinema, Steam, YouTube e música, de verdade

Aplicativo Android pessoal, independente e *offline-first*, com WebView local (HTML/CSS/JavaScript) e integrações Android nativas. Não é uma rede social. A versão 4.0 transforma as três novas conexões da versão 3.0 em **módulos interativos completos**, sem quebrar o ECHO musical e seu Universo 2.0.

## 4.0: 31 ambientes interativos

### ECHO LIFE — quatro áreas
- **Painel multimídia** com totais dos catálogos e atalhos de exploração.
- **Linha do tempo** reúne entradas datadas do diário do Letterboxd, sessões manuais de games e vídeos, memórias pessoais e destaques musicais disponíveis; não é um registro completo automático de todos os serviços.
- **Explorar** reúne roleta que mistura filmes, jogos e vídeos, metas de progressão e missões multimídia.
- **Meu cofre** faz backup/restauração JSON das notas pessoais, favoritos, sessões, duelos, metas e entradas *criadas no ECHO LIFE 4*. Não inclui credenciais, nem substitui a exportação de origem Spotify/Letterboxd. No Android, o seletor nativo salva e lê os backups privados em um local escolhido pelo usuário.

### Cinema / Letterboxd — nove áreas
- Painel de cinema com atividade por mês, nota média, sessões datadas e registros recentes.
- Acervo pesquisável, ordenação, favoritos, filtros, importação de filmes e inclusão manual.
- Calendário de sessões, reprises e anos mais assistidos (somente quando há data).
- DNA cinematográfico: distribuição de estrelas, décadas, melhores e piores notas registradas.
- Watchlist, marcações pessoais, roleta de filmes e controle de itens escolhidos.
- Batalhas ELO entre dois filmes com ranking de preferências que evolui a cada duelo.
- Caderno para opiniões privadas, lembranças, notas pessoais e tags.
- Missões e conquistas calculadas de registros disponíveis no ECHO.
- Conectar: usuário Letterboxd, sincronizar RSS público, importar ZIP/CSV, desconectar.

### Games / Steam — nove áreas
- Painel com horas acumuladas e últimas duas semanas **reportadas pela Steam**.
- Biblioteca pesquisável, filtros por status e jogo, títulos manuais e favoritos.
- Backlog pessoal, jogando, pausado e concluído; roleta para títulos abandonados.
- Diário de sessões **manuais** com data, duração, humor, texto e histórico.
- Análises de concentração de horas, jogos não iniciados e evolução das sessões manuais.
- Batalhas ELO entre seus jogos preferidos.
- Caderno de memórias de jogos, notas e tags pessoais.
- Missões e conquistas *do ECHO*, não conquistas oficiais Steam.
- Conectar: SteamID64, Steam Web API Key (guardada cifrada), sincronizar biblioteca.

### YouTube — nove áreas
- Painel com playlists públicas, vídeos da amostra, fila e sessões pessoais.
- Explorador de playlists com contagens publicadas pela API e vídeos carregados.
- Biblioteca buscável com filtros, favoritos e inclusão manual por link do YouTube.
- Minha fila pessoal, roleta, marcações de visualização e opção de abrir o YouTube.
- Diário **manual** de sessões assistidas (minutos, data, humor e memória).
- Análises de canais presentes nos vídeos retornados, tamanho de playlists e diário.
- Caderno de anotações, resumos e avaliações pessoais.
- Missões e conquistas baseadas nas atividades guardadas no ECHO.
- Conectar: ID do canal/@handle + YouTube Data API v3 Key (cifrada), sincronização de **playlists públicas**.

## Limites e privacidade — importante
- **Letterboxd:** RSS público não é histórico completo. Para importar filmes antigos, usar `Settings → Data → Export` no Letterboxd. ZIP/CSV podem ter filmes sem data de visualização; estes não contam nas análises temporais. O ECHO não sincroniza avaliações feitas dentro dele de volta para o Letterboxd.
- **Steam:** a Web API devolve biblioteca exposta e tempo total de jogo; quando existe, período recente. **Não fornece histórico diário completo de sessões**, portanto o registro de sessões no ECHO é manual. Flags 'finished', 'playing' etc. também são pessoais e não alteram Steam.
- **YouTube:** API Key pública permite apenas dados públicos; **não há acesso ao histórico de visualizações pessoais, minutos assistidos, Watch Later, likes privados ou playlists privadas** sem projeto OAuth e escopos específicos, ainda não implementados. Os vídeos carregados são amostra das primeiras playlists públicas. Não se deve interpretar a lista de vídeos públicos como vídeos assistidos.
- **Spotify:** mantém o login PKCE, rankings oficiais e importação de JSON/ZIP que já existiam. Minutos reais dependem do histórico disponibilizado pelo Spotify.
- **Backups:** os novos dados pessoais 4.0 ficam no `localStorage` privado do WebView. Você pode salvar um arquivo JSON e restaurá-lo. Esse backup não copia o banco SQLite com histórico musical, nem o diário original do ECHO Universe 2.0. Faça backup dos dados importantes antes de desinstalar qualquer versão.
- O aplicativo não possui servidor ECHO, não solicita senha de serviços e não publica suas anotações.
- Steam API Key e YouTube API Key são armazenadas com AES-GCM + Android Keystore pelo `LifeIntegrations.java` nativo e não são expostas ao JavaScript nem ao repositório.
- Código-fonte e interface são implementados localmente, com HTML escapado para dados externos, links validados por domínio e a opção de desligar qualquer serviço.

## Instalar APK

- GitHub Actions: `Actions → Gerar APK do ECHO → Run workflow`, depois `Artifacts → ECHO-Android-APK → app-debug.apk`.
- O build usa Java 17, Gradle 8.11.1 e Android SDK 35, compilando para Android 8.0+.
- É um **APK de desenvolvimento**; a compilação confirma que o código compila, mas não substitui testar as conexões e o comportamento de arquivos em um aparelho físico.
- Por usar a assinatura debug de cada runner, upgrades podem falhar por incompatibilidade de certificado. **Não desinstale uma versão anterior sem exportar seus dados**. Precisamos de assinatura estável e proteção da chave para atualizações seguras no futuro.

## Fonte do projeto

- `app/src/main/assets/echo_life_studio.js`: 31 ambientes, filtros, desafios, duelos, diários, coleções, linha do tempo e backup.
- `app/src/main/assets/echo_life_studio.css`: interface adaptada a celular e computador.
- `app/src/main/assets/echo_life.js`: fluxo de sincronização da versão 3.0 + ponte para o ECHO Life Studio.
- `app/src/main/java/com/echomusic/stats/LifeIntegrations.java`: RSS/importador de Letterboxd, biblioteca Steam, playlists YouTube e chaves cifradas.
- `app/src/main/java/com/echomusic/stats/MainActivity.java`: interface, Spotify, operações nativas e backup JSON do Studio 4.0.
- `app/src/main/assets/echo_universe.js`, `app.js` e `StatsDatabase.java`: universo musical original preservado.

A prévia HTML offline funciona sem conectar APIs; nela você pode cadastrar itens manualmente. **Não há estatísticas fictícias de serviços carregadas como dados reais**. A área musical ainda contém demonstração marcada quando não há histórico importado.

Projeto independente, sem afiliação com Spotify, Letterboxd, Valve/Steam ou Google/YouTube.