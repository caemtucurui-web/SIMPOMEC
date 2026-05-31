# III SIMPOMEC 2026 — Sistema de Design
> Filho do sistema CAEM — mesmos tokens, expressão de evento

---

## Relação com o Sistema CAEM

Este site herda **todos os tokens** do sistema CAEM (`12 - Designer/CAEM/.interface-design/system.md`). As decisões de paleta, tipografia, espaçamento, raio e depth strategy são idênticas. O que difere é a **expressão**: o CAEM é sede permanente (placa de máquina), o SIMPOMEC é evento (cartaz de campeonato).

---

## Direção e Sensação

**Produto:** Site de evento acadêmico — III SIMPOMEC 2026.

**Quem abre:** Estudante de engenharia no celular, entre aulas, decidindo se se inscreve. Ou empresa avaliando patrocínio.

**Sensação alvo:** Cartaz que cola no corredor da faculdade e você para pra ler. Urgência de inscrição + prestígio acadêmico. Campeonato técnico, não feira institucional.

**Diferença intencional do CAEM:**
- CAEM → borders-only, frio, estático
- SIMPOMEC → hero com glow (evento tem calor), countdown como peça central, "III" como watermark estrutural

---

## Tokens (idênticos ao CAEM)

```css
--touro:   #8C2BBE;   /* accent principal */
--eixo:    #4B176E;   /* accent secundário */
--carbono: #08050D;   /* base */
--forja:   #100817;   /* superfície 1 */
--nucleo:  #16091F;   /* superfície 2 — cards */
--nucleo2: #1E0D2A;   /* superfície 3 — hover */
--aco:     #F6F4FA;   /* texto primário */
--prata:   #D8D7DE;   /* texto secundário */
--grafite: #787684;   /* texto terciário */
--sombra:  #3A3648;   /* texto quaternário */
--b1: rgba(140,43,190,0.10);
--b2: rgba(140,43,190,0.22);
--b3: rgba(140,43,190,0.45);
--ouro: #D4A843;  --prata2: #9BA4B5;  --bronze: #B87333;
```

---

## Signature do SIMPOMEC

### "III" como watermark estrutural
```css
.hero::after {
  content: 'III';
  position: absolute; left: 50%; top: 50%; transform: translate(-50%,-52%);
  font-family: 'Bebas Neue'; font-size: 40vw; line-height: 1;
  color: rgba(75,23,110,0.055);
  pointer-events: none; user-select: none;
}
```
Não é decoração — é a edição gravada permanentemente no evento.

### Countdown como painel de missão
```html
<div id="countdown">          <!-- border: --b2, background: rgba(carbono, 0.6) -->
  <div class="countdown-box"> <!-- min-width: 88px, padding: --s4 --s5 -->
    <span class="num" id="cd-d">--</span>   <!-- Bebas 48-72px -->
    <span class="unit">Dias</span>          <!-- 9px 700 caps -->
  </div>
  <!-- separador ":" via ::before em .countdown-box + .countdown-box -->
</div>
```
O countdown não é um widget pequeno — é a segunda hierarquia do hero.

### Tabs de programação (calendar day)
```html
<button class="prog-tab">
  <span class="dia-num">1</span>   <!-- Bebas 28px, --sombra → --touro when active -->
  <span class="dia-lbl">Dia 1</span>
</button>
```

### Stat-cards com accent bottom
```css
.stat-card::before {
  content: ''; position: absolute; bottom: 0; left: 0; right: 0;
  height: 2px; background: var(--touro);
}
```

---

## Componentes Específicos do SIMPOMEC

### Prog-item (linha de programação)
- `.prog-time` em Bebas 20px --touro, min-width 72px
- `.prog-type` como pill colorida por categoria

### Speaker-card
- Avatar 80px circular, border --b2
- Status: `.confirmed` (verde) ou `.tba` (muted)

### Sponsor tiers
- `.ouro` → --ouro, `.prata` → --prata2, `.bronze` → --bronze
- `.sponsor-slot` com border dashed --b2

### Radio-item (formulários)
- Background --forja, border --b1
- `:has(input:checked)` → border --b3, background rgba(touro, 0.06)

### File-drop
- Border dashed --b3
- `.has-file` → border verde, background rgba(green, 0.06)
- `.drag-over` → border --touro

---

## IDs críticos (não renomear — referenciados no JS)

| ID | Uso no JS |
|---|---|
| `countdown` | innerHTML substituído quando evento começa |
| `cd-d`, `cd-h`, `cd-m`, `cd-s` | `textContent` do countdown |
| `day-1` até `day-5` | Tabs de programação |
| `submit-btn` | disabled durante envio de inscrição |
| `artigo-submit-btn` | Botão de submissão de artigo |
| `inscricao-form` | Form listener async |
| `artigo-form` | Form com enctype multipart |
| `file-drop`, `pdf-input`, `file-drop-text` | Drag & drop PDF |
| `form-success` | `display:block` após envio OK |
| `nav-toggle`, `nav-links` | Mobile menu toggle |

## Classes críticas (usadas no JS)

`prog-day`, `prog-tab`, `active`, `open`, `has-file`, `drag-over`, `active-link`, `scrolled`

---

## Formulários (preservar ações)

| Form | Action | Backend |
|---|---|---|
| Inscrição | `https://formspree.io/f/xykvagky` | Formspree |
| Artigo PDF | `https://formsubmit.co/caemtucurui@gmail.com` | Formsubmit |

---

## Arquivos

```
SIMPOMEC/site/
  index.html
  portfolio.html
  .interface-design/system.md   ← este arquivo
  assets/
    logos/   logo-caem-roxo.png, logo-ufpa.png, logo-fem.png, logo-proex.jpg
```

**Repo:** https://github.com/caemtucurui-web/SIMPOMEC  
**Live:** https://caemtucurui-web.github.io/SIMPOMEC/
