# Baú NFC — projeto mecânico para impressão 3D

Baú com tampa articulada, compartimento superior para o prêmio e fundo falso removível que esconde a eletrônica. Um ESP32 lê o cartão pelo RC522 e libera uma fechadura solenoide metálica. O LCD 16×2 fica na frente. O servo SG90 foi abandonado.

Este repositório cobre só o **projeto mecânico** (CAD paramétrico em CadQuery, STEP e STL para o Bambu Studio).

## Estrutura

| Pasta | Conteúdo |
|---|---|
| `Bau_NFC_Trava_Lateral_v3/` | Versão 3, preservada como referência de medidas, componentes e funcionamento. Não editar. |
| `Bau_NFC_V4/` | Versão 4, redesenho completo (aparência e montagem). **Ainda não gerada.** |
| `docs/` | Análise da V3, decisões da V4 e medidas pendentes da fechadura. |

## Status (2026-11-05)

- [x] Leitura da V3: código, STEP, STL e imagens. Ver [`docs/ANALISE_V3.md`](docs/ANALISE_V3.md).
- [ ] Etapa 1: proposta visual da V4 (aberta, fechada e corte da trava).
- [ ] Etapa 2: CAD paramétrico da V4.
- [ ] Etapa 3: peças de teste da trava e do engate e verificação da trajetória da tampa.
- [ ] Etapa 4: STEP aberto e fechado, STLs separados e guia de montagem e impressão.

**Pendente com o dono do projeto:** medidas reais da fechadura (ver `docs/ANALISE_V3.md`) e modelo da impressora Bambu.

## Como rodar o CAD

Requer Python 3.10–3.12 (o CadQuery não tem wheels para 3.13+).

```bash
python -m venv .venv
.venv\Scripts\activate
pip install cadquery trimesh matplotlib numpy
```

V3: `python Bau_NFC_Trava_Lateral_v3/gerar.py` regenera os arquivos da V3.

> Observação: o Python da Microsoft Store não enxerga pastas dentro de `AppData\Roaming`. Mantenha o projeto numa pasta comum, como `Documentos`.
