<p align="center">
  <img src="assets/icon-256.png" width="120" alt="Ícone do projeto Nota SAP">
</p>

<h1 align="center">Nota SAP — Solicitação de Manutenção</h1>

<p align="center">
  Formulário web (HTML + Tailwind CSS + JS puro, sem dependências de build) para gerar notas de
  solicitação de manutenção industrial no formato de texto usado internamente, com validação de
  campos, cálculo automático de custos e sugestão de tempo total com base nas horas de mão de obra.
</p>

<p align="center">
  <a href="https://github.com/allanrein">
    <img alt="autor" src="https://img.shields.io/badge/autor-Allan%20Rein-1c2228?style=flat-square">
  </a>
  <img alt="stack" src="https://img.shields.io/badge/stack-HTML%20%2B%20Tailwind%20%2B%20JS-f2a71b?style=flat-square">
  <img alt="dependências" src="https://img.shields.io/badge/build-nenhum%20necessário-45c17c?style=flat-square">
</p>

---

## ✨ O que o formulário faz

- Reproduz, campo a campo, o padrão de nota SAP usado na manutenção (avaria, trabalho a executar,
  tag em bloqueio, mão de obra interna/externa, recursos e horas, NRs obrigatórias, materiais,
  ferramentas e histórico).
- Ao clicar em **Gerar nota**, monta o texto final exatamente no formato esperado, **omitindo por
  completo** qualquer seção, linha ou item que não tenha sido preenchido (nada de `...` ou campos
  em branco poluindo a nota).
- Botões para **copiar** o texto gerado ou **baixar como `.txt`**.
- Sem back-end, sem build, sem npm install — é um único arquivo HTML que roda em qualquer navegador.

## 🧩 Principais recursos

| Recurso | Descrição |
|---|---|
| **Mão de obra interna/externa** | Uma linha só entra na nota se a **Quantidade** estiver preenchida (horas/serviço sozinhos não bastam). |
| **Sugestão de Tempo Total** | Calcula, em tempo real, o **maior valor de horas** informado entre toda a mão de obra e oferece um botão para preencher o campo Tempo Total com um clique (o valor continua editável depois). |
| **Recursos / Horas** | Cada recurso (Andaime, Munck, Guindaste, Lift, Empilhadeira, Usinagem/Conserto Externo) só aparece na nota se o checkbox estiver marcado — mesmo que os campos extras estejam preenchidos. |
| **Condição da linha do Andaime** | Campo de escolha única (PPG / FUN) embutido na mesma linha do Andaime, ao lado de "Quant. de pontos". |
| **NRs Obrigatórias** | Só entram na nota as NRs efetivamente marcadas. |
| **Materiais (com e sem cadastro)** | Linhas repetíveis via botão **+ Adicionar material** (com remoção individual). Cada item tem Código/ID, Descrição, **Custo Unit.** e Quantidade. |
| **Custo automático** | A nota calcula `Custo Unit. × Quantidade = Custo Total` por item e soma tudo em `*CUSTO TOTAL ESTIMADO DE MATERIAIS*` no final. |
| **Código SAP flexível** | Aceita códigos numéricos puros (`833531`) ou iniciados pela letra **S** (`S12345`); qualquer outro caractere é filtrado automaticamente. |
| **Validação numérica** | Todos os campos numéricos (quantidade, horas, pontos, toneladas, custo, tempo total) bloqueiam caracteres inválidos e destacam em vermelho valores fora do permitido. |
| **Pronto para integração** | `coletarDados()` expõe um objeto JSON estruturado (`window.__ultimaNota`) com todos os campos, pronto para ser enviado a qualquer back-end (`fetch('/api/notas', { method: 'POST', body: JSON.stringify(dados) })`) e persistido em banco de dados. |

## 📂 Estrutura do repositório

```
.
├── nota_sap_manutencao.html   # aplicação (abra direto no navegador)
├── assets/
│   ├── icon.svg                # ícone/logo em vetor
│   ├── icon-512.png            # ícone em alta resolução
│   ├── icon-256.png            # ícone usado no README / apple-touch-icon
│   ├── favicon-32.png          # favicon
│   └── favicon-64.png          # favicon (tela retina)
└── README.md
```

> 💡 Para publicar com **GitHub Pages**, basta renomear `nota_sap_manutencao.html` para `index.html`
> e ativar o Pages nas configurações do repositório (branch `main`, pasta raiz).

## 🚀 Como usar

1. Baixe ou clone o repositório.
2. Abra `nota_sap_manutencao.html` em qualquer navegador (precisa de internet, pois o Tailwind CSS
   e as fontes são carregados via CDN).
3. Preencha os campos relevantes.
4. Clique em **Gerar nota** — o texto aparece no painel inferior, pronto para copiar ou baixar.

## 🔧 Stack técnica

- **HTML5** semântico, acessível (labels, `aria-label`, `fieldset`/`legend`).
- **Tailwind CSS** via CDN — nenhuma etapa de build necessária.
- **JavaScript puro (vanilla)** — sem frameworks, sem dependências de terceiros.
- Fontes **IBM Plex Sans / IBM Plex Mono** via Google Fonts.

## 📊 Analytics (Google Analytics 4)

O site já vem com o **Google Analytics 4 configurado e ativo** em `nota_sap_manutencao.html`,
apontando para a propriedade `G-7GN1BN0DCT`. Nenhuma configuração adicional é necessária — basta
publicar o arquivo.

Além da visualização de página padrão, o formulário dispara três eventos personalizados que
aparecem em **Relatórios → Engajamento → Eventos** no GA4:

| Evento | Quando dispara |
|---|---|
| `gerar_nota` | Ao clicar em **Gerar nota** |
| `copiar_nota` | Ao copiar o texto com sucesso |
| `baixar_nota` | Ao baixar o arquivo `.txt` |

Se o script do GA for bloqueado (ad-blocker) ou o ID não for configurado, o formulário continua
funcionando normalmente — o rastreamento falha em silêncio sem afetar a geração da nota.

## 📝 Histórico de atualizações

- **Formulário inicial** — campos fiéis ao modelo original da nota SAP (avaria, trabalho, mão de
  obra interna/externa, recursos, materiais, ferramentas), com geração de texto e correção de bug
  de submissão nativa do `<form>` que impedia a nota de aparecer em alguns visualizadores.
- **Materiais dinâmicos** — botão **+ Adicionar material** com remoção individual de linhas, tanto
  em "Material com Cadastro" quanto "Material sem Cadastro"; adicionado campo Descrição.
- **Atualização de layout da nota** — novos campos (Tag em Bloqueio, Brigadista, Empresa
  Especializada, Contratar Pacote, Condição da linha do Andaime, Toneladas, NRs Obrigatórias,
  Histórico); remoção de Civil e Pintor da mão de obra externa.
- **Omissão inteligente de campos vazios** — NRs não marcadas, recursos não flegados e seções sem
  nenhum dado preenchido somem completamente da nota gerada (sem `...` ou linhas em branco).
- **Reformulação visual completa em Tailwind CSS**, mantendo toda a lógica de geração intacta, com
  rodapé de crédito ao autor.
- **Condição da linha do Andaime** movida para dentro da mesma linha de "Quant. de pontos".
- **Campo Custo Unit.** adicionado aos materiais, com cálculo automático de custo total por item e
  custo total geral da nota.
- **Sugestão de Tempo Total** baseada no maior valor de horas informado na mão de obra (não a soma).
- **Otimização de altura da página** (menos espaçamento vertical, mesma fonte) e limpeza de textos
  de apoio; campo "N° da ID" renomeado de *Struxure* para **Solicitação**.
- **Código SAP** passou a aceitar códigos iniciados pela letra **S**; formato dos materiais na nota
  reorganizado em duas linhas (Código/Descrição/Quantidade e, abaixo, Custo Unit./Custo Total).
- **Ícone do projeto e README** adicionados.
- **Google Analytics (GA4)** integrado, com eventos personalizados para "Gerar nota", "Copiar" e
  "Baixar .txt".

## 👤 Autor

Desenvolvido por **[Allan Rein](https://github.com/allanrein)**.
