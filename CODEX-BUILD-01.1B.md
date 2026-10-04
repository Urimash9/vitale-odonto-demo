# VITALE ODONTOLOGIA — BUILD 01.1B / INTEGRAÇÃO CONSERVADORA DE ASSETS

## FONTE DE VERDADE

Repositório: `Urimash9/vitale-odonto-demo`

Base visual obrigatória: `build-01-vitale-clean`

A referência visual aprovada é o `index.html` existente nessa branch antes da integração fotográfica agressiva do PR #2.

O PR #2 foi rejeitado visualmente e NÃO deve ser reutilizado como referência.

## REGRA PRINCIPAL

Nesta rodada, A FOTO DEVE SE ADAPTAR AO LAYOUT EXISTENTE.

O layout NÃO deve se adaptar à foto.

A Build 01 atual já tem:
- tipografia aprovada;
- ritmo vertical aprovado;
- proporções aprovadas;
- ordem das seções aprovada;
- grids aprovados;
- formas/máscaras aprovadas;
- comportamento mobile aprovado;
- distribuição de massas visuais aprovada.

A tarefa é SOMENTE substituir os slots visuais existentes por fotografias reais, preservando a composição original.

## NÃO ALTERAR

Não alterar:
- ordem das seções;
- grid principal;
- largura/altura/proporção dos slots;
- `aspect-ratio` dos slots;
- `clip-path` aprovado;
- tipografia;
- tamanhos tipográficos;
- paddings principais;
- gaps principais;
- alturas/min-heights das seções;
- alinhamentos estruturais;
- posição dos slots;
- composição desktop;
- composição tablet;
- composição mobile;
- SVG do percurso de tratamentos;
- header;
- pilares;
- tratamentos;
- prova social;
- localização;
- CTA final;
- footer;
- `checkpoint-vitale-base.html`.

Não reorganizar nada para acomodar fotografia.

## SANDBOX CODEX

A branch local pode se chamar `work` e pode não ter `origin`.

Isso NÃO bloqueia a tarefa.

Validar pelo conteúdo do checkout e pelos assets disponíveis.

## ASSETS REAIS DISPONÍVEIS

- `assets/images/vitale/hero-amanda.webp`
- `assets/images/vitale/amanda-portrait-bw.webp`
- `assets/images/vitale/amanda-clinical-action.webp`
- `assets/images/vitale/clinic-reception.webp`
- `assets/images/vitale/clinic-hall.webp`

## INTEGRAÇÃO OBRIGATÓRIA

### 01 — HERO

Slot existente: `data-asset-slot="hero-amanda"`

Usar:
`assets/images/vitale/hero-amanda.webp`

Preservar EXATAMENTE:
- tamanho do slot;
- posição do slot;
- `aspect-ratio`;
- `clip-path`;
- composição assimétrica;
- aro/lente;
- ripado ao fundo;
- posição relativa entre texto e imagem.

Não aumentar a fotografia.
Não mover o slot.
Não aumentar a coluna da imagem.
Não reduzir a área do texto.

Ajustar apenas:
- `object-fit: cover`;
- `object-position` por breakpoint, se necessário.

Hero:
- `loading="eager"`
- `fetchpriority="high"`
- alt: `Dra. Amanda Neves Barbosa na Vitale Odontologia`

### 02 — EXPERIÊNCIA VITALE

Slot existente: `data-asset-slot="clinic-reception"`

Usar:
`assets/images/vitale/clinic-reception.webp`

Preservar EXATAMENTE o arco/forma vertical e sua posição atual.

Não transformar a seção em outro layout.
Não ampliar a foto para competir com o título.
Não alterar o grid de três massas visuais.

Usar apenas `object-fit` e `object-position` para encaixar a fotografia no slot existente.

### 03 — DRA. AMANDA

Slot existente: `data-asset-slot="amanda-portrait"`

Usar:
`assets/images/vitale/amanda-portrait-bw.webp`

Preservar:
- máscara poligonal atual;
- tamanho atual do retrato;
- posição atual;
- aro decorativo;
- distância para o texto;
- proporção da seção.

Não transformar em card.
Não aumentar a fotografia.
Não redesenhar a seção.

### 04 — PRECISÃO EM CADA DETALHE

Slot existente: `data-asset-slot="amanda-clinical-action"`

Usar:
`assets/images/vitale/amanda-clinical-action.webp`

Preservar:
- fundo `#4B4036`;
- dimensão do slot;
- elipse/lente;
- posição relativa entre imagem e texto;
- distribuição atual da seção.

A foto deve entrar na forma já existente.
Não aumentar o slot.
Não mover o texto.
Não reduzir o espaço tipográfico.

Ajustar apenas crop e `object-position` para preservar rosto/microscópio.

### 05 — CLÍNICA

Usar:
`assets/images/vitale/clinic-hall.webp`

Inserir em UM dos slots já existentes da colagem, preferencialmente no slot principal mais adequado à proporção da imagem.

Não redesenhar a colagem.
Não alterar grid.
Não alterar tamanhos ou offsets.
Não duplicar a fotografia.

Os outros slots sem fotografia real devem continuar com o sistema gráfico original.

## SLOTS QUE CONTINUAM COMO PLACEHOLDER GRÁFICO

Manter o design original para:
- `result-01`;
- `result-02`;
- `clinic-detail`;
- `clinic-facade`;
- qualquer outro slot sem asset real correspondente.

Não usar banco de imagens.
Não usar Unsplash.
Não inventar pacientes.
Não inventar before/after.

## ESTADO FOTOGRÁFICO

Criar apenas o CSS mínimo necessário para inserir fotos dentro dos slots existentes.

Preferência:

```css
.asset--filled img {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}
```

A classe pode remover SOMENTE o texto automático/mark que ficar sobre a fotografia.

NÃO remover automaticamente:
- máscara;
- `clip-path`;
- moldura;
- aro;
- forma estrutural;
- elementos externos decorativos que pertencem ao layout.

Se `::before` fizer parte da moldura/identidade, preservar.

Não criar uma classe global que descaracterize todos os slots fotográficos.

## PRINCÍPIO DE CROP

Se uma foto não encaixar perfeitamente:
1. primeiro ajustar `object-position`;
2. depois avaliar `object-fit`;
3. somente em último caso reduzir discretamente o zoom da imagem DENTRO do slot.

Nunca mudar o layout para acomodar a fotografia.

## RESPONSIVIDADE

Preservar os breakpoints e a composição existente.

Testar:
- 1440;
- 1280;
- 1100;
- 1024;
- 920;
- 768;
- 430;
- 390;
- 360.

Em mobile, não reorganizar seções.
Apenas ajustar o crop dentro do slot existente quando necessário.

## PERFORMANCE

Hero:
- `loading="eager"`;
- `fetchpriority="high"`.

Demais imagens:
- `loading="lazy"`;
- `decoding="async"`.

Sem bibliotecas novas.
Sem framework novo.

## CHECKPOINT

`checkpoint-vitale-base.html` é congelado.

Ao final:

```bash
git diff -- checkpoint-vitale-base.html
```

Deve retornar vazio.

## TESTE VISUAL DE APROVAÇÃO

Depois da integração, faça esta pergunta:

"Se eu esconder as fotografias e recolocar os placeholders, o layout continua exatamente igual ao da Build 01 aprovada?"

Se a resposta for NÃO, a implementação alterou demais e deve ser revertida.

Outro teste:

"A fotografia está ocupando o slot ou está obrigando o layout a se reorganizar?"

A resposta correta é: A FOTOGRAFIA ESTÁ OCUPANDO O SLOT.

## COMMIT

Mensagem:

`Build 01.1B — integra assets sem alterar composição`

## ENTREGA

Pode trabalhar na branch local `work` do sandbox Codex.

Ao finalizar, usar o fluxo de publicação do Codex para criar branch/PR de saída.

Base obrigatória do PR:
`build-01-vitale-clean`

NUNCA `main`.

Não fazer merge automático.

Na resposta final informar:
1. hashes verificados;
2. cinco assets detectados;
3. onde cada asset foi inserido;
4. `object-position` por breakpoint;
5. confirmação de que dimensões, grid, tipografia, espaçamentos e ordem não mudaram;
6. confirmação de que `checkpoint-vitale-base.html` ficou intacto;
7. commit local;
8. branch/PR de saída, se criado.
