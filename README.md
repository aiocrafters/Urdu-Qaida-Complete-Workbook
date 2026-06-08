# Urdu Qaida Workbook Generator (اردو قاعدہ ورک بک)

A beautifully formatted, printable Urdu alphabet learning and practice workbook (`حروفِ تہجی مشق کتاب`) covering the entire Urdu alphabet from Alif to Bari Yay (`الف` سے `ے` تک). Designed specifically for children and beginners, this workbook offers structured tracing, guided writing, and free-hand cursive writing practice.

🔗 **GitHub Repository:** [aiocrafters/Urdu-Qaida-Complete-Workbook](https://github.com/aiocrafters/Urdu-Qaida-Complete-Workbook.git)

---

## 🎨 Visual Overview & Page Structure

Each letter is allocated a dedicated A4-sized practice page with a consistent, distraction-free grid layout.

```
+---------------------------------------------------------+
|                لکھائی کی بنیادی مشقیں                  |  <- Page Header
+------------------+-------------------+------------------+
|      [ک]         |   [Book Image]    |     کتاب         |  <- Letter Card Row (RTL)
|  (Large Letter)  |                   |  (Example Word)  |
+------------------+-------------------+------------------+
|  حرف ٹریس کریں                                          |  <- Tracing Section Title
|  [ ? ] [ ? ] [ ? ] [ ? ] [ ? ] [ ? ] [ ? ]             |  <- Tracing Grid (Row 1)
|  [ ? ] [ ? ] [ ? ] [ ? ] [ ? ] [ ? ] [ ? ]             |  <- Tracing Grid (Row 2)
+---------------------------------------------------------+
|  باکس میں لکھیں                                         |  <- Guided Writing Title
|  [ ک ] [ ک ] [ ک ] [ ک ] [ ک ] [ ک ] [ ک ]             |  <- Guided Grid (Row 1)
|  [ ک ] [ ک ] [ ک ] [ ک ] [ ک ] [ ک ] [ ک ]             |  <- Guided Grid (Row 2)
|  [ ک ] [ ک ] [ ک ] [ ک ] [ ک ] [ ک ] [ ک ]             |  <- Guided Grid (Row 3)
+---------------------------------------------------------+
|                      آزادانہ مشق                         |  <- Independent Title
|  _____________________________________________________  |  
|  _____________________________________________________  |  <- 5 Cursive Practice Lines
|  _____________________________________________________  |  
+---------------------------------------------------------+
|                        حرف ک                            |  <- Page Footer
+---------------------------------------------------------+
```

---

## ✨ Features & Functional Details

1. **Cover Page**: A minimal, elegant cover page featuring large traditional Urdu typography:
   - **Main Title**: `اردو قاعدہ` (Urdu Qaida)
   - **Subtitle**: `حروفِ تہجی مشق کتاب` (Alphabet Practice Workbook)
   - **Range Indicator**: `الف سے ے تک` (Alif to Bari Yay)

2. **Educational Illustration Assets**:
   - Includes **37 educational illustrations** located in the `images/` directory.
   - Each letter has a custom cartoon/vector-style graphic that matches the example word (e.g., `ب` with `images/bay-bakri.png` for Goat, `ف` with `images/fay-fawwara.png` for Fountain).
   - If an image fails to load, a fallback placeholder service dynamic URL is used to prevent layout breakages.

3. **Single Dotted Tracing (حرف ٹریس کریں)**:
   - Contains **14 square boxes** (2 rows of 7) per page.
   - Features the letter rendered in **single dotted lines** (rather than standard font outline tracks) to help students trace the exact stroke paths of letters correctly.

4. **Guided Writing (باکس میں لکھیں)**:
   - Contains **21 square boxes** (3 rows of 7) per page.
   - Displays a very light gray letter template in the center of the box to act as a visual baseline and structure guide for self-writing.

5. **Independent Cursive Writing (آزادانہ مشق)**:
   - Includes **10 wide, ruled lines** at the bottom of the page, allowing free-hand practice of connecting letters, writing full words, or practicing cursive strokes.

6. **Fully Printable**:
   - Optimized with A4 physical dimensions (`210mm x 297mm`) and specific print stylesheets (`@media print`).
   - Automatically handles pagination, breaks pages cleanly between letters (`page-break-after: always`), and strips browser background colors/gray templates for a crisp black-and-white print.

---

## 🛠️ Technical Implementation & Custom CSS Fixes

Developing clean calligraphic layouts in web browsers presents unique challenges for Arabic-script languages like Urdu. The project employs custom design systems to overcome these:

### 1. The Nastaliq "Double-Outline" Tracing Fix
- **Problem**: Traditional Nastaliq fonts (like *Noto Nastaliq Urdu*) have wide, calligraphic glyph forms. When styled with a stroke in SVG, they render double outlines (outer and inner bounds of the pen stroke), which is confusing for early writers.
- **Solution**: Tracing and guided writing grids import and use `Noto Sans Arabic` (Naskh style) with `font-weight: 100`. The thin glyph profiles converge when stroked, creating a clean, single dotted line using:
  ```css
  stroke-width: 2px;
  stroke-dasharray: 4 5;
  ```

### 2. RTL SVG Centering Shift Fix
- **Problem**: Under Right-to-Left documents (`dir="rtl"`), browser render engines shift text anchors in SVGs dynamically, moving letters to the right margin of the box.
- **Solution**: The layout overrides the SVG text element's direction and overrides standard bidi behavior:
  ```css
  text-anchor: middle;
  dominant-baseline: central;
  direction: ltr;
  unicode-bidi: bidi-override;
  ```
  This centers the Urdu character mathematically in the absolute center (`x="50%" y="48%"`) of the SVG viewport.

### 3. Aspect Ratio and Grid Alignment
- **Problem**: CSS Grid layouts default to stretching cells to fit rows, which deforms writing boxes into rectangles on wide screens.
- **Solution**: Tracing and stroke grids employ:
  ```css
  align-items: start;
  ```
  Coupled with grid cells styled with `aspect-ratio: 1 / 1` and `width: 100%`, this ensures that every writing box is a perfect square under all viewport sizes.

### 4. Nastaliq Descender & Overhang Clipping Fix
- **Problem**: Extended descenders on Urdu characters (`ب, پ, ج, چ, ح, خ, س, ش, ص, ض, ع, غ, ق, ل, م, ن, ی`) and wide/slanted strokes (`ک, گ`) frequently clip past the boundaries of container blocks due to tight line-heights.
- **Solution**:
  - Expanded the line-height of `.col-right` to `1.4`.
  - Added a safety padding offset (`padding-right: 20px`) to prevent Nastaliq calligraphic sweeps from overlapping or clipping on the right edge.

---

## 📖 Alphabet Dictionary (حروفِ تہجی ڈکشنری)

Below is the dictionary map implemented in the workbook generator:

| Letter (حرف) | Word (لفظ) | Meaning | Image Asset |
| :---: | :---: | :---: | :--- |
| **ا** | انار | Pomegranate | `images/alif-anar.png` |
| **ب** | بکری | Goat | `images/bay-bakri.png` |
| **پ** | پتنگ | Kite | `images/pay-patang.png` |
| **ت** | تتلی | Butterfly | `images/tay-titli.png` |
| **ٹ** | ٹماٹر | Tomato | `images/ttay-tamatar.png` |
| **ث** | ثواب | Reward (spiritual) | `images/say-sawab.png` |
| **ج** | جہاز | Airplane / Ship | `images/jeem-jahaz.png` |
| **چ** | چڑیا | Sparrow | `images/chay-chiria.png` |
| **ح** | حلوہ | Halwa (Sweet) | `images/hay-halwa.png` |
| **خ** | خرگوش | Rabbit | `images/khay-rabbit.png` |
| **د** | درخت | Tree | `images/daal-tree.png` |
| **ڈ** | ڈبہ | Box | `images/ddaal-box.png` |
| **ذ** | ذرا | Particle / Tiny | `images/za.png` |
| **ر** | رنگ | Paint / Color | `images/ray-rang.png` |
| **ڑ** | گاڑی | Car (Letter is middle/end) | `images/rray-car.png` |
| **ز** | زمین | Earth / Ground | `images/zay-earth.png` |
| **ژ** | ژالہ | Hailstorm | `images/zhay-dew.png` |
| **س** | سیب | Apple | `images/seen-apple.png` |
| **ش** | شیر | Lion | `images/sheen-lion.png` |
| **ص** | صابن | Soap | `images/suad-soap.png` |
| **ض** | ضیافت | Feast / Banquet | `images/zuad-feast.png` |
| **ط** | طوطا | Parrot | `images/toay-parrot.png` |
| **ظ** | ظرف | Vessel / Bowl | `images/zoay-bowl.png` |
| **ع** | عینک | Glasses | `images/ain-glasses.png` |
| **غ** | غبارہ | Balloon | `images/ghain-balloon.png` |
| **ف** | فوارہ | Fountain | `images/fay-fawwara.png` |
| **ق** | قلم | Pen | `images/qaaf-pen.png` |
| **ک** | کتاب | Book | `images/kaaf-book.png` |
| **گ** | گلاب | Rose | `images/gaaf-rose.png` |
| **ل** | لیموں | Lemon | `images/laam-lemon.png` |
| **م** | مچھلی | Fish | `images/meem-fish.png` |
| **ن** | نارنگی | Orange | `images/noon-orange.png` |
| **و** | ورزش | Exercise | `images/wow-warzish.png` |
| **ہ** | ہاتھی | Elephant | `images/hay-elephant.png` |
| **ء** | ہمزہ | Hamza (glottal stop) | `images/hamza.png` |
| **ی** | یاقوت | Ruby | `images/yay-ruby.png` |
| **ے** | بڑی ے | Bari Yay (Grammatical ending)| `images/bariyay.png` |

---

## 🚀 How to Run and Print

### 1. Clone the Repository
Clone this repository to your local machine:
```bash
git clone https://github.com/aiocrafters/Urdu-Qaida-Complete-Workbook.git
cd Urdu-Qaida-Complete-Workbook
```

### 2. View Locally
To prevent image loading blockages due to local file origins, host the directory using any static web server.
Using Python:
```powershell
python -m http.server 8000
```
Then, open your web browser and navigate to:
```
http://localhost:8000/index.html
```

### 3. Export / Print to PDF
1. Open the page in your browser (Chrome/Edge recommended).
2. Press `Ctrl + P` (or Cmd + P on macOS) to open the print dialog.
3. Set **Destination** to `Save as PDF`.
4. Under **More Settings**:
   - Set **Paper size** to `A4`.
   - Set **Margins** to `None` or `Minimum` (the page container has a built-in `15mm` margin suitable for binder holes).
   - Ensure **Background graphics** is checked (this displays the light gray guided letters and illustration borders).
5. Click **Save** to export your premium Urdu Qaida Workbook!
