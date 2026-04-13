<!DOCTYPE html>
<html lang="pt-BR">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Delícias Delivery Firebase</title>
  <style>
    :root{
      --bg:#f7f5ff;
      --card:#ffffff;
      --primary:#7c3aed;
      --primary-dark:#4c1d95;
      --green:#22c55e;
      --text:#1f1f1f;
      --muted:#6b7280;
      --border:#ece8ff;
      --soft:#f3e8ff;
      --chip:#f5f3ff;
      --shadow:0 10px 30px rgba(76,29,149,.10);
      --shadow-strong:0 20px 50px rgba(76,29,149,.18);
    }
    *{box-sizing:border-box}
    body{margin:0;font-family:Arial,Helvetica,sans-serif;background:linear-gradient(180deg,#f7f5ff 0%,#ffffff 100%);color:var(--text)}
    .topbar{background:rgba(255,255,255,.88);backdrop-filter:blur(10px);border-bottom:1px solid var(--border);position:sticky;top:0;z-index:50}
    .topbar-inner{max-width:1280px;margin:auto;padding:14px 18px;display:flex;align-items:center;justify-content:space-between;gap:16px;flex-wrap:wrap}
    .brand{display:flex;align-items:center;gap:14px;font-weight:800;font-size:24px;color:var(--primary)}
    .brand-badge{width:52px;height:52px;border-radius:18px;background:linear-gradient(135deg,#a78bfa,var(--primary-dark));color:#fff;display:grid;place-items:center;font-weight:900;box-shadow:0 10px 24px rgba(124,58,237,.28);font-size:22px}
    .brand-meta small{display:block;color:var(--muted);font-size:12px;font-weight:700;letter-spacing:.4px}
    .top-actions{display:flex;align-items:center;gap:10px;flex-wrap:wrap}
    .user-badge{background:var(--soft);color:var(--primary-dark);padding:10px 14px;border-radius:999px;font-size:14px;font-weight:700;border:1px solid #ddd6fe}
    .hero,.auth-wrap,.search-area,.container,.setup-wrap{max-width:1280px;margin:18px auto 0;padding:0 18px}
    .hero-banner{background:
      linear-gradient(135deg, rgba(139,92,246,.96) 0%, rgba(124,58,237,.95) 46%, rgba(76,29,149,.96) 100%),
      url('https://images.unsplash.com/photo-1504674900247-0877df9cc836?auto=format&fit=crop&w=1600&q=80') center/cover;
      color:#fff;border-radius:32px;padding:34px;box-shadow:var(--shadow-strong);position:relative;overflow:hidden;min-height:300px;display:flex;align-items:center}
    .hero-banner::after{content:"";position:absolute;right:-40px;top:-30px;width:220px;height:220px;background:rgba(255,255,255,.10);border-radius:50%}
    .hero-grid{display:grid;grid-template-columns:1.1fr .9fr;gap:20px;align-items:center;position:relative;z-index:1;width:100%}
    .hero-banner h1{margin:0 0 10px;font-size:clamp(30px,4vw,48px);line-height:1.05}
    .hero-banner p{margin:0;max-width:620px;line-height:1.55;color:#ede9fe;font-size:16px}
    .hero-meta{margin-top:18px;display:flex;gap:10px;flex-wrap:wrap}
    .meta-pill{background:rgba(255,255,255,.14);border:1px solid rgba(255,255,255,.16);padding:10px 14px;border-radius:999px;font-size:14px}
    .hero-card{justify-self:end;background:rgba(255,255,255,.12);border:1px solid rgba(255,255,255,.18);backdrop-filter:blur(6px);border-radius:24px;padding:18px;max-width:330px;box-shadow:0 10px 25px rgba(0,0,0,.12)}
    .hero-card h3{margin:0 0 8px;font-size:18px}
    .hero-card p{font-size:14px;color:#f3e8ff}
    .setup-card,.auth-card,.card{background:#fff;border:1px solid var(--border);border-radius:24px;box-shadow:var(--shadow)}
    .setup-card{padding:20px}
    .setup-card h3,.auth-card h3{margin:0 0 6px;font-size:22px;color:var(--primary-dark)}
    .setup-card p,.auth-card p{margin:0;color:var(--muted);font-size:14px;line-height:1.45}
    .setup-grid,.auth-wrap,.auth-grid,.admin-grid,.form-grid{display:grid;gap:10px}
    .auth-wrap{grid-template-columns:1.2fr .8fr}
    .auth-card{padding:22px}
    .auth-grid{grid-template-columns:1fr 1fr;margin-top:16px}
    .setup-grid{grid-template-columns:repeat(3,minmax(0,1fr));margin-top:16px}
    .full{grid-column:1/-1}
    .input,select,textarea{width:100%;border:1px solid var(--border);border-radius:16px;padding:14px 16px;font-size:15px;outline:none;background:#fff}
    .input:focus,select:focus,textarea:focus{border-color:#a78bfa;box-shadow:0 0 0 4px rgba(124,58,237,.10)}
    .search-box{background:#fff;border:1px solid var(--border);border-radius:22px;box-shadow:var(--shadow);padding:14px;display:grid;grid-template-columns:1.4fr .8fr;gap:12px}
    .container{margin:18px auto 32px;display:grid;grid-template-columns:1.6fr .95fr;gap:20px;align-items:start}
    .section-title{padding:22px 22px 8px;display:flex;justify-content:space-between;align-items:center;gap:12px;flex-wrap:wrap}
    .section-title h2{margin:0;font-size:24px}
    .section-title p{margin:4px 0 0;color:var(--muted);font-size:14px}
    .chips{padding:0 22px 18px;display:flex;gap:10px;flex-wrap:wrap}
    .chip{background:var(--chip);border:1px solid transparent;padding:10px 14px;border-radius:999px;font-weight:700;color:#4b5563;cursor:pointer}
    .chip.active{background:var(--soft);color:var(--primary-dark);border:1px solid #d8b4fe}
    .grid{padding:0 22px 22px;display:grid;grid-template-columns:repeat(3,minmax(0,1fr));gap:16px}
    .produto{border:1px solid var(--border);border-radius:22px;background:#fff;overflow:hidden;display:flex;flex-direction:column;transition:.2s ease}
    .produto:hover{transform:translateY(-4px);box-shadow:0 16px 28px rgba(76,29,149,.10)}
    .produto-top{height:190px;background:linear-gradient(135deg,#f3e8ff,#ddd6fe);display:grid;place-items:center;font-size:46px;font-weight:800;color:var(--primary-dark);position:relative;overflow:hidden}
    .produto-top img{width:100%;height:100%;object-fit:cover;display:block}
    .produto-top::after{content:"Destaque";position:absolute;top:12px;left:12px;background:#fff;color:var(--primary-dark);font-size:12px;font-weight:800;padding:7px 10px;border-radius:999px;border:1px solid #ddd6fe;z-index:2}
    .produto-body{padding:16px;display:flex;flex-direction:column;gap:10px;flex:1}
    .produto-title{display:flex;justify-content:space-between;gap:8px;align-items:flex-start}
    .produto h3{margin:0;font-size:18px;line-height:1.3}
    .categoria-tag{background:var(--soft);color:var(--primary-dark);font-size:12px;font-weight:700;padding:6px 10px;border-radius:999px;white-space:nowrap;border:1px solid #ddd6fe}
    .desc{color:var(--muted);font-size:14px;line-height:1.45;min-height:42px}
    .price-row{margin-top:auto;display:flex;justify-content:space-between;align-items:center;gap:10px}
    .price{font-size:24px;font-weight:800;color:var(--primary-dark)}
    .btn{border:none;border-radius:14px;padding:12px 14px;font-weight:800;cursor:pointer;transition:.2s ease}
    .btn:hover{transform:translateY(-1px)}
    .btn-primary{background:var(--primary);color:#fff}.btn-primary:hover{background:var(--primary-dark)}
    .btn-soft{background:#f3f4f6;color:#111827}.btn-success{background:linear-gradient(135deg,var(--primary),var(--primary-dark));color:#fff}
    .btn-danger{background:#ef4444;color:#fff}.btn-warning{background:#f59e0b;color:#fff}.btn-outline{background:#fff;color:var(--primary-dark);border:1px solid #d8b4fe}.btn-info{background:#06b6d4;color:#fff}
    .side{display:grid;gap:18px;position:sticky;top:88px}.cart,.admin{padding:20px}
    .cart-list,.admin-list{list-style:none;padding:0;margin:14px 0 0;display:grid;gap:12px}
    .cart-item{border:1px solid var(--border);border-radius:18px;padding:14px;background:#faf8ff}
    .cart-top{display:flex;justify-content:space-between;gap:10px;align-items:flex-start}
    .cart-name{font-weight:800}.cart-price{font-size:14px;color:var(--muted);margin-top:4px}
    .qtd-controls{display:flex;justify-content:space-between;align-items:center;gap:10px;margin-top:12px;flex-wrap:wrap}
    .stepper{display:flex;align-items:center;gap:8px}.stepper button{width:34px;height:34px;border:none;background:#ede9fe;color:var(--primary-dark);border-radius:10px;font-size:18px;font-weight:800;cursor:pointer}
    .summary{background:#f8f5ff;border:1px solid #ddd6fe;border-radius:20px;padding:16px;margin-top:16px;display:grid;gap:10px}
    .summary-line{display:flex;justify-content:space-between;gap:10px;color:#374151}.summary-line.total{border-top:1px solid #ddd6fe;padding-top:10px;font-size:21px;color:var(--primary-dark);font-weight:800}
    .admin-grid{grid-template-columns:1fr 1fr}.admin-list li{border:1px solid var(--border);border-radius:16px;padding:12px;display:grid;gap:10px;background:#fff}
    .admin-product-top{display:flex;justify-content:space-between;gap:10px;align-items:flex-start;flex-wrap:wrap}.admin-actions{display:flex;gap:8px;flex-wrap:wrap}
    .admin-thumb{width:100%;max-width:90px;height:70px;border-radius:12px;object-fit:cover;border:1px solid var(--border);background:#f3e8ff}
    .admin-lock,.recover-box,.status-box{background:#faf8ff;border:1px dashed #c4b5fd;border-radius:18px;padding:16px;color:var(--muted);line-height:1.5;margin-top:14px}
    .status-box strong{color:var(--primary-dark)}
    .pill{font-size:12px;color:#fff;padding:6px 10px;border-radius:999px;font-weight:700}.on{background:var(--green)}.off{background:#ef4444}
    .empty{text-align:center;color:var(--muted);padding:24px 12px}.footer-note{text-align:center;font-size:12px;color:var(--muted);margin-top:10px}.hidden{display:none !important}
    @media (max-width:1024px){.hero-grid,.setup-grid,.auth-wrap,.container{grid-template-columns:1fr}.side{position:static}.grid{grid-template-columns:repeat(2,minmax(0,1fr))}.hero-card{justify-self:start;max-width:none}}
    @media (max-width:720px){.auth-grid,.search-box,.admin-grid,.setup-grid{grid-template-columns:1fr}.grid{grid-template-columns:1fr}.topbar-inner{padding:12px 14px}.hero,.setup-wrap,.auth-wrap,.search-area,.container{padding-left:14px;padding-right:14px}.hero-banner{padding:22px;min-height:auto}.section-title,.chips,.grid{padding-left:16px;padding-right:16px}}
  </style>
</head>
<body>
  <header class="topbar">
    <div class="topbar-inner">
      <div class="brand">
        <div class="brand-badge">DE</div>
        <div class="brand-meta">
          <span>Delícias Delivery</span>
          <small>DELIVERY PREMIUM</small>
        </div>
      </div>
      <div class="top-actions">
        <div id="clienteStatus" class="user-badge">Cliente não conectado</div>
        <div id="adminStatus" class="user-badge">Admin offline</div>
      </div>
    </div>
  </header>

  <section class="hero">
    <div class="hero-banner">
      <div class="hero-grid">
        <div>
          <h1>Sabor caseiro, entrega rápida e visual profissional</h1>
          <p>Seu delivery com cara de aplicativo grande, cadastro real com Firebase, painel administrativo online e cardápio bonito para vender mais.</p>
          <div class="hero-meta">
            <span class="meta-pill">🍽️ Pratos regionais</span>
            <span class="meta-pill">🥤 Bebidas geladas</span>
            <span class="meta-pill">⚡ Pedido no WhatsApp</span>
          </div>
        </div>
        <div class="hero-card">
          <h3>Cardápio em destaque</h3>
          <p>Arroz com Galinha, Vatapá, Torta Salgada, Lasanha e bebidas geladas como Coca-Cola, Fanta Uva, Fanta Laranja e Guaraná.</p>
        </div>
      </div>
    </div>
  </section>

  <section class="setup-wrap">
    <div class="setup-card">
      <h3>Configuração do Firebase</h3>
      <p>Cole as chaves do seu app web e defina o e-mail do administrador. Depois publique no Netlify.</p>
      <div class="setup-grid">
        <input id="firebaseApiKey" class="input" placeholder="apiKey" />
        <input id="firebaseAuthDomain" class="input" placeholder="authDomain" />
        <input id="firebaseProjectId" class="input" placeholder="projectId" />
        <input id="firebaseStorageBucket" class="input" placeholder="storageBucket" />
        <input id="firebaseMessagingSenderId" class="input" placeholder="messagingSenderId" />
        <input id="firebaseAppId" class="input" placeholder="appId" />
        <input id="adminEmailConfig" class="input full" placeholder="E-mail do administrador" />
        <button class="btn btn-primary full" onclick="salvarConfiguracaoFirebase()">Salvar configuração</button>
      </div>
      <div id="firebaseStatus" class="status-box">Firebase ainda não configurado.</div>
    </div>
  </section>

  <section class="auth-wrap">
    <div class="auth-card">
      <h3>Área do cliente</h3>
      <p>Cadastre-se ou entre com conta real do Firebase.</p>
      <div class="auth-grid">
        <input id="cadNome" class="input" placeholder="Nome completo" />
        <input id="cadTelefone" class="input" placeholder="Telefone" />
        <input id="cadEmail" class="input full" placeholder="E-mail" />
        <input id="cadSenha" class="input" type="password" placeholder="Crie uma senha" />
        <input id="cadEndereco" class="input" placeholder="Endereço" />
        <button class="btn btn-success" onclick="cadastrarCliente()">Cadastrar cliente</button>
        <button class="btn btn-outline" onclick="loginCliente()">Entrar cliente</button>
        <button class="btn btn-soft full" onclick="recuperarSenhaCliente()">Recuperar senha por e-mail</button>
      </div>
      <div id="senhaRecuperada" class="recover-box hidden"></div>
    </div>

    <div class="auth-card">
      <h3>Login do administrador</h3>
      <p>Use o e-mail admin configurado acima e a senha criada no Firebase Authentication.</p>
      <div class="auth-grid">
        <input id="adminUser" class="input full" placeholder="E-mail do administrador" />
        <input id="adminSenha" class="input full" type="password" placeholder="Senha do administrador" />
        <button id="btnAdminLogin" class="btn btn-primary full" onclick="loginAdmin()">Entrar como administrador</button>
        <button id="btnAdminLogout" class="btn btn-soft full hidden" onclick="logoutAdmin()">Sair do administrador</button>
      </div>
      <div class="footer-note">Neste modelo, o admin é controlado pelo e-mail definido na configuração.</div>
    </div>
  </section>

  <section class="search-area">
    <div class="search-box">
      <input id="busca" class="input" placeholder="Buscar pratos, bebidas e combos" oninput="render()" />
      <select id="filtroCategoria" onchange="render()">
        <option value="">Todas as categorias</option>
      </select>
    </div>
  </section>

  <main class="container">
    <section class="card">
      <div class="section-title">
        <div>
          <h2>Cardápio</h2>
          <p>Produtos carregados do Firestore.</p>
        </div>
      </div>
      <div id="chipsCategorias" class="chips"></div>
      <div id="produtos" class="grid"></div>
    </section>

    <aside class="side">
      <section class="card cart">
        <div class="section-title" style="padding:0 0 8px">
          <div>
            <h2>Seu carrinho</h2>
            <p>Confira seus itens antes de enviar.</p>
          </div>
        </div>
        <ul id="carrinho" class="cart-list"></ul>
        <div class="summary">
          <div class="summary-line"><span>Subtotal</span><strong id="subtotal">R$ 0,00</strong></div>
          <div class="summary-line"><span>Entrega</span><strong id="taxaEntrega">R$ 5,00</strong></div>
          <div class="summary-line total"><span>Total</span><strong id="total">R$ 0,00</strong></div>
        </div>
        <div class="form-grid">
          <input id="nome" class="input" placeholder="Seu nome" />
          <input id="endereco" class="input" placeholder="Endereço completo" />
          <input id="telefone" class="input" placeholder="Telefone" />
          <select id="pagamento"><option>Pix</option><option>Dinheiro</option><option>Cartão</option></select>
          <textarea id="observacao" rows="3" placeholder="Alguma observação do pedido?"></textarea>
          <button class="btn btn-success" onclick="finalizar()">Enviar pedido no WhatsApp</button>
          <button class="btn btn-soft" onclick="limparCarrinho()">Limpar carrinho</button>
        </div>
        <div class="footer-note">Troque o número do WhatsApp no código pelo seu número.</div>
      </section>

      <section class="card admin">
        <div class="section-title" style="padding:0 0 8px">
          <div>
            <h2>Painel admin</h2>
            <p>Produtos salvos diretamente no Firebase.</p>
          </div>
        </div>
        <div id="adminPainel" class="hidden">
          <div class="admin-grid">
            <input id="novoNome" class="input" placeholder="Nome do produto" />
            <input id="novoPreco" class="input" placeholder="Preço" />
            <input id="novaCategoria" class="input" placeholder="Categoria" />
            <input id="novaDescricao" class="input" placeholder="Descrição curta" />
            <input id="novaImagem" class="input full" placeholder="URL da imagem do produto" />
            <div class="full" style="display:flex; gap:10px; flex-wrap:wrap;">
              <button id="btnSalvarProduto" class="btn btn-primary" style="flex:1" onclick="addOuAtualizarProduto()">Adicionar produto</button>
              <button id="btnCancelarEdicao" class="btn btn-soft hidden" style="flex:1" onclick="cancelarEdicao()">Cancelar edição</button>
            </div>
          </div>
          <ul id="listaAdmin" class="admin-list"></ul>
        </div>
        <div id="adminBloqueado" class="admin-lock">Faça login como administrador para liberar a gestão online dos produtos.</div>
      </section>
    </aside>
  </main>

  <script type="module">
    import { initializeApp } from "https://www.gstatic.com/firebasejs/10.12.5/firebase-app.js";
    import {
      getAuth,
      createUserWithEmailAndPassword,
      signInWithEmailAndPassword,
      sendPasswordResetEmail,
      signOut,
      onAuthStateChanged,
      updateProfile
    } from "https://www.gstatic.com/firebasejs/10.12.5/firebase-auth.js";
    import {
      getFirestore,
      doc,
      setDoc,
      getDoc,
      addDoc,
      updateDoc,
      deleteDoc,
      collection,
      onSnapshot,
      query,
      orderBy,
      getDocs
    } from "https://www.gstatic.com/firebasejs/10.12.5/firebase-firestore.js";

    const WHATSAPP_NUMERO = "559198312053";
    const TAXA_ENTREGA = 5;
    const NOME_LOJA = "Delícias Delivery";
    const NOME_LOJA_UPPER = "DELÍCIAS DELIVERY";

    const PRODUTOS_INICIAIS = [
      { nome:"Arroz com Galinha", preco:18, categoria:"Pratos", descricao:"Prato regional bem servido e muito saboroso.", imagem:"https://images.unsplash.com/photo-1512058564366-18510be2db19?auto=format&fit=crop&w=900&q=80", ativo:true },
      { nome:"Vatapá", preco:16, categoria:"Pratos", descricao:"Sabor marcante, cremoso e caseiro.", imagem:"https://images.unsplash.com/photo-1544025162-d76694265947?auto=format&fit=crop&w=900&q=80", ativo:true },
      { nome:"Torta Salgada", preco:10, categoria:"Lanches", descricao:"Leve, saborosa e ideal para o lanche.", imagem:"https://images.unsplash.com/photo-1464306076886-da185f6a9d05?auto=format&fit=crop&w=900&q=80", ativo:true },
      { nome:"Lasanha", preco:20, categoria:"Massas", descricao:"Massa cremosa e gratinada no ponto certo.", imagem:"https://images.unsplash.com/photo-1619895092538-128341789043?auto=format&fit=crop&w=900&q=80", ativo:true },
      { nome:"Coca-Cola", preco:7, categoria:"Bebidas", descricao:"Refrigerante gelado para acompanhar seu pedido.", imagem:"https://images.unsplash.com/photo-1624517452488-04869289c4ca?auto=format&fit=crop&w=900&q=80", ativo:true },
      { nome:"Fanta Uva", preco:7, categoria:"Bebidas", descricao:"Refrigerante gelado com sabor de uva.", imagem:"https://images.unsplash.com/photo-1581006852262-e4307cf6283a?auto=format&fit=crop&w=900&q=80", ativo:true },
      { nome:"Fanta Laranja", preco:7, categoria:"Bebidas", descricao:"Refrigerante gelado com sabor de laranja.", imagem:"https://images.unsplash.com/photo-1513558161293-cdaf765ed2fd?auto=format&fit=crop&w=900&q=80", ativo:true },
      { nome:"Guaraná", preco:7, categoria:"Bebidas", descricao:"Guaraná bem gelado para completar a refeição.", imagem:"https://images.unsplash.com/photo-1544145945-f90425340c7e?auto=format&fit=crop&w=900&q=80", ativo:true }
    ];

    let firebaseApp = null, auth = null, db = null, produtos = [], carrinho = [], categoriaChipAtiva = "", clienteLogado = null, adminLogado = false, editandoProdutoId = null, firebaseReady = false, unsubscribeProdutos = null;
    const configSalva = JSON.parse(localStorage.getItem("deliveryFirebaseConfig") || "null");

    function formatarMoeda(valor){ return Number(valor || 0).toLocaleString("pt-BR", { style:"currency", currency:"BRL" }); }
    function atualizarStatusFirebase(texto){ document.getElementById("firebaseStatus").innerHTML = texto; }

    function preencherConfigSalva(){
      if(!configSalva) return;
      document.getElementById("firebaseApiKey").value = configSalva.apiKey || "";
      document.getElementById("firebaseAuthDomain").value = configSalva.authDomain || "";
      document.getElementById("firebaseProjectId").value = configSalva.projectId || "";
      document.getElementById("firebaseStorageBucket").value = configSalva.storageBucket || "";
      document.getElementById("firebaseMessagingSenderId").value = configSalva.messagingSenderId || "";
      document.getElementById("firebaseAppId").value = configSalva.appId || "";
      document.getElementById("adminEmailConfig").value = configSalva.adminEmail || "";
      document.getElementById("adminUser").value = configSalva.adminEmail || "";
    }

    window.salvarConfiguracaoFirebase = async function(){
      const config = {
        apiKey: document.getElementById("firebaseApiKey").value.trim(),
        authDomain: document.getElementById("firebaseAuthDomain").value.trim(),
        projectId: document.getElementById("firebaseProjectId").value.trim(),
        storageBucket: document.getElementById("firebaseStorageBucket").value.trim(),
        messagingSenderId: document.getElementById("firebaseMessagingSenderId").value.trim(),
        appId: document.getElementById("firebaseAppId").value.trim(),
        adminEmail: document.getElementById("adminEmailConfig").value.trim().toLowerCase()
      };
      if(!config.apiKey || !config.authDomain || !config.projectId || !config.appId || !config.adminEmail) return alert("Preencha pelo menos apiKey, authDomain, projectId, appId e e-mail do administrador.");
      localStorage.setItem("deliveryFirebaseConfig", JSON.stringify(config));
      atualizarStatusFirebase(`<strong>Configuração salva.</strong><br>Recarregando a página...`);
      location.reload();
    }

    function atualizarStatusTopo(){
      document.getElementById("clienteStatus").textContent = clienteLogado ? `Cliente: ${clienteLogado.nome || clienteLogado.email}` : "Cliente não conectado";
      document.getElementById("adminStatus").textContent = adminLogado ? "Admin online" : "Admin offline";
    }

    function atualizarAreaAdmin(){
      document.getElementById("adminPainel").classList.toggle("hidden", !adminLogado);
      document.getElementById("adminBloqueado").classList.toggle("hidden", adminLogado);
      document.getElementById("btnAdminLogin").classList.toggle("hidden", adminLogado);
      document.getElementById("btnAdminLogout").classList.toggle("hidden", !adminLogado);
      atualizarStatusTopo();
    }

    function preencherClienteNoCarrinho(){
      if(!clienteLogado) return;
      document.getElementById("nome").value = clienteLogado.nome || "";
      document.getElementById("telefone").value = clienteLogado.telefone || "";
      document.getElementById("endereco").value = clienteLogado.endereco || "";
      document.getElementById("cadNome").value = clienteLogado.nome || "";
      document.getElementById("cadTelefone").value = clienteLogado.telefone || "";
      document.getElementById("cadEmail").value = clienteLogado.email || "";
      document.getElementById("cadEndereco").value = clienteLogado.endereco || "";
    }

    async function semearProdutosIniciais(){
      const snap = await getDocs(collection(db, "produtos"));
      if(!snap.empty) return;
      for (const produto of PRODUTOS_INICIAIS) await addDoc(collection(db, "produtos"), produto);
    }

    async function initFirebase(){
      if(!configSalva){ atualizarStatusFirebase("Firebase ainda não configurado. Cole suas chaves acima para ativar cadastro e produtos online."); return; }
      try {
        firebaseApp = initializeApp({
          apiKey: configSalva.apiKey,
          authDomain: configSalva.authDomain,
          projectId: configSalva.projectId,
          storageBucket: configSalva.storageBucket,
          messagingSenderId: configSalva.messagingSenderId,
          appId: configSalva.appId
        });
        auth = getAuth(firebaseApp);
        db = getFirestore(firebaseApp);
        firebaseReady = true;
        atualizarStatusFirebase(`<strong>Firebase conectado.</strong><br>Projeto: ${configSalva.projectId}<br>Admin: ${configSalva.adminEmail}`);
        await semearProdutosIniciais();
        onAuthStateChanged(auth, async (user) => {
          if(user){
            const perfilRef = doc(db, "clientes", user.uid);
            const perfilSnap = await getDoc(perfilRef);
            const perfil = perfilSnap.exists() ? perfilSnap.data() : {};
            clienteLogado = {
              uid: user.uid,
              nome: perfil.nome || user.displayName || "Cliente",
              telefone: perfil.telefone || "",
              endereco: perfil.endereco || "",
              email: user.email || ""
            };
            adminLogado = (user.email || "").toLowerCase() === (configSalva.adminEmail || "").toLowerCase();
          } else {
            clienteLogado = null;
            adminLogado = false;
          }
          preencherClienteNoCarrinho();
          atualizarAreaAdmin();
        });
        if(unsubscribeProdutos) unsubscribeProdutos();
        const produtosQuery = query(collection(db, "produtos"), orderBy("nome"));
        unsubscribeProdutos = onSnapshot(produtosQuery, (snapshot) => {
          produtos = snapshot.docs.map(docItem => ({ id: docItem.id, ...docItem.data() }));
          render();
        });
      } catch(error) {
        atualizarStatusFirebase(`<strong>Erro ao conectar Firebase:</strong><br>${error.message}`);
      }
    }

    window.cadastrarCliente = async function(){
      if(!firebaseReady) return alert("Configure o Firebase primeiro.");
      const nome = document.getElementById("cadNome").value.trim();
      const telefone = document.getElementById("cadTelefone").value.trim();
      const email = document.getElementById("cadEmail").value.trim().toLowerCase();
      const senha = document.getElementById("cadSenha").value.trim();
      const endereco = document.getElementById("cadEndereco").value.trim();
      if(!nome || !telefone || !email || !senha || !endereco) return alert("Preencha todos os campos do cadastro do cliente.");
      try {
        const cred = await createUserWithEmailAndPassword(auth, email, senha);
        await updateProfile(cred.user, { displayName: nome });
        await setDoc(doc(db, "clientes", cred.user.uid), { nome, telefone, email, endereco, criadoEm: new Date().toISOString() });
        alert("Cliente cadastrado com sucesso no Firebase.");
      } catch(error) { alert(error.message); }
    }

    window.loginCliente = async function(){
      if(!firebaseReady) return alert("Configure o Firebase primeiro.");
      const email = document.getElementById("cadEmail").value.trim().toLowerCase();
      const senha = document.getElementById("cadSenha").value.trim();
      if(!email || !senha) return alert("Digite e-mail e senha.");
      try { await signInWithEmailAndPassword(auth, email, senha); alert("Login do cliente realizado com sucesso."); } catch(error) { alert(error.message); }
    }

    window.recuperarSenhaCliente = async function(){
      if(!firebaseReady) return alert("Configure o Firebase primeiro.");
      const email = document.getElementById("cadEmail").value.trim().toLowerCase();
      const box = document.getElementById("senhaRecuperada");
      if(!email) return alert("Digite seu e-mail para recuperar a senha.");
      try {
        await sendPasswordResetEmail(auth, email);
        box.innerHTML = `<strong>E-mail enviado.</strong><br>Verifique sua caixa de entrada para redefinir a senha.`;
        box.classList.remove("hidden");
      } catch(error) { alert(error.message); }
    }

    window.loginAdmin = async function(){
      if(!firebaseReady) return alert("Configure o Firebase primeiro.");
      const email = document.getElementById("adminUser").value.trim().toLowerCase();
      const senha = document.getElementById("adminSenha").value.trim();
      if(email !== (configSalva.adminEmail || "").toLowerCase()) return alert("Esse e-mail não é o administrador configurado.");
      try { await signInWithEmailAndPassword(auth, email, senha); alert("Administrador conectado com sucesso."); } catch(error) { alert(error.message); }
    }

    window.logoutAdmin = async function(){ if(!firebaseReady) return; await signOut(auth); cancelarEdicao(); alert("Sessão encerrada."); }

    function popularCategorias(){
      const select = document.getElementById("filtroCategoria");
      const categoriaAtual = select.value;
      const categorias = [...new Set(produtos.map(p => p.categoria).filter(Boolean))].sort();
      select.innerHTML = '<option value="">Todas as categorias</option>';
      categorias.forEach(cat => { select.innerHTML += `<option value="${cat}">${cat}</option>`; });
      select.value = categoriaChipAtiva || categoriaAtual;
      const chips = document.getElementById("chipsCategorias");
      chips.innerHTML = `<button class="chip ${!categoriaChipAtiva ? 'active' : ''}" onclick="selecionarCategoria('')">Todos</button>` + categorias.map(cat => `<button class="chip ${categoriaChipAtiva === cat ? 'active' : ''}" onclick="selecionarCategoria('${cat.replace(/'/g,"\'")}')">${cat}</button>`).join('');
    }

    window.selecionarCategoria = function(cat){ categoriaChipAtiva = cat; document.getElementById("filtroCategoria").value = cat; render(); }

    function renderProdutoTopo(produto){
      if(produto.imagem) return `<img src="${produto.imagem}" alt="${produto.nome}" onerror="this.remove()">`;
      return (produto.nome || "P").charAt(0).toUpperCase();
    }

    function render(){
      popularCategorias();
      const busca = document.getElementById("busca").value.toLowerCase().trim();
      const categoria = categoriaChipAtiva || document.getElementById("filtroCategoria").value;
      const div = document.getElementById("produtos");
      const filtrados = produtos.filter(p => {
        const okAtivo = p.ativo !== false;
        const okBusca = (p.nome || "").toLowerCase().includes(busca) || (p.descricao || "").toLowerCase().includes(busca) || (p.categoria || "").toLowerCase().includes(busca);
        const okCategoria = !categoria || p.categoria === categoria;
        return okAtivo && okBusca && okCategoria;
      });
      div.innerHTML = !filtrados.length
        ? '<div class="empty card" style="grid-column:1/-1">Nenhum produto encontrado.</div>'
        : filtrados.map(p => `
          <div class="produto">
            <div class="produto-top">${renderProdutoTopo(p)}</div>
            <div class="produto-body">
              <div class="produto-title">
                <h3>${p.nome}</h3>
                <span class="categoria-tag">${p.categoria || 'Geral'}</span>
              </div>
              <div class="desc">${p.descricao || 'Produto disponível no cardápio.'}</div>
              <div class="price-row">
                <div class="price">${formatarMoeda(p.preco)}</div>
                <button class="btn btn-primary" onclick="addCarrinho('${p.id}')">Adicionar</button>
              </div>
            </div>
          </div>`).join('');

      if(adminLogado){
        document.getElementById("listaAdmin").innerHTML = produtos.map(p => `
          <li>
            <div class="admin-product-top">
              <div style="display:flex; gap:12px; align-items:center; flex:1; min-width:0;">
                <img class="admin-thumb" src="${p.imagem || 'data:image/svg+xml;utf8,<svg xmlns=\"http://www.w3.org/2000/svg\" width=\"180\" height=\"140\"><rect width=\"100%25\" height=\"100%25\" fill=\"%23ede9fe\"/><text x=\"50%25\" y=\"54%25\" dominant-baseline=\"middle\" text-anchor=\"middle\" font-size=\"24\" fill=\"%234c1d95\">IMG</text></svg>'}" alt="${p.nome}">
                <div>
                  <strong>${p.nome}</strong><br>
                  <small>${p.categoria || 'Sem categoria'} • ${formatarMoeda(p.preco)}</small><br>
                  <small>${p.descricao || 'Sem descrição'}</small>
                </div>
              </div>
              <span class="pill ${p.ativo !== false ? 'on' : 'off'}">${p.ativo !== false ? 'Disponível' : 'Indisponível'}</span>
            </div>
            <div class="admin-actions">
              <button class="btn ${p.ativo !== false ? 'btn-warning' : 'btn-success'}" onclick="toggle('${p.id}')">${p.ativo !== false ? 'Desativar' : 'Ativar'}</button>
              <button class="btn btn-info" onclick="editarProduto('${p.id}')">Editar</button>
              <button class="btn btn-danger" onclick="excluirProduto('${p.id}')">Excluir</button>
            </div>
          </li>`).join('');
      }
      updateCarrinho();
    }

    window.addCarrinho = function(id){
      const produto = produtos.find(p => p.id === id && p.ativo !== false);
      if(!produto) return;
      const existente = carrinho.find(item => item.id === id);
      if(existente) existente.qtd += 1; else carrinho.push({ ...produto, qtd:1 });
      updateCarrinho();
    }

    window.alterarQtd = function(id, delta){
      const item = carrinho.find(p => p.id === id);
      if(!item) return;
      item.qtd += delta;
      if(item.qtd <= 0) carrinho = carrinho.filter(p => p.id !== id);
      updateCarrinho();
    }
    window.limparCarrinho = function(){ carrinho = []; updateCarrinho(); }
    window.removerItem = function(id){ carrinho = carrinho.filter(p => p.id !== id); updateCarrinho(); }

    function updateCarrinho(){
      const ul = document.getElementById("carrinho");
      ul.innerHTML = !carrinho.length
        ? '<li class="empty">Seu carrinho está vazio.</li>'
        : carrinho.map(item => `
          <li class="cart-item">
            <div class="cart-top"><div><div class="cart-name">${item.nome}</div><div class="cart-price">${formatarMoeda(item.preco)} cada</div></div><strong>${formatarMoeda(item.preco * item.qtd)}</strong></div>
            <div class="qtd-controls">
              <div class="stepper"><button onclick="alterarQtd('${item.id}', -1)">−</button><strong>${item.qtd}</strong><button onclick="alterarQtd('${item.id}', 1)">+</button></div>
              <button class="btn btn-danger" onclick="removerItem('${item.id}')">Remover</button>
            </div>
          </li>`).join('');
      const subtotal = carrinho.reduce((acc, item) => acc + Number(item.preco) * item.qtd, 0);
      const total = subtotal > 0 ? subtotal + TAXA_ENTREGA : 0;
      document.getElementById("subtotal").innerText = formatarMoeda(subtotal);
      document.getElementById("taxaEntrega").innerText = subtotal > 0 ? formatarMoeda(TAXA_ENTREGA) : formatarMoeda(0);
      document.getElementById("total").innerText = formatarMoeda(total);
    }

    window.finalizar = function(){
      const nome = document.getElementById("nome").value.trim();
      const endereco = document.getElementById("endereco").value.trim();
      const telefone = document.getElementById("telefone").value.trim();
      const pagamento = document.getElementById("pagamento").value;
      const observacao = document.getElementById("observacao").value.trim();
      if(carrinho.length === 0) return alert("Adicione pelo menos 1 item no carrinho.");
      if(!nome || !endereco || !telefone) return alert("Preencha nome, endereço e telefone.");
      const subtotal = carrinho.reduce((acc, item) => acc + Number(item.preco) * item.qtd, 0);
      const total = subtotal + TAXA_ENTREGA;
      const itens = carrinho.map(item => `- ${item.nome} (x${item.qtd}) = ${formatarMoeda(item.preco * item.qtd)}`).join("\n");
      const msg = `*NOVO PEDIDO - ${NOME_LOJA_UPPER}*\n\n*Cliente:* ${nome}\n*Telefone:* ${telefone}\n*Endereço:* ${endereco}\n\n*Itens do pedido:*\n${itens}\n\n*Subtotal:* ${formatarMoeda(subtotal)}\n*Taxa de entrega:* ${formatarMoeda(TAXA_ENTREGA)}\n*Total:* ${formatarMoeda(total)}\n*Pagamento:* ${pagamento}\n*Observação:* ${observacao || 'Sem observações'}`;
      window.open(`https://wa.me/${WHATSAPP_NUMERO}?text=${encodeURIComponent(msg)}`, "_blank");
    }

    function limparFormularioProduto(){
      document.getElementById("novoNome").value = "";
      document.getElementById("novoPreco").value = "";
      document.getElementById("novaCategoria").value = "";
      document.getElementById("novaDescricao").value = "";
      document.getElementById("novaImagem").value = "";
    }

    window.cancelarEdicao = function(){
      editandoProdutoId = null;
      limparFormularioProduto();
      document.getElementById("btnSalvarProduto").textContent = "Adicionar produto";
      document.getElementById("btnCancelarEdicao").classList.add("hidden");
    }

    window.editarProduto = function(id){
      const produto = produtos.find(p => p.id === id);
      if(!produto) return;
      editandoProdutoId = id;
      document.getElementById("novoNome").value = produto.nome || "";
      document.getElementById("novoPreco").value = produto.preco || "";
      document.getElementById("novaCategoria").value = produto.categoria || "";
      document.getElementById("novaDescricao").value = produto.descricao || "";
      document.getElementById("novaImagem").value = produto.imagem || "";
      document.getElementById("btnSalvarProduto").textContent = "Salvar alterações";
      document.getElementById("btnCancelarEdicao").classList.remove("hidden");
    }

    window.excluirProduto = async function(id){
      if(!firebaseReady || !adminLogado) return alert("Faça login como administrador.");
      const produto = produtos.find(p => p.id === id);
      if(!produto) return;
      if(!confirm(`Deseja excluir o produto "${produto.nome}"?`)) return;
      try {
        await deleteDoc(doc(db, "produtos", id));
        carrinho = carrinho.filter(item => item.id !== id);
        if(editandoProdutoId === id) cancelarEdicao();
      } catch(error) { alert(error.message); }
    }

    window.addOuAtualizarProduto = async function(){
      if(!firebaseReady || !adminLogado) return alert("Faça login como administrador.");
      const nome = document.getElementById("novoNome").value.trim();
      const preco = parseFloat(document.getElementById("novoPreco").value.replace(",", "."));
      const categoria = document.getElementById("novaCategoria").value.trim() || "Geral";
      const descricao = document.getElementById("novaDescricao").value.trim();
      const imagem = document.getElementById("novaImagem").value.trim();
      if(!nome || isNaN(preco) || preco <= 0) return alert("Informe nome e preço válidos.");
      try {
        const payload = { nome, preco, categoria, descricao, imagem, ativo:true };
        if(editandoProdutoId){
          const original = produtos.find(p => p.id === editandoProdutoId);
          await updateDoc(doc(db, "produtos", editandoProdutoId), { ...payload, ativo: original?.ativo !== false });
          carrinho = carrinho.map(item => item.id === editandoProdutoId ? { ...item, ...payload, ativo: original?.ativo !== false } : item);
        } else {
          await addDoc(collection(db, "produtos"), payload);
        }
        cancelarEdicao();
      } catch(error) { alert(error.message); }
    }

    window.toggle = async function(id){
      if(!firebaseReady || !adminLogado) return alert("Faça login como administrador.");
      const produto = produtos.find(p => p.id === id);
      if(!produto) return;
      try {
        await updateDoc(doc(db, "produtos", id), { ativo: !(produto.ativo !== false) });
        if(produto.ativo !== false) carrinho = carrinho.filter(item => item.id !== id);
      } catch(error) { alert(error.message); }
    }

    preencherConfigSalva();
    atualizarAreaAdmin();
    atualizarStatusTopo();
    render();
    initFirebase();
  </script>
</body>
</html>
