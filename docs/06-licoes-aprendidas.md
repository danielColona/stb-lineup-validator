# 6. Lições aprendidas

[← Voltar ao README](../README.md)

## O que funcionou bem

- **Usar o OBS como analisador.** O OBS já decodifica, escala e compõe os quadros; o Advanced Scene Switcher transforma isso em regras sem uma linha de visão computacional própria. Ajustar um limiar é mudar um número na interface.
- **Duas condições complementares.** "Cor preta" sozinha não pega congelamento; "não mudou" sozinha não pega preto com ruído. Juntas, com **OU**, cobrem as falhas percebidas pelo assinante.
- **Evidência em vídeo.** Um print de tela preta não diz se o canal voltou em 2 s. Um clipe de 10 s, e outro na reativação, encerram a discussão.
- **Prova de vida periódica.** O clipe de 15 em 15 minutos transformou silêncio em informação.
- **Painel no próprio stream.** Quem acompanha o multiview remotamente vê os alertas sem abrir outro sistema.

## Decisões de projeto e o problema que cada uma evita

| Decisão | Problema evitado |
|---|---|
| Contagem + pausa de 15 min + reativação automática | Um canal fora do ar geraria um print a cada poucos segundos |
| Zeragem do contador após 36 s com 1–2 alertas | Alertas isolados, distantes no tempo, seriam tratados como recorrentes |
| Janela de zeragem ajustável por STB (36 s / 70 s) | Canais com comportamento diferente exigem tolerâncias diferentes |
| Telegram **e** overlay no multiview | Quem está na sala de controle não olha o celular; quem está fora não vê o multiview |
| Reboot controlado + correção do `global.ini` | OBS abrindo em safe mode após encerramento sujo, esperando um clique |
| Tempo de permanência do zapping por lista (`P13` / `P17`) | Canal com zap lento sair da tela antes de completar a janela de detecção |

## Limitações conhecidas

- **Não analisa áudio.** Canal com vídeo e sem som não é detectado.
- **Não identifica o conteúdo.** Canal sintonizado com programação errada (troca de mapeamento entre dois canais ativos) não é detectado.
- **Um script por STB.** A configuração foi replicada por STB; adicionar uma STB exige duplicar macros e scripts.
- **Dependência de sessão gráfica.** Captura e Browser Source exigem usuário logado no Windows.

## Próximos passos

- [ ] **Detecção de áudio** — condição de nível de áudio (silêncio sustentado) no próprio Advanced Scene Switcher.
- [ ] **OCR do número do canal** — confirmar, durante o zapping, que o STB sintonizou o canal pedido (o plugin já oferece condição de OCR).
- [ ] **Script de alerta único parametrizado** — STB, legenda e pastas como argumentos, eliminando a replicação.
- [ ] **Histórico persistente** — registrar todos os alertas (não só os 3 últimos) para relatórios de disponibilidade por canal.
- [ ] **Integração com o NMS** — publicar eventos via webhook/SNMP trap além do Telegram.
- [ ] **Correlação entre STBs** — falha simultânea em várias STBs no mesmo canal aponta para o headend; falha em uma só aponta para o ponto/STB.
