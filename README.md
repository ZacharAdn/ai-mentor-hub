# מדריכי לימוד אינטראקטיביים

אוסף מדריכים אינטראקטיביים בעברית ובאנגלית עבור סטודנטים בתחומי ML/AI, DevOps, וכלי פיתוח. כל מדריך הוא קובץ HTML עצמאי (כל ה-CSS וה-JS פנימה), ללא תהליך build וללא תלויות.

## איך לצפות

פשוט פתחו כל קובץ `.html` בדפדפן — אין צורך בשרת או בהתקנה.

```bash
open confusion-matrix-explorer.html   # macOS
start confusion-matrix-explorer.html  # Windows
```

לחלופין, אפשר לפרוס את הריפו ב-GitHub Pages ולגשת ישירות מהדפדפן.

## המדריכים

### מושגי ML/AI אינטראקטיביים

| מדריך | נושא |
|-------|------|
| [logistic-regression.html](logistic-regression.html) | Logistic Regression — סליידרים חיים וגרפי scatter |
| [decision-tree.html](decision-tree.html) | Decision Tree ו-Overfitting — סליידר עומק עץ |
| [confusion-matrix-explorer.html](confusion-matrix-explorer.html) | Confusion Matrix, Precision, Recall — סליידר סף החלטה |
| [cnn.html](cnn.html) | Convolutional Neural Networks — דיאגרמות מונפשות |
| [llm-guide.html](llm-guide.html) | יסודות Large Language Models |
| [llm-guide-reference.html](llm-guide-reference.html) | LLM — מדריך עומק (אלי) |
| [omer-concepts-guide.html](omer-concepts-guide.html) | VIF, Feature Engineering, Stacking, RAG, QLoRA (עומר) |

### ארכיטקטורה ו-Production

| מדריך | נושא |
|-------|------|
| [fullstack-data-flow.html](fullstack-data-flow.html) | זרימת נתונים בארכיטקטורת full-stack |
| [demo-to-production-itay.html](demo-to-production-itay.html) | מ-demo ל-production (איתי) |
| [production-readiness-explorer.html](production-readiness-explorer.html) | מסגרת 7 ממדים לבשלות production |
| [i24-three-pillars.html](i24-three-pillars.html) | פירוק פרויקט i24 לשלושה עמודים |
| [i24-timeseries-deep-dive.html](i24-timeseries-deep-dive.html) | חקירת time-series ב-i24 |

### כלים והתקנה

| מדריך | נושא |
|-------|------|
| [index.html](index.html) | התקנת Claude Code ל-Windows |
| [claude-code-installation-guide.html](claude-code-installation-guide.html) | התקנת Claude Code — Windows, Mac ו-VS Code |
| [git-github-setup.html](git-github-setup.html) | מאפס ל-Push הראשון — GitHub signup, Git install, config, ו-commit/push דרך VS Code UI |
| [technion-lbs-setup.html](technion-lbs-setup.html) | הגדרת סביבת פיתוח Technion LBS |
| [whatsapp-setup.html](whatsapp-setup.html) | התקנת WhatsApp Skill |
| [hebrew-terminal-fix.html](hebrew-terminal-fix.html) | תיקון תצוגת עברית ב-terminal של Windows |
| [self-improving-skills-hooks.html](self-improving-skills-hooks.html) | Claude Code Skills ו-Hooks |
| [openclaw-guide.html](openclaw-guide.html) | הפניה למדריך OpenClaw |
| [links.html](links.html) | אוסף קישורים חיצוניים |

## תוספת מדריך חדש

הדרך המהירה: הריצו את הסקיל `/teaching-html` בתוך Claude Code עם נושא המדריך, והוא יבנה דראפט שתואם לסגנון הריפו.

ידנית: העתיקו מדריך קיים שדומה בסוג האינטראקציה (לדוגמה `confusion-matrix-explorer.html` למושג ML עם סליידרים), שנו את התוכן, ושמרו על:

- `<html lang="he" dir="rtl">` ועל מתג שפה HE/EN.
- פונט Heebo מ-Google Fonts.
- פלטת הצבעים הקיימת (רקע כהה, gradients סגול/אינדיגו/ורוד).
- JS וונילה בלבד — Canvas/SVG, ללא frameworks.
- קובץ אחד עצמאי — בלי לחלץ CSS או JS משותפים.

לאחר היצירה, הוסיפו לינק ב-`index.html` או ב-`links.html` לפי ההקשר.

## מבנה הריפו

```
.
├── *.html              # המדריכים — כל קובץ עצמאי לחלוטין
├── gifs/               # screenshots ו-GIFs (משמשים את claude-code-installation-guide.html)
├── .claude/            # הגדרות Claude Code לפרויקט + סקיל learn מקומי
└── .mcp.json           # רישום Playwright MCP לוולידציה דרך דפדפן
```

## הערות סגנון

- עברית — שפת בסיס לטקסט מול הסטודנט. מונחים טכניים (Python, gradient, regression, RAG וכו') נשארים באנגלית גם בתוך משפטים בעברית.
- אנגלית — לקוד, identifiers, ושמות ספריות.
- כל מדריך עצמאי — שינויים בקובץ אחד לא משפיעים על קבצים אחרים, וזה במכוון.
