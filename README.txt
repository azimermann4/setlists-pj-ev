═══════════════════════════════════════════════════════════
  PEARL JAM + EDDIE VEDDER — ARQUIVO DE SHOWS
═══════════════════════════════════════════════════════════

COMO USAR:
  Duplo clique em index.html. Abre no browser.
  (Se o browser bloquear por CORS, use Firefox ou abra via
   servidor local: python -m http.server 8000)

ESTRUTURA DE PASTAS:
  index.html
  media/
    <show-id>/                  ex: pj-2011-11-06
      poster.jpg                arte oficial pearljam.com
      photo-1.jpg               fotos oficiais full size (~1200px)
      photo-1-thumb.jpg         fotos oficiais miniatura (~400px)
      photo-2.jpg ...
      mine/                     SUAS fotos pessoais
        photo-1.jpg             (mesma convenção de nomes)
        photo-1-thumb.jpg
        photo-2.jpg ...
      videos/                   SEUS vídeos
        video-1.mp4
        video-2.mp4

═══════════════════════════════════════════════════════════
  COMO ADICIONAR SUAS FOTOS PESSOAIS
═══════════════════════════════════════════════════════════

Passo 1 — Coloque suas fotos originais numa pasta temporária
Passo 2 — Mande elas pro Claude e diga de qual show são
         (ele organiza, cria thumbnails e otimiza)

Aparecerão no drawer do show numa seção destacada
"★ Minhas fotos", com borda âmbar diferenciada das oficiais.

═══════════════════════════════════════════════════════════
  COMO ADICIONAR VÍDEOS
═══════════════════════════════════════════════════════════

MP4 funciona direto (HTML5 video). Coloque em:
  media/<show-id>/videos/video-1.mp4
  media/<show-id>/videos/video-2.mp4

Não precisa converter. Aparecerão como players controláveis
na seção "★ Meus vídeos".

═══════════════════════════════════════════════════════════

Indicadores no card do show:
  📷  tem fotos oficiais
  ★   tem fotos pessoais suas
  ▶   tem vídeos
