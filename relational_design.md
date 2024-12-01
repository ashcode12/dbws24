Write SQL CREATE TABLE Scripts**
### **1. Benutzer (Users)**
```sql
CREATE TABLE Benutzer (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Email VARCHAR(100) UNIQUE NOT NULL,
    Ernährungspräferenz VARCHAR(50), -- e.g., vegan, gluten-free
    Erstellt_Am TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### **2. Mahlzeiten (Meals)**
```sql
CREATE TABLE Mahlzeiten (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Benutzer_ID INT NOT NULL, -- FK to Benutzer
    Rezept_ID INT NOT NULL, -- FK to Rezepte
    Datum DATE NOT NULL, -- Planned date for the meal
    FOREIGN KEY (Benutzer_ID) REFERENCES Benutzer(ID),
    FOREIGN KEY (Rezept_ID) REFERENCES Rezepte(ID)
);
```

### **3. Rezepte (Recipes)**
```sql
CREATE TABLE Rezepte (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Kategorie_ID INT NOT NULL, -- FK to Kategorien
    Zubereitungszeit INT NOT NULL, -- Preparation time in minutes
    Anleitung TEXT NOT NULL, -- Recipe instructions
    Erstellt_Am TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (Kategorie_ID) REFERENCES Kategorien(ID)
);
```

### **4. Kategorien (Categories)**
```sql
CREATE TABLE Kategorien (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(50) NOT NULL,
    Beschreibung TEXT -- Optional description of the category
);
```

### **5. Zutaten (Ingredients)**
```sql
CREATE TABLE Zutaten (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Name VARCHAR(100) NOT NULL,
    Ist_Allergen BOOLEAN DEFAULT FALSE, -- Whether the ingredient is an allergen
    Kalorien_Pro_Einheit DECIMAL(10, 2) NOT NULL, -- Calories per 100g
    Erstellt_Am TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### **6. RezeptZutaten (Recipe-Ingredients Junction Table)**
```sql
CREATE TABLE RezeptZutaten (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Rezept_ID INT NOT NULL, -- FK to Rezepte
    Zutat_ID INT NOT NULL, -- FK to Zutaten
    Menge DECIMAL(10, 2) NOT NULL, -- Quantity in grams
    FOREIGN KEY (Rezept_ID) REFERENCES Rezepte(ID),
    FOREIGN KEY (Zutat_ID) REFERENCES Zutaten(ID)
);
```

### **7. Nährstoffprotokolle (Nutrition Logs)**
```sql
CREATE TABLE Nährstoffprotokolle (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Benutzer_ID INT NOT NULL, -- FK to Benutzer
    Datum DATE NOT NULL, -- Log date
    Kalorien_Gesamt DECIMAL(10, 2) NOT NULL, -- Total calories consumed on the date
    FOREIGN KEY (Benutzer_ID) REFERENCES Benutzer(ID)
);
```

### **8. Bewertungen (Ratings)**
```sql
CREATE TABLE Bewertungen (
    ID INT AUTO_INCREMENT PRIMARY KEY,
    Benutzer_ID INT NOT NULL, -- FK to Benutzer
    Rezept_ID INT NOT NULL, -- FK to Rezepte
    Bewertung INT CHECK (Bewertung BETWEEN 1 AND 5), -- Rating (1-5)
    Text TEXT, -- Optional feedback text
    Erstellt_Am TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (Benutzer_ID) REFERENCES Benutzer(ID),
    FOREIGN KEY (Rezept_ID) REFERENCES Rezepte(ID)
);
```

---

### **Save and Test the Scripts**
1. Save the scripts in a `.sql` file.
2. Test in a MySQL database:
   - Run each `CREATE TABLE` statement.
   - Use `SHOW TABLES;` and `DESCRIBE TableName;` to verify the structure.

---
