# Project #2 - Modal Window

This small project we're going to build our first UI component. That is called the modal window that we can see here by opening, or by clicking actually on one of these buttons.

It's simply a window that appears and gives an overly which gets overlaid over the rest of the page. So no matter which of these three buttons we click, it will always open this modal window.

- we will be able to close the window by the esc key, closing out of it or simply by clicking off the window

## What should we target first?

- we want to target: modal, overlay, close-modal show-modal

### modal, overlay, close-modal

- this time when we call these with document.qs we want to store them as a variable so this is why we save it inside const modal.

```
const modal = document.querySelector('.modal');
const overlay = document.querySelector('.overlay');
const btnCloseModal = document.querySelector('.close-modal');
const btnShowModal = document.querySelector('.show-modal');
```

## document.querySelectorAll()

- so there is an instance where we have 3 of the .show-modals class. Here we will use the document.querySelectorAll() property to select them all.
- When we look at the console it shows the 3 buttons in a nodelist which is kind of like an array. So if we wanted something to cycle to the buttons we could make a for loop for them

### for looping the NodeList

for (let i = 0; i < btnsShowModal.length; i++) {
console.log(btnsShowModal[i].textContent);
}

with a loop like this we end up printing the btns to the console and then when we add the .textContent it'll just show modal 1 > modal 2 > modal 3

- if there is only one line of code in a for loop we dont actually need the curly braces. in our example with the console.log this is the only code that will be run after the for loop

## Let's attach an event handler function to our btns

first lets change the previous code. We no longer want it to say the textContent we want to attach an event listener to it.

```
for (let i = 0; i < btnsShowModal.length; i++)
  btnsShowModal[i].addEventListener('click', function() {
    console.log('Button clicked!');
  });
```

- so we removed textContent for the event listener. Remember we need to have the event `'Click'` followed by the function expression. `function() {}` as its second parameter. This time we will have the function console.log(`Button clicked`); each time we click the button.
  - it will return to the console: `Button Clicked!`.

## let's try to attach the modal

- the modal is already in the html but it is hidden with CSS
  - so we take this element that we selected here previously `modal` and we attach classList property to it
  - ### modal.classList.remove()
  - has a couple of properties:
    - .add
    - .remove
    - we are going to use remove to get rid of the hidden class. so we do

```
modal.classList.remove('hidden');
```

we can also remove multiple classes for that we just have to pass them in with commas. Also unlike the querySelector when it targets a class we DO NOT use the `.` when calling the classes. The `.` is only for the selector.

```
modal.classList.remove('hidden');
```

so now when we click the button the modal window appears! in the console the hidden class is no longer there when inspecting the page it just says `modal`. Of course we cannot close it yet but when we have that functionality we can!

### overlay.classList.remove()

- remember that our overlay also has a hidden class. Let's change that too!

```
overlay.classList.remove('hidden');
```

- now this gives us our nice overlay!

### closing the modal window modal.classList.add()

so lets take our `btnsCloseModal` variable and attach an event listener to it. This time we are gonna do the opposite and add the hidden class back

```
btnCloseModal.addEventListener('click', function () {
  modal.classList.add('hidden');
  overlay.classList.add('hidden');
});
```

When we come back to this it works on our page!

### now we want our modal window to close when we click it from the outside

- we want to target the overlay, lets give it an event listener. Theoretically, we could put the same code in this block like we did before and it would do the same thing:

btnCloseModal.addEventListener('click', function () {
modal.classList.add('hidden');
overlay.classList.add('hidden');
});

overlay.addEventListener('click', function () {
modal.classList.add('hidden');
overlay.classList.add('hidden');
});

BUT it would be repeating code. Let's try making it into a real function so lets cut this code out:

const closeModal = function() {
modal.classList.add('hidden');
overlay.classList.add('hidden');
}

btnCloseModal.addEventListener('click');

- give it the code that we original had
- now we can call it in the function again like this.

const closeModal = function() {
modal.classList.add('hidden');
overlay.classList.add('hidden');
}

btnCloseModal.addEventListener('click', closeModal);

- notice we are not calling the function closeModal() would not work at all.
- we can also do the same thing for the overlay eventlistener.

```
btnCloseModal.addEventListener('click', closeModal);
overlay.addEventListener('click', closeModal);
```

- for the sake of keeping everything the same let's do the same thing to the showModal

```
const showModal = function () {
  console.log('Button clicked!');
  modal.classList.remove('hidden');
  overlay.classList.remove('hidden');
};

btnsShowModal[i].addEventListener('click', showModal);
```

## RECAP

### Part 1

If we want to use the same function in multiple event lsiteners, like here:

```
btnCloseModal.addEventListener('click', function () {
modal.classList.add('hidden');
overlay.classList.add('hidden');
});

overlay.addEventListener('click', function () {
modal.classList.add('hidden');
overlay.classList.add('hidden');
});
```

you need to specify that function as a separate function, like this here:

```
 const showModal = function () {
  modal.classList.remove('hidden');
  overlay.classList.remove('hidden');
};

const closeModal = function () {
  modal.classList.add('hidden');
  overlay.classList.add('hidden');
};
```

once you do this you can pass this function as an argument to multiple addEventListeners methods:

```
btnsShowModal[i].addEventListener('click', showModal);

btnCloseModal.addEventListener('click', closeModal);
overlay.addEventListener('click', closeModal);
```

### Part 2

Really in practice use the functionality of adding and removing classes all the time in order to change the appearance of elements on our page.

This is because classes allow us to basically aggregate multiple CSS properties in just one, like a container

So each class functions a bit like a container with a lot of properties in it. - by adding and removing them can activate and deactivate certain styles all the time

