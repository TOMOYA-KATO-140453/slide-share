# インフォグラフィックHTMLスライドひな形

---

## 1. スライド全体構成（カラム・行の可変対応）

- `.slide-container`内の`.content`は**1～4カラム**まで可変
  - カラム数は`.column`の数で調整（1～4個までOK）
  - 各カラム内に**1～4行**（`.row`）を配置可能
- カラム幅は`flex`で**比率可変**（例: 1:1, 1:2, 1:5, 2:1:1:2 など）
  - 各`.column`に`flex`スタイルで比率指定
  - 例: `<div class="column" style="flex:5">...</div>`（5/6幅）
- 行数も`.row`で柔軟に増減可能
  - 例: 1カラム4行、2カラム2行ずつ、3カラム1行ずつなど

---

## 1.1 カラーコードの取り決め

| 色        | HEX      | 用途例                      |
|-----------|----------|-----------------------------|
| Cyan      | #00A9E0  | メインカラー、強調、枠線等  |
| Gray      | #2D2D2D  | 文字色、アイコン等           |
| Light Gray| #F4F4F4  | 背景、カード背景等           |
| White     | #FFFFFF  | カード・スライド背景         |
| Magenta   | #DA1884  | Aチーム、強調               |
| Purple    | #8031A7  | 最終課題、強調              |
| Turquoise | #00B2A9  | Hチーム、強調               |
| Green     | #78BE20  | 教育・技術伝承、強調         |
| Yellow    | #EEDD00  | 注意、業務プロセス           |
| Orange    | #FF6A13  | サーベイ、アンケート         |

> **スタイル指定例（CSS）**  
> `.icon-cyan { background: #00A9E0; color: #fff; }`  
> `.icon-magenta { background: #DA1884; color: #fff; }`  
> ...など、index.htmlのスタイルを参照

---

## 2. HTMLひな形（カラム・行可変/比率可変/カラー指定）

```html
<!-- filepath: slideTemplate2.html -->
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=1600, initial-scale=1.0">
  <title>スライドタイトル</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@400;500;700&display=swap');
    body { background: #F4F4F4; font-family: 'Noto Sans JP', sans-serif; }
    .slide-container {
      width: 1600px; height: 900px; background: #FFFFFF; border-radius: 12px;
      box-shadow: 0 4px 20px rgba(0,0,0,0.08); padding: 40px 48px 32px 48px; margin: 40px auto 0;
      position: relative; overflow: hidden; display: flex; flex-direction: column;
    }
    .header { display: flex; justify-content: space-between; align-items: center; margin-bottom: 32px; border-bottom: 1.5px solid #00A9E0; padding-bottom: 18px; }
    .header-title {
      font-size: 36px; font-weight: 700;
      background: linear-gradient(90deg, #DA1884 0%, #00A9E0 100%);
      -webkit-background-clip: text; background-clip: text; color: transparent;
      letter-spacing: 1px;
    }
    .header-date { color: #2D2D2D; font-size: 18px; }
    .content {
      display: flex;
      gap: 40px;
      flex: 1;
      align-items: stretch;
      min-height: 0;
    }
    .column {
      display: flex;
      flex-direction: column;
      gap: 32px;
      justify-content: stretch;
      min-height: 0;
      /* 幅はstyle属性でflex指定（例: flex:2, flex:5など） */
    }
    .row {
      display: flex;
      flex-direction: row;
      gap: 24px;
      min-height: 0;
      /* 行内に複数カードを並べたい場合に使用 */
    }
    .card {
      background: #FFFFFF;
      border-radius: 12px;
      box-shadow: 0 2px 10px rgba(0,0,0,0.05);
      padding: 28px 24px 20px 24px;
      border: 2px solid #F4F4F4;
      display: flex;
      flex-direction: column;
      flex: 1 1 0;
      min-height: 0;
      justify-content: flex-start;
    }
    .card-title {
      font-size: 20px;
      font-weight: 700;
      margin-bottom: 14px;
      display: flex;
      align-items: center;
      gap: 10px;
    }
    .card-content {
      font-size: 15px;
      color: #2D2D2D;
      line-height: 1.6;
      flex: 1 1 auto;
      min-height: 0;
      overflow: auto;
    }
    .footer { color: #94a3b8; font-size: 13px; margin-top: 18px; }
    /* 必要に応じて .highlight, .flowchart, .icon-bullet など追加 */
    /* カラーコードは以下を必ず使用すること
      Cyan      #00A9E0
      Gray      #2D2D2D
      LightGray #F4F4F4
      White     #FFFFFF
      Magenta   #DA1884
      Purple    #8031A7
      Turquoise #00B2A9
      Green     #78BE20
      Yellow    #EEDD00
      Orange    #FF6A13
    */
    /* 例: */
    .icon-cyan { background: #00A9E0; color: #fff; }
    .icon-magenta { background: #DA1884; color: #fff; }
    .icon-turquoise { background: #00B2A9; color: #fff; }
    .icon-orange { background: #FF6A13; color: #fff; }
    .icon-purple { background: #8031A7; color: #fff; }
    .icon-yellow { background: #EEDD00; color: #2D2D2D; }
    .icon-green { background: #78BE20; color: #fff; }
    .icon-gray { background: #2D2D2D; color: #fff; }
    .icon-lightgray { background: #F4F4F4; color: #2D2D2D; }
  </style>
  <!-- Mermaid.js CDN -->
  <script src="https://cdn.jsdelivr.net/npm/mermaid@10.9.0/dist/mermaid.min.js"></script>
</head>
<body>
  <!-- 例1: 1カラム1行 -->
  <div class="slide-container">
    <div class="header">
      <div class="header-title">1カラム1行例</div>
      <div style="display: flex; align-items: center; gap: 12px;">
        <span class="header-date" id="header-date-1"></span>
        <button class="svg-download-btn" data-slide="slide-1" style="background: none; border: none; padding: 0; cursor: pointer;">
          <svg width="36" height="36" viewBox="0 0 44 44" fill="none">
            <circle cx="22" cy="22" r="18" fill="#F4F4F4"/>
            <circle cx="22" cy="22" r="18" fill="none" stroke="#00A9E0" stroke-width="2"/>
            <g>
              <path d="M22 13v13" stroke="#00A9E0" stroke-width="2.2" stroke-linecap="round"/>
              <path d="M17 22l5 5 5-5" stroke="#00A9E0" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/>
            </g>
          </svg>
        </button>
      </div>
    </div>
    <div class="content">
      <div class="column" style="flex:1">
        <div class="card">
          <div class="card-title">1カラム1行</div>
          <div class="card-content">内容</div>
        </div>
      </div>
    </div>
    <div class="footer">Smart R&D | 作成者名 | チーム名</div>
  </div>

  <!-- 例2: 2カラム2行（比率1:1） -->
  <div class="slide-container">
    <div class="header">
      <div class="header-title">2カラム2行例（1:1）</div>
      <div style="display: flex; align-items: center; gap: 12px;">
        <span class="header-date" id="header-date-1"></span>
        <button class="svg-download-btn" data-slide="slide-1" style="background: none; border: none; padding: 0; cursor: pointer;">
          <svg width="36" height="36" viewBox="0 0 44 44" fill="none">
            <circle cx="22" cy="22" r="18" fill="#F4F4F4"/>
            <circle cx="22" cy="22" r="18" fill="none" stroke="#00A9E0" stroke-width="2"/>
            <g>
              <path d="M22 13v13" stroke="#00A9E0" stroke-width="2.2" stroke-linecap="round"/>
              <path d="M17 22l5 5 5-5" stroke="#00A9E0" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/>
            </g>
          </svg>
        </button>
      </div>
    </div>
    <div class="content">
      <div class="column" style="flex:1">
        <div class="card">左カラム1行目</div>
        <div class="card">左カラム2行目</div>
      </div>
      <div class="column" style="flex:1">
        <div class="card">右カラム1行目</div>
        <div class="card">右カラム2行目</div>
      </div>
    </div>
    <div class="footer">Smart R&D | 作成者名 | チーム名</div>
  </div>

  <!-- 例3: 2カラム（比率1:5） -->
  <div class="slide-container">
    <div class="header">
      <div class="header-title">2カラム例（1:5）</div>
      <div style="display: flex; align-items: center; gap: 12px;">
        <span class="header-date" id="header-date-1"></span>
        <button class="svg-download-btn" data-slide="slide-1" style="background: none; border: none; padding: 0; cursor: pointer;">
          <svg width="36" height="36" viewBox="0 0 44 44" fill="none">
            <circle cx="22" cy="22" r="18" fill="#F4F4F4"/>
            <circle cx="22" cy="22" r="18" fill="none" stroke="#00A9E0" stroke-width="2"/>
            <g>
              <path d="M22 13v13" stroke="#00A9E0" stroke-width="2.2" stroke-linecap="round"/>
              <path d="M17 22l5 5 5-5" stroke="#00A9E0" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/>
            </g>
          </svg>
        </button>
      </div>
    </div>
    <div class="content">
      <div class="column" style="flex:1">
        <div class="card">左カラム（狭い）</div>
      </div>
      <div class="column" style="flex:5">
        <div class="card">右カラム（広い）</div>
      </div>
    </div>
    <div class="footer">Smart R&D | 作成者名 | チーム名</div>
  </div>

  <!-- 例4: 3カラム（比率2:1:3） -->
  <div class="slide-container">
    <div class="header">
      <div class="header-title">3カラム例（2:1:3）</div>
      <div style="display: flex; align-items: center; gap: 12px;">
        <span class="header-date" id="header-date-1"></span>
        <button class="svg-download-btn" data-slide="slide-1" style="background: none; border: none; padding: 0; cursor: pointer;">
          <svg width="36" height="36" viewBox="0 0 44 44" fill="none">
            <circle cx="22" cy="22" r="18" fill="#F4F4F4"/>
            <circle cx="22" cy="22" r="18" fill="none" stroke="#00A9E0" stroke-width="2"/>
            <g>
              <path d="M22 13v13" stroke="#00A9E0" stroke-width="2.2" stroke-linecap="round"/>
              <path d="M17 22l5 5 5-5" stroke="#00A9E0" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/>
            </g>
          </svg>
        </button>
      </div>
    </div>
    <div class="content">
      <div class="column" style="flex:2">
        <div class="card">左カラム</div>
      </div>
      <div class="column" style="flex:1">
        <div class="card">中央カラム</div>
      </div>
      <div class="column" style="flex:3">
        <div class="card">右カラム</div>
      </div>
    </div>
    <div class="footer">Smart R&D | 作成者名 | チーム名</div>
  </div>

  <!-- 例5: 4カラム（比率1:1:1:1） -->
  <div class="slide-container">
    <div class="header">
      <div class="header-title">4カラム例（均等）</div>
      <div style="display: flex; align-items: center; gap: 12px;">
        <span class="header-date" id="header-date-1"></span>
        <button class="svg-download-btn" data-slide="slide-1" style="background: none; border: none; padding: 0; cursor: pointer;">
          <svg width="36" height="36" viewBox="0 0 44 44" fill="none">
            <circle cx="22" cy="22" r="18" fill="#F4F4F4"/>
            <circle cx="22" cy="22" r="18" fill="none" stroke="#00A9E0" stroke-width="2"/>
            <g>
              <path d="M22 13v13" stroke="#00A9E0" stroke-width="2.2" stroke-linecap="round"/>
              <path d="M17 22l5 5 5-5" stroke="#00A9E0" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/>
            </g>
          </svg>
        </button>
      </div>
    </div>
    <div class="content">
      <div class="column" style="flex:1"><div class="card">カラム1</div></div>
      <div class="column" style="flex:1"><div class="card">カラム2</div></div>
      <div class="column" style="flex:1"><div class="card">カラム3</div></div>
      <div class="column" style="flex:1"><div class="card">カラム4</div></div>
    </div>
    <div class="footer">Smart R&D | 作成者名 | チーム名</div>
  </div>

  <!-- 例6: 2カラム・各カラム内で複数行（row） -->
  <div class="slide-container">
    <div class="header">
      <div class="header-title">2カラム・各カラム2行（row）</div>
      <div style="display: flex; align-items: center; gap: 12px;">
        <span class="header-date" id="header-date-1"></span>
        <button class="svg-download-btn" data-slide="slide-1" style="background: none; border: none; padding: 0; cursor: pointer;">
          <svg width="36" height="36" viewBox="0 0 44 44" fill="none">
            <circle cx="22" cy="22" r="18" fill="#F4F4F4"/>
            <circle cx="22" cy="22" r="18" fill="none" stroke="#00A9E0" stroke-width="2"/>
            <g>
              <path d="M22 13v13" stroke="#00A9E0" stroke-width="2.2" stroke-linecap="round"/>
              <path d="M17 22l5 5 5-5" stroke="#00A9E0" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/>
            </g>
          </svg>
        </button>
      </div>
    </div>
    <div class="content">
      <div class="column" style="flex:1">
        <div class="row">
          <div class="card">左カラム1行目-1</div>
          <div class="card">左カラム1行目-2</div>
        </div>
        <div class="row">
          <div class="card">左カラム2行目-1</div>
        </div>
      </div>
      <div class="column" style="flex:2">
        <div class="row">
          <div class="card">右カラム1行目-1</div>
        </div>
        <div class="row">
          <div class="card">右カラム2行目-1</div>
          <div class="card">右カラム2行目-2</div>
        </div>
      </div>
    </div>
    <div class="footer">Smart R&D | 作成者名 | チーム名</div>
  </div>

  <!-- Mermaidプレビュー付きスライド例も同様にカラム数・比率調整可 -->
  <div class="slide-container" id="slide-mermaid">
    <div class="header">
      <div class="header-title">図解スライド（Mermaidプレビュー）</div>
      <div style="display: flex; align-items: center; gap: 12px;">
        <span class="header-date" id="header-date-mermaid"></span>
        <button class="svg-download-btn" data-slide="slide-mermaid" style="background: none; border: none; padding: 0; cursor: pointer;">
          <svg width="36" height="36" viewBox="0 0 44 44" fill="none">
            <circle cx="22" cy="22" r="18" fill="#F4F4F4"/>
            <circle cx="22" cy="22" r="18" fill="none" stroke="#00A9E0" stroke-width="2"/>
            <g>
              <path d="M22 13v13" stroke="#00A9E0" stroke-width="2.2" stroke-linecap="round"/>
              <path d="M17 22l5 5 5-5" stroke="#00A9E0" stroke-width="2.2" stroke-linecap="round" stroke-linejoin="round"/>
            </g>
          </svg>
        </button>
      </div>
    </div>
    <div class="content" style="display:flex;flex-direction:row;align-items:stretch;gap:40px;">
      <!-- Mermaidコード入力 -->
      <div id="mermaid-input-panel" style="flex:1;min-width:0;display:flex;flex-direction:column;">
        <div class="card" style="height:100%;display:flex;flex-direction:column;">
          <div class="card-title" style="color:#00A9E0;">Mermaidコード入力</div>
          <div class="card-content" style="font-size:13px;flex:1 1 0;display:flex;flex-direction:column;">
            <textarea id="mermaid-input" style="width:100%;height:calc(100% - 60px);min-height:120px;max-height:400px;font-family:monospace;font-size:15px;padding:8px;border-radius:6px;border:1.5px solid #00A9E0;resize:vertical;box-sizing:border-box;">flowchart TB
  A --> B
  B --> C
  C --> D
</textarea>
          </div>
          <div style="padding:0 0 8px 0;display:flex;justify-content:flex-end;">
            <button id="mermaid-preview-btn" style="margin-top:8px;padding:12px 32px;font-size:16px;font-weight:bold;background:#00A9E0;color:#fff;border:none;border-radius:8px;cursor:pointer;width:100%;">🔄 Preview</button>
          </div>
        </div>
      </div>
      <!-- Mermaidプレビュー -->
      <div id="mermaid-preview-panel" style="flex:5;min-width:0;display:flex;flex-direction:column;overflow:hidden;position:relative;">
        <div class="card" style="background:#F4F4F4; border:2px solid #00A9E0; min-height:480px; display:flex; flex-direction:column; align-items:stretch; height:100%;">
          <div class="card-title" style="color:#00A9E0; justify-content: center; text-align: center; width: 100%;">Mermaidプレビュー</div>
          <div class="card-content" id="mermaid-card-content" style="font-size:13px;flex:1 1 0;display:flex;align-items:center;justify-content:center;overflow:hidden;">
            <div class="mermaid" id="mermaid-diagram" style="width:100%;min-height:400px;max-height:700px;background:#fff;border-radius:8px;padding:8px;overflow:auto;display:flex;align-items:center;justify-content:center;">
              <!-- Mermaid SVG will be rendered here -->
            </div>
          </div>
        </div>
      </div>
    </div>
    <div class="footer">Smart R&D | 作成者名 | チーム名</div>
  </div>

  <script>
    // 日付表示
    function setDate(id) {
      var today = new Date();
      var y = today.getFullYear();
      var m = today.getMonth() + 1;
      var d = today.getDate();
      document.getElementById(id).textContent = y + '/' + String(m).padStart(2, '0') + '/' + String(d).padStart(2, '0');
    }
    setDate('header-date-1');
    setDate('header-date-mermaid');

    // Mermaidプレビュー
    function renderMermaidFromInput() {
      var code = document.getElementById('mermaid-input').value.trim();
      var mermaidDiv = document.getElementById('mermaid-diagram');
      if (!code) {
        mermaidDiv.innerHTML = '<div style="color:#999;text-align:center;padding:40px;font-size:16px;">Mermaidコードを入力してください</div>';
        return;
      }
      if (window.mermaid && mermaidDiv) {
        mermaidDiv.innerHTML = '<div style="color:#666;text-align:center;padding:20px;">描画中...</div>';
        try {
          var uniqueId = 'mermaidGraph_' + Date.now() + '_' + Math.floor(Math.random() * 1000);
          mermaid.render(uniqueId, code).then(function(result) {
            mermaidDiv.innerHTML = result.svg;
            var svg = mermaidDiv.querySelector('svg');
            if (svg) {
              svg.style.width = '100%';
              svg.style.height = '100%';
              svg.style.maxWidth = '100%';
              svg.style.maxHeight = '100%';
              svg.removeAttribute('width');
              svg.removeAttribute('height');
              if (!svg.getAttribute('viewBox')) {
                var bbox = svg.getBBox();
                svg.setAttribute('viewBox', `${bbox.x} ${bbox.y} ${bbox.width} ${bbox.height}`);
              }
            }
          }).catch(function(error) {
            mermaidDiv.innerHTML = '<div style="color:red;padding:20px;text-align:center;">Mermaidコードのパースエラー<br><small>' + (error && error.message ? error.message : 'Unknown error') + '</small></div>';
          });
        } catch (e) {
          mermaidDiv.innerHTML = '<div style="color:red;padding:20px;text-align:center;">Mermaidエラー<br><small>' + (e && e.message ? e.message : 'Unknown error') + '</small></div>';
        }
      } else {
        mermaidDiv.innerHTML = '<div style="color:red;padding:20px;text-align:center;">Mermaidライブラリが読み込まれていません</div>';
      }
    }
    document.addEventListener('DOMContentLoaded', function() {
      if (window.mermaid) {
        mermaid.initialize({ startOnLoad: false, theme: 'default', securityLevel: 'loose' });
        setTimeout(function() { renderMermaidFromInput(); }, 500);
      }
      var previewBtn = document.getElementById('mermaid-preview-btn');
      if (previewBtn) {
        previewBtn.addEventListener('click', function() {
          renderMermaidFromInput();
        });
      }
    });

    // SVGダウンロード機能（簡易版）
    document.querySelectorAll('.svg-download-btn').forEach(function(btn) {
      btn.addEventListener('click', function() {
        var slideId = btn.getAttribute('data-slide');
        var container = document.getElementById(slideId);
        var svgEls = container.querySelectorAll('svg');
        if (svgEls.length > 0) {
          // Mermaid図がある場合はそれをダウンロード
          var svg = svgEls[0];
          var serializer = new XMLSerializer();
          var svgString = serializer.serializeToString(svg);
          var blob = new Blob([svgString], {type: 'image/svg+xml'});
          var url = URL.createObjectURL(blob);
          var link = document.createElement('a');
          link.download = slideId + '.svg';
          link.href = url;
          link.click();
          URL.revokeObjectURL(url);
        } else {
          alert('SVGが見つかりません');
        }
      });
    });
  </script>
</body>
</html>
```

---

## 3. スライド作成時のポイント

- `.content`内の`.column`数・`flex`比率・`.row`数は自由に調整
- 1カラム～4カラム、各カラム1～4行まで柔軟に設計
- カードの内容量や図解に応じて比率や行数を調整
- Mermaidプレビューや図解も同様にカラム・行数・比率を調整して利用

---

## 4. カスタマイズ例

- カード数やカラム数は柔軟に調整可
- `.card-title`や`.card-content`に色やアイコンを追加可
- `.flowchart`や`.process-flow`などの構造も追加可
- Mermaidコードを使った図解も可

---

## 5. テンプレートの使い方

- このひな形をコピーし、タイトル・本文・リスト・フロー等を差し替えて利用
- スライドが複数枚必要な場合は`.slide-container`を複数追加
- スタイルや構造は必要に応じて拡張

---
