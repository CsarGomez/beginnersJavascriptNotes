<a name="SeriousPractice"></a>
# **Module #6 - Serious practice exercises**
---
<a name="Etch-a-sketch"></a> 
## **ETCH-A-SKETCH**

>Example [here](https://codepen.io/cgope/pen/yLaVayG)

We need to select all elements on the page.
The canvas is the element and the place were we will drawing is called context (ctx), then we call the getContext method which in this case is 2d

```js
const canvas = document.querySelector('#etch-a-sketch');

const ctx = canvas.getContext('2d');

const shakeButton = document.querySelector('.shake');

const MOVE_AMOUNT = 10;
```
then set up canvas for drawing

```js
const {width, height} = canvas;

let x = Math.floor(Math.random() * width);

let y = Math.floor(Math.random() * height);
```

After that we will create random x and y starting points on the canvas

```js
ctx.lineJoin = 'round';
ctx.lineCap = 'round';
ctx.lineWidth = MOVE_AMOUNT;

let hue = 0;
ctx.strokeStyle = `hsl(${hue}, 100%, 50%)`;
ctx.beginPath(); //start drawing
ctx.moveTo(x, y);
ctx.lineTo(x, y);
ctx.stroke();
```

Now we can write a draw function

```js
function draw({ key }){
  //increment the hue
  hue += 5;
  ctx.strokeStyle = `hsl(${hue}, 100%, 50%)`;
  ctx.beginPath();
  ctx.moveTo(x, y);
  //move our x and y values depending on what the user did
  switch (key){
    case 'ArrowUp': 
      y -= MOVE_AMOUNT;
      break;
    case 'ArrowRight': 
      x += MOVE_AMOUNT;
      break;
    case 'ArrowDown': 
      y += MOVE_AMOUNT;
      break;
    case 'ArrowLeft': 
      x -= MOVE_AMOUNT;
      break;
    default:
      break;
  }
  ctx.lineTo(x, y);
  ctx.stroke();
}
```

Now we need to write a handler for keys

```js
function handleKey(e){
  if (e.key.includes('Arrow')){
    e.preventDefault();
    draw({key: e.key});
  }
}
```

And now we can work on the clean/shake button

```js
function clearCanvas(){
  canvas.classList.add('shake');
  ctx.clearRect(0, 0, width, height);
   canvas.addEventListener('animationend',function(){
    canvas.classList.remove('shake');
  }, {once:true});
}
```
Finally we will have to listen for the arrow keys and shake button

```js
window.addEventListener('keydown', handleKey);
shakeButton.addEventListener('click', clearCanvas);
```

<br>

<a name="Click-Outside-Modal"></a> 
## **CLICK OUTSIDE MODAL**

>Example [here](https://codepen.io/cgope/pen/vYypLMO)

The main goal of this exercise is to know about the clicking outside, the example is about we have some cards which contains an image, a title and a button, so if you click on the button a higher version of the image will be displayed, then if you click outside it will close it and return to the main cards.

So first thing is select the button for each card, loop into each button and add and evend listener for the click that will trigger a function called _**handleCardButtonClick**_:

```js
//select the buttons
const cardButtons = document.querySelectorAll('.card button');

//loop into each button and listen for a click
cardButtons.forEach(button => button.addEventListener('click', handleCardButtonClick));
```

Next step is grab something to show in the modal, so it will be the image in a hihger version, the data description, this will happend in the function:

```js
function handleCardButtonClick(event){
  //grab the button and card
  const button = event.currentTarget;
  const card = button.closest('.card');
  //grab the img src
  const imgSrc = card.querySelector('img').src;
  const desc = card.dataset.description;
  const name = document.querySelector('h2').textContent;
  //populate modal with new info
  modalInner.innerHTML = `
  <img src="${imgSrc.replace('200', '500')}" alt="${name}"/>
  <p>${desc}</p>
  `;

  //Show the modal
modalOuter.classList.add('open');
}
```

we use the _closest_ method to get the card asociated with the button that got clicked.  
The replace the 200 for 500 to get the higher version of the image, meaning that insted of the img of 200px we will use the 500px version of the same image.  

And dont forget to select the modal before we try to show the modal in the function:

```js 
const modalOuter = document.querySelector('.modal-outer');
const modalInner = document.querySelector('.modal-inner');
```

Now the most important part of the exercise is to close the card, so we need to write a function for that:

```js
function closeModal(){
  modalOuter.classList.remove('open');
}
```

this simple remove the class of open, but now we need to close the modal when we click in the outside of the inner modal.
we can do this using a event listener and making sure that the user clicked outside the modal.
so the _closest_ method can be helpful here too to tell us if the click happends outside or inside the inner modal, so if you click inside of the modal inner it will find the modal inner, if not it will not be able to find anything, then we can convert into a boolean, so if find something it will be false and if dont find something it will be true:

```js
modalOuter.addEventListener('click', function(event){
  //the ! will convert into a boolean
  const isOutSide = !event.target.closest('.modal-inner');
  if (isOutSide){
    closeModal();
  }
});
```

a feature can be added with the Esc key, so if the user type the esc key it will close the modal as well:

```js
window.addEventListener('keydown', event=>{
  if(event.key==='Escape'){
    closeModal();
  }
});
```

you can find the event key for whatever key you want you can go to [keycode](https://keycode.info/) webside


<br>

<a name="ScrollEvents-IntersectionObserver"></a> 
## **SCROLL EVENTS AND INTERSECTION OBSERVER**

>Example [here](https://codepen.io/cgope/pen/vYypLMO)

In the example we work with Terms and Conditions, maybe scroll event isn't the best way to aproach this because you will have to deal offsets, margin, padding, heights, instead of scroll events we will use _Intersection Observer_

first thing first is select the Terms and conditions and the button:

```js
const terms = document.querySelector('.terms-and-conditions');

const button = document.querySelector('.agree');
```

After select the elements we can create a funciton called obCallBack, this function will give us a payload.
we will use ```payload[0]``` since it will be the first thing in the payload, you can watch for multiple items.  
```IntersectionRatio``` will tell us how much is visible on the page.
so when the intersection ratio it's equals to 1 we can enable the buttom to accept the terms and conditions.

```js
function obCallBack(payload){
  if (payload[0].intersectionRatio === 1){
    button.disabled = false;
    //stop observing the button
    ob.unobserve(terms.lastElementChild)
  } 
}
```

Now we can create the Intersection Observer, this will watch if an element is on or off or partway on or off of the page.  
the way that we know is 100% visible on the page is by using the second argument can be an options object:  
first the **root** of what we are scrolling with by default is the body, in this case is terms, and the **threshold** we can give it an array like [0, 0.5, 1] where 0 means off,  0/5 means halfway on and 1 means totally on, for our case we only care when is totally on

```js
const ob = new IntersectionObserver(obCallBack, {
  root: terms,
  threshold: 1,
});
```

the intersection observer is going to take a callback (obCallBack in this case)  

>NOTE: a callback is a function that gets called at a certain point. Intersection observer is a callback that will be fired every single time that it needs to check if something is currently on the page, for more info you can visit [MDN](https://developer.mozilla.org/en-US/docs/Web/API/Intersection_Observer_API).

this still do anything until we told it to watch for any element, which in this case will be the terms.  
the way that we know that is the user scroll to the bottom is looking for the last element inside terms and conditions, which is the ```<hr>``` and we wait until the tag be 100% on the screen, for that we use ```lastElementChild```
```js
ob.observe(terms.lastElementChild);
```

<br>

<a name="tabs"></a> 
## **TABS**

>Example [here](https://codepen.io/cgope/pen/NWbBbpQ)

This example contains roles and aria labels in the HTML, this is important to make your tabs accessible and your content will be easly read by search engine.  
We will need the tabs, buttons and panels:
```js
const tabs = document.querySelector('.tabs');

const tabButtons = tabs.querySelectorAll('[role="tab"]');

//convert into an array to use the find method in the fuction by using Array.from
const tabPanels = Array.from (tabs.querySelectorAll('[role="tabpanel"]'));
```
for buttons (```tabButtons```) we are going to select from ```tabs``` looking for anything with the role of "tab" because you can have multiple tabs on the same page and this can be reused for any number of tabs.   
```tabPanels``` should be converted from a node list into an array in order to use the Find method to show the panels, how to will be explained at the end of this Module.

Then add the listener for each tab buttons:
```js
tabButtons.forEach(button => button.addEventListener('click',handleTabClick));
```

Now create the function to handle the click:
```js
function handleTabClick(event){
  //hide all tab panels
  tabPanels.forEach(panel => {
    panel.hidden = true;
  });
  //mark all tabs as unselected
  tabButtons.forEach(tab => {
    tab.setAttribute('aria-selected', false);
  });
  //mark the clicked tab as selected
  event.currentTarget.setAttribute('aria-selected', true);
  //find the associated tabPanel and show it!
  const id = event.currentTarget.id;
  
  /*Method 1
  const tabPanel = tabs.querySelector(`[aria-labelledby="${id}"]`);
  tabPanel.hidden = false;
  */
  
  //Method 2 - find method
  const tabPanel = tabPanels.find(panel => panel.getAttribute('aria-labelledby') === id);
  tabPanel.hidden = false;
}
```
When somebody click on a tab, we need to hide all of the other tab panels.  
After that we need to mark all tabs as unselected, the way we can do it its by using the ```setAttribute``` because its a custom propertie.  
then we need to mark the tab that user clicked as selected, and find the ID asossiated panel for the tab and show it, there are many ways to do it, this example contains 2 of them:  
The first one is by matching the aria-atributte from the panels with the ID of the tabs, if its a match then we can change the hidden to false.
```js
  const tabPanel = tabs.querySelector(`[aria-labelledby="${id}"]`);
  tabPanel.hidden = false;
```
The second option is by using the find method, we can loop into tabPanels until it finds the one that match if you want to use this method make sure that you turn the selected item as an array first:
```js
const tabPanels = Array.from (tabs.querySelectorAll('[role="tabpanel"]'));
```
after that you can take each panel and get the attirube from the aria lebel to match with the ID of the tab
```js
 const tabPanel = tabPanels.find(panel => panel.getAttribute('aria-labelledby') === id);
  tabPanel.hidden = false;
```



<br>

---
back to [Table of Content](tableOfContent.md)  
previous [Events](05_events.md)  
next [Logic and flow control](07_LogicAndFlowControl.md)