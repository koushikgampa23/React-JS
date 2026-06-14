# React-JS
Contains all the concepts of react js

## Javascript Basics(map, filter, find, some, every, reduce)
### Map
    We use it to tranform the data like updating, updating at index

    Basic
    let arr = [10,20,30,40]
    let doubledArr = arr.map((item, key)=> arr*2);
    
    let cart = [{"name": "bottle", "price": 1, "quantity":10}, {"name": "bottle", "price": 2, "quantity": 10}, {"name": "copper_bottle", "price": 10, "quantity":2}]
    console.log(cart);
    
    // Double price of all the items
    let newCart = cart.map((cartItem, key) => {
        return {...cartItem, price:cartItem.price*2}
    })
    console.log(newCart);
    
    // Double price at specific index
    index = 2
    let updatedCart = cart.map((cartItem, key)=> {
        if(index===key){
            return {...cartItem, price: cartItem.price*2}
        }
        return cartItem
    });
    
### Filter(gives values if the condition is true)
    //Basic
    let arr = [1,3,5,10,24,30]
    let filteredArr = arr.filter((item, key)=>item>5);

    //filter the cart if the quantity is less than 5
    let filteredCart = cart.filter((cartItem, key) => cartItem.quantity > 5)
    console.log(filteredCart);
    
    console.log("--------");
    
### Find(Gives first occurence of value)
    //Basic
    let ids = [10,20,30,40]
    let findId = ids.find((item)=>item===10);
    console.log(findId); //true

    //find price of an item 20
    let findFirstItem = cart.find((cartItem)=>cartItem.price===10);
    let findAllItem = cart.filter((cartItem)=>cartItem.quantity===10);
    console.log(findFirstItem); //if not found returns undefined
    console.log(findAllItem);

### Some
    //Basic
    let prices = [10,20,30,50]
    //all prices are valid if atleast one price is greater than 40
    let validPrices = prices.some((item)=> item>25);
    console.log(true); //since there are value like 30,50 > 25

    // Find if atleast one name exists
    let bottleName = cart.some((cartItem)=>cartItem.name==="bottle");
    console.log(bottleName); //Gives true or false
    if(bottleName){
        console.log("Bottle already exist");
    }

### Every
    // Check all the values are valid or not
    // Example quantity cannot be negative or zero
    let quantity = [-1, 0, 10, 50]
    let isQuantityValid = quantity.every((item) => item >= 1);
    console.log(false); //there are quantities like -1, 0 in it

    // all the quantities are correct?
    let areQuantityValid = cart.every((cartItem)=> cartItem.quantity >= 1);
    console.log(areQuantityValid);

### Calculate total
    let arr = [10,20,30]
    let total = arr.reduce((acc, currentValue)=>acc+currentValue, 0);
    console.log(total);
    
    // Total of the cart
    let totalCartValue = cart.reduce((sum, item) => sum + item.price*item.quantity, 0);
    console.log(totalCartValue);
    

    
    
