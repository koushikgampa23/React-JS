# React-JS
Contains all the concepts of react js

## Javascript Basics(map, filter, find, some, every, reduce, sort, search)
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

### Reduce
    let arr = [10,20,30]
    let total = arr.reduce((acc, currentValue)=>acc+currentValue, 0);
    console.log(total);
    
    // Total of the cart
    let totalCartValue = cart.reduce((sum, item) => sum + item.price*item.quantity, 0);
    console.log(totalCartValue);

### Sort
    let arr = [1,9,5,10,8]
    // arr.sort(); //This doesnot work since javascript treats everthing as string
    arr.sort((a,b) => b-a) //b-a desc, a-b asc
    console.log(arr);
    // Sort manuplates the original arr we need to use spread operator to temp copy and use it
    let sortedArr = [...arr].sort((a,b)=>b-a)
    console.log(sortedArr);
    console.log(arr);

    let names = ["krk","abc","xerox"]
    names.sort((a,b) => a.localeCompare(b))
    console.log(names);

    let sortedCart = [...cart].sort((a,b)=>a.name.localeCompare(b.name))
    console.log(sortedCart);

### Search
    let searchName = "bottle"
    let filteredResults = searchName ? cart.filter((cartItem) => cartItem.name.toLowerCase().includes(searchName.toLowerCase())) : cart;
    console.log(filteredResults);
    
### To master cart application need to learn this
    Basic: Add Product, Delete Product, Increase Quantity, Decrease Quantity
    Intermediate: 
        Calculate Cart Total using reduce()
        Show Number of Products
        Prevent Duplicate Products using some()
        Find Product by Name using find()
    Advanced: 
        Search Products 
        Sort by Price
        Sort by Name
        Filter Products by Price Range
        Edit Product
        Persist Cart in localStorage
### Cart Application that contains add product, delete product, edit, increase quantity, sort, filter, reduce, search
        "use client";

        import { useState } from "react";
        import {
        Button,
        Input,
        Stack,
        Typography,
        Alert,
        Table,
        TableBody,
        TableRow,
        TableCell,
        TableHead,
        } from "@mui/material";
        import SortIcon from "@mui/icons-material/Sort";

        export const CartPage = () => {
        const [productName, setProductName] = useState("");
        const [productQuantity, setProductQuantity] = useState(0);
        const [productPrice, setProductPrice] = useState(0);
        const [cart, setCart] = useState([]);
        const [totalAmount, setTotalAmount] = useState(0);
        const [error, setError] = useState(null);
        const [searchProduct, setSearchProduct] = useState("");
        const [edit, setEdit] = useState(null);

        const handleCart = () => {
            let isItemExists = cart.some(
            (cartItem) => cartItem.productName === productName,
            );
            if (isItemExists) {
            setError(`${productName} already exists`);
            return;
            }
            setCart((prevState) => [
            ...prevState,
            {
                id: crypto.randomUUID(),
                productName: productName,
                productQuantity: productQuantity,
                productPrice: productPrice,
            },
            ]);
            setProductName("");
            setProductPrice(0);
            setProductQuantity(0);
        };

        const handleIncreaseQuantity = (id) => {
            let updatedCart = cart.map((cartItem) => {
            if (cartItem.id === id) {
                return { ...cartItem, productQuantity: cartItem.productQuantity + 1 };
            } else {
                return cartItem;
            }
            });
            setCart(updatedCart);
        };

        const handleDecreaseQuantity = (id) => {
            let updatedCart = cart.map((cartItem) => {
            if (cartItem.id === id) {
                return { ...cartItem, productQuantity: cartItem.productQuantity - 1 };
            } else {
                return cartItem;
            }
            });
            setCart(updatedCart);
        };

        const handleDelete = (id) => {
            let updatedCart = cart.filter((cartItem) => cartItem.id !== id);
            setCart(updatedCart);
        };

        const handleBillingAmount = () => {
            let billingAmount = cart.reduce(
            (sum, item) => sum + item.productPrice * item.productQuantity,
            0,
            );
            setTotalAmount(billingAmount);
        };

        const sortBasedOnProductName = () => {
            let sortProductName = [...cart].sort((a, b) =>
            a.productName.localeCompare(b.productName),
            );
            setCart(sortProductName);
        };

        const sortBasedOnProductQuantity = () => {
            let sortProductQuantity = [...cart].sort(
            (a, b) => b.productQuantity - a.productQuantity,
            );
            setCart(sortProductQuantity);
        };

        const filteredCart = searchProduct
            ? cart.filter((cartItem) =>
                cartItem.productName
                .toLowerCase()
                .includes(searchProduct.toLocaleLowerCase()),
            )
            : cart;

        const handleProductEdit = (value, id) => {
            let updatedCart = cart.map((cartItem) => {
            if (cartItem.id === id) {
                return { ...cartItem, productName: value };
            }
            return cartItem;
            });
            setCart(updatedCart);
        };

        const handleGenericEdit = (value, field, id) => {
            let updatedCart = cart.map((cartItem) => {
            if (cartItem.id === id) {
                return { ...cartItem, [field]: value };
            }
            return cartItem;
            });
            setCart(updatedCart);
        };

        return (
            <Stack gap={4}>
            <Stack
                direction="row"
                gap={2}
                sx={{ justifyContent: "space-between", alignItems: "center" }}
            >
                <Input
                placeholder={"Product Name"}
                onChange={(e) => setProductName(e.target.value)}
                value={productName}
                />
                <Input
                placeholder="Product Quantity"
                onChange={(e) => setProductQuantity(parseInt(e.target.value))}
                value={parseInt(productQuantity)}
                />
                <Input
                type="number"
                placeholder="Product Price"
                onChange={(e) => setProductPrice(parseFloat(e.target.value))}
                value={parseFloat(productPrice)}
                />
                <Button variant="contained" onClick={handleCart}>
                Add Product to cart
                </Button>
            </Stack>
            <Typography variant="h5">Cart Items</Typography>
            <Input
                placeholder="Search product here"
                onChange={(e) => setSearchProduct(e.target.value)}
            />
            <Table>
                <TableHead>
                {filteredCart.length > 0 && (
                    <TableRow>
                    <TableCell>
                        Product Name
                        <SortIcon onClick={sortBasedOnProductName} />
                    </TableCell>
                    <TableCell>
                        Product Quantity{" "}
                        <SortIcon onClick={sortBasedOnProductQuantity} />
                    </TableCell>
                    <TableCell>Product Price</TableCell>
                    <TableCell>Controls</TableCell>
                    </TableRow>
                )}
                </TableHead>
                <TableBody>
                {filteredCart.length > 0 &&
                    filteredCart.map((cartItem) => (
                    <TableRow key={cartItem.id}>
                        <TableCell>
                        {edit && edit === cartItem.id ? (
                            <Input
                            value={cartItem.productName}
                            onChange={(e) =>
                                handleProductEdit(e.target.value, cartItem.id)
                            }
                            ></Input>
                        ) : (
                            cartItem.productName
                        )}
                        </TableCell>
                        <TableCell>{cartItem.productQuantity}</TableCell>
                        <TableCell>{cartItem.productPrice}</TableCell>
                        <TableCell>
                        {edit && edit === cartItem.id ? (
                            <Button onClick={() => setEdit(null)}>Done</Button>
                        ) : (
                            <Button onClick={() => setEdit(cartItem.id)}>Edit</Button>
                        )}
                        <Button onClick={() => handleIncreaseQuantity(cartItem.id)}>
                            +
                        </Button>
                        <Button onClick={() => handleDecreaseQuantity(cartItem.id)}>
                            -
                        </Button>
                        <Button onClick={() => handleDelete(cartItem.id)}>
                            Delete
                        </Button>
                        </TableCell>
                    </TableRow>
                    ))}
                </TableBody>
            </Table>
            <Stack direction={"row"} sx={{ alignItems: "center" }}>
                <Button onClick={handleBillingAmount}>Billing Amount</Button>
                <Typography variant="caption">{totalAmount}</Typography>
            </Stack>
            {error && <Alert severity="error">{error}</Alert>}
            </Stack>
        );
        };

    
    
