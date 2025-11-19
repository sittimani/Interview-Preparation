# Angular 17 Quick Revision README

A lightweight and simple revision guide to quickly recall **Signals**, **Signal-based Input/Output**, and **New Directive Syntax** before your interview.

---

## 🚀 1. Signals (with computed & effect)

Signals are Angular’s new reactive system. They store values and notify the UI when those values change.

---

### ✅ **Signal** — "A reactive variable"

A **signal** holds a value. Reading it is done by calling it like a function.

**Example:**

```ts
count = signal(0); // create
count();           // read → 0
count.set(5);      // update
count.update(v => v + 1); // update using callback
```

**Use in template:**

```html
<p>{{ count() }}</p>
```

---

### ✅ **Computed** — "A derived value"

A **computed** signal depends on other signals.
Whenever the dependency changes, computed value auto-updates.

**Example:**

```ts
total = signal(10);
doubleTotal = computed(() => total() * 2);
```

If `total` becomes 20 → `doubleTotal()` becomes 40 automatically.

---

### ✅ **Effect** — "Runs code automatically when signals change"

Use **effect** when you want to perform some logic whenever a signal updates.

**Example:**

```ts
effect(() => {
  console.log('Count changed:', count());
});
```

Every time `count()` updates → effect runs.

✔ Great for logging, API calls, syncing to localStorage, etc.

---

(Very Simple Explanation)
**Signals** are like variables that automatically update the UI whenever their value changes.

* No need for observables or async pipe.
* Just call the signal like a function to read its value.

### **Example**

```ts
count = signal(0);       // create signal

this.count.set(5);       // set value
this.count.update(v => v + 1); // update value
```

### **Use in Template**

```html
<p>{{ count() }}</p>
```

---

## 🔄 2. Signal-Based @Input / @Output (Simple Explanation)

### **Input() - Simple Explanation**

`input()` creates a reactive input property.
It replaces the old `@Input()` decorator but works better with signals.

### **Output() - Simple Explanation**

`output()` replaces `EventEmitter`.
It is a simple and strongly typed way to send data from **child → parent**.

### **Example (Combined)**

#### **child.component.ts**

```ts
import { Component, input, output } from '@angular/core';

@Component({
  selector: 'child-box',
  standalone: true,
  template: `
    <h3>{{ title() }}</h3>
    <button (click)="send()">Click</button>
  `
})
export class ChildBox {
  // Input
  title = input<string>();

  // Output
  clicked = output<string>();

  send() {
    this.clicked.emit('Child button clicked');
  }
}
```

#### **parent.component.html**

```html
<child-box [title]="'Hello Signals'" (clicked)="onChildMsg($event)"></child-box>
```

#### **parent.component.ts**

```ts
onChildMsg(msg: string) {
  console.log(msg);
}
```

---

## 🧱 3. Structural Directives (Old vs New Syntax)

Here are the **old Angular 15 syntax** and the **new Angular 17 block syntax** side-by-side.

### **✔ ngIf**

**Old way:**

```html
<div *ngIf="isLoggedIn">Welcome User</div>
```

**New way:**

```html
@if (isLoggedIn) {
  <p>Welcome User</p>
}
```

---

### ✔ **ngFor**

**Old way:**

```html
<li *ngFor="let item of items; trackBy: trackItem">{{ item.name }}</li>
```

**New way:**

```html
@for (item of items; track item.id) {
  <li>{{ item.name }}</li>
}
```

---

### ✔ **ngSwitch**

**Old way:**

```html
<div [ngSwitch]="role">
  <p *ngSwitchCase="'admin'">Admin</p>
  <p *ngSwitchDefault>Guest</p>
</div>
```

**New way:**

```html
@switch (role) {
  @case ('admin') { <p>Admin</p> }
  @default { <p>Guest</p> }
}
```

---

## 🆚 Angular 15 vs Angular 17 (Quick Comparison)

| Feature                       | Angular 15                                | Angular 17                                             |
| ----------------------------- | ----------------------------------------- | ------------------------------------------------------ |
| **Signals**                   | ❌ Not available                           | ✅ Fully supported (signal, computed, effect)           |
| **Signal-based Input/Output** | ❌ Only @Input / @Output with EventEmitter | ✅ `input()` & `output()` (no EventEmitter, reactive)   |
| **Directive Syntax**          | ❌ Only `*ngIf`, `*ngFor`, `*ngSwitch`     | ✅ New block syntax → `@if`, `@for`, `@switch`          |
| **Standalone Components**     | ✅ Supported, encouraged                   | ✅ Default standard, no NgModules needed                |
| **Change Detection**          | Zone.js dependent                         | Optional **zoneless** mode with signals                |
| **Rendering**                 | Traditional CSR                           | Improved SSR + hydration + deferrable views (`@defer`) |
| **Builder**                   | Webpack-based                             | Vite-based, ESBuild (faster)                           |
