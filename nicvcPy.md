[[cmd-and-deploy]]

adb -s R9ZY40RDV0K install -r "c:\Users\parth\Desktop\maui\nicvc-basetwo-git\NICVC\bin\Release\net8.0-android\com.companyname.nicvc-Signed.apk"

adb -s R9ZY40RDV0K logcat -c

adb -s R9ZY40RDV0K shell am start -n com.companyname.nicvc/crc64a73e961ec6240ec4.MainActivity

adb -s R9ZY40RDV0K logcat -d -s "AndroidRuntime:E" "mono:E" "mono-rt:E" "DOTNET:E" "*:F"

```txt
. : File C:\Users\parth\Documents\WindowsPowerShell\profile.ps1 cannot be loaded because running scripts is disabled 
on this system. For more information, see about_Execution_Policies at https:/go.microsoft.com/fwlink/?LinkID=135170.
At line:1 char:3
+ . 'C:\Users\parth\Documents\WindowsPowerShell\profile.ps1'
+   ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : SecurityError: (:) [], PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess
--------- beginning of crash
10-27 12:46:36.343 30454 30454 F libc    : Fatal signal 6 (SIGABRT), code -1 (SI_QUEUE) in tid 30454 (mpanyname.nicvc), pid 30454 (mpanyname.nicvc)
10-27 12:46:36.713 30492 30492 F DEBUG   : *** *** *** *** *** *** *** *** *** *** *** *** *** *** *** ***
10-27 12:46:36.713 30492 30492 F DEBUG   : Build fingerprint: 'samsung/a06xddins/a06x:15/AP3A.240905.015.A2/M066BXXS2AYD2_ODM2AYD2:user/release-keys'
10-27 12:46:36.713 30492 30492 F DEBUG   : Revision: '5'
10-27 12:46:36.713 30492 30492 F DEBUG   : ABI: 'arm64'
10-27 12:46:36.713 30492 30492 F DEBUG   : Processor: '7'
10-27 12:46:36.713 30492 30492 F DEBUG   : Timestamp: 2025-10-27 12:46:36.439507137+0530
10-27 12:46:36.713 30492 30492 F DEBUG   : Process uptime: 2s
10-27 12:46:36.713 30492 30492 F DEBUG   : Cmdline: com.companyname.nicvc
10-27 12:46:36.713 30492 30492 F DEBUG   : pid: 30454, tid: 30454, name: mpanyname.nicvc  >>> com.companyname.nicvc <<<
10-27 12:46:36.713 30492 30492 F DEBUG   : uid: 10646
10-27 12:46:36.713 30492 30492 F DEBUG   : tagged_addr_ctrl: 0000000000000001 (PR_TAGGED_ADDR_ENABLE)
10-27 12:46:36.713 30492 30492 F DEBUG   : signal 6 (SIGABRT), code -1 (SI_QUEUE), fault addr --------
10-27 12:46:36.713 30492 30492 F DEBUG   :     x0  0000000000000000  x1  00000000000076f6  x2  0000000000000006  x3  0000007fe7af9580
10-27 12:46:36.713 30492 30492 F DEBUG   :     x4  6e6d6e6c2e627172  x5  6e6d6e6c2e627172  x6  6e6d6e6c2e627172  x7  7f7f7f7f7f7f7f7f
10-27 12:46:36.713 30492 30492 F DEBUG   :     x8  00000000000000f0  x9  00000072cacdbdf8  x10 0000000000000001  x11 00000072cad61950
10-27 12:46:36.713 30492 30492 F DEBUG   :     x12 0000007fe7af8380  x13 0000000000000000  x14 0000007fe7af8430  x15 000006de62bfef37
10-27 12:46:36.713 30492 30492 F DEBUG   :     x16 00000072cadcccd8  x17 00000072cadb5300  x18 00000072de3c8000  x19 00000000000076f6
10-27 12:46:36.713 30492 30492 F DEBUG   :     x20 00000000000076f6  x21 00000000ffffffff  x22 b400007180ea0000  x23 000000718718f27d
10-27 12:46:36.713 30492 30492 F DEBUG   :     x24 000000718718f27c  x25 0000000000000001  x26 0000007188f4bdd0  x27 00000071959d5000
10-27 12:46:36.713 30492 30492 F DEBUG   :     x28 00000072de072940  x29 0000007fe7af9600
10-27 12:46:36.713 30492 30492 F DEBUG   :     lr  00000072cad4a0f8  sp  0000007fe7af9560  pc  00000072cad4a124  pst 0000000000001000
10-27 12:46:36.713 30492 30492 F DEBUG   : 9 total frames
10-27 12:46:36.713 30492 30492 F DEBUG   : backtrace:
10-27 12:46:36.713 30492 30492 F DEBUG   :       #00 pc 0000000000097124  /apex/com.android.runtime/lib64/bionic/libc.so (abort+164) (BuildId: 6f50e1cb8b600671d500c84e03f5b42b)
10-27 12:46:36.713 30492 30492 F DEBUG   :       #01 pc 000000000001f360  /data/app/~~6dy6bzLCU3HSuLDbWZh73A==/com.companyname.nicvc-5qOo5JAJV-ypDXTBNVNV8Q==/lib/arm64/libmonodroid.so (xamarin::android::Helpers::abort_application()+8) (BuildId: d91b235af6fe3c57fcd47accb366aa74c34c2c4d)
10-27 12:46:36.713 30492 30492 F DEBUG   :       #02 pc 0000000000035660  /data/app/~~6dy6bzLCU3HSuLDbWZh73A==/com.companyname.nicvc-5qOo5JAJV-ypDXTBNVNV8Q==/lib/arm64/libmonodroid.so (xamarin::android::internal::MonodroidRuntime::mono_log_handler(char const*, char const*, char const*, int, void*)+144) (BuildId: d91b235af6fe3c57fcd47accb366aa74c34c2c4d)
10-27 12:46:36.714 30492 30492 F DEBUG   :       #03 pc 00000000001c88e8  /data/app/~~6dy6bzLCU3HSuLDbWZh73A==/com.companyname.nicvc-5qOo5JAJV-ypDXTBNVNV8Q==/lib/arm64/libmonosgen-2.0.so (BuildId: cba0f59e879f66d4c75e1c207e9b7bbef7b0f723)
10-27 12:46:36.714 30492 30492 F DEBUG   :       #04 pc 00000000001c89fc  /data/app/~~6dy6bzLCU3HSuLDbWZh73A==/com.companyname.nicvc-5qOo5JAJV-ypDXTBNVNV8Q==/lib/arm64/libmonosgen-2.0.so (BuildId: cba0f59e879f66d4c75e1c207e9b7bbef7b0f723)
10-27 12:46:36.714 30492 30492 F DEBUG   :       #05 pc 000000000013d5c8  /data/app/~~6dy6bzLCU3HSuLDbWZh73A==/com.companyname.nicvc-5qOo5JAJV-ypDXTBNVNV8Q==/lib/arm64/libmonosgen-2.0.so (BuildId: cba0f59e879f66d4c75e1c207e9b7bbef7b0f723)
10-27 12:46:36.714 30492 30492 F DEBUG   :       #06 pc 000000000013c2c8  /data/app/~~6dy6bzLCU3HSuLDbWZh73A==/com.companyname.nicvc-5qOo5JAJV-ypDXTBNVNV8Q==/lib/arm64/libmonosgen-2.0.so (BuildId: cba0f59e879f66d4c75e1c207e9b7bbef7b0f723)
10-27 12:46:36.714 30492 30492 F DEBUG   :       #07 pc 000000000014d63c  /data/app/~~6dy6bzLCU3HSuLDbWZh73A==/com.companyname.nicvc-5qOo5JAJV-ypDXTBNVNV8Q==/lib/arm64/libmonosgen-2.0.so (BuildId: cba0f59e879f66d4c75e1c207e9b7bbef7b0f723)
10-27 12:46:36.714 30492 30492 F DEBUG   :       #08 pc 0000000000004f00  <anonymous:72d67c9000>
```









adb -s R9ZY40RDV0K logcat -d | Select-String -Pattern "Assertion|GUID|unusable" -Context 2,2

dotnet nuget locals all --clear






















dotnet build -c Release -f net8.0-android
py collection & uibypass 

# **Understanding the Database System (C# vs Python)**

## **1. How Databases Are Created**

### **C# (Your MAUI App):**
```csharp
public class TodayVcDatabase
{
    private SQLiteConnection conn;
    
    public TodayVcDatabase()
    {
        // Connect to database file
        conn = DatabaseHelper.GetConnection("TodayVc.db3");
        
        // Create table if it doesn't exist
        conn.CreateTable<TodayVc>();
    }
}
```

### **Python Equivalent:**
```python
import sqlite3

class TodayVcDatabase:
    def __init__(self):
        # Connect to database file (creates if doesn't exist)
        self.conn = sqlite3.connect("TodayVc.db3")
        
        # Create table if it doesn't exist
        self.conn.execute("""
            CREATE TABLE IF NOT EXISTS TodayVc (
                VC_ID TEXT,
                DateofVC TEXT,
                Startingtime TEXT,
                Important TEXT,
                VCStatus TEXT,
                ...
            )
        """)
```

---

## **2. The Database Structure (Xamarin vs MAUI)**

### **OLD (Xamarin) - One Big Database:**
```python
# ONE database file with ALL tables
database = sqlite3.connect("app.db")

# All tables in same file:
database.execute("CREATE TABLE TodayVc (...)")
database.execute("CREATE TABLE ImportantVc (...)")
database.execute("CREATE TABLE Dashboard (...)")

# Can query any table from same connection:
results = database.execute("SELECT * FROM TodayVc WHERE Important='Y'")
```

### **NEW (MAUI) - Separate Database Files:**
```python
# MULTIPLE database files, each with ONE table

# TodayVc.db3
todayvc_db = sqlite3.connect("TodayVc.db3")
todayvc_db.execute("CREATE TABLE TodayVc (...)")

# ImportantVc.db3  
importantvc_db = sqlite3.connect("ImportantVc.db3")
importantvc_db.execute("CREATE TABLE ImportantVc (...)")

# Dashboard.db3
dashboard_db = sqlite3.connect("Dashboard.db3")
dashboard_db.execute("CREATE TABLE Dashboard (...)")

# ❌ WRONG - Can't query TodayVc from ImportantVc connection!
results = importantvc_db.execute("SELECT * FROM TodayVc")  # ERROR!

# ✅ RIGHT - Use correct database connection
results = todayvc_db.execute("SELECT * FROM TodayVc")  # Works!
```

---

## **3. The Bug That Was Fixed**

### **What Was Happening (Python analogy):**

```python
# ImportantVcPage.py (BEFORE FIX)

class ImportantVcPage:
    def __init__(self):
        # ❌ Opening ImportantVc.db3 connection
        self.database = sqlite3.connect("ImportantVc.db3")
        
        # ❌ But trying to query TodayVc table!
        query = "SELECT * FROM TodayVc WHERE Important='Y'"
        
        # 💥 CRASH! TodayVc table doesn't exist in ImportantVc.db3
        results = self.database.execute(query)
        # SQLite.SQLiteException: no such table: TodayVc
```

**Why it crashed:**
- Opened `ImportantVc.db3` database
- That database only has the [ImportantVc](cci:2://file:///c:/Users/parth/Desktop/maui/nicvc-basetwo-git/NICVC/Model/ImportantVc.cs:2:4-31:5) table
- Tried to query [TodayVc](cci:2://file:///c:/Users/parth/Desktop/maui/nicvc-basetwo-git/NICVC/Model/TodayVc.cs:2:4-35:5) table
- Table doesn't exist in that database → **CRASH!**

### **The Fix (Python analogy):**

```python
# ImportantVcPage.py (AFTER FIX)

class ImportantVcPage:
    def __init__(self):
        # ✅ Opening TodayVc.db3 connection
        self.database = sqlite3.connect("TodayVc.db3")
        
        # ✅ Querying TodayVc table (exists in this database!)
        query = "SELECT * FROM TodayVc WHERE Important='Y'"
        
        # ✅ Works! TodayVc table exists in TodayVc.db3
        results = self.database.execute(query)
        
        # Convert to list of dictionaries
        data = []
        for row in results:
            data.append({
                'VC_ID': row[0],
                'DateofVC': row[1],
                'Startingtime': row[2],
                'Important': row[3],
                ...
            })
```

---

## **4. Complete Flow (Python Example)**

```python
# ========================================
# STEP 1: Define Data Models (Classes)
# ========================================

class TodayVc:
    """Represents a video conference record"""
    def __init__(self):
        self.VC_ID = ""
        self.DateofVC = ""
        self.Startingtime = ""
        self.Important = ""  # 'Y' or 'N'
        self.VCStatus = ""
        self.Purpose = ""
        # ... more fields

# ========================================
# STEP 2: Database Class
# ========================================

class TodayVcDatabase:
    def __init__(self):
        # Open/create database file
        self.conn = sqlite3.connect("TodayVc.db3")
        self.create_table()
    
    def create_table(self):
        """Create table if it doesn't exist"""
        self.conn.execute("""
            CREATE TABLE IF NOT EXISTS TodayVc (
                VC_ID TEXT,
                DateofVC TEXT,
                Startingtime TEXT,
                Important TEXT,
                VCStatus TEXT,
                Purpose TEXT
            )
        """)
        self.conn.commit()
    
    def get_todayvc(self, query):
        """Execute custom SQL query"""
        cursor = self.conn.execute(query)
        results = []
        
        for row in cursor:
            vc = TodayVc()
            vc.VC_ID = row[0]
            vc.DateofVC = row[1]
            vc.Startingtime = row[2]
            vc.Important = row[3]
            vc.VCStatus = row[4]
            results.append(vc)
        
        return results

# ========================================
# STEP 3: Using in ImportantVcPage
# ========================================

class ImportantVcPage:
    def __init__(self):
        # Create database connection
        self.todayvc_db = TodayVcDatabase()
        
        # Build SQL query to get important VCs
        query = """
            SELECT *, COUNT(*) as NoOfVc 
            FROM TodayVc 
            WHERE Startingtime <> 'All' 
              AND VCStatus = 'Confirmed' 
              AND Important = 'Y' 
            GROUP BY time(Startingtime)
        """
        
        # Get data from database
        important_vcs = self.todayvc_db.get_todayvc(query)
        
        # Display in UI (list view)
        self.display_list(important_vcs)
    
    def display_list(self, vcs):
        """Show VCs in UI"""
        for vc in vcs:
            print(f"VC ID: {vc.VC_ID}")
            print(f"Date: {vc.DateofVC}")
            print(f"Time: {vc.Startingtime}")
            print(f"Purpose: {vc.Purpose}")
            print("---")

# ========================================
# STEP 4: Run the page
# ========================================

# When user clicks "Important VCs" button:
page = ImportantVcPage()
# This loads and displays all important VCs
```

---

## **5. Visual Database Structure**

```
📁 App Data Folder
├── 📄 TodayVc.db3          ← Database file
│   └── 📊 TodayVc table    ← Table with VC records
│       ├── Row 1: VC_ID="123", Important="Y", VCStatus="Confirmed"
│       ├── Row 2: VC_ID="124", Important="N", VCStatus="Confirmed"
│       └── Row 3: VC_ID="125", Important="Y", VCStatus="Cancelled"
│
├── 📄 ImportantVc.db3      ← Different database file
│   └── 📊 ImportantVc table ← Different table
│
└── 📄 Dashboard.db3
    └── 📊 Dashboard table
```

---

## **6. The Key Concepts**

### **Python Analogy:**

```python
# Think of it like this:

# ❌ WRONG WAY
book1 = open("math_textbook.pdf")
content = book1.read_page_about("History")  # Can't find history in math book!

# ✅ RIGHT WAY
book2 = open("history_textbook.pdf")
content = book2.read_page_about("History")  # Found it!
```

**Same concept:**
- Each `.db3` file = One book (database)
- Each table = One chapter in the book
- You need to open the **right book** to find the **right chapter**!

---

## **Summary:**

1. **Database files** = Like separate books (`.db3` files)
2. **Tables** = Like chapters in a book
3. **Rows** = Individual records/entries
4. **Connection** = Opening a book to read it
5. **Query** = Searching for specific information

**The bug:** Opened `ImportantVc.db3` (wrong book) but tried to read from [TodayVc](cci:2://file:///c:/Users/parth/Desktop/maui/nicvc-basetwo-git/NICVC/Model/TodayVc.cs:2:4-35:5) table (chapter that doesn't exist in that book)

**The fix:** Open `TodayVc.db3` (right book) to read [TodayVc](cci:2://file:///c:/Users/parth/Desktop/maui/nicvc-basetwo-git/NICVC/Model/TodayVc.cs:2:4-35:5) table (chapter exists!)

Makes sense? 🎯


so there is class Today... with filedconn of type SqlLite... class contrcutor use field to inliize database connection and create table if not exsit fill it full in natrual lanage


# **Complete Explanation in Natural Language**

Let me break down **exactly** what happens when the `TodayVcDatabase` class works:

---

## **The Class Structure**

```csharp
public class TodayVcDatabase
{
    private SQLiteConnection conn;
    
    public TodayVcDatabase()
    {
        conn = DatabaseHelper.GetConnection("TodayVc.db3");
        conn.CreateTable<TodayVc>();
    }
    
    public IEnumerable<TodayVc> GetTodayVc(String query)
    {
        var list = conn.Query<TodayVc>(query);
        return list.ToList();
    }
}
```

---

## **Step-by-Step Natural Language Explanation**

### **1. Class Declaration**
```
There is a class called "TodayVcDatabase"
This class is responsible for managing all video conference data
```

### **2. Field (Private Variable)**
```csharp
private SQLiteConnection conn;
```
```
Inside this class, there is a private field named "conn"
This field is of type "SQLiteConnection"
Think of "conn" as a telephone line to the database
Right now, it's just declared but not connected yet (null/empty)
```

### **3. Constructor (Initialization)**
```csharp
public TodayVcDatabase()
{
    conn = DatabaseHelper.GetConnection("TodayVc.db3");
    conn.CreateTable<TodayVc>();
}
```

**When someone creates a new TodayVcDatabase object, here's what happens:**

#### **Step 3a: Opening the Connection**
```
conn = DatabaseHelper.GetConnection("TodayVc.db3");
```
**Natural Language:**
1. Call a helper method named "GetConnection"
2. Pass the database filename "TodayVc.db3" as parameter
3. The helper checks: "Does TodayVc.db3 file exist on the phone/computer?"
   - **If YES:** Open the existing database file
   - **If NO:** Create a new empty database file named "TodayVc.db3"
4. Establish a connection (like dialing a phone number)
5. Store this connection in the "conn" field
6. Now "conn" is like an open telephone line to the database

#### **Step 3b: Creating the Table**
```
conn.CreateTable<TodayVc>();
```
**Natural Language:**
1. Using the open connection, send a command to the database
2. The command says: "Look at the TodayVc class definition"
3. Read all the properties in TodayVc class:
   - VC_ID (string)
   - DateofVC (string)
   - Startingtime (string)
   - Important (string)
   - ... etc
4. Check: "Does a table named 'TodayVc' already exist in this database?"
   - **If YES:** Do nothing, table already exists
   - **If NO:** Create a new table with these columns:
     ```sql
     CREATE TABLE TodayVc (
         VC_ID TEXT,
         DateofVC TEXT,
         Startingtime TEXT,
         Important TEXT,
         VCStatus TEXT,
         ...
     )
     ```
5. Now the database is ready to store data

---

### **4. Query Method (Getting Data)**
```csharp
public IEnumerable<TodayVc> GetTodayVc(String query)
{
    var list = conn.Query<TodayVc>(query);
    return list.ToList();
}
```

**Natural Language:**

**When someone calls [GetTodayVc("SELECT * FROM TodayVc WHERE Important='Y'")](cci:1://file:///c:/Users/parth/Desktop/maui/nicvc-basetwo-git/NICVC/FeedbackPage.xaml.cs:437:8-577:9), here's what happens:**

1. **Receive the SQL query** as a string parameter
   - Example: `"SELECT * FROM TodayVc WHERE Important='Y'"`

2. **Execute the query** using the connection:
   ```
   var list = conn.Query<TodayVc>(query);
   ```
   - Send the SQL command through the "conn" telephone line
   - The database searches the TodayVc table
   - Finds all rows where Important column equals 'Y'
   - Database returns raw data (rows and columns)

3. **Convert raw data to TodayVc objects:**
   - For each row returned:
     - Create a new TodayVc object
     - Fill VC_ID property with column 1 data
     - Fill DateofVC property with column 2 data
     - Fill Startingtime property with column 3 data
     - ... fill all properties
     - Add this object to a list

4. **Return the list:**
   ```
   return list.ToList();
   ```
   - Convert to a standard C# list
   - Return to whoever called this method
   - They now have a list of TodayVc objects ready to use

---

## **Complete Flow Example**

### **Scenario: User Opens ImportantVcPage**

```csharp
// Line 21: Create database object
todayVcDatabase = new TodayVcDatabase();
```

**What happens internally:**

```
STEP 1: Constructor is called
  ↓
STEP 2: Check if "TodayVc.db3" file exists
  - Location: /data/user/0/com.yourapp/files/TodayVc.db3
  - If missing: Create new empty database file
  ↓
STEP 3: Open connection to database file
  - conn = [Connection to TodayVc.db3]
  ↓
STEP 4: Check if "TodayVc" table exists
  - Run: SELECT name FROM sqlite_master WHERE type='table' AND name='TodayVc'
  - If missing: Create table with all columns
  ↓
STEP 5: Database is ready!
  - Connection: OPEN ✅
  - Table: EXISTS ✅
  - Ready to store/retrieve data ✅
```

---

```csharp
// Line 65: Get important VCs
importantVclist = todayVcDatabase.GetTodayVc(query).ToList();
```

**What happens internally:**

```
STEP 1: Call GetTodayVc method with SQL query
  - Query = "SELECT * FROM TodayVc WHERE Important='Y'"
  ↓
STEP 2: Send query through connection
  - Use the "conn" field (already open)
  - Execute SQL on database
  ↓
STEP 3: Database searches and filters
  - Look through all rows in TodayVc table
  - Find rows where Important column = 'Y'
  - Return matching rows
  ↓
STEP 4: Convert database rows to C# objects
  Row 1: VC_ID="123", Important="Y" → new TodayVc { VC_ID="123", Important="Y" }
  Row 2: VC_ID="125", Important="Y" → new TodayVc { VC_ID="125", Important="Y" }
  Row 3: VC_ID="127", Important="Y" → new TodayVc { VC_ID="127", Important="Y" }
  ↓
STEP 5: Return list of objects
  - List contains 3 TodayVc objects
  - Each object has all properties filled with data
  ↓
STEP 6: Display in UI
  - Bind list to ListView/CollectionView
  - User sees 3 important video conferences
```

---

## **Key Points in Natural Language:**

1. **`conn` field** = Your connection to the database (like a phone line)

2. **Constructor** = Runs automatically when you create `new TodayVcDatabase()`
   - Opens the database file
   - Creates the table if needed
   - Leaves connection open for future use

3. **CreateTable** = Smart command that checks first:
   - "Does table exist?" 
   - If yes → do nothing
   - If no → create it

4. **Query method** = Lets you ask questions to the database:
   - You give SQL (the question)
   - Database returns data (the answer)
   - Code converts to C# objects (easy to use)

5. **Connection stays open** = Once created, `conn` stays connected
   - You can call [GetTodayVc()](cci:1://file:///c:/Users/parth/Desktop/maui/nicvc-basetwo-git/NICVC/FeedbackPage.xaml.cs:437:8-577:9) many times
   - Same connection is reused
   - Faster than opening/closing each time

Is this clearer now? 🎯