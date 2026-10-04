# VITALE ODONTOLOGIA — BUILD 01.1 / HANDOFF CODEX

## Ambiente obrigatório

- Repositório: `Urimash9/vitale-odonto-demo`
- Branch exclusiva: `build-01-vitale-clean`
- NÃO usar branch `work`
- NÃO criar nova branch
- NÃO abrir PR
- NÃO alterar `main`
- NÃO acessar `Urimash9/vitale-odontologia-demo`
- `checkpoint-vitale-base.html` é congelado e não deve ser modificado

## Antes de editar

Execute:

```bash
git remote -v
git branch --show-current
git rev-parse HEAD
git status --short
find assets/images/vitale -maxdepth 1 -type f | sort
```

O checkout correto precisa conter:

- `index.html`
- `checkpoint-vitale-base.html`
- `assets/images/vitale/hero-amanda.webp`
- `assets/images/vitale/amanda-portrait-bw.webp`
- `assets/images/vitale/amanda-clinical-action.webp`
- `assets/images/vitale/clinic-reception.webp`
- `assets/images/vitale/clinic-hall.webp`

Se esses arquivos não existirem, NÃO implemente sobre checkout antigo.

## Objetivo da Build 01.1

Não redesenhar a Home. Integrar os assets reais disponíveis e recalibrar composição, crop, `object-position`, proporções e responsividade.

### Hero

Integrar `assets/images/vitale/hero-amanda.webp` no slot `hero-amanda`.

- `loading="eager"`
- `fetchpriority="high"`
- alt: `Dra. Amanda Neves Barbosa na Vitale Odontologia`
- preservar headline, CTAs, assimetria e aro/lente
- crop separado para desktop/tablet/mobile

### Dra. Amanda

Integrar `assets/images/vitale/amanda-portrait-bw.webp` no slot `amanda-portrait`.

- alt: `Dra. Amanda Neves Barbosa`
- preservar caráter editorial
- ajustar máscara se o recorte real ficar ruim

### Precisão

Integrar `assets/images/vitale/amanda-clinical-action.webp` no slot `amanda-clinical-action`.

- alt: `Dra. Amanda Neves Barbosa durante atendimento odontológico`
- imagem deve reforçar a seção `Precisão em cada detalhe.`
- preservar fundo quente escuro `#4B4036`
- lente gráfica não pode cobrir microscópio ou rosto

### Clínica / Experiência

Usar com critério:

- `clinic-reception.webp`
- `clinic-hall.webp`

Evitar repetir a mesma foto em vários pontos apenas para preencher. Se recepção funcionar melhor em Experiência, usar ali; na Clínica, manter colagem editorial com corredor e placeholders gráficos elegantes para slots ainda ausentes.

## Slots ainda sem fotografia real

Manter sem inventar imagens:

- `clinic-detail`
- `clinic-facade`
- `result-01`
- `result-02`

Não usar banco de imagens, Unsplash, pacientes fictícios, before/after fictício ou avaliações inventadas.

## Estado fotográfico

Criar estado específico para containers com foto real (`.asset--photo` ou equivalente):

- remover fundo/gradiente de placeholder
- remover label automática sobre a foto
- remover `asset-mark` quando competir com fotografia
- preservar máscara/recorte quando funcionar

Base:

```css
.asset img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}
```

Cada foto precisa de `object-position` próprio.

Hero ≠ retrato Amanda ≠ microscópio ≠ clínica.

## Performance

Hero: `loading="eager"`, `fetchpriority="high"`.

Outras imagens: `loading="lazy"`, `decoding="async"`.

Sem bibliotecas ou frameworks novos.

## Não reinterpretar

Preservar estruturalmente:

- Header
- Pilares
- Percurso de Tratamentos
- Prova social
- Localização
- CTA final
- Footer

Ajustes de espaço são permitidos apenas quando necessários devido às fotos reais.

## Responsividade obrigatória

Testar:

- 1440
- 1280
- 1100
- 1024
- 920
- 768
- 430
- 390
- 360

Verificar principalmente crop, rosto cortado, `object-position`, overflow-x, proporção de imagem e ritmo vertical.

## Checkpoint

Ao final:

```bash
git diff -- checkpoint-vitale-base.html
```

Deve estar vazio.

## QA

Executar no mínimo:

```bash
git diff --check
```

Servir localmente e validar carregamento dos assets, links internos, WhatsApp, Instagram, Maps, menu mobile e ausência de overflow horizontal.

## Commit

Mensagem:

`Build 01.1 — integra assets reais e calibra composição`

Publicar somente em `origin build-01-vitale-clean`.

Se push/fetch falhar por proxy 403, não criar PR, não criar branch alternativa e não reutilizar checkout antigo. Manter commit local e relatar o hash.

## Critério de aprovação

A Home deve deixar de parecer uma composição conceitual com placeholders e começar a parecer realmente Vitale: Amanda como autoridade humana, arquitetura como acolhimento e ação clínica como precisão — mantendo originalidade, elegância e estabilidade.