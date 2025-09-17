
<html lang="pt-BR">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />

  <link rel="stylesheet" href="style.css">
</head>
<body>
  <header>
    <div class="brand">
      <div class="logo" aria-hidden="true"></div>
      <div>
        <h1>O Pequeno Príncipe</h1>
        <div class="description">Projeto com foco em literatura e acessibilidade digital</div>
      </div>
    </div>
    <nav aria-label="Menu principal">
      <button class="btn" id="open-a11y" aria-haspopup="true" aria-controls="a11y-title">
        Menu de Acessibilidade
      </button>
    </nav>
  </header>

  <main id="main">
    <div class="grid">
      <section class="card">
        <div class="section">
          <h3>Sobre o livro</h3>
          <p><strong>O Pequeno Príncipe</strong> foi escrito por <em>Antoine de Saint-Exupéry</em>, publicado em 1943. É uma das obras literárias mais traduzidas do mundo e traz reflexões sobre amizade, amor, responsabilidade e o olhar inocente da infância.</p>
        </div>
        <div class="section">
          <h3>Sobre o filme</h3>
          <p>Em 2015, foi lançado o filme <em>O Pequeno Príncipe</em>, dirigido por Mark Osborne. A animação mistura técnicas de stop-motion e 3D, trazendo a história para um novo público, mas mantendo a essência poética e filosófica da obra original.</p>
        </div>
        <div class="section">
          <h3>Principais Temas</h3>
          <ul>
            <li>A amizade verdadeira.</li>
            <li>A importância de olhar com o coração.</li>
            <li>A responsabilidade pelos laços que criamos.</li>
            <li>A valorização da simplicidade.</li>
          </ul>
        </div>
      </section>
      <aside class="card" aria-labelledby="a11y-title">
        <h2 id="a11y-title">Menu de Acessibilidade</h2>
        <div class="a11y">
          <p class="muted">Personalize a interface: tamanho da fonte, contraste e movimentos.</p>
          <div>
            <label for="font-size-range">Tamanho da fonte</label>
            <div class="controls">
              <button class="btn" id="decrease-font" aria-label="Diminuir fonte">A-</button>
              <input id="font-size-range" type="range" min="12" max="22" step="1" value="16">
              <button class="btn" id="increase-font" aria-label="Aumentar fonte">A+</button>
            </div>
          </div>
          <div>
            <label for="contrast-toggle">Modo alto contraste</label>
            <div class="controls">
              <button class="btn" id="toggle-contrast" aria-pressed="false">Ativar contraste</button>
            </div>
          </div>
          <div>
            <label for="motion-toggle">Reduzir movimentos</label>
            <div class="controls">
              <button class="btn" id="toggle-motion" aria-pressed="false">Reduzir animações</button>
            </div>
          </div>
          <div>
            <button class="btn" id="reset" aria-label="Restaurar padrões">Restaurar padrões</button>
          </div>
        </div>
      </aside>
    </div>
  </main>

  <div class="aria-status" aria-live="polite" id="a11y-status"></div>

  <footer>
    <small>© Projeto O Pequeno Príncipe — Inspirado na obra de Antoine de Saint-Exupéry</small>
  </footer>

  <script>
    const root = document.documentElement;
    const range = document.getElementById('font-size-range');
    const inc = document.getElementById('increase-font');
    const dec = document.getElementById('decrease-font');
    const toggleContrast = document.getElementById('toggle-contrast');
    const resetBtn = document.getElementById('reset');
    const status = document.getElementById('a11y-status');
    const toggleMotion = document.getElementById('toggle-motion');

    function announce(msg){ status.textContent = msg; }

    function setFontSize(size){
      root.style.setProperty('--base-font', size + 'px');
      range.value = size;
      announce('Tamanho da fonte: ' + size + 'px');
    }
    inc.addEventListener('click', ()=> setFontSize(Math.min(Number(range.max), Number(range.value)+1)));
    dec.addEventListener('click', ()=> setFontSize(Math.max(Number(range.min), Number(range.value)-1)));
    range.addEventListener('input', (e)=> setFontSize(e.target.value));

    function setContrast(on){
      if(on){
        document.body.classList.add('high-contrast');
        toggleContrast.textContent = 'Desativar contraste';
        toggleContrast.setAttribute('aria-pressed','true');
        announce('Contraste ativado');
      } else {
        document.body.classList.remove('high-contrast');
        toggleContrast.textContent = 'Ativar contraste';
        toggleContrast.setAttribute('aria-pressed','false');
        announce('Contraste desativado');
      }
    }
    toggleContrast.addEventListener('click', ()=> setContrast(toggleContrast.getAttribute('aria-pressed')!=='true'));

    function setMotion(on){
      if(on){
        document.documentElement.style.setProperty('scroll-behavior','auto');
        toggleMotion.textContent = 'Animações reduzidas';
        toggleMotion.setAttribute('aria-pressed','true');
        announce('Movimentos reduzidos');
      } else {
        document.documentElement.style.removeProperty('scroll-behavior');
        toggleMotion.textContent = 'Reduzir animações';
        toggleMotion.setAttribute('aria-pressed','false');
        announce('Movimentos normais');
      }
    }
    toggleMotion.addEventListener('click', ()=> setMotion(toggleMotion.getAttribute('aria-pressed')!=='true'));

    resetBtn.addEventListener('click', ()=>{
      setFontSize(16);
      setContrast(false);
      setMotion(false);
      announce('Preferências restauradas');
    });
  </script>
</body>
</html>
