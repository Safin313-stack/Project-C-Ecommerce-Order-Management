<div align="center">

<br/>

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,50:1a0a2e,100:2d1560&height=200&section=header&text=E-commerce+Order+Management&fontSize=42&fontColor=ffffff&fontAlignY=38&desc=A+full-featured+console+based+order+management+system+in+C&descAlignY=60&descSize=14&descColor=94a3b8" width="100%"/>

<br/>

[![C](https://img.shields.io/badge/Language-C-00599C?style=flat-square&logo=c&logoColor=white)](https://en.wikipedia.org/wiki/C_(programming_language))
[![Platform](https://img.shields.io/badge/Platform-Linux-FCC624?style=flat-square&logo=linux&logoColor=black)](https://www.linux.org/)
[![Compiler](https://img.shields.io/badge/Compiler-GCC-f97316?style=flat-square)](https://gcc.gnu.org/)
[![Editor](https://img.shields.io/badge/Editor-VS%20Code-007ACC?style=flat-square&logo=visual-studio-code&logoColor=white)](https://code.visualstudio.com/)
[![MIT License](https://img.shields.io/badge/License-MIT-22c55e?style=flat-square)](LICENSE)

<br/>

<a href="https://github.com/Safin313-stack/Project-C-Ecommerce-Order-Management/blob/main/(PROJECT)_E-commerce_Order_Management_System.c">
  <img src="https://img.shields.io/badge/-%F0%9F%92%BB%20%20VIEW%20SOURCE%20%20%E2%86%92-1a0a2e?style=for-the-badge&logoColor=white" alt="View Source" height="42"/>
</a>

<br/>
<sub>✦ Click above to view the full source code on GitHub ✦</sub>

<br/><br/>

</div>

---

<div align="center">

### 🛒 Features

| 📦 Products | 🧾 Orders | 💰 Billing | 🔍 Search | ✏️ Update/Delete | 💾 File Storage |
|:---:|:---:|:---:|:---:|:---:|:---:|
| Add and view full product catalogue | Place and manage customer orders | Auto-calculate total bill with itemised receipt | Search orders by name or ID | Update or delete existing records | File handling for persistent data storage |

</div>

---

## 🖥️ Terminal UI Preview

> The program launches with an **animated ASCII art banner** and a **cursor-style interactive menu**

```
  ·····                         ·····
  ·····  ·····             ·····  ·····
    ·····  ·················  ·····
      ·······················
    🛒  E - C O M M E R C E   O R D E R   S Y S T E M  🛒
      ·······················
    ·····  ·················  ·····
  ·····  ·····             ·····  ·····
  ·····                         ·····

         ( Choose one of the options )

              → Add Order
                Display Orders
                Search Order
                Update Order
                Save & Exit
```

> ✦ The `→` cursor moves with keyboard input · styled with ANSI colors in the terminal

---

## 🎨 UI Highlights

### Animated ASCII Art Banner on Launch

```c
// Dotted loading animation rendered before the main menu appears
void loadingAnimation() {
    printf("\033[2J\033[H");   // clear screen
    // print dot pattern frame by frame with usleep() delays
    for (int i = 0; i < FRAMES; i++) {
        printFrame(i);
        usleep(80000);          // 80ms between frames
        printf("\033[H");       // reset cursor to top
    }
}
```

### ANSI Color Styling

```c
// ANSI escape codes for terminal colors
#define CYAN    "\033[36m"
#define MAGENTA "\033[35m"
#define RESET   "\033[0m"

printf(CYAN "  🛒  E - C O M M E R C E   O R D E R   S Y S T E M" RESET);
```

### Cursor-Style Interactive Menu

```c
// Arrow cursor moves to highlight the selected option
void printMenu(int selected) {
    const char *options[] = {
        "Add Order", "Display Orders",
        "Search Order", "Update Order", "Save and Exit"
    };
    for (int i = 0; i < 5; i++) {
        if (i == selected)
            printf("  -> %s\n", options[i]);   // highlighted
        else
            printf("     %s\n", options[i]);   // normal
    }
}
```

---

## 🧠 Core Logic

### Struct-based Order Records

```c
struct Order {
    int   id;
    char  productName[50];
    int   quantity;
    float price;
    float total;
};
```

### File Handling for Persistent Storage

```c
void saveToFile(struct Order orders[], int count) {
    FILE *fp = fopen("orders.dat", "wb");
    fwrite(orders, sizeof(struct Order), count, fp);
    fclose(fp);
}

int loadFromFile(struct Order orders[]) {
    FILE *fp = fopen("orders.dat", "rb");
    if (!fp) return 0;
    int n = fread(orders, sizeof(struct Order), 100, fp);
    fclose(fp);
    return n;
}
```

### Auto Bill Calculation

```c
void generateBill(struct Order orders[], int count) {
    float total = 0;
    printf("\n======== RECEIPT ========\n");
    for (int i = 0; i < count; i++) {
        printf("%-20s x%d = %.2f\n",
            orders[i].productName,
            orders[i].quantity,
            orders[i].total);
        total += orders[i].total;
    }
    printf("-------------------------\n");
    printf("TOTAL : %.2f\n", total);
}
```

---

## 🛠️ Compile and Run

### Prerequisites
- Linux OS
- GCC installed

```bash
# Check GCC
gcc --version

# Install if needed (Ubuntu/Debian)
sudo apt install gcc
```

### Compile

```bash
gcc -o ecommerce "(PROJECT)_E-commerce_Order_Management_System.c"
```

### Run

```bash
./ecommerce
```

### One-liner

```bash
gcc -o ecommerce "(PROJECT)_E-commerce_Order_Management_System.c" && ./ecommerce
```

---

## 📁 Project Structure

```
Project-C-Ecommerce-Order-Management/
│
├── 📄 (PROJECT)_E-commerce_Order_Management_System.c   ← Full source code
└── 📄 README.md                                        ← Project documentation
```

---

## 🛠️ Tech Stack

```
┌──────────────────────────────────────────────────────┐
│                C Console Application                 │
├─────────────────┬────────────────────────────────────┤
│  Language       │  C (C99 standard)                  │
│  Compiler       │  GCC (Linux)                       │
│  Editor         │  VS Code                           │
│  Libraries      │  stdio.h · stdlib.h · string.h     │
│  UI             │  ANSI escape codes · ASCII art      │
│  Storage        │  Binary file handling (.dat)        │
│  Platform       │  Linux                             │
└─────────────────┴────────────────────────────────────┘
```

---

## 📚 Key Concepts Used

```
struct           → custom data type for Order records
ANSI codes       → terminal colors and cursor positioning
usleep()         → microsecond delay for animations (Linux)
fopen/fclose     → open and close files
fread/fwrite     → binary file read and write
strstr()         → search substring (order search)
printf/scanf     → formatted console I/O
arrays/pointers  → store and pass record collections
```

---

<div align="center">

## 👤 Developer

<br/>

**Saharia Hassan Safin**
C Developer · Front-end Developer

<br/>

[![GitHub](https://img.shields.io/badge/GitHub-Safin313--stack-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Safin313-stack)
&nbsp;
[![Source Code](https://img.shields.io/badge/Source%20Code-View%20File-1a0a2e?style=for-the-badge&logo=github&logoColor=white)](https://github.com/Safin313-stack/Project-C-Ecommerce-Order-Management/blob/main/(PROJECT)_E-commerce_Order_Management_System.c)

<br/>

*"Building a full store with structs, ANSI colors, and a .dat file"* 🛒

<br/>

</div>

---

<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:2d1560,50:1a0a2e,100:0d1117&height=120&section=footer" width="100%"/>

<sub>MIT License · © 2025 Saharia Hassan Safin · ⭐ Star this repo if it helped you!</sub>

</div>
