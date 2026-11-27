# Design Analysis: EGs F2E Week 3 – Scrum 新手村

Source: Figma file `UE8NpczYv3MaAyDVJCqtRF` (a duplicate of the original `fWQvcoua0uhqduVbYYPToL`, made because the MCP server rejected the original). Page `● UI` (node `1:2`).

Status: analysis only. No implementation has been started.

## 0. How to read this document

Each statement carries a tag.

| Tag | Meaning |
|---|---|
| **[O]** | Observed directly in Figma (variables, node metadata, or a screenshot I looked at). |
| **[D]** | Derived by arithmetic from observed values. The rule is stated. |
| **[A]** | Assumption or proposal. It is not in the design and must be confirmed before it is relied on. |
| **[U]** | Unverified or missing. The design has no answer, or I could not read it. |

### 0.1 Coverage and limits of this analysis

The Figma MCP server on this account (Starter plan) hit its monthly tool-call limit during the analysis. What was and was not reviewed:

| Area | Coverage |
|---|---|
| Design system board (`19:1714`), component board (`19:1061`), resource board (`19:15327`), read-me (`19:1867`), flow caption (`19:4530`) | Viewed as screenshots. |
| Design variables (colors, text styles, `btn_3d` effect) | Read via `get_variable_defs` on the design system board. **[O]** |
| Layer tree for all 46 screens on the `● UI` page | Read from metadata (names, sizes, text, hidden layers). |
| Screens viewed as pixels | `loading`, `0-1`, `0-2`, `1-1-1`, `1-2-1`, `1-2-3`, `1-2-5`, `3-1-4`, plus the two 1920px frames (`0-1`, `1-2-2`). |
| Other screens (2-x, 3-1-1/2/3/5/6, 4-x, 5-x, 6-1, 1-2-2 and 1-2-4 at 1440) | **Metadata only.** Layout and text are known. Visual styling is not verified. |
| Page `Prototype / 毛玻璃圖層分析` (`19:4529`) | **Not inspected.** The read-me says it holds the frosted-glass layer breakdown. |
| Page `Flow Chart / Wireframe / User story / Cover` (`0:1`) | **Not inspected.** |
| Figma comments | **Not accessible.** The read-me says the specs are annotated through comments, and comments are not exposed by the MCP tools I used. |
| Prototype interactions, animation durations and easing | **Not accessible.** The read-me points to a prototype video for them. |

Frames I did not view must be re-checked before building their screens (section 11).

---

## 1. Page structure and layout hierarchy

### 1.1 Figma file structure **[O]**

Page `● UI` contains, left to right on the canvas:

| Group | Node | Notes |
|---|---|---|
| `thanks` | `2548:6291` | Credits board, 1920×2206. |
| `reference` boards | `19:1867` read me, `19:1842` anchor, `19:1839` Q&A/message/feedback, `19:1714` design system, `19:1061` component, `19:15327` resource | Design-system and asset sources of truth. |
| `loading` | `103:5838` | 1440×1024. |
| Sections 0–6 | `@media 1440px` row | Main screens, each 1440×1024. |
| `@media 1920px` | `43:2321`, `43:2373` | Only 2 frames, 1920×1080. |
| `Desktop caption` | `19:4530` | Flow chart of sections. |

### 1.2 Product flow **[O]** (caption frame and frame names)

```
主頁/前導 → 團隊-產品負責人 → 短衝規劃會議介紹 → 短衝待辦清單-出題 → 短衝流程介紹 → 自省會議-出題 → 畢業
   (0)          (1)                (2)                  (3)               (4)            (5)         (6)
```

The site is a linear, game-style tutorial. The user advances through scenes with dialogue, then completes one challenge per section.

| Section | Screens (Figma frame names) | Count |
|---|---|---|
| loading | `loading` | 1 |
| 0 入口 | `0-1 start`, `0-2 intro` | 2 |
| 1 產品待辦清單 | `1-1-1 團隊介紹-產品負責人`, `1-2-1 出題`, `1-2-2 使用說明`, `1-2-3 玩家實作`, `1-2-4 實作完成`, `1-2-5 完成提示` | 6 |
| 2 短衝規劃會議 | `2-1-1 介紹`, `2-1-2 團隊介紹-ScrumMaster`, `2-1-3 團隊介紹-開發人員`, `2-2-1 點數介紹`, `2-2-2 點數介紹2` | 5 |
| 3 短衝待辦清單 | `3-1-1 出題`, `3-1-2 玩家實作`, `3-1-3 實作尚未完成`, `3-1-4 點數超過`, `3-1-5 實作完成`, `3-1-6 完成提示` | 6 |
| 4 短衝流程介紹 | `4-1-1 前言`, `4-1-2 介紹`, `4-1-3 介紹`, `4-2-1 出題`, `4-2-2 答題錯誤`, `4-2-3 實作完成`, `4-2-4 完成提示` | 7 |
| 5 Retro 會議 | `5-1 前言`, `5-2-1 出題`, `5-2-2 答題錯誤`, `5-2-3 實作完成`, `5-2-4 完成提示` | 5 |
| 6 完成任務 | `6-1 通過試煉` | 1 |

Naming convention in the design: `X-Y-Z` = section, sub-part, step. Each challenge follows a repeating state pattern: **出題 (prompt) → 玩家實作 (play) → [錯誤 / 未完成 / 超過 (invalid state)] → 實作完成 (valid) → 完成提示 (completion hint)**. Section 1 has no invalid-state frame. **[O]**

### 1.3 Layout of a standard screen (1440×1024) **[O]**

Layers from the layer tree (`1-2-3`, `19:15139`) and the screenshots:

```
Screen 1440×1024
├─ bg_village           1440×1024, full-bleed background illustration
├─ progress             1440×12, pinned to top
├─ role (character)     467×461 in sections 0–2-1, 380×375 from 2-1-3 onward
├─ role/pop (dialogue)  width 1007 (sections 1–2), 1080 (sections 3+), height 128–224 by content
│    ├─ tag chip        role label (PO / GG …)  overlapping the top-left corner
│    └─ continue icon   ▼ at bottom-right (only on click-to-continue dialogs)
├─ main content         list panels / cards / meeting cards, varies by screen
├─ btn                  188×66, bottom-right or centered
├─ hint                 268×52 pill "點擊畫面任意處繼續" (click-to-continue screens only)
└─ progress/Copyright   1440×44 at y=980 (footer bar)
```

Observed placement:

- **Dialogue and character**: Character top-left, dialogue to its right in section 1 and 2 (`1-1-1`, `1-2-x`). In `3-1-4`, the dialogue is on the left and the character (red, Team2) is top-right. **[O]** So character side depends on the speaker.
- **Footer**: text "© 2022 The F2E | UI Design - EG | F2E - OOO", centered, on every screen. **[O]**
- **Top progress bar**: 12px tall, full width. The filled part is lighter. Observed fills: section 1 = 240px of 1440 (1/6), section 3 `3-1-4` = 720px of 1440 (1/2). 1920 frame `1-2-2` = 320 of 1920 (1/6). **[O]** Fill for sections 2, 4, 5, 6 not measured; the pattern "section index ÷ 6" is **[A]**.

### 1.4 Special screens

| Screen | Layout **[O]** |
|---|---|
| `loading` | Dark `bg/Dark` background with a cyan gradient glow at the top edge. Four character sprites (255×120) centered at y≈374. A 1000×8 loading bar at x=220, y=518 (fill 458px = 45.8% in the artboard). Footer text at the bottom. |
| `0-1 start` | Full-bleed leaf illustration. Center: glowing "新手村 SCRUM" logo over a "hole" ellipse (324×83 asset `hole`), tagline "深入敏捷の村一探究竟", and a button "進入村莊". |
| `0-2 intro` | Leaf illustration (darker variant). Center dialogue panel 908×430 with tag "（謎之音）", two paragraphs, then button "接受挑戰" below it. |
| `6-1 通過試煉` | Leaf layers plus `bg_village`. `logo_txt` (600×365), text "《敏捷任務 - 最初の試煉》", "恭喜你通過", four 300×298 characters each with a short speech bubble, and colored dots (`logo_dot_*`). Metadata only; not viewed. |

---

## 2. Reusable UI components

### 2.1 Components documented on the Figma component board **[O]**

| Component | Variants shown | Notes |
|---|---|---|
| Continue icon (triangle) | 4 colors: cyan, purple, yellow, orange | Assets `ic_continue_po/sm/team1/team2`, 32×28. |
| Button (primary, 3D) | Normal (×2 shown), Disabled | 188×66 instance in screens. Gradient teal pill with `btn_3d` shadow. Disabled = grey. |
| Text button "再玩一次" | 2 shown | Small outlined text button. Where it is used is **[U]**; not found in the screens I viewed. |
| Dot / radio-like indicator | 2 shown (grey filled, teal ring) | Purpose and state meaning **[U]**. |
| Progress bar (`progress`) | 7 fill levels | Same lines at 0, ~1/6, … full. |
| Copyright footer (`progress/Copyright`) | 1 | 1440×44. |
| Dialogue box (`role/pop`) | Large (tag "（謎之音）") and compact (tag "PO" + ▼) | Glassmorphism panel with cyan border and glow. |
| Role character | 4 roles with light/glow | See 2.3. |

### 2.2 Components identified from screens **[O]** unless marked

| Component | Where | Details |
|---|---|---|
| **Dialogue / RolePop** | Every game screen | Rounded panel, translucent dark fill over the background, 1–2px colored border with outer glow in the speaker's role color (cyan for PO; orange for the Team2 speaker in `3-1-4`). Role tag chip (rectangle, flat) at top-left overlapping the border. Optional ▼ continue icon. Optional bold heading plus a hint line (`1-2-3`, `3-1-4`). Inline highlighted text in cyan (`Text/Tint`). |
| **Role tag** | Dialogue box | Symbols `title_po/sm/team1/team2`, 83×52. Fill matches the role color. |
| **Click-to-continue hint** | `1-1-1`, `1-2-5` | Outlined cyan pill, 268×52, bold cyan text. |
| **ListPanel** (backlog) | `1-2-x`, `3-1-x` | 524×620 frame: three layered 500×596 backgrounds creating a "stack" depth effect, header 500×100 with title and English subtitle, list area 416×432. Header color: cyan for Product Backlog, yellow for Sprint Backlog (`3-1-4`). |
| **Slot** | Inside ListPanel | 416×96 dashed outline placeholder. Four slots in the Product Backlog (`1-2-3`). |
| **Priority caption** | ListPanel left | 高 / 低 labels with a vertical arrow (380px). |
| **StoryCard** | Floating and in lists | Rounded rectangle, dark teal fill, 2px cyan border; height 60 (one line) or 96 (two lines); widths 226–343 floating. In Sprint lists: a circular **point badge** at left (number 5, 8, 13…) and text 308px wide. |
| **Point badge** | StoryCard | Circle ≈ 48–50px (from screenshot; exact size **[U]**). Cyan fill in Product Backlog, gold fill in Sprint Backlog, number in Highlight style. |
| **Capacity meter** | Sprint panel bottom | Pill bar showing "N / 20 (5人)" (83×22 to 93×22 text). Turns red when over capacity (`21 / 20`). Fill logic **[U]**. |
| **MeetingCard** | `4-1-2`, `4-1-3`, `4-2-x` | Three cards: Daily Scrum (每日站立會議), Sprint Review (短衝檢視會議), Sprint Retrospective (短衝自省會議). Each: illustration (`sprint_daily/review/retro`, 400×188 in 4-1 and 315.8×188 in 4-2), title 200×48, English subtitle, body text 380×277 (300×277 in 4-2). |
| **Retro board** | `5-2-x` | Two question headings ("Q1.做得好的地方?", "Q2.有哪些可以做得更好？") and four role characters (240×238), each with a speech bubble (220-wide text). |
| **Point scale visuals** | `2-2-1`, `2-2-2` | Story cards (195×185), `story_spine` 55×185, clocks `time` (165×165) and `time_1/2/3/5/8/13/21` (110×105), story variants `story_13`, `story_21`. Values: 1, 2, 3, 5, 8, 13, 21. |
| **Planning illustrations** | `2-1-1`–`2-1-3` | `planning_team`, `planning_sprint`, `planning_point`, `sprintPlan`, each 580×580 or 300×300. |
| **Tool logos** | `1-2-2`, `3-1-1`, `4-1-3` | `logo_jira_w` (110×38 in use), `logo_confluence_w` (210×28 in use). |
| **Loading screen** | `loading` | Sprites, bar, footer. |
| **Leaf transition layers** | Between scenes | Assets `bg_leafDark_1..4`, `bg_leafTint_1..4`. See 7.2. |

### 2.3 Roles **[O]**

| Role | Color token | Character (color) | Tag/icon assets |
|---|---|---|---|
| PO (Product Owner) | `Primary/Default` #00FFE0 | Cyan monster | `title_po`, `ic_continue_po` |
| SM (Scrum Master) | `Role/Sm` #D355FF | Purple monster | `title_sm`, `ic_continue_sm` |
| Team1 (Developer) | `Role/Team1` #FFC700 | Yellow monster | `title_team1`, `ic_continue_team1` |
| Team2 (Developer) | `Role/Team2` #FF5C00 | Red monster | `title_team2`, `ic_continue_team2` |

The color-to-character pairing is from the Component board's Role section and the Resource board. **[O]** The Team2 character being the red one is supported by `3-1-4`, where the speaker tag "GG" is orange and the character is red. **[O]**

---

## 3. Design tokens

### 3.1 Color **[O]** (Design System board and `get_variable_defs`)

| Token (Figma name) | Value | Notes |
|---|---|---|
| Primary/Default | `#00FFE0` | |
| Primary/Dark | `#008D96` | |
| Primary/Deepdark | `#005656` | Also used for the board headers. |
| Primary/Linear | Gradient, stops `rgba(0,255,224,0)` 0%, `0.25` 60%, `0.45` 80%, `0.7` 90%, `0.9` 100% | Direction: top to bottom as drawn on the board. |
| Text/Default | `#FFFFFF` | |
| Text/Dark | `#1C3245` | |
| Text/Tint | `#00FFE0` (color) | The variable listing also shows `Text/Tint` as an 18px bold style (see 3.2). Two variables share the name in the dump. |
| Role/Sm | `#D355FF` | |
| Role/Sm_Dark | `#4C0071` | |
| Role/Sm_Tint | `#FF00F5` | |
| Role/Team1 | `#FFC700` | |
| Role/Team2 | `#FF5C00` | |
| Role/Team_Dark | `#933500` | |
| Role/Sm_Linear | `rgba(211,85,255,0)` 0% → `0.05` 60% → `0.2` 80% → `0.6` 100% | |
| Role/Team1_Linear | `rgba(255,199,0,0)` 0% → `0.05` 60% → `0.2` 80% → `0.6` 100% | |
| Role/Team2_Linear | `rgba(255,122,0,0)` 0% → `0.05` 60% → `0.2` 80% → `0.6` 100% | Note: base is `255,122,0`, not `255,92,0` (Role/Team2). **[O]** |
| bg/Dark | `#0A0D14` | |
| bg/Dark60 | `rgba(10,13,20,0.6)` | |
| bg/Transitions | `rgba(28,50,69,0.6)` | The variable dump lists `#1C3245` and drops alpha; the board shows 0.6. |
| Danger/Default | `#FF0000` | |
| Black/100, Black/0 | `#000000`, `#FFFFFF` | |
| Secondary/Default | `#4D4D4D` | In the variable dump; not shown on the board. |
| Gray/40, Gray/White | `#999999`, `#FFFFFF` | In the variable dump; not shown on the board. |
| Text Color / 100%, 87%, 60% | all listed as `#000000` | Opacity values not recoverable from the dump. **[U]** |

Notes:

- There is no `Role/Team2_Dark` or `Role/Team1_Dark`. Only `Role/Team_Dark` (#933500) exists. **[O]**
- Gradient directions beyond "top to bottom as drawn" were not read from the paint data. **[U]**

### 3.2 Typography **[O]**

Font family in variables: **Gen Jyuu Gothic P** (Figma name). The Design System board labels the family "思源柔黑體". `Subtitle` uses **Noto Sans TC**.

| Style (variable name) | Size | Weight | Line height | Letter spacing |
|---|---|---|---|---|
| H2 32px w700 Lh150% | 32 | 700 | 1.5 | 5 |
| H3 24px w500 Lh180% | 24 | 500 | 1.8 | 5 |
| body 20px w500 Lh180% | 20 | 500 | 1.8 | 5 |
| Highlight 20px w700 Lh180% | 20 | 700 | 1.8 | 5 |
| talk_L 24px w500 Lh180% | 24 | 500 | 1.8 | 5 |
| Default/Highlight 18px B (= Text/Tint style) | 18 | 700 | 1.4 | 5 |
| Capation 16px w700 Lh180% | 16 | 700 | **1.4** | 0 |
| Subtitle 14px B (Noto Sans TC) | 14 | 700 | 1.4 | 0 |

Inconsistencies inside the design itself **[O]**, to be resolved before coding:

1. **H2**: the board shows "H2 44px Medium", the variable is 32px Bold.
2. **Highlight**: the board label says "20px 500", the variable is Bold 700 (the sample text renders bold).
3. **Caption**: the board says "16px 500", the variable is Bold 700. The variable name says "Lh180%" but its line height is 1.4.
4. **Letter spacing "5"**: the unit (px or %) is not stated in the dump. In the screenshots, body text has visibly wide tracking. **[U]** Which unit applies must be checked against the Figma text panel.
5. The board only lists a "desktop" set. No tablet or mobile type scale exists. **[O]**

### 3.3 Spacing **[U]/[D]**

The file defines no spacing variables **[O]**. Values below are measured from layers:

| Measure | Value | Basis |
|---|---|---|
| Stage width | 1440 (1920 frame: 1440 centered, 240 inset each side) | **[O]** |
| Progress bar height | 12 | **[O]** |
| Footer height / y | 44 / 980 | **[O]** |
| Standard button size | 188×66 | **[O]** |
| Slot size / list inner size | 416×96 / 416×432 | **[O]** |
| Gap between slots | 16 | **[D]**: (432 − 4×96) ÷ 3 |
| ListPanel size / header height | 524×620 / 100 | **[O]** |
| Dialogue widths | 1007 (sections 1–2), 1080 (3+), 908 (`0-2`, 430 tall) | **[O]** |
| Dialogue padding, card padding, gaps between panels | not measured | **[U]** |

I did not extract an 8-pt (or any) spacing scale because the design does not define one.

### 3.4 Border radius **[U]**

No radius variables exist. From screenshots only:

- Buttons are full pills. **[O]** (visual)
- Dialogue boxes have large radii (visually about 40px at 128–224px height; larger on `0-2`). **[O]** (visual, exact value **[U]**)
- StoryCards and slots have moderate radii (visually ~16–20px). **[O]** (visual, exact value **[U]**)
- Role tag chips are square-cornered. **[O]** (visual)

Exact radii must be read from the node properties when MCP access returns.

### 3.5 Shadow and effects

| Effect | Value | Basis |
|---|---|---|
| `btn_3d` (button) | Drop `#D7D7D766` offset (0,2) blur 8; Drop `#B3B3B366` offset (0,1) blur 5; Inner `#D7D7D733` offset (0,-6) blur 6; Inner `#B3B3B399` offset (0,-2) blur 3; Inner `#D7D7D729` offset (0,2) blur 5 | **[O]** exact |
| Dialogue glow | Cyan (or role-color) outer glow plus 1–2px border | **[O]** visual; blur radius and opacity **[U]** |
| Dialogue / overlay frosted glass | Background blur over scene content (see `1-2-5`, where the list behind is blurred and the screen has a bottom cyan gradient) | **[O]** visual; blur radius **[U]**. Detail lives on page `19:4529`, not inspected. |
| Panel stack depth | Three offset copies of the panel background behind the top one | **[O]** (layer tree) |
| Role character glow | Radial "spray" light around each character (`role_*_light`, 467×454) | **[O]** (assets) |

---

## 4. Responsive behavior

What the design provides **[O]**:

| Breakpoint | Frames | Observed behavior |
|---|---|---|
| `@media 1440px` | 46 screens + loading, 1440×1024 | Reference layout. |
| `@media 1920px` | Only `0-1 start` and `1-2-2` (1920×1080) | A **1440-wide stage stays centered**, with 240px of dark forest background on each side. The logo, button and text sizes are the same as at 1440 (the stage is not scaled). The progress bar spans the full 1920 width. |

Not provided **[O]**:

- No tablet or mobile frames. No breakpoint below 1440.
- No behavior for heights other than 1024 (at 1920 the frame is 1080 tall).
- No definition of what the sides show for the other 44 screens at 1920.

Therefore:

- A **fixed-size stage centered in the viewport** is what the design shows. **[O]**
- Anything smaller than 1440 wide (including mobile) has **no design reference**. This conflicts with the project rule "Support Responsive Design" in `product.md`. A decision is needed (section 10, question 1). I am not inventing a mobile layout. **[A]** only a proposal is possible.
- The 1920 side-area treatment on non-start screens is **[U]**.

---

## 5. Interactive elements and expected behavior

Behavior listed as **[O]** is what the screens directly show. Rules for correct answers are mostly **not stated in the design**. The comments and prototype were not accessible.

| # | Element | Observed behavior | Unknown / not specified |
|---|---|---|---|
| 1 | Loading screen | Bar fills (artboard shows 45.8%); character sprites present; footer. **[O]** | What is loaded; duration; transition out. **[U]** |
| 2 | "進入村莊" (`0-1`) | Navigates to `0-2` by flow order. **[O]** (flow) | Transition animation (leaf layers likely). **[U]** |
| 3 | "接受挑戰" (`0-2`) | Navigates to `1-1-1`. **[O]** (flow) | |
| 4 | Click-to-continue dialogue | ▼ icon + hint "點擊畫面任意處繼續"; clicking anywhere advances (`1-1-1`, `1-2-5`). **[O]** | Whether text types in; keyboard (Space/Enter) support. **[U]** |
| 5 | Dialogue with button | Some screens have a button "準備好了" / "我完成了" / "開始sprint" / "我了解了" instead of click-anywhere. **[O]** | |
| 6 | Drag stories into Product Backlog (`1-2-3`) | Four floating story cards are dragged into four slots, ordered 高 → 低. The `1-2-2` frame shows a demo of this (arrow from a floating card to the first slot, hand cursor, other cards dimmed). **[O]** | Whether there is a "correct" order. No error frame exists for section 1, so validation is **[U]**. |
| 7 | "我完成了" button (`1-2-3`) | Disabled (grey) in the observed state. **[O]** | What enables it (all slots filled is the likely rule). **[A]** |
| 8 | After completion (`1-2-4`/`1-2-5`) | Final order of list: 後台職缺管理功能, 會員系統, 應徵者的線上履歷編輯器, 前台職缺列表、應徵. **[O]** (blurred list in `1-2-5`) | Whether this order is the only accepted one. **[U]** |
| 9 | Drag stories from Product Backlog to Sprint Backlog (`3-1-x`) | Counter "N / 20 (5人)". States: `0/20` (start), `13/20` (not finished), `21/20` (over), `17/20` (done). **[O]** (text) | Rules to pass: see 10. |
| 10 | Over capacity (`3-1-4`) | Dialogue switches to the Team2 speaker with an error message; sprint items get a red border and dark-red fill; counter bar turns red; "開始sprint" button is disabled (grey). **[O]** | Whether the user can drag items back. **[A]** yes. |
| 11 | Meeting cards (`4-2-x`) | The three cards appear in the quiz frames, with hidden layers for each. **[O]** (layer tree) | What the user does with them (match, order, choose). **[U]** |
| 12 | Retro board (`5-2-x`) | Four characters with speech bubbles; two question headings Q1 / Q2. **[O]** (layer tree) | Presumably sorting bubbles into Q1/Q2. **[A]** Not verified. |
| 13 | Wrong-answer states (`4-2-2`, `5-2-2`) | Frames exist. **[O]** | Message and retry behavior. **[U]** |
| 14 | Completion screen (`6-1`) | Congratulation text and four speech bubbles. **[O]** | Any restart / "再玩一次" action. The component board has a "再玩一次" text button, so it likely belongs here. **[A]** |
| 15 | Hover / focus / pressed states | **No frames provided** for buttons, cards or drop targets. **[O]** | All **[U]**. |
| 16 | Top progress bar | Static indicator of section progress. **[O]** | Animated or not. **[U]** |

---

## 6. Assets

### 6.1 Inventory (from the Resource board `19:15327`; sizes from symbol metadata) **[O]**

| Group | Asset | Size | Notes |
|---|---|---|---|
| **Background** | `bg_village` | 1440×1024 | Used on nearly every game screen. Two variants named `bg_village 2` / `3` appear in layer names. **[O]** |
| **Leaf layers (dark)** | `bg_leafDark_1_l`, `_2_b`, `_3_r`, `_4_t` | 794×1024, 777×488, 738×1024, 910×464 | Used on `0-1`, `0-2`, `6-1`. |
| **Leaf layers (tint)** | `bg_leafTint_1_lt`, `_2_lb`, `_3_t`, `_4_rb` | 566×665, 806×343, 693×387, 646×706 | Hidden on `0-2`, visible on `6-1` and `0-1`. |
| **Logo** | `logo_hole_txt`, `logo_hole`, `logo_txt`, `logo_dot_blue/purple/red/yellow` | 1000×736, 1000×736, 600×365, 134–152 | Logo is a raster/illustration, not text. |
| **Favicon** | one cyan dot | small | Shown under `favicon` on the resource board. Source file **[U]**. |
| **Roles** | `role_po`, `role_sm`, `role_team1`, `role_team2` | 320×304 each | Characters. |
| **Role lights** | `role_*_light` (×4) | 467×454 | Glow behind each character. |
| **Hole** | `hole` | 324×83 | Dark ellipse the characters sit on. |
| **Icons** | `ic_continue_po/sm/team1/team2` | 32×28 | Colored triangles. |
| **Role tags** | `title_po/sm/team1/team2` | 83×52 | |
| **Story and points** | `story`, `story_13`, `story_21`, `story_spine`, `time`, `time_1/2/3/5/8/13/21` | 195×185, 55×185, 165×165, 110×105 | Point-scale illustration. |
| **Planning** | `planning_team`, `planning_sprint`, `planning_point`, `sprintPlan` | 580×580, 300×300 | Section 2 illustrations. |
| **Sprint meetings** | `sprint_daily`, `sprint_review`, `sprint_retro` | 615×290 | Section 4. |
| **Partner logos** | `logo_jira_w`, `logo_confluence_w` | 258×89, 210×27 | White variants. |
| **Loading** | `loading` (symbol) | 255×120 | Four character sprites. |
| **GIFs** | animated continue triangles, animated characters | n/a | Under `gif` on the resource board. Format **[U]** (GIF vs sprite sheet vs CSS). |
| **Misc illustrations** | Clock, cube/box, "frames" in orange/red, burst | n/a | "Attached pic" section of the resource board. Use per screen **[U]**. |
| **Link icon** | `link` | 52×62 | Resource board only. Not needed in the app. |

### 6.2 Fonts

| Font | Use | Source |
|---|---|---|
| Gen Jyuu Gothic P (思源柔黑體 on the board) | All text except subtitles | **[U]** Not confirmed available on a standard CDN. Needs a self-hosted subset. |
| Noto Sans TC | `Subtitle` style only | Available through `next/font/google`. **[A]** |

### 6.3 How to obtain the assets **[U]**

- The resource board has a link "大圖切圖檔". Its target is **[U]**: I could not read the hyperlink.
- Exports can be pulled from Figma with `download_assets`, which was not possible once the MCP limit hit.
- Which assets are raster vs vector is **[U]**; the illustrations are textured and are most likely raster. **[A]**

---

## 7. Animation and motion

### 7.1 What is stated **[O]**

The read-me says there are "many dynamic effects" and tells the reader to watch the prototype video. It also says the frosted-glass layers are detailed on page `19:4529`. Neither source was available to me.

### 7.2 What can be inferred from names **[A]**

- **Leaf transitions**: the resource board contains "開頭第一層葉子" and "開頭第二層葉子" (opening first-layer / second-layer leaves). This suggests a two-layer opening animation when entering the village. Timing, direction and trigger are **[U]**.
- **Loading**: animated sprites and a growing bar.
- **Continue icon**: GIF-like pulsing triangle.
- **`bg/Transitions`** color `rgba(28,50,69,0.6)` exists for scene transitions or overlays. **[A]**

No durations, delays or easing curves are known. **[U]**

---

## 8. Suggested component architecture **[A]**

Follows the project structure rules (`src/components/{ui,layout,features}`, `hooks`, `lib`, `types`, `constants`). Server Components by default; Client Components only where noted.

```
src/
├─ app/
│  ├─ layout.tsx            fonts, <html lang="zh-Hant">, global background color
│  ├─ page.tsx              entry (start screen)
│  └─ globals.css           Tailwind v4 @theme tokens (section 9)
├─ components/
│  ├─ ui/
│  │  ├─ Button.tsx            variants: primary | disabled | text  (client only if it holds state)
│  │  ├─ HintPill.tsx          "點擊畫面任意處繼續"
│  │  ├─ RoleTag.tsx           PO | SM | Team1 | Team2
│  │  ├─ ContinueIcon.tsx      ▼ in role colors
│  │  ├─ PointBadge.tsx
│  │  ├─ ProgressBar.tsx       top 12px section progress
│  │  └─ GlassPanel.tsx        translucent, bordered, glow variants by role color
│  ├─ layout/
│  │  ├─ Stage.tsx             1440-wide centered stage, side background
│  │  ├─ SceneBackground.tsx   bg_village / leaf layers
│  │  └─ Footer.tsx            copyright bar (44px)
│  └─ features/
│     ├─ dialogue/   DialogueBox.tsx, RoleCharacter.tsx
│     ├─ backlog/    BacklogPanel.tsx, StoryCard.tsx, DropSlot.tsx, CapacityMeter.tsx
│     ├─ meetings/   MeetingCard.tsx
│     ├─ retro/      RetroBoard.tsx
│     ├─ loading/    LoadingScreen.tsx
│     └─ scenes/     one small component per screen type, composed from the above
├─ hooks/
│  ├─ useSceneFlow.ts          current scene, next/back, section progress
│  ├─ useDragAndDrop.ts        pointer-based drag with drop targets
│  └─ useClickAnywhere.ts      advance on click or key
├─ lib/        validators for each challenge (priority order, sprint capacity), asset helpers
├─ types/      Role, Scene, Story, ChallengeState
└─ constants/  scenes.ts (data-driven scene list), stories.ts, roles.ts
```

Design notes:

- **Data-driven scenes.** The 46 frames repeat a small set of layouts (dialogue only, dialogue + button, backlog challenge, meeting cards, retro board). A `scenes` config avoids 46 hand-written pages. **[A]**
- **Routing is an open question** (section 10, question 4): one route with client state, or a route per section.
- **Drag and drop without a library.** The rules say to avoid unnecessary dependencies. Native Pointer Events are enough for 4 cards and 2–3 lists. **[A]** Touch support depends on the mobile decision.
- **Validators are pure functions** in `lib/`, so the over-capacity and ordering rules are testable. **[A]**
- **React Compiler is on**, so no manual memoization is needed.

---

## 9. Suggested Tailwind design tokens **[A]**

The project uses Tailwind CSS v4 (`tailwindcss` 4.3.3), so tokens go in `@theme` in `src/app/globals.css`. Values below are **[O]** from section 3. The names are my proposal. Spacing and radius are intentionally left out because the design defines none.

```css
@theme {
  /* Primary */
  --color-primary: #00ffe0;
  --color-primary-dark: #008d96;
  --color-primary-deepdark: #005656;

  /* Text */
  --color-text: #ffffff;
  --color-text-dark: #1c3245;
  --color-text-tint: #00ffe0;

  /* Roles */
  --color-role-sm: #d355ff;
  --color-role-sm-dark: #4c0071;
  --color-role-sm-tint: #ff00f5;
  --color-role-team1: #ffc700;
  --color-role-team2: #ff5c00;
  --color-role-team-dark: #933500;

  /* Backgrounds */
  --color-bg-dark: #0a0d14;
  --color-bg-dark60: rgb(10 13 20 / 0.6);
  --color-bg-transition: rgb(28 50 69 / 0.6);

  /* Status */
  --color-danger: #ff0000;

  /* Fonts (family names to be confirmed, see 6.2) */
  --font-sans: "Gen Jyuu Gothic P", "Noto Sans TC", sans-serif;
  --font-subtitle: "Noto Sans TC", sans-serif;

  /* Type scale */
  --text-h2: 32px;      --text-h2--line-height: 1.5;
  --text-h3: 24px;      --text-h3--line-height: 1.8;
  --text-talk: 24px;    --text-talk--line-height: 1.8;
  --text-body: 20px;    --text-body--line-height: 1.8;
  --text-highlight: 18px; --text-highlight--line-height: 1.4;
  --text-caption: 16px; --text-caption--line-height: 1.4;
  --text-subtitle: 14px; --text-subtitle--line-height: 1.4;

  /* Tracking: unit still to be confirmed (see 3.2 item 4). 5 is the Figma value. */
  --tracking-wide-figma: 5px;

  /* Shadow: exact btn_3d recipe */
  --shadow-btn-3d:
    0 2px 8px #d7d7d766,
    0 1px 5px #b3b3b366,
    inset 0 -6px 6px #d7d7d733,
    inset 0 -2px 3px #b3b3b399,
    inset 0 2px 5px #d7d7d729;
}
```

Gradients (Primary/Linear, Role/*_Linear) should be defined as utilities or CSS variables using the stops in 3.1. Direction "top to bottom" is **[U]** until read from the paint data.

Open before finalizing tokens:

- H2 size (32 vs 44) and Highlight/Caption weights (3.2 items 1–3).
- Letter-spacing unit (3.2 item 4).
- Radius scale (3.4) and spacing values (3.3).

---

## 10. Potential implementation challenges and open questions

### 10.1 Challenges

1. **Responsive requirement vs design.** The design only covers 1440 and a 1440 stage on a 1920 canvas. There is no mobile or tablet design (section 4). Scaling the stage with CSS transform is the likely approach, but it is **[A]** and not shown in Figma.
2. **CJK web font.** Gen Jyuu Gothic P covers thousands of glyphs, so a full file is large. A subset is required, and the font source is unconfirmed. Wide letter spacing (5) and 180% line height also affect text fitting in fixed-size panels.
3. **Frosted glass.** `backdrop-filter` blur plus gradient overlays on top of large illustrations, with glow borders per role color. The exact recipe is on page `19:4529` (not inspected). Performance on large backgrounds and Safari support need testing.
4. **Image weight.** Many full-bleed textured illustrations (1440×1024 background, large leaf layers, 4 characters with glow). Needs optimization via `next/image` with attention to the transparent PNG/WebP choice. Original formats **[U]**.
5. **Drag and drop.** Needs pointer-based dragging with drop slots, reordering inside a list, returning items to the source list, dimming of other cards, and a hand cursor. Accessibility (keyboard alternative) is not designed. **[U]**
6. **Fill-level and capacity logic.** Counter `N / 20` plus red state; validation rules per challenge are not in the frames.
7. **Many state variants per challenge.** Each challenge has 4–6 frames (prompt, play, invalid, valid, hint). They map to a state machine, not separate pages.
8. **Animations from the prototype.** Leaf transitions, loading, GIFs. Timings unknown; without the prototype video or an access path they would be guessed.
9. **Size and position differences.** Character size changes from 467×461 to 380×375 between sections; dialogue width changes 1007 → 1080; the speaker side changes per role. These need to be part of scene config, not hard-coded.
10. **Hidden layers.** Several frames contain hidden layers (leaf tints on `0-2`; meeting-card variants on `4-2-x`; `story`/`story_13`/`story_21` on `2-2-2`). Scene components must reproduce only the visible state.
11. **Free-plan MCP limit.** Further Figma reads are blocked for this account until the monthly quota resets or the plan changes.

### 10.2 Inconsistencies found inside the design

1. **Tagline punctuation.** `0-1` at 1440 reads "深入敏捷の村一探究竟" while the 1920 frame reads "深入敏捷の村一探究竟**!**". **[O]**
2. **Intro copy.** The component board sample reads "嗨囉，歡迎進入…", while `0-2` reads "呦呼，歡迎進入…". The screen is treated as the source of truth. **[O]**
3. **Point total in `3-1-5`.** Metadata text shows items 13 and 5 in the Sprint Backlog with the counter "17 / 20". 13 + 5 = 18. **[O]/[D]** I did not view this frame as pixels, so the counter text or one of the item values may be wrong in Figma. Needs confirmation.
4. **Typography labels vs variables** (3.2 items 1–3).
5. **Role/Team2_Linear** uses `255,122,0` while `Role/Team2` is `255,92,0` (3.1). **[O]**

### 10.3 Questions to resolve before implementation

1. Is mobile/tablet in scope? If yes, is a scaled 1440 stage acceptable, or is a separate layout needed?
2. Where is the "大圖切圖檔" asset source, and in what formats?
3. What is the correct answer / pass rule for each challenge (1-2-3, 3-1-x, 4-2-x, 5-2-x)?
4. Single-route client state, or one route per section? (Affects deep links and the back button.)
5. Font source and license for Gen Jyuu Gothic P.
6. Letter-spacing unit, H2 size, and Highlight/Caption weights.
7. Which screen handles "再玩一次" and what does it reset?
8. Hover / focus / disabled states for interactive elements.

---

## 11. Items to re-check once Figma access is available

1. Screens not viewed as pixels: `2-1-1`–`2-2-2`, `3-1-1`, `3-1-2`, `3-1-3`, `3-1-5`, `3-1-6`, all of sections 4, 5 and 6, and `1-2-2` / `1-2-4` at 1440.
2. Page `19:4529` (frosted-glass breakdown) and page `0:1` (flow chart, wireframe, user stories).
3. Figma comments (annotations).
4. Radius, padding, gap and blur values via node properties or `get_design_context` on key components (Button, DialogueBox, StoryCard, ListPanel, CapacityMeter).
5. Gradient directions, point-badge size, capacity-meter fill logic.
6. Asset export (`download_assets`) and file formats.
