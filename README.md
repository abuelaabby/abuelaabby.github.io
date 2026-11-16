[index.html](https://github.com/user-attachments/files/34920741/index.html)
<!doctype html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<meta name="robots" content="noindex, nofollow">
<title>Libro de Abuela Abby</title>
<style>
  :root {
    --bg: #fbf7f1;
    --text: #2b2420;
    --muted: #7a6e66;
    --accent: #ff9900;
    --accent-text: #1a1a1a;
    --border: #e6ddd3;
  }
  * { box-sizing: border-box; }
  body {
    margin: 0;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    background: var(--bg);
    color: var(--text);
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
    padding: 24px 16px;
    text-align: center;
  }
  main { width: 100%; max-width: 360px; }
  h1 { font-size: 22px; margin: 0 0 8px; }
  p { margin: 0 0 24px; color: var(--muted); font-size: 15px; line-height: 1.4; }
  .btn {
    display: block;
    width: 100%;
    padding: 15px 16px;
    border-radius: 12px;
    font-size: 16px;
    font-weight: 600;
    text-decoration: none;
    margin-bottom: 12px;
  }
  .primary { background: var(--accent); color: var(--accent-text); }
  .secondary { background: transparent; color: var(--text); border: 1px solid var(--border); }
  small { display: block; margin-top: 20px; color: var(--muted); font-size: 12px; line-height: 1.4; }
</style>
</head>
<body>
<main>
  <h1>Abriendo Amazon…</h1>
  <p>Si no se abre solo, toca el botón.</p>
  <a id="app" class="btn primary" href="#">Abrir en la app de Amazon</a>
  <a id="web" class="btn secondary" href="#">Abrir en el navegador</a>
  <small>Como afiliada de Amazon, Abuela Abby gana una comisión por las compras que cumplen los requisitos.</small>
</main>

<script>
  // ===== Configuración: para otro producto, cambia solo estas dos líneas =====
  var ASIN = "B0GR4Q2LWC";
  var TAG = "abuelaabby-20";
  // ============================================================================

  var path = "www.amazon.com/dp/" + ASIN + "?tag=" + TAG;
  var webUrl = "https://" + path;

  var ua = navigator.userAgent || "";
  var isAndroid = /android/i.test(ua);
  var isIOS = /iphone|ipad|ipod/i.test(ua) ||
              (navigator.platform === "MacIntel" && navigator.maxTouchPoints > 1);

  var appUrl = webUrl;
  if (isAndroid) {
    // Abre la app de Amazon; si no está instalada, Android va solo a la web.
    appUrl = "intent://" + path +
      "#Intent;scheme=https;package=com.amazon.mShop.android.shopping;" +
      "S.browser_fallback_url=" + encodeURIComponent(webUrl) + ";end";
  } else if (isIOS) {
    appUrl = "com.amazon.mobile.shopping.web://" + path;
  }

  document.getElementById("app").href = appUrl;
  document.getElementById("web").href = webUrl;

  if (!isAndroid && !isIOS) {
    // Computadora: directo a la web de Amazon.
    window.location.replace(webUrl);
  } else {
    // Celular: intenta abrir la app automáticamente.
    // En iPhone no hay salto automático a la web, para no interrumpir
    // el cartel de "¿Abrir en Amazon?" que a veces muestra Instagram.
    window.location.href = appUrl;
  }
</script>
</body>
</html>
