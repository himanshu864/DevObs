#react 

**reducer** simplifies complex useState.

```jsx
import { createContext, useReducer } from "react";

export const CartContext = createContext({
  items: [],
  addItemToCart: () => {},
  updateCartItemQuantity: () => {},
});

function cartReducer(state, action) {
  if (action.type == "ADD_ITEM") {
    //...
    return { items: updatedItems };
  }
  if (action.type == "UPDATE_ITEM") {
    //...
    return { items: updatedItems };
  }
  return state;
}

export default function CartContextProvider({ children }) {
  const [cartState, cartDispatch] = useReducer(cartReducer, {
    items: [],
  });

  function handleAddItemToCart(id) {
    cartDispatch({
      type: "ADD_ITEM",
      payload: id,
    });
  }

  function handleUpdateCartItemQuantity(productId, amount) {
    cartDispatch({
      type: "UPDATE_ITEM",
      payload: {
        productId,
        amount,
      },
    });
  }

  const ctxValue = {
    items: cartState.items,
    addItemToCart: handleAddItemToCart,
    updateCartItemQuantity: handleUpdateCartItemQuantity,
  };

  return (
    <CartContext.Provider value={ctxValue}>{children}</CartContext.Provider>
  );
}
```

- useReducer() takes in two parameters: A reducer function and an initial state value.
- And it returns two values inside an array: State and Dispatch
- We call dispatch with action as parameter. Which calls reducer function, which changes state as per action.
- Use can pass anything inside action, but typically contains type and payload.
- This way functions only call dispatch. And reducer handles state changes.
