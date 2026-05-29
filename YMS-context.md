# YMS Improvements v4 — Project Context

> Leia este arquivo no início de cada sessão antes de trabalhar na FRF.

---

## Pessoas
- **PM:** Camila Braz (camila.braz@shopee.com) — Shopee BR
- **FRF owner:** Guilherme Frassan (Local Group Product)

## Regras gerais
- Texto da FRF sempre em **inglês**
- Nunca editar a FRF diretamente — mandar texto no chat para a Camila colar
- Logs **não** aparecem em flow diagrams
- Toggle "Show Release Time to Driver" fica no cartão **STA Threshold** (nível station), não no modal de entry site individual

---

## TO Pack Types (sistema: TO Pack Configuration)
| ID | Nome | Status |
|----|------|--------|
| 3 | **Scuttle** | Available |
| 2 | **Saca** | Available |
| 4 | **Pallet** | Available |
| 6 | **Volumoso** | Available |
| 5 | **Saca Sorter** | Available |
| 1 | [NÃO USAR] TESTE | Unavailable |

> ⚠️ Scuttle e Saca são tipos **diferentes**. Não confundir.
> 📄 Referência completa: `referencias/to-pack-types.md`

## Size Types
- **Bulky**, **Normal**, **Quasi-bulky**
- Mutuamente exclusivos por order; somam 100%

## Composição de carga
- TO Pack Type: cada TO tem exatamente um tipo → percentuais somam **100%**
- Size Type: cada order tem exatamente um tipo → percentuais somam **100%**
- As duas dimensões são **independentes** entre si

---

## Entry Site logic
- Sites numerados 1 (mais perto da doca) a 5 (mais longe)
- Avaliação de **5 → 1** (atribui o mais distante disponível primeiro)
- Cascade sempre move drivers de sites mais altos para mais baixos quando vaga abre
- Vehicle Type Pools: mesmo tipo não pode estar em dois pools do mesmo site; soma de vagas ≤ capacidade do site

## STA Threshold (nível station)
- Campos: STA LH Inbound (min) + STA LH Outbound (min)
- Toggle: **Show Release Time to Driver** — quando ON, mostra horário de liberação no Driver App; quando OFF, só mensagem genérica
- Se threshold não configurado para o tipo de chegada → check é ignorado

## QSDC — Queue Sequence Display Control (nível station)
- Toggle: Hide Queue Sequence From Driver After Certain Sequence (default ON)
- Campo: Default Value for Hidden Sequence (From Xth Onwards) — obrigatório quando toggle ON

---

## Arquivos do projeto
| Arquivo | Descrição |
|---------|-----------|
| `[BR FRF] YMS Improvements v4 atualizado.docx` | FRF principal |
| `entry-site-config-interactive.html` | Mockup interativo Entry Site Config (sem animação) |
| `entry-site-config-animated.html` | Mockup animado Entry Site Config |
| `4114-examples-table.html` | Tabela visual de exemplos 4.1.1.4 |
| `4114-gdocs-table.html` | Tabela de exemplos 4.1.1.4 no formato Google Docs (colar diretamente) |
| `4114-example6.html` | Example 6 isolado (section-level fallback) para colar no Google Docs |
| `early-arrival-monitoring-flow.html` | Flow diagram 4.2.3.5 |
| `entry-site-assignment-flow.html` | Flow diagram 4.2.3.6 |
| `vacancy-cascade-flow.html` | Flow diagram 4.2.3.7 |

---

## Status da FRF
- ✅ 4.1 — Revisado e consistente
- ✅ 4.2 — Revisado e consistente
- ⏳ 4.3 — Notifications (ainda não atualizado)
- ✅ 4.4 — Queue list visibility (ok)
