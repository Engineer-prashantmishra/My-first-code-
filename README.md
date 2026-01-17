import React, { useState } from "react"; import { ShoppingCart, Plus, Minus } from "lucide-react"; import { Card, CardContent } from "@/components/ui/card"; import { Button } from "@/components/ui/button";

export default function ShopifyClone() { const products = [ { id: 1, name: "T-Shirt", price: 799 }, { id: 2, name: "Shoes", price: 2499 }, { id: 3, name: "Watch", price: 1599 }, ];

const [cart, setCart] = useState([]);

const addToCart = (product) => { setCart([...cart, product]); };

const removeFromCart = (id) => { setCart(cart.filter((item) => item.id !== id)); };

const total = cart.reduce((sum, item) => sum + item.price, 0);

return ( <div className="min-h-screen bg-gray-100 p-6"> <header className="flex justify-between items-center mb-8"> <h1 className="text-3xl font-bold">Shopify</h1> <div className="flex items-center gap-2"> <ShoppingCart /> <span>{cart.length}</span> </div> </header>

<div className="grid grid-cols-1 md:grid-cols-3 gap-6">
    {products.map((product) => (
      <Card key={product.id} className="rounded-2xl shadow">
        <CardContent className="p-4">
          <h2 className="text-xl font-semibold">{product.name}</h2>
          <p className="text-gray-600">₹ {product.price}</p>
          <Button
            className="mt-4 w-full"
            onClick={() => addToCart(product)}
          >
            Add to Cart
          </Button>
        </CardContent>
      </Card>
    ))
  </div>

  <div className="mt-10 bg-white p-6 rounded-2xl shadow">
    <h2 className="text-2xl font-bold mb-4">Cart</h2>
    {cart.length === 0 && <p>Your cart is empty</p>}
    {cart.map((item) => (
      <div key={item.id} className="flex justify-between mb-2">
        <span>{item.name}</span>
        <div className="flex gap-2 items-center">
          <span>₹ {item.price}</span>
          <Button size="icon" variant="destructive" onClick={() => removeFromCart(item.id)}>
            <Minus />
          </Button>
        </div>
      </div>
    ))}
    <hr className="my-4" />
    <h3 className="text-xl font-semibold">Total: ₹ {total}</h3>
  </div>
</div>

); }

