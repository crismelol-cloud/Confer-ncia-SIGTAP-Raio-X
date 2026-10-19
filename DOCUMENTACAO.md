# Documentação — Conferência SINFRA × Prestador

Secretaria Municipal de Saúde de Franca/SP
Última atualização: 19/10/2026

Ferramenta interna, de página única (HTML), que roda **inteiramente no navegador** — nenhum
arquivo é enviado para servidores. A biblioteca de leitura de planilhas está embutida, então
funciona até sem internet.

---

## O que o sistema faz (primeira parte)

Confronta o **relatório do SINFRA (OCI)** com as **planilhas do prestador** (Raio-X /
Densitometria), **pelo nome do paciente** — coluna BENEFICIARIO das planilhas × coluna Paciente
do SINFRA — e gera **uma planilha** listando todos os registros do SINFRA, cada um marcado como:

- **Encontrado no prestador** — o nome aparece nas planilhas do prestador; e
- **Não encontrado** — o nome não aparece.

Para os encontrados, a planilha ainda mostra **quais exames** o paciente fez no prestador
(código + procedimento) e **as datas** correspondentes.

O cruzamento ignora acento, espaço e pontuação (ex.: "JOÃO DA SILVA" = "JOAO DA  SILVA").

**Destaques (na tela e no arquivo exportado).** São duas regras, ambas com **fundo amarelo**:

- **Fonte vermelha** — um **código RX prioritário (OCI)** está **nas duas planilhas**: o SINFRA
  pediu aquele código (coluna Exame) e o prestador realizou o mesmo código.
- **Fonte verde** — o EXAME (SINFRA) veio **apenas como "RAIO-X"** (genérico, sem código) **e** os
  EXAMES REALIZADOS (PRESTADOR) incluem pelo menos um dos códigos prioritários.

Há contadores para cada regra e um filtro "Evidenciados" (mostra as duas). A lista dos 20 códigos
prioritários está no fim deste guia.

> Há também uma aba auxiliar "Conferência SIGTAP", que apenas mostra o código SIGTAP de cada
> procedimento das planilhas do prestador. É um apoio; a **primeira parte** é a planilha de
> comparação descrita acima.

---

## Os modelos de arquivo (o que alimentar o sistema)

### 1. Planilhas do prestador (.xls ou .xlsx) — uma ou várias
A empresa que faz o Raio-X envia esses arquivos. O sistema **procura sozinho** a linha de
cabeçalho que contém a coluna **PROCEDIMENTO**, então a posição das colunas pode variar.

| Coluna          | Uso                                                |
|-----------------|----------------------------------------------------|
| DATA            | Data do exame no prestador                         |
| BENEFICIARIO    | Nome do paciente (**chave do cruzamento**)         |
| QTDE            | Quantidade (informativo)                           |
| CODIGO          | Código SIGTAP — usado quando existe na planilha    |
| PROCEDIMENTO    | Nome do procedimento (ex.: RX JOELHO DIREITO AP+P) |
| VALOR (R$)      | Informativo                                        |

Linhas com "TOTAL" são ignoradas.

### 2. Relatório SINFRA — OCI (.csv, .xls ou .xlsx)
Arquivo exportado do SINFRA. Aceita separador **vírgula ou ponto-e-vírgula** (detecta sozinho).
O sistema procura a linha de cabeçalho com a coluna **Paciente**. Colunas usadas:

Especialidade · **Paciente** (formato "123456 - NOME") · Idade · Medico Solicitante ·
Unidade Solicitante · CID · **Data Cons.** (1ª consulta) · **Data Agendamento** (2ª consulta) ·
**Exame** · Data do Exame · Status OCI · Contatos Paciente.

---

## Como usar (passo a passo)

1. Abra o app (link do GitHub Pages — ver "Onde está hospedado").
2. **Passo 1**: arraste as planilhas do prestador.
3. **Passo 2**: arraste o relatório do SINFRA. O app abre a aba "SINFRA × Prestador".
4. Confira na tela; use a busca e os filtros (Todos / Encontrados / Não encontrados).
5. Clique em **Exportar XLSX** (ou CSV).

> **Download:** só funciona na versão hospedada (GitHub Pages) ou no arquivo aberto direto no
> navegador. Na pré-visualização do claude.ai os botões de download ficam bloqueados (limitação
> do ambiente) — lá serve só para ver.

---

## Colunas da planilha gerada

COD PACIENTE · PACIENTE · SITUACAO · QTD EXAMES NO PRESTADOR · IDADE · ESPECIALIDADE ·
MEDICO SOLICITANTE · UNIDADE SOLICITANTE · CID · **DATA 1ª CONSULTA** · **DATA 2ª CONSULTA** ·
EXAME (SINFRA) · **EXAMES REALIZADOS (PRESTADOR)** · DATA DO EXAME (SINFRA) · **DATA PRESTADOR** ·
STATUS OCI · CONTATOS.

Quando o paciente fez mais de um exame, os itens em EXAMES REALIZADOS e DATA PRESTADOR vêm
separados por " | ", na mesma ordem.

---

## Regras importantes (para lembrar)

- **Cruzamento por nome**, não por CPF/CNS (as planilhas do prestador não têm identificador).
  Nome grafado diferente nos dois sistemas cai como "Não encontrado" mesmo sendo a mesma pessoa.
- As planilhas do prestador são **de um mês**; o SINFRA costuma ter agendamentos de vários meses.
  Por isso muitos "Não encontrado" são apenas exames de outro mês (ou agendados para o futuro),
  não erro.
- Na aba auxiliar de SIGTAP: quando a planilha do prestador traz a coluna CODIGO, é esse código
  que vale; sem CODIGO, o sistema deduz pelo nome do procedimento.

---

## Onde está hospedado e como atualizar

- **App (uso real):** `index.html` hospedado no GitHub Pages (repositório crismelol-cloud.github.io).
- **Pré-visualização/compartilhamento:** link do claude.ai (downloads bloqueados lá).
- **Para atualizar:** substituir o `index.html` por uma versão nova (Upload files no GitHub).

## Códigos RX prioritários (OCI) — usados no destaque

02.04.02.003-4 · 02.04.02.004-2 · 02.04.02.007-7 · 02.04.02.008-5 · 02.04.02.009-3 ·
02.04.02.010-7 · 02.04.02.013-1 · 02.04.04.003-5 · 02.04.04.007-8 · 02.04.04.009-4 ·
02.04.04.011-6 · 02.04.04.012-4 · 02.04.06.006-0 · 02.04.06.009-5 · 02.04.06.010-9 ·
02.04.06.012-5 · 02.04.06.013-3 · 02.04.06.014-1 · 02.04.06.015-0 · 02.04.06.017-6.

(No app, gravados sem pontos: 0204020034, 0204020042, 0204020077, 0204020085, 0204020093,
0204020107, 0204020131, 0204040035, 0204040078, 0204040094, 0204040116, 0204040124, 0204060060,
0204060095, 0204060109, 0204060125, 0204060133, 0204060141, 0204060150, 0204060176.)

## Arquivos desta pasta

- `index.html` — o app completo e autocontido.
- `DOCUMENTACAO.md` — este guia.
