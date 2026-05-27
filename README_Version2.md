# 🌐 DOM Manipulation in JavaScript — Hinglish Notes

> Ek complete beginner-friendly guide jisme hum DOM ko samjhenge, manipulate karenge, aur real-world examples ke saath practice karenge. 🚀

---

## 📌 Table of Contents

1. [DOM Kya Hota Hai?](#1-dom-kya-hota-hai)
2. [DOM Tree Structure](#2-dom-tree-structure)
3. [Elements Ko Select Karna](#3-elements-ko-select-karna)
4. [Content Change Karna](#4-content-change-karna)
5. [Attributes Manipulate Karna](#5-attributes-manipulate-karna)
6. [CSS Styles Change Karna](#6-css-styles-change-karna)
7. [Classes Add/Remove Karna](#7-classes-addremove-karna)
8. [Naye Elements Banana](#8-naye-elements-banana)
9. [Elements Remove Karna](#9-elements-remove-karna)
10. [Event Handling](#10-event-handling)
11. [Event Delegation](#11-event-delegation)
12. [Form Handling](#12-form-handling)
13. [Traversing the DOM](#13-traversing-the-dom)
14. [Mini Projects](#14-mini-projects)
15. [Best Practices](#15-best-practices)

---

## 1. DOM Kya Hota Hai?

**DOM = Document Object Model**

Jab browser HTML page load karta hai, to wo us HTML ko ek **tree structure (object form)** me convert kar deta hai jise DOM kehte hain. Is tree ko JavaScript se access aur modify kiya ja sakta hai.

👉 Simple words me: **DOM = HTML ka JavaScript version**

```html
<!DOCTYPE html>
<html>
  <head><title>Demo</title></head>
  <body>
    <h1>Hello World</h1>
  </body>
</html>
```

Browser isko aise dekhta hai:

```
document
   └── html
        ├── head
        │    └── title → "Demo"
        └── body
             └── h1 → "Hello World"
```

---

## 2. DOM Tree Structure

Har HTML element ek **node** hota hai. 3 main types:

| Node Type | Example |
|-----------|---------|
| Element Node | `<div>`, `<p>`, `<h1>` |
| Text Node | "Hello World" |
| Attribute Node | `class="btn"`, `id="main"` |

**Relationship terms:**
- `parent` → upar wala element
- `child` → andar wala element
- `sibling` → same level wale elements

---

## 3. Elements Ko Select Karna

Sabse pehle element ko **pakadna** padta hai, tabhi to use change karenge. 😎

### 🔹 `getElementById()`
```javascript
const heading = document.getElementById("title");
console.log(heading);
```

### 🔹 `getElementsByClassName()` (HTMLCollection return karta hai)
```javascript
const items = document.getElementsByClassName("item");
console.log(items[0]);
```

### 🔹 `getElementsByTagName()`
```javascript
const allPara = document.getElementsByTagName("p");
```

### 🔹 `querySelector()` ⭐ (Most Used)
Pehla matching element return karta hai. CSS selector use hota hai.
```javascript
const btn = document.querySelector(".btn");      // class
const box = document.querySelector("#box");      // id
const firstLi = document.querySelector("ul li"); // nested
```

### 🔹 `querySelectorAll()` (NodeList return karta hai)
```javascript
const allBtns = document.querySelectorAll(".btn");
allBtns.forEach(btn => console.log(btn));
```

---

## 4. Content Change Karna

### 🔹 `innerText` — sirf visible text
```javascript
document.querySelector("h1").innerText = "Naya Heading!";
```

### 🔹 `innerHTML` — HTML ke saath
```javascript
document.querySelector("#box").innerHTML = "<b>Bold Text</b>";
```

### 🔹 `textContent` — saara text (hidden bhi)
```javascript
document.querySelector("p").textContent = "Simple text content";
```

**⚠️ Difference:**
- `innerText` → CSS ka dhyaan rakhta hai (hidden text skip)
- `innerHTML` → HTML tags parse karta hai
- `textContent` → raw text (fastest)

---

## 5. Attributes Manipulate Karna

```javascript
const img = document.querySelector("img");

// Get
img.getAttribute("src");

// Set
img.setAttribute("src", "newImage.jpg");
img.setAttribute("alt", "Nayi photo");

// Remove
img.removeAttribute("alt");

// Check
img.hasAttribute("src"); // true
```

**Direct property access bhi possible hai:**
```javascript
img.src = "photo.png";
img.alt = "Meri photo";
```

---

## 6. CSS Styles Change Karna

```javascript
const box = document.querySelector("#box");

box.style.backgroundColor = "skyblue";
box.style.color = "white";
box.style.padding = "20px";
box.style.borderRadius = "10px";
box.style.fontSize = "18px";
```

> 💡 Note: CSS me `background-color` likhte hain, JS me `backgroundColor` (camelCase).

---

## 7. Classes Add/Remove Karna

`classList` use karte hain — bahut powerful hai! 💪

```javascript
const card = document.querySelector(".card");

card.classList.add("active");          // class add
card.classList.remove("hidden");       // class remove
card.classList.toggle("dark-mode");    // on/off switch
card.classList.contains("active");     // true/false
card.classList.replace("old", "new");  // replace
```

**Example: Dark Mode Toggle**
```javascript
const btn = document.querySelector("#themeBtn");
btn.addEventListener("click", () => {
  document.body.classList.toggle("dark-mode");
});
```

---

## 8. Naye Elements Banana

3 Steps: **Create → Configure → Append**

```javascript
// Step 1: Create
const newDiv = document.createElement("div");

// Step 2: Configure
newDiv.innerText = "Main naya div hoon!";
newDiv.classList.add("box");
newDiv.style.color = "red";

// Step 3: Append
document.body.appendChild(newDiv);
```

### 🔹 Append Methods

| Method | Kaam |
|--------|------|
| `appendChild(el)` | Last me add karta hai |
| `prepend(el)` | First me add karta hai |
| `append(el)` | Last me add (text bhi le sakta hai) |
| `before(el)` | Element ke pehle |
| `after(el)` | Element ke baad |
| `insertBefore(new, ref)` | Reference se pehle |

**Example: List me item add karna**
```javascript
const ul = document.querySelector("#myList");
const li = document.createElement("li");
li.innerText = "Naya item";
ul.appendChild(li);
```

---

## 9. Elements Remove Karna

```javascript
const item = document.querySelector(".item");

// Modern way ✅
item.remove();

// Old way
item.parentNode.removeChild(item);
```

---

## 10. Event Handling

Events = User ke actions (click, hover, type, scroll, etc.)

### 🔹 `addEventListener()` ⭐
```javascript
const btn = document.querySelector("#myBtn");

btn.addEventListener("click", function() {
  alert("Button click hua!");
});
```

### 🔹 Common Events

| Event | Kab Hota Hai |
|-------|--------------|
| `click` | Click karne par |
| `dblclick` | Double click |
| `mouseover` | Hover karne par |
| `mouseout` | Hover hatne par |
| `keydown` | Key dabane par |
| `keyup` | Key chhodne par |
| `submit` | Form submit |
| `change` | Input value change |
| `input` | Type karte waqt |
| `load` | Page load hone par |
| `scroll` | Scroll karne par |

### 🔹 Event Object
```javascript
btn.addEventListener("click", (e) => {
  console.log(e.target);       // konsa element clicked
  console.log(e.type);         // event ka type
  e.preventDefault();          // default behaviour rokna
});
```

**Example: Counter App**
```javascript
let count = 0;
const display = document.querySelector("#count");
const btn = document.querySelector("#incBtn");

btn.addEventListener("click", () => {
  count++;
  display.innerText = count;
});
```

---

## 11. Event Delegation

Jab bahut saare similar elements ho, har ek pe listener lagana fizool hai. Parent pe ek listener laga do — sab handle ho jayenge. 🔥

```javascript
document.querySelector("#list").addEventListener("click", (e) => {
  if (e.target.tagName === "LI") {
    e.target.classList.toggle("done");
  }
});
```

---

## 12. Form Handling

```html
<form id="myForm">
  <input type="text" id="name" placeholder="Naam">
  <input type="email" id="email" placeholder="Email">
  <button type="submit">Submit</button>
</form>
```

```javascript
const form = document.querySelector("#myForm");

form.addEventListener("submit", (e) => {
  e.preventDefault(); // page reload rokna
  
  const name = document.querySelector("#name").value;
  const email = document.querySelector("#email").value;
  
  console.log(`Name: ${name}, Email: ${email}`);
});
```

---

## 13. Traversing the DOM

Ek element se uske rishtedaaron (parent, child, siblings) tak jaana.

```javascript
const item = document.querySelector(".item");

// Parent
item.parentElement;

// Children
item.children;          // sirf elements
item.firstElementChild;
item.lastElementChild;

// Siblings
item.nextElementSibling;
item.previousElementSibling;
```

**Example:**
```html
<ul id="menu">
  <li>Home</li>
  <li class="active">About</li>
  <li>Contact</li>
</ul>
```

```javascript
const active = document.querySelector(".active");
console.log(active.parentElement);              // <ul>
console.log(active.nextElementSibling);         // Contact
console.log(active.previousElementSibling);     // Home
```

---

## 14. Mini Projects

### 🎯 Project 1: To-Do List

```html
<input type="text" id="todoInput" placeholder="Kaam likho...">
<button id="addBtn">Add</button>
<ul id="todoList"></ul>
```

```javascript
const input = document.querySelector("#todoInput");
const addBtn = document.querySelector("#addBtn");
const list = document.querySelector("#todoList");

addBtn.addEventListener("click", () => {
  if (input.value.trim() === "") return;
  
  const li = document.createElement("li");
  li.innerText = input.value;
  
  // Delete on click
  li.addEventListener("click", () => li.remove());
  
  list.appendChild(li);
  input.value = "";
});
```

### 🎯 Project 2: Background Color Changer

```javascript
const btn = document.querySelector("#colorBtn");

btn.addEventListener("click", () => {
  const colors = ["red", "blue", "green", "purple", "orange"];
  const random = colors[Math.floor(Math.random() * colors.length)];
  document.body.style.backgroundColor = random;
});
```

### 🎯 Project 3: Live Character Counter

```html
<textarea id="msg"></textarea>
<p>Characters: <span id="count">0</span></p>
```

```javascript
const msg = document.querySelector("#msg");
const count = document.querySelector("#count");

msg.addEventListener("input", () => {
  count.innerText = msg.value.length;
});
```

---

## 15. Best Practices

✅ **DO's:**
- `querySelector` / `querySelectorAll` prefer karo (modern + flexible)
- `addEventListener` use karo, `onclick` nahi
- Variables me elements store karo (baar-baar select mat karo)
- `classList` use karo styling toggle ke liye
- Event delegation use karo multiple similar elements pe

❌ **DON'Ts:**
- `innerHTML` ke saath user input mat daalo (XSS risk ⚠️)
- DOM me baar-baar changes mat karo (slow hota hai) → batch updates karo
- Inline JS (`onclick="..."` HTML me) avoid karo
- Global variables se bacho

---

## 🎓 Quick Cheat Sheet

```javascript
// Select
document.querySelector(".class");
document.querySelectorAll(".class");
document.getElementById("id");

// Modify
el.innerText = "text";
el.innerHTML = "<b>html</b>";
el.style.color = "red";
el.setAttribute("src", "x.jpg");
el.classList.add/remove/toggle("class");

// Create & Remove
const el = document.createElement("div");
parent.appendChild(el);
el.remove();

// Events
el.addEventListener("click", (e) => { ... });
```

---

## 📚 Aage Kya Padhein?

- 🔸 **Event Bubbling & Capturing**
- 🔸 **LocalStorage / SessionStorage**
- 🔸 **Fetch API & AJAX**
- 🔸 **Promises & Async/Await**
- 🔸 **ES6 Modules**

---

> 💡 **Pro Tip:** Bina practice ke ye notes sirf kagaz hain. Roz ek mini project banao — DOM master ban jaoge! 💯

**Happy Coding! 🚀**