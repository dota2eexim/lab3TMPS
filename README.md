# lab3TMPS
___
Use behavorial patterns: Command, Iterator, Memento, Meditor and Strategy.

It is a laboratory number 3, where 5 template have been used.
### Command

I have TV and switch for them; I can conect TV and disconnect. Where TV is connected its volume increse and when is disconnected volume == zero.
Here code for TV
```js
class TV {
    constructor(volume) {
        this.volume = volume || 0;
    }

    connect() {
        this.volume += 1;
        console.log('TV is connected!');
        console.log('Volume is ' + this.volume);
    }

    disconnect() {
        this.volume -= 1;
        console.log('TV is disconnected!');
        console.log('Volume is ' + this.volume);
    }
}
```

and for Switch:

```js
class Switch {
    constructor(connect, disconnect) {
        this.connect = connect;
        this.disconnect = disconnect;
    }

    connecting() {
        this.connect.execute();
    }

    disconnecting() {
        this.disconnect.execute();
    }
}
```

then I use it
```js
let tv = new TV();
let connectC = new IsConnecting(tv);
let disconnectC = new IsDisconnecting(tv);
let tvSwitching = new Switch(connectC, disconnectC);

tvSwitching.connecting();
tvSwitching.disconnecting();
```

### Iterator
I use Iterator for iterate all of my TV brands and it is amazing, becouse client-side don't know how it's works

```js
class NameIterator extends Iterator {
    constructor(names) {
        super();
        this.id = 0;
        this.names = names;
    }

    hasNext() {
        if(this.id < this.names.length) {
            return true;
        }
        return false;
    }

    next() {
        if (this.hasNext()) {
            return this.names[this.id++];
        }
        return null;
    }
}
```
### Memento
I use memento for make some copy of my TV state, and when i want to make reset, I easy make it and restore state of my previous TV.
You can see that its works
```js
let careTaker = new CareTaker();

careTaker.add(1, tv.compress());

tv.volume = 3;
console.log("New volume is " + tv.volume);

tv.deCompress(careTaker.get(1));
console.log("Old volume is " + tv.volume);
```
This caretaker can save many and many TV as you needed
```js
class CareTaker {
    constructor() {
        this.mementos = {};
    }

    add(key, memento) {
        this.mementos[key] = memento;
    }

    get(key) {
        return this.mementos[key];
    }
}
```

### Mediator

I have two TV's and they need to communiacte.
Mediator can easy help us in this case.
That pattern takes 2 or more TV's, if it needed, and help use)

```js
class ConcreteMediator extends Mediator {
    constructor() {
        super();
    }

    setTvClass1(tvClass1) {
        this.tvClass1 = tvClass1;
    }

    setTvClass2(tvClass2) {
        this.tvClass2 = tvClass2;
    }

    send(message, tvClass) {
        if (tvClass === this.tvClass2) {
            this.tvClass1.notify(message);
        }
        else {
            this.tvClass2.notify(message);
        }
    }
}
```
Easy. These TV's doesn't communicate with one other directly, they communiacte throw the Mediator pattern and if need to change we can do this in easy way.

### Strategy

I use this pattern for show 3 TV post. 

```js
class Strategy {
    tvShow(btnNum){}
}

class RemoteDevice {
    constructor(strategy) {
        this.strategy = strategy;
    }

    execStrategy(btnNum) {
        return this.strategy.tvShow(btnNum);
    }
}
```
I have algorith tvShow(), that every TVPost need to do.
I put it algo in Strategy and use it in easy mode.
