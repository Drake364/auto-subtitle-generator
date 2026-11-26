# Gerador Automático de Legendas (Auto Subtitle Generator)

O Gerador Automático de Legendas é um aplicativo Android para criar, editar, traduzir e exportar legendas diretamente no seu dispositivo. O reconhecimento de fala roda localmente com [whisper.cpp](https://github.com/ggerganov/whisper.cpp) (modelos Whisper) ou [Vosk](https://github.com/alphacep/vosk-api), a tradução roda no dispositivo com o [ML Kit](https://developers.google.com/ml-kit/language/translation), e o processamento de mídia é feito pelo [FFmpeg Kit](https://github.com/arthenica/ffmpeg-kit/tree/main/android). Nenhum serviço em nuvem é necessário e o seu áudio nunca sai do dispositivo.

![Ícone do Gerador Automático de Legendas](https://github.com/user-attachments/assets/8d2f8631-a595-49ec-92ec-9b60a72e73cf)

## Destaques

- Gere legendas a partir de vídeos totalmente offline.
- Dois motores de reconhecimento: Whisper (whisper.cpp) e Vosk.
- Carimbos de tempo em nível de palavra do Whisper para uma sincronização precisa e clicável.
- Transcrição multilíngue com detecção automática de idioma.
- Tradução no dispositivo, incluindo legendas bilíngues (original + tradução).
- Detecção Opcional de Atividade de Voz (VAD) para pular silêncios e acelerar vídeos longos.
- Enfileire vários vídeos e continue o processamento enquanto o app está em segundo plano.
- Baixe, pause, retome, cancele e gerencie modelos de fala dentro do app.
- Modelo Whisper em inglês já incluído para o app funcionar imediatamente.
- Pré-visualize as legendas com a reprodução do vídeo antes de exportar.
- Edite, mescle, divida, exclua e ajuste o tempo das legendas geradas.
- Exporte arquivos de legenda como SRT ou VTT.
- Exporte vídeos com legendas suaves (soft) ou legendas embutidas (hard burned-in).
- Crie legendas estilizadas para formatos curtos, incluindo a sincronização palavra por palavra.
- Use o modelo local Gemma 4 E2B para encontrar, revisar, cortar e exportar Shorts a partir de transcrições de vídeos longos.
- Exportação em lote de arquivos de legenda ou vídeos com legendas.
- Acompanhe as exportações concluídas em uma biblioteca de exportação.

## Capturas de Tela

| Gerar | Prévia | Modelos |
| --- | --- | --- |
| <img width="270" height="600" alt="Screenshot_20260602_001838" src="https://github.com/user-attachments/assets/1b0b5085-228b-4503-b573-de4e3254001d" /> | <img width="270" height="600" alt="Screenshot_20260602_002104" src="https://github.com/user-attachments/assets/fcaec73e-fd06-4018-9f1f-40e5ceaac0d5" /> | <img width="270" height="600" alt="Screenshot_20260602_002154" src="https://github.com/user-attachments/assets/587eb864-e00f-419e-84db-bf352fd14abe" /> |

| Exportações | Configurações |
| --- | --- |
| <img width="270" height="600" alt="Screenshot_20260602_002525" src="https://github.com/user-attachments/assets/3ba347db-fd3d-4073-9e75-fdbc7a75136e" /> | <img width="270" height="600" alt="Screenshot_20260602_002536" src="https://github.com/user-attachments/assets/6e5429ef-df4b-4024-b675-aec1d40b6040" /> |

## Instalar APK
Você pode encontrar as versões mais recentes com os arquivos APK aqui: https://github.com/Serkali-sudo/auto-subtitle-generator/releases

## Funcionalidades

### Geração local de legendas

O Gerador Automático de Legendas extrai o áudio do vídeo selecionado, executa o reconhecimento de fala localmente e transforma a fala reconhecida em legendas sincronizadas. As legendas geradas podem ser revisadas imediatamente na tela de pré-visualização.

Como o reconhecimento é local, o áudio do vídeo não é enviado para um servidor. A precisão depende do modelo selecionado, da qualidade do áudio, do idioma, dos sotaques, do ruído de fundo e do desempenho do dispositivo.

### Motores de reconhecimento

O aplicativo suporta dois motores offline e permite escolher um modelo a partir de um único catálogo:

- **Whisper (whisper.cpp):** o motor padrão. Fornece timestamps em nível de palavra, forte precisão multilíngue e detecção automática de idioma. Os modelos variam de `tiny` e `base` até `small`, `medium` e `large-v3` / `large-v3-turbo`, cada um com variantes apenas em inglês e multilíngues, além de versões quantizadas (`q5`/`q8`) que trocam tamanho por precisão. Um modelo Base em inglês quantizado já vem incluído no APK para que a geração funcione sem nenhum download.
- **Vosk:** modelos leves baseados em Kaldi que cobrem uma ampla variedade de idiomas, úteis em dispositivos mais simples ou para idiomas onde um pequeno modelo dedicado é preferível.

### Idioma e tradução

- **Seleção de idioma:** escolha um idioma específico para transcrição ou deixe o Whisper detectá-lo automaticamente. Modelos Whisper multilíngues podem transcrever áudios que não sejam em inglês diretamente.
- **Tradução no dispositivo:** traduza as legendas geradas com o ML Kit. Os pacotes de idiomas para tradução são baixados sob demanda e rodam localmente.
- **Camadas de legenda:** exporte a transcrição original, apenas a tradução, ou legendas **duplas (bilíngues)** que empilham o texto original e o traduzido juntos.

### Detecção de Atividade de Voz (pular silêncio)

Para vídeos longos, o VAD pode detectar regiões de fala e pular trechos de silêncio para que a transcrição seja mais rápida. Dois detectores estão disponíveis:

- **WebRTC VAD** (rápido, leve)
- **Silero VAD** (neural, mais seletivo)

Cada um suporta sensibilidade Normal / Agressiva / Muito agressiva. O VAD vem **desativado por padrão**, pois pular áudio pode ocasionalmente perder falas baixas ou alterar os tempos. Quando você adiciona um vídeo longo, o aplicativo oferece ativar o salto de silêncio para aquele vídeo, com uma clara compensação entre velocidade e precisão, deixando os vídeos mais curtos intocados.

### Processamento de fila

Você pode adicionar vários vídeos à fila de legendas e processá-los um por um. O estado da fila é persistido, então os itens pendentes e concluídos permanecem visíveis mesmo após reiniciar o aplicativo. Cada vídeo na fila também lembra suas próprias configurações, como se o salto de silêncio foi ativado para ele.

A fila suporta:

- Geração de vídeo único.
- Geração de fila com vários vídeos.
- Acompanhamento do progresso do trabalho ativo.
- Cancelamento de trabalho de mídia ativo.
- Ações de seleção múltipla.
- Selecionar tudo para os itens visíveis na fila.
- Exportação em lote de legendas.
- Exportação em lote de vídeos.

### Trabalho em segundo plano (Foreground)

Trabalhos de longa duração são gerenciados por um serviço em primeiro plano (foreground service) em vez de serem de responsabilidade apenas da tela ou do view model. Isso mantém o trabalho iniciado pelo usuário vivo quando o aplicativo vai para segundo plano ou a interface é recriada, e um wake lock mantém o dispositivo trabalhando durante tarefas longas.

O serviço é usado para:

- Geração de legendas.
- Salvamento de arquivos de legenda.
- Exportação de vídeo com legendas suaves (soft).
- Exportação de vídeo com legendas embutidas (hard).
- Exportações em lote.
- Downloads de modelos.

Downloads de modelos e processamento de mídia usam notificações separadas, para que um download possa continuar enquanto a geração de legendas ou a exportação também está rodando.

### Pré-visualização e edição de legendas

A tela de pré-visualização permite inspecionar e ajustar as legendas geradas antes de exportar.

As ações de edição suportadas incluem:

- Editar o texto da legenda.
- Mesclar falas.
- Dividir ou ajustar o tempo da legenda.
- Excluir falas.
- Pré-visualizar as legendas durante a reprodução do vídeo.
- Usar legendas estilizadas para vídeos de formato curto.

### Exportação de arquivo de legenda

As legendas geradas podem ser salvas como:

- `SRT`
- `VTT`

O formato padrão de exportação em lote de legendas pode ser alterado nas configurações.

### Exportação de vídeo

O aplicativo pode criar arquivos de vídeo com legendas de duas maneiras principais:

- **Legendas suaves (Soft):** as legendas são armazenadas como um fluxo de legenda separado no contêiner do vídeo quando possível, para que os players compatíveis possam ativá-las ou desativá-las.
- **Legendas embutidas (Hard):** as legendas são gravadas nos quadros do vídeo e ficam sempre visíveis.

A exportação de legenda suave é útil quando você deseja uma faixa de legenda não destrutiva. A exportação de legenda embutida é útil para plataformas ou players onde as legendas devem estar sempre visíveis. Ambas respeitam a camada de legenda selecionada (original, tradução ou bilíngue).

### Legendas para Shorts

O estilo de legenda para formato curto está disponível para vídeos verticais/para redes sociais. O aplicativo pode usar o tempo em nível de palavra para criar legendas palavra por palavra e pode exportar legendas estilizadas em saídas de vídeo suportadas.

As configurações incluem opções para:

- Tamanho padrão da legenda curta.
- Legendas curtas em maiúsculas.
- Modo palavra por palavra.
- Pular a janela de configuração de shorts.

### Extração de Shorts

Os itens concluídos na fila incluem a ação **Criar Shorts**. No Android 12 ou superior, o modelo opcional Gemma 4 E2B analisa a transcrição salva com timestamps inteiramente no dispositivo e propõe cinco clipes editáveis de 20 a 60 segundos. A tela de revisão suporta seleção de clipes, ajustes de limites encaixados nas legendas, legendas embutidas originais/traduzidas/bilíngues, e um corte horizontal 9:16 por clipe. Os clipes selecionados são exportados como vídeos MP4 de 1080×1920 e aparecem na biblioteca de exportação.

O modo de montagem de frases não requer o Gemma. Digite uma palavra ou frase e o AutoSub une todas as ocorrências com timestamps em um único vídeo, usando o tempo exato da palavra ou expandindo cada correspondência para a sua fala completa na legenda.

Os itens concluídos na fila também oferecem **Apenas fala**, que une todas as falas das legendas em um corte de fala contínuo, e **Sem silêncio**, que usa as configurações WebRTC ou Silero VAD selecionadas para remover regiões de silêncio. A remoção de silêncio via VAD também é opcional ao exportar Shorts selecionados por IA.

O modelo LiteRT-LM tem aproximadamente 2.6 GB e é gerenciado na tela de Modelos com downloads que podem ser retomados. Dispositivos com menos de 8 GB de RAM recebem um aviso antes de carregá-lo. Versões mais antigas do Android mantêm todos os recursos de legenda existentes, mas não carregam o ambiente de execução de IA.

### Gerenciador de modelos

O aplicativo inclui um gerenciador unificado para modelos de reconhecimento de fala Whisper e Vosk.

Os recursos do modelo incluem:

- Suporte ao modelo Whisper em inglês já incluído.
- Catálogo de modelos para download cobrindo muitos idiomas e níveis de precisão.
- Pesquisa e filtros horizontais (chips).
- Pausar, retomar e cancelar downloads.
- Fila de downloads de modelos.
- Retomada de downloads parciais.
- Verificações de compatibilidade para modelos grandes.
- Opção de exibição do uso de RAM.

Os modelos baixados não são carregados automaticamente após a conclusão do download enquanto outra tarefa de geração ou exportação estiver ativa. Isso evita que o processamento de mídia ativo seja interrompido por uma troca de modelo.

### Biblioteca de exportação

As exportações concluídas são salvas na biblioteca de exportação para que sejam fáceis de encontrar depois.

A biblioteca de exportação suporta:

- Registros de exportação de legendas e vídeos.
- Pesquisa e filtragem.
- Visualização em grade/lista.
- Abertura de arquivos exportados.
- Compartilhamento de arquivos exportados.
- Movimentação de arquivos.
- Exclusão de registros.
- Ações de seleção múltipla.
- Selecionar tudo para os itens de exportação visíveis.

### Configurações

As configurações atuais incluem:

- Idioma de reconhecimento / detecção automática (Whisper).
- Tradução de legendas, com idiomas de origem e destino.
- Modelo e sensibilidade da Detecção de Atividade de Voz.
- Máximo de palavras por legenda.
- Manter frases juntas.
- Suprimir legendas não-faladas (SDH).
- Formato de exportação em lote de legendas.
- Preferência de local de exportação.
- Tamanho do texto da legenda curta.
- Legendas curtas em maiúsculas.
- Legendas curtas palavra por palavra.
- Pular janela de configuração de shorts.
- Notificações de conclusão.
- Exibição do uso de RAM.

## Como funciona

1. Escolha um vídeo ou adicione vídeos à fila.
2. Escolha o modelo de fala (Whisper ou Vosk) que deseja usar.
3. Opcionalmente, defina o idioma, a tradução e as opções de salto de silêncio.
4. Gere legendas localmente no dispositivo.
5. Pré-visualize e edite as legendas geradas.
6. Exporte as legendas como um arquivo ou renderize um vídeo com legendas.

Para operações de longa duração, o serviço em primeiro plano mantém a tarefa ativa conectada ao sistema de notificações do Android. A interface se reconecta a esse serviço quando o aplicativo é reaberto, para que o progresso e o estado da tarefa ativa possam ser mostrados novamente sem reiniciar a tarefa.

## Permissões

O aplicativo usa permissões de serviço em primeiro plano e wake lock do Android para trabalhos de longa duração:

- `FOREGROUND_SERVICE`
- `FOREGROUND_SERVICE_MEDIA_PROCESSING`
- `FOREGROUND_SERVICE_DATA_SYNC`
- `WAKE_LOCK`

O trabalho de processamento de mídia usa o tipo de serviço em primeiro plano de processamento de mídia. Os downloads de modelos usam o tipo de serviço em primeiro plano de sincronização de dados. O wake lock mantém a CPU ativa durante transcrições e exportações longas.

No Android 13 ou superior, a permissão de notificação afeta notificações opcionais de conclusão/progresso. As notificações obrigatórias do serviço em primeiro plano ainda fazem parte do caminho ativo do serviço em primeiro plano.

## Tecnologias utilizadas

- Aplicativo Android escrito em Java.
- [whisper.cpp](https://github.com/ggerganov/whisper.cpp) para reconhecimento de fala Whisper offline com tempo em nível de palavra.
- [Vosk Android](https://github.com/alphacep/vosk-api) para reconhecimento de fala offline baseado em Kaldi.
- [android-vad](https://github.com/gkonovalov/android-vad) (WebRTC e Silero) para detecção de atividade de voz.
- [ML Kit Translation](https://developers.google.com/ml-kit/language/translation) para tradução de legendas no dispositivo.
- [FFmpeg Kit](https://github.com/arthenica/ffmpeg-kit/tree/main/android) para extração de áudio e exportação de vídeo/legenda.
- [AndroidX Media3](https://developer.android.com/jetpack/androidx/releases/media3) para reprodução de vídeo.
- [LiteRT-LM](https://developers.google.com/edge/litert-lm/android) para rodar o AI Shorts Editor, que é basicamente o modelo Gemma42B
- [ML Face Detection](https://developers.google.com/ml-kit/vision/face-detection/android) para rastrear e enquadrar automaticamente rostos falantes nos shorts gerados
- Serviços em primeiro plano do Android para geração, exportação e download de longa duração.
- Material Components para a interface do Android.

## Compilar a partir do código-fonte

Clone o projeto e abra no Android Studio, ou compile pela linha de comando:

```powershell
.\gradlew.bat :app:assembleDebug
