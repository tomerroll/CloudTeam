# 🔍 Web Document Search Engine

מערכת פשוטה לחיפוש מסמכים מאתרי אינטרנט, הכוללת אינדוקס, חיפוש בוליאני (AND/OR), ודירוג תוצאות.

---

## 🧱 Architecture

1. **DocumentFetcher** – שואב מסמכים מהאינטרנט (HTML → טקסט).
2. **TextProcessor** – מעבד טקסט, מבצע ניקוי מילים נפוצות ולממטיזציה.
3. **Indexer** – בונה אינדקס הפוך: מונח → רשימת מזהי מסמכים.
4. **FirebaseUploader** – מעלה את האינדקס ל־Firebase.
5. **LogicalSearch** – תומך בחיפושי `AND` / `OR` ומדרג מסמכים.
6. **Coordinator** – מתזמן את כל התהליך ומנהל ממשק משתמש קונסול.

---

## 🛠 Service Documentation

### 🧾 `DocumentFetcher.fetch()`  
- **קלט**: רשימת URLים  
- **פלט**: מילון של מזהה מסמך לתוכן טקסטואלי

### 🔤 `TextProcessor.process(docs)`  
- **קלט**: מילון מסמכים  
- **פלט**: מילון ספירת מילים לאחר ניקוי ועיבוד

### 📚 `Indexer.build_index(docs)`  
- **פלט**: אינדקס הפוך – term → {count, DocIDs}

### ☁ `FirebaseUploader.upload(index, doc_map)`  
- **פלט**: הצלחה / כשלון בהעלאה

### 🔎 `LogicalSearch.search(query)`  
- **קלט**: שאילתה בוליאנית (לדוגמה: `"mqtt AND broker"`)  
- **פלט**: מסמכים תואמים + דירוג

---

## 💡 Usage Example

```bash
# הפעלת המנוע
python search_engine.py

🔎 Enter search query (AND/OR), or 'exit': mqtt AND broker
📄 Matching documents:
🔹 https://mqtt.org/getting-started/ (Score: 2)
🔹 https://mqtt.org/faq/ (Score: 1)
