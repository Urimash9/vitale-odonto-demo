# VITALE ODONTOLOGIA — BUILD 01.1 / HANDOFF CODEX

## REGRA PRINCIPAL

Este arquivo foi escrito especificamente para o ambiente isolado do Codex.

O Codex pode abrir o checkout local em uma branch sintética chamada `work` e sem `remote` configurado. ISSO É NORMAL e não deve bloquear a tarefa.

NÃO exigir que `git branch --show-current` retorne `build-01-vitale-clean`.
NÃO exigir `origin` local.
NÃO tentar trocar de branch apenas por o checkout se chamar `work`.

A fonte de verdade é o CONTEÚDO do checkout recebido.

## Repositório de origem

`Urimash9/vitale-odonto-demo`

## Branch de destino no GitHub

`build-01-vitale-clean`

A `main` é somente base/checkpoint e NÃO deve receber esta Build 01.1.

NÃO acessar o repositório legado:

`Urimash9/vitale-odontologia-demo`

## Verificação correta do snapshot

Antes de editar, execute:

```bash
git status --short --branch
pwd
ls -la
find assets/images/vitale -maxdepth 1 -type f | sort

git hash-object index.html
git hash-object checkpoint-vitale-base.html
git hash-object assets/images/vitale/hero-amanda.webp
git hash-object assets/images/vitale/amanda-portrait-bw.webp
git hash-object assets/images/vitale/amanda-clinical-action.webp
git hash-object assets/images/vitale/clinic-reception.webp
git hash-object assets/images/vitale/clinic-hall.webp
```

O snapshot correto deve conter os seguintes blobs:

- `index.html` → `ded4c2ac272923a51abc31dd9ce4a2c0f336fcca`
- `checkpoint-vitale-base.html` → `355ac9a130214bfad104b20e190c5333790b432e`
- `hero-amanda.webp` → `1d47a9da4da46828bf76d14fce61874e53d1b912`
- `amanda-portrait-bw.webp` → `b7631a09ceb68209ebbcef5b124e2001a8490219`
- `amanda-clinical-action.webp` → `5cfb98c1268ec25f7926afe0ba9ec646d28be887`
- `clinic-reception.webp` → `c79359733d0977b620a09dfb2033cbb172c313b8`
- `clinic-hall.webp` → `c5f31c532c230864c0656d1cf4646822182d69a3`

Se esses arquivos e hashes coincidirem, o checkout é o correto MESMO QUE:

- a branch local se chame `work`;
- `git remote -v` esteja vazio;
- `git rev-parse HEAD` seja diferente do SHA remoto;
- o ambiente não consiga fazer `fetch`.

Nesses casos, CONTINUE A IMPLEMENTAÇÃO.

Pare apenas se os arquivos obrigatórios ou seus blobs não corresponderem ao snapshot acima.

## Objetivo da Build 01.1

Não redesenhar a Home.

Integrar os assets reais já presentes no checkout e recalibrar:

- composição;
- crop;
- `object-position`;
- proporções;
- ritmo vertical;
- responsividade.

## Assets reais

### Hero

`assets/images/vitale/hero-amanda.webp`

Substituir o slot `hero-amanda`.

- usar `<img>` real;
- `loading="eager"`;
- `fetchpriority="high"`;
- alt: `Dra. Amanda Neves Barbosa na Vitale Odontologia`;
- preservar headline, CTAs, assimetria e aro/lente;
- calibrar crop separadamente em desktop/tablet/mobile.

### Dra. Amanda

`assets/images/vitale/amanda-portrait-bw.webp`

Substituir o slot `amanda-portrait`.

- alt: `Dra. Amanda Neves Barbosa`;
- preservar caráter editorial;
- ajustar máscara se o recorte real ficar ruim;
- não transformar em card de equipe.

### Precisão

`assets/images/vitale/amanda-clinical-action.webp`

Substituir o slot `amanda-clinical-action`.

- alt: `Dra. Amanda Neves Barbosa durante atendimento odontológico`;
- a imagem deve reforçar `Precisão em cada detalhe.`;
- preservar fundo `#4B4036`;
- lente gráfica não pode cobrir rosto/microscópio.

### Experiência / Clínica

Usar com critério:

- `assets/images/vitale/clinic-reception.webp`
- `assets/images/vitale/clinic-hall.webp`

Evitar duplicar a mesma foto apenas para preencher espaço.

Preferência inicial:

- recepção → seção Experiência Vitale;
- corredor → seção Clínica.

Os demais slots de clínica continuam como elementos gráficos temporários até recebermos os assets reais.

## Slots ainda sem fotografia real

Não inventar imagens para:

- `clinic-detail`;
- `clinic-facade`;
- `result-01`;
- `result-02`.

Não usar Unsplash, banco de imagens ou fotos externas.

## Estado fotográfico

Criar uma classe específica para containers com fotografia, por exemplo `.asset--photo`.

Quando houver foto real:

- remover gradiente de placeholder;
- remover label automática de placeholder;
- remover `asset-mark` se competir com a foto;
- preservar apenas máscara/forma que realmente favoreça a composição.

Usar:

```css
.asset--photo img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}
```

Definir `object-position` INDIVIDUALMENTE para cada imagem.

## Performance

Hero:

- `loading="eager"`;
- `fetchpriority="high"`.

Demais fotos:

- `loading="lazy"`;
- `decoding="async"`.

Não adicionar biblioteca ou framework.

## Seções que NÃO devem ser redesenhadas

Preservar arquitetura da Build 01 em:

- Header;
- Pilares;
- Tratamentos;
- Prova social;
- Localização;
- CTA final;
- Footer.

Ajustes de espaçamento são permitidos apenas quando necessários após a entrada das fotos.

## Tratamentos

Preservar o percurso clínico e o SVG orgânico.

Não transformar em cards.

## Responsividade

Validar:

- 1440;
- 1280;
- 1100;
- 1024;
- 920;
- 768;
- 430;
- 390;
- 360.

Atenção especial a:

- rostos cortados;
- `object-position`;
- máscara estranha;
- imagem esmagada;
- whitespace excessivo;
- texto invadindo fotografia;
- `overflow-x`.

## Checkpoint

`checkpoint-vitale-base.html` é congelado.

NÃO modificar.

Ao final:

```bash
git diff -- checkpoint-vitale-base.html
```

Deve retornar vazio.

## Testes

Executar ao menos:

```bash
git diff --check
```

Também verificar:

- HTML estrutural;
- carregamento dos cinco assets;
- ausência de 404;
- links internos;
- WhatsApp;
- Instagram;
- Maps;
- menu mobile;
- ausência de overflow horizontal.

Se navegador automatizado não estiver disponível, isso NÃO bloqueia a entrega.

## Commit no sandbox Codex

É permitido e esperado criar commit na branch local `work` do ambiente Codex.

Mensagem:

`Build 01.1 — integra assets reais e calibra composição`

O nome `work` é apenas o sandbox local e não é problema.

## Como devolver a alteração ao GitHub

Como o sandbox pode não possuir `remote`, NÃO tente forçar `push` manual se não houver origin.

Após concluir a implementação, use o fluxo de entrega do próprio Codex para criar uma branch/PR de saída.

O PR DEVE TER COMO BASE:

`build-01-vitale-clean`

NUNCA usar `main` como base.

O PR é apenas o transporte da alteração do sandbox para o GitHub.

NÃO fazer merge automaticamente.

Após o PR ser criado, ele será revisado antes do merge.

## Entrega final

Informar:

1. branch local do sandbox encontrada;
2. hashes dos arquivos-base verificados;
3. cinco assets detectados;
4. assets integrados;
5. crops / `object-position` adotados;
6. placeholders restantes;
7. ajustes desktop/tablet/mobile;
8. checkpoint intacto;
9. testes executados;
10. hash do commit local;
11. PR criado apontando para `build-01-vitale-clean`, se o fluxo do Codex estiver disponível.

## Critério final

A Build 01.1 deve transformar a página de uma composição com placeholders em uma primeira versão realmente visual da Vitale, sem redesenhar a Build 01.

Amanda = autoridade humana.

Arquitetura = acolhimento.

Imagem clínica = precisão.

ORIGINALIDADE + ELEGÂNCIA + ESTABILIDADE.
