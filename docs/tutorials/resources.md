# Recursos e Uso do Sistema

Quais recursos estão disponíveis e quanto estou usando?

## recursos
- processamento cpu
- processamento gpu
- armazenamento
- escrita/leitura de disco
- transferência de rede


Alguns comandos úteis para visualizar recursos
- htop / top
    visualizar processamento e memória RAM disponíveis na máquina
- nvidia-smi
    visualizar processamento e memória de GPU disponíveis
- taskset
    limita a cadeia de processo provenientes de um comando a um conjunto de CPUs.
    taskset -c 3-16

- CUDA_VISIBLE_DEVICES=1
    flag para indicar GPUs disponíveis para o seu código. É uma forma rápida 
    CUDA_VISIBLE_DEVICES=1 command

- du -sh
