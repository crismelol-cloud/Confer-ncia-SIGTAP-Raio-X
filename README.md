# Conferência SIGTAP — Raio-X e Densitometria

Ferramenta interna da Secretaria Municipal de Saúde de Franca/SP.

Lê as planilhas mensais de Raio-X / Densitometria, localiza o **código SIGTAP**
oficial de cada procedimento e, opcionalmente, cruza com o relatório do **SINFRA (OCI)**
para identificar quais pacientes já realizaram o exame.

## Como usar

1. Abra o `index.html` (ou o link do GitHub Pages).
2. **Passo 1** — arraste as planilhas de Raio-X / Densitometria (`.xls` ou `.xlsx`).
- esses documentos são as planilhas que são enviadas pelo setor de pagamento -
3. **Passo 2 (opcional)** — arraste o relatório do SINFRA (`.csv`, `.xls` ou `.xlsx`).
- esse documento é extraído do sistema SINFRA -
4. Confira os resultados nas abas e exporte em **XLSX** ou **CSV**.

Os procedimentos da lista prioritária aparecem **em destaque** (linha amarela e
coluna `DESTAQUE` na exportação).

## Privacidade

Todo o processamento acontece **no próprio navegador**. Nenhum arquivo é enviado
para servidores. A biblioteca de leitura de planilhas está embutida no arquivo,
então funciona mesmo sem internet.

## Arquivo

- `index.html` — o app completo, autocontido (não depende de nada externo).
