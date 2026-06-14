# React-JS
Contains all the concepts of react js

## Javascript Basics(map, filter, find, some, every, reduce)
### Map
    We use it to tranform the data like updating, updating at index
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
    //filter the cart if the quantity is less than 5
    let filteredCart = cart.filter((cartItem, key) => cartItem.quantity > 5)
    console.log(filteredCart);
    
    console.log("--------");
    
### Find(Gives first occurence of value)
    //find price of an item 20
    let findFirstItem = cart.find((cartItem)=>cartItem.price===10);
    let findAllItem = cart.filter((cartItem)=>cartItem.quantity===10);
    console.log(findFirstItem); //if not found returns undefined
    console.log(findAllItem);

### Some
    // Find if atleast one name exists
    let bottleName = cart.some((cartItem)=>cartItem.name==="bottle");
    console.log(bottleName); //Gives true or false
    if(bottleName){
        console.log("Bottle already exist");
    }

###
    

    
    
