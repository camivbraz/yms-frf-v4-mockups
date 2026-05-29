# Queue Statuses — YMS
Source: Guia do Usuário - Gerenciamento de Fila e de Pátio

| Status | Nome no App | Descrição |
|--------|------------|-----------|
| **Pending** | Aguardando doca | Driver registrado na fila, aguardando atribuição de doca |
| **Assigned** | Pronto para doca | Driver com doca atribuída, a caminho ou aguardando chamada |
| **On Hold** | Veículo em espera | Driver desprioritizado; doca atribuída é removida; tempo de espera começa a contar |
| **Occupied** | — | Driver ocupando a doca |
| **Completed** | — | Processo finalizado |

## Transições possíveis de On Hold
- On Hold → **Pending** (Add to queue)
- On Hold → **Assigned** (Reassign — atribui nova doca diretamente)

## Observações
- On Hold pode ser aplicado a drivers com status Pending ou Assigned
- Ao ir para On Hold: doca atribuída é removida
- Fonte slides 25-29 (SOC) e slide 119 (LM)
