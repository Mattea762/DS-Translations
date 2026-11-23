# DS Game Translator Android 0.1.0

Aplicativo Android nativo para analisar ROMs Nintendo DS, extrair sequências de texto simples para CSV, permitir tradução fora do app e aplicar traduções por substituição em lugar.

## Fluxo
1. Abrir um arquivo `.nds` próprio.
2. Analisar e extrair sequências ASCII e UTF-16LE simples.
3. Exportar `textos_para_traduzir.csv`.
4. Editar a coluna `translation` em um editor de planilhas/texto, mantendo as colunas `offset`, `encoding` e `original`.
5. Importar o CSV e salvar uma cópia `_traduzido.nds`.

## Limitações
- Não reconhece automaticamente arquivos internos NitroFS, arquivos compactados, tabelas de caracteres proprietárias, ponteiros de texto ou scripts específicos de cada jogo.
- A busca por texto simples pode encontrar falsos positivos (dados que parecem texto).
- Para evitar corromper offsets, a tradução não pode ocupar mais bytes que a sequência original; nesta versão, os caracteres permitidos são ASCII básico.
- Não garante que o jogo aceite ou exiba a tradução. Cada jogo pode precisar de um adaptador específico.
- Use somente cópias de jogos que você tenha direito de modificar; não inclui nem fornece ROMs.

## Compilar APK
Abra o projeto no Android Studio com JDK 17, Android SDK 35 e Gradle compatível. Use Build > Build Bundle(s) / APK(s) > Build APK(s).
Saída esperada: `app/build/outputs/apk/debug/app-debug.apk`.

O ambiente de geração não tem Android SDK/Gradle configurados; este ZIP contém o projeto-fonte, não um APK compilado.


## Compilar sem computador (GitHub Actions)
O projeto inclui `.github/workflows/android.yml` para compilar o APK na nuvem:
1. Crie um repositório no GitHub e envie todos os arquivos desta pasta.
2. Abra a aba **Actions** do repositório.
3. Selecione **Build Android APK** e toque em **Run workflow** (ou aguarde o build após enviar para `main`).
4. Quando terminar, abra a execução e baixe o artefato `DSGameTranslator-debug-apk`.
5. Extraia o ZIP do artefato; dentro estará `app-debug.apk`.

O APK produzido é de depuração (debug), não assinado para publicação na Play Store.
