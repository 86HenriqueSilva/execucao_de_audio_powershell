Sistema de Automação de Áudios Hospitalares (PowerShell)

Este script em PowerShell foi desenvolvido para gerenciar a execução de áudios informativos (mensagens de Ouvidoria, avisos programados e comunicados aleatórios) em um ambiente hospitalar, garantindo o cumprimento de rotinas fixas e o balanceamento de avisos diários.
Funcionalidades Principais

    Áudios Fixos (Ouvidoria): Execução do áudio da Ouvidoria em horários predefinidos (ex: 09:00, 10:00, 11:00, 13:00, 14:00, 15:00, 16:00), de segunda a sexta-feira.

    Rotinas Programadas (Blocos B1-B6): Execução de blocos de áudios em horários específicos, com repetição definida (geralmente 3 vezes por execução).

    Rotina Noturna Específica (20:30): Execução alternada e sequencial de cinco áudios programados (B6, B5, B3, B4, B2), repetindo o ciclo completo 3 vezes.

    Áudios Aleatórios (Blocos A1-A6): Execução balanceada e randômica de áudios dentro do período das 07:30h às 22:00h.

    Limite Diário: A execução dos áudios aleatórios é limitada a 20 vezes por dia, com distribuição automática ao longo do período.

    Balanceamento: O script garante que cada áudio aleatório seja executado um número similar de vezes para manter a exposição equilibrada.

    Registro de Logs: Geração de logs diários com data, hora, usuário de execução e o status (início e fim) de cada áudio tocado, facilitando a auditoria e o acompanhamento.

 Pré-requisitos e Configuração

Para que o script funcione corretamente, o ambiente deve atender aos seguintes requisitos:

    Sistema Operacional: Windows com suporte a PowerShell.

    Biblioteca de Mídia: O script utiliza a biblioteca .NET PresentationCore para a reprodução de áudios MP3.

    Estrutura de Pastas:

        Crie a pasta principal: C:\execucao de audio

        Dentro dela, o script criará a pasta de logs: C:\execucao de audio\logs

Estrutura de Arquivos de Áudio

Todos os arquivos de áudio (.mp3) devem ser colocados na pasta C:\execucao de audio.

Tipo de Áudio
	

Nome do Arquivo Exemplo
	

Função

Fixo
	

Ouvidoria Alfa.mp3
	

Tocado em horários fixos (seg-sex).

Aleatório (A)
	

A1 - Crachá dos acompanhantes..mp3
	

Escolhido aleatoriamente, limitado a 20x/dia.

Programado (B)
	

B6 - UTI_09.mp3
	

Tocado em horários específicos (11:00, 15:00, etc.).
Como Executar o Script

O script é projetado para rodar continuamente em loop (while ($true)), idealmente executado como uma Tarefa Agendada (Scheduled Task) do Windows com privilégios adequados, para garantir que ele esteja ativo durante todo o período de operação (07:30 às 22:00) e monitorando os horários programados.
Passos de Execução

    Configurar Arquivos: Garanta que todos os arquivos MP3 estejam em C:\execucao de audio.

    Abrir PowerShell: Execute o PowerShell (de preferência como Administrador).

    Rodar o Script:

    # Supondo que você salvou o script como 'AudioScheduler.ps1'
    .\AudioScheduler.ps1

    Monitoramento: O script exibirá logs no console e registrará tudo nos arquivos de log na pasta logs.

Logs

Os arquivos de log são criados diariamente na pasta C:\execucao de audio\logs no formato execucao_YYYY-MM-DD.log.

Exemplo de linha de log:

2025-11-09 15:00:05 - [HENRIQUE] - Iniciada execução do áudio: C:\execucao de audio\B6 - UTI_09.mp3

 Notas Importantes

    Resolução de Conflitos: O script prioriza as execuções fixas e programadas. Ele NÃO executará um áudio aleatório se já estiver ocupado executando uma rotina fixa ou programada no mesmo momento.

    Balanceamento (Aleatórios): O balanceamento garante que a execução de cada áudio aleatório não exceda o teto de execuções (20 no total / 6 áudios = 4 execuções por áudio, arredondando para cima), antes de todos os outros áudios atingirem esse mesmo limite.
