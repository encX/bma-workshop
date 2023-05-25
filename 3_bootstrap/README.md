# Chapter 3: React with Bootstrap

## Step 1: Install React Bootstrap
1. Type `Ctrl + C` in your terminal to terminate the website
2. Type `yarn add react-bootstrap bootstrap` and press `Enter`
3. Now your website should be able to use Bootstrap components

4. Add Bootstrap CSS to your website by adding the following line to the top of `App.tsx`
**Please make sure you import bootstrap.min.css before our style.css**

```diff
+ import 'bootstrap/dist/css/bootstrap.min.css';
  import './style.css';
```

## Step 2: Use a basic Bootstrap component in your website

### Step 2.1: Replace the old css with Bootstrap css

1. Replace the content of `style.css` with the following code, because we don't need any custom styles anymore

```css
html, body {
  background: #000;
  color: #e0e0e0;
}
```

### Step 2.2: Apply Bootstrap Grid Components to layout your website

#### App.tsx

1. Import `Container` from `react-bootstrap` by adding the following line to the top of `App.tsx`

```tsx
import { Container } from 'react-bootstrap';
```

2. Wrap your layout inside the responsive container

```diff
  function App() {
    return (
      <>
+       <Container>
          <h1>Quick Steam Store</h1>

          {games.map((game) => (
            <GameCard
              key={game.id}
              image={game.image}
              title={game.title}
              rating={game.rating}
              price={game.price}
            />
          ))}
+       </Container>
      </>
    );
  }
```

#### GameCard.tsx

1. Import `Row`, `Col` and `Button` from `react-bootstrap` by adding the following line to the top of `GameCard.tsx`

```tsx
import { Row, Col, Button } from 'react-bootstrap';
```

2. Replace the `div` with class `gamecard` with the following code

```diff
  const GameCard = (props: GameCardProps) => {
    const [isBought, setIsBought] = useState(false);
    return (
-     <div className={`gamecard ${isBought ? 'gamecard--bought' : ''}`}>
-       <div className="gamecard__image">
-         <img src={props.image} alt={props.title} />
-       </div>
-       <div className="gamecard__info">
-         <h2 className="gamecard__title">{props.title}</h2>
-         <h4 className="gamecard__rating">{props.rating} / 5</h4>
-         <div className="gamecard__price">${props.price}</div>
-         <div className="gamecard__button">
-           <button onClick={() => setIsBought(true)}>Buy</button>
-         </div>
-       </div>
-     </div>
+     <Row className={`${isBought ? 'bg-success' : 'bg-dark'}`}>
+       <Col>
+         <img src={props.image} alt={props.title} />
+       </Col>
+       <Col>
+         <h3>{props.title}</h3>
+         <div>{props.rating} / 5</div>
+         <h5>${props.price}</h5>
+         <div>
+           {!isBought &&
+             <Button variant="success" onClick={() => setIsBought(true)}>
+               Buy
+             </Button>
+           }
+         </div>
+       </Col>
+     </Row>
    );
  };
```

3. Now you should see your layout is as you think it should be, but something is still wrong  
Let's try replacing that bunch with the following code

```tsx
<Row className={`mt-2 mb-2 ${isBought ? 'bg-success' : 'bg-dark'}`}>
  <Col md={5} className="p-0">
    <img src={props.image} className="w-100 h-100" style={{ objectFit: 'cover' }} alt={props.title} />
  </Col>
  <Col md={7} className="pt-2 pb-2 d-flex flex-column">
    <h3 className="title">{props.title}</h3>
    <div className="rating">{props.rating} / 5</div>
    <h5 className="text-end align-items-end d-flex flex-row justify-content-end flex-grow-1">
      ${props.price}
    </h5>
    <div className="d-flex flex-row align-items-end justify-content-end">
      {!isBought &&
        <Button variant="success" size="lg" className="rounded-0" onClick={() => setIsBought(true)}>
          Buy
        </Button>
      }
    </div>
  </Col>
</Row>
```

---

## At the end of this section, your code should look like this:

`style.css`

```css
html, body {
  background: #000;
  color: #e0e0e0;
}
```

`GameCard.tsx`

```tsx
import { useState } from 'react';
import { Row, Col, Button } from 'react-bootstrap';

interface GameCardProps {
  title: string;
  rating: number;
  price: number;
  image: string;
}

const GameCard = (props: GameCardProps) => {
  const [isBought, setIsBought] = useState(false);
  return (
    <Row className={`mt-2 mb-2 ${isBought ? 'bg-success' : 'bg-dark'}`}>
      <Col md={5} className="p-0">
        <img src={props.image} className="w-100 h-100" style={{ objectFit: 'cover' }} alt={props.title} />
      </Col>
      <Col md={7} className="pt-2 pb-2 d-flex flex-column">
        <h3 className="title">{props.title}</h3>
        <div className="rating">{props.rating} / 5</div>
        <h5 className="text-end align-items-end d-flex flex-row justify-content-end flex-grow-1">
          ${props.price}
        </h5>
        <div className="d-flex flex-row align-items-end justify-content-end">
          {!isBought &&
            <Button variant="success" size="lg" className="rounded-0" onClick={() => setIsBought(true)}>
              Buy
            </Button>
          }
        </div>
      </Col>
    </Row>
  );
};

export default GameCard;
```

`App.tsx`

```tsx
import GameCard from './GameCard';
import 'bootstrap/dist/css/bootstrap.min.css';
import './style.css';
import { games } from './data';

function App() {
  return (
    <>
      <Container>
        <h1>Quick Steam Store</h1>

        {games.map((game) => (
          <GameCard
            key={game.id}
            image={game.image}
            title={game.title}
            rating={game.rating}
            price={game.price}
          />
        ))}
      </Container>
    </>
  );
}

export default App;
```