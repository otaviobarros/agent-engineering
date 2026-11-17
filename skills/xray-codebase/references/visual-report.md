# Visual report rules

Shared reference for skills that return a visual HTML report. Read it with the
[shared workflow contract](workflow-contract.md). The calling skill owns the
content and its sections; this reference owns the page, its elements, the
diagrams, and the render check.

## Purpose and voice

The report replaces reading, so the reader must understand more, with less effort,
than the source material gives. Clarity wins over brevity: keep a fact the reader
needs, and give it the element that shows it fastest.

- **Elements carry the content.** A number goes in a chip or a bar, a comparison
  in a table or a before/after pair, a flow in a step strip or diagram, a choice in
  a question. Prose holds what no element can.
- **Prose:** at most two sentences in a row. Write points as `Label: point`
  bullets of one line each.
- **Plain words.** Name the file, function, count, or user effect. Cut
  intensifiers, hedges, and stock phrases such as "comprehensive", "robust",
  "seamless", "leverage", and "it's important to note".
- **One fact, one place.** A risk appears once, at its question. A file appears
  once, at its stop. Link to the place instead of restating it.
- **First screen:** the answer and the decision board. The reader knows what is
  being asked of them before they scroll.

## Location and safety

- Write one self-contained `.html` file. Use the path the user names. Otherwise use
  the project's ignored scratch directory when `git check-ignore` confirms it is
  ignored, else the OS temporary directory. Name it
  `<skill>-<subject>-<YYYYMMDD-HHMM>.html`.
- Writing the report needs no project-file authority. Writing it inside tracked
  project files, committing it, posting it, or uploading it needs explicit
  authority.
- Treat the page as shareable. Redact credentials, tokens, personal data, and
  internal hostnames found in source. Escape `<`, `>`, and `&` in every code
  excerpt, label, and diagram source.
- The page loads nothing from the network: no CDN, fonts, analytics, or remote
  images. Diagrams render with the bundled Pele library, inlined into the page.

## Page anatomy

The page reads top to bottom as a *route*: a vertical line whose stops are the
items the reader walks through, in reading order. The calling skill names the
sections; these are the elements it fills them with.

| Element | Use it for | Rules |
| --- | --- | --- |
| Header | Subject, one meta line, title, lede | Title states the outcome in plain words. Lede: two sentences at most. |
| Decision board | The questions the reader answers | Numbered checklist, each item linked to its question. A dial counts answered items. Beside it, a 3×3 grid that places each item by impact and likelihood, or value and cost. |
| Proportion bar and area table | Where the volume or effort sits | One bar split by area, then one table row per area: swatch, linked name, count, size, level. |
| Step strip | A linear process of 3 to 7 steps | Each step: a kind word (`Reads`, `Writes`, `You`), a name, one line. Color the step that writes or acts. |
| Diagram | Branching flow, dependencies, states, call order | See [Diagrams](#diagrams). Never for a list or a straight line of steps. |
| Route stop | One area, candidate, or item | Level marker, title with level text, fact chips, 2 to 5 `Label: point` bullets, then its questions, transfers, and detail. |
| Fact chip | Counts, file names, warnings | Short noun phrases. A warning chip uses the medium color. |
| Transfer | Where the item reaches an external system | A colored branch off the route line: system name, then what crosses. |
| Question | A decision the reader makes | Number, question, `file:line`, evidence tag. Opens to "Approve if" and "Hold if" side by side, then the basis in one line. |
| Before/after pair | A structure the change or proposal alters | Left: today, with code or data. Right: the proposal, often a diagram. One line under each on what differs. |
| Detail | Supporting evidence the reader may skip | A collapsed `<details>` with a named summary such as "Why it is low risk". Bullets with `file:line`. |
| Decision table | Choices the reader inherits | Decision, instead of, tradeoff, source. |
| Unknown box | Gaps | Dashed box at the route's end. Write "None found" when empty. |

Every element that opens shows a chevron at its right edge that turns when it
opens, and its summary is a full-width hit target. A reader must see that a
question or detail holds more without trying it.

Show every level as text as well as color. Color is never the only signal.

## Evidence and levels

Each claim that needs a source carries an evidence tag:

- *cited*: a source states it: `file:line`, commit, PR body, review thread, plan,
  ADR, or issue. The tag's title or the detail names the source.
- *inferred*: your reasoning from the code. The detail gives the `file:line` it
  rests on.
- *unknown*: not established. It also appears in the unknown box.

Level combines impact and likelihood:

- *High*: a plausible failure reaches users, data, money, security, or an external
  system.
- *Medium*: a plausible failure stays contained, or recovery is simple.
- *Low*: failure is unlikely, or its effect is cosmetic.

A question's "Approve if" and "Hold if" each state a condition the reader can
check. Its basis gives the trigger, who feels the failure, and the evidence.
Coverage is separate from risk: report it with the
[evidence ladder](verification.md#coverage-map), and never lower a level because a
test exists.

## Diagrams

Draw a diagram when the reader must see structure that text and tables flatten:
branches, dependencies, states, order across actors, shares of a whole, or a trend.
Write Mermaid syntax in a `pre.mermaid` block inside a `.diagram` element; the
bundled [Pele](pele/pele.global.js) library draws it when the page opens. Pele
supports every Mermaid type plus its own; pick the type by the question it answers.

Each diagram must earn its place. Before you add one, name the reader's question it
answers and check that no element already on the page answers it. The area bar and
table already show which files changed and how much; a file tree, treemap, or
branch graph that repeats them is noise. Most reports need one or two diagrams;
the type table lists options, not a checklist. When a diagram explains less than
the table or step strip beside it, drop the diagram.

| Question the reader has | Type |
| --- | --- |
| What calls or depends on what, and what the change reaches | `flowchart LR` |
| Where changed files sit, when their location is the point (a move or split) | `treeView-beta` |
| Who calls whom, in what order | `sequenceDiagram` |
| Which actor or service does each step of a process | `swimlane-beta LR` |
| Which states exist and which transitions are legal | `stateDiagram-v2` |
| How types, interfaces, and implementations relate | `classDiagram` |
| What the schema or migration changes | `erDiagram` |
| Which services, stores, and external systems connect | `architecture-beta`, or `C4Context` for people and system boundaries |
| How items rank on two axes, such as value and cost | `quadrantChart` |
| How a measure changes over time, such as churn per month | `xychart` |
| How a total splits across areas | `treemap-beta` (shares) or `sankey` (flows from one source) |
| How branches diverge or merge, when the history is the point | `gitGraph` |
| Which steps a migration or rollout takes, in order | `timeline` |
| Which causes lead to one failure | `ishikawa-beta` |

A straight sequence of 3 to 7 steps is a step strip; exact values across items are
a table. Avoid `pie`: a treemap or bar shows the same shares more legibly.

- At most 12 nodes or items per diagram. Split by area or drop detail before
  adding more.
- Quote labels that hold punctuation or paths: `api["orders/api.py"]`. Use short
  alphanumeric node IDs; avoid `end`, `graph`, `style`, and `class`.
- Label edges with the relation: `-->|calls|`, `-->|writes|`.
- Mark changed or proposed nodes with `class ID changed`, and new ones with
  `class ID added`. The scaffold styles both classes in theme colors, so a marked
  node follows light and dark mode. Avoid colors in `style` or `classDef`: they stay
  fixed when the theme changes. Say what the marks mean in the caption.
- Give each chart a title and axis labels with units.
- Escape `<`, `>`, and `&` in the source; the browser restores them before Pele
  reads it.

The scaffold's `.diagram` rule maps the page tokens to Pele's theme variables:
background, text, lines, node surfaces, accent, critical, radius, the eight series
colors, and both fonts. Diagrams therefore share the page's palette and type in
light and dark themes. Keep that mapping; change the page tokens instead of
recoloring one diagram. The render script uses `pele.mount`, which fits each
diagram to its container, switches wide layouts to vertical below 420 px
(`directionBreakpoint`) so a half-width column keeps them horizontal,
adds zoom controls when a diagram shrinks to fit, and draws a diagram inside a
closed `<details>` when it opens. Mount replaces its container's content, so the
script mounts into a new element in place of the `pre`; the caption stays.

Hand-build a visual with HTML and inline SVG when no type fits the point: layers a
call passes through, an interface against its implementation, or a call tree that
collapses into one module. Inline SVG sets a `viewBox`, sizes with CSS, colors
through the page's CSS variables, and has a `<title>`.

## Scaffold

Start from this page and keep its tokens, so every report shares one visual
language in light and dark themes. Replace the samples with real content; delete
elements a section does not need. Checkboxes are for the reader's own tracking;
nothing is saved.

```html
<!doctype html>
<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>SUBJECT</title>
<style>
:root{--paper:#FBFCFE;--ink:#1B2430;--soft:#5B6675;--rule:#DCE2EA;--wash:#EEF2F7;--line:#2B59C3;--transfer:#B83280;--high:#D7263D;--medium:#C98A00;--low:#2E8B57;
  --sans:"Avenir Next",Avenir,"Segoe UI Variable Display","Segoe UI",system-ui,sans-serif;--code:ui-monospace,"SF Mono",Menlo,monospace}
@media (prefers-color-scheme:dark){:root{--paper:#0F1722;--ink:#E6ECF3;--soft:#97A3B3;--rule:#263243;--wash:#162131;--line:#6E95F2;--transfer:#E26AAE;--high:#FF6B7D;--medium:#F2B544;--low:#5CC98B}}
*{box-sizing:border-box}
html{background:var(--paper)}
body{margin:0;color:var(--ink);font:16px/1.55 var(--sans);-webkit-font-smoothing:antialiased}
main{max-width:920px;margin:0 auto;padding:48px 20px 72px}
section{margin:0 0 52px}
code{font:13px var(--code);color:var(--soft)}
a{color:var(--line);text-decoration:none}
a:hover{text-decoration:underline}
:focus-visible{outline:3px solid var(--line);outline-offset:2px;border-radius:4px}
.pr{font-size:15px;color:var(--soft);margin:0 0 6px}
.pr b{color:var(--ink)}
h1{font-size:36px;line-height:1.12;font-weight:600;letter-spacing:-.012em;margin:0 0 14px;max-width:24ch}
.lede{font-size:19px;margin:0 0 28px;max-width:60ch}
h2{font-size:24px;font-weight:600;margin:0 0 4px}
.sub{color:var(--soft);margin:0 0 18px;font-size:15px}
.n{display:inline-grid;place-items:center;flex:none;width:22px;height:22px;border-radius:50%;background:var(--ink);color:var(--paper);font-size:12px;font-weight:600}
.lvl{font-size:13px;font-weight:600;white-space:nowrap}
.lvl::before{content:"";display:inline-block;width:9px;height:9px;border-radius:50%;margin-right:6px;box-sizing:border-box}
.lvl.h{color:var(--high)}.lvl.h::before{background:var(--high)}
.lvl.m{color:var(--medium)}.lvl.m::before{background:var(--medium)}
.lvl.l{color:var(--low)}.lvl.l::before{border:2px solid var(--low)}
.src{font-size:12px;color:var(--soft);border:1px solid var(--rule);border-radius:5px;padding:0 5px;cursor:help}
/* Decision board */
.board{display:grid;grid-template-columns:1fr auto;gap:28px;align-items:center;padding:22px 24px;border-radius:16px;background:var(--wash)}
.progress{display:flex;gap:16px;align-items:center}
.progress p{margin:0;font-size:15px}
.dial{--p:0;width:60px;height:60px;border-radius:50%;flex:none;background:conic-gradient(var(--line) calc(var(--p)*1%),var(--rule) 0);display:grid;place-items:center}
.dial span{width:46px;height:46px;border-radius:50%;background:var(--wash);display:grid;place-items:center;font-weight:600}
.qlist{list-style:none;margin:14px 0 0;padding:0;display:grid;gap:4px;font-size:15px}
.qlist li{display:flex;gap:10px;align-items:baseline}
.qlist li.done a{color:var(--soft);text-decoration:line-through}
.grid{display:grid;grid-template-columns:auto repeat(3,64px);grid-template-rows:repeat(3,44px) auto;gap:3px;font-size:12px;color:var(--soft)}
.grid .cell{border-radius:6px;display:flex;align-items:center;justify-content:center;gap:3px}
.grid .y{display:flex;align-items:center;justify-content:flex-end;padding-right:8px}
.grid .x{text-align:center;padding-top:4px}
.c-l{background:color-mix(in srgb,var(--low) 16%,transparent)}.c-m{background:color-mix(in srgb,var(--medium) 20%,transparent)}.c-h{background:color-mix(in srgb,var(--high) 18%,transparent)}
/* Proportion bar and area table */
.bar{display:flex;height:22px;border-radius:7px;overflow:hidden;gap:2px;margin:0 0 14px}
table{width:100%;border-collapse:collapse;font-size:15px}
th{text-align:left;font-size:13px;font-weight:600;color:var(--soft);padding:0 10px 8px;border-bottom:2px solid var(--rule)}
td{padding:10px;border-bottom:1px solid var(--rule);vertical-align:top}
.sw{display:inline-block;width:12px;height:12px;border-radius:3px;margin-right:8px;vertical-align:-1px}
.num{text-align:right;color:var(--soft);white-space:nowrap;font-variant-numeric:tabular-nums}
/* Step strip */
.steps{list-style:none;margin:0 0 14px;padding:0;display:grid;grid-template-columns:repeat(auto-fit,minmax(0,1fr));grid-auto-flow:column}
.steps li{padding:14px 14px 14px 22px;margin-left:-6px;background:var(--wash);font-size:14px;color:var(--soft);display:flex;flex-direction:column;gap:2px;clip-path:polygon(0 0,calc(100% - 12px) 0,100% 50%,calc(100% - 12px) 100%,0 100%,12px 50%)}
.steps li:first-child{margin-left:0;padding-left:16px;border-radius:12px 0 0 12px;clip-path:polygon(0 0,calc(100% - 12px) 0,100% 50%,calc(100% - 12px) 100%,0 100%)}
.steps b{color:var(--ink);font-size:15.5px}
.steps .k{font-size:12px;font-weight:600;color:var(--line)}
.steps .w{background:color-mix(in srgb,var(--transfer) 16%,var(--wash))}.steps .w .k{color:var(--transfer)}
.steps .y{background:var(--line);color:#fff}.steps .y b,.steps .y .k{color:#fff}
/* Diagrams */
figure{margin:0}
.diagram{background:var(--wash);border-radius:14px;padding:16px 14px 12px;min-width:0}
pre.mermaid{margin:0;font:13px var(--code);white-space:pre-wrap;color:var(--soft)}
.diagram{--pele-bg:var(--wash);--pele-fg:var(--ink);--pele-fg-on-light:#1B2430;--pele-fg-on-dark:#FFFFFF;--pele-muted:var(--soft);--pele-line:var(--soft);
  --pele-surface:var(--paper);--pele-surface-alt:color-mix(in srgb,var(--rule) 45%,var(--wash));--pele-border:color-mix(in srgb,var(--line) 45%,var(--rule));--pele-accent:var(--line);
  --pele-critical:var(--high);--pele-error:var(--high);--pele-font:var(--sans);--pele-font-mono:var(--code);--pele-radius:8px;--pele-title-weight:600;--pele-heading-weight:600;
  --pele-series-1:var(--line);--pele-series-2:var(--transfer);--pele-series-3:var(--low);--pele-series-4:var(--medium);--pele-series-5:var(--high);--pele-series-6:#7A5AF8;--pele-series-7:#0E9AA7;--pele-series-8:var(--soft)}
.diagram svg{display:block;max-width:100%;height:auto;margin:0 auto}
.diagram .changed :is(rect,path,polygon,circle){stroke:var(--line);stroke-width:2.5px}
.diagram .added :is(rect,path,polygon,circle){stroke:var(--low);stroke-width:2.5px}
.diagram .changed>.pele-label{fill:var(--line);font-weight:600}
.diagram .added>.pele-label{fill:var(--low);font-weight:600}
.diagram-error{box-shadow:inset 4px 0 var(--high)}
figcaption{font-size:14px;color:var(--soft);margin-top:10px}
/* Route */
.route{position:relative;list-style:none;margin:0;padding:0}
.route::before{content:"";position:absolute;left:15px;top:14px;bottom:40px;width:6px;border-radius:3px;background:var(--line);transform-origin:top;animation:draw .9s cubic-bezier(.2,.7,.2,1) both}
@keyframes draw{from{transform:scaleY(0)}}
@media (prefers-reduced-motion:reduce){.route::before{animation:none}}
.stop{position:relative;padding:0 0 40px 58px}
.stop::before{content:"";position:absolute;left:4px;top:4px;width:28px;height:28px;box-sizing:border-box;border-radius:50%;background:var(--paper);border:6px solid var(--ink)}
.stop.high::before{border-color:var(--high);background:var(--high)}
.stop.medium::before{border-color:var(--medium);background:var(--medium);box-shadow:inset 0 0 0 4px var(--paper)}
.stop.low::before{border-color:var(--low)}
.stop.end::before{background:var(--ink);border-radius:6px}
.stop h3{font-size:21px;font-weight:600;margin:0}
.stop h3 .lvl{margin-left:10px;vertical-align:2px}
.chips{display:flex;flex-wrap:wrap;gap:6px;margin:6px 0 12px;padding:0;list-style:none}
.chips li{font-size:13px;padding:2px 9px;border-radius:999px;background:var(--wash);color:var(--soft)}
.chips .warn{color:var(--medium);background:color-mix(in srgb,var(--medium) 14%,transparent)}
.points{margin:0 0 14px;padding:0;list-style:none;display:grid;gap:5px;max-width:66ch}
.points li{padding-left:18px;position:relative}
.points li::before{content:"";position:absolute;left:2px;top:.62em;width:7px;height:7px;border-radius:2px;background:var(--rule)}
.points b{font-weight:600}
.transfer{display:flex;align-items:baseline;flex-wrap:wrap;gap:4px 10px;font-size:14px;color:var(--soft);margin:-2px 0 14px -42px}
.transfer::before{content:"";flex:none;align-self:center;width:34px;height:4px;border-radius:2px;background:var(--transfer)}
.transfer b{color:var(--transfer)}
/* Openable elements: chevron at the right edge */
summary{cursor:pointer;list-style:none}
summary::-webkit-details-marker{display:none}
summary::after{content:"";flex:none;width:8px;height:8px;margin:0 4px 0 auto;border:solid var(--soft);border-width:0 2px 2px 0;transform:translateY(-2px) rotate(45deg);transition:transform .2s}
details[open]>summary::after{transform:translateY(2px) rotate(-135deg)}
.q{display:grid;grid-template-columns:auto 1fr;gap:4px 12px;padding:12px 14px;margin:0 0 10px;border:1.5px solid var(--rule);border-radius:12px;background:var(--paper)}
.q:hover,.q:target{border-color:var(--line)}
.q input{appearance:none;width:22px;height:22px;margin:2px 0 0;border:2px solid var(--soft);border-radius:6px;cursor:pointer;display:grid;place-items:center}
.q input:checked{background:var(--line);border-color:var(--line)}
.q input:checked::after{content:"";width:6px;height:11px;border:solid #fff;border-width:0 2.5px 2.5px 0;transform:translateY(-1px) rotate(45deg)}
.q:has(input:checked){background:var(--wash);border-color:transparent}
.q details{min-width:0}
.q summary{display:flex;flex-wrap:wrap;gap:4px 8px;align-items:baseline}
.q summary{position:relative;padding-right:28px}
.q summary::after{position:absolute;right:4px;top:.6em;margin:0}
.ask{font-weight:600;font-size:16.5px}
.answers{display:grid;grid-template-columns:1fr 1fr;gap:10px;margin:12px 0 2px;font-size:14.5px}
.answers p{margin:0;padding:10px 12px;border-radius:9px;background:var(--wash)}
.answers .safe{box-shadow:inset 3px 0 var(--low)}.answers .unsafe{box-shadow:inset 3px 0 var(--high)}
.answers b{display:block;font-size:13px;margin-bottom:2px}
.basis{grid-column:1/-1;color:var(--soft);font-size:14px}
.more{font-size:14.5px;color:var(--soft);margin:0 0 10px;max-width:66ch}
.more summary{display:flex;align-items:center;gap:8px;padding:8px 12px;border-radius:9px;color:var(--line);font-weight:500}
.more summary:hover{background:var(--wash)}
.more ul{margin:6px 0 0;padding-left:30px}
/* Before/after pair */
.ba{display:grid;grid-template-columns:minmax(0,.7fr) minmax(0,1.3fr);gap:12px;margin:0 0 14px}
.ba>div{background:var(--wash);border-radius:12px;padding:12px 14px;min-width:0}
.ba h4{margin:0 0 6px;font-size:14px}
.ba pre:not(.mermaid){margin:0;font:13px/1.5 var(--code);overflow:auto}
.ba p{margin:8px 0 0;font-size:14px;color:var(--soft)}
.ba .diagram{padding:4px 0 0}
/* Unknown box */
.unknown{margin:16px 0 0;padding:12px 14px;border-radius:10px;border:1.5px dashed var(--rule)}
.unknown ul{margin:4px 0 0;padding-left:18px;color:var(--soft)}
@media (max-width:700px){
  main{padding-top:28px}h1{font-size:28px}.lede{font-size:17px}
  .board,.answers,.ba{grid-template-columns:1fr}
  .steps{grid-auto-flow:row;grid-template-columns:1fr;gap:4px}
  .steps li,.steps li:first-child{clip-path:none;border-radius:10px;margin:0;padding:10px 14px}
  .transfer{flex-wrap:nowrap;align-items:center}
  .wide{display:none}
}
</style>
</head>
<body>
<main>
<header>
<p class="pr"><b>SUBJECT ID</b>, META FACTS</p>
<h1>OUTCOME IN PLAIN WORDS</h1>
<p class="lede">WHAT IT DELIVERS. HIGHEST LEVEL AND HOW MANY QUESTIONS NEED THE READER.</p>
</header>

<section aria-label="Decisions">
<div class="board">
  <div>
    <div class="progress"><div class="dial" id="dial"><span id="count">0/1</span></div>
      <p><b id="left">1 question open</b><br>Each one sits at its stop below.</p></div>
    <ol class="qlist" id="qlist"><li data-q="q1"><span class="n">1</span><a href="#q1">SHORT QUESTION</a></li></ol>
  </div>
  <div class="grid" role="img" aria-label="Risk grid: question 1 is medium impact and possible.">
    <div class="y">High impact</div><div class="cell c-m"></div><div class="cell c-h"></div><div class="cell c-h"></div>
    <div class="y">Medium</div><div class="cell c-l"></div><div class="cell c-m"><span class="n">1</span></div><div class="cell c-m"></div>
    <div class="y">Low</div><div class="cell c-l"></div><div class="cell c-l"></div><div class="cell c-l"></div>
    <div></div><div class="x">Unlikely</div><div class="x">Possible</div><div class="x">Likely</div>
  </div>
</div>
</section>

<section>
<h2>SECTION TITLE</h2>
<p class="sub">WHAT THIS SECTION SHOWS, IN ONE LINE.</p>
<div class="bar" role="img" aria-label="Lines added by area"><span style="flex:120;background:var(--line)" title="AREA, 120"></span><span style="flex:40;background:var(--rule)" title="AREA, 40"></span></div>
<table>
  <tr><td><span class="sw" style="background:var(--line)"></span><a href="#s1">AREA</a></td><td class="num wide">2 files</td><td class="num">+120 −8</td><td><span class="lvl m">Medium</span></td></tr>
</table>
</section>

<section>
<h2>SECTION TITLE</h2>
<ol class="steps">
  <li><span class="k">Reads</span><b>STEP</b><span>ONE LINE</span></li>
  <li class="w"><span class="k">Writes</span><b>STEP</b><span>ONE LINE</span></li>
  <li class="y"><span class="k">You</span><b>Decide</b><span>ONE LINE</span></li>
</ol>
<figure class="diagram">
<pre class="mermaid">flowchart LR
  api["orders/api.py"] -->|calls| pay["payments/client.py"]
  pay -->|writes| db[("orders table")]
  class pay changed</pre>
<figcaption>WHAT THE DIAGRAM ANSWERS. BLUE: CHANGED; GREEN: ADDED.</figcaption>
</figure>
</section>

<section>
<h2>SECTION TITLE</h2>
<ol class="route">
  <li class="stop medium" id="s1">
    <h3>AREA OR ITEM<span class="lvl m">Medium</span></h3>
    <ul class="chips"><li>FILE OR COUNT</li><li class="warn">WARNING</li></ul>
    <ul class="points"><li><b>LABEL:</b> ONE-LINE POINT</li></ul>
    <div class="transfer"><b>EXTERNAL SYSTEM</b> WHAT CROSSES TO IT</div>
    <div class="q" id="q1"><input type="checkbox" data-q="q1" aria-label="Answered question 1">
      <details><summary><span class="n">1</span><span class="ask">QUESTION?</span><code>file.py:42</code><span class="src" title="SOURCE">cited</span></summary>
        <div class="answers">
          <p class="safe"><b>Approve if</b>CHECKABLE CONDITION.</p>
          <p class="unsafe"><b>Hold if</b>CHECKABLE CONDITION.</p>
          <p class="basis">TRIGGER, WHO FEELS IT, EVIDENCE.</p>
        </div></details></div>
    <div class="ba">
      <div><h4>Today</h4><pre>CODE OR DATA</pre><p>WHAT IS WRONG WITH IT.</p></div>
      <div><h4>Proposed</h4><figure class="diagram"><pre class="mermaid">stateDiagram-v2
  [*] --> New
  New --> Paid: pay</pre></figure></div>
    </div>
    <details class="more"><summary>DETAIL NAME</summary><ul><li>EVIDENCE <code>file.py:10</code></li></ul></details>
  </li>
  <li class="stop end">
    <h3>CLOSING STOP TITLE</h3>
    <table><thead><tr><th>Decision</th><th>Instead of</th><th>Tradeoff</th><th>Source</th></tr></thead>
      <tr><td><b>DECISION</b></td><td>ALTERNATIVE</td><td>WHAT THE READER ACCEPTS</td><td><code>SOURCE</code></td></tr></table>
    <div class="unknown"><b>Not yet known</b><ul><li>GAP, OR "None found"</li></ul></div>
  </li>
</ol>
</section>
</main>
<script>
const boxes=[...document.querySelectorAll('.q input')];
const update=()=>{const n=boxes.filter(b=>b.checked).length,t=boxes.length;
  document.getElementById('dial').style.setProperty('--p',t?n/t*100:100);
  document.getElementById('count').textContent=`${n}/${t}`;
  document.getElementById('left').textContent=n===t?'All questions answered':`${t-n} question${t-n===1?'':'s'} open`;
  boxes.forEach(b=>document.querySelector(`#qlist [data-q="${b.dataset.q}"]`)?.classList.toggle('done',b.checked));};
boxes.forEach(b=>b.addEventListener('change',update));update();
</script>
<!-- pele -->
<script>
for (const node of document.querySelectorAll('pre.mermaid')) {
  const box = node.closest('.diagram');
  const source = node.textContent;
  const host = document.createElement('div');
  node.replaceWith(host);
  try {
    pele.mount(host, source, {
      links: false, images: false, zoom: 'auto', directionBreakpoint: 420,
      onError: (error) => { box.classList.add('diagram-error'); box.dataset.error = String(error?.message ?? error); },
    });
  } catch (error) {
    box.classList.add('diagram-error');
    box.dataset.error = String(error?.message ?? error);
  }
}
document.body.dataset.diagrams = 'done';
</script>
</body>
</html>
```

## Inline the diagram library

A page with a `pre.mermaid` block needs the library. After you write the page,
replace the `<!-- pele -->` line with a `<script>` element holding the license
notices from [`pele/LICENSE`](pele/LICENSE) as a `/*! */` comment, then the full
text of [`pele/pele.global.js`](pele/pele.global.js). Resolve both from this
reference's directory. Splice the files with a command; the library is 734 KB, so
never retype or summarize it:

```bash
python3 -c "import sys, pathlib; p, lib = sys.argv[1:]; s = open(p).read(); notice = (pathlib.Path(lib).parent / 'LICENSE').read_text(); open(p, 'w').write(s.replace('<!-- pele -->', '<script>/*!\n' + notice + '*/\n' + open(lib).read() + '</script>', 1))" REPORT.html PATH/TO/pele/pele.global.js
```

Without Python, use any tool that does the same exact replacement. A page without
diagrams deletes the `<!-- pele -->` line and the rendering script after it. The
library is Pele 1.13.0 under the MIT license, with Lucide icons under the ISC
license. Both licenses require their notices in every copy, so a page that holds
the library also holds `pele/LICENSE`.

## Render check

Run the check before you report the page. Use a browser already on the machine.
Installing one, or adding files to the project for the check, needs explicit
authority; probe scripts and screenshots go beside the report.

1. A headless browser is available, such as Playwright with Chromium → open the
   file with the network blocked. Wait up to 20 seconds for
   `body[data-diagrams="done"]`, then confirm:
   - every `.diagram` holds an `svg` and `.diagram-error` matches nothing;
   - the page made no network request;
   - the first screen at 1280×800 shows the answer and the decision board;
   - after you open one question, its chevron has turned and both answers show.

   Take the first-screen and full-page screenshots in light and dark themes and
   one at 375 px wide, and look at each: labels are readable, nothing overlaps or
   is cut off, and each diagram's text is legible at its width. Fix each failure
   and run the check again.
2. No browser → state the render as unverified and name the reason. Keep the
   diagram source valid by the rules above.

Either way, a page with diagrams passes a text search for `Pele 1.13.0`,
`Copyright (c) 2026 kepano`, and `Lucide Icons and Contributors`. A miss means
the splice failed; run it again.

In the response, give the report's absolute path, the render check result with
the screenshot paths, and the answer and questions as text. Open the file with the
host's viewer when the host allows it.
