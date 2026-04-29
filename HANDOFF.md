# HANDOFF — Setlists PJ + EV

Snapshot de análise gerado em 2026-04-29, antes da formatação do PC.
Este documento descreve o projeto, suas dependências e como restaurá-lo
em qualquer máquina.

---

## 1. O que é

Site estático single-file que cataloga shows do Pearl Jam + Eddie Vedder
assistidos pelo dono do projeto. Mostra setlists, capas de álbuns,
posters oficiais, fotos pessoais e vídeos por show. Filtros por artista
e ano, lightbox de imagens, tema claro/escuro.

## 2. Estrutura de arquivos

```
setlists-pj-ev/
├── index.html              # 159 KB — app completo (HTML+CSS+JS+DADOS)
├── media-manifest.json     #   1 KB — referência humana do manifest
├── README.txt              # instruções de uso
├── HANDOFF.md              # este arquivo
└── media/                  # 25 MB total, 385 arquivos
    ├── albums/             # 12 capas de álbuns (ten.jpg, vs.jpg, ...)
    ├── pj-YYYY-MM-DD/      # uma pasta por show Pearl Jam
    │   ├── poster.jpg
    │   ├── poster-1.jpg, poster-2.jpg ...   (quando há múltiplos)
    │   ├── photo-N.jpg          # full size (~1200px)
    │   ├── photo-N-thumb.jpg    # miniatura (~400px)
    │   ├── mine/                # fotos pessoais (estrutura pronta, vazia hoje)
    │   └── videos/              # MP4s (estrutura pronta, vazia hoje)
    └── ev-YYYY-MM-DD/      # mesma estrutura para Eddie Vedder solo
```

## 3. Dependências

| Tipo                | Item                          | Status                 |
|---------------------|-------------------------------|------------------------|
| Runtime             | Browser moderno               | Qualquer Chromium/FF   |
| CDN externo         | Google Fonts (fonts.googleapis.com) | Opcional, tem fallbacks |
| Backend             | Nenhum                        | —                      |
| Build/bundler       | Nenhum                        | —                      |
| Banco de dados      | Nenhum                        | —                      |
| node_modules        | Não existe                    | —                      |
| Persistência local  | localStorage (apenas tema UI) | Não guarda conteúdo    |

**Caminhos:** todos relativos (`media/<show-id>/...`). Mover a pasta
para qualquer lugar funciona sem ajuste.

## 4. Como rodar

**Modo simples:** duplo clique em `index.html`.

**Se o browser bloquear por CORS** (raro, depende do browser):
```bash
cd setlists-pj-ev
python -m http.server 8000
# abrir http://localhost:8000
```

## 5. Onde os dados moram (importante para edições futuras)

Os shows, setlists, álbuns e o manifest de mídia estão **embutidos
inline em `index.html`** como objetos JS:

- `ALBUMS` — definido por volta da linha ~1545
- `SHOWS` (com setlists) — linha 1547 (objeto longo, ~21 KB)
- `MEDIA_MANIFEST` — linha 1595

O arquivo `media-manifest.json` é apenas uma cópia para leitura humana.
Para adicionar fotos/posters/vídeos a um show, **edite `index.html`**
(o objeto `MEDIA_MANIFEST`), não o JSON externo.

## 6. Convenções de mídia

- Foto oficial: `media/<show-id>/photo-N.jpg` + `photo-N-thumb.jpg`
- Poster único: `media/<show-id>/poster.jpg` (`poster: true` no manifest)
- Múltiplos posters: `poster-1.jpg`, `poster-2.jpg` ... (`posters: N`)
- Foto pessoal: `media/<show-id>/mine/photo-N.jpg` + thumb
- Vídeo pessoal: `media/<show-id>/videos/video-N.mp4`
- Capa de álbum: `media/albums/<albumId>.jpg`
  (ids válidos: ten, vs, vitalogy, nocode, yield, binaural, riotact,
   lostdogs, pj2006, backspacer, lightningbolt, darkmatter)

## 7. Estratégia de backup pré-formatação

Execute todas as camadas. Em ordem:

### 7.1 ZIP local
```bash
cd C:/Users/FourD/Downloads
# criar ZIP — use o Explorador do Windows (botão direito → Enviar para → Pasta compactada)
# ou via PowerShell:
powershell Compress-Archive -Path setlists-pj-ev -DestinationPath setlists-pj-ev-backup-2026-04-29.zip
```

### 7.2 Hash de integridade
```bash
# PowerShell:
Get-FileHash setlists-pj-ev-backup-2026-04-29.zip -Algorithm SHA256
# Anote o hash em outro lugar (papel, celular, e-mail)
```

### 7.3 Cópias redundantes (mínimo 2 destinos)
- [ ] HD externo / pendrive
- [ ] Google Drive
- [ ] OneDrive / Dropbox
- [ ] (Opcional) Repositório Git privado no GitHub

### 7.4 Restauração após formatar
1. Baixar o ZIP de uma das nuvens
2. Verificar hash SHA-256 — comparar com o anotado
3. Descompactar
4. Abrir `index.html` no browser — verificar se renderiza shows e fotos

## 8. Estado atual do conteúdo (snapshot 2026-04-29)

- **18 shows catalogados** com mídia (vide `MEDIA_MANIFEST`)
  - 17 Pearl Jam (2005, 2011, 2013, 2015, 2018, 2024)
  - 1 Eddie Vedder solo (2014)
- **12 capas de álbuns** em `media/albums/`
- **Fotos pessoais (`mine/`)** e **vídeos (`videos/`)** — diretórios
  criados mas ainda vazios em todos os shows.

## 9. O que NÃO está versionado

- Histórico de mudanças (não há `.git`)
- Lista de "shows desejados" futuros — só está na cabeça do dono
- Qualquer rascunho/anotação fora desta pasta

Recomendação forte: depois de restaurar pós-format, rodar
`git init && git add . && git commit -m "restore"` para ter histórico.

---

*Gerado por análise automatizada em 2026-04-29.*
