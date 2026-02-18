# [[../../appunti-completi#312-prototipi-prototypes|Prototipi (Prototypes)]]

Il meccanismo dei **prototipi** (prototype) in JavaScript funziona come un sistema di **"fallback"** per le proprietà degli oggetti.

Quando si cerca di accedere a una proprietà su un oggetto e questa non viene trovata, JavaScript cerca automaticamente nella **catena dei prototipi** (prototype chain), risalendo fino a trovare la proprietà su un oggetto collegato. Questo processo è noto come **delega** (delegation).

## Esempio Base: Object.create()

```javascript
var foo = { a: 42 };

// Crea un oggetto collegato a foo
var bar = Object.create(foo);

console.log(bar.a); // 42 (delegato a foo)
console.log(bar.hasOwnProperty("a")); // false

bar.a = 100; // Crea proprietà propria su bar

console.log(bar.a); // 100 (propria)
console.log(foo.a); // 42 (invariato)
```

La proprietà `"a"` non esiste direttamente su `bar`, ma viene trovata risalendo la catena prototipale fino a `foo`.

## L'Astrazione delle Classi ES6

Nello sviluppo moderno è raro manipolare direttamente i prototipi. La sintassi **`class`** di ES6 è **zucchero sintattico** che astrae la manipolazione del prototipo:

```javascript
// ES6
class Person {
  constructor(name) {
    this.name = name;
  }

  greet() {
    console.log("Ciao, sono " + this.name);
  }
}

// Equivalente pre-ES6 (con prototipi)
function Person(name) {
  this.name = name;
}

Person.prototype.greet = function () {
  console.log("Ciao, sono " + this.name);
};
```

Ogni volta che si definisce una **classe** e i suoi **metodi**, si sta utilizzando il sistema dei prototipi.

## Uso Implicito dei Prototipi

L'interazione con la **catena dei prototipi** avviene continuamente:

**Metodi degli Array** → `.map()`, `.filter()`, `.forEach()` risiedono su `Array.prototype` e ogni array delega a questo prototipo.

```javascript
var numbers = [1, 2, 3];

console.log(numbers.hasOwnProperty("map")); // false
console.log(Array.prototype.hasOwnProperty("map")); // true
```

**Metodi degli Oggetti** → `.toString()` e `.hasOwnProperty()` sono ereditati da `Object.prototype`.

**Il DOM** → Ogni elemento eredita metodi come `.addEventListener()` da prototipi come `EventTarget.prototype`.

## Perché è Importante Conoscerli?

**Debugging** → Aiuta a diagnosticare errori come `TypeError: is not a function`, ispezionando quale metodi sono disponibili nella catena prototipale.

**Performance** → I metodi sul prototipo sono **condivisi** tra tutte le istanze, risparmiando memoria rispetto a metodi duplicati su ogni istanza.

```javascript
// ❌ Inefficiente: 1000 copie del metodo
function PersonBad(name) {
  this.name = name;
  this.greet = function () {
    console.log(this.name);
  };
}

// ✅ Efficiente: 1 copia sul prototipo
function PersonGood(name) {
  this.name = name;
}
PersonGood.prototype.greet = function () {
  console.log(this.name);
};
```

**Polyfilling** → Implementare funzionalità moderne per browser vecchi richiede di estendere prototipi nativi:

```javascript
if (!Array.prototype.includes) {
  Array.prototype.includes = function (searchElement) {
    for (var i = 0; i < this.length; i++) {
      if (this[i] === searchElement) return true;
    }
    return false;
  };
}
```

## Riepilogo

I prototipi costituiscono il **motore del sistema a oggetti di JavaScript**. Sebbene la manipolazione diretta sia rara, comprenderne il funzionamento è fondamentale per:

- Capire come funzionano le **classi ES6**
- **Debugging** e ispezione degli oggetti
- Ottimizzazione delle **performance**
- Creare **polyfill** per compatibilità

## Collegamenti

- [[oggetti]] - Gli oggetti e le loro proprietà
- [[../funzioni/this]] - This e il suo ruolo nei prototipi
- [[../funzioni/funzioni]] - Le funzioni costruttore e i prototipi
